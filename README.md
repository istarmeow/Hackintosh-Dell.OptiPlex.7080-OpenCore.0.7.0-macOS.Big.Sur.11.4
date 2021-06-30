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
