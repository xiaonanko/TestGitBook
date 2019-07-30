# Sensor Initialization与Sensor Capabilities

主要用于Sensor的初始化和表现

Sensor Initialization通常设置为0x77

```
[7] - reserved. Write as 0b.
[6] - Init Scanning
        1b = enable scanning (this bit=1b implies that the sensor accepts the ‘enable/disable scanning’ bit in the Set Sensor Event Enable command).
        开启扫描模式，受到Set Sensor Event Enable命令中的enable/disable scanning位的影响
[5] - Init Events
        1b = enable events (per Sensor Event Message Control Support bits in Sensor Capabilities field, and per the Event Mask fields)
        开启记录SEL功能
[4] - reserved.    Write as 0b.
[3] - Init Hysteresis
        1b = initialize sensor hysteresis (per Sensor Hysteresis Support bits in the Sensor Capabilities field)
        还不清楚，好像和Capabilities有关
[2] - Init Sensor Type 1b = initialize Sensor Type and Event / Reading Type code
        初始化Sensor Type和Event / Reading Type code

Sensor Default (power up) State
Reports how this sensor comes up on device power up and hardware/cold reset.
The Initialization Agent does not use this bit. This bit solely reports to software how the sensor comes prior to being initialized by the Initialization Agent.
[1] - 0b = event generation disabled, 1b = event generation enabled
[0] - 0b = sensor scanning disabled, 1b = sensor scanning enabled
```

Sensor Capabilities通常设置为0x40
```
[7] - 1b = ignore sensor if Entity is not present or disabled.
      0b = don’t ignore sensor.

Sensor Auto Re-arm Support
Indicates whether the sensor requires manual rearming, or automatically rearms itself when the event clears. ‘manual’ implies that the get sensor event status and rearm sensor events commands are supported
[6] - 0b = no (manual), 1b = yes (auto)

Sensor Hysteresis Support
[5:4] - 00b = No hysteresis, or hysteresis built-in but not specified.
        01b = hysteresis is readable.
        10b = hysteresis is readable and settable.
        11b = Fixed, unreadable, hysteresis. Hysteresis fields values implemented in the sensor.

Sensor Threshold Access Support
[3:2] - 00b = no thresholds.
        01b = thresholds are readable, per Reading Mask, below.
        10b = reserved
        11b = Fixed, unreadable, thresholds. Which thresholds are supported is reflected by the Reading Mask. The threshold value fields report
the values that are ‘hard-coded’ in the sensor.

Sensor Event Message Control Support
Indicates whether this sensor generates Event Messages, and if so, what type of Event Message control is offered.
[1:0] - 00b = per threshold/discrete-state event enable/disable control (implies that entire sensor and global disable are also supported)
        01b = entire sensor only (implies that global disable is also supported)
        10b = global disable only
        11b = no events from sensor    设置了这一项就不会产生任何SEL
```


#Assert & Deassert

典型设置值0x7015,0x7a95

0x7015    只有Lower的方式记日志，Upper的方式不记日志

0x7a95    超过高的还有低的都记日志

```
[15]    reserved    write 0
[14]    write 0
[13]    write 0
[12]    write 0
[11]    assertion for upper non-recoverable going high supported    超过UNR
[10]    assertion for upper non-recoverable going low supported     低于UNR
[09]    assertion for upper critical going high supported           超过UC
[08]    assertion for upper critical going low supported            低于UC
[07]    assertion for upper non-critical going high supported       超过UNC
[06]    assertion for upper non-critical going low supported        低于UNC
[05]    assertion for lower non-recoverable going high supported    超过LNR
[04]    assertion for lower non-recoverable going low supported     低于LNR
[03]    assertion for lower critical going high supported           超过LC
[02]    assertion for lower critical going low supported            低于LC
[01]    assertion for lower non-critical going high supported       超过LNC
[00]    assertion for lower non-critical going low supported        低于LNC
```

