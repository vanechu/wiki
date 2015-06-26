---
title: "C++ basic"
layout: page
date: 2015-06-20 00:00
---

# Reference #

[04831750.1x C++ 程序设计](https://courses.edx.org/courses/course-v1:PekingX+04831750.1x+2015T1/info)

## Chapter 1

### 1.1 函数指针

#### Definition

类型名 (* 指针变量名)(参数类型1, 参数类型2,…);

```
#include <stdio.h>

void PrintMin(int a,int b) {
    if( a<b )
    printf("%d",a);
    else
    printf("%d",b);
}
int main() {
    void (* pf)(int ,int);
    int x = 4, y = 5;
    pf = PrintMin;
    pf(x,y);
    return 0; 
}
```

#### qsort

```
void qsort(void *base, int nelem, unsigned int width,
 int ( * pfCompare)( const void *, const void *));
``` 

```
#include <stdio.h>
#include <stdlib.h>
int MyCompare( const void * elem1, const void * elem2 )
{
    unsigned int * p1, * p2;
    p1 = (unsigned int *) elem1; // “* elem1” 非法
    p2 = (unsigned int *) elem2; // “* elem2” 非法
    return (* p1 % 10) - (* p2 % 10 );
}
#define NUM 5
int main()
{
    unsigned int an[NUM] = { 8,123,11,10,4 };
    qsort( an,NUM,sizeof(unsigned int), MyCompare);
    for( int i = 0;i < NUM; i ++ )
    printf("%d ",an[i]);
    return 0;
}
```

### 1.2 命令行参数

#### Definition

```
int main(int argc, char * argv[]){}
```
`argc` : 命令行参数的个数。C/C++语言规定，可执行程序程序本身的文件名，也算一个命令行参数，因此，argc的值至少是1
`argv` : 指针数组，其中的每个元素都是一个char* 类型的指针，该指针指向一个字符串，这个字符串里就存放着命令行参数

#### Example

```
#include <stdio.h>
int main(int argc, char * argv[])
{
    for(int i = 0;i < argc; i ++ )
    printf( "%sn",argv[i]);
    return 0;
}
```

### 1.3 位运算

#### 按位与 "&"

##### Definition
将参与运算的两操作数各对应的二进制位进行与操作，只有对应的两个二进位均为1时，结果的对应二进制位才为1，否则为0。

```
例如：表达式“21 & 18 ”的计算结果是16(即二进制数10000)，因为：

21 用二进制表示就是：
0000 0000 0000 0000 0000 0000 0001 0101
18 用二进制表示就是:
0000 0000 0000 0000 0000 0000 0001 0010
二者按位与所得结果是：
0000 0000 0000 0000 0000 0000 0001 0000
```

##### Usage
通常用来将某变量中的某些位清0且同时保留其他位不变。也可以用来获取某变量中的某一位。

```
例如，如果需要将int型变量n的低8位全置成0，而其余位不变，则可以执行：
n = n & 0xffffff00;
or:
n &= 0xffffff00;
如果n是short类型的，则只需执行：
n &= 0xff00;
```

#### 按位或 "|"

##### Definition
将参与运算的两操作数各对应的二进制位进行或操作，只有对应的两个二进位都为0时，结果的对应二进制位才是0，否则为1。

```
例如：表达式“21 | 18 ”的值是23，因为：
21:    0000 0000 0000 0000 0000 0000 0001 0101
18:    0000 0000 0000 0000 0000 0000 0001 0010
21|18: 0000 0000 0000 0000 0000 0000 0001 0111
```

##### Usage
按位或运算通常用来将某变量中的某些位置1且保留其他位不变。

```
例如，如果需要将int型变量n的低8位全置成1，而
其余位不变，则可以执行：
n |= 0xff;
0xff: 1111 1111
```

#### 按位异或 "^"

##### Definition
将参与运算的两操作数各对应的二进制位进行异或操作，即只有对应的两个二进位不相同时，结果的对应二进制位才是1，否则为0。

```
例如：表达式“21 ^ 18 ”的值是7(即二进制数111)。
21:    0000 0000 0000 0000 0000 0000 0001 0101
18:    0000 0000 0000 0000 0000 0000 0001 0010
21^18: 0000 0000 0000 0000 0000 0000 0000 0111
```

##### Usage
- 按位异或运算通常用来将某变量中的某些位取反，且保留其他位不变。

```
n ^= 0xff;
0xff: 1111 1111
```
- 异或运算的特点是:
如果 a^b=c，那么就有 c^b = a以及c^a=b(穷举法可证)。此规律可以用来进行最简单的加密和解密。

- 另外异或运算还能实现不通过临时变量，就能交换两个变量的值：即实现a,b值交换。穷举法可证。
```
 int a = 5, b = 7;
 a = a ^ b;
 b = b ^ a;
 a = a ^ b;
```

#### 按位非 "~"

##### Definition
将操作数中的二进制位0变成1, 1变成0。

```
例如，表达式“~21”的值是整型数 0xffffffea
21:  0000 0000 0000 0000 0000 0000 0001 0101
~21: 1111 1111 1111 1111 1111 1111 1110 1010
```

#### 左移运算符 “<<”

表达式：a << b 的值是：将a各二进位全部左移b位后得到的值。左移时，高位丢弃，低位补0。a 的值不因运算而改变。

```
例如:
9 << 4
9的二进制形式：
0000 0000 0000 0000 0000 0000 0000 1001
因此，表达式“9<<4”的值，就是将上面的二进制数左移4位，得：
0000 0000 0000 0000 0000 0000 1001 0000
即为十进制的144。
```

#### 
a >> b 的值是：将a各二进位全部右移b位后得到的值。右移时，移出最右边的位就被丢弃。 a 的值不因运算而改变。

对于有符号数，如long,int,short,char类型变量，在右移时，符号位（即最高位）将一起移动，并且大多数C/C++编译器规定，如果原符号位为1，则右移时高位就补充1，原符号位为0，则右移时高位就补充0。实际上，右移n位，就相当于左操作数除以2n，*并且将结果往小里取整*。

```
-25 >> 4 = -2
-2 >> 4 = -1
18 >> 4 = 1
```

```
#include <stdio.h>
int main()
{
    int n1 = 15;
    short n2 = -15;
    unsigned short n3 = 0xffe0;
    char c = 15;
    n1 = n1>>2;
    n2 >>= 3;
    n3 >>= 4;
    c >>= 3;
    printf( "n1=%d,n2=%x,n3=%x,c=%x",n1,n2,n3,c);
} //输出结果是：n1=3,n2=fffffffe,n3=ffe,c=1
```


### 1.4 引用

#### Definition

定义引用时一定要将其初始化成引用某个变量. 初始化后，它就一直引用该变量，不会再引用别的变量了

`类型名 & 引用名 = 某变量名;`

```
int n = 4;
int & r = n; // r引用了 n, r的类型是
```

#### 引用作为函数的返回值

```
int n = 4;
int & SetValue() { return n; }
int main()
{
    SetValue() = 40;
    cout << n;
    return 0;
} //输出： 40
```

#### 常引用

- 定义引用时，前面加const关键字，即为“常引用”. 不能通过常引用去修改其引用的内容:

```
int n = 100;
const int & r = n;
r = 200; //编译错
n = 300; // 没问题
```

- 常引用和非常引用的转换

const T & 和T & 是不同的类型.
T & 类型的引用或T类型的变量可以用来初始化const T & 类型的引用。
const T 类型的常变量和const T & 类型的引用则不能用来初始化T &类型的引用，除非进行强制类型转换。

```
int n = 8;
const int & r1 = n;
int & r2 = r1; //错

int n = 8;
int & r1 = n;
const int r2 = r1;  //对
```

### 1.5 const

#### 常量

```
const int MAX_VAL = 23;
```


#### 常量指针

- 不可通过常量指针修改其指向的内容

```
int n,m;
const int * p = & n;
* p = 5; //编译出错
n = 4; //ok
p = &m; //ok, 常量指针的指向可以变化
```

- 不能把常量指针赋值给非常量指针，反过来可以

```
const int * p1; int * p2;
p1 = p2; //ok
p2 = p1; //error
p2 = (int * ) p1; //ok,强制类型转换
```

- 函数参数为常量指针时，可避免函数内部不小心改变参数指针所指地方的内容

```
void MyPrintf( const char * p )
{
    strcpy( p,"this"); //编译出错
    printf("%s",p); //ok
}
```

### 1.6 动态内存分配

#### new 运算符

- 第一种用法，分配一个变量:

`P = new T;`

'T'是任意类型名，P是类型为'T*' 的指针。动态分配出一片大小为'sizeof(T)'字节的内存空间，并且将该
内存空间的起始地址赋值给'P'。比如:

```
int * pn;
pn = new int;
* pn = 5;
```

- 第二种用法,分配一个数组:

```
P = new T[N];

T :任意类型名
P :类型为T * 的指针 (非T* [])
N :要分配的数组元素的个数，可以是整型表达式

动态分配出一片大小为 sizeof(T)字节的内存空间，并且将该内存空间的起始地址赋值给P。

int * pn;
int i = 5;
pn = new int[i * 20];
pn[0] = 20;
pn[100] = 30; //编译没问题。运行时导致数组越界
```

- 用“new”动态分配的内存空间，一定要用"delete"运算符进行释放

```
int * p = new int;
* p = 5;
delete p;
delete p; //导致异常，一片空间不能被delete多次

int * p = new int[20];
p[0] = 1;
delete [] p; // 用"delete"释放动态分配的数组，要加"[]"
```

## Chapter 2

### 2.1 类

#### Declaration

```
class CRectangle
{
    public
    :
    int w, h;
    void Init( int w_, int h_ ) {
        w = w_; h = h_;
    }
    int Area() {
        return w * h;
    }
    int Perimeter() {
        return 2 * ( w + h );
    }
};

int main() {
    int w, h;
    CRectangle r; //r是一个对象
    cin >> w >> h;
    r.Init(w, h);
    cout << r.Area() << endl << r. Perimeter();
    return 0;
}
```

#### 对象的内存空间
- 对象的大小 = 所有成员变量的大小之和
- E.g. `CRectangle`类的对象, `sizeof(CRectangle) = 8`

#### 访问类的成员变量和成员函数

- 用法1: 对象名.成员名

```
CRectangle r1, r2;
r1.w = 5;
r2.Init(3,4);
```

- 用法2: 指针->成员名

```
CRectangle r1, r2;
CRectangle * p1 = & r1;
CRectangle * p2 = & r2;
p1->w = 5;
p2->Init(3,4); //Init作用在p2指向的对象上
```

- 用法3: 引用名.成员名

```
CRectangle r2;
CRectangle & rr = r2;
rr.w = 5;
rr.Init(3,4); //rr的值变了，r2的值也变
```

- 另一种输出结果的方式

```
void PrintRectangle(CRectangle & r) {
    cout << r.Area() << ","<< r.Perimeter();
}
CRectangle r3;
r3.Init(3,4);
PrintRectangle(r3);
```

### 2.2 内联成员函数

#### 两种方式

1. inline + 成员函数 
2. 整个函数体出现在类定义内部

```
class B{
    inline void func1(); // 1. inline + 成员函数 
    void func2() {  // 2. 整个函数体出现在类定义内部
    };
};
void B::func1() { }
```

### 2.3 构造函数

#### Definition

- 名字与类名相同，可以有参数，不能有返回值(void也不行)
- 作用是对对象进行初始化，如给成员变量赋初值
- 如果定义类时没写构造函数，则编译器生成一个默认的无参数的构造函数. 默认构造函数无参数，不做任何操作
- 如果定义了构造函数，则编译器不生成默认的无参数的构造函数
- 对象生成时构造函数自动被调用。对象一旦生成，就再也不能在其上执行构造函数
- 一个类可以有多个构造函数
- 构造函数最好是public的，private构造函数不能直接用来初始化对象

```
class Complex {
    private :
    double real, imag;
    public:
    void Set( double r, double i );
    Complex(double r, double i );
    Complex (double r );
    Complex (Complex c1, Complex c2);
};
Complex::Complex(double r, double i)
{
    real = r; imag = i;
}
Complex::Complex(double r)
{
    real = r; imag = 0;
}
Complex::Complex (Complex c1, Complex c2);
{
    real = c1.real+c2.real;
    imag = c1.imag+c2.imag;
}
Complex c1(3) , c2 (1,0), c3(c1,c2);
// c1 = {3, 0}, c2 = {1, 0}, c3 = {4, 0};
```

#### 构造函数在数组中的使用

```
class Test {
    public:
    Test( int n) { } //(1)
    Test( int n, int m) { } //(2)
    Test() { } //(3)
};
Test array1[3] = { 1, Test(1,2) };
// 三个元素分别用(1),(2),(3)初始化
Test array2[3] = { Test(2,3), Test(1,2) , 1};
// 三个元素分别用(2),(2),(1)初始化
Test * pArray[3] = { new Test(4), new Test(1,2) };
//两个元素分别用(1),(2) 初始化
```