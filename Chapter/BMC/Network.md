#修改Dedicated Lan网口灯闪烁模式

文件：linux/drivers/net/ethernet/aspeed/ast_ether.c

第239行添加如下代码
```
 //Set the PHY  LED  to the right Mode
 ast_ether_phy_write_register(dev,  priv->phy_addr, 31, 0x0d04);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 31, 0x0d04);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 0x10, 0x091b);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 0x10, 0x091b);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 31, 0x0000);

 //Close  Default EEE  Mode
 ast_ether_phy_write_register(dev,  priv->phy_addr, 31, 0x0d04);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 0x11, 0x0000);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 0x11, 0x0000);
 ast_ether_phy_write_register(dev,  priv->phy_addr, 31, 0x0000);
```

#修改MAC保存到EEPROM相关配置

文件：Bootloader_ex/spx/DEFCONFIG

最下方修改
```
/* I2C EEPROM (AT24C128) configuration */
#define CONFIG_I2C_CHANNEL_ID			CONFIG_SPX_FEATURE_GLOBAL_UBOOT_ENABLE_I2C_BUS
#define CONFIG_SYS_EEPROM_ADDR			0x50
#define	CONFIG_SYS_I2C_EEPROM_ADDR_LEN	2   

/* Network Configuration */
#define CONFIG_MACADDR_IN_EEPROM
#define CONFIG_CMD_EEPROM 				0
#define CONFIG_EEPROM_MACADDR_OFFSET	0x0f00
#define CONFIG_EEPROM_MAC1ADDR_OFFSET	0x0f08
```

#修改心跳灯软件模式

文件：uboot/arch/arm/cpu/astcommon/interrupts.c

注释掉50行开始的一部分代码
```
+	/* Enable Software blinking mode */
+	*(UINT32 *)(HW_HEART_BEAT_STATUS_REG) = ((*(UINT32 *)(HW_HEART_BEAT_STATUS_REG)) & 0xffffffef) | (1 << 4);
+	*(UINT32 *)(HEART_BEAT_LED_OUTPUT_REG) = 0x01;
```

#BMC获取IP

使用BMC重新获取DHCP IP的命令
```
udhcp -b -i eth0 -p /var/run/udhcpc.pid -R    添加-R能够使得dhcp server重新分配ip
```

#Package ID

板载网卡的package ID为1，OCP-A网卡的package ID为0 

#Ping操作

指定网卡进行ping操作    ping -I eth1 10.0.22.54

#白名单

清理白名单设置的指令    iptables  -D INPUT -j DROP

#端口测试

可以用以下命令进行端口是否开启的测试：
```
sudo traceroute -n -T -p port HostIP
```
全部是*表示端口没有开启，如果能找到地址，说明端口已经开启


#关闭与开启SSH服务

IPMITOOL关闭ssh服务
```
ipmitool -I lanplus -H 10.0.22.88 -U admin -P admin raw 0x32 0x6A 0x20 0x00 0x00 0x00 0x00 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x00 0xff 0xff 0xff 0xff 0x16 0x00 0x00 0x00 0x58 0x02 0x00 0x00 0xff 0x00
```
IPMITOOL开启ssh服务
```
ipmitool -I lanplus -H 10.0.22.88 -U admin -P admin raw 0x32 0x6A 0x20 0x00 0x00 0x00 0x01 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x46 0x00 0xff 0xff 0xff 0xff 0x16 0x00 0x00 0x00 0x58 0x02 0x00 0x00 0xff 0x00
```


