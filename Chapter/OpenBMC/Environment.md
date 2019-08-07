# Sugon OpenBMC下载与编译

第一步：克隆库文件
```
git clone  git@10.0.27.57:/home/git/openbmc-sugon.git
```

密码：111

第二步：配置环境

建议使用一个干净的环境，防止出现库依赖的相关问题

```
sudo apt-get install -y git build-essential libsdl1.2-dev texinfo gawk chrpath diffstat
```

[参考连接](https://github.com/openbmc/openbmc)


第三步：编译

可以查看git目录下的howtouse

第一次编译的过程会很漫长，后续会加快

```
export TEMPLATECONF=meta-sugon/meta-demoboard/conf
source openbmc-env
bitbake obmc-phosphor-image
```

成功后会在openbmc-sugon/build/tmp/deploy/images/demoboard目录下看到一个文件
```
obmc-phosphor-image-demoboard-20190807031140.static.mtd
```

该文件名会随着编译的时间与工程名称改变
