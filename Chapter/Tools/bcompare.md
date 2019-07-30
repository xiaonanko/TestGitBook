# Beyond Compare 3 安装

DEBIAN, UBUNTU

Beyond Compare 4.1 and newer require matching package and OS architecture (amd64.deb or i386.deb).  Beyond Compare 3 - 4.0.7 require the i386.deb package on all supported versions of Debian and Ubuntu (32-bit and 64-bit).

Beyond Compare 3 on Debian 7, 8 64-bit

Enable 32-bit architecture support:``` sudo dpkg --add-architecture i386 ```

Graphical Install
Double click on the .deb package to install using the graphical package manager.

Terminal Install
```
sudo apt-get update
sudo apt-get install gdebi
sudo gdebi bcompare-4.1.6.21095_amd64.deb
```

Terminal Uninstall
```
sudo apt-get remove bcompare
```

# Beyond Compare 3 注册

[Ubuntu 14.04安装Beyond Compare 3方法](https://blog.csdn.net/u014113463/article/details/80661191)

注册码
```
HmB5oANygQOhaStTHNa+zOKgOeWHOkeAp6d1+QwIebz6z9kwYCm9-O0jF9F79zvzed9v5UVC4VrDkDMmTM8nB+
```


#Beyond Comapre 4 破解方法

主机环境：ubuntu14.04LTS

软件环境：bcompare-4.1.6.21095_amd64.deb

辅助软件：wxhexeditor（可用```sudo apt-get install wxhexeditor```安装，不用可卸载）

网址：[破解方法网址](http://blog.163.com/yesaidu@126/blog/static/518193072015814101859418/)

Beyond Compare是一个非常强大的文件/文件夹比较工具，它支持Windows、Mac和Linux下运行；它是一个商业软件，需要付费才能长期使用它。如果你喜欢它，建议购买它。

安装后，备份/usr/lib/beyondcompare/BCompare，

这里用wxhexeditor编辑之前需要将该文件赋予写权限

用VIM+xxd或者MadEdit或者wxhexeditor打开这个文件，编辑替换如下地址的内容：
```
offset start: 0x00162233
offset end:  0x00162387
size: 0x155
```
好像上边的地址和偏移没什么用，直接用下边的查找就可以

下面两种查找方式使用任意一种就可以

使用字符串查找替换如下：

查找串：
```
keexjEP3t4Mue23hrnuPtY4TdcsqNiJL-5174TsUdLmJSIXKfG2NGPwBL6vnRPddT7tH29qpkneX63DO9ECSPE9rzY1zhThHERg8lHM9IBFT+rVuiY823aQJuqzxCKIE1bcDqM4wgW01FH6oCBP1G4ub01xmb4BGSUG6ZrjxWHJyNLyIlGvOhoY2HAYzEtzYGwxFZn2JZ66o4RONkXjX0DF9EzsdUef3UAS+JQ+fCYReLawdjEe6tXCv88GKaaPKWxCeaUL9PejICQgRQOLGOZtZQkLgAelrOtehxz5ANOOqCaJgy2mJLQVLM5SJ9Dli909c5ybvEhVmIC0dc9dWH
```
替换为：
```
N9KmiLVlKMU7RJqnE+WXEEPI1SgglmfmLc1yVH7dqBb9ehOoKG9UE+HAE1YvH1XX2XVGeEqYUY-Tsk7YBTz0WpSpoYyPgx6Iki5KLtQ5G-aKP9eysnkuOAkrvHU8bLbGtZteGwJarev03PhfCioJL4OSqsmQGEvDbHFEbNl1qJtdwEriR+VNZts9vNNLk7UGfeNwIiqpxjk4Mn09nmSd8FhM4ifvcaIbNCRoMPGl6KU12iseSe+w+1kFsLhX+OhQM8WXcWV10cGqBzQE9OqOLUcg9n0krrR3KrohstS9smTwEx9olyLYppvC0p5i7dAx2deWvM1ZxKNs0BvcXGukR
```

使用十六进制查找替换如下：
查找：
```
6B 65 65 78 6A 45 50 33 74 34 4D 75 65 32 33 68 72 6E 75 50 74 59 34 54 64 63 73 71 4E 69 4A 4C 2D 35 31 37 34 54 73 55 64 4C 6D 4A 53 49 58 4B 66 47 32 4E 47 50 77 42 4C 36 76 6E 52 50 64 64 54 37 74 48 32 39 71 70 6B 6E 65 58 36 33 44 4F 39 45 43 53 50 45 39 72 7A 59 31 7A 68 54 68 48 45 52 67 38 6C 48 4D 39 49 42 46 54 2B 72 56 75 69 59 38 32 33 61 51 4A 75 71 7A 78 43 4B 49 45 31 62 63 44 71 4D 34 77 67 57 30 31 46 48 36 6F 43 42 50 31 47 34 75 62 30 31 78 6D 62 34 42 47 53 55 47 36 5A 72 6A 78 57 48 4A 79 4E 4C 79 49 6C 47 76 4F 68 6F 59 32 48 41 59 7A 45
74 7A 59 47 77 78 46 5A 6E 32 4A 5A 36 36 6F 34 52 4F 4E 6B 58 6A 58 30 44 46 39 45 7A 73 64 55 65 66 33 55 41 53 2B 4A 51 2B 66 43 59 52 65 4C 61 77 64 6A 45 65 36 74 58 43 76 38 38 47 4B 61 61 50 4B 57 78 43 65 61 55 4C 39 50 65 6A 49 43 51 67 52 51 4F 4C 47 4F 5A 74 5A 51 6B 4C 67 41 65 6C 72 4F 74 65 68 78 7A 35 41 4E 4F 4F 71 43 61 4A 67 79 32 6D 4A 4C 51 56 4C 4D 35 53 4A 39 44 6C 69 39 30 39 63
35 79 62 76 45 68 56 6D 49 43 30 64 63 39 64 57 48
```
替换为：
```
4E 39 4B 6D 69 4C 56 6C 4B 4D 55 37 52 4A 71 6E 45 2B 57 58 45 45 50 49 31 53 67 67 6C 6D 66 6D 4C 63 31 79 56 48 37 64 71 42 62 39 65 68 4F 6F 4B 47 39 55 45 2B 48 41 45 31 59 76 48 31 58 58 32 58 56 47 65 45 71 59 55 59 2D 54 73 6B 37 59 42 54 7A 30 57 70 53 70 6F 59 79 50 67 78 36 49 6B 69 35 4B 4C 74 51 35 47 2D 61 4B 50 39 65 79 73 6E 6B 75 4F 41 6B 72 76 48 55 38 62 4C 62 47 74 5A 74 65 47 77 4A 61 72 65 76 30 33 50 68 66 43 69 6F 4A 4C 34 4F 53 71 73 6D 51 47 45 76 44 62 48 46 45 62 4E 6C 31 71 4A 74 64 77 45 72 69 52 2B 56 4E 5A 74 73 39 76 4E 4E 4C 6B 37 55 47 66 65 4E 77 49 69 71 70 78 6A 6B 34 4D 6E 30 39 6E 6D 53 64 38 46 68 4D 34 69 66 76 63 61 49 62 4E 43 52 6F 4D 50 47 6C 36 4B 55 31 32 69 73 65 53 65 2B 77 2B 31 6B 46 73 4C 68 58 2B 4F 68 51 4D 38 57 58 63 57 56 31 30 63 47 71 42 7A 51 45 39 4F 71 4F 4C 55 63 67 39 6E 30 6B 72 72 52 33 4B 72 6F 68 73 74 53 39 73 6D 54 77 45 78 39 6F 6C 79 4C 59 70 70 76 43 30 70 35 69 37 64 41 78 32 64 65 57 76 4D 31 5A 78 4B 4E 73 30 42 76 63 58 47 75 6B 52
```

最后，使用如下注册码即可注册成功：
```
--- BEGIN LICENSE KEY ---
gCh0q+aTeOSxkmHm+dJdnNW+BX0mvx3Bi09VC9mSmGhN3I6qxcnk8QBLjq3Xl7A3iXCPncqflD9CXI+LONqH-Mnqe4DHXwQ7dHPvON0nqztC0hVH9Ynd8PCW0G2eN9PKiptFjaxxzulLqScDMmcR5BCx2bHes-kfzybCvhhv8yEDivZcUQACxYYWwcA49DCQOoDzwDXGJKZ7YwkZWgJfGzGSaxT546hP-5phfMQF5DHq47oGBtlmpyRu5P-taBJa+txla5fyl8w9+BcB4b9FvnooVzNohzbzbgDc6g0ABh4xVfGwNc+bj1obl6h3C5+FmCRffmqaRXnq108oYakpL+++
--- END LICENSE KEY -----
```

#Beyond Compare 4 过期后处理方法

[过期后处理方法网址](https://blog.csdn.net/croop520/article/details/84140922)

错误提示：This license key has been revoked xxxxx

Windows 系统：

解决方法：

删除以下目录中的所有文件即可。

C:\Users\Administrator\AppData\Roaming\Scooter Software\Beyond Compare 4

Linux系统：

解决方法：

1.删除下面目录中的所有文件：
```
/home/xxx/.config/bcompare
```
2.重新破解
```
$cd /usr/lib/beyondcompare/

$sudo sed -i "s/keexjEP3t4Mue23hrnuPtY4TdcsqNiJL-5174TsUdLmJSIXKfG2NGPwBL6vnRPddT7tH29qpkneX63DO9ECSPE9rzY1zhThHERg8lHM9IBFT+rVuiY823aQJuqzxCKIE1bcDqM4wgW01FH6oCBP1G4ub01xmb4BGSUG6ZrjxWHJyNLyIlGvOhoY2HAYzEtzYGwxFZn2JZ66o4RONkXjX0DF9EzsdUef3UAS+JQ+fCYReLawdjEe6tXCv88GKaaPKWxCeaUL9PejICQgRQOLGOZtZQkLgAelrOtehxz5ANOOqCaJgy2mJLQVLM5SJ9Dli909c5ybvEhVmIC0dc9dWH+/N9KmiLVlKMU7RJqnE+WXEEPI1SgglmfmLc1yVH7dqBb9ehOoKG9UE+HAE1YvH1XX2XVGeEqYUY-Tsk7YBTz0WpSpoYyPgx6Iki5KLtQ5G-aKP9eysnkuOAkrvHU8bLbGtZteGwJarev03PhfCioJL4OSqsmQGEvDbHFEbNl1qJtdwEriR+VNZts9vNNLk7UGfeNwIiqpxjk4Mn09nmSd8FhM4ifvcaIbNCRoMPGl6KU12iseSe+w+1kFsLhX+OhQM8WXcWV10cGqBzQE9OqOLUcg9n0krrR3KrohstS9smTwEx9olyLYppvC0p5i7dAx2deWvM1ZxKNs0BvcXGukR+/g" BCompare
```

3.此时BCompare文件已被破解，打开软件会提示“Trial Mode Error！”表示成功，输入下面TEAM ZWT生成的密钥即可注册成功
```
--- BEGIN LICENSE KEY ---
GXN1eh9FbDiX1ACdd7XKMV7hL7x0ClBJLUJ-zFfKofjaj2yxE53xauIfkqZ8FoLpcZ0Ux6McTyNmODDSvSIHLYhg1QkTxjCeSCk6ARz0ABJcnUmd3dZYJNWFyJun14rmGByRnVPL49QH+Rs0kjRGKCB-cb8IT4Gf0Ue9WMQ1A6t31MO9jmjoYUeoUmbeAQSofvuK8GN1rLRv7WXfUJ0uyvYlGLqzq1ZoJAJDyo0Kdr4ThF-IXcv2cxVyWVW1SaMq8GFosDEGThnY7C-SgNXW30jqAOgiRjKKRX9RuNeDMFqgP2cuf0NMvyMrMScnM1ZyiAaJJtzbxqN5hZOMClUTE+++
--- END LICENSE KEY -----
```
