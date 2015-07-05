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

## Chapter 3

### 3.1 复制构造函数

#### 基本概念
- 只有一个参数,即对同类对象的引用
- 形如 `X::X( X& )` 或 `X::X(const X &)`, 二者选一. 后者能以常量对象作为参数
- 如果没有定义复制构造函数，那么编译器生成默认复制构造函数。默认的复制构造函数完成复制功能。

```
class Complex {
private :
 double real,imag;
};
Complex c1; //调用缺省无参构造函数
Complex c2(c1);//调用缺省的复制构造函数,将 c2 初始化成和c1一样
```

如果定义的自己的复制构造函数，则默认的复制构造函数不存在。

```
class Complex {
  public :
  double real,imag;
  Complex(){ }
  Complex( const Complex & c ) {
      real = c.real;
      imag = c.imag;
      cout << “Copy Constructor called”;
  }
};
Complex c1;
Complex c2(c1);//调用自己定义的复制构造函数，输出 Copy Constructor called
```

不允许有形如 X::X( X )的构造函数。

```
class CSample {
  CSample( CSample c ) {
  } //错，不允许这样的构造函数
};
```

#### 复制构造函数起作用的三种情况

1. 当用一个对象去初始化同类的另一个对象时。(同上)

```
Complex c2(c1);
Complex c2 = c1; //初始化语句，非赋值语句
```

2. 如果某函数有一个参数是类 A 的对象，那么该函数被调用时，类A的复制构造函数将被调用。

```
class A
{
  public:
  A() { };
  A( A & a) {
    cout << "Copy constructor called" <<endl;
  }
};

void Func(A a1){}
int main(){
  A a2;
  Func(a2);
  return 0;
}
//程序输出结果为: Copy constructor called
```

3. 如果函数的返回值是类A的对象时，则函数返回时，A的复制构造函数被调用:

```
class A
{
  public:
  int v;
  A(int n) { v = n; };
  A( const A & a) {
    v = a.v;
    cout << "Copy constructor called" <<endl;
  }
};

A Func() {
  A b(4);
  return b;
}

int main() {
  cout << Func().v << endl;
  return 0;
}
//输出结果：
//Copy constructor called
//4
```

### 3.2 类型转换构造函数

#### 目的:
- 实现类型的自动转换

#### 特点:
- 只有一个参数
- 不是复制构造函数
- 编译系统会自动调用 -> 转换构造函数 (建立一个 临时对象 / 临时变量)

```
class Complex {
    public:
    double real, imag;
    Complex( int i ) { //类型转换构造函数
        cout << “IntConstructor called” << endl;
        real = i; imag = 0;
    }
    Complex( double r, double i )
    { real = r; imag = i; }
};
int main () {
    Complex c1(7, 8);
    Complex c2 = 12; //初始化
    c1 = 9; // 9被自动转换成一个临时Complex对象
    cout << c1.real << "," << c1.imag << endl;
    return 0;
}
// 输出:
// IntConstructor called
// IntConstructor called
// 9,0
```

### 3.3 析构函数


#### Definition

- 成员函数的一种
- 名字与类名相同
- 在前面加 ‘~’
- 没有参数和返回值
- 一个类最多只有一个析构函数
- 对象消亡时 -> 自动被调用
- 在对象消亡前做善后工作(释放分配的空间等)
- 定义类时没写析构函数, 则编译器生成`缺省析构函数`, 不涉及释放用户申请的内存释放等清理工作
- 定义了析构函数, 则编译器不生成缺省析构函数


```
class String{
    private :
    char * p;
    public:
    String () {
        p = new char[10];
    }
    ~ String ();
};
String ::~ String() {
    delete [] p;
}
```

#### 析构函数和数组
对象数组生命期结束时 -> 对象数组的每个元素的析构函数都会被调用
```
class Ctest {
    public:
    ~Ctest() { cout<< "destructor called" << endl; }
};
int main () {
    Ctest array[2];
    cout << "End Main" << endl;
    return 0;
}
输出:
End Main
destructor called
destructor called
```

#### 析构函数和运算符 delete
delete 运算导致析构函数调用:
```
Ctest * pTest;
pTest = new Ctest; //构造函数调用
delete pTest; //析构函数调用
------------------------------------------------------------------
pTest = new Ctest[3]; //构造函数调用3次
delete [] pTest; //析构函数调用3次
```

#### 构造函数和析构函数调用时机的例题

```
class Demo {
    int id;
    public:
    Demo( int i )
    {
        id = i;
        cout << “id=” << id << “ Constructed” << endl;
    }
    ~Demo()
    {
        cout << “id=” << id << “ Destructed” << endl;
    }
};

Demo d1(1);
void Func(){
    static Demo d2(2);
    Demo d3(3);
    cout << “Func” << endl
    ;
}
int main (){
    Demo d4(4);
    d4 = 6;
    cout << “main” << endl;
    { Demo d5(5);}
    Func();
    cout << “main ends” << endl
    ;
    return 0;
}

输出:
id=1 Constructed
id=4 Constructed
id=6 Constructed
id=6 Destructed // 类型转换构造函数临时对象析构时
main
id=5 Constructed
id=5 Destructed // {}作用域
id=2 Constructed
id=3 Constructed
Func
id=3 Destructed
main ends
id=6 Destructed
id=2 Destructed
id=1 Destructed
```

### 3.4 静态成员变量和静态成员函数

#### 基本概念

- 静态成员：在说明前面加了static关键字的成员。
- 普通成员变量每个对象有各自的一份，而静态成员变量一共就一份，为所有对象共享。
- 普通成员函数必须具体作用于某个对象，而静态成员函数并不具体作用与某个对象。
- 因此静态成员不需要通过对象就能访问
- 静态成员变量本质上是全局变量，哪怕一个对象都不存在，类的静态成员变量也存在。
- 静态成员函数本质上是全局函数。
- 设置静态成员这种机制的目的是将和某些类紧密相关的全局变量和函数写到类里面，看上去像一个整体，易于维护和理解。
```
class CRectangle
{
    private:
    int w, h;
    static int nTotalArea; //静态成员变量
    static int nTotalNumber;
    public:
    CRectangle(int w_,int h_);
    ~CRectangle();
    static void PrintTotal(); //静态成员函数
};
```

- 普通成员变量每个对象有各自的一份，而静态成员变量一共就一份，为所有对象共享。

```
//sizeof 运算符不会计算静态成员变量。
class CMyclass {
 int n;
 static int s;
};
// sizeof( CMyclass ) 等于 4
```

#### 如何访问静态成员

- 类名::成员名
`CRectangle::PrintTotal();`
- 对象名.成员名
`CRectangle r; r.PrintTotal();`
- 指针->成员名
`CRectangle * p = &r; p->PrintTotal();`
- 引用.成员名
`CRectangle & ref = r; int n = ref.nTotalNumber; `

#### 静态成员示例
考虑一个需要随时知道矩形总数和总面积的图形处理程序, 可以用全局变量来记录总数和总面积. 用静态成员将这两个变量封装进类中，就更容易理解和维护

```
class CRectangle {
    private:
    int w, h;
    static int nTotalArea;
    static int nTotalNumber;
    public:
    CRectangle(int w_,int h_);
    ~CRectangle();
    static void PrintTotal();
};

CRectangle::CRectangle(int w_,int h_) {
    w = w_;
    h = h_;
    nTotalNumber ++;
    nTotalArea += w * h;
}
CRectangle::~CRectangle() {
    nTotalNumber --
    ;
    nTotalArea
    -= w * h;
}
void CRectangle::PrintTotal() {
  cout << nTotalNumber << "," << nTotalArea << endl;
}

int CRectangle::nTotalNumber = 0;
int CRectangle::nTotalArea = 0;
// 必须在定义类的文件中对静态成员变量进行一次说明
//或初始化。否则编译能通过，链接不能通过。
int main()
{
    CRectangle r1(3,3), r2(2,2);
    //cout << CRectangle::nTotalNumber; // Wrong , 私有
    CRectangle::PrintTotal();
    r1.PrintTotal();
    return 0;
}

输出结果：
2,13
2,13
```

#### 注意事项

在静态成员函数中，不能访问非静态成员变量，也不能调用非静态成员函数。

```
void CRectangle::PrintTotal()
{
  cout << w << "," << nTotalNumber << "," << nTotalArea << endl; //wrong
}
CRetangle::PrintTotal(); //解释不通，w 到底是属于那个对象的？
```

#### 与赋值构造函数联系例子

有何缺陷?
```
CRectangle::CRectangle(int w_,int h_)
{
    w = w_;
    h = h_;
    nTotalNumber ++;
    nTotalArea += w * h;
}
CRectangle::~CRectangle()
{
    nTotalNumber --;
    nTotalArea -= w * h;
}
void CRectangle::PrintTotal()
{
    cout << nTotalNumber << "," << nTotalArea << endl;
}
```

在使用CRectangle类时，有时会调用复制构造函数生成临时的隐藏的CRectangle对象
- 调用一个以CRectangle类对象作为参数的函数时，
- 调用一个以CRectangle类对象作为返回值的函数时
临时对象在消亡时会调用析构函数，减少nTotalNumber 和 nTotalArea的值，可是这些临时对象在生成时却没有增加nTotalNumber 和 nTotalArea的值。

解决办法：为CRectangle类写一个复制构造函数。
```
CRectangle :: CRectangle(CRectangle & r )
{
  w = r.w; h = r.h;
  nTotalNumber ++;
  nTotalArea += w * h;
}
```

### 3.5 成员对象和封闭类

#### 成员对象: 一个类的成员变量是另一个类的对象. 包含 成员对象 的类叫 封闭类 (Enclosing)
生成封闭类对象的语句 -> 明确 “对象中的成员对象”
```
class CTyre { //轮胎类
    private:
    int radius; //半径
    int width; //宽度
    public:
    CTyre(int r, int w):radius(r), width(w) { }
};
class CEngine {} //引擎类

class CCar { //汽车类->“封闭类”
    private:
      int price; //价格
      CTyre tyre;
      CEngine engine;
    public:
      CCar(int p, int tr, int tw);
};
CCar::CCar(int p, int tr, int w):price(p), tyre(tr, w){ // 初始化列表
};
int main(){
    CCar car(20000,17,225);
    // 如果 CCar 类不定义构造函数, 则
    // CCar car; -> 编译出错
    // car.engine 的初始化没有问题: 用默认构造函数(因为没参数)
    return 0;
}
```

#### 封闭类构造函数的初始化列表

定义封闭类的构造函数时, 添加初始化列表:

成员对象初始化列表中的参数
- 任意复杂的表达式
- 函数 / 变量/ 表达式中的函数, 变量有定义

```
类名::构造函数(参数表):成员变量1(参数表), 成员变量2(参数表), …
{
    …
}
```

#### 调用顺序

1. 当封闭类对象生成时,
- S1: 执行所有成员对象 的构造函数
- S2: 执行 封闭类 的构造函数
2. 成员对象的构造函数调用顺序
- 和成员对象在类中的说明顺序一致
- 与在成员初始化列表中出现的顺序无关
3. 当封闭类的对象消亡时,
- S1: 先执行 封闭类 的析构函数
- S2: 执行 成员对象 的析构函数
4. 析构函数顺序和构造函数的调用顺序相反


```
class CTyre {
    public:
    CTyre() { cout << "CTyre contructor" << endl; }
    ~CTyre() { cout << "CTyre destructor" << endl; }
};
class CEngine {
    public:
    CEngine() { cout << "CEngine contructor" << endl; }
    ~CEngine() { cout << "CEngine destructor" << endl; }
};

class CCar {
    private:
    CEngine engine;
    CTyre tyre;
    public:
    CCar( ) { cout << “CCar contructor” << endl; }
    ~CCar() { cout << "CCar destructor" << endl; }
};
int main(){
    CCar car;
    return 0;
}

程序的输出结果是：
CEngine contructor
CTyre contructor
CCar contructor
CCar destructor
CTyre destructor
CEngine destructor
```

### 3.6 友元

#### 友元函数
一个类的友元函数(包括构造, 析构函数)可以访问该类的私有成员

```
class CCar; //提前声明 CCar类, 以便后面CDriver类使用
class CDriver {
    public:
    void ModifyCar( CCar * pCar) ; //改装汽车
};
class CCar {
    private:
    int price;
    friend int MostExpensiveCar( CCar cars[], int total); //声明友元
    friend void CDriver::ModifyCar(CCar * pCar); //声明友元
};
void CDriver::ModifyCar( CCar * pCar)
{
    pCar->price += 1000; //汽车改装后价值增加
}
int MostExpensiveCar( CCar cars[], int total) //求最贵汽车的价格
{
    int tmpMax = -1;
    for( int i = 0; i < total; ++i )
    if( cars[i].price > tmpMax)
    tmpMax = cars[i].price;
    return tmpMax;
}
int main(){return 0;}
```

#### 友元类

A是B的友元类 -> A的成员函数可以访问B的私有成员. 友元类之间的关系, 不能传递, 不能继承

```
class CCar {
    private:
    int price;
    friend class CDriver; //声明CDriver为友元类
};
class CDriver {
    public:
    CCar myCar;
    void ModifyCar() { //改装汽车
        myCar.price += 1000; // CDriver是CCar的友元类可以访问其私有成员
    }
};
int main() { return 0; }
```

### 3.7 this指针

早期编译c++ 是先编译成C再通过C的编译器编译. 其作用就是指向成员函数所作用的对象

```
//C++
class CCar
{
    public:
    int price;
    void SetPrice
    (int p);
};
void CCar::SetPrice(int p){ price = p; }

int main() {
    CCar car;
    car.SetPrice(20000);
    return 0;
}

//C. 通过 this 指针指向对应结构体(即C++中的类实例)
struct CCar {
    int price;
};
void SetPrice(struct CCar * this, int p){
  this->price = p;
}
int main() {
    struct CCar car;
    SetPrice( & car, 20000);
    return 0;
}
```

#### this指针作用
非静态成员函数中可以直接使用this来代表指向该函数作用的对象的指针。

```
class Complex {
    public:
    double real, imag;
    void Print() { cout << real << "," << imag ; }
    Complex(double r,double i):real(r),imag(i){ }
    Complex AddOne() {
        this->real ++; //等价于 real ++;
        this->Print(); //等价于 Print
        return * this; // 返回对象自身
    }
};

int main() {
    Complex c1(1,1),c2(0,0);
    c2 = c1.AddOne(); //这里不是是复制构造函数吗,非初始化时
    return 0;
} //输出 2,1
```

另一个例子
```
class A{
    int i;
    public:
      void Hello() { cout << "hello" << endl; }
};
int main(){
    A * p = NULL;
    p->Hello(); //结果会怎样？
}

//会正常输出
// 翻译为 void Hello(A * this ) { cout << "hello" << endl; }
// Hello(p);
// 复合C的语法

//但如果在Hello中添加 i:
class A{
    int i;
  public:
    void Hello() { cout << i << "hello" << endl; }
  }; // 翻译为 void Hello(A * this ) { cout << this->i << "hello"<< endl; }
     //this若为NULL，则出错！！
  int main(){
    A * p = NULL;
    p->Hello();// 翻译为 Hello(p);
  } // 输出：hello
```

#### this指针和静态成员函数

静态成员函数中不能使用 this 指针！ 因为静态成员函数并不具体作用与某个对象!
因此，静态成员函数的真实的参数的个数，就是程序中写出的参数个数！

### 3.8 常量对象、常量成员函数和常引用

#### 常量对象
如果不希望某个对象的值被改变，则定义该对象的时候可以在前面加const关键字。

```
class Demo{
    private :
    int value;
    public:
    void SetValue() { }
};
const Demo Obj; // 常量对象
```

#### 常量成员函数
- 在类的成员函数说明后面可以加const关键字，则该成员函数成为常量成员函数。
- 常量成员函数执行期间不应修改其所作用的对象。因此，在常量成员函数中不能修改成员变量的值（静态成员变量除外），也不能调用同类的非常量成员函数(静态成员函数除外）。

```
class Sample{
    public:
      int value;
    void GetValue() const; //常量成员函数
    void func() { };
    Sample() { }
};
void Sample::GetValue() const{ //常量成员函数
    value = 0; // wrong
    func(); //wrong
}

int main() {
    const Sample o; //常量对象
    o.value = 100; //err.常量对象不可被修改
    o.func(); //err.常量对象上面不能执行非常量成员函数
    o.GetValue(); //ok,常量对象上可以执行常量成员函数
    return 0;
} //在Dev C++中，要为Sample类编写无参构造函数才可以，Visual Studio2010中不需要
```

#### 常量成员函数的重载
两个成员函数，名字和参数表都一样，但是一个是const,一个不是，算重载。
```
class CTest {
    private :
    int n;
    public:
    CTest() { n = 1 ; }
    int GetValue() const { return n ; }
    int GetValue() { return 2 * n ; }
};
int main() {
    const CTest objTest1;
    CTest objTest2;
    cout << objTest1.GetValue() << "," << objTest2.GetValue() ; //调用不同的成员函数
    return 0;
}
```

#### 常引用
引用前面可以加const关键字，成为常引用。不能通过常引用，修改其引用的变量

```
const int & r = n;
r = 5; //error
n = 4; //ok
```

常引用的作用:
对象作为函数的参数时，生成该参数需要调用复制构造函数，效率比较低。用指针作参数，代码又不好看，如何解决？
可以用对象的引用作为参数，如：

```
class Sample {
    …
};
void PrintfObj(Sample & o)
{
    ……
}
// 对象引用作为函数的参数有一定风险性，若函数中不小心修改了形参o，则实参也跟着变，这可能不是我们想要的。如何避免？

class Sample {
    …
};
void PrintfObj(const Sample & o)
{
    ……
}
```

## Chapter 4

### 4.1 运算符重载的基本概念

#### 基本运算符

C++预定义表示对数据的运算, 只能用于基本的数据类型:

```
+, -,*, /, %, ^, &, ~, !, |, =, <<, >>, != ……
```

#### 运算符重载

C++提供了数据抽象的手段: 例如用户自己定义数据类型 -- 类.  调用类的成员函数 -> 操作它的对象, 但很不方便. 例如在数学上, 两个复数可以直接进行+/-等运算, 但不能直接作用于两个负数类.

运算符重载使得对抽象数据类型也能够直接使用C++提供的运算符: 程序更简洁, 代码更容易理解.

例如:
- complex_a和complex_b是两个复数对象
- 求两个复数的和, 希望能直接写: `complex_a + complex_b`

#### 运算符重载的实质是函数重载
同一个运算符, 对不同类型的操作数, 所发生的行为不同.

在程序编译时:
- 把含 运算符的表达式 -> 对 运算符函数 的调用
- 把 运算符的操作数 -> 运算符函数的 参数
- 运算符被多次重载时, 根据 实参的类型 决定调用哪个运算符函数
- 运算符可以被重载成普通函数
- 也可以被重载成类的成员函数

```
返回值类型 operator 运算符（形参表）
{
    ……
}

//重载为普通函数, 参数个数为运算符目数
class Complex {
    public:
    Complex( double r = 0.0, double i= 0.0 ){
        real = r;
        imaginary = i;
    }
    double real; // real part
    double imaginary; // imaginary part
};

Complex operator+ (const Complex & a, const Complex & b)
{
    return Complex( a.real+b.real, a.imaginary+b.imaginary);
} // “类名(参数表)” 就代表一个对象

Complex a(1,2), b(2,3), c;
c = a + b; // 调用operator+(a, b)函数, 参数个数为2


// 重载为成员函数, 参数个数为运算符目数减一
class Complex {
    public:
    Complex( double r= 0.0, double m = 0.0 ):
    real(r), imaginary(m) { } // constructor
    Complex operator+ ( const Complex & ); // addition
    Complex operator- ( const Complex & ); // subtraction
    private:
    double real; // real part
    double imaginary; // imaginary part
};

Complex Complex::operator+(const Complex & operand2) { // Overloaded addition operator
    return Complex( real + operand2.real, imaginary + operand2.imaginary );
}

Complex Complex::operator- (const Complex & operand2){ // Overloaded subtraction operator
    return Complex( real - operand2.real, imaginary - operand2.imaginary );
}
int main(){
    Complex x, y(4.3, 8.2), z(3.3, 1.1);
    x = y + z; //等价于 x = y.opeator+(z)
    x = y - z; //等价于 x = y.operator-(z)
    return 0;
}
```

### 4.2 赋值运算符'='的重载

1. 赋值运算符 两边的类型 可以 不匹配
- 把一个 int类型变量 赋值给一个 Complex对象
- 把一个 char * 类型的字符串 赋值给一个 字符串对象
2. 需要 重载赋值运算符 ‘=’
3. 赋值运算符 “=” 只能重载为 成员函数

```
class String {
    private:
    char * str;
    public:
    String () : str(NULL) { } //构造函数, 初始化str为NULL
    const char * c_str() { return str; }
    char * operator = (const char * s);
    ~String( );
};

char * String::operator = (const char * s){ //重载 ‘=’  obj = “hello”能够成立
    if(str) delete [] str;
    if(s) { //s不为NULL才会执行拷贝
        str = new char[strlen(s)+1];
        strcpy(str, s);
    }
    else
    str = NULL;
    return str;
}
String::~String( ) {
    if(str) delete [] str;
};
int main(){
    String s;
    s = “Good Luck,” ;
    cout << s.c_str() << endl;
    // String s2 = “hello!”; //这条语句要是不注释掉就会出错, 因为调用的是赋值构造函数
    s = "Shenzhou 8!";
    cout << s.c_str() << endl;
    return 0;
}

// 程序输出结果：
// Good Luck,
// Shenzhou 8!
```

#### 重载赋值运算符的意义 – 浅复制和深复制

浅复制/浅拷贝
- 执行逐个字节的复制工作

深复制/深拷贝
- 将一个对象中指针变量指向的内容 -> 复制到另一个对象中指针成员对象指向的地方

```
MyString S1, S2;
S1 = “this”;
S2 = “that”;
S1 = S2;
```
