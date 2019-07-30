#Linux下时间和时间戳

[网页连接](http://blog.csdn.net/ljafl9988/article/details/16847935)

1.时间戳转格式化日期，比如：1384936600 → 2013-11-20 08:36:40  输入一个long，输出一个nsstring

2.反过来：2013-11-20 08:36:40 → 1384936600 输入nsstring，输出一个long

好久没碰C语言。。好多函数都现查怎么用，还好一会就搞定了

1.时间戳转格式化

```
#include <stdio.h>  
#include <time.h>  
  
int main(int argc, const char * argv[])  
{  
    time_t t;  
    struct tm *p;  
    t=1384936600;  
    p=gmtime(&t);  
    char s[100];  
    strftime(s, sizeof(s), "%Y-%m-%d %H:%M:%S", p);  
    printf("%d: %s\n", (int)t, s);  
    return 0;  
}  
```

2.格式化转时间戳
```
#include <stdio.h>  
#include <time.h>  
  
int main(int argc, const char * argv[])  
{  
    struct tm* tmp_time = (struct tm*)malloc(sizeof(struct tm));  
    strptime("20131120","%Y%m%d",tmp_time);  
    time_t t = mktime(tmp_time);  
    printf("%ld\n",t);  
    free(tmp_time);  
    return 0;  
}  
```
