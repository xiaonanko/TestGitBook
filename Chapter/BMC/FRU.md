# FRU简介

FRU的初始化是作为一个sensor，在libipmimsghndlr/Sensor.c中的506行,有关FRU的设置宏定义存放在ipmipdk_dev/PDKFRU.h中，主要是FRU的类型和FRU的大小

#刷写FRU中的某个部分

单独修改FRU的一项内容
```
ipmitool -I lanplus -H xx.xx.xx.xx -U admin -P admin fru edit <fruid> field <section> <index> <string> - edit FRU string
```
Example:
```
ipmitool -I lanplus -H 10.0.22.95 -U admin -P admin fru edit 0 field p 0x00 Sugon
```

p for Product Area    c for Chassis Area    b for Board Area

所使用到的编号就是fru list的结果，从0x00开始排序,后边接的是要修改的字符串或者数字


#FRU报错的一种原因

FRU这个sensor的Modify Type要设置成0x02,否则ipmitool fru会在echo $?时候会报错误1


