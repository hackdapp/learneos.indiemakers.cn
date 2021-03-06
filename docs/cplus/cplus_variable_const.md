# 基础数据类型及变量、常量定义

前一部分向大家展示了一个C++标准程序的大致组成部分。接下来我们将分开讲解每一部分内部的具体使用细节。在程序业务处理过程，往往对某一些数值做计算时，可能都需要一些临时内存地址用于存放一些要计算的原始数值，最后计算完成后再将数据值存储到一个新的地址。而在整个过程，我们要存放的数据所占用的物理空间大小是多少呢？在程序中如何使用内存中存放的数据呢? 包括不同业务场景中如何确定使用哪种数据类型呢？

## 基础数据类型

在业务场景，我可能需要对两个或多个数值进行一些数据运算，比如：相乘、相加、取余或者求平方等，或者我们可能需要存储某一段文字内容、或者我们需要对一些货币进行一些简单运算。应该如何去做呢？

这时候就需要大家对程序语言中的基础数据类型有一个初步的理解与认识，不过只需要搞明白以下几点就可以很很好的运用了

1）数据类型有哪些？
2）每种数据类型占用字节数是多少？
3）每种数值类型边界范围是多少

数据类型分为： char、wchar_t、int（short/long）、float、double、bool。

各个数据类型所占用字节大小如下：

|变量类型|占用字节|描述|数据范围|
|---|---|---|---|
|char|1|字符型 e.g. 'A' |signed: -2^8/22^8/2-1; unsigned: 0  2^8|
|short|2|短整型|signed: 2^16/2  2^16/2-1 usigned: 0  2^16-1|
|long|4|长整型|signed: 2^32/2  2^32/2-1 usigned: 0  2^32-1|
|int|4|视操作系统不同可能占用字节不同。MSDOS下为2字节；而现今的32或64位系统为4字节|2字节则和short边界相同;4字节则和long边界相同|
|float|4|浮点型字段，多用于处理精度要求不高的运算，比如简单的百分比计算、平方根、正余弦等|3.4e + / - 38 (7 digits)|
|double|8|多用于精度要求高的运算。|1.7e + / - 308 (15 digits)|
|long double|10|bool|1|wechar_t|2


除此之外，还有枚举类型。枚举类型(enumeration)是C
比如：

我们定义`数据状态`字典, 可以用以下形式表示:

`c++
enum RunStatus { ready = 0, running = 1, pause = 2, destory = 3};
`

## 变量定义

关于变量的定义，主要由三部分组成：

`
<数据类型> <变量名称> = <初始值>;
or
<数据类型> <变量名称> (<初始值>);
`

**数据类型**：可以为除了上面介绍的基础数据类型之外，也可以用我们自定义数据结构体或标准库中提供的数据结构。

**变量名称**：变量的名称在程序也不是随意乱取的，而是由字母、数字、下划线三部分组成，对于名称的长度，根据系统的不同也会有所不同。除此之外， 变量名称开头第一个字不允放为数字。

**初始值**： 变量的初始化可以分为两种：定义时直接初始化或者先定义后续初始化。两种初始化方式最终效果并无不同，只是表现形式不同而已。

代码示例如下:

`
//1. 直接初始化
int a = 5;
or
int a (5)

//2. 间接初始化
int a;
a = 5;
`

如果存在同一类型的多变量定义，那么可以使用如下形式进行定义, 可以简化程序代码。

代码示例如下：

`
int a, b, c;
`

## 常量定义

常量，其实与枚举功能相同，均作为字典数据使用，将一个数字或字符串对应到一个容易被大家所理解的名称上。只不过常量只有一种状态，枚举可以存在多种状态。

常量主要用于存储一个固定值，一定初始化之后是不允许再次修改，供整个程序代码中直接调用，防制`魔术数字`问题的产出，从而提供代码的可读性。

常量的定义方式，有两种：

### 1. `const <数据类型> <常量名称> = <初始值>`

代码示例如下:

`
const int status = 1;
或者¡
const int status (1);    
`

### 2. `#define <常量名> <初始值>`
define往往用于给某个特定常量值定义一个便于理解且操作的别名定义。常定义于文件开头处。

代码示例如下:

`
#include <iostream>
#define PI 3.14159265

int main()
{
    float r = 3.1;
    float val = PI*r^2;
    cout << val << endl;
    return 0;
}
`

另外，按照编码规范，常量的命名往往以大写字母定义。

## 作用域
变量定义在程序中的不同位置，直接决定了它的作用域范围不同，即可被访问的范围。通常我们讨论的作用域，主要为以下三种
- 条件语句代码块中
- 函数块内
- 函数块外

根据不同的作用域，可将变量分为全局或本地变量：

### 本地变量
定义在函数体内或代码区块中的变量统称为本地变量。本地变量不允许函数体外的程序进行访问。

示例如下:

```cpp
#include <iostream>
using namespace std;

int main()
{
	//本地变量
	int a = 19;

	return 0;
}
```


### 全局变量
定义在函数体外的变量
