# 编译Storelib库

storelib的修改内容(SAS卡部分)：

1.需要修改slcommon.c中i2c的库文件名以及通信的函数名称，原始为slir3_bmc_i2c.so、master_write_on_bus、writeread_on_bus，需要改为/usr/local/lib/libi2c.so、i2c_master_write_on_bus、i2c_writeread_on_bus

2.不能修改slinternal.h中规定的debug使用的目录文件名称，必须保持slit3combo_bmc_conf.ini、slit3combo_bmc_debug.txt，如果需要修改目录可以按照如下的方法修改，修改sllinux.h中的SL_LINUX_DBG_FILE_PATH宏定义修改为"/var/log"，然后在挂在的ini文件中修改DEBUGDIR=/var/log,可以达到同样的修改debug日志路径的目的

3.需要将slinternal.h中的DEFAULT_I2C_BMC_I2C_ADDRESS改为5

4.需要切换slMCTP.h中i2c的完整性验证为FALSE，SL_INTEGRITY_CHECK SL_FALSE

5.需要修改transpI2CMsg.h中的宏定义修改为#define DEFAULT_I2C_MAX_WRITE_SIZE      64，   #define DEFAULT_I2C_MAX_READ_SIZE       64，   #define DEFAULT_I2C_MAX_READWRITE_SIZE  36，同时需要修改ini_conf文件中对应的三个宏定义


#硬盘状态

存储系统的硬盘有一个状态叫做Foreign，该状态表示这个硬盘在其他的Raid卡上做过Raid，但是又更换了控制器,可以用如下指令清空该状态
```
/opt/MegaRAID/storcli/storcli64 /c0 /fall del
```

#SIGPIPE信号

产生SIGPIPE信号的问题研究

产生原因：对于一个PIPE或者FIFO的写操作，如果是以非阻塞方式只写方式(O_WRONLY)打开的管道，在读端关闭以后，如果还向管道中写数据，则会产生SIGPIPE的信息

避免方式：在PIPE或者FIFO写端打开的时候，指定打开的权限为读写方式(O_WRRD)，这样即使关闭了读端的管道，写数据仍然不会出现SIGPIPE，但是可能造成数据的错位
