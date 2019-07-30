#网页编译目录
```
build dir  /home/zhanghao/sugon/project/BaiduOEM170325/development/Build/.build/webui_html5-2.398.0-src/data/
tmp dir    /home/zhanghao/sugon/project/BaiduOEM170325/development/Build/.workspace/tmp
```

#中文设定

清除网页上的中文设定，否则某些异常退出的情况下由于cookie缓存造成BMC页面无法打开
```
localStorage.setItem('locale', 'root');
```

#用curl下载文件
```
//登陆
curl -X POST -d "username=ADMIN&password=ADMIN" "http://10.0.22.31/api/session" -c ./cookie
//下载
curl -o test.txt -H "X-CSRFTOKEN:ipMOdTeL" "http://10.0.22.31/baidu/maintenance/sol/dump"  -b ./cookie
```
