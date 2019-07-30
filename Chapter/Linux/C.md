# C语言中的宏定义

众多C++书籍都忠告我们C语言宏是万恶之首，但事情总不如我们想象的那么坏，就如同goto一样。宏有一个很大的作用，就是自动为我们产生代码。如果说模板可以为我们产生各种型别的代码(型别替换)，

那么宏其实可以为我们在符号上产生新的代码(即符号替换、增加)。

关于宏的一些语法问题，可以在google上找到。相信我，你对于宏的了解绝对没你想象的那么多。如果你还不知道#和##，也不知道prescan，那么你肯定对宏的了解不够。

我稍微讲解下宏的一些语法问题(说语法问题似乎不妥，macro只与preprocessor有关，跟语义分析又无关)：

1. 宏可以像函数一样被定义，例如：
```
#define min(x,y) (x 但是在实际使用时，只有当写上min()，必须加括号，min才会被作为宏展开，否则不做任何处理。
```

2. 如果宏需要参数，你可以不传，编译器会给你警告(宏参数不够)，但是这会导致错误。如C++书籍中所描述的，编译器(预处理器)对宏的语法检查不够，所以更多的检查性工作得你自己来做。

3. 很多程序员不知道的#和##

"#"符号把一个符号直接转换为字符串，例如：
```
#define STRING(x) #x const char *str = STRING( test_string ); 
```
str的内容就是"test_string"，也就是说#会把其后的符号直接加上双引号。

"##"符号会连接两个符号，从而产生新的符号(词法层次)，例如：
```
#define SIGN( x ) INT_##xint SIGN( 1 ); 
```
宏被展开后将成为：int INT_1;

4. 变参宏，这个比较酷，它使得你可以定义类似的宏：
```
#define LOG( format, ... ) printf( format, __VA_ARGS__ ) LOG( "%s %d", str, count );
```
__VA_ARGS__是系统预定义宏，被自动替换为参数列表。

5. 当一个宏自己调用自己时，会发生什么？例如：
```
#define TEST( x ) ( x + TEST( x ) ) TEST( 1 );
```
会发生什么？为了防止无限制递归展开，语法规定，当一个宏遇到自己时，就停止展开，也就是说，当对TEST( 1 )进行展开时，展开过程中又发现了一个TEST，那么就将这个TEST当作一般的符号。TEST(1)最终被展开为：1 + TEST( 1) 。

6. 宏参数的prescan，

当一个宏参数被放进宏体时，这个宏参数会首先被全部展开(有例外，见下文)。当展开后的宏参数被放进宏体时，

预处理器对新展开的宏体进行第二次扫描，并继续展开。例如：
```
#define PARAM( x ) x
#define ADDPARAM( x ) INT_##x
PARAM( ADDPARAM( 1 ) );
```
因为ADDPARAM( 1 ) 是作为PARAM的宏参数，所以先将ADDPARAM( 1 )展开为INT_1，然后再将INT_1放进PARAM。

例外情况是，如果PARAM宏里对宏参数使用了#或##，那么宏参数不会被展开：
```
#define PARAM( x ) #x
#define ADDPARAM( x ) INT_##x
PARAM( ADDPARAM( 1 ) ); 将被展开为"ADDPARAM( 1 )"。
```

使用这么一个规则，可以创建一个很有趣的技术：打印出一个宏被展开后的样子，这样可以方便你分析代码：
```
#define TO_STRING( x ) TO_STRING1( x )
#define TO_STRING1( x ) #x
```

TO_STRING首先会将x全部展开(如果x也是一个宏的话)，然后再传给TO_STRING1转换为字符串，现在你可以这样：```const char *str = TO_STRING( PARAM( ADDPARAM( 1 ) ) );```去一探PARAM展开后的样子。

7. 一个很重要的补充：就像我在第一点说的那样，如果一个像函数的宏在使用时没有出现括号，那么预处理器只是将这个宏作为一般的符号处理(那就是不处理)。


我们来见识一下宏是如何帮助我们自动产生代码的。如我所说，宏是在符号层次产生代码。我在分析Boost.Function模块时，因为它使用了大量的宏(宏嵌套，再嵌套)，导致我压根没看明白代码。后来发现了一个小型的模板库ttl，说的是开发一些小型组件去取代部分Boost(这是一个好理由，因为Boost确实太大)。同样，这个库也包含了一个function库。

这里的function也就是我之前提到的functor。ttl.function库里为了自动产生很多类似的代码，使用了一个宏：

```
#define TTL_FUNC_BUILD_FUNCTOR_CALLER(n) /
template< typename R, TTL_TPARAMS(n) > /
struct functor_caller_base##n /
///...
```

该宏的最终目的是：通过类似于TTL_FUNC_BUILD_FUNCTOR_CALLER(1)的调用方式，自动产生很多functor_caller_base模板：
```
template struct functor_caller_base1
template struct functor_caller_base2
template struct functor_caller_base3
///...
```

那么，核心部分在于TTL_TPARAMS(n)这个宏，可以看出这个宏最终产生的是：
```
typename T1
typename T1, typename T2
typename T1, typename T2, typename T3
///...
```
我们不妨分析TTL_TPARAMS(n)的整个过程。分析宏主要把握我以上提到的一些要点即可。以下过程我建议你翻着ttl的代码，相关代码文件：function.hpp, macro_params.hpp, macro_repeat.hpp, macro_misc.hpp, macro_counter.hpp。

so, here we Go

分析过程，逐层分析，逐层展开，例如TTL_TPARAMS(1)：

```
#define TTL_TPARAMS(n) TTL_TPARAMSX(n,T) 
=> TTL_TPARAMSX( 1, T )
#define TTL_TPARAMSX(n,t) TTL_REPEAT(n, TTL_TPARAM, TTL_TPARAM_END, t)
=> TTL_REPEAT( 1, TTL_TPARAM, TTL_TPARAM_END, T )
#define TTL_TPARAM(n,t) typename t##n,
#define TTL_TPARAM_END(n,t) typename t##n
#define TTL_REPEAT(n, m, l, p) TTL_APPEND(TTL_REPEAT_, TTL_DEC(n))(m,l,p) TTL_APPEND(TTL_LAST_REPEAT_,n)(l,p)
注意，TTL_TPARAM, TTL_TPARAM_END虽然也是两个宏，他们被作为TTL_REPEAT宏的参数，按照prescan规则，似乎应该先将
这两个宏展开再传给TTL_REPEAT。但是，如同我在前面重点提到的，这两个宏是function-like macro，使用时需要加括号，
如果没加括号，则不当作宏处理。因此，展开TTL_REPEAT时，应该为：
=> TTL_APPEND( TTL_REPEAT_, TTL_DEC(1))(TTL_TPARAM,TTL_TPARAM_END,T) TTL_APPEND( TTL_LAST_REPEAT_,1)(
TTL_TPARAM_END,T)
这个宏体看起来很复杂，仔细分析下，可以分为两部分：
TTL_APPEND( TTL_REPEAT_, TTL_DEC(1))(TTL_TPARAM,TTL_TPARAM_END,T)以及
TTL_APPEND( TTL_LAST_REPEAT_,1)(TTL_TPARAM_END,T)
先分析第一部分：
#define TTL_APPEND( x, y ) TTL_APPEND1(x,y) //先展开x,y再将x,y连接起来
#define TTL_APPEND1( x, y ) x ## y
#define TTL_DEC(n) TTL_APPEND(TTL_CNTDEC_, n)
根据先展开参数的原则，会先展开TTL_DEC(1)
=> TTL_APPEND(TTL_CNTDEC_,1) => TTL_CNTDEC_1
#define TTL_CNTDEC_1 0 注意，TTL_CNTDEC_不是宏，TTL_CNTDEC_1是一个宏。
=> 0 ， 也就是说，TTL_DEC(1)最终被展开为0。回到TTL_APPEND部分：
=> TTL_REPEAT_0 (TTL_TPARAM,TTL_TPARAM_END,T)
#define TTL_REPEAT_0(m,l,p)
TTL_REPEAT_0这个宏为空，那么，上面说的第一部分被忽略，现在只剩下第二部分：
TTL_APPEND( TTL_LAST_REPEAT_,1)(TTL_TPARAM_END,T)
=> TTL_LAST_REPEAT_1 (TTL_TPARAM_END,T) // TTL_APPEND将TTL_LAST_REPEAT_和1合并起来
#define TTL_LAST_REPEAT_1(m,p) m(1,p)
=> TTL_TPARAM_END( 1, T )
#define TTL_TPARAM_END(n,t) typename t##n
=> typename T1 展开完毕。
```

虽然我们分析出来了，但是这其实并不是我们想要的。我们应该从那些宏里去获取作者关于宏的编程思想。很好地使用宏看上去似乎是一些偏门的奇技淫巧，但是他确实可以让我们编码更自动化。
