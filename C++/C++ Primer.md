# 变量和基本类型

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

