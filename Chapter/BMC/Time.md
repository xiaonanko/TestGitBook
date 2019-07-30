#通过IPMITOOL设置BMC时间

ipmitool设置BMC时间的时候会根据系统的时间设置一个带有时区的时间戳给BMC，同时BMC中会将时区设为0，导致后续时间的错误，为了减少此类问题的影响，ipmitool设置BMC时间的时候应该遵循下方的过程

1.ipmitool设置时间的时候应该在正确的localtime基础上减去一个时区时间

2.ipmitool设置完时间后一定要再次设置时区

example:设置时间为2018/01/15 17:00:00

```
1.ipmitool -I lanplus -H 10.0.22.31 -U admin -P admin sel time set "01/15/2017 09:00:00"    //在17点的基础上减去当前时区8小时
2.ipmitool -I lanplus -H 10.0.22.31 -U admin -P admin raw 0x0a 0x5d 0xe0 0x01               //设置时区为8小时(480分钟)
3.ipmitool -I lanplus -H 10.0.22.31 -U admin -P admin sel time get                          //返回时间为    01/15/2017 18:00:32
```
