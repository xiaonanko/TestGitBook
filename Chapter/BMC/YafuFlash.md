#编译YafuFlash工具的方法

MDS中修改存放在MDS安装目录下的workspace/software/yafuflash-x.x.x-ANY,编译用到的source存放在development/software/yafuflash-x.x.x-ANY

1.Yafulash编译过程中会出现MAX_NAME_LEN未定义的问题，在workspace/software/yafuflash-x.x.x-ANY/Commom/Include/main.h中添加宏定义#define MAX_NAME_LEN    256

2.编译过程中会出现IDBG_LINUXAPP_AuditOut无法连接的问题，需要在libipmi/libipmi_AMIOEM.c文件中注释掉出现TAUDIT的两行，目前是3782和3786行

3.正常编译会缺少相关依赖的库和文件，需要进入workspace/software/libipmi_sw-x.x.x-ANY/Linux目录下执行sudo make clean, sudo make all, sudo make install

这样就能在workspace/software目录下编译出相关的库文件

4.这个时候再进入workspace/software/yafuflash-x.x.x-ANY/目录下相关平台的目录中，执行sudo make clean, sudo make all

编译成功就可以在 workspace/software/yafuflash-x.x.x-ANY/obj目录中产生二进制文件


#YafuFlash刷新BMC

./Yafuflash -nw -ip BMCIP -u USER -p PASSWORD -force-boot BMC.ima

加入-force-boot能够不用输入y
