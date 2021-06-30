## 硬软件信息
Dell.OptiPlex.7080-OpenCore.0.7.0-macOS.Big.Sur.11.4

|   条目    |                                         内容                                         |
| -------- | ----------------------------------------------------------------------------------- |
| Model    | Dell OptiPlex 7080                                                                  |
| CPU      | Intel(R) Core(TM) i7-10700 CPU @ 2.90GHz                                            |
| GPU      | Intel(R) UHD Graphics 630    /    测试RX590免驱                                      |
| NetCard  | Intel(R) Ethernet Connection (11) I219-LM                                           |
| Audio    | ALC256                                                                              |
| Disk     | Micron 2300 NVMe 512GB                                                              |
| OpenCore | OpenCore 0.6.9 Debug                                                                |
| Dmg      | Install.macOS.Big.Sur.11.4(20F71).with.OpenCore.0.6.9.and.Clover.r5135.and.WEPE.dmg |



## 工作情况
- 正常工作
    - 网卡正常，通过更换驱动实现WOL唤醒功能（停电后网启失效，正常关机不影响）
    - 显卡UHD630正常，显存正常，DP输出正常
    - 独显RX590免驱，多显正常
    - 系统安装时，建议采用集显DP，如安装A卡可能进系统黑屏（例如独显RX5700），考虑添加启动参数`agdpmod=pikera`
    - USB可用，已进行USB端口定制
    - 声卡输出问题已解决
    - iPad连接正常，使用`brew install svn` 安装好svn 工具
- 不正常工作
    - 集显仅支持DP输出，测试2k显示器无异常，测试DP转HDMI无法输出，*DP to HDMI必须是主动式转换的，被动转换、便宜的转接头会直接黑屏*

## Dell主机BIOS配置
### BIOS设置
- General → Advanced Boot Options：全部取消勾选
- System Configuration → SATA Operation：勾选AHCI
- Secure Boot → Secure Boot Enable：取消勾选
- Intel® Software Guard Extensions™ → Intel® SGX™ Enable：选择Disabled
- Power Management → Block Sleep：一般不勾选，否则不能进入深度睡眠，深度睡眠影响可切换
- Virtualization Support → VT for Direct I/O：取消勾选
### 改DVMT 64M和关闭CFG
（必须修改）参数，需要自行查看这两个值：
- DVMT to 64M：`setup_var 0x??? 0x02`
- Disable CFG lock：`setup_var 0x??? 0x00`

各机型键值

- Dell OptiPlex 7050
    - DVMT to 64M：`setup_var 0x795 0x02`
    - Disable CFG lock：`setup_var 0x4ED 0x00`
- Dell OptiPlex 7060
    - DVMT to 64M：`setup_var 0x8DC 0x02`
    - Disable CFG lock：`setup_var 0x5BE 0x00`
- Dell OptiPlex 7080、Dell ChengMing 3991
    - DVMT to 64M：`setup_var 0xF5 0x02`
    - Disable CFG lock：`setup_var 0x3E 0x00`
