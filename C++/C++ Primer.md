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
