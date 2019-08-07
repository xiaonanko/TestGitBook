#使用SIT的PreTest工具方法

环境相关信息：

ip:10.0.27.98

username:root

password:password

pwd:/root/sugonPreTest

需要将准备测试的镜像放在Date文件中，并重新命名为bmc.ima

command:

python Main.py -D 10.0.22.88 -S 10.0.22.22 -N bmc.ima -F 3.72

python Main.py -D 10.0.22.51 -S 10.0.22.92 -N bmc.ima -F 3.72
