#上传spx包的命令
```
./svnspx --spxconfig-file=./spxconfig-tpl --ci /home/liyongcheng/sprint-dev/sprint18/Project/SugonBase/new-uboot-spx/Bootloader_amiext_ex-2.47.0-src.spx --force-commit --non-interactive
```

#spx包命令

打开AMI spx包命令
```
python /usr/mds-4.0.1/spx/utils/PackSPX.py -x packagesname.spx outputdirname
```
打包source为AMI spx包命令
```
python /usr/mds-4.0.1/spx/utils/PackSPX.py -c sourcedirname packagesname.spx
```

#Java设置

JAVA环境配置安全等级    /usr/lib/jvm/jdk1.8.0_20/bin/ControlPanel

