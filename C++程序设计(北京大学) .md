# 郭炜

C++语言是特别讲究效率的语言，对效率是锱铢必较的。

## [](https://www.yuque.com/lianmt/it/fgmi63#pa1ycq)01 | 函数指针

函数指针，用来指向变量的地址。有起始地址（入口地址），通过函数指针调用函数体。

函数的名称和函数的指针是匹配的。

函数指针的必要性：可以对任意类型的数组进行排序。

![](http://upload-images.jianshu.io/upload_images/3317226-85cc843c020dc830.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#ck1izy)02 | 命令行参数

## [](https://www.yuque.com/lianmt/it/fgmi63#49cttf)03 | 位运算

### [](https://www.yuque.com/lianmt/it/fgmi63#kwreui)按位与**&**

1、**将某些变量中的某些位“清0”且同时保留其他位不变；也可以用来获取变量中的某一位。**

n = n & 0xffffff00;

也可以写成

n&= 0xffffff00;

如果n是short类型的，则只需执行：

n &= 0xff00;

2、如何判断一个int型变量n的第7位（从右往左，从0开始数）是否是1？

只需看表达式 “n & 0x80” 的值是否等于 0x80 即可。

### [](https://www.yuque.com/lianmt/it/fgmi63#8kwmdr)按位或“|”

将参与运算的两操作数各对应的二进制位进行或操作。

用来将某变量中的某些位“置1”且保留其他位不变。

### [](https://www.yuque.com/lianmt/it/fgmi63#rfpads)按位异或“^”

两个二进制位不相同时，结果才是1，否则为0；

用来将某变量中的某些位取反，且保留其他位不变。

**如果 a^b=c，那么就有 c^b=a 以及 c^a=b; (穷举法可证)**

**此规律可以用来进行最简单的加密和解密。**

另外还有一个有意思的点，即不通过临时变量，就能交换两个变量的值：

```
var a = 1, b = 2
a = a^b
b = b^a
a = a^b
console.log(a, b)

// a => 2
// b => 1

```

### [](https://www.yuque.com/lianmt/it/fgmi63#ocvzse)按位非 “~”

是单目运算符，能将二进制为0变成1，1变成0。（就是取反）

### [](https://www.yuque.com/lianmt/it/fgmi63#6eo0iw)左移运算符“<<”

a << b

的值是：将a各二进制位全部左移b位后得到的值。左移时高位丢弃，低位补0。

a 的值不因运算而改变。

```
9 << 4
0000 1001
1001 0000 
// 144

```

左移1位，就等于是乘以2，左移n位，就等于是乘以2<sup>n</sup>。

### [](https://www.yuque.com/lianmt/it/fgmi63#k2urui)右移运算符 “>>”

同理，移出最右边的位就被丢弃。 a 的值不因运算而改变。

大多数c/c++编译器规定，如果原符号位为1，则右移时高位就补充1，原符号位为0，则右移时高位就补充0。

右移1位，就等于是除以2，左移n位，就等于是除以2<sup>n</sup>，并且将结果往小里取整。

```
-25 >> 4 = -2
-2 >> 4  = -1
18 >> 4  = 1

```

**`所以答题，算对是很重要的，所以要小心谨慎。`**

### [](https://www.yuque.com/lianmt/it/fgmi63#kol9bk)答题

1、负数的二进制表示？

2、有两个int型的变量a和n（0 <= n <= 31） `32进制` ，

要求写一个表达式，使该表达式的值和a 的第n位相同。

`其实问题就是让你判断，a的n位是0还是1？`

(a >> n) & 1

当 n 不等于 31时，

(a & (1 << n)) >> n

**位运算很重要，它的速度非常快，能提高效率。**

## [](https://www.yuque.com/lianmt/it/fgmi63#lo2qht)04 | 引用

1、某个变量的引用，等价于这个变量，相当于该变量的一个别名。

2、**初始值改变，引用的值也跟着改变。**

3、**使用引用有3条要注意的地方：**

*   **定义引用时，一定要将其初始化成引用某个变量；**

*   **初始化后，它就一直引用该变量，不会再引用别的变量了（引用从一而终）。**

*   **引用只能引用变量，不能引用常量和表达式。**

![](http://upload-images.jianshu.io/upload_images/3317226-b21bf87ef435d9d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
r1引用了a
b 赋值给r1

则a = b
r1从一而终，依然是4

```

4、c语言中，如何编写交换两个整型变量值的函数？

**把参数变成指针，把指针的内容进行交换。**

5、c++，优化成了引用，引用的是指针。其实也是一回事。

```
void swap(int & a, int & b) {
    int tmp;
    tmp = a;
    a = b;
    b = tmp;
}
int n1, n2;
swap(n1, n2) // n1, n2的值被交换

```

6、引用可以作为函数的返回值

一个函数的返回值是引用。

```
int n = 4;
int & SetValue() { return n; }
int main() {
    SetValue() = 40;
    cout << n;
    return 0;
} // 输出：40

```

7、常引用

cont int & r = n;

特点，不能通过常引用去修改其引用的内容；除非进行强制类型的转换。

## [](https://www.yuque.com/lianmt/it/fgmi63#bt2lsk)05 | const 关键字和常量

定义常量，const是有类型的，便于类型检查。

1、定义常量指针

**不可通过常量指针修改其指向的内容。**

`而不是说不能修改其内容`

```
int n, m;
const int * p = &n;
*p = 5; // 编译出错
n = 4; // ok
p = &m; // ok, 常量指针的指向可以变化

```

2、不能把常量指针赋值给非常量指针，反过来可以

```
const int * p1; int * p2;
p1 = p2 //ok
p2 = p1; // error

// 如果就是想要把一个常量指针，指向非常量指针，那就需要强制类型转换
p2 = (int * ) p1; // ok,强制类型转换

```

3、函数参数为常量指针时，可避免函数内部不小心改变参数指针所指地方的内容

```
void MyPrintf(const char * p) {
    strcpy(p, "this"); // 编译出错
    printf("%s", p) ;; //ok
}

```

那编译器是如何发现问题的呢？根据strcpy的参数类型的不同

## [](https://www.yuque.com/lianmt/it/fgmi63#veqpah)06 | 动态内存分配

**实际运行需要多少空间，就按照这个需要去进行空间的动态内容分配。**

![](http://upload-images.jianshu.io/upload_images/3317226-6ffca2f595b64d8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-10310f3ef66f0c7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
int * pn;
int i = 5;
pn = new int[i * 20];
pn[0] = 20;
pn[100 = 30; // 编译没问题。运行时导致数组越界

```

**用“new”动态分配的内存空间，一定要用“delete”运算符进行释放。否则就容易特别慢，或者导致崩溃。**

**delete 指针; // 该指针必须指向new出来的空间**

```
int * p = new int;
* p = 5;
delete p;
delete p; // 导致异常，一片空间不能被delete多次

```

**如果动态分配的是数组，要加“[]”**

**delete [] 指针; // 该指针必须指向 new 出来的数组**

```
int * p = new int[]/20 ;
p[0] = 1;
delete [] p;

```

## [](https://www.yuque.com/lianmt/it/fgmi63#4rb9dn)07 | 内联函数、函数重载、函数缺省参数

### [](https://www.yuque.com/lianmt/it/fgmi63#0bfwdy)1、内联函数

![](http://upload-images.jianshu.io/upload_images/3317226-7c8bfef25984aee4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**这样一个简单的函数，如果调用次数过多，那函数的内容的开销跟调用函数的开销差不多，就形成了浪费，所以使用内敛函数，就可以提高函数执行的效率。**

![](http://upload-images.jianshu.io/upload_images/3317226-a4f2dee0e101d24f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### [](https://www.yuque.com/lianmt/it/fgmi63#wq4uuh)2、函数重载

![](http://upload-images.jianshu.io/upload_images/3317226-6892ec81aa33e6ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#7oi2bf)08 | 函数缺省参数

**适应需求，当功能增加的时候，可以少改很多个缺省调用语句，可以减少程序修改量的目的，那 说明你的程序的扩展性比较好。**

![](http://upload-images.jianshu.io/upload_images/3317226-411fa1c56dd64b1b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
void func(int x1, int x2 = 2, int x3 = 3) {}

func(10); // 等效于func(10, 2, 3)
func(10, 8); // 等效于func(10, 8, 3)
func(10, , 8) // 不行，只能最右边的连续若干个参数缺省

```

![](http://upload-images.jianshu.io/upload_images/3317226-7398af5f3714e3dd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# [](https://www.yuque.com/lianmt/it/fgmi63#toiquf)刘家瑛

## [](https://www.yuque.com/lianmt/it/fgmi63#xu70yz)09 | 面向对象程序设计方法

### [](https://www.yuque.com/lianmt/it/fgmi63#5qk7gl)结构化程序设计

1、将复杂的问题 → 层层分解/模块化 → 若干子问题

每个模块都不同的开发人员来实现，同时能他们要约定要相互的通讯，和协作接口。

2、结构化设计，就是自顶向下，逐步求精的过程。

程序 = 数据结构（变量） + 算法（函数）

3、结构化程序设计的4大囧境

理解难、修改难、差错难、重用难。

### [](https://www.yuque.com/lianmt/it/fgmi63#hoookd)面向对象的程序设计

1、面向对象的设计方法：抽象成类、封装成方法

![](http://upload-images.jianshu.io/upload_images/3317226-cb5dab2f6c7886e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#0t32ra)10 | 面向对象程序设计的发展历程

![](http://upload-images.jianshu.io/upload_images/3317226-05a3151c8127f3b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-218a53fa0a92464a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-2303f8970ba2de7a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#h4erbb)11 | 类成员的可访问范围

## [](https://www.yuque.com/lianmt/it/fgmi63#fehvub)12 | 内联成员函数和重载成员函数

# [](https://www.yuque.com/lianmt/it/fgmi63#0uo3lw)郭炜

## [](https://www.yuque.com/lianmt/it/fgmi63#chiybz)13 | 构造函数

![](http://upload-images.jianshu.io/upload_images/3317226-52cf9a3cedd867bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-90884d8bed526a3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-228240526bf1c563.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

整型可以被自动转化为doubler类型。

![](http://upload-images.jianshu.io/upload_images/3317226-88e0430b9ec3d70a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

带 * 的表示指针，而指针不会生成对象，所以不会调用构造函数，所以第三行只打印了2个。

![](http://upload-images.jianshu.io/upload_images/3317226-482b4bf9c7387d27.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#c78gkl)14 | 复制构造函数

![](http://upload-images.jianshu.io/upload_images/3317226-80ded3167214b8d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

复制构造函数起作用的3种情况: 赋值、函数参数、return

![](http://upload-images.jianshu.io/upload_images/3317226-00fbde86722ec181.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-16b629bef9cfe417.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-d2013fa661f9a5f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-c1906624162f6d55.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-acad26d7cbbcbe21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#06cnwd)15 | 类型转换构造函数

![](http://upload-images.jianshu.io/upload_images/3317226-7f98769f2517f6ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#pmdxwg)16 | 析构函数

为消亡构造函数，有了析构函数

![](http://upload-images.jianshu.io/upload_images/3317226-0812448a049c3f51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-3e706a5abba31d3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-91d36678bf087a2f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-9888c034fe3787c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

先被构造的函数，会最后被析构掉。

![](http://upload-images.jianshu.io/upload_images/3317226-1b6860be46e1ca9c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## [](https://www.yuque.com/lianmt/it/fgmi63#9g66cn)


## 17 | 静态成员变量和静态成员函数

静态成员：在说明前面加了static关键字的成员。

*   普通成员变量每个对象有各自的一份，而静态成员变量一共就一份，为所有对象共享。

*   普通成员函数必须具体作用域某个对象，而静态成员安徽省农户并不具体作用域某个对象。

*   因此静态成员不需要通过对象就能访问。

如何访问静态成员

1）类名::成员名

2）对象名.成员名

3）指针->成员名

4）引用.成员名

*   静态成员变量本质上是全局变量，哪怕一个对象都不存在，类的静态成员变量也存在。

*   静态成员函数本质上是全局函数。

## [](https://www.yuque.com/lianmt/it/fgmi63#8lwnog)18 | 成员对象和封闭类的概念

## [](https://www.yuque.com/lianmt/it/fgmi63#ms4gxr)19 | 友元函数

## 20 | this指针

this指针指向，成员函数所作用的那个对象。

![](http://upload-images.jianshu.io/upload_images/3317226-00e9845607da5172.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-7d1b1c34553ad256.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 21 | 常量对象、常量成员函数和常引用

![](https://upload-images.jianshu.io/upload_images/3317226-0af782857b34a832.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 22 | 运算符重载的基本概念
运算符重载
对已有的运算符赋予多重的含义

使同一运算符作用于不同类型的数据时 -> 不同类型的行为
目的

扩展C++中提供的运算符的适用范围，以用于类所表示的抽象数据类型
同一个运算符，对不同类型的操作数，所发生的行为不同。

## 23 | 赋值运算符的重载

赋值运算符“=”只能重载为 **成员函数**

### [](https://www.yuque.com/lianmt/it/fgmi63#okm2gc)重载赋值运算符的意义-浅复制和深复制

浅复制/浅拷贝

*   执行逐个字节的复制工作

![](http://upload-images.jianshu.io/upload_images/3317226-8d4d056b0f928b9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/3317226-b19891b325a45fcf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

浅复制/浅拷贝的bug：

s1 = s2有个问题，当内存空间同时消亡的时候，那么（2）的内存空间就会被先后释放2次，这样会导致严重的内存错误，甚至可能引发程序的意外终止。

深复制/深拷贝：

![](http://upload-images.jianshu.io/upload_images/3317226-bb11575c7ce618c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


[视频链接](https://www.bilibili.com/video/av10046030/?p=3)
