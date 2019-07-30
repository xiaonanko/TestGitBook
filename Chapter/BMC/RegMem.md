#BMC寄存器

读取BMC寄存器设置的指令，BMC下使用如下指令

```
devmem address    eg:devmem 0x1e6e2070
regmemapp         eg:regmemapp -r -a 0x1e6e2070 -l 0x04    最好参照help信息，部分高地址会读不到
```
