# crontab中date命令

crontab中的date命令使用的坑

1、习惯上的`date +"%Y%m%d_%H:%M"` 和 $(date +"%Y%m%d_%H:%M")在crontab下不起作用，需采用如下形式 `date +"\%Y\%m\%d_\%H:\%M"` 和 $(date +"\%Y\%m\%d_\%H:\%M")

2、直接在crontab里以sudo执行命令无效，会提示 sudo: sorry, you must have a tty to run sudo .需要修改/etc/sudoers，执行visudo或者vim /etc/sudoers 将"Defaults  requiretty"这一行注释掉。因为sudo默认需要tty终端，而crontab里的命令实际是以无tty形式执行的。注释掉"Defaults  requiretty"即允许以无终端方式执行sudo

