![]()变量和基本类型

## 基本内置类型

### 算术类型

整型和浮点型

|     类型      |      含义      |   最小尺寸   |
| :-----------: | :------------: | :----------: |
|    `bool`     |    布尔类型    |    未定义    |
|    `char`     |      字符      |     8位      |
|   `wchar_t`   |     宽字符     |     16位     |
|  `char16_t`   |  Unicode字符   |     16位     |
|  `char32_t`   |  Unicode字符   |     32位     |
|    `short`    |     短整型     |     16位     |
|     `int`     |      整型      |     16位     |
|    `long`     |     长整型     |     32位     |
|  `long long`  |     长整型     |     64位     |
|    `float`    |  单精度浮点数  | 6位有效数字  |
|   `double`    |  双精度浮点数  | 10位有效数字 |
| `long double` | 扩展精度浮点数 | 10位有效数字 |

一个char的大小和一个机器字节一样。

一个int至少和一个short一样大，一个long至少和一个int一样大，一个long long至少和一个long一样大。long long在C++11中定义。

通常，float以1个字（32比特）来表示，double以2个字（64比特）来表示，long double以3或4个字（96或128比特）来表示。类型float和double分别有7和16个有效位。

> 大多数计算机将内存中的每个字节与一个数字(被称为“地址(address))关联起来。
>
> ![](.\Picture\Address.png)



### 类型转换

非布尔类型的算术值赋给布尔类型时，0为false，其他为true
布尔值赋给非布尔类型时，false为0，true为1
浮点数赋给整数类型时，近似处理，仅保留浮点数中小数点之前的部分
整数值赋给浮点类型时，小数部分记为 0
赋给无符号类型一个超出它表示范围的值时，结果是初始值对无符号类型表示数值总数取模后的余数
当我们赋给带符号类型一个超出它表示范围的值时，结果是未定义的(undefined)
算数表达式既有无符号数又有int值时，int就会转换成无符号数
**勿混用带符号类型和无符号类型**

### 字面值常量

形如42的值被称为**字面值常量**。

`20	/*十进制*/`			`024	/*八进制*/`		`0x14	/*十六进制*/`

十进制字面值是带符号数，八进制、十六进制字面值既可能是带符号的也可能是无符号的。
十进制字面值是int、long和long long中尺寸最小者
八进制和十六进制是int、unsigned int、long、 unsigned long、 long long、unsigned long long中的尺寸最小者
严格说，十进制字面值不会是负数，负号的作用只是对字面值取负值

`'a'			// 字符字面值`		`"Hello World！"			// 字符串字面值`

单引号包裹的一个字符，称为char型字面值
双引号包裹的0个或多个字符称为字符串型字面值
字符串字面值类型是由常量字符构成的数组
编译器在字符串后添加一个空字符('\0')，实际长度+1

> 换行符	\n			纵向制表符	\v			反斜线	\\\\
> 回车符	\r			横向制表符	\t			退格符	\b
> 问号	\?				进纸符	\f					报警(响铃)符	\a
> 双引号	\\"			单引号	\\'

转义字符：不可打印的字符；在C++中有特殊含义的字符

> \7(响铃)			\12(换行符)			\115(字符M)
> \0(空字符)		\40(空格)				\x4d (字符M)

泛化转义序列：\x后跟1个或多个十六进制数字；\后跟1个、2个或3个八进制数字

> L'a'										// 宽字符型字面值，类型是wchar_t
> u8"hi!"									//utf-8字符串字面值(utf-8用8位编码一个Unicode字符)
> 42ULL									// 无符号整型字面值，类型是unsigned long long
> 1E-3F									// 单精度浮点型字面值，类型是 float
> 3.14159L								// 扩展精度浮点型字面值，类型是 long double

<img src=".\Picture\指定字面值的类型.png" style="zoom:50%;" />



## 变量

### 变量初始化（变量定义）

初始化不是赋值，初始化是创建变量时赋予一个初始值，赋值是把对象当前值删除，以一个新值来代替。

**列表初始化：**

```c++
int units_sold = 0;
int units_sold = {0};			// 列表初始化
int units_sold{0};				// 列表初始化
int units_sold(0);
```

使用列表初始化，且初始化有丢失信息的风险，编译器会报错。

**默认初始化：**
默认初始化的值，由变量类型决定，定义变量的位置也会有影响。
定义在函数体内的内置类型的对象如果没有初始化，其值未定义。
类的对象没有显式初始化，其值由类确定。

### 变量声明和定义的关系

声明：让名字为程序所知
定义：负责创建与名字关联的实体

如果想声明变量而不是定义，在变量前添加关键字extern。
在函数体内部，试图初始化一个extern关键字标记的变量，会报错。



### 标识符

标识符要求：

1. 由字母、数字和下画线组成
2. 必须以字母或下画线开头
3. 标识符的长度没有限制，但是对大小写字母敏感
4. 自定义标识符不能出现连续两个下划线
5. 不能以下划线紧跟大写字母开头
6. 函数体外的标识符不能以下划线开头



### 名字的作用域

全局作用域
块作用域：内层作用域、外层作用域



## 复合类型

### 引用

引用为对象起了另一个名称，引用即别名
定义引用时，程序把引用和初始值绑定在一起，因此无法令引用重新绑定另外一个对象，引用必须初始化
引用只能绑定在对象上，不能与字面值或某个表达式的i计算结果绑定在一起。

### 指针

指针是指向另外一种类型的复合类型。

**指针与引用的异同:**
	相同：
		指针和引用实现了对其他对象的间接访问。
	不同：
		指针本身就是一个对象，允许对指针赋值和拷贝，而且在指针的生命周期内它可以先后指向几个不同的对象
		指针无须在定义时赋初值
		和其他内置类型一样，在块作用域内定义的指针如果没有被初始化，也将拥有一个不确定的值

**获取对象的地址：**
	取地址符&

```c++
	int ival = 42;
	int *p = &ival;
```

**利用指针访问对象：**
解引用符：

```c++
int ival = 42;
int *p = &ival;	
cout << *p;		// 通过解引用符*得到指针p指的对象
```

赋值：

```c++
*p = 0;			//给指针所指的对象赋值
cout << *p;
```

**空指针：**nullptr

### 理解复合类型的声明

```C++
//i是一个int型的数，p是一个int型指针，r是一个int型引用
int i = 1024，*p = &i，&r = i;

int* p1, p2;	// p1是指向int的指针，p2是int
```

**指向指针的指针：**

```c++
int ival = 1024;
int *pi = &ival;//pi指向一个int型的数
int **ppi = &pi;//ppi指向一个int型的指针
```

<img src=".\Picture\指向指针的指针.png" style="zoom:50%;" align="left"/>

**指向指针的引用：**
引用本身不是对象，不存在指向引用的指针。指针是对象，存在对指针的引用。

```c++
int i = 42;
int *p;				//p是一个int型指针
int *&r = p;		//r是一个对指针p的引用

r = &i;				//r引用了一个指针，因此给r赋值&i就是令p指向i
*r = 0;				//解引用r得到i，也就是p指向的对象，将i的值改为0
```

从右到左阅读r的定义

## const限定符

const 对象一旦创建后其值不能再改变，所以必须初始化。
只能在const类型的对象上执行不改变其内容的操作。

默认状态下，const对象**只在文件内有效**。
多个文件出现同名的const变量时，等同于在不同文件中分别定义独立的变量。

当需要在多个文件中使用同一个const时，需要加入extern关键字。

### const引用

对常量的引用不能修改它所绑定的对象：

```c++
const int ci = 1024;
const int &r1 = ci;			//正确:引用及其对应的对象都是常量
r1 = 42;					//错误:r1是对常量的引用
int &r2 = ci;				//错误:试图让一个非常量引用指向一个常量对象
```

引用类型必须与其引用对象的类型一致
例外情况：
	在初始化常量引用时，允许任意表达式作为初始值，只要表达式结果可以转换成引用的类型即可。

```c++
int i = 42:					
const int &r1 = i;			//允许将const int&绑定到一个普通int对象上
const int &r2 = 42;			//正确:r1是一个常量引用

const int &r3 = r1 * 2;		//正确:r3是一个常量引用
// 相当于
const int temp = r1 * 2;	//生成一个临时的整型常量
const int &r3 = temp;		//让r3绑定这个临时量

int &r4 = r1 * 2;			//错误:r4是一个普通的非常量引用
```

对const的引用可能引用一个并非const的对象

### 指针和const

指向常量的指针不能用于改变其所指对象的值

```c++
const double pi = 3.14;					//pi是个常量，它的值不能改变
double* ptr = &pi;						//错误:ptr是一个普通指针
const double *cptr = &pi;				//正确:cptr可以指向一个双精度常量
*cptr = 42;								//错误:不能给*cptr赋值
```

**const指针**

常量指针必须初始化，而且之后不能改变其值。
将*放在const之前用以说明指针是一个常量，不变的是指针本身而非指向的那个值。

```c++
int errNumb = 0;
int *const curErr = &errNumb;			// curErr将一直指向errNumb
const double pi = 3.14159;
const double *const pip = &pi;			// pip是一个指向常量对象的常量指针
```

### 顶层const

顶层const表示指针本身是一个常量；
	顶层const可以表示任意的对象是常量
底层const表示指针所指的对象是一个常量
	底层const与指针和引用等复合类型的基本类型部分有关

```c++
inti = 0;
int *const p1 = &i;				//不能改变p1的值，这是一个顶层const
const int ci = 42;				//不能改变ci的值，这是一个顶层const
const int *p2 = &ci;			//允许改变p2的值，这是一个底层const
const int *const p3 = p2;		//靠右的const是顶层const，靠左的是底层const
const int&r = ci;				//用于声明引用的const都是底层const

i = ci;							//正确:拷贝ci的值，ci是一个顶层const，对此操作无影响
p2 = p3;						//正确:p2和p3指向的对象类型相同，p3顶层const 的部分不影响

int *p = p3;					//错误:p3包含底层const 的定义，而p没有
p2 = p3;						//正确:p2和p3都是底层const
p2 = &i;						//正确:int*能转换成const int*
int &r = ci;					//错误:普通的int&不能绑定到int常量上
const int &r2 = i;				//正确:const int&可以绑定到一个普通int上
```

### constexpr和常量表达式

常量表达式指值不会改变并且在编译过程就能得到计算结果的表达式。

```c++
const int max files = 20;				//max_files是常量表达式
const int limit = max_files + 1;		//limit是常量表达式

//由于staff_size的数据类型只是一个普通int而非const int，所以它不属于常量表达式
int staff_size=27;						//staff_size不是常量表达式

//sz 本身是一个常量，但它的具体值直到运行时才能获取到，所以也不是常量表达式
const int sz = get_size();				//sz不是常量表达式
```

**constexpr变量**
C++11规定，允许将变量声明为constexpr类型，编译器会判断变量的值是否是常量表达式。

```c++
constexpr int mf = 20;						//20是常量表达式
constexpr int limit = mf + 1;				//mf+I是常量表达式
constexpr int sz = size();					//只有当 size是一个constexpr函数时
											//才是一条正确的声明语句
```

**字面值类型**
算术类型、引用和指针属于字面值类型

**指针和constexpr**
在constexpr声明中如果定义一个指针，限定符constexpr**仅对指针有效**，与指针所指的对象无关:

```c++
const int *p = nullptr;				// P是一个指向整型常量的指针
constexpr int *q = nullptr; 		// q是一个指向整数的常量指针

constexpr int *np = nullptr; 		// np是一个指向整数的常量指针，其值为空
int j = 0;
constexpr int i = 42;				// i的类型是整型常量
// i和j都必须定义在函数体之外
constexpr const int *p = &i;		// p是常量指针，指向整型常量i
constexpr int *p1 = &j;				// p1是常量指针，指向整数j
```

## 处理类型

### 类型别名

类型别名是某种类型的同义词。
有两种方法定义类型别名：
	使用关键字typedef
	使用别名声明

```c++
typedef double wages;			//wages是double的同义词
typedef wages base, *p; 		//base是double的同义词，p是double*的同义词

using SI = Sales_item;			//SI是Sales_item的同义词

wages hourly, weekly;			//等价于double hourly、weekly;
SI item;						//等价于Salesitem item
```

**指针、常量和类型别名**

```c++
typedef char *pstring;		// pstring实际是类型char*的别名，pstring是指向char的指针
const pstring cstr = 0;		// cstr是指向char的常量指针
const pstring *ps;			// ps是一个指针，它的对象是指向char的常量指针
```

### auto类型说明符

c++11引入auto可以让编译器判断表达式所属类型。
auto定义的变量必须有初始值。
auto一条语句可以声明多个变量，一条声明语句只能有一个基本数据类型，该语句中的所有变量初始类型必须**相同**

```c++
// 由val1和val2相加的结果可以推断出item的类型
auto item = val1 + val2;			//item初始化为val1和val2相加的结果

auto i = 0, *p = &i;				//正确:i是整数、p是整型指针
auto sz = 0, pi = 3.14; 			//错误:sz和pi的类型不一致
```

**复合类型、常量和auto**

```c++
int i = 0, &r = i;
auto a = r;			//a是一个整数(r是i的别名，而i是一个整数)

const int ci = i, &cr = ci;		
auto b = ci;					// b是一个整数(ci的顶层const特性被忽略掉了)
auto c = cr;					// c是一个整数(cr是ci的别名，ci本身是一个顶层const)
auto d = &i;					// d是一个整型指针(整数的地址就是指向整数的指针)
auto e = &ci; 					// e是一个指向整数常量的指针(对常量对象取地址是一种底层 const)
```

如果希望推断出的auto类型是一个顶层const，需要明确指出：

```c++
const auto f = ci;				// ci的推演类型是int，f是const int
auto &g = ci;					// g是一个整型常量引用，绑定到ci
auto &h = 42;					// 错误:不能为非常量引用绑定字面值
const auto &j = 42;				// 正确:可以为常量引用绑定字面值
```

在一条语句中定义多个变量，符号&和*只从属于某个声明符，而非基础数据类型的一部分，初始值必须是同一种类型

```c++
auto k = ci, &l = i;			// k是整数，l是整型引用
auto &m = ci, *p = &ci;			// m是对整型常量的引用，p是指向整型常量的指针
auto &n = i, *p2 = &ci;			// 错误:i的类型是int而&ci的类型是const int
```

### decltype类型指示符

C++11引入decltype，作用是选择并返回操作数的数据类型
编译器分析表达式并得到它的类型，不实际计算表达式的值

```c++
decltype(f()) sum = x;			//sum的类型就是函数 f的返回类型

```

decltype 使用的表达式是一个变量，则 decltype 返回该变量的类型(包括顶层 const 和引用在内):

```c++
const int ci = 0, &cj = ci;
decltype(ci) x = 0;				// x的类型是const int
decltype(cj) y = x;				// y的类型是const int&，y绑定到变量x
decltype(cj) z;					// 错误:z是一个引用，必须初始化

```

**decltype和引用**

```c++
//decltype的结果可以是引用类型
int i = 42, *p = &i, &r = i;
decltype(r+0) b; 				// 正确:加法的结果是int，因此b是一个(未初始化的)int
decltype(*p) c;					//错误:c是int&，必须初始化

// decltype的表达式如果是加上了括号的变量，结果将是引用
decltype((i)) d;				//错误:d是int&，必须初始化
decltype(i) e;					//正确:e是一个(未初始化的)int
```

<u>decltype((variable))(注意是双层括号)的结果永远是引用，而decltype(variable)结果只有当 variable 本身就是一个引用时才是引用。</u>



## 自定义数据结构

### 定义Sales_data类型

```c++
struct Sales_data {
	std::string bookNo;
	unsigned units_sold = 0;
	double revenue = 0.0;
};

// 类体右侧的表示结束的花括号后必须写一个分号，这是因为类体后面可以紧跟变量名以示对该类型对象的定义，所以分号必不可少:
struct Sales_data { /* ... */} accum, trans, *salesptr;
struct Sales_data { /* ... */};
Sales_data accum, trans, *salesptr;
```

数据成员：
	定义类对象的具体内容。
	C++11规定，可以为数据提供类内初始值(in-class initializer)，没有初始值的成员被默认初始化。

### 编写自己的头文件

为了确保各个文件中类的定义一致，类通常被定义在头文件中，而且类所在头文件的名字应与类的名字一样。
头文件通常包含那些只能被定义一次的实体，如类、const 和 constexpr 变量(参见2.4节,第54页)等头文件也经常用到其他头文件的功能。
头文件一旦改变，相关的源文件必须重新编译以获取更新过的声明。

**预处理器概述**
	预处理器是在编译之前执行的一段程序，可以部分地改变我们所的程序。
	头文件保护符(header guard)：
		头文件保护符依赖于预处理变量
		预处理变量有两种状态:已定义和未定义。
			#define 指令把一个名字设定为预处理变量
			#ifdef当且仅当变量已定义时为真
			#ifndef 当且仅当变量未定义时为真。
			一旦检查结果为真，则执行后续操作直至遇到#endif指令为止

​	预处理变量无视 C++语言中关于作用域的规则

```c++
#ifndef SALES_DATA_H
#define SALES_DATA_H
#include<string>
struct Sales_data{
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
#endif
```



# 字符串、向量和数组

## 命名空间的using声明

`using namespace::name;`

```c++
#include <iostream>
//using声明，当我们使用名字cin时，从命名空间 std中获取它
using std::cin;

int main()
{
	int i;
    cin >> i;		//正确:cin和std::cin含义相同
    cout << i;		//错误:没有对应的using声明，必须使用完整的名字
    std::cout << i;	//正确:显式地从std中使用cout
    return 0;    
}
```

**每个名字都需要独立的using声明**
**头文件不应包含using声明**

## 标准库类型string

`#include <string>`

### 定义和初始化string对象

```c++
string s1;				// 默认初始化，s1是一个空字符串
string s2 = s1;			// s2是s1的副本
string s3 = "hiya";		// s3是该字符串字面值的副本
string s4(10, 'c');		// s4的内容是 cccccccccc
```

| 初始化string对象的方式 | 实例                                                  |
| ---------------------- | ----------------------------------------------------- |
| `string s1`            | 默认初始化，s1是一个空串                              |
| `string s2(s1)`        | s2是s1的副本                                          |
| `string s2 = s1`       | 等价于s2(s1)，s2是s1的副本                            |
| `string s3("value")`   | s3是字面值“value”的副本，除了字面值最后的那个空字符外 |
| `string s3 = "value"`  | 等价于s3("value")，s3是字面值“value”的副本            |
| `string s4(n, 'c')`    | 把s4初始化为由连续n个字符c组成的串                    |

直接初始化：如果不使用等号，执行的是直接初始化
拷贝初始化：使用等号，把等号右侧的初始值拷贝到新创建的对象中

```c++
string s5 = "hiya";			// 拷贝初始化
string s6("hiya");			// 直接初始化
string s7(10, 'c');			// 直接初始化，s7的内容是 cccccccccc
string s8 = string(10, 'c');// 拷贝初始化，s8的内容是 cccccccccc
```

### string对象上的操作

| string的操作               | 说明                                                         |
| -------------------------- | ------------------------------------------------------------ |
| `os << s`                  | 将s写到输出流os当中，返回os                                  |
| `is >> s`                  | 从is中读取字符串赋给s，字符串以空白分隔，返回is              |
| `getline(is, s)`           | 从is中读取一行赋给s，返回is                                  |
| `s.empty()`                | s为空返回true，否则返回 false                                |
| `s.size()`                 | 返回s中字符的个数                                            |
| `s[n]`                     | 返回s中第n个字符的引用，位置n从0计起                         |
| `s1 + s2`                  | 返回s1和s2连接后的结果                                       |
| `s1 = s2`                  | 用s2的副本代替s中原来的字符                                  |
| `s1 == s2`<br />`s1 != s2` | 如果s1和s2中所含的字符完全一样，则它们相等;string对象的相等性判断对字母的大小写敏感 |
| `<, <=, >, >=`             | 利用字符在字典中的顺序进行比较，且对字母的大小写敏感         |

**读写string对象**

```c++
//注意：要想编译下面的代码需要适当的#include 和 using
//在执行读取操作时，string 对象会自动忽略开头的空白(即空格符、换行符、制表符等)并从第一个真正的字符开始读起，直到遇见下一处空白为止。
//如果程序的输入是“Hello World!(注意开头和结尾处的空格)，则输出将是“Hel1o”，输出结果中没有任何空格。
int main()
{
	string s;				// 空字符串
    cin >> s;				// 将string对象读入s，遇到空白停止
    cout << s << endl;		// 输出s
    return 0;
}

// 输入内容“Hello World!”， 输出将是 "HelloWorld!"
string s1，s2;
cin >> sl >> s2;			// 把第一个输入读到s1中，第二个输入读到s2中
cout << sl << s2 << endl;	// 输出两个string对象
```

**读取未知数量的string对象**

```c++
int main()
{
	string word;			
	while (cin >>word)			//反复读取，直至到达文件末尾
        cout << word << endl;	//逐个输出单词，每个单词后面紧跟一个换行
   	return 0;
}
```

**使用getline读取一整行**
getline只要遇到换行符就结束读取操作并返回结果，返回的字符串不包含换行符

```c++
int main()
{
	string line;
    // 每次读入一整行，直至到达文件末尾
    while (getline(cin， line))
		cout << line << endl;
    return 0;    
}
```

**string的empty和size操作**

```c++
// 每次读入一整行，遇到空行直接跳过
while (getline(cin， line))
    if (!line.empty())
		cout << line<<endl;

string line;
// 每次读入一整行，输出其中超过 80个字符的行
while (getline(cin，line))
    if (line.size() > 80)
		cout << line << endl;
```

**string::size_type类型**
size函数返回的是string::size_type类型

配套的标准库类型与机器无关，类型 size_type 即是其中的一种
在具体使用的时候，通过作用域操作符来表明名字size_type是在类string 中定义的

表达式中如果有size()函数，不要使用int，避免混用int和unsigned带来的问题

**比较string对象**
	如果两个string对象的长度不同，而且较短string 对象的每个字符都与较长string对象对应位置上的字符相同，则较短string对象小于较长string对象。
	如果两个string对象在某些对应的位置上不一致，则string对象比较的结果其实是string对象中第一对相异字符比较的结果。

 **为string对象赋值**

```c++
string st1(10, 'c'), st2;			// st1的内容是cccccccccc; st2是一个空字符串
st1 = st2;							// 赋值:用st2的副本替换st1的内容
									// 此时st1和st2都是空字符串
```

**两个string对象相加**

```c++
string s1 = "hello, ", s2 = "world\n";
string s3 = s1 + s2;				// s3的内容是hello，world\n
s1 += s2;							// 等价于s1 = s1 + s2
```

**字面值和string对象相加**

```c++
string s1 = "hello", s2 = "world";		// 在sl和s2中都没有标点符号
string s3 = s1 + ", " + s2 + '\n';		

string s4 = s1 + ", ";					// 正确:把一个string 对象和一个字面值相加
string s5 = "hello" + ", ";				// 错误:两个运算对象都不是string
string s6 = s1 + ", " + "world";		// 正确:每个加法运算符都有一个运算对象是 string
string s7 = "hello" + ", " + s2;		// 错误：不能把字面值直接相加
```

C++字面值和string是不同的类型

### 处理string对象中的字符

| cctype头文件中的函数 | 说明                                                         |
| :------------------: | :----------------------------------------------------------- |
|     `isalnum(c)`     | 当c是字母或数字时为真                                        |
|     `isalpha(c)`     | 当c是字母时为真                                              |
|     `iscntrl(c)`     | 当c是控制字符时为真                                          |
|     `isdigit(c)`     | 当c是数字时为真                                              |
|     `isgraph(c)`     | 当c不是空格但可打印时为真                                    |
|     `islower(c)`     | 当c是小写字母时为真                                          |
|     `isprint(c)`     | 当c是可打印字符时为真(即c是空格或c具有可视形式)              |
|     `ispunct(c)`     | 当c是标点符号时为真(即c不是控制字符、数字、字母、可打印空白中的一种) |
|     `isspace(c)`     | 当c是空白时为真(即c是空格、横向制表符、纵向制表符、回车符、换行符、进纸符中的一种) |
|     `isupper(c)`     | 当c是大写字母时为真                                          |
|    `isxdigit(c)`     | 当c是十六进制数字时为真                                      |
|     `tolower(c)`     | 如果c是大写字母，输出对应的小写字母;否则原样输出c            |
|     `toupper(c)`     | 如果c是小写字母，输出对应的大写字母:否则原样输出c            |

**范围for语句**
用于处理每个元素

```c++
string str("some string");
//每行输出str中的一个字符
for(auto c : str)			// 对于str中的每个字符
	cout << c << endl;		// 输出当前字符，后面紧跟一个换行符

string s("Hello World!!!");
// punct_cnt的类型和s.size的返回类型一样
decltype(s.size()) punct_cnt = 0;
// 统计s中标点符号的数量
for (auto c : s)				// 对于s中的每个字符
    if (ispunct(c))				// 如果该字符是标点符号
        ++punctcnt;				// 将标点符号的计数值加1
cout << punctcnt << " punctuation characters in " << s << endl;	// 3 punctuation characters in Hello World!!!

string s("Hello World!!!");
//转换成大写形式
for(auto &c : s)			// 对于s中的每个字符(注意:c是引用)
	c = toupper(c);			// c是一个引用，因此赋值语句将改变s中字符的值
cout << s << endl;			// HELLO WORLD!!!
```

**使用下标进行迭代**

```c++
//依次处理s中的字符直至我们处理完全部字符或者遇到一个空白
for (decltype(s.size()) index = 0; index != s.size() && !isspace(s[index]); ++index)
    s[index] = toupper(s[index]);//将当前字符改成大写形式
```

**使用下标执行随机访问**

```c++
const string hexdigits = "0123456789ABCDEF";		// 可能的十六进制数字
cout << "Enter a series of numbers between 0and 15" 
    << " separated by spaces. Hit ENTER when finished: "
    << endl;
string result;			// 用于保存十六进制的字符串
string::sizetype n;		// 用于保存从输入流读取的数
while (cin >> n)
    if (n < hexdigits.size())		// 忽略无效输入
        result += hexdigits[n]; 	// 得到对应的十六进制数字

cout << "Your hex number is: " << result << endl;
//Input: 12 0 5 15 8 15
//Output: Your hex number is: C05F8F
```

## 标准库类型vector

vector是一个类模板，可以将模板看成编译器生成类或者函数编写的一份说明。
编译器根据模板创建类或函数的过程称为实例化。

### 定义和初始化vector对象

| 初始化vector对象的方法        | 说明                                                    |
| ----------------------------- | ------------------------------------------------------- |
| `vector<T> v1`                | v1是一个空vector，它潜在的元素是T类型的，执行默认初始化 |
| `vector<T> v2(v1)`            | v2中包含有v1所有元素的副本                              |
| `vector<T> v2 = v1`           | 等价于v2(v1)，v2中包含有v1所有元素的副本                |
| `vector<T> v3(n, val)`        | v3包含了n个重复的元素，每个元素的值都是val              |
| `vector<T> v4(n)`             | v4包含了n个重复地执行了值初始化的对象                   |
| `vector<T> v5{a, b, c...}`    | v5包含了初始值个数的元素，每个元素被赋予相应的初始值    |
| `vector<T> v5 = {a, b, c...}` | 等价于v5{a,b,c...}，列表初始化                          |

```c++
vector<int> v1(10);			// v1有10个元素，每个的值都是0
vector<int> v2{10};			// v2有1个元素，该元素的值是10

vector<int> v3(10，1);		// v3有10个元素，每个的值都是1
vector<int> v4{10，1};		// v4有2个元素，值分别是10和1

vector<string> v5{"hi"};		// 列表初始化:v5有一个元素
vector<string> v6("hi");		// 错误:不能使用字符串字面值构建vector 对象
vector<string> v7{10};			// v7有10个默认初始化的元素
vector<string> v8{10, "hi");	// v8有10个值为"hi"的元素
```

### 向vector对象中添加元素

```c++
vector<int> v2; //空vector对象
for(int i = 0; i != 100; ++i)
	v2.push_back(i);//依次把整数值放到v2尾端
//循环结束后v2有100个元素，值从0到99


//从标准输入中读取单词，将其作为vector对象的元素存储
string word;
vector<string> text;		//空vector 对象
while (cin >> word) {
    text.push_back(word);	//把 word添加到 text后面
}
```

不能用下标添加元素

```c++
vector<int> ivec;						//空vector对象
for (decltype(ivec.size()) ix = 0; ix != 10; ++ix)
	ivec[ix] = ix;//严重错误:ivec不包含任何元素

for (decltype(ivec.size()) ix = 0; ix != 10; ++ix)
    ivec.push_back(ix); // 正确:添加一个新元素，该元素的值是 ix
```



## 迭代器介绍

### 使用迭代器

获取迭代器不是使用取地址符，有迭代器的类型同时拥有返回迭代器的成员
这些类型都拥有名为 begin和end 的成员，
	begin 成员负责返回指向第一个元素(或第一个字符)的迭代器
	end成员则负责返回指向容器(或string对象)“尾元素的下一位置 (one past the end)”的迭代器
		该迭代器指示的是容器的一个本不存在的“尾后 (off the end)”元素
		这样的迭代器仅是个标记而已，表示我们已经处理完了容器中的所有元素

```c++
//由编译器决定b和e的类型;参见2.5.2节(第61页)
//b表示v的第一个元素，e表示v尾元素的下一位置
auto b = v.begin(), e = v.end();			//b和e的类型相同
```

**迭代器运算符**

| 标准容器迭代器的运算符             | 作用                                                         |
| ---------------------------------- | ------------------------------------------------------------ |
| *iter                              | 返回迭代器iter所指元素的引用                                 |
| iter->mem                          | 解引用iter并获取该元素的名为mem的成员，等价于(*iter).mem     |
| ++iter                             | 令iter指示容器中的下一个元素                                 |
| --iter                             | 令iter指示容器中的上一个元素                                 |
| iter1 == iter2<br />iter1 != iter2 | 判断两个迭代器是否相等(不相等)，如果两个迭代器指示的是同一个元素或者它们是同一个容器的尾后迭代器，则相等;反之，不相等 |

**迭代器类型**
拥有迭代器的标准库类型使用**iterator**和**const_iterator**来表示迭代器的类型:

```c++
vector<int>::iterator it;			//it能读写vector<int>的元素
string::iterator it2;				//it2能读写string对象中的字符
vector<int>::const_iterator it3;	// it3只能读元素，不能写元素
string::const_iterator it4;			// it4只能读字符，不能写字符
```

​	***但凡是使用了迭代器的循环体，都不要向迭代器所属的容器添加元素***

### 迭代器运算

| vector和string迭代器支持的运算 | 操作                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| iter + n                       | 迭代器加上一个整数值仍得一个迭代器，迭代器指示的新位置与原来相比向前移动了若干个元素。结果迭代器或者指示容器内的一个元素，或者指示容器尾元素的下一位置 |
| iter - n                       | 迭代器减去一个整数值仍得一个迭代器，迭代器指示的新位置与原来相比向后移动了若干个元素。结果迭代器或者指示容器内的一个元素，或者指示容器尾元素的下一位置 |
| iter1 += n                     | 迭代器加法的复合赋值语句，将iter1加n的结果赋给iter1          |
| iter1 -= n                     | 迭代器减法的复合赋值语句，将iter1减n的结果赋给iter1          |
| iter1 - iter2                  | 两个迭代器相减的结果是它们之间的距离，也就是说，将运算符右侧的迭代器向前移动差值个元素后将得到左侧的迭代器。参与运算的两个迭代器必须指向的是同一个容器中的元素或者尾元素的下一位置 |
| >、 >=、 <、 <=                | 迭代器的关系运算符，如果某迭代器指向的容器位置在另一个迭代器所指位置之前，则说前者小于后者。参与运算的两个迭代器必须指向的是同个容器中的元素或者尾元素的下一位置 |

## 数组

数组大小固定

### 定义和初始化内置数组

```c++
unsigned cnt = 42;			// 不是常量表达式
constexpr unsigned sz = 42;	// 常量表达式，关于constexpr，参见2.4.4节(第59页)
int arr[10];				// 含有10个整数的数组
int* parr[sz];				// 含有42个整型指针的数组
string bad[cnt];			// 错误:cnt不是常量表达式
string strs[get size()];	// 当get_size是constexpr时正确;否则错误

const unsigned sz = 3;		
int ia1[sz] = {0, 1, 2};		// 含有3个元素的数组,元素值分别是0，1，2
int a2[] = {0, 1, 2};		// 维度是3的数组
int a3[5] = {0, 1, 2};		// 等价于a3[]=[0，1，2，0，0]
string a4[3] = {"hi", "bye"};// 等价于a4[] = {"hi"，"bye"，“"]
int a5[2] = {0, 1, 2};		// 错误:初始值过多

char a1[] = {'C', '+', '+'};		// 列表初始化，没有空字符
char a2[] = {'C', '+', '+', '\0'};	// 列表初始化，含有显式的空字符
char a3[] = "C++";					// 自动添加表示字符串结束的空字符
const char a4[6] = "Daniel";		// 错误:没有空间可存放空字符!

// 不允许拷贝和赋值
int a[] = {0, 1, 2};				// 含有3个整数的数组
int a2[] = a;						// 错误:不允许使用一个数组初始化另一个数组
a2 = a;								// 错误:不能把一个数组直接赋值给另一个数组      

// 理解复杂的数组声明
int *ptrs[10];						// ptrs是含有10个整型指针的数组
int &refs[10] = /*?*/;				// 错误:不存在引用的数组
int (*Parray)[10] = &arr;			// Parray指向一个含有10个整数的数组
int (&arrRef)[10] = arr;			// arrRef引用一个含有10个整数的数组

int *(&arry)[10] = ptrs;			// arry是数组的引用，该数组含有10个指针
```

### 访问数组元素

在使用数组下标的时候，通常将其定义为 size_t 类型
size_t 是一种机器相关的无符号类型，它能表示内存中任意对象的大小
在 cstddef 头文件中定义了size_t

### 指针和数组

在很多用到数组名字的地方，编译器都会自动地将其替换为一个指向数组首元素的指针

```c++
int ia[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};	// ia是一个含有10个整数的数组
auto ia2(ia);								// ia2 是一个整型指针，指向 ia的第一个元素
ia2 = 42;									// 错误:ia2是一个指针，不能用int 值给指针赋值

auto ia2(&ia[0]);							// 显然ia2的类型是int*

//ia3是一个含有10个整数的数组
decltype(ia) ia3 = {0,1,2,3,4,5,6,7,8,9};
ia3 = p;						// 错误:不能用整型指针给数组赋值
ia3[4] = i;						// 正确:把i的值赋给ia3的一个元素

// 指针也是迭代器
int arr[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int *p = arr;				// p指向arr的第一个元素
++p;						// p指向arr[1]

// 标准库函数begin和end
int ia[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};	// ia是一个含有10个整数的数组
int *beg = begin(ia);						// 指向 ia首元素的指针
int *last = end(ia);						// 指向arr尾元素的下一位置的指针

// 指针运算
constexpr sizet sz = 5;
int arr[sz] = {1,2,3,4,5};
int *ip = arr;					// 等价于int *ip = &arr[0]
int *ip2 = ip + 4;				// ip2指向arr的尾元素 arr[4]
// 两指针相减的结果是名为ptrdiff_t的标准库类型
auto n = end(arr) - begin(arr);	// n的值是5，也就是arr中元素的数量

int ia[] = {0, 2, 4, 6, 8}; 		// 含有5个整数的数组
int last = *(ia + 4);				// 正确:把last初始化成8，也就是ia[4]的值
last = *ia + 4;						// 正确：last=4等价于ia[0] + 4
```



### C风格字符串

C 风格字符串不是一种类型，而是为了表达和使用字符串而形成的一种约定俗成的写法
按此习惯书写的字符串存放在字符数组中并以空字符结束 (null terminated)
以空字符结束的意思是在字符串最后一个字符后面跟着一个空字符(\0)

**C标准库String函数**

| C风格字符串的函数 | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| `strlen(p)`       | 返回p的长度，空字符不计算在内                                |
| `strcmp(p1, p2)`  | 比较p1和p2的相等性。如果p1==p2，返回0;如果p1>p2返回一个正值;如果p1<p2，返回一个负值 |
| `strcat(p1, p2)`  | 将p2附加到p1之后，返回p1                                     |
| `strcpy(p1, p2)`  | 将p2拷贝给p1，返回p1                                         |

传入此类函数的指针必须指向以空字符作为结束的数组

**比较字符串**

```c++
string s1 = "A string example";
string s2 = "Adifferent string";
if (s1 < s2)				// false: s2小于s1
	cout << "";    
    
const char cal[] = "A string example";
const char ca2[] = "A different string";
if (cal < ca2)			// 未定义的:试图比较两个无关地址
	cout << "";

if (strcmp(cal, ca2) < 0)			// 和两个string对象的比较s1 < s2效果一样
```



### 与旧代码的接口

```c++
string s("Hello World");		//s的内容是Hello World
*str = s;						//错误:不能用strinq对象初始化char*
char const char* str = s.cstr();//正确

// 使用数组初始化vector对象
int int_arr[]={0，1，2，3，4，5};
// ivec有6个元素，分别是int_arr中对应元素的副本
vector<int> ivec(begin(int_arr), end(int_arr));

//拷贝三个元素:int arr[1]、int arr[2]、int arr[3]
vector<int> subVec(int_arr + 1, int_arr + 4);
```



## 多维数组

C++语言中没有多维数组，通常所说的多维数组其实是数组的数组。

```c++
int ia[3][4];//大小为3的数组，每个元素是含有4个整数的数组

// 大小为 10的数组，它的每个元素都是大小为 20 的数组
// 这些数组的元素是含有30个整数的数组
int arr[10][20][30] = [0];//将所有元素初始化为0
```

**多维数组的初始化**

```c++
int ia[3][4] = {			// 三个元素，每个元素都是大小为4的数组
    {0, 1, 2, 3},			// 第1行的初始值
    {4, 5, 6, 7},			// 第2行的初始值
    {8, 9, 10, 11}			// 第3行的初始值
};

int ia[3][4] = {0,1,2,3,4,5,6,7,8,9,10,11};// 没有标识每行的花括号，与之前的初始化语句是等价的
int ia[3][4]={{0}, {4}, {8}};		// 显式地初始化每行的首元素
int ix[3][4] = {0, 3, 6, 9};		// 显式地初始化第1行，其他元素执行值初始化
```

**多维数组的下标引用**

```c++
ia[2][3] = arr[0][0][0];	// 用arr的首元素为 ia最后一行的最后一个元素赋值
int (&row)[4] = ia[1];		// 把row绑定到ia的第二个4元素数组上
```

**使用范围for语句处理多维数组**

```c++
size_t cnt = 0;
for(auto &row : ia)			// 对于外层数组的每一个元素
    for (auto &col : row){	// 对于内层数组的每一个元素
        col = cnt;			// 将下一个值赋给该元素
        ++cnt;				// 将cnt加1
    }

for(const auto &row : ia)	// 对于外层数组的每一个元素
	for (auto col : row)	// 对于内层数组的每一个元素
        cout << col <<endl;
// To
for (auto row : ia)			// 程序将无法通过编译
    for (auto col : row)
        cout << col <<endl;
// 第一个循环遍历 ia 的所有元素，注意这些元素实际上是大小为4的数组。
// 因为 row 不是引用类型，所以编译器初始化 row 时会自动将这些数组形式的元素(和其他类型的数组一样)转换成指向该数组内首元素的指针
// 这样得到的 row的类型就是 int*，内层的循环不合法
```

**指针和多维数组**

```c++
int ia[3][4];				// 大小为3的数组，每个元素是含有4个整数的数组
int (*p)[4] = ia;			// p指向含有4个整数的数组
p = &ia[2];					// p指向ia的尾元素
```



# 表达式

## 基础

### 基本概念

一元运算符、二元运算符

组合运算符、运算对象
	优先级、结合律、求值顺序

运算对象转换

重载运算符

左值和右值
	当一个对象被用作右值的时候，用的是对象的值(内容)
	当对象被用作左值的时候，用的是对象的身份(在内存中的位置)

### 优先级和结合律

括号无视优先级和结合律

### 求值顺序

1. 拿不准的时候最好用括号来强制让表达式的组合关系符合程序逻辑的要求
2. 如果改变了某个运算对象的值，在表达式的其他地方不要再使用这个运算对象

## 算术运算符

| 运算符 | 功能     | 用法        |
| ------ | -------- | ----------- |
| +      | 一元正号 | + expr      |
| -      | 一元负号 | - expr      |
| *      | 乘法     | expr * expr |
| /      | 除法     | expr / expr |
| %      | 求余     | expr % expr |
| +      | 加法     | expr + expr |
| -      | 减法     | expr - expr |

按照运算符优先级分组
在除法运算中，如果两个运算对象的符号相同则商为正(如果不为 0的话)，否则商为负
C++11 新标准则规定商一律向0取整(即直接切除小数部分)

```c++
21 % 6;		/* 结果是3 */		21 / 6;		/* 结果是3 */
21 % 7;		/* 结果是0 */		21 / 7;		/* 结果是3 */
-21 % -8;	/* 结果是-5 */		-21 / -8;	/* 结果是2 */
21 % -5;	/* 结果是1 */		21 / -5;	/* 结果是-4 */
```

## 逻辑和关系运算符

| 结合律 | 运算符 | 功能     | 用法           |
| ------ | ------ | -------- | -------------- |
| 右     | ！     | 逻辑非   | !expr          |
| 左     | <      | 小于     | expr < expr    |
| 左     | <=     | 小于等于 | expr <= expr   |
| 左     | >      | 大于     | expr > expr    |
| 左     | >=     | 大于等于 | expr >= expr   |
| 左     | ==     | 相等     | expr == expr   |
| 左     | !=     | 不相等   | expr != expr   |
| 左     | &&     | 逻辑与   | expr && expr   |
| 左     | \|\|   | 逻辑或   | expr \|\| expr |

短路求值
	对于逻辑与运算符来说，当且仅当左侧运算对象为真时才对右侧运算对象求值
	对于逻辑或运算符来说，当且仅当左侧运算对象为假时才对右侧运算对象求值

```c++
//s是对常量的引用;元素既没有被拷贝也不会被改变
for (const auto &s : text) {		// 对于text的每个元素
    cout << s;						// 输出当前元素
	//遇到空字符串或者以句号结束的字符串进行换行
    if (s.empty() || s[s.size() - 1] == ‘.’)
        cout << endl;
	else
		cout << " ";		//否则用空格隔开
```

## 赋值运算符

赋值运算符的左侧运算对象必须是一个可修改的左值

```c++
int i = 0, j = 0, k = 0;		// 初始化而非赋值
const int ci = i;				// 初始化而非赋值

1024 = k;						// 错误:字面值是右值
i + j = k;						// 错误:算术表达式是右值
ci = k;							// 错误:ci是常量(不可修改的)左值


// 赋值运算的结果是它的左侧运算对象，并且是一个左值
// 结果的类型就是左侧运算对象的类型
// 如果赋值运算符的左右两个运算对象类型不同，则右侧运算对象将转换成左侧运算对象的类型
k = 0;								// 结果:类型是int，值是0
k = 3.14159;						// 结果:类型是int，值是3

k = {3.14};							// 错误:窄化转换
vector<int> vi;						// 初始为空
vi = {0,1,2,3,4,5,6,7,8,9};			// vi现在含有10个元素了，值从0到9

// +=	-=	*=	/=	%=				// 算术运算符
// <<=	>>=	&=	^=	|=				// 位运算符
```

赋值运算符满足右结合律
赋值运算符优先级很低

## 递增和递减运算符

递增和递减运算符有两种形式:前置版本和后置版本
前置版本：首先将运算对象加1(或减 1)，然后将改变后的对象作为求值结果
后置版本：也会将运算对象加1(或减1)，求值结果是运算对象改变之前那个值的副本

```c++
// 该循环的行为是未定义的!
while (beg != s.end() && !isspace(*beg))
	*beg = toupper(*beg++); 	//错误:该赋值语句未定义
//问题在于:赋值运算符左右两端的运算对象都用到了 beg，并且右侧的运算对象还改变了 beg 的值，所以该赋值语句是未定义的。
```

## 成员访问运算符

ptr->mem等价于(*ptr).mem:

```c++
string s1 = "a string", *p = &s1;
auto n = s1.size();					// 运行string对象s1的size成员
n = (*p).size();					// 运行p所指对象的size成员
n = p->size();						// 等价于(*p).size()

//运行p的size成员，然后解引用size的结果，解引用运算符的优先级低于点运算符
*p.size();							// 错误:p是一个指针，它没有名为size的成员
```

## 条件表达式

cond ? expr1 : expr2;

```c++
finalgrade = (grade > 90) ? "high pass"
	: (grade < 60) ? "fail" : "pass";
```

## 位运算符

| 运算符 | 功能   | 用法           |
| ------ | ------ | -------------- |
| ~      | 位求反 | ~expr          |
| <<     | 左移   | expr1 << expr2 |
| >>     | 右移   | expr1 >> expr2 |
| &      | 位与   | expr1 & expr2  |
| ^      | 位异或 | expr1 ^ expr2  |
| \|     | 位或   | expr1 \| expr2 |

## sizeof运算符

sizeof (type)
sizeof expr

```c++
Sales_data data, *p;
sizeof(Sales_data);				// 存储Sale_sdata类型的对象所占的空间大小
sizeof data;					// data的类型的大小，即sizeof(Sales data)
sizeof p;						// 指针所占的空间大小
sizeof *p;						// p所指类型的空间大小，即sizeof(Sales data)
sizeof data.revenue;			// Sales_data的revenue成员对应类型的大小
sizeof Sales_data::revenue;		// 另一种获取revenue大小的方式
```

对char或者类型为**char**的表达式执行 sizeof 运算，结果得1
对**引用类型**执行sizeof运算得到**被引用对象所占空间的大小**
对**指针**执行sizeof运算得到**指针本身所占空间的大小**
对**解引用指针**执行sizeof运算得到**指针指向的对象所占空间的大小**，**指针不需有效**
对**数组**执行sizeof 运算得到**整个数组所占空间的大小**，等价于对数组中所有的元素各执行一次 sizeof运算并将所得结果求和
	sizeof 运算**不会把数组转换成指针**来处理
对**string对象**或vector对象执行sizeof运算只返回**该类型固定部分的大小**，不会计算对象中的元素占用了多少空间

## 逗号运算符

逗号运算符(comma operator)含有两个运算对象，按照从左向右的顺序依次求值

```c++
vector<int>::size_type cnt = ivec.size();
//将把从size到1的值赋给ivec的元素
for (vector<int>::size_type ix = 0; ix != ivec.size(); ++ix, --cnt)
	ivec[ix] = cnt;
```

## 类型转换

隐式转换：
	在大多数表达式中，比 int 类型小的整型值首先提升为较大的整数类型
	在条件中，非布尔值转换成布尔类型
	初始化过程中，初始值转换成变量的类型；在赋值语句中，右侧运算对象转换成左侧运算对象的类型
	如果算术运算或关系运算的运算对象有多种类型，需要转换成同一种类型
	函数调用时也会发生类型转换

### 算数转换

```c++
bool			flag;		char			cval;
short			sval;		unsigned short	usval;
int				ival;		unsigned int	uival;
long			lval;		unsigned long	ulval;
float			fval;		double			dval;

3.14159L + 'a';		// 'a'提升成int，然后该int 值转换成long double
dval + ival;		// ival转换成 double
dval + fval;		// fval转换成 double
ival = dval;		// dval转换成(切除小数部分后)int
flag = dval;		// 如果dval是0，则flag是false，否则flag是true
cval + fval;		// cval提升成int，然后该int值转换成float
sval + cval;		// sval和cval都提升成int
cval + lval;		// cval转换成long
ival + ulval;		// ival转换成unsigned long
usval + ival;		// 根据unsigned short和int所占空间的大小进行提升
uival + lval;		// 根据unsigned int和long所占空间的大小进行转换
```

### 其他隐式类型转换

**数组转换成指针**：在大多数用到数组的表达式中，数组自动转换成指向数组首元素的指针

**指针的转换:**
	常量整数值 0或者字面值nullptr 能转换成任意指针类型
	指向任意非常量的指针能转换成void*
	指向任意对象的指针能转换成const void*

**转换成布尔类型：**如果指针否则转换结果是 true；或算术类型的值为0，转换结果是 false

**转换成常量**：如果T是一种类型，我们就能将指向T的指针或引用分别转换成指向const T的指针或引用

**类类型定义的转换：**类类型能定义由编译器自动执行的转换，不过编译器每次只能执行种类类型的转换

### 显式转换

虽然有时不得不使用强制类型转换，但这种方法本质上是非常危险的。
cast-name: static_cast、dynamic_cast、const_cast 和 reinterpret_cast
`cast-name<type>(expression);`

**static_cast:**
任何具有明确定义的类型转换，只要**不包含底层const**，都可以使用static_cast。

```c++
int i，j;
double slope = i / j;

// 进行强制类型转换以便执行浮点数除法
double slope = static_cast<double>(j) / i;

void* p = &d;			// 正确:任何非常量对象的地址都能存入 void*
//正确:将void*转换回初始的指针类型
double *dp = static_cast<double*>(p);
```

**const_cast:**
const_cast只能改变运算对象的底层const，只有 const_cast 能改变表达式的常量属性
使用其他形式的命名强制类型转换改变表达式的常量属性都将引发编译器错误
不能用 const cast 改变表达式的类型:

```c++
const char *pc;
char *p = const_cast<char*>(pc);		// 正确:但是通过p写值是未定义的行为

const char *cp;
char *q = static_cast<char*>(cp);		// 错误:static cast不能转换掉const性质
static_cast<string>(cp);				// 正确:字符串字面值转换成string类型
const_cast<string>(cp);					// 错误:const_cast 只改变常量属性
```

**reinterpret_cast：**
reinterpret_cast通常为运算对象的位模式提供较低层次上的重新解释

```c++
int *ip;
char *pc = reinterpret_cast<char*>(ip);
// 必须牢记 pc 所指的真实对象是一个 int 而非字符，如果把 pc 当成普通的字符指针使用就可能在运行时发生错误
string str(pc);		//可能导致异常的运行时行为
```

**旧式的强制类型转换**

```c++
type (expr);	// 函数形式的强制类型转换
(type) expr;	// C语言风格的强制类型转换
```

## 运算符优先级表

| 结合律 | 运算符        | 功能               | 用法                    |
| ------ | ------------- | ------------------ | ----------------------- |
| 左     | ::            | 全局作用域         | ::name                  |
| 左     | ::            | 类作用域           | class::name             |
| 左     | ::            | 命名空间作用域     | namespace::name         |
|        |               |                    |                         |
| 左     | .             | 成员选择           | object.member           |
| 左     | ->            | 成员选择           | pointer->member         |
| 左     | []            | 下标               | expr[expr]              |
| 左     | ()            | 函数调用           | name(expr_list)         |
| 左     | {}            | 类型构造           | type(expr_list)         |
|        |               |                    |                         |
| 右     | ++            | 后置递增运算       | lvalue++                |
| 右     | --            | 后置递减运算       | lvalue--                |
| 右     | typeid        | 类型ID             | typeid(type)            |
| 右     | typeid        | 运行时类型ID       | typeid(expr)            |
| 右     | explicit_cast | 类型转换           | `cast_name<type>(expr)` |
|        |               |                    |                         |
| 右     | ++            | 前置递增运算       | ++lvalue                |
| 右     | --            | 前置递减运算       | --lvalue                |
| 右     | ~             | 位求反             | ~expr                   |
| 右     | !             | 逻辑非             | !expr                   |
| 右     | -             | 一元负号           | -expr                   |
| 右     | +             | 一元正号           | +expr                   |
| 右     | *             | 解引用             | *expr                   |
|        | &             | 取地址             | &lvalue                 |
| 右     | ()            | 类型转换           | (type) expr             |
| 右     | sizeof        | 对象的大小         | sizeof expr             |
| 右     | sizeof        | 类型的大小         | sizeof(type)            |
| 右     | sizeof...     | 参数包的大小       | sizeof...(name)         |
| 右     | new           | 创建对象           | new type                |
| 右     | new[]         | 创建数组           | new type[size]          |
| 右     | delete        | 释放对象           | delete expr             |
| 右     | delete[]      | 释放数组           | delete[] expr           |
| 右     | noexcept      | 能否抛出异常       | noexcept(expr)          |
|        |               |                    |                         |
| 左     | ->*           | 指向成员选择的指针 | ptr->*ptr_to_member     |
| 左     | .*            | 指向成员选择的指针 | obj.*ptr_to_member      |
|        |               |                    |                         |
| 左     | *             | 乘法               | expr * expr             |
| 左     | /             | 除法               | expr / expr             |
| 左     | %             | 取模(取余)         | expr % expr             |
|        |               |                    |                         |
| 左     | +             | 加法               | expr + expr             |
| 左     | -             | 减法               | expr - expr             |
|        |               |                    |                         |
| 左     | <<            | 向左移位           | expr << expr            |
| 左     | >>            | 向右移位           | expr >> expr            |
|        |               |                    |                         |
| 左     | <             | 小于               | expr < expr             |
| 左     | <=            | 小于等于           | expr <= expr            |
| 左     | >             | 大于               | expr > expr             |
| 左     | >=            | 大于等于           | expr >= expr            |
|        |               |                    |                         |
| 左     | ==            | 相等               | expr == expr            |
| 左     | !=            | 不相等             | expr != expr            |
|        |               |                    |                         |
| 左     | &             | 位与               | expr & expr             |
|        |               |                    |                         |
| 左     | ^             | 位异或             | expr ^ expr             |
|        |               |                    |                         |
| 左     | \|            | 位或               | expr \| expr            |
|        |               |                    |                         |
| 左     | &&            | 逻辑与             | expr && expr            |
|        |               |                    |                         |
| 左     | \|\|          | 逻辑或             | expr \|\| expr          |
|        |               |                    |                         |
| 右     | ? :           | 条件               | expr ? expr : expr      |
|        |               |                    |                         |
| 右     | =             | 赋值               | lvalue = expr           |
|        |               |                    |                         |
| 右     | *=、 /=、 %=  | 复合赋值           | lvalue += expr          |
| 右     | +=、 -=       | 复合赋值           |                         |
| 右     | <<=、 >>=     | 复合赋值           |                         |
| 右     | &=、 \|=、 ^= | 复合赋值           |                         |
|        |               |                    |                         |
| 右     | throw         | 抛出异常           | throw expr              |
|        |               |                    |                         |
| 左     | ,             | 逗号               | expr, expr              |



# 语句

## 简单语句

**复合语句**：指用花括号括起来的(可能为空的)语句和声明的序列，复合语句也被称作块 (block)

## 语句作用域

定义在控制结构当中的变量只在相应语句的内部可见，一旦语句结束，变量也就超出其作用范围了

## 条件语句

### if语句

```c++
if (condition)
	statement
else
	statement2
    
const vector<string> scores = {"E"，"D"，"C"，"B"，"A"，"A++"};
// 如果grade小于60，对应的字母是E;否则计算其下标
string lettergrade;
if (grade<60)
	lettergrade = scores[0];
else
	lettergrade = scores[(grade - 50)/10];
```

**悬垂else**
怎么知道某个给定的else是和哪个if匹配呢

```c++
//错误:实际的执行过程并非像缩进格式显示的那样;else 分支匹配的是内层if 语句
if (grade % 10 >= 3)
	if (grade % 10 > 7)
        lettergrade += '+';			// 末尾是8或者9的成绩添加一个加号
else
	lettergrade += '-';				// 末尾是3、4、5、6或者7的成绩添加一个减号!
```

### switch 语句

case标签必须是整型常量表达式

```c++
//为每个元音字母初始化其计数值
unsigned aCnt =0, eCnt = 0, iCnt = 0, oCnt = 0, uCnt = 0;
char ch;
while (cin >> ch){
    // 如果 ch 是元音字母，将其对应的计数值加 1
    switch (ch){
        case 'a':
        	++aCnt;
        	break;
        case 'e':
        	++eCnt;
        	break;
        case 'i':
        	++iCnt;
        	break;
        case 'o':
        	++oCnt;
        	break;
        case 'u':
        	++uCnt;
        	break;
    }
}

unsigned vowelCnt = 0;
switch (ch)
{
    //出现了a、e、i、o或u中的任意一个都会将vowelCnt的值加1
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        ++vowelCnt;
        break;
}
```

**default标签**
如果没有任何一个 case 标签能匹配上 switch 表达式的值，程序将执行紧跟在 default 标签 (default label)后面的语句

## 迭代语句

### while语句

```c++
while (condition)
	statement
```

### 传统for语句

```c++
for (init-statemen; condition; expression)
	statement;
    
// 传统for循环的执行流程
// 重复处理 s 中的字符直至我们处理完全部字符或者遇到了一个表示空白的字符
for (decltype(s.size()) index = 0; index != s.size() && !isspace(s[index]); ++index)
	s[index] = toupper(s[index]);		//将当前字符改成大写形式

// for语句头中的多重定义
// 记录下v的大小，当到达原来的最后一个元素后结束循环
for (decltype(v.size()) i = 0, sz = v.size(); i != sz; ++i)
	v.push_back(v[i]);

// 省略for语句头中的某些部分
auto begv.begin();// 什么也不做
for(/*空语句 */; beg != v.end() && *beg >= 0; ++beg)
    ;		// 什么也不做
```

### 范围for语句

```c++
for (declaration : expression)
	statement
```

```c++
vector<int> v= {0, 1, 2, 3, 4, 5};// 范围变量必须是引用类型，这样才能对元素执行写操作
for (auto &r : v)				//对于v中的每一个元素
    r *= 2;
```

### do while语句

```c++
do
	statement
while (condition);
```

## 跳转语句

break、continue、goto、return

### break

break 语句(break statement)负责终止离它最近的while do while for或switch语句，并从这些语句之后的第一条语句开始继续执行。

### continue

continue语句(continue statement)终止最近的循环中的当前选代并立即开始下一次迭代。

### goto

goto语句(goto statement)的作用是从goto语句无条件跳转到同一函数内的另一条语句。

```c++
//向后跳过一个带初始化的变量定义是合法的
begin:
	int sz = get size();
	if (sz <= 0){
		goto begin;
    }
```

## try语句块和异常处理

- **throw表达式**(throw expression)，异常检测部分使用throw表达式来表示它遇到了无法处理的问题。我们说throw引发(raise)了异常。
- **try语句块**(try block)，异常处理部分使用try语块处理异常。try语句块以关键字 try开始，并以一个或多个 **catch 子句**(catch clause)结束。try语句块中代码抛出的异常通常会被某个 catch 子句处理。因为 catch 子句“处理”异常，所以它们也被称作**异常处理代码**(exception handler)。
- 一套**异常类**(exception class)，用于在throw 表达式和相关的catch子句之间传递异常的具体信息。

### throw表达式

```c++
Sales_item iteml, item2;
cin >> iteml >> item2;
//首先检查item1和item2是否表示同一种书籍
if (iteml.isbn() == item2.isbn()) {
    cout << item1 + item2 << endl;
    return 0; //表示成功
} else {
	cerr << "Data must refer to same ISBN" << endl;
    return -1;//表示失败
}

//首先检查两条数据是否是关于同一种书籍的
if (iteml.isbn() !=item2.isbn())
	throw runtime error("Data must refer to same ISBN");
//如果程序执行到了这里，表示两个ISBN是相同的
cout << item1 + item2 << endl;
```

### try语句块

```c++
try {
	program-statements
} catch (exception-declaration) {
    handler-statements
} catch (exception-declaration) {
    handler-statements
} // ...
```

**编写处理代码**

```c++
while (cin >> iteml >> item2){
    try {
        // 执行添加两个Sales item 对象的代码
        // 如果添加失败，代码抛出一个runtimeerror异常
    } catch (runtime_error err) {
        //提醒用户两个ISBN必须一致，询问是否重新输入
        cout << err.what()
            << "Try Again? Enter y or n" << endl;
        char c;
        cin >> c;
        if (!cin || c == 'n')
            break;	//跳出while循环
    }
}
```

### 标准异常

- exception头文件定义了最通用的异常类exception。它只报告异常的发生，不提供任何额外信息。
- stdexcept 头文件定义了几种常用的异常类。
- new头文件定义了 bad_alloc 异常类型。
- type_info头文件定义了 bad_cast 异常类型。

| \<stdexcept\>定义的异常类 |                                               |
| ------------------------- | --------------------------------------------- |
| exception                 | 最常见的问题                                  |
| runtime_error             | 只有在运行时才能检测出的问题                  |
| range_error               | 运行时错误:生成的结果超出了有意义的值域范围   |
| overflow_error            | 运行时错误:计算上溢                           |
| underflow_error           | 运行时错误:计算下溢                           |
| logic_error               | 程序逻辑错误                                  |
| domain_error              | 逻辑错误:参数对应的结果值不存在               |
| invalid_argument          | 逻辑错误:无效参数                             |
| length_error              | 逻辑错误:试图创建一个超出该类型最大长度的对象 |
| out_of_range              | 逻辑错误:使用一个超出有效范围的值             |

异常类型只定义了一个名为 what 的成员函数，该函数没有任何参数，返回值是一个指向C 风格字符串的const char*。
该字符串的目的是提供关于异常的一些文本信息。



# 函数

## 函数基础

函数(function)定义包括以下部分:
	返回类型(return type)、函数名字、由0个或多个形参(parameter)组成的列表以及函数体。
		形参以逗号隔开，形参的列表位于一对圆括号之内

调用运算符的形式是一对圆括号
	它作用于一个表达式，该表达式是函数或者指向函数的指针
	圆括号之内是一个用逗号隔开的实参(argument)列表
	调用表达式的类型就是函数的返回类型

```c++
// val的阶乘是 val * (val - l) * (val - 2) ... * (( val - (val - 1)) * 1)
int fact(int val)
{
    int ret = 1;				// 局部变量，用于保存计算结果
	while (val > 1)
        ret *= val--;			// 把ret和val的乘积赋给ret，然后将val减1
    return ret;					// 返回结果
}

// 调用函数
int main()
{
    int j = fact(5);			// j等于120，即fact(5)的结果
    cout << "5! is" << j << endl;
    return 0;
}

// 形参和实参
fact("hello");		// 错误:实参类型不正确
fact();				// 错误:实参数量不足
fact(42, 10, 0);	// 错误:实参数量过多
fact(3.14);			// 正确:该实参能转换成int类型
```



### 局部对象

- 名字的作用域是程序文本的一部分，名字在其中可见
- 对象的生命周期是程序执行过程中该对象存在的一段时间

**局部对象**：形参和函数体内部定义的变量
**自动对象**：只存在于块执行期间的对象。当块的执行结束后，块中创建的自动对象的值变成未定义的
**局部静态对象**：执行路径**第一次**经过对象定义语句时初始化，并且**直到程序终止才被销毁**，在此期间即使对象所在的函数结束执行也不会对它有影响

```c++
size_t count_calls()
{
	static size_t ctr = 0;			//调用结束后，这个值仍然有效
    return ++ctr;    
}

int main()
{
	for (size_t i = 0; i != 10; ++i)
        cout << count_calls() << endl;
    return 0;
}
//这段程序将输出从1到10(包括10在内)的数字
```



### 函数声明

函数的名字也必须在使用之前声明，函数只能定义一次，但可以声明多次
函数声明无须函数体，用一个分号替代即可

```c++
// 我们选择beg和end作为形参的名字以表示这两个迭代器划定了输出值的范围
void print(vector<int>::const_iterator beg, vector<int>::const_iterator end);
```

**在头文件中进行函数声明**
定义函数的源文件应该把含有函数声明的头文件包含进来，编译器负责验证函数的定义和声明是否匹配。



### 分离式编程

为了允许编写程序时按照逻辑关系将其划分开来，C++语言支持分离式编译(separate compilation)
分离式编译允许我们把程序分割到几个文件中去，每个文件独立编译

### 编译和链接多个源文件

.obj或.o文件
链接器



## 参数传递

**引用传递**：形参是引用类型时，引用形参是它对应的实参的别名

### 传值参数

当初始化一个非引用类型的变量时，初始值被拷贝给变量。对变量的改动不会影响初始值

**指针形参**
	指针的行为和其他非引用类型一样
	当执行指针拷贝操作时，拷贝的是指针的值
	拷贝之后，两个指针是不同的指针

```c++
// 该函数接受一个指针，然后将指针所指的值置为 0
void reset(int *ip)
{
    *ip = 0;			// 改变指针ip所指对象的值
    ip = 0;				// 只改变了ip的局部拷贝，实参未被改变
}

int i = 42;
reset(&i);				// 改变i的值而非的地址
cout << "i = " << i << endl;		// 输出 i = 0
```

### 传引用参数

```c++
// 该函数接受一个int 对象的引用，然后将对象的值置为0
void reset(int &i)		// i是传给 reset函数的对象的另一个名字
{
	i = 0;    			// 改变了所引对象的值
}

int j = 42;
reset(j);							// j采用传引用方式，它的值被改变
cout << "j = " << j << endl;		// 输出j = 0
```

**使用引用避免拷贝**

```c++
//比较两个string对象的长度
bool isShorter(const string &s1, const string &s2)
{
	return s1.size() < s2.size();
}
```

**使用引用形参返回额外信息**

```c++
// 返回s中c第一次出现的位置索引
// 引用形参occurs负责统计c出现的总次数
string::size_type find_char(const string &s, char c, string::size_type &occurs)
{
    auto ret = s.size();		// 第一次出现的位置(如果有的话)
    occurs = 0;					// 设置表示出现次数的形参的值
    for (decltype(ret) i = 0; i != s.size(); ++i)
    {
        if (s[i] == c){
            if (ret == s.size())
                ret = i;		// 记录c第一次出现的位置
            ++occurs;			// 将出现的次数加1
        }
    }
    return ret;					// 出现次数通过occurs 隐式地返回	
}
```

### const形参和实参

```c++
void fcn(const int i) { /* fcn能够读取i，但是不能向i写值 */ }
void fcn(const int i) { /*fcn能够读取i，但是不能向i写值 */ }
void fcn(int i) { /* ...*/ } //错误:重复定义了fcn(int)
```

**指针或引用形参与const**

```c++
int i = 42;
const int *cp = &i;			// 正确:但是cp不能改变i
const int &r = i; 			// 正确:但是r不能改变i
const int &r2 = 42;			// 正确
int* p = cp;				// 错误:p的类型和cp的类型不匹配
int &r3 = r;				// 错误:r3的类型和r的类型不匹配
int &r4 = 42;				// 错误:不能用字面值初始化一个非常量引用

int i = 0;
const int ci = i;
string::size_type ctr = 0;
reset(&i);					// 调用形参类型是int*的reset函数
reset(&ci);					// 错误:不能用指向const int 对象的指针初始化int*
reset(i);					// 调用形参类型是int&的reset函数
reset(ci);					// 错误:不能把普通引用绑定到const对象ci上
reset(42);					// 错误:不能把普通应用绑定到字面值上
reset(ctr);					// 错误:类型不匹配，ctr是无符号类型
// 正确:findchar的第一个形参是对常量的引用
find_char("Hello World!", 'o', ctr);
```

尽量使用常量引用



### 数组形参

不能以值传递的方式传递数组，可以把形参写成类似数组的形式

```c++
//尽管形式不同，但这三个print 函数是等价的
//每个函数都有一个const int*类型的形参
void print(const int*);			
void print(const int[]);		// 可以看出来，函数的意图是作用于一个数组
void print(const int[10]);		// 这里的维度表示我们期望数组含有多少元素，实际不一定

int i = 0， j[2] = {0, 1};
print(&i);			// 正确:&i的类型是int*
print(j);			// 正确:j转换成int*并指向j[0]

// 使用标记指定数组长度
void print(const char *cp)
{
    if (cp)						// 若cp不是一个空指针
        while(*cp)				// 只要指针所指的字符不是空字符
            cout << *cp++;		// 输出当前字符并将指针向前移动一个位置
}

// 使用标准库规范
void print(const int *beg, const int *end)
{
    // 输出beg到end之间(不含end)的所有元素
    while (beg != end)
        cout << *beg++ << endl;// 输出当前元素并将指针向前移动一个位置
}

// 显式传递一个表示数组大小的形参
// const int ia[]等价于const int* ia
// size 表示数组的大小，将它显式地传给函数用于控制对ia元素的访问
void print(const int ia[], size_t size)
{
	for (size_t i = 0; i != size; ++i)
    {
        cout << ia[i] << endl;    
    }
}

// 数组引用形参
//正确:形参是数组的引用，维度是类型的一部分
void print(int (&arr)[10])
{
	for (auto elem :arr)
        cout << elem <<endl;    
}

// 传递多维数组
// matrix 指向数组的首元素，该数组的元素是由10个整数构成的数组
void print(int (*matrix)[10], int rowSize) { /*。。。*/ }
//等价定义
void print(int matrix[][10], int rowSize) { /*。。。*/ }
//matrix的声明看起来是一个二维数组，实际上形参是指向含有10个整数的数组的指针
```



### main:处理命令行选项

```c++
int main(int argc, char *argv[]) { ... }
// Or
int main(int argc, char **argv) { ... }

// prog -d -o ofile data0
argv[0] = "prog"; // 或者argv[0]也可以指向一个空字符串
argv[1] = "-d";
argv[2] = "-o";
argv[3] = "ofile";
argv[4] = "data0";
argv[5] = 0;
```



### 含有可变形参的函数

**initializer_list形参**：initializer_list 是一种标准库类型，用于表示某种特定类型的值的数组

| initializer_list提供的操作           | 说明                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| `initializer_list<T> Ist;`           | 默认初始化;T类型元素的空列表                                 |
| `initializer_list<T> lst(a,b,c...};` | lst 的元素数量和初始值一样多; lst 的元素是对应初始值的副本; 列表中的元素是const |
| `lst2(lst)`<br />`lst2 = lst`        | 拷贝或赋值一个initializer_list对象不会拷贝列表中的元素; 拷贝后原始列表和副本共享元素 |
| `lst.size()`                         | 列表中的元素数量                                             |
| `lst.begin()`                        | 返回指向lst中首元素的指针                                    |
| `lst.end()`                          | 返回指向lst中尾元素下一位置的指针                            |

```c++
initializer_list<string> ls;			// initializer_list的元素类型是string
initializer_list<int> li;				// initializer_list的元素类型是int

void error_msg(initializer_list<string> il)
{
    for (auto beg = il.begin(); beg != il.end(); ++beg)
        cout << *beg << " ";
    cout << endl;
}

// expected和actual是string 对象
if(expected != actual)
	error_msg({"functionX", "expected", "actual"});
else
	error_msg({"functionX"，"okay"});
```

**省略符形参(varargs)**

```c++
void foo(parm list, ...);			// 形参声明后面的逗号是可选的
void foo(...);
```

### 返回类型和return语句

```c++
return;
return expression;
```

### 无返回值函数

没有返回值的return语句只能用在返回类型是void的函数中

```c++
void swap(int &vl， int &v2)
{
    // 如果两个值是相等的，则不需要交换，直接退出
	if (v1 == v2)
        return;
    // 如果程序执行到了这里，说明还需要继续完成某些功能
    int tmp = v2;
    v2 = v1;
	v1 = tmp;
    // 此处无须显式的return语句
}
```

### 有返回值函数

函数内的每条return语句必须返回一个值
return语句返回值的类型必须与函数的返回类型相同，或者能隐式地转换成函数的返回类型

```c++
// 因为含有不正确的返回值，所以这段代码无法通过编译
bool str_subrange(const string &str1, const string &str2)
{
    // 大小相同:此时用普通的相等性判断结果作为返回值
    if (str1.size() == str2.size())
        return str1 == str2;			//正确: ==运算符返回布尔值
    // 得到较短string对象的大小
    auto size = (str1.size() < str2.size()) ? str1.size() : str2.size();
    // 检查两个string对象的对应字符是否相等，以较短的字符串长度为限
    for(decltype(size) i = 0; i != size; ++i)
    {
        if( str1[i] != str2[i] )
            return;				// 错误 #1:没有返回值，编译器将报告这一错误
    }
    
    // 错误 #2:控制流可能尚未返回任何值就结束了函数的执行
    // 编译器可能检查不出这一错误
}
```

**值是如何返回的**
	返回的值用于初始化调用点的一个临时量

```c++
//如果ctr的值大于1，返回word的复数形式
string make_plural(size_t ctr, const string &word, const string &ending)
{
    return (ctr > 1) ? word + ending : word;
}
// 该函数的返回类型是string,意味着返回值将被拷贝到调用点。
// 因此,该函数将返回word的副本或者一个未命名的临时string 对象，该对象的内容是 word和ending 的和。

// 如果函数返回引用，则该引用仅是它所引对象的一个别名
//  挑出两个string 对象中较短的那个，返回其引用
const string &shorterString(const string &s1, const string &s2){
    return s1.size() <= s2.size() ? s1 : s2;
}
```

**禁止返回局部对象的引用或指针**

```c++
//严重错误:这个函数试图返回局部对象的引用
const string &manip()
{
    string ret;
    //以某种方式改变一下ret
    if (!ret.empty())
        return ret;			//错误:返回局部对象的引用!
    else
        return "Empty";		//错误:"Empty"是一个局部临时量
}
```

**引用返回左值**

```c++
char &get_val(string &str， string::size_type ix)
{
	return str[ix];    	// get_val假定索引值是有效的
}
int main()
{
	string s("a value");
	cout << s << endl;    	// 输出a value
	get_val(s, 0) = 'A';    // 将s[0]的值改为A
    cout << s << endl;		// 输出A value
    return 0;
}
```

**列表初始化返回值**

```c++
vector<string> process()
{
    // ...
    // expected和actual是string对象
	if(expected.empty())
        return {};    		// 返回一个空vector对象
    else if (expected == actual)
        return {"functionX", "okay"}; // 返回列表初始化的vector对象
    else
        return {"functionX", expected, actual};
}
```

**主函数的返回值**

允许main函数没有 return语句直接结束
如果控制到达了main函数的结尾处而且没有return语句，编译器将隐式地插入一条返回0的return语句

```c++
int main()
{
	if (some_failure)
        return EXIT_FAILURE;		// 定义在cstdlib头文件中
    else
        return EXIT_SUCCESS;		// 定义在cstdlib头文件中
}
```

**递归**

```c++
// 计算val的阶乘，即1 * 2 * 3 ... * val
int factorial(int val)
{
    if (val > l)
        return factorial(val - 1) * val;
    return 1;
}
```

### 返回数组指针

函数不能返回数组，但是函数可以返回数组的指针或引用

```c++
int (*func(int i))[10];
```

- `func(inti)` 表示调用 func函数时需要一个int类型的实参
- `(*func(int i))`意味着我们可以对函数调用的结果执行解引用操作
- `(*func(int i))[10]`表示解引用func的调用将得到一个大小是10的数组
- `int (*func(int i))[10]`表示数组中的元素是int类型

**使用尾置返回类型**

```c++
// func 接受一个int 类型的实参，返回一个指针，该指针指向含有10个整数的数组
auto func(int i) -> int(*)[10];
```

**使用decltype**

```c++
int odd[] = {1, 3, 5, 7, 9};
int even[] = {0, 2, 4, 6, 8};
// 返回一个指针，该指针指向含有 5个整数的数组
decltype(odd) *arrPtr(int i)
{
    return (i % 2) ? &odd : &even;//返回一个指向数组的指针
}
```



## 函数重载

```c++
void print(const char *cp);
void print(const int *beg, const int *end);
void print(const int ia[], size_t size);

int j[2] ={0, 1};
print("Hello World");			// 调用 print(const char*)
print(j, end(j) - begin(j));	// 调用 print(const int*, size_t)
print(begin(j), end(j));		// 调用 print(const int*, const int*)
```

**定义重载函数**

```c++
Record lookup(const Account&);		// 根据Account查找记录
Record lookup(const Phone&);		// 根据Phone查找记录
Record lookup(const Name&);			// 根据Name查找记录
Account acct;
Phone phone;
Record r1 = lookup(acct);			// 调用接受Account的版本
Record r2 = lookup(phone);			// 调用接受Phone的版本

// 判断两个形参的类型是否相异
//  每对声明的是同一个函数
Record lookup(const Account &acct);
Record lookup(const Account&);	//  省略了形参的名字
typedef Phone Telno;
Record lookup(const Phone&);
Record lookup(const Telno&);	// Telno和Phone的类型相同

// 重载和const形参
//  一个拥有顶层const的形参无法和另一个没有顶层const的形参区分开来:
Record lookup(Phone);
Record lookup(const Phone);		// 重复声明了Record lookup(Phone)

Record lookup(Phone*);
Record lookup(Phone* const);	// 重复声明了Record lookup(Phone*)

// 如果形参是某种类型的指针或引用，则通过区分其指向的是常量对象还是非常量对象可以实现函数重载，此时的const是底层的:
// 对于接受引用或指针的函数来说，对象是常量还是非常量对应的形参不同
// 定义了4个独立的重载函数
Record lookup(Account&);			// 函数作用于Account的引用
Record lookup(const Account&);		// 新函数，作用于常量引用

Record lookup(Account*);			// 新函数，作用于指向Account的指针
Record lookup(const Account*);		// 新函数，作用于指向常量的指针

// const_cast和重载
// const_cast在重载函数的情景中最有用
//  比较两个string对象的长度，返回较短的那个引用
const strinq &shorterString(const string &s1, const string &s2)
{
	return s1.size() <= s2.size() ? s1 : s2;    
}
// To
string &shorterString(string &sl, string &s2)
{
    auto &r = shorterString(const_cast<const string&>(sl), 
                            const_cast<const string&>(s2));
    return const_cast<string&>(r);
}
```

**调用重载函数**

- 偏译器找到一个与实参最佳匹配(best match)的函数，并生成调用该函数的代码。
- 找不到任何一个函数与调用的实参匹配，此时编译器发出无匹配(no match)的错误信息。
- 有多于一个函数可以匹配,但是每一个都不是明显的最佳选择。此时也将发生错误称为二义性调用(ambiguous call)。

### 重载与作用域

```c++
string read();
void print(const string &);
void print(double); // 重载print函数
void fooBar(int ival)
{
    bool read = false;		// 新作用域:隐藏了外层的 read
    string s = read();		// 错误:read是一个布尔值，而非函数
	// 不好的习惯:通常来说，在局部作用域中声明函数不是一个好的选择
    void print(int);		// 新作用域:隐藏了之前的 print
	print("Value: ");		// 错误:print(const string &)被隐藏掉了
    print(ival);			// 正确:当前print(int)可见
    print(3.14);    		// 正确:调用print(int); print(double)被隐藏掉了
}

void print(const string &);
void print(double);			// print函数的重载形式
void print(int);			// print函数的另一种重载形式
void fooBar2(int ival)
{
    print("Value:");		// 调用print(const string &)
    print(ival);			// 调用print(int)
    print(3.14);			// 调用print(double)
}
```



## 特殊用途语言特征

### 默认实参

```c++
typedef string::size_type sz;
string screen(sz ht = 24, sz wid = 80, char backgrnd = ' ');

// 使用默认实参调用函数
string window;
window = screen();				// 等价于screen(24, 80, ' ')
window = screen(66);			// 等价于screen(66, 80, ' ')
window = screen(66, 256);		// 等价于screen(66, 256, ' ')
window = screen(66, 256, '#');	// 等价于screen(66, 256, '#')

window = screen(, , '?');		// 错误:只能省略尾部的实参1
window = screen('?');			// 调用screen('?', 80, ' ')
```

***在给定的作用域中一个形参只能被赋予一次默认实参，函数的后续声明只能为之前那些没有默认值的形参添加默认实参***

```c++
// 表示高度和宽度的形参没有默认值
string screen(sz, sz, char = ' ');
// 不能修改一个已经存在的默认值:
string screen(sz, sz, char = '*');		// 错误:重复声明
// 可以按照如下形式添加默认实参:
string screen(sz = 24, sz = 80, char);	// 正确:添加默认实参

// 默认实参初始值
//  局部变量不能作为默认实参。除此之外，只要表达式的类型能转换成形参所需的类型，该表达式就能作为默认实参:
// wd、def和ht的声明必须出现在函数之外
sz wd = 80;
char def = ' ';
sz ht();
string screen(sz = ht(), sz = wd, char = def);
string window = screen();		// 调用 screen(ht(), 80, ' ')
```



### 内联函数和constexpr函数

把内联函数和constexpr函数放在头文件内
内联函数(inline)，通常就是将它在每个调用点上“内联地”展开

```c++
cout << shorterString(s1, s2) << endl;
// 编译过程会展开成如下形式
cout << (s1.size() < s2.size() ? s1 : s2) << endl;

//内联说明只是向编译器发出的一个请求，编译器可以选择忽略这个请求
```

**constexpr函数**
constexpr 函数(constexpr function)是指能用于常量表达式的函数。
	函数的返回类型及所有形参的类型都得是字面值类型 
	函数体中必须有且只有一条return语句
constexpr函数被隐式地指定为内联函数
constexpr函数不一定返回常量表达式

```c++
constexpr int new_sz() { return 42; }
constexpr int foo = newsz();			// 正确:foo是一个常量表达式

// 如果arg是常量表达式，则 scale(arg)也是常量表达式
constexpr size_t scale(size_t cnt) { return new_sz() * cnt; }

int arr[scale(2)];		// 正确:scale(2)是常量表达式
int i = 2;				// 不是常量表达式
int a2[scale(i)];		// 错误:scale(i)不是常量表达式
```

### 调试帮助

**assert 预处理宏**

首先对expr求值，如果表达式为假(即0)，assert 输出信息并终止程序的执行，如果为真，assert什么都不做

```c++
assert(expr);
```

**NDEBUG预处理变量**
如果定义了NDEBUG,则assert 什么也不做
默认状态下没有定义NDEBUG,此时assert 将执行运行时检查

```c++
void print(const int ia[], size_t size)
{
#ifndef NDEBUG
    // __func__是编译器定义的一个局部静态变量，用于存放函数的名字
    cerr << __func__ << ": array size is " << size << endl;
#endif
}
// ...
// __FILE__: 存放文件名的字符串字面值
// __LINE__: 存放当前行号的整型字面值
// __TIME__: 存放文件编译时间的字符串字面值
// __DATE__: 存放文件编译日期的字符串字面值
```

## 函数匹配

```c++
void f();
void f(int);
void f(int, int);
void f(double, double = 3.14);
f(5.6);		// 调用void f(double, double)
```

**确定候选函数和可行函数**
	与被调用的函数同名
	其声明在调用点可见
	寻找最佳匹配

### 实参类型转换

精确匹配
	实参类型和形参类型相同
	实参从数组类型或函数类型转换成对应的指针类型
	向实参添加顶层const或者从实参中删除顶层const
通过const转换实现的匹配
通过类型提升实现的匹配
通过算术类型转换实现的匹配
通过类类型转换实现的匹配 

**需要类型提升和算术类型转换的匹配**

```c++
void ff(int);
void ff(short);
ff('a');			// char提升成int;调用 f(int)

void manip(long);
void manip(float);
manip(3.14);			//错误:二义性调用

Record lookup(Account&);	// 函数的参数是Account的引用
Record lookup(const Account&);	// 函数的参数是一个常量引用
const Account a;
Account b;

lookup(a);			// 调用 lookup(const Account&)
lookup(b);			// 调用 lookup(Account&)
```

## 函数指针

函数指针指向的是函数而非对象

```c++
// 比较两个string对象的长度
bool lengthCompare(const string &, const string &);

// pf指向一个函数，该函数的参数是两个const string的引用，返回值是bool类型
bool (*pf)(const string &, const string &);			//未初始化

// 使用函数指针
pf = lengthCompare;				// pf指向名为lengthCompare的函数
pf = &lengthCompare;			// 等价的赋值语句:取地址符是可选的

bool b1 = pf("hello", "goodbye");				// 调用engthCompare函数
bool b2 = (*pf)("hello", "goodbye");			// 一个等价的调用
bool b3 = lengthCompare("hello", "goodbye"); 	// 另一个等价的调用

string::size_type sumLength(const string&, const string&);
bool cstringCompare(const char*, const char*);
pf = 0;					// 正确:pf不指向任何函数
pf = sumLength;			// 错误:返回类型不匹配
pf = cstringCompare;	// 错误:形参类型不匹配
pf = lenqthCompare;		// 正确:函数和指针的类型精确匹配

// 重载函数的指针
void ff(int*);
void ff(unsigned int);
void (*pf1)(unsigned int) = ff;		// pf1指向 ff(unsigned)
void (*pf2)(int) = ff;				// 错误:没有任何一个ff与该形参列表匹配
double (*pf3)(int*) = ff;			// 错误:ff和pf3的返回类型不匹配

// 函数指针形参
// 第三个形参是函数类型，它会自动地转换成指向函数的指针
void useBigger(const string &s1, const string &s2, bool pf(const string&, const string &));
// 等价的声明：显式地将形参定义成指向函数的指针
void useBigger(const string &s1, const string &s2, bool (*pf)(const string &, const string &));

//自动将函数lengthCompare转换成指向该函数的指针
useBigger(s1, s2, lengthCompare);


// Func和Func2是函数类型
typedef bool Func(const string&, const string&);
typedef decltype(lengthCompare) Func2;				// 等价的类型
// FuncP和FuncP2是指向函数的指针
typedef bool(*FuncP)(const string&, const string&);
typedef decltype(lengthCompare) *FuncP2;			// 等价的类型

//useBigger的等价声明，其中使用了类型别名
void useBigger(const string&, const string&, Func);
void useBigger(const string&, const string&, FuncP2);

// 返回指向函数的指针
using F = int(int*，int);			// F是函数类型，不是指针
using PF = int(*)(int*,int);		// PF是指针类型
PF f1(int);							// 正确:PF是指向函数的指针，f1返回指向函数的指针
F f1(int);							// 错误:F是函数类型，f1不能返回一个函数
F *f1(int);							// 正确:显式地指定返回类型是指向函数的指针
int (*f1(int))(int*, int);
auto f1(int) -> int (*)(int*, int);

//将auto和decltype用于函数指针类型
string::size_type sumLength(const string&, const string&);
string::size_type largerLength(const string&, const string&);
// 根据其形参的取值，getFcn 函数返回指向 sumLength 或者largerLength 的指针
decltype(sumLength) *getFcn(const string &);
// 将 decltype 作用于某个函数时，它返回函数类型而非指针类型
// 因此，我们显式地加上*以表明我们需要返回指针，而非函数本身
```



# 类

类的基本思想是数据抽象(data abstraction)和封装(encapsulation)。
	数据抽象是一种依赖于**接口**(interface)和**实现** (implementation)分离的编程(以及设计)技术

类的接口包括用户所能执行的操作
类的实现则包括
	类的数据成员
	负责接口实现的函数体
	定义类所需的各种私有函数

## 定义抽象数据类型

### 设计Sales_data类

Sales_data的接口应该包含以下操作:

- 一个isbn成员函数，用于返回对象的ISBN编号
- 一个combine成员函数，用于将一个 Sales_data 对象加到另一个对象上
- 一个名为add的函数，执行两个Sales_data对象的加法
- 一个read函数，将数据从istream读入到Sales_data对象中
- 一个print函数，将Sales_data对象的值输出到ostream

**使用改进的Sales_data类**

```c++
Sales_data total;				// 保存当前求和结果的变量
if (read(cin, total)){			// 读入第一笔交易
    Sales_data trans;			// 保存下一条交易数据的变量
    while(read(cin, trans)) {	// 读入剩余的交易
        if (total.isbn() == trans.isbn()) // 检查isbn
            total.combine(trans);// 更新变量total当前的值
        else {
            print(cout, total) << endl;	// 输出结果
            total = trans;				// 处理下一本书	
        }
    }
    print(cout, total) << endl;			// 输出最后一条交易
} else {								// 没有输入任何信息		
    cerr << "No data?!" << endl;		// 通知用户
}
```



### 定义改进的Sales_data类

```c++
struct Sales_data{
    // 新成员:关于Sales_data对象的操作
    std::string isbn() const { return bookNo; }
    Sales_data& combine(const Sales_data&);
    double avg_price() const;
    
	std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
// Sales_data的非成员接口函数
Sales_data add(const Sales_data&, const Sales_data&);
std::ostream &print(std::ostream&, const Sales_data&);
std::istream &read(std::istream&, Sales_data&);

//定义成员函数
// const的作用是修改隐式this指针的类型
// 默认情况下,this的类型是指向类类型非常量版本的常量指针
// 紧跟在参数列表后面的 const 表示 this 是一个指向常量的指针。
// 使用const的成员函数被称作常量成员函数(constmember function)。
std::string isbn() const { return bookNo; }

//在类外部定义成员函数
double Sales_data::avg price() const {
    if (units_sold)
        return revenue / units_sold;
    else
        return 0;
}

Sales_data& Sales_data::combine(const Sales_data &rhs)
{
	units_sold += rhs.units_sold;			// 把rhs的成员加到this对象的成员上    
    revenue += rhs.revenue;
    return *this;							// 返回调用该函数的对象
}

```

### 定义类相关的非成员函数

```c++
//输入的交易信息包括ISBN、售出总数和售出价格
istream &read(istream &is, Sales_data &item)
{
    double price = 0;
    is >> item.bookNo >> item.units_sold >> price;
    item.revenue = price * item.units_sold;
    return is;
}

ostream &print(ostream &os, const Sales_data &item)
{
	os << item.isbn() << " " << item.units_sold << " " << item.revenue << " " << item.avg_price();
	return os;    
}

Sales_data add(const Sales_data &lhs, const Sales_data &rhs)
{
    Sales_data sum = lhs;		// 把lhs的数据成员拷贝给sum
    sum.combine(rhs);			// 把rhs的数据成员加到sum当中
    return sum;
}

```

### 构造函数

构造函数的名字和类名相同
构造函数没有返回类型
构造函数也有一个(可能为空的)参数列表和一个(可能为空的)函数体
类可以包含多个构造函数，不同的构造函数之间必须在参数数量或参数类型上有所区别

默认构造函数无须任何实参
	如果存在类内的初始值，用它来初始化成员
	否则，默认初始化该成员

**定义Sales_data的构造函数**

- 一个istream&，从中读取一条交易信息
- 一个const string&，表示ISBN编号；一个unsigned，表示售出的图书数量;以及一个 double，表示图书的售出价格
- 一个const string&，表示ISBN编号；编译器将赋予其他成员默认值
- 一个空参数列表(即默认构造函数)，正如刚刚介绍的，既然我们已经定义了其他构造函数，那么也必须定义一个默认构造函数。

```c++
struct Sales_data{
    //新增的构造函数
	Sales_data() = default;
    Sales_data(const std::string &s) : bookNo(s){}
    Sales_data(const std::string &s, unsigned n, double p) : bookNo(s), units_sold(n), revenue(p*n){}
    Sales_data(std::istream &);
   	
    //之前已有的其他成员
    std::string isbn() const { return bookNo; }
    Sales_data& combine(const Sales_data&);
    double avg_price() const;
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
```

**= default的含义**
	`Sales_data()=default;`
如果 = default 在类的内部，则默认构造函数是内联的；如果它在类的外部，则该成员默认情况下不是内联的。

**构造函数初始值列表**

```c++
Sales_data(const std::string &s) : bookNo(s) {}
Sales_data(const std::string &s, unsigned n, double p) : 
	bookNo(s), units_sold(n), revenue(p * n) {}
```

**在类外部定义构造函数**

```c++
Sales_data::Sales_data(std::istream &is)
{
    read(is, *this);	// read函数的作用是从is中读取一条交易信息然后
    					// 存入this对象中
}
```

### 拷贝、赋值和析构

不主动定义这些操作，则编译器将合成它们

**某些类不能依赖于合成的版本**

## 访问控制与封装

定义在public说明符之后的成员在**整个程序内可被访问**，public成员定义类的接口。
定义在private说明符之后的成员可以**被类的成员函数访问**，但是**不能被使用该类的代码访问**，private部分封装了(即隐藏了)类的实现细节。

```c++
class Sales_data {
public:						// 添加了访问说明符
    Sales_data() = default;
    Sales_data(const std::string &s, unsigned n, double p) : 
    		bookNo(s), units_sold(n), revenue(p * n) { }
    Sales_data(const std::string &s) : bookNo(s) { }
    Sales_data(std::istream&);
    
    std::string isbn() const { return bookNo; }
    Sales_data &combine(const Sales_data&);
    
private:					// 添加了访问说明符
    double avg_price() const
    	{ return units_sold ? revenue / units_sold : 0; }
    std::string bookNo;
    unsigned units_sold = 0;
    double revenue = 0.0;
};
```

**使用class或struct关键字**
唯一的一点区别是，struct和class的默认访问权限不一样
	如果我们使用**struct**关键字,则定义在第一个访问说明符之前的成员是**public**的
	相反，如果我们使用**class**关键字，则这些成员是**private**的

### 友元

类可以允许其他类或者函数访问它的非公有成员，方法是令其他类或者函数成为它的友元(friend)
友元声明只能出现在类定义的内部，但是在类内出现的具体位置不限
友元不是类的成员也不受它所在区域访问控制级别的约束

```c++
class Sales_data {
// 为Salesdata的非成员函数所做的友元声明
friend Sales_data add(const Sales_data&, const Sales_data&);
friend std::istream &read(std::istream&, Sales_data&);
friend std::ostream &print(std::ostream&, const Sales_data&);

// 其他成员及访问说明符与之前一致
public:
    Sales_data() = default;
    Sales_data(const std::string &s, unsigned n, double p) :
    	bookNo(s), units_sold(n), revenue(p * n) { }
    Sales_data(const std::string &s) : bookNo(s) { } 
    Sales_data(std::istream&);
    std::string isbn() const { return bookNo; }
    Sales_data &combine(const Sales_data&);

private:
    std::string bookNo;
    unsiqned units_sold = 0;
    double revenue = 0.0;
};
// Salesdata接口的非成员组成部分的声明
Sales_data add(const Sales_data&, const Sales_data&);
std::istream &read(std::istream&, Sales_data&);
std::ostream &print(std::ostream&, const Sales_data&);
```

**友元的声明**
友元的声明仅仅指定了访问的权限，而非一个通常意义上的函数声明
如果希望类的用户能够调用某个友元函数，那么就必须在友元声明之外再专门对函数进行一次声明

## 类的其他特性

包括:

> 类型成员
> 类的成员的类内初始值
> 可变数据成员
> 内联成员函数
> 从成员函数返回*this
> 关于如何定义并使用类类型
> 友元类的更多知识

### 类成员再探

```c++
// 定义一个类型成员
class Screen {
public:
    typedef std::string::size_type pos;

private:
    pos cursor = 0;
    pos height = 0, width = 0;
    std::string contents;
};

// Screen类的成员函数
class Screen {
public:
    typedef std::string::size_type pos;
    Screen() = default;//因为Screen有另一个构造函数, 所以本函数是必需的
    
    // cursor被其类内初始值初始化为0
    Screen(pos ht, pos wd, char c) : height(ht), width(wd), contents(ht * wd, c) { }
    char get() const 					// 读取光标处的字符
    	{ return contents[cursor]; }	// 隐式内联	
    inline char get(pos ht, pos wd) const;	// 显式内联
    Screen &move(pos r, pos c);				// 能在之后被设为内联
private:
    pos cursor = 0;
	pos height = 0, width = 0;
    std::string contents;
};

// 能在类的外部用inline关键字修饰函数的定义:
inline Screen &Screen::move(pos r, pos c)		// 可以在函数的定义处指定 inline
{
    pos row = r * width;						// 计算行的位置
    cursor = row + c;							// 在行内将光标移动到指定的列
    return *this;								// 以左值的形式返回对象
}

char Screen::get(pos r, pos c)const				// 在类的内部声明成inline
{
    pos row = r * width;						// 计算行的位置
    return contents[row + c];					// 返回给定列的字符
}
```

**可变数据成员**
一个可变数据成员(mutable data member)永远不会是const，即使它是const对象的成员
一个 const 成员函数可以改变一个可变成员的值

```c++
class Screen {
public:
	void some_member() const;
private:
    mutable size_t access_ctr;	// 即使在一个const对象内也能被修改
	// 其他成员与之前的版本一致
};

void Screen::some_member() const
{
    ++access_ctr;		// 保存一个计数值，用于记录成员函数被调用的次数	
    // 该成员需要完成的其他工作
}
```

**类数据成员的初始值**
C++11新标准中，最好的方式就是把这个默认值声明成一个类内初始值

```c++
class Window_mgr {
private:
    // 这个Window_mgr追踪的 Screen
    // 默认情况下，一个Window_mgr包含一个标准尺寸的空白Screen
    std::vector<Screen> screens{Screen(24, 80, ' ')};
}
// 当我们提供一个类内初始值时，必须以符号=或者花括号表示
```

### 返回*this的成员函数

```c++
class Screen {
public:
    Screen &set(char);
    Screen &set(pos, pos, char);
    // 其他成员和之前的版本一致
};
inline Screen &Screen::set(char c)
{
    contents[cursor] = c;		// 设置当前光标所在位置的新值
    return *this;				// 将this对象作为左值返回
}

inline Screen &Screen::set(pos r, pos col, char ch)
{
    contents[r * width + col] = ch;			// 设置给定位置的新值
    return *this;							// 将this对象作为左值返回
}

// 把光标移动到一个指定的位置，然后设置该位置的字符值
myScreen.move(4, 0).set('#');
```

**基于const的重载**

```c++
class Screen {
public:
    // 根据对象是否是 const 重载了display函数
    Screen &display(std::ostream &os)
    	{ do_display(os); return *this; }
    const Screen &display(std::ostream &os) const
    	{ do_display(os); return *this; }
    
private:
    // 该函数负责显示Screen的内容
    void do_display(std::ostream &os) const { os << contents; }
    // 其他成员与之前的版本一致
};

/*
	display 函数各自返回解引用this 所得的对象
	在非常量版本中，this 指向一个非常量对象，因此display 返回一个普通的(非常量)引用
	而const成员则返回一个常量引用
*/
Screen myScreen(5, 3);
const Screen blank(5, 3);
myScreen.set('#').display(cout);	// 调用非常量版本
blank.display(cout);				// 调用常量版本
```

### 类类型

每个类定义了唯一的类型

```c++
struct First
{
	int memi;
    int getMem();
};
struct Second {
    int memi;
    int getMem();
};
First obj1;
Second obj2 = obj1;			// 错误:obj1和obj2的类型不同
```

**类的声明**
	仅声明类而暂时不定义它
	在它声明之后定义之前是一个不完全类型(incomplete type)

只能在非常有限的情景下使用:
	可以定义指向这种类型的指针或引用
	也可以声明(但是不能定义)以不完全类型作为参数或者返回类型的函数。

因为只有当类全部完成后类才算被定义，所以**一个类的成员类型不能是该类自己**
	然而，一旦一个类的名字出现后，它就被认为是声明过了(但尚未定义)，因此**类允许包含指向它自身类型的引用或指针**

```c++
class Link_screen{
    Screen window;
    Link_screen *next;
    Link_screen *prev;
};
```

### 友元再探

类可以把其他的类定义成友元
也可以把其他类(之前已定义过的) 的成员函数定义成友元

友元函数能定义在类的内部，这样的函数是隐式内联的

```c++
class Screen {
    // Window_mgr的成员可以访问Screen类的私有部分
    friend class Window_mgr;
    // Screen类的剩余部分
};

class Window_mgr {
public:
    // 窗口中每个屏幕的编号
    using ScreenIndex = std::vector<Screen>::size_type;
    // 按照编号将指定的Screen重置为空白
    void clear(ScreenIndex);
private:
    std::vector<Screen> screens{Screen(24, 80, ' ')};
};

/*
	如果clear不是Screen的友元，下面的代码将无法通过编译
	因为此时clear将不能访问Screen的height、width和contents成员
*/
void Window_mgr::clear(ScreenIndex i)
{
    // s是一个Screen的引用，指向我们想清空的那个屏幕
    Screen &s = screens[i];
    // 将那个选定的Screen重置为空白
    s.contents = string(s.height * s.width, ' ');
}

// 令成员函数作为友元
class Screen {
    // Windowmgr::clear必须在Screen类之前被声明
    friend void Window_mgr::clear(ScreenIndex);
    // Screen类的剩余部分
};
//函数重载和友元
// 如果一个类想把一组重载函数声明成它的友元，它需要对这组函数中的每一个分别声明:
// 重载的storeOn函数
//  Screen类把接受ostream&的storeOn函数声明成它的友元，但是接受BitMap&作为参数的版本仍然不能访问screen
extern std::ostream& storeOn(std::ostream &, Screen &);
extern BitMap& storeOn(BitMap&, Screen &);
class Screen {
    // storeOn的ostream版本能访问Screen对象的私有部分
    friend std::ostream& storeOn(std::ostream &, Screen &);
    // ....
};

//友元声明和作用域
// 即使仅仅是用声明友元的类的成员调用该友元函数，它也必须是被声明过的:
struct X {
    friend void f() { /* 友元函数可以定义在类的内部 */ }
    X() { f(); }		// 错误:f还没有被声明
    void g();
    void h();
};

void X::g() { return f(); }		// 错误:f还没有被声明
void f();						// 声明那个定义在X中的函数
void X::h() { return f(); }		// 正确:现在f的声明在作用域中了
```

## 类的作用域

在类的作用域之外，普通的数据和函数成员只能由对象、引用或者指针使用成员访问运算符来访问
对于类类型成员则使用作用域运算符访问
不论哪种情况，跟在运算符之后的名字都必须是对应类的成员

```c++
//作用域和定义在类外部的成员
// 因为编译器在处理参数列表之前已经明确了我们当前正位于window mgr类的作用域中所以不必再专门说明 ScreenIndex 是 Window_mgr 类定义的。
void Window_mgr::clear(ScreenIndex i)
{
    Screen &s = screens[i];
    s.contents = string(s.height * s.width，' ');
}

class Window_mgr {
public:
    //向窗口添加一个Screen，返回它的编号
    ScreenIndex addscreen(const Screen&);
    //其他成员与之前的版本一致
};
// 首先处理返回类型，之后我们才进入Window_mgr的作用域
Window_mgr::ScreenIndex Window_mgr::addScreen(const Screen &s)
{
	screens.push_back(s);
    return screens.size() - 1;    
}
```

### 名字查找与类的作用域

首先，编译成员的声明
直到类全部可见后才编译函数体

```c++
typedef double Money;
string bal;
class Account {
public:
    Money balance() { return bal; }	// return Money bal
private:
    Money bal;
    // ...
};

//类型名要特殊处理
typedef double Money;
class Account{
public:
    Money balance() { return bal; }		// 使用外层作用域的Money
private:
    typedef double Money;				// 错误:不能重新定义Money
    Money bal;
    // ...
};

```

## 构造函数再探

### 构造函数初始值列表

```c++
string foo = "Hello World!";		// 定义并初始化
string bar;							// 默认初始化成空string对象
bar = "Hello World!";				// 为bar赋一个新值

//构造函数的初始值有时必不可少
class ConstRef {
public:
    ConstRef(int ii);
private:
    int i;
    const int ci;
    int &ri;
};
// 错误:ci和ri必须被初始化
ConstRef::ConstRef(int ii){//赋值:
	i = ii;			// 正确
    ci = ii;		// 错误:不能给 const 赋值
    ri = i;			// 错误:ri没被初始化
}
// 正确:显式地初始化引用和const成员
ConstRef::ConstRef(int ii) : i(i), ci(i), ri(i) {}

//成员初始化顺序
// 成员的初始化顺序与它们在类定义中的出现顺序一致
//  最好用构造函数的参数作为成员的初始值
class X {
	int i;
    int j;
public:    
	// 未定义的:i在之前被初始化
    X(int val) : j(val), i(j) { }    
};

//默认实参和构造函数
class Sales_data {
public:
    // 定义默认构造函数，令其与只接受一个string 实参的构造函数功能相同
    Sales data(std::string s = "") : bookNo(s) {}
    // 其他构造函数与之前一致
    Sales_data(std::string s, unsigned cnt, double rev) : 
    		bookNo(s), units_sold(cnt), revenue(rev * cnt) {}
    Sales_data(std::istream &is) { read(is, *this); } 
    // 其他成员与之前的版本一致
};
```

### 委托构造函数

它把它自己的一些(或者全部)职责委托给了其他构造函数

```c++
class Sales_data {
public:
	// 非委托构造函数使用对应的实参初始化成员
    Sales_data(std::string s, unsigned cnt, double price) : 
    	bookNo(s), units_sold(cnt), revenue(cnt * price) { }
    // 其余构造函数全都委托给另一个构造函数
    Sales_data() : Sales_data("", 0, 0) { }
    Sales_data(std::string s) : Sales_data(s, 0, 0) {}
    Sales_data(std::istream &is): Sales_data() { read(is, *this); }
    // 其他成员与之前的版本一致
};
```

### 默认构造函数的作用

**使用默认构造函数**

```c++
Sales_data obj();				// 正确:定义了一个函数而非对象
if (obj.isbn() == Primer_5th_ed.isbn()) //错误:ob是一个函数
    return;

// 定义一个使用默认构造函数进行初始化的对象
Sales_data obj;
```

### 隐式的类类型转换

如果构造函数**只接受一个实参**，则它实际上定义了转换为此类类型的隐式转换机制，有时我们把这种构造函数称作转换构造函数
只允许一步类类型转换

```c++
string null_book = "9-999-99999-9";
// 构造一个临时的Sales_data对象
// 该对象的units_sold 和 revenue等于0，bookNo等于null_book
item.combine(null_book);

// 错误:需要用户定义的两种转换:
// (1)把“g-999-99999-9”转换成string
// (2)再把这个(临时的)string 转换成Sales_data
item.combine("9-999-99999-9");

//正确:显式地转换成string，隐式地转换成Sales_data
item.combine(string("9-999-99999-9"));
//正确:隐式地转换成string，显式地转换成Sales_data
item.combine(Sales_data("9-999-99999-9"));

//抑制构造函数的隐式转换
// 声明为 explicit

class Sales_data {
public:
    Sales_data() = default;
    Sales_data(const std::string &s, unsigned n, double p) : 
    	bookNo(s), units_sold(n), revenue(p * n) { }
    explicit Sales_data(const std::strinq &s) : bookNo(s) { }
    explicit Sales_data(std::istream&);
    //其他成员与之前的版本一致
};
//  explicit构造函数只能用于直接初始化
Sales_data item1(null_book);	//正确:直接初始化
// 错误:不能将explicit构造函数用于拷贝形式的初始化过程
Sales_data item2 = null_book;

//正确:实参是一个显式构造的Salesdata对象
item.combine(Sales_data(null_book));
//正确:static_cast可以使用explicit的构造函数
item.combine(static_cast<Sales_data>(cin));
```

### 聚合类

聚合类(aggregate class)使得用户可以直接访问其成员，并且具有特殊的初始化语法形式。

- 所有成员都是public的
- 没有定义任何构造函数
- 没有类内初始值
- 没有基类，也没有virtual函数

```c++
struct Data{
    int ival;
    string s;  
};
// 可以提供一个花括号括起来的成员初始值列表，并用它初始化聚合类的数据成员
// val1.ival = 0; val1.s = string("Anna")
Data val1 = { 0, "Anna" };
//初始值的顺序必须与声明的顺序一致
// 错误:不能使用"Anna"初始化ival，也不能使用1024初始化s
Data val2 = { "Anna", 1024 };
```

### 字面值常量类

数据成员都是字面值类型的聚合类是字面值常量类

如果不是聚合类，满足下面的要求也是字面值常量类：

- 数据成员都必须是字面值类型
- 类必须至少含有一个 constexpr 构造函数
- 如果一个数据成员含有类内初始值，则内置类型成员的初始值必须是一条常量表达式
  或者如果成员属于某种类类型，则初始值必须使用成员自己的constexpr构造函数
- 类必须使用析构函数的默认定义，该成员负责销毁类的对象

```c++
class Debug {
public:
    // constexpr构造函数必须初始化所有数据成员，初始值或者使用constexpr 构造函数， 或者是一条常量表达式。
    constexpr Debug(bool b = true) : hw(b), io(b), other(b) { }
    constexpr Debug(bool h, bool i, bool o):
		hw(h), io(i), other(o) { }
    constexpr bool any() { return hw || io || other; }
    void set_io(bool b){ io = b; }
    void set_hw(bool b){ hw = b; }
    void set_other(bool b){ hw = b;}
private:
    bool hw;					// 硬件错误，而非TO错误
    bool io;					// IO错误
    bool other;					// 其他错误
};

// constexpr构造函数用于生成constexpr对象以及constexpr函数的参数或返回类型:
constexpr Debug io_sub(false, true, false);				// 调试 IO
if (io_sub.any())										// 等价于if(true)
    cerr << "print appropriate error messages" << endl;
constexpr Debug prod(false);							// 无调试
if (prod.any())											// 等价于if(false)
	cerr << "print an error message" << endl;
```

## 类的静态成员

```c++
//声明静态成员
class Account{
public:
    // 成员函数不用通过作用域运算符就能直接使用静态成员
    void calculate() { amount += amount * interestRate; }
    static double rate() { return interestRate; }
    static void rate(double);
private:
    std::string owner;
    double amount;
    // 静态成员的类内初始化，要求静态成员必须是字面值常量类型 constexpr
    static constexpr int period = 30;
    double daily_tbl[period];	// period是常量表达式
    static double interestRate;
    static double initRate();
};

//使用类的静态成员
double r;
r = Account::rate();			// 使用作用域运算符访问静态成员

Account ac1;
Account *ac2 = &ac1;
//调用静态成员函数rate的等价形式
r = ac1.rate();				// 通过Account的对象或引用
r = ac2->rate();			// 通过指向Account对象的指针

// 当在类的外部定义静态成员时，不能重复static关键字
void Account::rate(double newRate)
{
    interestRate = newRate;
}
// 定义并初始化一个静态成员
double Account::interestRate = initRate();

// 如果在类的内部提供了一个初始值，则成员的定义不能再指定一个初始值了
//  一个不带初始值的静态成员的定义
constexpr int Account::period;	// 初始值在类的定义内提供
```

**静态成员能用于某些场景，而普通成员不能**

```c++
// 静态数据成员可以是不完全类型
//  静态数据成员的类型可以就是它所属的类类型
class Bar
{
public:
    // ...
private:
    static Bar mem1;		// 正确:静态成员可以是不完全类型
    Bar *mem2;				// 正确:指针成员可以是不完全类型
    Bar mem3;				// 错误:数据成员必须是完全类型
};

// 可以使用静态成员作为默认实参
class Screen {
public:
	// bkground表示一个在类中稍后定义的静态成员
    Screen& clear(char = bkground);
private:
    static const char bkground;
};
```



# IO库

## IO类

`iostream `定义了用于读写流的基本类型
`fstream`定义了读写命名文件的类型
`sstream`定义了读写内存string对象的类型

| 头文件     | 类型                                                         |
| ---------- | ------------------------------------------------------------ |
| `iostream` | istream，wistream从流读取数据<br />ostream，wostream向流写入数据<br />iostream，wiostream读写流 |
| `fstream`  | ifstream，wifstream从文件读取数据<br />ofstream，wofstream向文件写入数据<br />fstream，wfstream读写文件 |
| `sstream`  | istringstream，wistringstream从string读取数据<br />ostringstream，wostringstream向string写入数据<br />stringstream，wstrinqstream读写string |

**IO类型间的关系**
继承机制
利用模板

### IO对象无拷贝或赋值

```c++
ofstream out1, out2;
out1 = out2;						// 错误:不能对流对象赋值
ofstream print(ofstream);			// 错误:不能初始化ofstream参数
out2 = print(out2);					// 错误:不能拷贝流对象

// 进行IO操作的函数通常以引用方式传递和返回流
// 读写一个IO对象会改变其状态，因此传递和返回的引用不能是 const 的
```

### 条件状态

| IO库条件状态      | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| strm::iostate     | strm是一种IO类型。是一种机器相关的类型，提供了表达条件状态的完整功能 |
| strm::badbit      | strm::badbit用来指出流已崩溃                                 |
| strm::failbit     | strm::failbit用来指出一个IO操作失败了                        |
| strm::eofbit      | strm::eofbit用来指出流到达了文件结束                         |
| strm::goodbit     | strm::goodbit用来指出流未处于错误状态。此值保证为零          |
| s.eof()           | 若流s的eofbit置位，则返回true                                |
| s.fail()          | 若流s的failbit或badbit置位，则返回true                       |
| s.bad()           | 若流s的badbit置位，则返回true                                |
| s.good()          | 若流s处于有效状态，则返回true                                |
| s.clear()         | 将流s中所有条件状态位复位，将流的状态设置为有效。返回void    |
| s.clear(flags)    | 根据给定的flags标志位，将流s中对应条件状态位复位。flags的类型为strm::iostate。返回void |
| s.setstate(flags) | 根据给定的flags标志位，将流s中对应条件状态位置位。flags的类型为strm::iostate。返回void |
| s.rdstate()       | 返回流s的当前条件状态，返回值类型为strm::iostate             |

一个流一旦发生错误，其上后续的IO操作都会失败。只有当一个流处于无错状态时，我们才可以从它读取数据，向它写入数据。

**查询流的状态**
	badbit 表示系统级错误，如不可恢复的读写错误
		通常情况下，一旦 badbit 被置位，流就无法再使用了
	在发生可恢复错误后，failbit 被置位
		如期望读取数值却读出一个字符等错误。这种问题通常是可以修正的，流还可以继续使用
	如果到达文件结束位置，eofbit 和 failbit 都会被置位
	goodbit 的值为0，表示流未发生错误
	如果badbit、failbit和eofbit 任一个被置位，则检测流状态的条件会失败。

**管理流的状态**

```c++
// 记住cin的当前状态
auto old_state = cin.rdstate();				// 记住cin的当前状态
cin.clear();								// 使cin有效
process_input(cin);							// 使用cin
cin.setstate(old_state);					// 将cin置为原有状态

// 复位 failbit和badbit，保持其他标志位不变
cin.clear(cin.rdstate() & ~ cin.failbit & ~cin.badbit);
```

### 管理输出缓冲

每个输出流都管理一个缓冲区，用来保存程序读写的数据
由于设备的写操作可能很耗时，允许操作系统将多个输出操作组合为单一的设备写操作可以带来很大的性能提升

导致缓冲刷新(即，数据真正写到输出设备或文件)的原因：

- 程序正常结束，作为main函数的return 操作的一部分，缓冲刷新被执行
- 缓冲区满时，需要刷新缓冲，而后新的数据才能继续写入缓冲区
- 可以使用操纵符如endl (参见1.2节，第6页)来显式刷新缓冲区
- 在每个输出操作之后，可以用操纵符unitbuf设置流的内部状态，来清空缓冲区。
  默认情况下，对cerr是设置unitbuf的，因此写到cerr的内容都是立即刷新的。
- 一个输出流可能被关联到另一个流
  在这种情况下，当读写被关联的流时，关联到的流的缓冲区会被刷新
  例如，默认情况下，cin和cerr 都关联到cout。因此，读cin或写cerr都会导致cout 的缓冲区被刷新。

**刷新输出缓冲区**

```c++
cout << "hi!" << endl;			// 输出hi和一个换行，然后刷新缓冲区
cout << "hi!" << flush;			// 输出hi，然后刷新缓冲区，不附加任何额外字符
cout << "hi!" << ends;			// 输出hi和一个空字符，然后刷新缓冲区

//unitbuf操纵符
cout << unitbuf;			// 所有输出操作后都会立即刷新缓冲区
// 任何输出都立即刷新，无缓冲
cout << nounitbuf;			// 回到正常的缓冲方式
```

**关联输入和输出流**
当一个输入流被关联到一个输出流时，任何试图从输入流读取数据的操作都会先刷新关联的输出流。

```c++
cin >> ival;		// 导致cout的缓冲区被刷新
```

tie有两个重载的版本:
	一个版本不带参数，返回指向输出流的指针。
		如果本对象当前关联到一个输出流，则返回的就是指向这个流的指针
		如果对象未关联到流，则返回空指针
	第二个版本接受一个指向ostream 的指针，将自己关联到此ostream

```c++
cin.tie(&cout);		//仅仅是用来展示:标准库将cin和cout关联在一起
// old_tie指向当前关联到cin的流(如果有的话)
ostream *old_tie = cin.tie(nullptr);// cin不再与其他流关联
// 将cin与cerr关联;这不是一个好主意，因为cin应该关联到cout
cin.tie(&cerr);				// 读取cin会刷新cerr而不是cout
cin.tie(old_tie);			// 重建cin和cout间的正常关联
```

## 文件输入输出

头文件fstream定义了三个类型来支持文件IO:
	fstream从一个给定文件读取数据
	ofstream向一个给定文件写入数据
	fstream可以读写给定文件

| fstream特有的操作       | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| fstream fstrm;          | 创建一个未绑定的文件流。fstream是头文件fstream中定义的一个类型 |
| fstream fstrm(s);       | 创建一个fstream，并打开名为s的文件。s可以是string类型或者是一个指向C风格字符串的指针<br />这些构造函数都是explicit的<br />默认的文件模式mode依赖于fstream的类型 |
| fstream fstrm(s, mode); | 与前一个构造函数类似，但按指定mode打开文件                   |
| fstrm.open(s)           | 打开名为s的文件，并将文件与 fstrm 绑定<br />s可以是一个string或一个指向C风格字符串的指针<br />默认的文件mode依赖于fstream的类型。返回void |
| fstrm.close()           | 关闭与fstrm绑定的文件。返回void                              |
| fstrm.is_open()         | 返回一个bool值，指出与fstrm关联的文件是否成功打开且尚未关闭  |

### 使用文件流对象

```c++
ifstream in(ifile);	// 构造一个ifstream并打开给定文件
ofstream out;		// 输出文件流未关联到任何文件

//用fstream代替iostream&
ifstream input(argv[1]);				// 打开销售记录文件
ofstream output(argv[2]);				// 打开输出文件
Sales_data total;						// 保存销售总额的变量
if (read(input, total)) {				// 读取第一条销售记录
    Sales_data trans;					// 保存下一条销售记录的变量
    while (read(input, trans)) {		// 读取剩余记录
        if (total.isbn() == trans.isbn())	// 检查isbn
            total.combine(trans);			// 更新销售总额
        else {
            print(outputrtotal) << endl;	// 打印结果
            total = trans;					// 处理下一本书
        }
    }
    print(output, total) << endl;			// 打印最后一本书的销售额
} else										// 文件中无输入数据
    cerr << "No data?!" << endl;

//成员函数open和close
ifstream in(ifile);		// 构筑一个ifstream并打开给定文件
ofstream out;			// 输出文件流未与任何文件相关联
out.open(ifile + ".copy");	// 打开指定文件
// 进行 open 是否成功的检测通常是一个好习惯:
if (out)		//检查open是否成功
	return;			//open成功，我们可以使用文件了

// 一旦一个文件流已经打开，它就保持与对应文件的关联。
// 为了将文件流关联到另外一个文件，必须首先关闭已经关联的文件。
// 一旦文件成功关闭，我们可以打开新的文件:
in.close();		//关闭文件
in.open(ifile + "2");	//打开另一个文件

//自动构造和析构
// 对每个传递给程序的文件执行循环操作
// 当一个fstream对象被销毁时，close会自动被调用
for (auto p = argv + 1; p != argv + argc; ++p) {
    ifstream input(*p);			// 创建输出流并打开文件
     if (input){				// 如果文件打开成功，“处理”此文件
         process(input);
     } else
         cerr << "couldn't open: " + string(*p);
}	// 每个循环步input都会离开作用域，因此会被销毁
```

### 文件模式

| 文件模式 |                              |
| -------- | ---------------------------- |
| in       | 以读方式打开                 |
| out      | 以写方式打开                 |
| app      | 每次写操作前均定位到文件末尾 |
| ate      | 打开文件后立即定位到文件末尾 |
| trunc    | 截断文件                     |
| binary   | 以二进制方式进行IO           |

指定文件模式有如下限制:

- 只可以对ofstream或fstream对象设定out模式
- 只可以对ifstream或fstream对象设定in模式
- 只有当out也被设定时才可设定trunc模式
- 只要 trunc 没被设定，就可以设定 app 模式
  在app模式下，即使没有显式指定out 模式，文件也总是以输出方式被打开
- 默认情况下，即使我们没有指定 trunc，以out 模式打开的文件也会被截断
  为了保留以out 模式打开的文件的内容，我们必须同时指定 app 模式，这样只会将数据追加写到文件末尾
  或者同时指定 in模式，即打开文件同时进行读写操作
- ate和binary模式可用于任何类型的文件流对象，且可以与其他任何文件模式组合使用

**以out模式打开文件会丢弃已有数据**

```c++
// 在这几条语句中，filel都被截断
ofstream out("file1");		// 隐含以输出模式打开文件并截断文件
ofstream out2("file1", ofstream::out);	// 隐含地截断文件
ofstream out3("file1", ofstream::out | ofstream::trunc);
// 为了保留文件内容，我们必须显式指定app模式
ofstream app("file2", ofstream::app);	// 隐含为输出模式
ofstream app2("file2", ofstream::out | ofstream::app);

//每次调用open时都会确定文件模式
ofstream out;			//未指定文件打开模式
out.open("scratchpad");	//模式隐含设置为输出和截断
out.close();			//关闭out，以便我们将其用于其他文件
out.open("precious", ofstream::app);//模式为输出和追加
out.close();
```

## string流

istringstream从string 读取数据
ostringstream向string 写入数据
stringstream既可从string读数据也可向string写数据

| stringstream特有的操作 | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| sstream strm;          | strm是一个未绑定的stringstream对象。sstream是头文件sstream中定义的一个类型 |
| sstream strm(s);       | strm是一个sstream对象，保存strings的一个拷贝。此构造函数是explicit的 |
| strm.str()             | 返回strm所保存的strinq的拷贝                                 |
| strm.str(s)            | 将strings拷贝到strm中。返回void                              |

### 使用istringstream

```c++
// 待录入数据
// 名称 家庭电话 工作电话 移动电话
// morgan 2015552368 8625550123
// drew 9735550130
// lee 6095550132 2015550175 8005550000

struct PersonInfo {
    string name;
    vector<string> phones;
};

string line, word;	// 分别保存来自输入的一行和单词
vector<PersonInfo> people;	// 保存来自输入的所有记录
// 逐行从输入读取数据，直至cin 遇到文件尾(或其他错误)
while (getline(cin, line)) {
    PersonInfo info;	// 创建一个保存此记录数据的对象
    istringstream record(line);	// 将记录绑定到刚读入的行
    record >> info.name;		// 读取名字
    while (record >> word)		// 读取电话号码
        info.phones.push_back(word);  // 保持它们
    people.push_back(info);		// 将此记录追加到people末尾
}
```

### 使用ostringstream

```c++
for (const auto &entry : people){		// 对people中每一项
    ostringstream formatted, badNums;	// 每个循环步创建的对象
    for (const auto& nums : entry.phones) {// 对每个数
		if (!valid(nums)){
            badNums << " " << nums; //将数的字符串形式存入badNums
        } else {
            // 将格式化的字符串“写入”formatted
            formatted << " " << format(nums);
        }
    }
    if (badNums.str().empty())			// 没有错误的数
        os << entry.name << " "			// 打印名字
        	<< formatted.str() << endl;	// 和格式化的数
    else								// 否则，打印名字和错误的数
        cerr << "input error:" << entry.name 
        		<< " invalid number(s) " << badNums.str() << endl;
}
```



# 顺序容器

顺序容器(sequential container)为程序员提供了控制元素存储和访问顺序的能力
这种顺序不依赖于元素的值，而是与元素加入容器时的位置相对应

## 顺序容器概述

| 顺序容器类型 | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| vector       | 可变大小数组。支持快速随机访问。在尾部之外的位置插入或删除元素可能很慢 |
| deque        | 双端队列。支持快速随机访问。在头尾位置插入/删除速度很快      |
| list         | 双向链表。只支持双向顺序访问。在list中任何位置进行插入/删除操作速度都很快 |
| forward_list | 单向链表。只支持单向顺序访问。在链表任何位置进行插入/删除操作速度都很快 |
| array        | 固定大小数组。支持快速随机访问。不能添加或删除元素           |
| string       | 与 vector 相似的容器，但专门用于保存字符。随机访问快。在尾部插入/删除速度快 |

选择容器的基本原则:

- 除非你有很好的理由选择其他容器，否则应使用 vector。
- 如果你的程序有很多小的元素，且空间的额外开销很重要，则不要使用 list 或forward_list
- 如果程序要求随机访问元素，应使用vector或deque
- 如果程序要求在容器的中间插入或删除元素，应使用list或forward_list
- 如果程序需要在头尾位置插入或删除元素，但不会在中间位置进行插入或删除操作，则使用 deque
- 如果程序只有在读取输入时才需要在容器中间位置插入元素，随后需要随机访问元素，则
  - 首先，确定是否真的需要在容器中间位置添加元素。当处理输入数据时，通常可以很容易地向 vector 追加数据，然后再调用标准库的 sort 函数来重排容器中的元素，从而避免在中间位置添加元素。
  - 如果必须在中间位置插入元素，考虑在输入阶段使用 list，一旦输入完成，将list中的内容拷贝到一个 vector中。



## 容器库概览

某些操作是所有容器类型都提供的

| 类型别名        | 说明                                                   |
| --------------- | ------------------------------------------------------ |
| iterator        | 此容器类型的迭代器类型                                 |
| const_iterator  | 可以读取元素，但不能修改元素的迭代器类型               |
| size_type       | 无符号整数类型，足够保存此种容器类型最大可能容器的大小 |
| difference_type | 带符号整数类型，足够保存两个迭代器之间的距离           |
| value_type      | 元素类型                                               |
| reference       | 元素的左值类型; 与value_type&含义相同                  |
| const_reference | 元素的const左值类型(即，const value_type&)             |

| 构造函数          | 说明                                                      |
| ----------------- | --------------------------------------------------------- |
| C c;              | 默认构造函数，构造空容器                                  |
| C c1(c2);         | 构造c2的拷贝c1                                            |
| C c(b, e);        | 构造c，将迭代器b和e指定的范围内的元素拷贝到c(array不支持) |
| C c{a, b, c ...}; | 列表初始化c                                               |

| 赋值与swap           | 说明                                        |
| -------------------- | ------------------------------------------- |
| c1 = c2              | 将c1中的元素替换为c2中元素                  |
| c1 = { a, b, c ... } | 将c1中的元素替换为列表中元素(不适用于array) |
| a.swap(b)            | 交换a和b的元素                              |
| swap(a, b)           | 与a.swap(b)等价                             |

| 大小         | 说明                                     |
| ------------ | ---------------------------------------- |
| c.size()     | c中元素的数目(不支持forward list)        |
| c.max_size() | c可保存的最大元素数目                    |
| c.empty()    | 若c中存储了元素，返回false，否则返回true |

| 添加/删除元素（不适用于array） | 说明                        |
| ------------------------------ | --------------------------- |
| c.insert(args)                 | 将args中的元素拷贝进c       |
| c.emplace(inits)               | 使用inits构造c中的一个元素  |
| c.erase(args)                  | 删除args指定的元素          |
| c.clear()                      | 删除c中的所有元素，返回void |

| 关系运算符   | 说明                           |
| ------------ | ------------------------------ |
| ==, !=       | 所有容器都支持相等(不等)运算符 |
| <, <=, >, >= | 关系运算符(无序关联容器不支持) |

| 获取迭代器           | 说明                                      |
| -------------------- | ----------------------------------------- |
| c.begin(), c.end()   | 返回指向c的首元素和尾元素之后位置的迭代器 |
| c.cbegin(), c.cend() | 返回const_iterator                        |

| 反向容器的额外成员（不支持forward_list） | 说明                                      |
| ---------------------------------------- | ----------------------------------------- |
| reverse_iterator                         | 按逆序寻址元素的迭代器                    |
| const_reverse_iterator                   | 不能修改元素的逆序迭代器                  |
| c.rbegin(), c.rend()                     | 返回指向c的尾元素和首元素之前位置的迭代器 |
| c.crbegin(), c.crend()                   | 返回const_reverse_iterator                |

### 迭代器

**迭代器范围**
两个迭代器通常被称为begin和end，或者是first 和last(可能有些误导)，它们标记了容器中元素的一个范围。
这种元素范围被称为左闭合区间 (left-inclusive interval)，其标准数学描述为 [begin，end)

**使用左闭合范围蕴含的编程假定**

- 如果begin与end相等，则范围为空
- 如果begin与end 不等，则范围至少包含一个元素，且 begin 指向该范围中的第一个元素
- 我们可以对begin递增若干次，使得begin == end

```c++
while (begin != end) {   
    *begin = val;			// 正确:范围非空，因此begin指向一个元素
    ++begin;				// 移动迭代器，获取下一个元素
} 
```

### 容器类型成员

```c++
//显式使用类名
// iter是通过list<string>定义的一个迭代器类型
list<string>::iterator iter;
// count是通过vector<int>定义的一个difference_type类型
vector<int>::difference_type count;
```

### begin和end成员

```c++
list<string> a = {"Milton", "Shakespeare", "Austen"};
auto it1 = a.begin();	// list<strinq>::iterator
auto it2 = a.rbegin();	// list<string>;:reverse_iterator
auto it3 = a.cbegin();	// list<string>::const_iterator
auto it4 = a.crbegin();	// list<string>::const_reverse_@iterator

//显式指定类型
list<string>::iterator it5 = a.begin();
list<string>::const_iterator it6 = a.begin(); 
// 是iterator还是 const_iterator依赖于a的类型
auto it7 = a.begin();	// 仅当a是const时，it7是const_iterator
auto it8 = a.cbeqin();	// it8是const_iterator
```

### 容器定义和初始化

|  容器定义和初始化                             | 说明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| C c;                                    | 默认构造函数。如果c是一个array，则c中元素按默认方式初始化；否则c为空 |
| C c1(c2);<br />C c1 = c2; | c1初始化为c2的拷贝。c1和c2必须是相同类型(即，它们必须是相同的容器类型，且保存的是相同的元素类型；对于array类型，两者还必须具有相同大小) |
| C c{a, b, c...}<br />C c = {a, b, c...} | c初始化为初始化列表中元素的拷贝。列表中元素的类型必须与c的元素类型相容。对于array类型，列表中元素数目必须等于或小于array的大小，任何遗漏的元素都进行值初始化(参见3.3.1节，第88页) |
| C c(b,e)                                | c初始化为迭代器b和e指定范围中的元素的拷贝。范围中元素的类型必须与c的元素类型相容(array不适用) |
|  | 只有顺序容器 (不包括array)的构造函数才能接受大小参数 |
| C seq(n) | seq 包含 n个元素，这些元素进行了值初始化;此构造函数是explicit的。(string 不适用) |
| C seq(n, t) | seq包含n个初始化为值t的元素 |

**将一个容器初始化为另一个容器的拷贝**
可以直接拷贝整个容器，或者(array除外)拷贝由一个迭代器对指定的元素范围

```c++
// 每个容器有三个元素，用给定的初始化器进行初始化
list<string> authors = {"Milton", "Shakespeare", "Austen"};
vector<const char*> articles = {"a", "an", "the"};
list<string> list2(authors);		// 正确:类型匹配
deque<string> authList(authors);	// 错误:容器类型不匹配
vector<string> words(articles);		// 错误:容器类型必须匹配
// 正确:可以将const char*元素转换为string
forward_list<string> words(articles.beqin(), articles.end());

// 拷贝元素，直到(但不包括)it 指向的元素
deque<string> authList(authors.begin(), it);

//列表初始化
// 每个容器有三个元素，用给定的初始化器进行初始化
list<string> authors = {"Milton", "Shakespearer", "Austen"};
vector<const char*> articles = {"a", "an", "the"};

//与顺序容器大小相关的构造函数
vector<int> ivec(10, -1);			// 10个int元素，每个都初始化为-1
list<string> svec(10, "hi!");		// 10个strings;每个都初始化为"hi!"
forward_list<int> ivec(10);			// 10个元素，每个都初始化为 0
deque<string> svec(10);				// 10个元素，每个都是空string

//标准库array具有固定的大小
// 标准库 array 的大小也是类型的一部分。当定义一个array 时，除了指定元素类型，还要指定容器大小:
array<int, 42>			//类型为:保存42个int的数组
array<string, 10>		//类型为:保存10个string的数组

array<int, 10>::size_type i;		// 数组类型包括元素类型和大小
array<int>::size_type j;			// 错误:array<int>不是一个类型

array<int, 10> ial;			//10个默认初始化的int
array<int, 10> ia2 = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};	//列表初始化
array<int, 10> ia3 = {42}; 			//a3[0]为42，剩余元素为0

int digs[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int cpy[10] = digs;					// 错误:内置数组不支持拷贝或赋值
array<int, 10> digits = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
array<int, 10> copy = digits;		// 正确:只要数组类型匹配即合法
```

### 赋值和swap

```c++
// 将c1的内容替换为c2中元素的拷贝
c1 = c2;
cl = {a, b, c};		//赋值后，c1大小为3

array<int, 10> a1 = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
array<int, 10> a2 = {0};		// 所有元素值均为0
a1 = a2; 						// 替换a1中的元素
a2 = {0};						// 错误:不能将一个花括号列表赋予数组
```

| 容器赋值运算                  | 说明                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| c1 = c2                       | 将c1中的元素替换为c2中元素的拷贝。c1和c2必须具有相同的类型   |
| c = {a, b, c...}              | 将c1中元素替换为初始化列表中元素的拷贝(array不适用)          |
| swap{c1, c2}<br />c1.swap(c2) | 交换c1和c2中的元素。c1和c2必须具有相同的类型。swap通常比从c2向c1拷贝元素快得多 |
|                               | assign 操作不适用于关联容器和array                           |
| seq.assign(b, e)              | 将 seq中的元素替换为迭代器b和e所表示的范围中的元素。迭代器b和e不能指向seq中的元素 |
| seq.assign(il)                | 将seq中的元素替换为初始化列表il中的元素                      |
| seq.assign(n, t)              | 将seq中的元素替换为n个值为t的元素                            |



```c++
//使用assign（仅顺序容器）
list<string> names;
vector<const char*> oldstyle;
names = oldstyle;			// 错误:容器类型不匹配
// 正确:可以将const char*转换为string
names.assign(oldstyle.cbegin(), oldstyle.cend());

// 等价于slist1.clear();后跟slistl.insert(slist1.begin(), 10, "Hiya!");
list<string> slist1(1);		// 1个元素，为空string
slist1.assign(10, "Hiya!"); // 10个元素，每个都是“Hiya!”

//使用swap
// swap 只是交换了两个容器的内部数据结构
//  但是，swap两个array 会真正交换它们的元素
vector<string> svec1(10);//10个元素的vector
vector<string> svec2(24);//24个元素的vector
swap(svec1, svec2);
```

### 容器大小操作

成员函数size返回容器中元素的数目
empty当size为0时返回布尔值 true，否则返回 false
max_size返回一个大于或等于该类型容器所能容纳的最大元素数的值

forward_list支持max_size和empty，但不支持size

### 关系运算符

- 如果两个容器具有相同大小且所有元素都两两对应相等，则这两个容器相等:否则两个容器不等。
- 如果两个容器大小不同，但较小容器中每个元素都等于较大容器中的对应元素，则较小容器小于较大容器
- 如果两个容器都不是另一个容器的前缀子序列，则它们的比较结果取决于第一个不相等的元素的比较结果。

```c++
vector<int> v1 = {1, 3, 5, 7, 9, 12};
vector<int> v2 = {1, 3, 9};
vector<int> v3 = {1, 3, 5, 7};
vector<int> v4 = {1, 3, 5, 7, 9, 12};
v1 < v2;		// true: v1和v2在元素[2]处不同: v1[2]小于等于v2[2]
v1 < v3;		// false; 所有元素都相等，但v3中元素数目更少
v1 == v4;		// true;每个元素都相等，且v1和v4大小相同
v1 == v2;		// false;v2元素数目比v1少

//容器的关系运算符使用元素的关系运算符完成比较
// 容器的相等运算符实际上是使用元素的==运算符实现比较的
// 其他关系运算符是使用元素的<运算符
// 如果元素类型不支持所需运算符，那么保存这种元素的容器就不能使用相应的关系运算。
```

## 顺序容器操作

### 向顺序容器添加元素

这些操作会改变容器的大小;array不支持这些操作
forward_list有自己专有版本的insert和emplace
forward_list不支持push_back和emplace_back
vector和string不支持push_front和emplace_front

| 向顺序容器添加元素的操作                   |                                                              |
| ------------------------------------------ | ------------------------------------------------------------ |
| c.push_back(t)<br />c.emplace_back(args)   | 在c的尾部创建一个值为t或由args创建的元素。返回void           |
| c.push_front(t)<br />c.emplace_front(args) | 在c的头部创建一个值为t或由args创建的元素。返回void           |
| c.insert(p, t)<br />c.emplace(p, args)     | 在迭代器p指向的元素之前创建一个值为t或由args创建的元素。返回指向新添加的元素的迭代器 |
| c.insert(p, n, t)                          | 在迭代器p指向的元素之前插入n个值为的元素。返回指向新添加的第一个元素的迭代器;若n为0，则返回p |
| c.insert(p, b, e)                          | 将迭代器b和e指定的范围内的元素插入到迭代器p指向的元素之前。b和e不能指向c中的元素。返回指向新添加的第一个元素的迭代器;若范围为空，则返回p |
| c.insert(p, il)                            | il是一个花括号包围的元素值列表。将这些给定值插入到迭代器p指向的元素之前。返回指向新添加的第一个元素的迭代器若列表为空，则返回p |

emplace_front、emplace和emplace_back，这些操作**构造**而不是拷贝元素.

### 访问元素

包括array在内的每个顺序容器都有一个 front 成员函数
除forward_list之外的所有顺序容器都有一个 back 成员函数
这两个操作分别返回首元素和尾元素的引用:

```c++
//在解引用一个迭代器或调用 front或back之前检查是否有元素
if(!c.empty()) {
    // val和val2是c中第一个元素值的拷贝
    auto val = *c.begin(), val2 = c.front();
    // va13和val4是c中最后一个元素值的拷贝
    auto last = c.end();
    auto val3 = *(--last);	// 不能递减forward_list选代器
    auto va14 = c.back(); 	// forward_list不支持
}
```

at和下标操作只适用于string、vector、deque和array
back不适用于forward_list

| 在顺序容器中访问元素的操作 |                                                              |
| -------------------------- | ------------------------------------------------------------ |
| c.back()                   | 返回c中尾元素的引用。若c为空，函数行为未定义                 |
| c.front()                  | 返回c中首元素的引用。若c为空，函数行为未定义                 |
| c[n]                       | 返回c中下标为n的元素的引用,n是一个无符号整数。若n >= csize()则函数行为未定义 |
| c.at(n)                    | 返回下标为n的元素的引用。如果下标越界，则抛出 out_of_range异常 |

### 删除元素

forward_list有特殊版本的erase
forward_list不支持pop_back; vector和string不支持pop_front

|               | 顺序容器的删除操作                                           |
| ------------- | ------------------------------------------------------------ |
| c.pop_back()  | 删除c中尾元素。若c为空，则函数行为未定义。函数返回void       |
| c.pop_front() | 删除c中首元素。若c为空，则函数行为未定义。函数返回void       |
| c.erase(p)    | 删除迭代器p所指定的元素，返回一个指向被删元素之后元素的迭代器，若p指向尾元素，则返回尾后 (off-the-end)迭代器。若p是尾后迭代器，则函数行为未定义 |
| c.erase(b, e) | 删除迭代器b和e所指定范围内的元素。返回一个指向最后一个被删元素之后元素的迭代器，若e本身就是尾后迭代器，则函数也返回尾后迭代器 |
| c.clear()     | 删除c中的所有元素。返回void                                  |



```c++
// pop_front和pop_back成员函数
while (!ilist.empty()) {
    process(ilist.front());		// 对ilist的首元素进行一些处理
    ilist.pop_front();			// 完成处理后删除首元素
}

//从容器内部删除一个元素
list<int> lst = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
auto it = lst.begin();
while (it != lst.end())
    if(*it % 2)		//若元素为奇数
        it = lst.erase(it); //删除此元素
	else
        ++it;

//删除多个元素
// 删除两个迭代器表示的范围内的元素
// 返回指向最后一个被删元素之后位置的迭代器
elem1 = slist.erase(eleml, elem2);		//调用后，eleml==elem2
slist.clear();	//删除容器中所有元素
slist.erase(slist.begin(), slist.end());//等价调用
```

### 特殊的forward_list操作

![forward_list的特殊操作](\Picture\forward_list的特殊操作.png)

一个forward_list 中添加或删除元素的操作是通过改变给定元素之后的元素来完成的。

| 在forwardlist中插入或删除元素的操作                          |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Ist.before_begin()<br />lst.cbefore_begin()                  | 返回指向链表首元素之前不存在的元素的迭代器。此迭代器不能解引用。cbefore_begin()返回一个const_iterator |
| lst.insert_after(p, t)<br />lst.insert_after(p, n, t)<br />lst.insert_after(p, b, e)<br />lst.insert_after(p, il) | 在迭代器p之后的位置插入元素。t 是一个对象，n 是数量b和e是表示范围的一对迭代器(b和e不能指向lst内)，il是一个花括号列表。返回一个指向最后一个插入元素的迭代器。如果范围为空，则返回p。若p为尾后迭代器，则函数行为未定义 |
| emplace_after(p, args)                                       | 使用args在p指定的位置之后创建一个元素。返回一个指向这个新元素的迭代器。若p为尾后迭代器，则函数行为未定义 |
| lst.erase_after(p)<br />Ist.erase_after(b, e)                | 删除p指向的位置之后的元素，或删除从b之后直到(但不包含)e之间的元素。返回一个指向被删元素之后元素的迭代器，若不存在这样的元素，则返回尾后迭代器。如果p指向lst的尾元素或者是一个尾后迭代器，则函数行为未定义 |

```c++
forward_list<int> flst = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
auto prev = flst.before_begin();		// 表示flst的“首前元素”
auto curr = flst.begin();				// 表示flst中的第一个元素
while (curr != flst.end()) {			// 仍有元素要处理
    if (*curr % 2)						// 若元素为奇数
        curr = flst.erase_after(prev);	// 删除它并移动curr
    else {
        prev = curr;					// 移动迭代器curr，指向下一个元素，prev指向
        ++curr;							// curr 之前的元素
    }
}
```

### 改变容器大小

```c++
list<int> ilist(10, 42);		// 10个int:每个的值都是42
ilist.resize(15);				// 将5个值为0的元素添加到ilist的末尾
ilist.resize(25, -1);			// 将10个值为-1的元素添加到 ilist的末尾
ilist.resize(5);				// 从ilist末尾删除20个元素
```

| 顺序容器大小操作 |                                                              |
| ---------------- | ------------------------------------------------------------ |
| c.resize(n)      | 调整c的大小为n个元素。若n<c.size()，则多出的元素被丢弃。若必须添加新元素，对新元素进行值初始化 |
| c.resize(n, t)   | 调整c的大小为n个元素。任何新添加的元素都初始化为值t          |

**容器操作可能使迭代器失效**

## vector对象是如何增长的

当不得不获取新的内存空间时，vector和string 的实现通常会分配比新的空间需求更大的内存空间
容器预留这些空间作为备用，可用来保存更多的新元素

shrink_to_fit只适用于vector、string和deque
capacity和reserve只适用于vector和string

| 容器大小管理操作  |                                           |
| ----------------- | ----------------------------------------- |
| c.shrink_to_fit() | 请将capacity()减少为与size()相同大小      |
| c.capacity()      | 不重新分配内存空间的话，c可以保存多少元素 |
| c.reserve(n)      | 分配至少能容纳n个元素的内存空间           |

```c++
vector<int> ivec;
// size应该为0;capacity的值依赖于具体实现
cout << "ivec: size: " << ivec.size()
    << " capacity: " << ivec.capacity() << endl;
//向ivec添加24个元素
for (vector<int>::size_type ix = 0; ix != 24; ++ix)
    ivec.push_back(ix);

//size应该为24;capacity应该大于等于24，具体值依赖于标准库实现
cout << "ivec:size: " << ivec.size() 
    << "capacity: " << ivec,capacity() << endl;

// ivec: size: 0 capacity: 0
// ivec: size: 24 capacity: 32
```



## 额外的string操作

| 构造string的其他方法     | (n、len2和pos2都是无符号值)                                  |
| ------------------------ | ------------------------------------------------------------ |
| string s(cp, n)          | s是cp指向的数组中前n个字符的拷贝。此数组至少应该包含n个字符  |
| string s(s2, pos2)       | s是strings2从下标pos2开始的字符的拷贝。若pos2>s2size()，构造函数的行为未定义 |
| string s(s2, pos2, len2) | s是string s2从下标pos2开始len2个字符的拷贝若pos2>s2.size()，构造函数的行为未定义。不管len2的值是多少，构造函数至多拷贝s2.size()-pos2个字符 |

```c++
const char *cp = "HelloWorld!!!!";		// 以空字符结束的数组
char noNull[] = {'H', 'i'};				// 不是以空字符结束
string s1(cp);			// 拷贝cp中的字符直到遇到空字符;s1=="Hello World!!!"

string s2(noNul1, 2);		// 从noNull拷贝两个字符;s2=="Hi"
string s3(noNull);			// 未定义:noNull不是以空字符结束
string s4(cp+6, 5);			// 从cp[6]开始拷贝5个字符;s4=="World"
string s5(s1, 6, 5);		// 从s1[6]开始拷贝5个字符;s5=="World"
string s6(s1, 6);			// 从s1[6]开始拷贝，直至sl末尾;s6=="World!!!"
string s7(s1, 6, 20);		// 正确，只拷贝到s1末尾;s7=="World!!!"
string s8(s1, 16);			// 抛出一个out_of_range异常

//substr操作
string s("helloworld");
string s2 = s.substr(0, 5);		// s2 = hello
string s3 = s.substr(6);		// s3 = world
string s4 = s.substr(6, 11);	// s4 = world
string s5 = s.substr(12);		// 抛出一个out_of_range异常
```

| 子字符串操作     |                                                              |
| ---------------- | ------------------------------------------------------------ |
| s.substr(pos, n) | 返回一个string，包含s中从pos 开始的n个字符的拷贝。pos的默认值为0。n的默认值为s.size() - pos，即拷贝从pos开始的所有字符 |

### 改变string的其他方法

| 修改string的操作       |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| s.insert(pos, args)    | 在pos之前插入args指定的字符。pos可以是一个下标或一个选代器。接受下标的版本返回一个指向s的引用:接受迭代器的版本返回指向第一个插入字符的迭代器 |
| s.erase(pos, len)      | 删除从位置pos开始的len个字符。如果len被省略，则删除从pos开始直至s末尾的所有字符。返回一个指向s的引用 |
| s.assign(args)         | 将s中的字符替换为args指定的字符。返回一个指向s的引用         |
| s.append(args)         | 将args追加到s。返回一个指向s的引用                           |
| s.replace(range, args) | 删除s中范围range内的字符，替换为args指定的字符。range或者是一个下标和一个长度，或者是一对指向s的迭代器。返回一个指向s的引用 |

### string搜索操作

| string搜索操作            |                                               |
| ------------------------- | --------------------------------------------- |
| s.find(args)              | 查找s中args第一次出现的位置                   |
| s.rfind(args)             | 查找s中args最后一次出现的位置                 |
| s.find_first_of(args)     | 在s中查找args中任何一个字符第一次出现的位置   |
| s.find_last_of(args)      | 在s中查找args中任何一个字符最后一次出现的位置 |
| s.find_first_not_of(args) | 在s中查找第一个不在args中的字符               |
| s.find_last_not_of(args)  | 在s中查找最后一个不在args中的字符             |

### compare函数

根据s是等于、大于还是小于参数指定的字符串，s.compare返回0、正数或负数

### 数值转换

| string和数值之间的转换                                       |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| to_string(val)                                               | 组重载函数，返回数值val的string表示。val可以是任何算术类型(参见2.1.1节，第30页)。对每个浮点类型和int或更大的整型，都有相应版本的tostring。与往常一样，小整型会被提升 |
| stoi(s, p, b)<br />stol(s, p, b)<br />stoul(s, p, b)<br />stoll(s, p, b)<br />stoull(s, p, b) | 返回s的起始子串(表示整数内容)的数值,返回值类型分别是intlong、unsignedlong、long long、unsigned long long。b表示转换所用的基数，默认值为10。p是size_t指针，用来保存s中第一个非数值字符的下标，p默认为0，即，函数不保存下标 |
| stof(s, p)<br />stod(s, p)<br />stold(s, p)                  | 返回s的起始子串(表示浮点数内容)的数值，返回值类型分别是float、double或long double。参数p的作用与整数转换函数中一样 |

## 容器适配器

本质上，一个适配器是一种机制，能使某种事物的行为看起来像另外一种事物一样
一个容器适配器接受一种已有的容器类型，使其行为看起来像一种不同的类型

