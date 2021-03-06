C语言语法

1. C语言简介

C语言是1970年由Dennis Ritchel为UNIX系统设计的，并且在DEC
PDP-11计算机上实现。UNIX系统、C编译器、几乎所有的UNIX程序使用C编写。并推广到其他大型机、单片机中。C语言设计的目标有高效率、访问硬件、高级语言通用性、可移植性。

C语言最初为硬件简陋的计算机设计的操作系统的语言，并且是一门相对低级的高级语言，比较适宜开发操作系统和驱动。相对于其他语言，C语言的特性有：

-   效率高。约为汇编语言的的80%。

-   访问硬件。可以直接操作硬件、内存。

-   简陋。为了可移植性，C语言设计的特别小，很多时候需要自己手动实现一些基础功能。大量缩写需要熟练。

-   灵活。通用性强，限制少。比如指针，有好有坏，强大，但需要纪律约束。

学习C语言是因为C语言应用广泛，贴近底层，还算是一门容易入门的语言。特别适合用来学习计算机结构。一般称C语言程序，C语言连载一起作专有名词。

2. C语言程序编写环境

Windows系统中安装virtualbox，其中建立debian虚拟机，root登录后，在终端命令行输入“apt-get
install codeblocks”安装code blocks。或者直接在windows系统中下载安装code
blocks自由软件。

入门时，可以在windows环境中编写改程序，调试无误后放入linux中调试。除了学习操作系统，linux常作为服务端，大部分开发在windows环境中即可。

3.C语言程序结构

hello.c

/\* 这是C语言程序中的标准注释

\* file: D:/code/hello.c

\* author: zen

\* time: 2017-12-12

\*/

\#include \<stdio.h\> /\* 最常见的两个引入文件 \*/

\#include "stdlib.h\>" //这是单行注释，非标准注释

\#define MAXSIZE 10 /\*
定义全局变量，注意没有=。也叫宏定义。编译器会搜寻此名称并替换，用于约定变量名称和值\*/

/\*
C程序严格，定义函数前要有返回值类型，一般传入一个整数大小的指针，整数和字符较小时候也可以直接传值
\*/

int count(char\* string){
//传入待统计字符串的第一个字符的指针，用于引入整个字符串

int i; i=0; /\*老编译器严格先声明变量，再赋值,\*/

while(string[i]!='\\n'){ /\* C语言中字符串中\\n表示行结束 \*/

if(string[i]!=' '){ /\* 统计非空格字符数量 \*/

i++; /\* while(){}之外定义的的i在while内生效，但在main(){}中无效。
内层空间定义的变量只在内层生效，外层定义的空间在外层及其所包含的内层空间生效。\*/

} /\*
C程序采用;和{}区分代码块。;结束语句。{}分列行的左右两端，在左右两端都很清楚分块
\*/

}

if(i\>MAXSIZE){

print("name too long!");

return -1; /\* 约定-1表示错误 \*/

}

return i; /\* return结束函数并返回结果 \*/

}

/\* \*/

/\* 在此之前都是定义程序，只有main()是执行程序 \*/

int main(){

char name[20];

scanf("my name is ：%s",name); /\* 格式化输入函数scanf是scan
format的缩写，返回值是int，第一个参数是提示和占位符，后面的参数才是变量名。此语句将一个字符串类型赋值给name
\*/

char\* str; /\* 指针声明格式 \*/

str = \&name; /\* 指针赋值格式，一般从变量引入地址而不是直接赋值 \*/

int number; number=0； /\* number的地址上可能有垃圾值，所以声明变量即给默认赋值
\*/

nubmber = count(str); /\* 执行函数 \*/

printf("my name have %d charactors.", number); /\*
printf()与scanf()类似，C语言很节省，需要记住大量缩写 \*/

}

4.C语言中的数据类型

C语言的基本变量类型有integer，float，character。没有bool。记住C语言是在简陋机器上实现操作系统的语言。

int a=3; //表示给a赋值整数3

float b; b=’c’-0; print(b); //这行放在main()中 应该输出3.0. ‘c’

；表示执行该语句。

定义一个数组，int array[3]={1,2,3}，array[2]==’3’.C语言数组就这些操作。

4.C语言中运算符号

指针，附属于变量，先有变量，后有指针。

\<\<1 左移一位，相当于值翻倍二倍 \>\>1，右移一位，相当于弱减半。

goto ++ -- += -=

5. C语言调试

通用的调试办法由断点breakpoint、单步跟踪tracker、变量监视watcher、内存镜像memory
dump、函数调用栈call stack、断言assert()、日志输出fprint()。

Code blocks 新建项目，将以上窗口全开。

练习

思考代码出错的地方可能有哪些，比对编译器的提示，尝试三个程序验证。

C代码对照状态机格局

6.C语言中的指针

指针用于标记某个变量的地址，一般说指向某个地址，是指指向变量所占区域的起始地址位。

一个指针在32位系统中占用32位，占用小，控制精细。C语言实在简陋机器上实现操作系统，指针的应用十分广泛。其他语言中更多的是将变量的值复制过去再运行，避免指针灵活性滥用。

int x=1; y=2 ; z[10];

int\* p; // p是指针，指向一个int变量

p=\&x; //取得x地址，赋值给p

y=\*p; //将p所指向变量的值赋值给y，\*p==x

p=\&z[0]; //p为z[0]元素的地址，也就是z的地址。

y=\*(p+1); //y==z[1]

C语言很多时候引用变量的地址，有时候必须用指针，直接操作变量对象。

swap(int\* x, int\* y){

int tmp;

tmp=\*x;

\*x=\*y;

\*y=tmp;

}

7.C语言中的结构体

C语言没有特效，很多其他语言中的基础功能都要写轮子。指针加结构会实现灵活的功能。

struct Student{

unsigned ID;

char name[10];

float G;

}; //记住有;可能是因为要预备执行吧

struct Student Sean{123, ’Sean’, 3.88};

Sean.GPA==3.88;

P=\&Sean;

p-\>GPA==3.88;

参考书目：《C程序设计语言》 kernighan ritch

练习：《程序设计导引及在线实践》poj

视频教程：计算导论与C语言基础<https://www.coursera.org/specializations/biancheng-suanfa>
