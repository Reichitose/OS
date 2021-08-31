# x86 （80386）启动顺序

理解x86-32平台的启动过程

理解x86-32 的实模式 保护模式

理解段机制

## X86启动顺序 第一条指令

1. **寄存器初始值 CS = F000H, EIP = 0000FFF0H**

   cs是16位段寄存器，其中隐含一个base（基址）内容

   实际地址是

   Base + EIP = FFFF000H+0000FFF0H = FFFFFFF0H 

   这是BIOS 的EPRROM（Erasable Programmable Read Only Memory）的所在地

2. **当CS被新值加载，则地址转换规则开始起作用**

3. **通常第一条指令 是一条长跳转指令（这样CS和EIP都会更新）到BIOS代码中执行**

## X86启动顺序 处于实模式的段

段选择子（Segment Selector）：CS.DS.SS…

偏移量（Offset）：EIP 

base向左偏移四位构成20位的寻址方式

## X86启动顺序 从BIOS到Bootloader

BIOS加载存储设备上的 第一个扇区（主引导扇区MBR）的512字节到内存的0x7c00

然后跳转到0x7c00的第一条指令开始执行

零号扇区中就是BootLoader



## X86启动顺序 从BootLoader到OS

Bootloader做的事情

使能（enable）保护模式（protection）和段机制（segment-level protection）

从实模式切换到保护模式 从16位的寻址空间切换到32位寻址空间，1m的寻址切换成4g寻址

从硬盘中读取kernel in ELF格式的ucore kernel （跟在MBR之后的扇区）并放入内存的指定位置

跳转到ucore OS的入口点（entry point）执行，此时控制权到了ucore OS中

## X86启动顺序 段机制

## X86启动顺序 使能保护机制

## X86启动顺序 加载ELF格式的ucore OS kernel



