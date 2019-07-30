#使用ipmitool设置用户

1.设置用户名
```
    ipmitool -I lanplus -H -U -P user set name (user number) (user name)
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin user set name 0x03 sugon
```
2.设置用户密码
```
    ipmitool -I lanplus -H -U -P user set password (user number) (user password)
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin user set password 0x03 11111111
```
3.设置用户权限
```
    ipmitool -I lanplus -H -U -P user priv (user number) (user priv) (channel number)    channel number user 1 or 8
    ipmitool -I lanplus -H -U -P raw 0x06 0x43 (channel number) (user number) (user priv)    raw command
    channel number: channel 1 0xb1 channel 8 0xb8
    注意:当使用bond的时候只设置channel 1的权限就可以，当使用非bond的时候，必须channel 1和8同时设置
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin user priv 0x03 0x04 0x01
       ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin user priv 0x03 0x04 0x08
       ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin raw 0x06 0x43 0xb1 0x03 0x04
       ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin raw 0x06 0x43 0xb8 0x03 0x04
```
4.使能用户
```
    ipmitool -I lanplus -H -U -P user enable (user number)
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin user enable 0x03
```
5.设置用户拓展权限
```
    ipmitool -I lanplus -H -U -P raw 0x32 0xa3 (user number) 0x03 0x00 0x00 0x00
    ipmitool -I lanplus -H -U -P raw 0x32 0x7d (user number) 0x01 0x02 0x01 0x01
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin raw 0x32 0xa3 0x03 0x03 0x00 0x00 0x00
    ex:ipmitool -I lanplus -H 10.0.22.80 -U admin -P admin raw 0x32 0x7d 0x03 0x01 0x02 0x01 0x01
```
