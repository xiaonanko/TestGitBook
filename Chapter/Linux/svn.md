# svn取消修改

取消对代码的修改分为两种情况：

第一种情况：改动没有被提交（commit）

这种情况下，使用svn revert就能取消之前的修改。

svn revert用法如下：
```
# svn revert [-R] something
```
其中something可以是（目录或文件的）相对路径也可以是绝对路径。

当something为单个文件时，直接svn revert something就行了；当something为目录时，需要加上参数-R(Recursive,递归)，否则只会将something这个目录的改动。

在这种情况下也可以使用svn update命令来取消对之前的修改，但不建议使用。因为svn update会去连接仓库服务器，耗费时间。

注意：svn revert本身有固有的危险，因为它的目的是放弃未提交的修改。一旦你选择了恢复，Subversion没有方法找回未提交的修改。

第二种情况：改动已经被提交（commit）。

这种情况下，用svn merge命令来进行回滚。 

   回滚的操作过程如下： 
```
   1、保证我们拿到的是最新代码： svn update
   2、然后找出要回滚的确切版本号： svn log to confirm version    svn log 
   3、回滚到版本号： svn merge -r ori:des something    svn merge -r 28:25 something
     为了保险起见，再次确认回滚的结果： svn diff [something]
   4、提交回滚： svn commit -m "Revert revision from r28 to r25,because of ..." 
```
   将以上操作总结为三条如下：
```
   1. svn update，svn log，找到最新版本（latest revision）
   2. 找到自己想要回滚的版本号（rollbak revision）
   3. 用svn merge来回滚： svn merge -r : something
```

#svn历史版本

svn 查看历史信息 通过svn命令可以根据时间或修订号去除过去的版本，或者某一版本所做的具体的修改。以下四个命令可以用来查看svn 的历史：

svn log 用来展示svn 的版本作者、日期、路径等等

svn diff 用来显示特定修改的行级详细信息

svn cat 取得在特定版本的某文件显示在当前屏幕

svn list 显示一个目录或某一版本存在的文件

(一）svn log可以显示所有的信息，如果只希望查看特定的某两个版本之间的信息，可以使用：
```
svn log -r r1:r2
```
如果只想查看某一个文件的版本修改信息，可以使用
```
svn log A
```
如果希望得到目录的信息要加-v

如果希望显示限定N条记录的目录信息，使用
```
svn log --limit N -v
```

（二）svn diff用来检查历史修改的详情

  检查本地修改

  比较工作拷贝与版本库

  比较版本库与版本库
```
（1）如果用svn diff，不带任何参数，它将会比较你的工作文件与缓存在.svn的“原始”拷贝
（2）比较工作拷贝和版本库    svn diff -r 3 rule.txt，就是比较你的工作拷贝和版本库中版本号为3的文件rule.txt
（3）比较版本库与版本库    通过-r(revision)传递两个通过冒号分开的版本号，这两个版本会进行比较    svn diff -r 2:3 rule.txt 用来比较svn工作版本中版本号2和3的这个文件的变化
```

（三）svn cat

如果只是希望检查一个过去版本，不希望查看他们的区别，可使用svn cat
```
svn cat -r 版本号 rule,txt
```
这个命令会显示在该版本号下的该文件内容

（四）svn list

svn list可以在不下载文件到本地目录的情况下来察看目录中的文件：

如果你希望察看详细信息，你可以使用--verbose(-v) 参数：

这些列告诉你文件和目录最后修改的修订版本、做出修改的用户、如果是文件还会有文件的大小，最后是修改日期和项目的名字。


#svn上传.so文件无效

通过终端打开配置文件: open ~/.subversion/config，把下面两行(也可能是一行)中的注释和*.so去掉，然后保存
```
# global-ignores = *.o *.lo *.la *.al .libs *.a *.pyc *.pyo __pycache__
```
以后上传文件如果有*.so *.[0-9]需要专门 svn add 一下才能够正常上传


#svn上传后可执行权限

svn上传文件后添加可执行权限
```
svn propset svn:executable on targetfile
```
svn删除仓库中的文件可执行权限
```
svn propdel svn:executable targetfile
```
