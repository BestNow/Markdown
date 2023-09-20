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

| 容器定义和初始化                        | 说明                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| C c;                                    | 默认构造函数。如果c是一个array，则c中元素按默认方式初始化；否则c为空 |
| C c1(c2);<br />C c1 = c2;               | c1初始化为c2的拷贝。c1和c2必须是相同类型(即，它们必须是相同的容器类型，且保存的是相同的元素类型；对于array类型，两者还必须具有相同大小) |
| C c{a, b, c...}<br />C c = {a, b, c...} | c初始化为初始化列表中元素的拷贝。列表中元素的类型必须与c的元素类型相容。对于array类型，列表中元素数目必须等于或小于array的大小，任何遗漏的元素都进行值初始化(参见3.3.1节，第88页) |
| C c(b,e)                                | c初始化为迭代器b和e指定范围中的元素的拷贝。范围中元素的类型必须与c的元素类型相容(array不适用) |
|                                         | 只有顺序容器 (不包括array)的构造函数才能接受大小参数         |
| C seq(n)                                | seq 包含 n个元素，这些元素进行了值初始化;此构造函数是explicit的。(string 不适用) |
| C seq(n, t)                             | seq包含n个初始化为值t的元素                                  |

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

| 所有容器适配器都支持的操作和类型 |                                                              |
| -------------------------------- | ------------------------------------------------------------ |
| size_type                        | 一种类型，足以保存当前类型的最大对象的大小                   |
| value_type                       | 元素类型                                                     |
| container_type                   | 实现适配器的底层容器类型                                     |
| A a;                             | 创建一个名为a的空适配器                                      |
| A a(c);                          | 创建一个名为a的适配器，带有容器c的一个拷贝                   |
| 关系运算符                       | 每个适配器都支持所有关系运算符:==、!=、<、<=、>和>=这些运算符返回底层容器的比较结果 |
| a.empty()                        | 若a包含任何元素，返回false，否则返回true                     |
| a.size()                         | 返回a中的元素数目                                            |
| swap(a, b)<br />a.swap(b)        | 交换a和b的内容，a和b必须有相同类型，包括底层容器类型也必须相同 |

```c++
//定义一个适配器
stack<int> stk(deq);		//从deq拷贝元素到stk

// 在vector上实现的空栈
stack<string, vector<string>> str_stk;
// strstk2在vector上实现，初始化时保存svec的拷贝
stack<string, vector<string>> str_stk2(svec);

//栈适配器
stack<int> intStack;//空栈
//填满栈
for (size_t ix = 0; ix != 10; ++ix)
    intStack.push(ix);				// intStack保存0到9十个数
while (!intStack.empty()){ 			// intStack 中有值就继续循环
    int value = intStack.top();
    //使用栈顶值的代码
    intStack.pop();					// 弹出栈顶元素，继续循环
}
```

栈默认基于deque实现，也可以在 list或vector之上实现

| 栈的单独操作                       |                                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| s.pop()                            | 删除栈顶元素，但不返回该元素值                               |
| s.push(item)<br />s.emplace (args) | 创建一个新元素压入栈顶，该元素通过拷贝或移动item而来，或者由args构造 |
| s.top()                            | 返回栈顶元素，但不将元素弹出栈                               |

queue默认基于deque实现，priority_queue默认基于vector实现
queue也可以用list或vector实现，priority_queue 也可以用deque实现

| 队列的单独操作                    |                                                              |
| --------------------------------- | ------------------------------------------------------------ |
| q.pop()                           | 返回queue的首元素或priority_queue的最高优先级的元素但不删除此元素 |
| q.front()<br />q.back()           | 返回首元素或尾元素，但不删除此元素<br />只适用于queue        |
| q.top()                           | 返回最高优先级元素，但不删除该元素<br />只适用于priority_queue |
| q.push(item)<br />q.emplace(args) | 在queue末尾或priority_queue中恰当的位置创建一个元素，其值为item，或者由args构造 |


priority_queue 允许我们为队列中的元素建立优先级。新加入的元素会排在所有优先级比它低的已有元素之前。


# 泛型算法

称它们为“算法”，
	是因为它们实现了一些经典算法的公共接口，如排序和搜索

称它们是“泛型的”
	是因为它们可以用于不同类型的元素和多种容器类型(不仅包括标准库类型，如 vector 或lst，还包括内置的数组类型)，以及我们将看到的，还能用于其他类型的序列

## 泛型算法分类

### 只读算法

```c++
// 对vec中的元素求和，和的初值是0
int sum = accumulate(vec.cbegin(), vec.cend(), 0);

string sum = accumulate(v.cbegin(), v.cend(), string(""));
// 错误:const char*上没有定义+运算符
string sum = accumulate(v.cbegin(), v.cend(), "");

// roster2中的元素数目应该至少与roster1一样多
equal(roster1.cbegin(), roster1.cend(), roster2.cbegin());
```

### 写容器元素的算法

```c++
fill(vec.begin(), vec.end(), 0);// 将每个元素重置为0
// 将容器的一个子序列设置为10
fill(vec.begin(), vec.begin() + vec.size() / 2, 10);

vector<int> vec;		// 空vector
// 使用vec，赋予它不同值
fill_n(vec.begin(), vec.size(), 0);	// 将所有元素重置为0

vector<int>vec;	// 空向量
// 灾难:修改 vec中的10个(不存在)元素
fill_n(vec.begin(), 10, 0);

// back_inserter接受一个指向容器的引用，返回一个与该容器绑定的插入迭代器。
// 当我们通过此迭代器赋值时，赋值运算符会调用push_back将一个具有给定值的元素添加到容器中:
vector<int> vec;	// 空向量
auto it = back_inserter(vec);	// 通过它赋值会将元素添加到vec中
*it = 42;		// vec中现在有一个元素，值为42

vector<int> vec;	// 空向量
// 正确:backinserter 创建一个插入迭代器，可用来向vec添加元素
fill_n(back_inserter(vec), 10, 0);	// 添加10个元素到vec

//拷贝算法
int al[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int a2[sizeof(a1) / sizeof(*a1)];	// a2与al大小一样
// ret指向拷贝到a2的尾元素之后的位置
auto ret = copy(begin(a1), end(a1), a2);	// 把a1的内容拷贝给a2

// 将所有值为0的元素改为 42
replace(ilst.begin(), ilst.end(), 0, 42);

// 使用back_inserter按需要增长目标序列
// 此调用后，ilst并未改变，ivec包含ilst的一份拷贝，不过原来在ilst中值为0的元素在ivec中都变为42
replace_copy(ilst.cbegin(), ilst.cend(), back_inserter(ivec), 0, 42);
```

### 重排容器元素的算法

```c++
// Input: the quick red fox jumps over the slow red turtle
// Output：fox jumps over quick red slow the turtle
void elimDups(vector<string> &words)
{
    // 按字典序排序 words，以便查找重复单词
    sort(words.begin(), words.end());
    // unique重排输入范围，使得每个单词只出现一次
    // 排列在范围的前部，返回指向不重复区域之后一个位置的迭代器
    auto end_unique = unique(words.begin(), words.end());
    // 使用向量操作erase删除重复单词
    words.erase(end_unique, words.end());
}
```

## 定制操作

谓词：
	谓词是一个可调用的表达式，其返回结果是一个能用作条件的值
	标准库算法所使用的谓词分为两类:
		一元谓词(unary predicate，意味着它们只接受单一参数)
		二元谓词(binary predicate，意味着它们有两个参数)
	接受谓词参数的算法对输入序列中的元素调用谓词，因此，元素类型必须能转换为谓词的参数类型

```c++
// 比较函数，用来按长度排序单词
bool isShorter(const string &sl, const string &s2)
{
    return sl.size() < s2.size();
}

// 按长度由短至长排序words
sort(words.begin(), words.end(), isShorter);

//排序算法
elimDups(words);//将words按字典序重排，并消除重复单词
// 按长度重新排序，长度相同的单词维持字典序
stable_sort(words.begin(), words.end(), isShorter);
for (const auto &s : words) //无须拷贝字符串
    cout << s << " ";	//打印每个元素，以空格分隔
cout << endl;
```

### lambda 表达式

一个lambda表达式表示一个可调用的代码单元。
我们可以将其理解为一个未命名的内联函数。
与任何函数类似，一个 lambda 具有一个返回类型、一个参数列表和一个函数体。
但与函数不同，lambda可能定义在函数内部。一个lambda表达式具有如下形式

```c++
[capture list](parameter list) -> return type { function body }
// capture list(捕获列表)是一个lambda所在函数中定义的局部变量的列表(通常为空);
// return type、parameter list和function body与任何普通函数一样，分别表示返回类型参数列表和函数体。
// 与普通函数不同，lambda 必须使用尾置返回来指定返回类型。

// 可以忽略参数列表和返回类型，但必须永远包含捕获列表和函数体
auto f = []{ return 42; };
cout << f() << endl;	// 打印42

//向lambda传递参数
[](const string &a, const string &b)
	{ return a.size() < b.size(); }

// 按长度排序，长度相同的单词维持字典序
stable_sort(words.begin(), words.end(), 
            [](const string &a, const string &b) 
            	{ return a.size() < b.size(); });

[sz](const string &a)
	{ return a.size() >= sz; };
//错误:sz未捕获
[](const string &a)
	{ return a.size() >= sz; };
// 获取一个迭代器，指向第一个满足size()>=sz的元素
auto wc = find_if(words.begin(), words.end(),
                  [sz](const string &a)
                  	{ return a.size() >= sz; });

//for_each算法
// 打印长度大于等于给定值的单词，每个单词后面接一个空格
for_each(wc, words.end(),
         [](const string &s) { cout << s << " ";});
cout << endl;

//完整的biggies
void biggies(vector<string> &words, 
             vector<string>::size_type sz)
{
    elimDups(words);// 将words按宇典序排序，删除重复单词
    // 按长度排序，长度相同的单词维持字典序
    stable_sort(words.begin(), words.end(),
                [](const string &a, const string &b)
                { return a.size() < b.size(); });
    // 获取一个迭代器，指向第一个满足size()>= sz的元素
    auto wc = find_if(words.begin(), words.end(),
                      [sz](const string &a)
                      { return a.size() >= sz; });
    // 计算满足size >= sz的元素的数目
    auto count = words.end() - wc;
    cout << count << make_plural(count, "word", "s")
        << " of length " << sz << " or longer" << endl;
    // 打印长度大于等于给定值的单词，每个单词后面接一个空格
    for_each(wc, words.end(),
             [](const string &s) { cout << s << " "; });
    cout << endl;
}
```

### lambda 捕获和返回

```c++
// 值捕获
void fcn1()
{
    size_t v1 = 42;		// 局部变量
    // 将v1拷贝到名为f的可调用对象
    auto f = [v1] { return v1; };
    v1 = 0;
    auto j = f();	// j为42；f保存了我们创建它时v1的拷贝
}

// 引用捕获
// 采用引用方式捕获一个变量，就必须确保被引用的对象在 lambda 执行的时候是存在的。
void fcn2()
{
    size_t v1 = 42;	// 局部变量
    // 对象f2包含v1的引用
    auto f2 = [&vl] { return v1; };
    v1 = 0;
    auto j = f2();	// j为0; f2保存v1的引用，而非拷贝
}

void biggies(vector<string> &words,
             vector<string>::size_type sz,
             ostream &os = cout, char c = '')
{
    // 与之前例子一样的重排 words 的代码
    // 打印 count的语句改为打印到os
    for_each(words.begin(), words.end(), 
             [&os, c] (const string &s) { os << s << c; });
}

//隐式捕获
// &告诉编译器采用捕获引用方式，=则表示采用值捕获方式
// sz为隐式捕获，值捕获方式
wc = find_if(words.begin(), words.end(), 
             [=](const string &s)
             { return s.size() >= sz; });

void biggies(vector<string> &words, 
             vector<string>::size_type sz,
             ostream &os = cout, char c = ' ')
{
    // 其他处理与前例一样
    // os隐式捕获，引用捕获方式;c显式捕获，值捕获方式
    for_each(words.begin(), words.end(), 
             [&, c](const string &s){ os << s << c; });
    // os显式捕获，引用捕获方式;c隐式捕获，值捕获方式
    for_each(words.begin(), words.end(),
             [=, &os](const string &s) { os << s << c; });
}
```

| lambda捕获列表       | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| []                   | 空捕获列表。lambda不能使用所在函数中的变量。一个lambda只有捕获变量后才能使用它们 |
| [names]              | names是一个逗号分隔的名字列表，这些名字都是lambda所在函数的局部变量。默认情况下，捕获列表中的变量都被拷贝。名字前如果使用了&，则采用引用捕获方式 |
| [&]                  | 隐式捕获列表，采用引用捕获方式。lambda体中所使用的来自所在函数的实体都采用引用方式使用 |
| [=]                  | 隐式捕获列表，采用值捕获方式。lambda体将拷贝所使用的来自所在函数的实体的值 |
| [&, identifier_list] | identifier_list是一个逗号分隔的列表，包含0个或多个来自所在函数的变量。这些变量采用值捕获方式，而任何隐式捕获的变量都采用引用方式捕获。identifier_list中的名字前面不能使用& |
| [=, identifier_list] | identifier_list中的变量都采用引用方式捕获，而任何隐式捕获的变量都采用值方式捕获。identifier_list中的名字不能包括this，且这些名字之前必须使用& |

```c++
//可变lambda
// 如果希望能改变个被捕获的变量的值，就必须在参数列表首加上关键字 mutable
void fcn3()
{
    size_t v1 = 42;	//	局部变量
    // f可以改变它所捕获的变量的值
    auto f = [v1] () mutable { return ++v1; }
    v1 = 0;
    autoj = f();//j为43
}

void fcn4()
{
    size_t v1 = 42;		// 局部变量
    // v1是一个非const变量的引用
    // 可以通过f2中的引用来改变它
    auto f2 = [&v1]{ return ++v1; };
    v1 = 0;
    auto j = f2();		// j为1
}

//指定lambda返回类型
// 无须指定返回类型，因为可以根据条件运算符的类型推断出来
transform(vi.begin(), vi.end(), vi.begin(), 
          [](int i) { return i < 0 ? -i : i; });
// 错误:不能推断lambda的返回类型, 编译器推断这个版本的lambda返回类型为void，但它返回了一个int值
transform(vi.begin(), vi.end(), vi.begin(), 
          [](int i){ if (i < 0) return -i; else return i; });
// 需要为一个lambda定义返回类型时，必须使用尾置返回类型
transform(vi.begin(), vi.end(), vi.begin(), 
          [](int i) -> int
          { if(i < 0) return -i; else return i; });
```

### 参数绑定

```c++
bool check_size(const string &s, string::size_type sz)
{
    return s.size() >= sz;
}
// 使用标准库bind可以将check_size传入check_size中

//标准库bind函数
auto newCallable = bind(callable, arg_list);
// newCallable 本身是一个可调用对象，arg_list是一个号分隔的参数列表，对应给定的callable 的参数
// 当我们调用newCallable时，newCallable会调用callable，并传递给它arg_list中的参数
// arg_list中的参数可能包含形如_n的名字，其中n是一个整数，这些参数是“占位符”

//绑定check_size的sz参数
// check6是一个可调用对象，接受一个string类型的参数
// 并用此string和值6来调用check_size
auto check6 = bind(check_size, _1, 6);
string s = "hello";
bool b1 = check6(s);		// check6(s)会调用check_size(s, 6)

auto wc = find_if(words.begin(), words.end(),
                  [sz](const string &a) { });
// To
auto wc = find_if(words.begin(), words.end(), 
                  bind(check_size, _1, sz));


//使用placeholders名字
// _1对应的using 声明为:
using std::placeholders::_1;

using namespace std::placeholders;

//bind参数
// g是一个有两个参数的可调用对象
auto g = bind(f, a, b, _2, c, _1);
g(_1, _2);
// To
f(a, b, _2, c, _1);
// 用bind重排参数顺序
// 按单词长度由短至长排序
sort(words.begin(), words.end(), isShorter);
// 按单词长度由长至短排序
sort(words.begin(), words.end(), bind(isShorter, _2, _1));

//绑定引用参数
// os是一个局部变量，引用一个输出流
// c是一个局部变量，类型为char
for_each(words.begin(), words.end(), 
         [&os, c](const string &s) { os << s << c; } );
// lambda To
ostream &print(ostream &os, const string &s, char c)
{
    return os << s << c;
}
// 不能直接用bind来代替os的捕获
// 错误:不能拷贝oS
for_each(words.begin(), words.end(), bind(print, os, 1, ' '));
// To Right，使用标准库ref函数
for_each(words.begin(), words.end(),
         bind(print, ref(os), _1, ' '));
```



## 再探迭代器

| 迭代器分类 | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| 插入迭代器 | 这些选代器被绑定到一个容器上，可用来向容器插入元素           |
| 流迭代器   | 这些迭代器被绑定到输入或输出流上，可用来遍历所关联的IO流     |
| 反向选代器 | 这些迭代器向后而不是向前移动。除了forward_list之外的标准库容器都有反向迭代器 |
| 移动迭代器 | 这些专用的迭代器不是拷贝其中的元素，而是移动它们             |

### 插入迭代器

它接受一个容器，生成一个迭代器，能实现向给定容器添加元素

| 插入迭代器操作  |                                                              |
| --------------- | ------------------------------------------------------------ |
| it = t          | 在it指定的当前位置插入值t<br />假定c是it绑定的容器，依赖于插入迭代器的不同种类，此赋值会分别调用 c.push_back(t)、c.push_front(t)或c.insert(t, p)，其中p为传递给inserter的迭代器位置 |
| *it, ++it, it++ | 这些操作虽然存在，但不会对it做任何事情。每个操作都返回it     |

| 插入器类型     |                                                              |
| -------------- | ------------------------------------------------------------ |
| back_inserter  | 创建一个使用push_back的选代器                                |
| front_inserter | 创建一个使用push_front的迭代器                               |
| inserter       | 创建一个使用 insert 的迭代器。<br />此函数接受第二个参数，这个参数必须是一个指向给定容器的迭代器。<br />元素将被插入到给定迭代器所表示的元素之前。 |

调用 inserter(c, iter)，得到一个迭代器
使用它时，会将元素插入到 iter 原来所指向的元素之前的位置

```c++
*it = val;
// Equals
it = c.insert(it, val);	// it指向新加入的元素
++it;			// 递增it使它指向原来的元素

list<int> lst = {1, 2, 3, 4};
list<int> lst2, lst3;	//空list
//拷贝完成之后，lst2包含 4 3 2 1
copy(lst.cbegin(), lst.cend(), front_inserter(lst2));
//拷贝完成之后，lst3包含 1 2 3 4
copy(lst.cbegin(), lst.cend(), inserter(lst3, lst3.begin()));
```



### iostream迭代器

| 分类             |                    |
| ---------------- | ------------------ |
| istream_iterator | 读取输入流         |
| ostream_iterator | 向一个输出流写数据 |

```c++
//istream_iterator操作
// istream_iterator要读取的类型必须定义了输入运算符
istream iterator<int> int_it(cin);		// 从cin读取int
istream iterator<int> int_eof;			// 尾后迭代器
ifstream in("afiler");
istream_iterator<string> str_it(in);	// 从"afile"读取字符串

// 用istream_iterator从标准输入读取数据，存入一个vector的例子

istream_iterator<int> in_iter(cin); 		// 从cin读取int
istream_iterator<int> eof;					// istream尾后迭代器
while (in_iter != eof)						// 当有数据可供读取时
    // 后置递增运算读取流，返回迭代器的旧值
    // 解引用迭代器，获得从流读取的前一个值
    vec.push_back(*in_iter++);
// 后置递增运算会从流中读取下一个值，向前推进，但返回的是迭代器的旧值。迭代器的旧值包含了从流中读取的前一个值，对迭代器进行解引用就能获得此值。

istream_iterator<int> in_iter(cin), eof;		// 从cin读取int
vector<int> vec(in_iter, eof);					// 从选代器范围构造vec
```

| istream_iterator 操作       | 说明                                                         |
| --------------------------- | ------------------------------------------------------------ |
| istream_iterator<T> in(is); | in从输入流is读取类型为T的值                                  |
| istream_iterator<T> end;    | 读取类型为T的值的istream_iterator迭代器表示尾后位置          |
| in1 == in2<br />in1 != in2  | in1和in2必须读取相同类型。如果它们都是尾后迭代器，或绑定到相同的输入，则两者相等 |
| *in                         | 返回从流中读取的值                                           |
| in->mem                     | 与(*in).mem的含义相同                                        |
| ++in, in++                  | 使用元素类型所定义的>>运算符从输入流中读取下一个值。与以往一样,前置版本返回一个指向递增后迭代器的引用，后置版本返回旧值 |

```c++
istream_iterator<int> in(cin), eof;
cout << accumulate(in, eof, 0) << endl;
// Input: 
// 23 109 45 89 6 34 12 90 34 23 56 23 8 89 23
// Output:
// 664
```

| ostream_iterator 操作           |                                                              |
| ------------------------------- | ------------------------------------------------------------ |
| ostream_iterator<T> out(os);    | out将类型为T的值写到输出流os中                               |
| ostream_iterator<T> out(os, d); | out将类型为T的值写到输出流os中，每个值后面都输出一个d。d指向一个空字符结尾的字符数组 |
| out = val                       | 用<<运算符将val写入到out所绑定的ostream中。val的类型必须与out可写的类型兼容 |
| *out, ++out, out++              | 这些运算符是存在的，但不对out 做任何事情。每个运算符都返回out |

```c++
ostream_iterator<int> out_iter(cout, " ");

for (auto e : vec)
    *out_iter++ =e;	// 赋值语句实际上将元素写到cout
cout << endl;
// Or
for (auto e : vec)
    out_iter = e;	// 赋值语句将元素写到 cout
cout << endl;
// Or
copy(vec.begin(), vec.end(), out_iter);
cout << endl;

//使用流迭代器处理类类型
istream_iterator<Sales_item> item_iter(cin), eof;
ostream_iterator<Sales_item> out_iter(cout, "\n");
// 将第一笔交易记录存在sum 中，并读取下一条记录
Sales_item sum = *itemiter++;
while (itemiter != eof) {
    // 如果当前交易记录(存在item_iter中)有着相同的ISBN号
    if (item_iter->isbn() == sum.isbn())
        sum += *item_iter++;		// 将其加到 sum 上并读取下一条记录
    else {
        out_iter = sum;				// 输出sum当前值
        sum = *item_iter++;			// 读取下一条记录
    }
}
out_iter = sum;						// 记得打印最后一组记录的和
```



### 反向迭代器

除了forward_list之外，其他容器都支持反向选代器



## 泛型算法结构

| 迭代器类别     |                                      |
| -------------- | ------------------------------------ |
| 输入迭代器     | 只读，不写;单遍扫描，只能递增        |
| 输出迭代器     | 只写，不读:单遍扫描，只能递增        |
| 前向迭代器     | 可读写;多遍扫描，只能递增            |
| 双向迭代器     | 可读写;多遍扫描，可递增递减          |
| 随机访问迭代器 | 可读写，多遍扫描，支持全部迭代器运算 |

### 5类迭代器

输入迭代器(input iterator):可以读取序列中的元素。一个输入迭代器必须支持：

- 用于比较两个迭代器的相等和不相等运算符(==、!=)
- 用于推进迭代器的前置和后置递增运算(++)
- 用于读取元素的解引用运算符(\*)：解引用只会出现在赋值运算符的右侧
- 箭头运算符(->)，等价于(*it).member，即，解引用迭代器，并提取对象的成员



输出迭代器(output iterator):可以看作输入选代器功能上的补集一-只写而不读元素。输出迭代器必须支持：

- 用于推进迭代器的前置和后置递增运算(++)
- 解引用运算符(*)，只出现在赋值运算符的左侧（向一个已经解引用的输出选代器赋值，就是将值写入它所指向的元素）



前向迭代器(forward iterator):可以读写元素。这类迭代器只能在序列中沿一个方向移动
	前向迭代器支持所有输入和输出迭代器的操作，而且可以多次读写同一个元素
	算法replace要求前向迭代器，forward_list 上的选代器是前向迭代器



双向迭代器 (bidirectional iterator):可以正向/反向读写序列中的元素
	除了支持所有前向迭代器的操作之外，双向迭代器还支持前置和后置递减运算符(--)
	算法 reverse要求双向迭代器，除了 forward_list 之外，其他标准库都提供符合双向迭代器要求的迭代。



随机访问迭代器(random-access iterator):提供在常量时间内访问序列中任意元素的能力。此类迭代器支持双向迭代器的所有功能，此外还支持的操作:

- 用于比较两个迭代器相对位置的关系运算符(<、<=、>和>=)
- 迭代器和一个整数值的加减运算(+、+=、-和-=)，计算结果是迭代器在序列中前进(或后退)给定整数个元素后的位置
- 用于两个迭代器上的减法运算符(-)，得到两个迭代器的距离
- 下标运算符(iter[n])，与*(iter[n])等价



### 算法形参模式

```c++
alg(beg, end, other args);
alg(beg, end, dest, other args);
alg(beg, end, beg2, other args);
alg(beg, end, beg2, end2, other args);
```



## 特定容器算法

| list和forward_list成员函数版本的算法      | 这些操作都返回void                                           |
| ----------------------------------------- | ------------------------------------------------------------ |
| lst.merge(lst2)<br/>Ist.merge(lst2, comp) | 将来自lst2的元素合并入lst。lst和lst2都必须是有序的。元素将从Ist2中删除。在合并之后，lst2变为空。第一个版本使用<运算符:第二个版本使用给定的比较操作 |
| lst.remove(val)<br />lst.remove_if(pred)  | 调用erase删除掉与给定值相等(==)或令一元谓词为真的每个元素    |
| lst.reverse()                             | 反转 lst 中元素的顺序                                        |
| lst.sort()<br/>Ist.sort(comp)             | 使用<或给定比较操作排序元素                                  |
| Ist.unique()<br />Ist.unique(pred)        | 调用erase删除同一个值的连续拷贝。第一个版本使用==；第二个版本使用给定的二元谓词 |



lst.splice(args) 或 flst.splice_after(args) 

| list和forward_list的splice成员函数的参数 |                                                              |
| ---------------------------------------- | ------------------------------------------------------------ |
| (p, Ist2)                                | p是一个指向lst中元素的迭代器，或一个指向 flst 首前位置的迭代器。函数将lst2的所有元素移动到1st中p之前的位置或是flst中p之后的位置。将元素从lst2中删除。Ist2的类型必须与lst或flst相同，且不能是同一个链表 |
| (p, Ist2, p2)                            | p2是一个指向lst2中位置的有效的迭代器。将p2指向的元素移动到lst中，或将p2之后的元素移动到flst中。lst2可以是与lst或flst相同的链表 |
| (p, Ist2, b, e)                          | b和e必须表示lst2中的合法范围。将给定范围中的元素从lst2移动到lst或flst。lst2与lst(或flst)可以是相同的链表，但p不能指向给定范围中元素 |



# 关联容器

关联容器支持高效的关键字查找和访问。
两个主要的关联容器(associative-container)类型是map和set。
	map 中的元素是一些关键字-值 (key-value)对:关键字起到索引的作用，值则表示与索引相关联的数据。
	set 中每个元素只包含一个关键字：set 支持高效的关键字查询操作一一检查一个给定关键字是否在 set 中。

| 关联容器类型         |                                  |
| -------------------- | -------------------------------- |
| 按关键字有序保存元素 |                                  |
| map                  | 关联数组;保存关键字-值对         |
| set                  | 关键字即值，即只保存关键字的容器 |
| multimap             | 关键字可重复出现的map            |
| multiset             | 关键字可重复出现的set            |
| 无序集合             |                                  |
| unordered_map        | 用哈希函数组织的map              |
| unordered_set        | 用哈希函数组织的set              |
| unordered_multimap   | 哈希组织的map;关键字可以重复出现 |
| unordered_multiset   | 哈希组织的set;关键字可以重复出现 |



## 使用关联容器

```c++
//使用map
// 统计每个单词在输入中出现的次数
map<string, size_t> word_count; // string到size_t的空map
string word;
while (cin >> word)
    ++word_count[word];			// 提取word的计数器并将其加 1
for (const auto &w : word_count) // 对map中的每个元素
    // 打印结果
    cout << w.first << " occurs " << w.second
    	<< ((w.second > 1) ? "times" : "time") << endl;

//使用set
// 统计输入中每个单词出现的次数
map<string, size_t> word_count;			// string到size_t的空map
set<string> exclude = {"The", "But", "And", "Or", "An", "A", 
                       "the", "but", "and", "or", "an", "a"};
string word;
while (cin >> word)
    // 只统计不在exclude中的单词
    if (exclude.find(word) == exclude.end())
        ++word_count[word];			// 获取并递增word的计数器

```



## 关联容器概述

### 定义关联容器

```c++
map<string, size_t> word_count;			// 空容器
// 列表初始化
set<string> exclude = {"The", "But", "And", "Or", "An", "A", 
                       "the", "but", "and", "or", "an", "a"};
// 三个元素：authors将姓映射为名
map<string, string> authors = {
    {"Joyce", "James"},
    {"Austen", "Jane"},
    {"Dickens", "Charles"}
};

//初始化multimap或multiset
// 定义一个有20个元素的 vector，保存0到9每个整数的两个拷贝
vector<int> ivec;
for (vector<int>::size_type i = 0; i != 10; ++i){
    ivec.push_back(i);
    ivec.push_back(i);		//每个数重复保存一次
}
// iset包含来自ivec的不重复的元素;miset包含所有 20个元素
set<int> iset(ivec.cbegin(), ivec.cend());
multiset<int> miset(ivec.cbegin(), ivec.cend());
cout << ivec.size() << endl;		// 打印出20
cout << iset.size() << endl;		// 打印出10
cout << miset.size() << endl;		// 打印出20
```

### 关键字类型的要求

有序容器的关键字类型：**严格弱序**，可以看作小于等于：

- 两个关键字不能同时”小于等于"对方;如果 k1“小于等于”k2，那么k2绝不能“小于等于”k1
- 如果k1“小于等于”k2，且k2“小于等于”k3，那么k1必须“小于等于”k3
- 如果存在两个关键字，任何一个都不“小于等于”另一个，那么我们称这两个关键字是“等价”的。如果k1“等价于”k2，且k2“等价于”k3，那么k1 必须“等价于”k3。

```c++
// 使用关键字类型的比较函数
bool compareIsbn(const Sales_data &lhs, const Sales_data &rhs)
{
    return lhs.isbn() < rhs.isbn();
}

// bookstore中多条记录可以有相同的ISBN
// bookstore中的元素以ISBN的顺序进行排列
multiset<Sales_data, decltype(compareIsbn)*> bookstore(compareIsbn);
```

### pair类型

一个pair保存两个数据成员。类似容器，pair 是一个用来生成特定类型的模板。当创建一个 pair 时，我们必须提供两个类型名，pair 的数据成员将具有对应的类型两个类型不要求一样:

```c++
pair<string, string> anon;				// 保存两个string
pair<string, size_t> word_count;		// 保存一个string和一个size_t
pair<string, vector<int>> line;			// 保存string和vector<int>

pair<string, string> author{"James", "Joyce"};
// 打印结果
cout << w.first << " occurs " << w.second
    << ((w.second) > 1) ? "times" : "time" << endl;
```

| pair上的操作               |                                                              |
| -------------------------- | ------------------------------------------------------------ |
| pair<T1, T2> p;            | p是一个pair，两个类型分别为T1和T2的成员都进行了值初始化      |
| pair<T1, T2> p(v1, v2)     | p是一个成员类型为T1和T2的pair；first和second成员分别用v1和v2进行初始化 |
| pair<T1, T2> p = {v1, v2}; | 等价于p(v1, v2)                                              |
| make_pair(v1, v2)          | 返回一个用v1和v2初始化的pair。pair的类型从v1和v2的类型推断出来 |
| p.first                    | 返回p的名为first的(公有)数据成员                             |
| p.second                   | 返回p的名为second的(公有)数据成员                            |
| p1 relop p2                | 关系运算符(<、>、<=、>=)按字典序定义:例如，当p1.first<p2.first或!(p2.first <p1.first)&& p1.second < p2.second成立时，p1<p2为 true。关系运算利用元素的<运算符来实现 |
| p1 == p2<br />p1 != p2     | 当first和second成员分别相等时，两个pair相等。相等性判断利用元素的==运算符实现 |

```c++
//创建pair对象的函数
pair<string, int> process(vector<string> &v)
{
    //处理v
    if (!v.empty())
        return {v.back(), v.back().size()};  // 列表初始化
    else
        return pair<string, int>();// 隐式构造返回值
}
```



## 关联容器操作

| 关联容器额外的类型别名 |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| key_type               | 此容器类型的关键字类型                                       |
| mapped_type            | 每个关键字关联的类型;只适用于map                             |
| value_type             | 对于set，与key_type相同<br />对于map，为pair<const key_type, mapped_type> |

```c++
set<string>::value_type v1;			// v1是一个string
set<string>::key_type v2;			// v2是一个string
map<string, int>::value_type v3;	// v3是一个pair<const string, int>
map<string, int>::key_type v4;		// v4是一个string
map<string, int>::mapped_type v5;	// v5是一个int
//只有map类型(unordered_map、unordered_multimap、multimap和map)才定义了mapped_type
```



### 关联容器迭代器

```c++
// 获得指向word_count中一个元素的选代器
auto map_it = word_count.begin();
// *map_it是指向一个pair<const string, size_t>对象的引用
cout << map_it->first;				// 打印此元素的关键字
cout << " " << map_it->second;		// 打印此元素的值
map_it->first = "new key";			// 错误:关键字是 const的
++map_it->second;					// 正确:我们可以通过迭代器改变元素
```

```c++
//set的迭代器是const的
set<int> iset = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
set<int>::iterator set_it = iset.begin();
if (set_it != iset.end()) {
    *set_it = 42;				// 错误:set 中的关键字是只读的
    cout << *set_it << endl;  	// 正确:可以读关键字
} 

//遍历关联容器
// 获得一个指向首元素的迭代器
auto map_it = word_count.cbegin();
// 比较当前迭代器和尾后迭代器
while (map_it != word_count.cend()) {
    // 解引用迭代器，打印关键字-值对
    cout << map_it->first << " occurs "
        << map_it->second << "times" << endl;
    ++map_it;	// 递增迭代器，移动到下一个元素
}
```

### 添加元素

```c++
vector<int> ivec = {2, 4, 6, 8, 2, 4, 6, 8};			// ivec有8个元素
set<int> set2;											// 空集合
set2.insert(ivec.cbegin(), ivec.cend());				// set2有4个元素
set2.insert({1, 3, 5, 7, 1, 3, 5, 7});					// set2现在有8个元素

//向map中添加元素
// 向word_count插入word的4种方法
word_count.insert({word, 1});
word_count.insert(make_pair(word, 1));
word_count.insert(pair<string, size_t>(word, 1));
word_count.insert(map<string, size_t>::value_type(word, 1));
```

| 关联容器insert操作                     |                                                              |
| -------------------------------------- | ------------------------------------------------------------ |
| c.insert(v)<br />c.emplace(args)       | v是value_type类型的对象；args用来构造一个元素<br />对于map和set，只有当元素的关键字不在c中时才插入(或构造)元素。函数返回一个 pair，包含一个迭代器，指向具有指定关键字的元素，以及一个指示插入是否成功的 bool值。<br />对于multimap和multiset，总会插入(或构造)给定元素，并返回一个指向新元素的迭代器 |
| c.insert(b，e)<br />c.insert(il)       | b和e是迭代器，表示一个c::value_type类型值的范围;il是这种值的花括号列表。函数返回void<br />对于map和set，只插入关键字不在c中的元素。对于multimap和multiset，则会插入范围中的每个元素 |
| c.insert(p，v)<br />c.emplace(p，args) | 类似insert(v)(或emplace(args))，但将选代器p作为一个提示，指出从哪里开始搜索新元素应该存储的位置。返回一个迭代器指向具有给定关键字的元素 |

```c++
//检查insert的返回值
//统计每个单词在输入中出现次数的一种更烦琐的方法
map<string, size_t> word_count;		// 从string到size_t的空map
string word;
while (cin >> word){
    // 插入一个元素，关键字等于word，值为1;
    // 若word已在word_count中，insert什么也不做
    auto ret = word_count.insert({word, 1});
    if (!ret.second)			// word已在word_count中
        ++ret.first->second;	// 递增计数器
}
```

### 删除元素

```c++
// 删除一个关键字，返回删除的元素数量
if (word_count.erase(removal_word))
    cout << "ok: " << removal_word << " removed\n";
else cout << "oops: " << removal_word << " not found!\n";

// 对允许重复关键字的容器，删除元素的数量可能大于1:
auto cnt = authors.erase("Barth, John");

```

| 从关联容器删除元素 |                                                              |
| ------------------ | ------------------------------------------------------------ |
| c.erase(k)         | 从c中删除每个关键字为k的元素。返回一个size_type值，指出删除的元素的数量 |
| c.erase(p)         | 从c中删除迭代器p指定的元素。p必须指向c中一个真实元素不能等于c.end()。返回一个指向p之后元素的选代器，若p指向c中的尾元素，则返回c.end() |
| c.erase(b, e)      | 删除迭代器对b和e所表示的范围中的元素。返回e                  |



### map的下标操作

| map和unordered_map的下标操作 |                                                              |
| ---------------------------- | ------------------------------------------------------------ |
| c[k]                         | 返回关键字为k的元素;如果k不在c中，添加一个关键字为k的元素，对其进行值初始化 |
| c.at(k)                      | 访问关键字为k的元素，带参数检查：若k不在中，抛出一个out_of_range异常 |

```c++
//使用下标操作的返回值
cout << word_count["Anna"];		// 用Anna作为下标提取元素;会打印出1
++word_count["Anna"];			// 提取元素，将其增 1
cout << word_count["Anna"];		// 提取元素并打印它;会打印出2
```



### 访问元素

```c++
set<int> iset = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
iset.find(1);		// 返回一个迭代器，指向key == 1的元素
iset.find(11);		// 返回一个迭代器，其值等于iset.end()
iset.count(1);		// 返回1
iset.count(11); 	// 返回0
```

lower_bound和upper_bound 不适用于无序容器
下标和at操作只适用于非const的map和unordered_map

| 在一个关联容器中查找元素的操作 |                                                              |
| ------------------------------ | ------------------------------------------------------------ |
| c.find(k)                      | 返回一个迭代器，指向第一个关键字为k的元素，若k不在容器中，则返回尾后迭代器 |
| c.count(k)                     | 返回关键字等于k的元素的数量。对于不允许重复关键字的容器，返回值永远是0或1 |
| c.lower_bound(k)               | 返回一个迭代器，指向第一个关键字不小于k的元素                |
| c.upper_bound(k)               | 返回一个迭代器，指向第一个关键字大于k的元素                  |
| c.equal_range(k)               | 返回一个迭代器pair，表示关键字等于k的元素的范围。若k不存在，pair的两个成员均等于c.end() |

```c++
//对map使用find代替下标操作
if (word_count.find("foobar") == word_count.end())
    cout << "foobar is not in the map" << endl;

//在multimap或multiset中查找元素
string searchitem("Alain de Botton");		// 要查找的作者
auto entries = authors.count(search_item);	// 元素的数量
auto iter = authors.find(search_item);		// 此作者的第一本书
// 用一个循环查找此作者的所有著作
while(entries)
{
    cout << iter->second << endl;			// 打印每个题目
    ++iter;									// 前进到下一本书
    --entries;								// 记录已经打印了多少本书
}
// Or
for (auto beg = authors.lower_bound(search_item),
     end = authors.upper_bound(search_item);
     beg != end; ++beg)
    cout << beg->second << endl;		// 打印每个题目

//equal_range函数
// authors和search item的定义，与前面的程序一样
// pos保存迭代器对，表示与关键字匹配的元素范围
for (auto pos = authors.equal_range(search_item);
     pos.first != pos.second; ++pos.first)
     cout << pos.first->second << endl;	// 打印每个题目
```



## 无序容器

新标准定义了4个无序关联容器(unordered associative container)。这些容器不是使用比较运算符来组织元素，而是使用一个哈希函数 (hash function)和关键字类型的 == 运算符。

```c++
//使用无序容器
// 统计出现次数，但单词不会按字典序排列
unordered_map<string, size_t> word_count;
string word;
while(cin >> word)
    ++word_count[word];			// 提取并递增word的计数器
for (const auto &w : word_count) // 对map中的每个元素
    // 打印结果
    cout << w.first << " occurs " << w.second
    	<< ((w.second > 1) ? " times" : " time") << endl;
```

| 无序容器管理操作       |                                                              |
| ---------------------- | ------------------------------------------------------------ |
| 桶接口                 |                                                              |
| c.bucket_count(）      | 正在使用的桶的数目                                           |
| c.max_bucket_count()   | 容器能容纳的最多的桶的数量                                   |
| c.bucket_size(n)       | 第n个桶中有多少个元素                                        |
| c.bucket(k)            | 关键字为k的元素在哪个桶中                                    |
| 桶迭代                 |                                                              |
| local_iterator         | 可以用来访问桶中元素的迭代器类型                             |
| const_local_iterator   | 桶迭代器的const版本                                          |
| c.begin(n), c.end(n)   | 桶n的首元素迭代器和尾后迭代器                                |
| c.cbegin(n), c.cend(n) | 与前两个函数类似，但返回const_local_iterator                 |
| 哈希策略               |                                                              |
| c.load_factor()        | 每个桶的平均元素数量，返回float值                            |
| c.max_load_factor()    | c试图维护的平均桶大小，返回float值。c会在需要时添加新的桶，以使得load_factor <= max_load_factor |
| c.rehash(n)            | 重组存储，使得bucket_count >= n且bucket_count > size / max_load_factor |
| c.reserve(n)           | 重组存储，使得c可以保存n个元素且不必rehash                   |

```c++
//无序容器对关键字类型的要求
// 不能直接定义关键字类型为自定义类类型的无序容器
//  必须提供我们自己的hash模板版本
size_t hasher(const Sales_data &sd)
{
    return hash<string>()(sd.isbn());
}
bool eqOp(const Sales_data &lhs, const Sales_data &rhs)
{
    return lhs.isbn() == rhs.isbn();
}
using SD_multiset = unordered_multiset<Sales_data, 
					decltype(hasher)*, decltype(egOp)* >;
// 参数是桶大小、哈希函数指针和相等性判断运算符指针
SD_multiset bookstore(42, hasher, eqOp);
// 使用FooHash生成哈希值;Foo必须有==运算符
unordered_set<Foo, decltype(FooHash)*> fooSet(10, FooHash);
```



# 动态内存

除了静态内存和栈内存，每个程序还拥有一个内存池。
这部分内存被称作自由空间(free store)或堆(heap)。
程序用堆来存储动态分配(dynamically allocate)的对象一即那些在程序运行时分配的对象。
动态对象的生存期由程序来控制，也就是说，当动态对象不再使用时，我们的代码必须显式地销毁它们。

## 动态内存与智能指针

new：在动态内存中为对象分配空间并返回一个指向该对象的指针，我们可以选择对对象进行初始化
delete：接受一个动态对象的指针，销毁该对象，并释放与之关联的内存

新的标准库提供了两种智能指针(smart pointer)类型来管理动态对象
智能指针的行为类似常规指针，重要的区别是它负责自动释放所指向的对象
	shared_ptr 允许多个指针指向同一个对象
	unique_ptr 则“独占”所指向的对象
标准库还定义了一个名为weak_ptr的伴随类，它是一种弱引用，指向shared_ptr所管理的对象
这三种类型都定义在memory头文件中。

### shared_ptr 类

```c++
shared_ptr<string> p1;		//shared_ptr，可以指向string
shared_ptr<list<int>> p2;	//shared_ptr，可以指向int的list

//如果p1不为空，检查它是否指向一个空string
if (p1 && p1->empty())
    *p1 = "hi";		// 如果p1指向一个空string，解引用p1，将一个新值赋予string
```

| shared_ptr和unique_ptr 都支持的操作    |                                                              |
| -------------------------------------- | ------------------------------------------------------------ |
| shared_ptr<T> sp<br />unique_ptr<T> up | 空智能指针，可以指向类型为T的对象                            |
| p                                      | 将p用作一个条件判断，若p指向一个对象，则为 true              |
| *p                                     | 解引用p，获得它指向的对象                                    |
| p->mem                                 | 等价于(*p).mem                                               |
| p.get()                                | 返回p中保存的指针。要小心使用，若智能指针释放了其对象，返回的指针所指向的对象也就消失了 |
| swap(p, q)<br />p.swap(q)              | 交换p和q中的指针                                             |

| shared_ptr独有的操作  |                                                              |
| --------------------- | ------------------------------------------------------------ |
| make_shared<T> (args) | 返回一个shared_ptr，指向一个动态分配的类型为T的对象。使用args初始化此对象 |
| shared_ptr<T> p(q)    | p是shared_ptr q的拷贝；此操作会递增q中的计数器。q中的指针必须能转换为T* |
| p = q                 | p和q都是shared_ptr，所保存的指针必须能相互转换<br />此操作会递减p的引用计数，递增q的引用计数<br />若p的引用计数变为0则将其管理的原内存释放 |
| p.unique()            | 若p.use_count()为1，返回true;否则返回 false                  |
| p.use_count()         | 返回与p共享对象的智能指针数量:可能很慢，主要用于调试         |

```c++
//make_shared函数
// 指向一个值为42的int的shared_ptr
shared_ptr<int> p3 = make_shared<int>(42);
// p4指向一个值为”9999999999"的string
shared_ptr<string> p4 = make_shared<string>(10, '9');
// p5指向一个值初始化的int，即，值为0
shared_ptr<int> p5 = make_shared<int>();

// p6指向一个动态分配的空vector<string>
auto p6 = make_shared<vector<string>>();
//shared_ptr的拷贝和赋值
auto p = make_shared<int>(42);	// p指向的对象只有p一个引用者
auto q(p);				// p和q指向相同对象，此对象有两个引用者
auto r = make_shared<int>(42);	// r指向的int只有一个引用者
r = q;				// 给r赋值，令它指向另一个地址
					// 递增q指向的对象的引用计数
					// 递减r原来指向的对象的引用计数
					// r 原来指向的对象已没有引用者，会自动释放

//shared_ptr自动销毁所管理的对象
// 析构函数(destructor)完成销毁工作
```



```c++
//定义StrBlob类
class StrBlob{
public:
    typedef std::vector<std::string>::size_type size_type;
    StrBlob();
    // 此构造函数可以接受一个初始化器的花括号列表
    StrBlob(std::initializer_list<std::string> il);
    size_type size() const { return data->size(); }
    bool empty() const { return data->empty(); }
    // 添加和删除元素
    void push_back(const std::string &t) { data->push_back(t); }
    void pop_back();
    // 元素访问
	std::string& front();
    std::string& back();
private:
    std::shared_ptr<std::vector<std::string>> data;
    // 如果data[i]不合法，抛出一个异常
    void check(size_type i, const std::string &msg) const;
};

//StrBlob构造函数
StrBlob::StrBlob() : data(make_shared<vector<string>>()) { }
StrBlob::StrBlob(initializer_list<string> il) : 
	data(make_shared<vector<string>>(il)) { }

void StrBlob::check(size type i, const string &msg) const 
{
    if (i >= data->size())
        throw out_of_range(msg);
}

string& StrBlob::front()
{
    // 如果 vector为空，check会抛出一个异常
    check(0, "front on empty StrBlob");
    return data->front();
}
string& StrBlob::back()
{
    check(0，"back on empty StrBlob");
    return data->back();
}
void StrBlob::pop_back()
{
    check(0, "popback on empty StrBlob");
    data->pop_back();
}
```

### 直接管理内存

运算符new分配内存，delete释放new分配的内存

```c++
int *pi = new int;			// pi指向一个动态分配的、未初始化的无名对象
string *ps = new string;	// 初始化为空string

int *pi = new int(1024);	// pi指向的对象的值为1024
string *ps = new string(10, '9');	// *ps为"9999999999"
// vector有10个元素，值依次从0到9
vector<int> *pv = new vector<int>{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};


string *ps1 = new string;			// 默认初始化为空string
string *ps = new string();			// 值初始化为空string
int *pi1 = new int;					// 默认初始化;*pi1的值未定义
int *pi2 = new int();				// 值初始化为0;*pi2为0

auto p1 = new auto(obj);			// p指向一个与obj类型相同的对象
									// 该对象用obj进行初始化
auto p2 = new auto{ a, b, c };		// 错误:括号中只能有单个初始化器

//动态分配的const对象
// 分配并初始化一个const int
const int *pci = new const int(1024);
// 分配并默认初始化一个const的空string
const string *pcs = new const string;

//内存耗尽
// 如果分配失败，new返回一个空指针
int *p1 = new int;	// 如果分配失败，new抛出std::bad_alloc

// 我们称这种形式的new为定位new(placement new)
// 定位 new 表达式允许我们向 new 传递额外的参数
// 如果将nothrow传递给new，我们的意图是告诉它不能抛出异常。如果这种形式的 new 不能分配所需内存，它会返回一个空指针。
// bad_alloc和nothrow都定义在头文件new中。
int *p2 = new(nothrow) int;	// 如果分配失败，new返回一个空指针

//释放动态内存
delete p;	// p必须指向一个动态分配的对象或是一个空指针

//指针值和delete
int i, *pi1 = &i, *pi2 = nullptr;
double *pd = new double(33), *pd2 = pd;
delete i;		// 错误:i不是一个指针
delete pi1;		// 未定义:pi1指向一个局部变量
delete pd;		// 正确
delete pd2;		// 未定义:pd2 指向的内存已经被释放了
delete pi2;		// 正确:释放一个空指针总是没有错误的

// 虽然一个const对象的值不能被改变，但它本身是可以被销毁的
const int *pci = new const int(1024);
delete pci;	// 正确:释放一个const对象

//动态对象的生存期直到被释放时为止
// factory返回一个指针，指向一个动态分配的对象
Foo* factory(T arg)
{
    // 视情况处理arg
    return new Foo(arg);	// 调用者负责释放此内存
}
void use_factory(T arg)
{
    Foo *p = factory(arg);
    // 使用p但不delete它
    
}//p离开了它的作用域，但它所指向的内存没有被释放!

//delete之后重置指针值, 只是提供了有限的保护
int *p(new int(42));		// p指向动态内存
auto q = p;					// p和q指向相同的内存
delete p;					// p和q均变为无效
p = nullptr;				// 指出p不再绑定到任何对象
```

### shared_ptr和new结合使用

```c++
shared_ptr<double> p1;				// shared_ptr可以指向一个double
shared_ptr<int> p2(new int(42));	// p2指向一个值为42的int

// 接受指针参数的智能指针构造函数是explicit的
shared_ptr<int> p1 = new int(1024);	// 错误:必须使用直接初始化形式
shared_ptr<int> p2(new int(1024));	// 正确:使用了直接初始化形式

shared_ptr<int> clone(int p) {
    return new int(p);	// 错误:隐式转换为shared_ptr<int>
}
shared_ptr<int> clone(int p) {
    return shared_ptr<int>(new int(p)); // 正确:显式地用int*创建shared_ptr<int>
}
```

| 定义和改变shared_ptr的其他方法               |                                                              |
| -------------------------------------------- | ------------------------------------------------------------ |
| shared_ptr<T> p(q)                           | p管理内置指针q所指向的对象;q必须指向new分配的内存，且能够转换为T*类型 |
| shared_ptr<T> p(u)                           | p从unique_ptr u那里接管了对象的所有权；将u置为空             |
| shared_ptr<T> p(q, d)                        | p接管了内置指针q所指向的对象的所有权，q必须能转换为T*类型。p将使用可调用对象d来代替delete |
| shared_ptr<T> p(p2, d)                       | p是shared_ptr p2的拷贝，唯一的区别是p将用可调用对象d来代替delete |
| p.reset()<br />p.reset(g)<br />p.reset(g, d) | 若p是唯一指向其对象的 shared_ptr，reset 会释放此对象。若传递了可选的参数内置指针q，会令 p指向q，否则会将p置为空。若还传递了参数d，将会调用d而不是 delete来释放q |

```c++
//不要混合使用普通指针和智能指针
int *x(new int(1024));		// 危险:是一个普通指针，不是一个智能指针
process(x);					// 错误:不能将int*转换为一个shared ptr<int>
process(shared_ptr<int>(x));// 合法的，但内存会被释放!
int j = *x;					// 未定义的:是一个空悬指针!

//也不要使用get初始化另一个智能指针或为智能指针赋值
shared_ptr<int> p(new int(42));	//引用计数为1
int *q = p.get();		// 正确:但使用q时要注意，不要让它管理的指针被释放
{
    // 新程序块
    // 未定义:两个独立的shared_ptr指向相同的内存
    shared_ptr<int>(q);
} // 程序块结束，q 被销毁，它指向的内存被释放
int foo = *p;	// 未定义:p指向的内存已经被释放了


shared_ptr p = new int(1024);	// 错误:不能将一个指针赋予
p.reset(new int(1024)); 		// 正确:p指向一个新对象

if(!p.unique())
    p.reset(new string(*p));	// 我们不是唯一用户;分配新的拷贝
*p += newVal;					// 现在我们知道自己是唯一的用户，可以改变对象的值
```



### 智能指针和异常

```c++
void f()
{
    shared_ptr<int> sp(new int(42));	// 分配一个新对象
    // 这段代码抛出一个异常，且在f中未被捕获
}	// 在函数结束时shared_ptr自动释放内存


void f()
{
    int *ip = new int(42);		// 动态分配一个新对象
    // 这段代码抛出一个异常，且在 f 中未被捕获
    delete ip;	// 在退出之前释放内存
}		// 如果在 new和delete 之间发生异常，且异常未在f中被捕获，则内存就永远不会被释放了。

//使用我们自己的释放操作
void end_connection(connection *p) { disconnect(*p); }
void f(destination &d /*其他参数*/)
{
    connection c = connect(&d);
    shared_ptr<connection> p(&c, end_connection);
    // 使用连接
    // 当f退出时(即使是由于异常而退出)，connection会被正确关闭
}

```



### unique_ptr类

unique_ptr“拥有”它所指向的对象
与shared_ptr不同，某个时刻只能有一个unique_ptr指向一个给定对象
当unique_ptr被销毁时，它所指向的对象也被销毁

```c++
unique_ptr<double> p1;			// 可以指向一个double的unique_ptr
unique_ptr<int> p2(new int(42));// p2指向一个值为42的int

// 由于一个unique_ptr拥有它指向的对象，因此unique_ptr不支持普通的拷贝或赋值操作:
unique_ptr<string> p1(new string("Stegosaurus"));
unique_ptr<string> p2(p1);		// 错误:unique_ptr不支持拷贝
unique_ptr<string> p3;
p3 = p2;			// 错误:unique_ptr不支持赋值
```

| unique_ptr操作                            |                                                              |
| ----------------------------------------- | ------------------------------------------------------------ |
| unique_ptr<T> u1<br />unique_ptr<T, D> u2 | 空unique_ptr,可以指向类型为T的对象。u1会使用delete来释放它的指针:u2会使用一个类型为D的可调用对象来释放它的指针 |
| unique_ptr<T, D> u(d)                     | 空unique_ptr，指向类型为T的对象，用类型为D的对象d代替delete  |
| u = nullptr                               | 释放u指向的对象，将u置为空                                   |
| u.release()                               | u放弃对指针的控制权，返回指针，并将u置为空                   |
| u.reset()                                 | 释放u指向的对象                                              |
| u.reset(q)<br />u.reset(nullptr)          | 如果提供了内置指针q，令u指向这个对象;否则将u置为空           |

```c++
// 将所有权从p1(指向string Stegosaurus)转移给p2
unique_ptr<string> p2(p1.release());	// release将p1置为空
unique_ptr<string> p3(new string("Trex"));
// 将所有权从p3转移给p2
p2.reset(p3.release());	// reset释放了p2原来指向的内存

p2.release();		// 错误:p2不会释放内存，而且我们丢失了指针
auto p = p2.release(); // 正确，但我们必须记得delete(p)

//传递unique_ptr参数和返回unique_ptr
// 不能拷贝 unique ptr 的规则有一个例外:
//  我们可以拷贝或赋值一个将要被销毁的unique ptr
unique_ptr<int> clone(int p) {
    // 正确:从int*创建一个unique_ptr<int>
    return unique_ptr<int>(new int(p));
}
//  还可以返回一个局部对象的拷贝
unique_ptr<int> clone(int p) {
    unique_ptr<int> ret(new int (p));
    // ... 
    return ret;
}
//向unique_ptr传递删除器
// p指向一个类型为 objT 的对象，并使用一个类型为 delT 的对象释放obiT 对象
// 它会调用一个名为fcn的delT类型对象
unique_ptr<objT, delT> p (new objT, fcn);


void f(destination &d /*其他需要的参数 */)
{
    connection c = connect(&d);	// 打开连接
    // 当p被销毁时，连接将会关闭
    unique_ptr<connection, decltype(end_connection)*>
        p(&c, end_connection);
    // 使用连接
    // 当f退出时(即使是由于异常而退出)，connection会被正确关闭
}
```



### weak_ptr

weak_ptr(见表12.5是一种不控制所指向对象生存期的智能指针，它指向由一个shared_ptr管理的对象。将一个 weak_ptr 绑定到一个 shared_ptr不会改变shared_ptr的引用计数。

| weak_ptr          |                                                              |
| ----------------- | ------------------------------------------------------------ |
| weak_ptr<T> w     | 空weak_ptr可以指向类型为T的对象                              |
| weak_ptr<T> w(sp) | 与shared_ptr sp指向相同对象的 weak_ptr。T必须能转换为sp 指向的类型 |
| w = p             | p可以是一个shared_ptr 或一个 weak_ptr。赋值后w与p共享对象    |
| w.reset()         | 将w置为空                                                    |
| w.use_count()     | 与w共享对象的 shared_ptr的数量                               |
| w.expired()       | 若w.use_count()为0，返回true，否则返回 false                 |
| w.lock()          | 如果expired为true，返回一个空 shared_ptr;否则返回一个指向w的对象的shared_ptr |

```c++
auto p = make_shared<int>(42);
weak_ptr<int> wp(p);	// wp 弱共享p; p的引用计数未改变

if (shared_ptr<int> np = wp.lock()) { // 如果np不为空则条件成立
	// 在if中，np与p共享对象
}
```



```c++
//核查指针类
// 对于访问一个不存在元素的尝试，strBlobPtr 抛出一个异常
class StrBlobPtr {
public:
    StrBlobPtr(): curr(0) { }
    StrBlobPtr(StrBlob &a, size_t sz = 0):
    	wptr(a.data), curr(sz) { }
    std::string& deref() const;
    StrBlobPtr& incr(); // 前缀递增
private:
    // 若检查成功，check 返回一个指向 vector的 shared_ptr
    std::shared_ptr<std::vector<std::string>>
        check(std::size_t, const std::string&) const;
    // 保存一个weak_ptr，意味着底层 vector 可能会被销毁
    std::weak_ptr<std::vector<std::string>> wptr;
    std::size_t curr;// 在数组中的当前位置
};

std::shared_ptr<std::vector<std::string>>
StrBlobPtr::check(std::size_t i, const std::string &msg) const
{
    auto ret = wptr.lock();	// vector还存在吗?
    if (!ret)
        throw std::runtime_error("unbound StrBlobPtr");
    if (i >= ret->size())
        throw std::out_of_range(msg);
    return ret;//否则，返回指向 vector的 shared_ptr
}

std::string& StrBlobPtr::deref() const
{
    auto p = check(curr, "dereference past end");
    return (*p)[curr]; // (*p)是对象所指向的 vector
}

// 前缀递增:返回递增后的对象的引用
StrBlobPtr& StrBlobPtr::incr()
{
    // 如果curr已经指向容器的尾后位置，就不能递增它
    check(curr, "increment past end of StrBlobPtr");
    ++curr;	// 推进当前位置
    return *this;
}

// 对于StrBlob中的友元声明来说，此前置声明是必要的
class StrBlobPtr;
class StrBlob {
    friend class StrBlobPtr;
    // 其他成员与之前声明相同
    // 返回指向首元素和尾后元素的 StrBlobPtr
    StrBlobPtr begin() { return StrBlobPtr(*this); }
    StrBlobPtr end() 
    {
        auto ret = StrBlobPtr(*this, data->size());
        return ret; 
    }
};
```



## 动态数组

C++语言定义了另一种 new 表达式语法，可以分配并初始化一个对象数组
标准库中包含一个名为allocator 的类，允许我们将分配和初始化分离
	使用 allocator 通常会提供更好的性能和更灵活的内存管理能力

### new和数组

```c++
// 调用get_size确定分配多少个int
int *pia = new int[get_size()];	// pia指向第一个int

typedef int arrT[42];		// arrT表示42个int的数组类型
int *p = new arrT;			// 分配一个42个int的数组;p指向第一个int

//分配一个数组会得到一个元素类型的指针

//初始化动态分配对象的数组
int *pia = new int[10];				// 10个未初始化的int
int *pia2 = new int[10]();			// 10个值初始化为0的int
string *psa = new string[10];		// 10个空string
string *psa2 = new string[10]();	// 10个空string

//C++11
// 10个int 分别用列表中对应的初始化器初始化
int *pia3 = new int[10]{0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
//10个string，前4个用给定的初始化器初始化，剩余的进行值初始化
string *psa3 = new string[10]{ "a", "an", "the", string(3, 'x')};

//动态分配一个空数组是合法的
// 错误:不能定义长度为0的数组
char arr[0];
char *cp = new char[0]; // 正确:但cp不能解引用

//释放动态数组
delete p;			// p必须指向一个动态分配的对象或为空
delete [] pa;		// pa必须指向一个动态分配的数组或为空

//智能指针和动态数组
// up指向一个包含10个未初始化int的数组
unique_ptr<int[]> up(new int[10]);
up.release();	// 自动用delete[]销毁其指针
```

指向数组的 unique_ptr 不支持成员访问运算符(点和箭头运算符)。其他unique_ptr操作不变

| 指向数组的unique_ptr  |                                                            |
| --------------------- | ---------------------------------------------------------- |
| unique_ptr<T[ ]> u    | u可以指向一个动态分配的数组，数组元素类型为 T              |
| unique_ptr<T[ ]> u(p) | u指向内置指针p所指向的动态分配的数组。p 必须能转换为类型T* |
| u[i]                  | 返回u拥有的数组中位置i处的对象<br />u必须指向一个数组      |

```c++
// 为了使用 shared_ptr，必须提供一个删除器
shared_ptr<int> sp(new int[10], [](int *p) { delete[] p; } );
sp.reset(); // 使用我们提供的lambda释放数组，它使用delete[]

// shared_ptr不直接支持动态数组管理这一特性会影响我们如何访问数组中的元素:
// shared_ptr未定义下标运算符，并且不支持指针的算术运算
for (size_t i = 0; i != 10; ++i)
    *(sp.get() + i) = i;	// 使用get获取一个内置指针
```



### allocator 类

当分配一大块内存时，通常计划在这块内存上按需构造对象
在此情况下，我们希望将内存分配和对象构造分离
这意味着我们可以分配大块内存，但只在真正需要时才真正执行对象创建操作(同时付出一定开销)

```c++
string *const p = new string[n];		// 构造n个空string
string s;
string *q = p;							// q指向第一个string
while (cin >> s && q != p + n)
    *q++ = s;							// 赋予*q一个新值
const size_t size = q - p;				// 记住我们读取了多少个string
// 使用数组
delete[] p;		// p指向一个数组;记得用delete[]来释放
```

**allocator 类**
标准库allocator类定义在头文件memory 中，它帮助我们将内存分配和对象构造分离开来
当一个allocator 对象分配内存时，它会根据给定的对象类型来确定恰当的内存大小和对齐位置

```c++
allocator<string> alloc;			// 可以分配string的allocator对象
auto const p = alloc.allocate(n);	// 分配n个未初始化的string
```

| 标准库allocator类及其算法 |                                                              |
| ------------------------- | ------------------------------------------------------------ |
| allocator<T> a            | 定义了一个名为a的allocator 对象，它可以为类型为T的对象分配内存 |
| a.allocate(n)             | 分配一段原始的、未构造的内存，保存n个类型为T的对象           |
| a.deallocate(p, n)        | 释放从T*指针p中地址开始的内存，这块内存保存了n个类型为T的对象;p必须是一个先前由allocate返回的指针且n必须是p创建时所要求的大小。在调用deallocate之前，用户必须对每个在这块内存中创建的对象调用destroy |
| a.construct(p, args)      | p必须是一个类型为T*的指针，指向一块原始内存;arg被传递给类型为T的构造函数，用来在p指向的内存中构造个对象 |
| a.destroy(p)              | p为T*类型的指针,此算法对p指向的对象执行析构函数              |

```c++
//allocator分配未构造的内存
auto q = p;	// q指向第一个未初始化的string
alloc.construct(q++);	// *q为空字符串
alloc.construct(q++, 10, 'c');	// *q为cccccccccc
alloc.construct(q++, "hi");		// *q为hi
cout << *p << endl; // 正确:使用string的输出运算符
cout << *q << endl;	// 灾难：q指向未构造的内存！

while (q != p)
    alloc.destroy(--q);	// 释放构造的 string
//Or
alloc.deallocate(p, n);
```

**拷贝和填充未初始化内存的算法**

| allocator算法                  |                                                              |
| ------------------------------ | ------------------------------------------------------------ |
| uninitialized_copy(b, e, b2)   | 从迭代器b和e指出的输入范围中拷贝元素到迭代器b2指定的未构造的原始内存中。b2指向的内存必须足够大，能容纳输入序列中元素的拷贝 |
| uninitialized_copy_n(b, n, b2) | 从迭代器b指向的元素开始，拷贝n个元素到b2开始的内存中         |
| uninitialized_fill(b, e, t)    | 在迭代器b和e指定的原始内存范围中创建对象，对象的值均为t的拷贝 |
| uninitialized_fill_n(b, n, t)  | 从迭代器b指向的内存地址开始创建n个对象。b必须指向足够大的未构造的原始内存，能够容纳给定数量的对象 |

```c++
// 分配比vi中元素所占用空间大一倍的动态内存
auto p = alloc.allocate(vi.size() * 2);
// 通过拷贝 vi 中的元素来构造从p开始的元素
auto q = uninitialized_copy(vi.begin(), vi.end(), p);
// 将剩余元素初始化为 42
uninitialized_fill_n(q, vi.size(), 42);
```



# 拷贝控制

定义一个类时，我们显式地或隐式地指定在此类型的对象拷贝、移动、赋值和销毁时做什么

- 拷贝构造函数(copy constructor)
- 拷贝赋值运算符(copy-assignment operator)
- 移动构造函数(move constructor)
- 移动赋值运算符(move-assignment operator)
- 析构函数(destructor)

拷贝和移动构造函数定义了当用同类型的另一个对象初始化本对象时做什么
拷贝和移动赋值运算符定义了将一个对象赋予同类型的另一个对象时做什么
析构函数定义了当此类型对象销毁时做什么
我们称这些操作为拷贝控制操作(copy control)

## 拷贝、赋值与销毁

### 拷贝构造函数

如果一个构造函数的**第一个参数**是**自身类类型的引用**，且任何额外参数都有默认值则此构造函数是拷贝构造函数
拷贝构造函数通常不应该是explicit的

```c++
class Foo {
public:
    Foo();				// 默认构造函数
    Foo(const Foo&); 	// 拷贝构造函数
    // ...
}
```

**合成拷贝构造函数**
合成拷贝构造函数用来阻止我们拷贝该类类型的对象
而一般情况，合成的拷贝构造函数会将其参数的成员逐个拷贝到正在创建的对象中

每个成员的类型决定了它如何拷贝:
	对类类型的成员，会使用其拷贝构造函数来拷贝；内置类型的成员则直接拷贝
	合成拷贝构造函数会逐元素地拷贝一个数组类型的成员
		如果数组元素是类类型，则使用元素的拷贝构造函数来进行拷贝

```c++
// Sales_data类的合成拷贝构造函数等价于
class Sales_data {
public:
    // 其他成员和构造函数的定义，如前
    // 与合成的拷贝构造函数等价的拷贝构造函数的声明
    Sales_data(const Sales_data&);
private:
    std::string bookNo;
    int units_sold = 0;
    double revenue = 0.0;
};
// 与Sales_data的合成的拷贝构造函数等价
Sales_data::Sales_data(const Sales_data &orig) : 
	bookNo(orig.bookNo), 			// 使用 string的拷贝构造函数
	units_sold(orig.units_sold), 	// 拷贝orig.units_sold
	revenue(orig.revenue)			// 拷贝orig.revenue
    { }								// 空函数体

//拷贝初始化
// 当我们使用拷贝初始化 (copy initialization)时，
// 要求编译器将右侧运算对象拷贝到正在创建的对象中，如果需要的话还要进行类型转换
string dots(10, '.');					// 直接初始化
string s(dots);							// 直接初始化
string s2 = dots;						// 拷贝初始化
string null_book = "9-999-99999-9";		// 拷贝初始化
string nines = string(100, '9');		// 拷贝初始化
```

拷贝初始化何时发生：

- 用=定义变量时会发生
- 将一个对象作为实参传递给一个非引用类型的形参
- 从一个返回类型为非引用类型的函数返回一个对象
- 用花括号列表初始化一个数组中的元素或一个聚合类中的成员

**为什么拷贝构造函数一定要是引用类型**
如果其参数不是引用类型，则调用永远也不会成功：为了调用拷贝构造函数，我们必须拷贝它的实参，但为了拷贝实参，我们又需要调用拷贝构造函数，如此无限循环。



### 拷贝赋值运算符

```c++
Sales_data trans, accum;
trans = accum;		//使用Sales_data的拷贝赋值运算符
```

```c++
class Foo {
public:
	Foo& operator=(const Foo&); // 赋值运算符
	// ...
};
```

为了与内置类型的赋值保持一致，赋值运算符通常返回**一个指向其左侧运算对象的引用**
标准库通常要求保存在容器中的类型要具有赋值运算符，且其返回值是左侧运算对象的引用

**合成拷贝赋值运算符**

```c++
//等价于Sales_data的合成拷贝赋值运算符
Sales_data& Sales_data::operator=(const Sales_data &rhs)
{
    bookNo = rhs.bookNo;			// 调用string::operator=
    units_sold = rhs.units_sold;	// 使用内置的int赋值
    revenue = rhs.revenue;			// 使用内置的double赋值
    return *this;					// 返回一个此对象的引用
}
```



### 析构函数

析构函数释放对象使用的资源，并销毁对象的非static数据成员
由于析构函数不接受参数，因此它不能被重载。对一个给定类，只会有唯一一个析构函数
在一个析构函数中，首先执行函数体，然后销毁成员
成员按初始化顺序的逆序销毁

```c++
class Foo{
public:
    ~Foo();	// 析构函数
    // ...
};
```

```c++
{
    // 新作用域
    // p和p2指向动态分配的对象
    Sales_data *p = new Sales_data;			// p是一个内置指针
    auto p2 = make_shared<Sales_data>();	// p2是一个shared_ptr
    Sales_data item(*p);					// 拷贝构造函数将*p拷贝到item 中
    vector<Sales_data> vec;					// 局部对象
    vec.push_back(*p2);						// 拷贝p2指向的对象
    delete p;								// 对p指向的对象执行析构函数
}
//退出局部作用域;对item、p2和vec调用析构函数
//销毁p2会递减其引用计数;如果引用计数变为 0，对象被释放
//销毁vec会销毁它的元素
```



### 三/五法则

需要析构函数的类也需要拷贝和赋值操作
需要拷贝操作的类也需要赋值操作，反之亦然

所有五个拷贝控制成员应该看作一个整体:一般来说，如果一个类定义了任何一个拷贝操作，它就应该定义所有五个操作。如前所述，某些类必须定义拷贝构造函数、拷贝赋值运算符和析构函数才能正确工作。这些类通常拥有一个资源，而拷贝成员必须拷贝此资源。一般来说，拷贝一个资源会导致一些额外开销。在这种拷贝并非必要的情况下，定义了移动构造函数和移动赋值运算符的类就可以避免此问题。



### 使用=default

将拷贝控制成员定义为=default 来显式地要求编译器生成合成的版本

```c++
class Sales_data {
public:
    //拷贝控制成员;使用default
    Sales_data() = default;
    Sales_data(const Sales_data&) = default;
    Sales_data& operator=(const Sales_data &);
    ~Sales_data() = default;
    //其他成员的定义，如前
};
// 不希望合成的成员是内联函数，应该只对成员的类外定义使用=default
Sales_data& Sales_data::operator=(const Sales_datas&) = default;
```



### 阻止拷贝

**定义删除的函数**
虽然声明了它们，但不能以任何方式使用它们
在函数的参数列表后面加上=delete 来指出我们希望将它定义为删除的
析构函数不能是删除的成员
合成的拷贝控制成员可能是删除的
	如果一个类有数据成员不能默认构造、拷贝、复制或销毁则对应的成员函数将被定义为删除的

```c++
struct NoCopy {
    NoCopy() = default;				// 使用合成的默认构造函数
    NoCopy(const NoCopy&) = delete;	// 阻止拷贝
    NoCopy &operator=(const NoCopy&) = delete;	// 阻止赋值
    ~NoCopy() = default;			// 使用合成的析构函数
	// 其他成员
};

//private 拷贝控制
// 在新标准发布之前，类是通过将其拷贝构造函数和拷贝赋值运算符声明为 private的来阻止拷贝:
class PrivateCopy {
    //无访问说明符;接下来的成员默认为 private的
    //拷贝控制成员是private的，因此普通用户代码无法访问
    PrivateCopy(const PrivateCopys);
    PrivateCopy &operator=(const PrivateCopys);
    //其他成员
public:
    PrivateCopy() = default;	// 使用合成的默认构造函数
    ~PrivateCopy();				// 用户可以定义此类型的对象，但无法拷贝它们
};
```



## 拷贝控制和资源管理

可以定义拷贝操作，使类的行为看起来像一个值或者像一个指针

### 行为像值的类

为了实现类值行为，HasPtr需要

- 定义一个拷贝构造函数，**完成string的拷贝**，而不是拷贝指针
- 定义一个析构函数来释放string
- 定义一个拷贝赋值运算符来释放对象当前的 string，并从右侧运算对象拷贝string

```c++
class HasPtr{
public:
    HasPtr(const std::string &s = std::string()) :
    	ps(new std::string(s)), i(0) { }
    // 对ps指向的string，每个HasPtr对象都有自己的拷贝
    HasPtr(const HasPtr &p) : 
        ps(new std::string(*p.ps)), i(p.i) { }
    HasPtr& operator=(const HasPtr &);
    ~HasPtr() { delete ps; }
private:
    std;:string *ps;
	int i;
};

//类值拷贝赋值运算符
HasPtr& HasPtr::operator=(const HasPtr &rhs)
{
    auto newp = new string(*rhs.ps); // 拷贝底层string
    delete ps;		// 释放旧内存
    ps = newp;		// 从右侧运算对象拷贝数据到本对象
    i = rhs.i;
    return *this;	// 返回本对象
}

```



### 定义行为像指针的类

```c++
//定义一个使用引用计数的类
class HasPtr {
public:
    // 构造函数分配新的 string 和新的计数器，将计数器置为1
    HasPtr(const std::string &s = std::string()):
    	ps(new std::string(s)), i(0), use(new std::size_t(1)) { }
    // 拷贝构造函数拷贝所有三个数据成员，并递增计数器
    HasPtr(const HasPtr &p):
    	ps(p.ps), i(p.i), use(p.use) { ++*use; }
    HasPtr& operator=(const HasPtr&);
    ~HasPtr();
private:
    std::string *ps;
    int i;
    std::size_t *use;	// 用来记录有多少个对象共享*ps的成员
};

HasPtr::~HasPtr()
{
    if (--*use == 0) {	// 如果引用计数变为0
        delete ps;		// 释放string内存
        delete use;		// 释放计数器内存
    }
}

HasPtr& HasPtr::operator=(const HasPtr &rhs)
{
    ++*rhs.use;	// 递增右侧运算对象的引用计数
    if (--*use == 0){	// 然后递减本对象的引用计数
        delete ps;		// 如果没有其他用户
        delete use;		// 释放本对象分配的成员
    }
    ps = rhs.ps;		// 将数据从rhs拷贝到本对象
    i = rhs.i;
    use = rhs.use;
	return *this;		// 返回本对象
}
```



## 交换操作

管理资源的类通常还定义一个名为 swap 的函数
对于那些与重排元素顺序的算法一起使用的类，定义swap是非常重要的
这类算法在需要交换两个元素时会调用 swap

```c++
//swap示例
HasPtr temp = v1;		// 创建v1的值的一个临时副本
v1 = v2;				// 将v2的值赋予v1
v2 = temp;				// 将保存的v1的值赋予v2
```

```c++
//编写我们自己的swap函数
class HasPtr{
    friend void swap(HasPtr&, HasPtr&);
};

inline void swap(HasPtr &lhs, HasPtr &rhs)
{
    using std::swap;
    swap(lhs.ps, rhs.ps);		// 交换指针，而不是string 数据
    swap(lhs.i, rhs.i);			// 交换int成员
}
```

每个 swap 调用应该都是未加限定的
	即,每个调用都应该是 swap,而不是 std::swap
如果存在类型特定的 swap 版本，其匹配程度会优于 std 中定义的版本

```c++
//在赋值运算符中使用swap
// 注意 rhs 是按值传递的，意味着 HasPtr的拷贝构造函数
// 将右侧运算对象中的string拷贝到rhs
HasPtr& HasPtr::operator=(HasPtr rhs){
    // 交换左侧运算对象和局部变量rhs的内容
    swap(*this, rhs);		// rhs现在指向本对象曾经使用的内存
    return *this;			// rhs被销毁，从而delete了rhs中的指针
}
```



## 对象移动

在其中某些情况下，对象拷贝后就立即被销毁了。在这些情况下，移动而非拷贝对象会大幅度提升性能

### 右值引用

所谓右值引用就是必须绑定到右值的引用
我们通过&&而不是&来获得右值引用

右值引用有一个重要的性质：**只能绑定到一个将要销毁的对象**。
	因此，我们可以自由地将一个右值引用的资源“移动”到另一个对象中

对于常规引用，不能将其绑定到要求转换的表达式、字面常量或是返回右值的表达式
右值引用有着完全相反的绑定特性：
	我们可以将一个右值引用绑定到这类表达式上
	但不能将一个右值引用直接绑定到一个左值上

```c++
int i = 42;					
int &r = i;					// 正确:r引用i
int &&rr = i;				// 错误:不能将一个右值引用绑定到一个左值上
int &r2 = i * 42;			// 错误:i*42是一个右值
const int &r3 = i * 42;		// 正确:我们可以将一个const的引用绑定到一个右值上
int &&rr2 = i * 42;			// 正确:将rr2绑定到乘法结果上
```

**左值持久;右值短暂**
左值有持久的状态
右值要么是字面常量，要么是在表达式求值过程中创建的临时对象

**变量是左值**

```c++
int &&rr1 = 42;		// 正确:字面常量是右值
int &&rr2 = rr1;	// 错误:表达式rr1是左值!
```

**标准库move函数**

```c++
int &&rr3 = std::move(rrl);	// ok
// move 调用告诉编译器:我们有一个左值，但希望像一个右值一样处理它
// 调用move就意味着承诺:除了对rr1赋值或销毁它外，我们将不再使用它
// 在调用move之后，我们不能对移后源对象的值做任何假设
```



### 移动构造函数和移动赋值运算符

移动构造函数的第一个参数是该类类型的一个引用
	不同于拷贝构造函数的是，这个引用参数在移动构造函数中是一个右值引用
	与拷贝构造函数一样，任何额外的参数都必须有默认实参

```c++
//移动构造函数
// 必须在类头文件的声明中和定义中(如果定义在类外的话)都指定noexcept
StrVec::StrVec(StrVec &&s) noexcept	// 移动操作不应抛出任何异常
    // 成员初始化器接管s中的资源
	: elements(s.elements), first_free(s.first_free), cap(s.cap)
{
    // 令s进入这样的状态-对其运行析构函数是安全的
    s.elements = s.first_free = s.cap = nullptr;
}
```

与拷贝构造函数不同，移动构造函数不分配任何新内存
在接管内存之后，它将给定对象中的指针都置为 nullptr
这样就完成了从给定对象的移动操作，此对象将继续存在
移后源对象会被销毁，意味着将在其上运行析构函数

```c++
//移动赋值运算符
StrVec &StrVec::operator=(StrVec &&rhs) noexcept
{
    // 直接检测自赋值
    if (this != &rhs) {
        free();						// 释放已有元素
        elements = rhs.elements;	// 从rhs接管资源
        first_free = rhs.first_free;
        cap = rhs.cap;	
        // 将rhs置于可析构状态
        rhs.elements = rhs.first_free = rhs.cap = nullptr;
    }
    return *this;
}
```

**移后源对象必须可析构**
除了将移后源对象置为析构安全的状态之外
移动操作还必须保证对象仍然是有效的
	对象有效就是指可以安全地为其赋予新值或者可以安全地使用而不依赖其当前值
	移动操作对移后源对象中留下的值没有任何要求
因此，我们的程序不应该依赖于移后源对象中的数据

**合成的移动操作**
与拷贝操作不同，编译器根本不会为某些类合成移动操作
	如果一个类定义了自己的拷贝构造函数、拷贝赋值运算符或者析构函数，编译器就不会为它合成移动构造函数和移动赋值运算符
	只有当一个类没有定义任何自己版本的拷贝控制成员，且类的每个非static数据成员都可以移动时，编译器才会为它合成移动构造函数或移动赋值运算符

```c++
//编译器会为X和hasX合成移动操作
struct X {
    int i;			// 内置类型可以移动
	std::string s;	// string定义了自己的移动操作
};
struct hasX{
    X mem;	// X有合成的移动操作
};
X x, x2 = std::move(x);			// 使用合成的移动构造函数
hasX hx, hx2 = std::move(hx);	// 使用合成的移动构造函数

// 假定丫是一个类，它定义了自己的拷贝构造函数但未定义自己的移动构造函数
struct hasY {
    hasY() = default;
    hasY(hasY&&) = default;
    Y mem;// hasY将有一个删除的移动构造函数
};
hasY hy, hy2 = std::move(hy);	// 错误:移动构造函数是删除的
```

定义了一个移动构造函数或移动赋值运算符的类必须也定义自己的拷贝操作否则，这些成员默认地被定义为删除的。

**移动右值，拷贝左值**

```c++
StrVec vl, v2;				
vl = v2;					// v2是左值;使用拷贝赋值
StrVec getVec(istream &);	// getVec 返回一个右值
v2 = getVec(cin);			// getVec(cin)是一个右值;使用移动赋值
```

**但如果没有移动构造函数，右值也被拷贝**

```c++
class Foo {
public:
    Foo() = default;
    Foo(const Foo&); // 拷贝构造函数
    // 其他成员定义，但 Foo 未定义移动构造函数
};
Foo x;
Foo y(x);				// 拷贝构造函数;x是一个左值
Foo z(std::move(x));	// 拷贝构造函数，因为未定义移动构造函数
```

**拷贝并交换赋值运算符和移动操作**

```c++
class HasPtr {
public:
    // 添加的移动构造函数
    HasPtr(HasPtr &&p) noexcept : ps(p.ps), i(p.i) { p.ps = 0; }
    // 赋值运算符既是移动赋值运算符，也是拷贝赋值运算符
    HasPtr& operator=(HasPtr rhs)
        { swap(*this，rhs); return *this; }
    // 其他成员的定义
};

hp = hp2;				// hp2是一个左值;hp2通过拷贝构造函数来拷贝
hp = std::move(hp2);	// 移动构造函数移动 hp2
```

**移动迭代器**
一个移动迭代器通过改变给定迭代器的解引用运算符的行为来适配此迭代器
	与其他迭代器不同，移动迭代器的解引用运算符生成一个右值引用
	一个其他的迭代器的解引用运算符返回一个指向元素的左值

```c++
void StrVec::reallocate()
{
    // 分配大小两倍于当前规模的内存空间
    auto newcapacity = size() ? 2 * size() : 1;
    auto first = alloc.allocate(newcapacity);
    // 移动元素
    auto last = uninitialized_copy(make_move_iterator(begin()),
                                   make_move_iterator(end()),
                                   first);
    free();					// 释放旧空间
    elements = first;		// 更新指针
    first_free =last;
    cap = elements + newcapacity;
}
```

只有在确信算法在为一个元素赋值或将其传递给一个用户定义的函数后不再访问它时，才能将移动迭代器传递给算法。

在移动构造函数和移动赋值运算符这些类实现代码之外的地方，只有当你确信需要进行移动操作且移动操作是安全的，才可以使用 std::move。



### 右值引用和成员函数

允许移动的成员函数通常使用与拷贝/移动构造函数和赋值运算符相同的参数模式
	一个版本接受一个指向 const 的左值引用
	第二个版本接受一个指向非const的右值引用

```c++
void push_back(const X&);	// 拷贝:绑定到任意类型的X
void push_back(X&&);		// 移动:只能绑定到类型X的可修改的右值
```

当我们希望从实参“窃取”数据时，通常传递一个右值引用。为了达到这目的，实参不能是 const 的
从一个对象进行拷贝的操作不应该改变该对象。因此，通常不需要定义一个接受一个(普通的)X&参数的版本

```c++
class StrVec {
public:
    void push_back(const std::string&);		// 拷贝元素
    void push_back(std::string&&);			// 移动元素
    // 其他成员的定义，如前
};

void StrVec::push_back(const string& s)
{
    chk_n_alloc();	// 确保有空间容纳新元素
    // 在first_free指向的元素中构造s的一个副本
    alloc.construct(first_free++, s);
}

void StrVec::push_back(string &&s)
{
    chk_n_alloc();	// 如果需要的话为 StrVec 重新分配内存
    alloc.construct(first_free++, std::move(s));
}

StrVec vec;//空StrVec
string s = "some string or another";
vec.push_back(s);		// 调用push_back(const string&)
vec.push_back("done");	// 调用push_back(string&&)
```



**右值和左值引用成员函数**

```c++
string s1 = "a value", s2 = "another";
auto n = (s1 + s2).find('a');

s1 + s2 = "wow!";	// 对两个string的连接结果一个右值，进行了赋值

//希望强制左侧运算对象(即，this 指向的对象)是一个左值
// 引用限定符(reference qualifier)
class Foo{
public:
	Foo &operator=(const Foo&) &;// 只能向可修改的左值赋值
    // Foo的其他参数    
};

Foo &Foo::operator=(const Foo &rhs) & 
{
    // 执行将rhs赋予本对象所需的工作
    return *this;
}

Foo &retFoo();		// 返回一个引用;retFoo调用是一个左值
Foo retVal();		// 返回一个值;retVal调用是一个右值
Foo i, j;			// i和j是左值
i = j;				// 正确:i是左值
retFoo() = j;		// 正确:retFoo()返回一个左值
retVal() = j;		// 错误:retVal()返回一个右值
i = retVal();		// 正确:我们可以将一个右值作为赋值操作的右侧运算对象

//一个函数可以同时用const 和引用限定。在此情况下,引用限定符必须跟随在const限定符之后:
class Foo {
public:
    Foo someMem() & const;		// 错误:const 限定符必须在前
    Foo anotherMem() const &;	// 正确:const限定符在前
};
```



**重载和引用函数**
引用限定符也可以区分重载版本

```c++
class Foo{
public:
    Foo sorted() &&;			// 可用于可改变的右值
    Foo sorted() const &;		// 可用于任何类型的 Foo
    // Foo的其他成员的定义
private:
    vector<int> data;
};

// 本对象为右值，因此可以原址排序
Foo Foo::sorted() &&
{
    sort(data.begin(), data.end());
    return *this;
}

// 本对象是 const 或是一个左值，哪种情况我们都不能对其进行原址排序
Foo Foo::sorted() const & {
    Foo ret(*this);		// 拷贝一个副本
    sort(ret.data.begin(), ret.data.end());	// 排序副本
    return ret;		// 返回副本
}

retVal().sorted();	// retVal()是一个右值，调用 Foo::sorted() &&
retFoo().sorted();	// retFoo()是一个左值，调用 Foo::sorted() const &

// 如果定义两个或两个以上具有相同名字和相同参数列表的成员函数，就必须对所有函数都加上引用限定符，或者所有都不加:
class Foo {
public:
    Foo sorted() &&;
    Foo sorted() const;		// 错误:必须加上引用限定符
    // comp是函数类型的类型别名
    // 此函数类型可以用来比较 int 值
    using Comp = bool(const int&, const int&);
    Foo sorted(Comp*);			// 正确:不同的参数列表
    Foo sorted(Comp*) const;	// 正确:两个版本都没有引用限定符
};
```



# 重载运算与类型转换

重载的运算符是具有特殊名字的函数:它们的名字由关键字 operator 和其后要定义的运算符号共同组成
和其他函数一样，重载的运算符也包含返回类型、参数列表以及函数体

重载运算符函数的参数数量与该运算符作用的运算对象数量一样多。
	一元运算符有个参数，二元运算符有两个
如果一个运算符函数是成员函数，则它的第一个(左侧)运算对象绑定到隐式的this指针上，因此，成员运算符函数的(显式)参数数量比运算符的运算对象总数少一个

对于一个运算符函数来说，它或者是类的成员，或者至少含有一个类类型的参数

![](.\Picture\运算符.png)



**直接调用一个重载的运算符函数**

```c++
// 一个非成员运算符函数的等价调用
data1 + data2;				// 普通的表达式
operator+(data1, data2);	// 等价的函数调用

data1 += data2;				// 基于“调用”的表达式
data1.operator+=(data2);	// 对成员运算符函数的等价调用
```

**使用与内置类型一致的含义**

- 如果类执行IO操作，则定义移位运算符使其与内置类型的IO 保持一致。
- 如果类的某个操作是检查相等性，则定义 operator==；如果类有了operator==，意味着它通常也应该有operator!=。
- 如果类包含一个内在的单序比较操作，则定义 operator<；如果类有了operator<，则它也应该含有其他关系操作。
- 重载运算符的返回类型通常情况下应该与其内置版本的返回类型兼容:逻辑运算符和关系运算符应该返回 bool，算术运算符应该返回一个类类型的值，赋值运算符和复合赋值运算符则应该返回左侧运算对象的一个引用。

**赋值和复合赋值运算符**
赋值运算符的行为与复合版本的类似:
	赋值之后，左侧运算对象和右侧运算对象的值相等，并且运算符应该返回它左侧运算对象的一个引用



## 输入和输出运算符

### 重载输出运算符<<

通常情况下，输出运算符的第一个形参是一个非常量 ostream 对象的引用
	之所以ostream 是非常量是因为向流写入内容会改变其状态
	而该形参是引用是因为我们无法直接复制一个ostream对象
第二个形参一般来说是一个常量的引用，该常量是我们想要打印的类类型
	第二个形参是引用的原因是我们希望避免复制实参
	而之所以该形参可以是常量是因为(通常情况下)打印对象不会改变对象的内容
为了与其他输出运算符保持一致，operator<<一般要返回它的ostream形参

```c++
//Sales_data的输出运算符
ostream &operator<<(ostream &os, const Sales_data &item)
{
    os << item.isbn() << " " << item.units_sold << " " 
        << item.revenue << " " << item.avg_price();
    return os;
}
//输出运算符尽量减少格式化操作

//输入输出运算符必须是非成员函数 IO运算符一般被声明为友元
Sales_data data;
data << cout;		// 如果operator<<是Sales_data的成员
```



### 重载输入运算符>>

第一个形参是运算符将要读取的流的引用
第二个形参是将要读入到的(非常量)对象的引用
	因为输入运算符本身的目的就是将数据读入到这个对象中，所以必须是个非常量

```c++
istream &operator>>(istream &is, Sales_data &item)
{
    double price;		// 不需要初始化，因为我们将先读入数据到 price，之后才使用它
	is >> item.bookNo >> item.units_sold >> price;
	if (is)	    // 检查输入是否成功
        item.revenue = item.units_sold * price;
    else
        item = Sales_data();	// 输入失败:对象被赋予默认的状态
    return is;
}

//标示错误
// 通常情况下,输入运算符只设置failbit。
// 设置eofbit 表示文件耗尽
// 而设置 badbit表示流被破坏
// 最好的方式是由IO标准库自己来标示这些错误。
```

## 算术和关系运算符

通常情况下，把算术和关系运算符定义成**非成员函数**以允许对左侧或右侧的运算对象进行转换
因为这些运算符一般不需要改变运算对象的状态，所以形参都是常量的引用

```c++
//假设两个对象指向同一本书
Sales_data operator+(const Sales_data &lhs, const Sales_data &rhs)
{
    Sales_data sum = lhs;		// 把lhs的数据成员拷贝给sum
    sum += rhs;					// 将rhs加到sum中
    return sum;
}
```

### 相等运算符

```c++
bool operator==(const Sales data &lhs， const Sales data &rhs)
{
    return lhs.isbn() == rhs.isbn() && 
        lhs.units_sold == rhs.units_sold && 
        lhs.revenue == rhs.revenue;
}
bool operator!=(const Sales data &lhs, const Sales_data &rhs)
{
    return !(lhs == rhs);
}
```

### 关系运算符

定义顺序关系，令其与关联容器中对关键字的要求一致
如果类同时也含有运算符的话，则定义一种关系令其与保持一致
	特别是，如果两个对象是!=的，那么一个对象应该<另外一个

## 赋值运算符

一种运算符接受花括号内的元素列表作为参数

```c++
vector<string> v;
v = {"a", "an", "the"};

class StrVec {
public:
    StrVec &operator=(std::initializer_list<std::string>);
    // ...
};

StrVec &StrVec::operator=(initializer_list<string> il)
{
    // alloc_n_copy分配内存空间并从给定范围内拷贝元素
    auto data = alloc_n_copy(il.begin(), il.end());
    free();		// 销毁对象中的元素并释放内存空间
    elements = data.first;	// 更新数据成员使其指向新空间
    first_free = cap = data.second;
    return *this;
}

//复合赋值运算符
// 作为成员的二元运算符:左侧运算对象绑定到隐式的 this 指针
// 假定两个对象表示的是同一本书
Sales_datas Sales_data;;operator+=(const Sales_data &rhs)
{
    units_sold += rhs.units_sold;
    revenue += rhs.revenue;
    return *this;
}
```



## 下标运算符

表示容器的类通常可以通过元素在容器中的位置访问元素，这些类一般会定义下标运算符operator[]
下标运算符必须是成员函数

下标运算符通常以所访问元素的引用作为返回值
最好同时定义下标运算符的常量版本和非常量版本

```c++
class StrVec {
public:
    std::string& operator[](std::size_t n)
    	{ return elements[n]; }
    const std::string& operator[](std::size_t n) const
    	{ return elements[n]; }
private:
    std::string *elements;	// 指向数组首元素的指针
};

// 假设svec是一个StrVec对象
const StrVec cvec = svec;		// 把svec的元素拷贝到cvec中
// 如果svec中含有元素，对第一个元素运行string的empty函数
if (svec.size() && svec[0].empty()) {
    svec[0] = "zero";		// 正确:下标运算符返回 string的引用
    cvec[0] = "Zip";			// 错误:对 cvec取下标返回的是常量引用
}
```



## 递增和递减运算符

递增和递减运算符既有前置版本有后置版本

```c++
class StrBlobPtr {
public:
    // 前置递增和递减运算符
    StrBlobPtr& operator++();		// 前置运算符
    StrBlobPtr& operator--();		
    // 其他成员和之前的版本一致
    
    // 后置版本接受一个额外的(不被使用)int类型的形参
    StrBlobPtr operator++(int);		//后置运算符
    StrBlobPtr operator--(int);
};

//前置版本:返回递增/递减对象的引用
StrBlobPtr& StrBlobPtr::operator++()
{
    // 如果curr已经指向了容器的尾后位置，则无法递增它
    check(curr, "increment past end of StrBlobPtr");
    ++curr;				// 将curr在当前状态下向前移动一个元素
    return *this;
}
StrBlobPtr& StrBlobPtr::operator--() {
    // 如果curr是0，则继续递减它将产生一个无效下标
    --curr;		// 将curr在当前状态下向后移动一个元素
    check(curr, "decrement past begin of StrBlobPtr");
    return *this;
}

//后置版本:递增/递减对象的值但是返回原值
StrBlobPtr StrBlobPtr::operator++(int)
{
    // 此处无须检查有效性，调用前置递增运算时才需要检查
    StrBlobPtr ret = *this; // 记录当前的值
    ++*this;				// 向前移动一个元素，前置++需要检查递增的有效性
	return ret;				// 返回之前记录的状态
}
StrBlobPtr StrBlobPtr::operator--(int)
{
    // 此处无须检查有效性，调用前置递减运算时才需要检查
    StrBlobPtr ret = *this;		// 记录当前的值
    --*this;					// 向后移动一个元素，前置--需要检查递减的有效性
    return ret;					// 返回之前记录的状态
}

//显式地调用后置运算符
StrBlobPtr p(a1);		// p指向al中的vector
p.operator++(0);		// 调用后置版本的operator++
p.operator++();			// 调用前置版本的operator++
```



## 成员访问运算符

在迭代器类及智能指针类中常常用到解引用运算符 (*)和箭头运算符(->)

```c++
class StrBlobPtr {
public:
    std::string& operator*() const 
    { 
        auto p = check(curr，"dereference past end");
        return (*p)[curr];			// (*p)是对象所指的vector
    }
    std::string* operator->() const
    {
        // 将实际工作委托给解引用运算符
        return & this->operator*();
    }
};

StrBlob a1 = {"hi", "bye", "now"};
StrBlobPtr p(a1);				// p指向a1中的vector
*p = "okay";					// 给al的首元素赋值
cout << p->size() << endl;		// 打印4，这是a1首元素的大小
cout << (*p).size() << endl;	// 等价于p->size()

//对箭头运算符返回值的限定
// 箭头运算符永远不能丢掉成员访问这个最基本的含义
// 对于形如point->mem的表达式来说，point必须是指向类对象的指针或者是一个重载了operator->的类的对象
// 根据 point 类型的不同，point-mem 分别等价于:
(*point).mem;				// point 是一个内置的指针类型
point.operator()->mem;		// point 是类的一个对象
```

## 函数调用运算符

如果类重载了函数调用运算符，则可以像使用函数一样使用该类的对象

```c++
struct absInt {
    int operator()(int val) const {
        return val < 0 ? -val : val;
    } 
};
int i = -42;
absInt absObj;				// 含有函数调用运算符的对象
int ui = absObj(i);			// 将i传递给absObj.operator()

//含有状态的函数对象类
class PrintString {
public:
    PrintString(ostream &o = cout, char c = ' ') :
    	os(o), sep(c) {}
    void operator()(const string &s) const { os << s << sep; }
private:
    ostream &os;		// 用于写入的目的流
    char sep;			// 用于将不同输出隔开的字符
};
PrintString printer;	// 使用默认值，打印到 cout
printer(s);				// 在cout中打印s，后面跟一个空格
PrintString errors(cerr, '\n');
errors(s);				// 在cerr中打印s，后面跟一个换行符

```

### lambda是函数对象

编译器将该表达式翻译成一个未命名类的未命名对象

```c++
// 根据单词的长度对其进行排序，对于长度相同的单词按照字母表顺序排序
stable_sort(words.begin(), words.end(), 
            [](const string &a, const string &b)
            { return a.size() < b.size(); });
// lambda函数等价于
class ShorterString {
public:
    bool operator()(const string &s1, const string &s2) const
    { return s1.size() < s2.size(); }
};
stable_sort(words.begin(), words.end(), ShorterString());
```

当一个lambda 表达式通过**引用**捕获变量时，将由**程序负责确保**lambda执行时引用所引的对象确实存在

```c++
//获得第一个指向满足条件元素的迭代器，该元素满足size() is >= sz
auto wc = find_if(words.begin(), words.end(), 
                  [sz](const string &a)
                  	{ return a.size() >= sz; });

class SizeComp {
    SizeComp(size_t n) : sz(n) { }	// 该形参对应捕获的变量
    // 该调用运算符的返回类型、形参和函数体都与lambda一致
    bool operator()(const string &s) const  
    	{ returns.size() >=sz; }
private:
    size_t sz;		// 该数据成员对应通过值捕获的变量
};

```



### 标准库函数对象

算术
	plus<Type>
	minus<Type>
	multiplies<Type>
	divides<Type>
	modulus<Type>
	negate<Type>

关系
	equal_to<Type>
	not_equal_to<Type>
	greater<Type>
	greater_equal<Type>
	less<Type>
	less_equal<Type>

逻辑
	logical_and<Type>
	logical_or<Type>
	logical_not<Type>

```c++
//在算法中使用标准库函数对象
//传入一个临时的函数对象用于执行两个string 对象的>比较运算
sort(svec.begin(), svec.end(), greater<string>());
```



### 可调用对象与function

可调用的对象
	函数
	函数指针
	lambda 表达式
	bind 创建的对象
	重载了函数调用运算符的类

```c++
//不同类型可能具有相同的调用形式
// 普通函数
int add(int i,int j){ return i + j; }
// lambda，其产生一个未命名的函数对象类
auto mod = [](int i, int j) { return i % j; };
// 函数对象类
struct divide {
    int operator()(int denominator, int divisor) {
        return denominator / divisor;
    } 
};

// 构建从运算符到函数指针的映射关系，其中函数接受两个int、返回一个int
map<string, int(*)(int, int)> binops;
//正确:add是一个指向正确类型函数的指针
binops.insert({"+", add}); 		// {"+", add}是一个pair
// mod是个lambda表达式，而每个lambda有它自己的类类型，该类型与存储在binops中的值的类型不匹配
binops.insert({"%", mod});		// 错误:mod不是一个函数指针
```

**标准库function类型**

| function的操作                                               |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| function<T> f;                                               | f是一个用来存储可调用对象的空function，这些可调用对象的调用形式应该与函数类型T相同(即T是retType(args)) |
| function<T> f(nullptr);                                      | 显式地构造一个空function                                     |
| function<T> f(obj);                                          | 在f中存储可调用对象obi的副本                                 |
| f                                                            | 将f作为条件:当f含有一个可调用对象时为真;否则为假             |
| f(args)                                                      | 调用f中的对象，参数是args                                    |
|                                                              | **定义为function<T>的成员的类型**                            |
| result_type                                                  | 该function类型的可调用对象返回的类型                         |
| argument_type<br />first_argument_type <br />second_argument_type | 当T有一个或两个实参时定义的类型。如果T只有一个实参则argument_type是该类型的同义词;如果T有两个实参则first_argument_type和second_argument_type分别代表两个实参的类型 |

```c++
function<int(int, int)> f1 = add;				// 函数指针
function<int(int, int)> f2 = divide();			// 函数对象类的对象
function<int(int, int)> f3 = [](int i, int j)	// lambda
							{ return i * j };
cout << f1(4, 2) << endl;	// 打印6
cout << f2(4, 2) << endl;	// 打印2
cout << f3(4, 2) << endl;	// 打印8

// 列举了可调用对象与二元运算符对应关系的表格
// 所有可调用对象都必须接受两个 int、返回一个 int
// 其中的元素可以是函数指针、函数对象或者 lambda
map<string, function<int(int, int)>> binops = {
    {"+", add},									// 函数指针
    {"-", std::minus<int>()},					// 标准库函数对象
    {"/", divide()},							// 用户定义的函数对象
    {"*", [](int i, int j) {return i * j;} },	// 未命名的lambda
    {"%", mod} };								// 命名了的lambda对象

binops["+"](10, 5);		// 调用add(10，5)
binops["-"](10, 5);		// 使用minus<int>对象的调用运算符
binops["/"](10, 5);		// 使用divide对象的调用运算符
binops["*"](10, 5);		// 调用lambda函数对象
binops["%"](10, 5);		// 调用lambda函数对象
```



**重载的函数与function**

```c++
int add(int i, int j) { return i + j; }
Sales_data add(const Sales_data&, const Sales_data&);
map<string, function<int(int, int)>> binops;
binops.insert( {"+", add} );		// 错误：哪个add？

int (*fp)(int, int) = add;			// 指针所指的 add是接受两个int的版本
binops.insert( {"+", fp} );			// 正确:fp指向一个正确的add 版本
//正确:使用lambda来指定我们希望使用的add版本
binops.insert( {"+", [](int a, int b) {return add(a, b);} } );
```



## 重载、类型转换与运算符

转换构造函数和类型转换运算符共同定义了**类类型转换**(class-type conversions)，这样的转换有时也被称作**用户定义的类型转换**(user-defined conversions)。

### 类型转换运算符

`operator type() const;`

类型转换运算符既没有显式的返回类型，也没有形参,而且必须定义成类的成员函数
类型转换运算符通常不应该改变待转换对象的内容，因此，类型转换运算符一般被定义成const成员

```c++
//定义含有类型转换运算符的类
class SmallInt {
public:
    SmallInt(int i = 0) : val(i)
    {
        if(i < 0 || i > 255)
            throw std::out_of_range("Bad SmallInt value");
    }
    operator int() const { return val; }
private:
    std::size_t val;
};

SmallInt si;
si = 4;		// 首先将4隐式地转换成SmallInt，然后调用SmallInt::operator=
si + 3;		// 首先将si隐式地转换成int，然后执行整数的加法

class SmallInt;
operator int(SmallInt&);			// 错误:不是成员函数
class SmallInt {
public:
    int operator int() const;			// 错误:指定了返回类型
    operator int(int = 0) const;		// 错误:参数列表不为空
    operator int*() const {return 42;} 	// 错误:42不是一个指针
};
```

**显式的类型转换运算符**

```c++
class SmallInt {
public:
    // 编译器不会自动执行这一类型转换
    explicit operator int()const { return val; }
    // 其他成员与之前的版本一致
}

SmallInt si = 3;		// 正确:SmallInt的构造函数不是显式的
si + 3;					// 错误:此处需要隐式的类型转换，但类的运算符是显式的
static_cast<int>(si) + 3;	// 正确:显式地请求类型转换
```

即如果表达式被用作条件，则编译器会将显式的类型转换自动应用于它
	if、while及do语句的条件部分
	for语句头的条件表达式
	逻辑非运算符 (!)、逻辑或运算符 (||)、逻辑与运算符(&&)的运算对象
	条件运算符(?:)的条件表达式



### 避免有二义性的类型转换

通常情况下，不要为类定义相同的类型转换，也不要在类中定义两个及两个以上转换源或转换目标是算术类型的转换。

**实参匹配和相同的类型转换**

```c++
// 最好不要在两个类之间构建相同的类型转换
struct B;
struct A  {
    A() = default;
    A(const B&);		// 把一个B转换成A
    // 其他数据成员
};
struct B {
    operator A() const;	// 也是把一个B转换成A
    //其他数据成员
};
A f(const A&);
B b;
A a = f(b); 	// 二义性错误:含义是f(B::operator A())
				// 还是 f(A::A(const B&))?

// 修改
A a1 = f(b.operator A());	// 正确:使用B的类型转换运算符
A a2 = f(A(b));				// 正确:使用A的构造函数
```

**二义性与转换目标为内置类型的多重类型转换**
	如果类定义了一组类型转换，它们的转换源(或者转换目标)类型本身可以通过其他类型转换联系在一起，则同样会产生二义性的问题。

```c++
struct A {
    A(int = 0);					// 最好不要创建两个转换源都是算术类型的类型转换
    A(double);
    operator int() const;
    operator double() const;	// 最好不要创建两个转换对象都是算术类型的类型转换
    // 其他成员
};
void f2(long double);
A a;
f2(a);	// 二义性错误:含义是f(A::operator int())
		// 还是f(A::operator double())?
long lg;
A a2(lg);	// 二义性错误:含义是A::A(int)还是A::A(double)?

short s = 42;
// 把short提升成int优于把short转换成double
A a3(s);	// 使用A::A(int)
```

当我们使用两个用户定义的类型转换时，如果转换函数之前或之后存在标准类型转换，则标准类型转换将决定最佳匹配到底是哪个。

**重载函数与转换构造函数**

```c++
struct C {
    C(int);
    // 其他成员
};
struct D{
    D(int);
    // 其他成员
};
void manip(const C&);
void manip(const D&);
manip(10);		// 二义性错误:含义是manip(C(10))还是manip(D(10))
manip(C(10));	// 正确:调用manip(const C&)
```

**重载函数与用户定义的类型转换**

```c++
struct E {
	E(double);
    // 其他成员
};
void manip2(const C&);
void manip2(const E&);
// 二义性错误:两个不同的用户定义的类型转换都能用在此处
manip2(10);	// 含义是manip2(C(10))还是manip2(E(double(10)))
```

### 函数匹配与重载运算符

表达式中运算符的候选函数集既应该包括成员函数，也应该包括非成员函数

```c++
class SmallInt {
    friend SmallInt operator+(const SmallInt&, const SmallInt&);
public:
    SmallInt(int = 0);						// 转换源为int的类型转换
    operator int() const { return val; }	// 转换目标为int的类型转换
private:
    std::size_t val;
};
SmallInt s1, s2;
SmallInt s3 = s1 + s2;			// 使用重载的operator+
int i = s3 + 0;					// 二义性错误
```



# 面向对象程序设计

## OOP概述

面向对象程序设计(object-oriented programming)的核心思想是数据抽象、继承和动态绑定。
	通过使用数据抽象，可以将类的接口与实现分离
	使用继承，可以定义相似的类型并对其相似关系建模
	使用动态绑定，可以在一定程度上忽略相似类型的区别，而以统一的方式使用它们的对象

```c++
class Quote{
public:
	std::string isbn() const;
	virtual double net_price(std::size_t n) const;
};

class Bulk_quote : public Quote{		// Bulk_quote继承了 Quote
public:
    double net price(std::size_t) const override;
}; 
```

**动态绑定**

```c++
// 计算并打印销售给定数量的某种书籍所得的费用
double print_total(ostream &os, const Quote &item, size_t n)
{
    // 根据传入item形参的对象类型调用Quote::net_price
    // 或者Bulkquote::net_price
    double ret =item.net_price(n);
    os << "ISBN: " << item.isbn()		// 调用 Quote::isbn
        << " #sold:" << n << " total due:" << ret << endl;
    return ret;
}

// basic的类型是Quote;bulk的类型是Bulk_quote
print_total(cout, basic, 20);		// 调用Quote的net_price
print_total(cout, bulk, 20);		// 调用Bulk_quote的net_price
```



## 定义基类和派生类

### 定义基类

```c++
class Quote {
public:
    Quote() = default;
    Quote(const std::string &book, double sales_price):
    	bookNo(book), price(sales_price){ }
    std::string isbn() const { return bookNo; }
    // 返回给定数量的书籍的销售总额
    // 派生类负责改写并使用不同的折扣计算算法
    virtual double net_price(std::size_t n) const
    	{ return n * price; }
    virtual ~Quote() = default; 	// 对析构函数进行动态绑定
private:
    std::string bookNo;				// 书籍的ISBN编号
protected:
    double price = 0.0;				// 代表普通状态下不打折的价格
};
```

### 定义派生类

```c++
class Bulk_quote : public Quote{	// Bulk_quote继承自Quote
public:
    Bulk_quote()= default;
    Bulk_quote(const std::string&, double, std::size_t, double);
    // 覆盖基类的函数版本以实现基于大量购买的折扣政策
    double net_price(std::size_t) const override;
private:
    std::size_t min_qty = 0;		// 适用折扣政策的最低购买量
    double discount = 0.0;			// 以小数表示的折扣额
};
```

派生类经常(但不总是)覆盖它继承的虚函数。如果派生类没有覆盖其基类中的某个虚函数，则该虚函数的行为类似于其他的普通成员，派生类会直接继承其在基类中的版本。

C++11 新标准允许派生类显式地注明它使用某个成员函数覆盖了它继承的虚函数。具体做法是在形参列表后面、或者在const成员函数的const关键字后面、或者在引用成员函数的引用限定符后面添加一个关键字override。

<img src=".\Picture\Bulk_quo对象的概念结构.png" style="zoom:50%;" />

```c++
Quote item;			// 基类对象
Bulk_quote bulk;	// 派生类对象
Quote *p = &item;	// p指向Quote对象
p = &bulk;			// p指向bulk的Quote部分
Quote &r = bulk;	// r绑定到bulk的Quote部分
```

**派生类构造函数**

```c++
Bulk_quote(const std::string& book, double p, std::sizet qty, double disc) :
	Quote(book, p), min_qty(qty), discount(disc) { }
//与之前一致
```

如果我们想将某个类用作基类，则该类必须已经定义而非仅仅声明

**防止继承的发生**

```c++
class NoDerived final { /* */ }；		// NoDerived不能作为基类
class Base {/* */};
// Last是final的;我们不能继承Last
class Last final : Base { /* */ };		// Last不能作为基类
class Bad : NoDerived { /* */ };		// 错误:NoDerived是final的
class Bad2 : Last{ /* */ };				// 错误:Last是final的
```



### 类型转换与继承

**静态类型与动态类型**
表达式的静态类型在编译时总是已知的，它是变量声明时的类型或表达式生成的类型
动态类型则是变量或表达式表示的内存中的对象的类型，动态类型直到运行时才可知

不存在从基类向派生类的隐式类型转换

```c++
Quote base;
Bulk_quote* bulkP = &base;	// 错误:不能将基类转换成派生类
Bulk_quote& bulkRef = base;	// 错误:不能将基类转换成派生类

Bulk_quote bulk;
Quote *itemP = &bulk;		// 正确:动态类型是Bulk_quote
Bulk_quote *bulkP = itemP;	// 错误:不能将基类转换成派生类
```

dynamic cast请求一个类型转换，该转换的安全检查将在运行时执行
已知某个基类向派生类的转换是安全的，则可以使用static_cast来强制覆盖掉编译器的检查工作

```c++
Bulk_quote bulk;	// 派生类对象
Quote item(bulk);	// 使用 Quote::Quote(const Quote&)构造函数
item = bulk;		// 调用 Quote::operator=(const Quote&)
```



## 虚函数

**对虚函数的调用可能在运行时才被解析**

```c++
Quote base("0-201-82470-1", 50);
print_total(cout, base, 10);		// 调用Quote::net_price
Bulk_quote derived("0-201-82470-1", 50, 5, .19);
print_total(cout, derived, 10);		// 调用Bulk_quote::net_price

base = derived;			// 把derived的Quote部分拷贝给base
base.net_price(20);		// 调用Quote::net_price
```

> C++的多态性
> 把具有继承关系的多个类型称为多态类型，因为我们能使用这些类型的“多种形式”而无须在意它们的差异。引用或指针的静态类型与动态类型不同这一事实正是C++语言支持多态性的根本所在。

**派生类中的虚函数**
一旦某个函数被声明成虚函数，则在所有派生类中它都是虚函数。

**final和override说明符**
使用 override 标记了某个函数，但该函数并没有覆盖已存在的虚函数，此时编译器将报错:

```c++
struct B {
    virtual void f1(int) const;
    virtual void f2();
    void f3();
};

struct D1 : B{
    void f1(int) const override;		// 正确:f1与基类中的f1匹配
    void f2(int) override;				// 错误:B没有形如f2(int)的函数
    void f3() override;					// 错误:f3不是虚函数
    void f4() override;					// 错误:B没有名为f4的函数
};
```

把某个函数指定为 final，如果我们已经把函数定义成 final了，则之后任何尝试覆盖该函数的操作都将引发错误:

```c++
struct D2 : B{
    //从B继承f2()和f3()，覆盖f1(int)
    void f1(int) const final;	//	不允许后续的其他类覆盖f1(int)
};
struct D3 : D2 {
    void f2();				// 正确:覆盖从间接基类B继承而来的f2
    void f1(int) const;		//错误:D2已经将f2声明成final
};

```

**虚函数与默认实参**
如果某次函数调用使用了默认实参，则该实参值由本次调用的静态类型决定。
	如果我们通过基类的引用或指针调用函数，则使用基类中定义的默认实参，即使实际运行的是派生类中的函数版本也是如此。此时，传入派生类函数的将是基类函数定义的默认实参。

**回避虚函数的机制**

```c++
// 强行调用基类中定义的函数版本而不管 baseP 的动态类型到底是什么
double undiscounted = baseP->Quote::net_price(42);
```

该调用将在编译时完成解析



## 抽象基类

**纯虚函数**

```c++
// 用于保存折扣值和购买量的类，派生类使用这些数据可以实现不同的价格策略
class Disc_quote : public Quote {
public:
    Disc_quote() = default;
    Disc_quote(const std::string& book, double price, 
		std::size_t qty, double disc) : 
    		Quote(book, price), 
    		quantity(qty), discount(disc) { }
    double net_price(std::size_t) const = 0;
protected:
    std::size_t quantity = 0;		// 折扣适用的购买量
    double discount = 0.0;			// 表示折扣的小数值
};
```

**含有纯虚函数的类是抽象基类**
含有(或者未经覆盖直接继承)纯虚函数的类是抽象基类 (abstract base class)
抽象基类负责定义接口，而后续的其他类可以覆盖该接口
不能(直接)创建一个抽象基类的对象

```c++
// Disc quote声明了纯虚函数，而 Bulk_quote将覆盖该函数
Disc_quote discounted;			// 错误:不能定义Disc_quote的对象
Bulk_quote bulk;				// 正确:Bulk_quote中没有纯虚函数
```

**派生类构造函数只初始化它的直接基类**

```c++
// 当同一书籍的销售量超过某个值时启用折扣
// 折扣的值是一个小于1的正的小数值，以此来降低正常销售价格
class Bulk_quote : public Disc_quote {
public:
    Bulk_quote() = default;
    
    // 派生类构造函数只初始化它的直接基类
    Bulk_quote(const std::string& book, double price,
               std::size_t qty, double disc) :
    	Disc_quote(book, price, qty, disc) { }
    // 覆盖基类中的函数版本以实现一种新的折扣策略
    double net_price(std::size_t) const override;
};
```

## 访问控制与继承

一个类使用 protected 关键字来声明那些它希望与派生类分享
但是不想被其他公共访问使用的成员

```c++
// 公有、私有和受保护继承
class Base {
public:
    void pub_mem();		// public成员
protected:
    int prot_mem;		// protected 成员
private:
    char priv_mem;		// private成员
};

struct Pub_Derv : public Base {
    // 正确:派生类能访问 protected 成员
    int f() { return prot_mem; }
    // 错误:private成员对于派生类来说是不可访问的
    char g() { return priv_mem; }
};

struct Priv_Derv : private Base {
    // private不影响派生类的访问权限
    int f1() const { return prot_mem; }
};


Pub_Derv d1;		// 继承自Base的成员是public的
Priv_Derv d2;		// 继承自Base的成员是private的
d1.pub_mem();		// 正确:pub_mem在派生类中是public的
d2.pub_mem();		// 错误:pub_mem在派生类中是private的
```

**友元与继承**
就像友元关系不能传递一样，友元关系同样也不能继承。

**改变个别成员的可访问性**

```c++
class Base {
public:
    std::size_t size() const { return n; }
protected:
    std::size_t n;
};

class Derived : private Base {	// 注意:private继承
public:
    // 保持对象尺寸相关的成员的访问级别
    using Base::size;
protected:
    using Base::n;
};
```

**默认的继承保护级别**

```c++
class Base { /* ... */ };
struct D1 : Base { /* ... */};	// 默认public继承
class D2 : Base [ /* ... */ };	// 默认private继承
```



## 继承中的类作用域

每个类定义自己的作用域，在这个作用域内我们定义类的成员。
当存在继承关系时，派生类的作用域嵌套在其基类的作用域之内。
如果一个名字在派生类的作用域内无法正确解析，则编译器将继续在外层的基类作用域中寻找该名字的定义。

**在编译时进行名字查找**

一个对象、引用或指针的静态类型决定了该对象的哪些成员是可见的
即使静态类型与动态类型可能不一致，能使用哪些成员仍然是由静态类型决定的

```c++
class Disc_quote : public Quote {
public:
    std::pair<size_t, double> discount_policy() const 
    	{ return {quantity, discount}; }	// 其他成员与之前的版本一致
};

Bulk_quote bulk;			
Bulk_quote *bulkP = &bulk;	// 静态类型与动态类型一致
Quote *itemP = &bulk;		// 静态类型与动态类型不一致
bulkP->discount_policy();	// 正确:bulkP的类型是Bulk_quotet
itemP->discount_policy();	// 错误:itemP的类型是Quote*
```

**名字冲突与继承**

```c++
struct Base {
    Base():mem(0) { }
protected:
    int mem;
};

struct Derived : Base {
    Derived(int i):mem(i) { }		// 用i初始化 Derived::mem
    								// 返回 Derived::mem
    int get_mem() { return mem; }	// Base::mem 进行跌认初始化
protected:
	int mem;		// 隐藏基类中的mem
};
// 通过作用域运算符来使用隐藏的成员
struct Derived : Base {
    int get_base_mem() { return Base::mem; }
    //...
};
```

**名字查找先于类型检查**

```c++
struct Base {
    int memfcn();
};
struct Derived : Base {
    int memfcn(int);	// 隐藏基类的memfcn
};
Derived d;Base b;
b.memfcn();		// 调用 Base::memfcn
d.memfcn(10);	// 调用 Derived::memfcn
d.memfcn();		// 错误:参数列表为空的 memfcn 被隐藏了
d.Base::memfcn();// 正确:调用 Base::emfcn
```

**虚函数与作用域**

```c++
class Base {
public:
    virtual int fcn();
};
class D1 : public Base {
public:
    // 隐藏基类的fcn，这个fcn不是虚函数
    // D1继承了Base::fcn()的定义
    int fcn(int);		// 形参列表与Base中的 fcn 不一致
    virtual void f2();	// 是一个新的虚函数，在 Base 中不存在
};
class D2 : public D1 {
public:
    int fcn(int);		// 是一个非虚函数，隐藏了 DI::fcn(int)
    int fcn();			// 覆盖了 Base的虚函数 fcn
    void f2();			// 覆盖了 D1的虚函数 f2
};

Base bobj; D1 dlobj; D2 d2obj;
Base *bp1 = &bobj, *bp2= &dlobj, *bp3 = &d2obj;
bp1->fcn();		// 虚调用，将在运行时调用 Base::fcn
bp2->fcn();		// 虚调用，将在运行时调用 Base::fcn
bp3->fcn();		// 虚调用，将在运行时调用 D2::fcn

D1 *dlp = &dlobj; D2 *d2p = &d2obj;
bp2->f2();		// 错误:Base没有名为 f2的成员
dlp->f2();		// 虚调用，将在运行时调用 D1::f2()
d2p->f2();		// 虚调用，将在运行时调用 D2::f2()

Base *p1 = &d2obj; D1 *p2 = &d2bj; D2 *p3 = &d2obj;
p1->fcn(42);		// 错误:Base中没有接受一个int的fcn
p2->fcn(42);		// 静态绑定，调用D1::fcn(int)
p3->fcn(42);		// 静态绑定，调用D2::fcn(int)
```



## 构造函数与拷贝控制

### 虚析构函数

通过在基类中将析构函数定义成虚函数以确保执行正确的析构函数版本:

```c++
class Quote {
public:
    // 如果我们删除的是一个指向派生类对象的基类指针，则需要虚析构函数
    virtual ~Quote() = default;		// 动态绑定析构函数
};
```

一个基类总是需要析构函数，而且它能将析构函数设定为虚函数
该析构函数为了成为虚函数而令内容为空，我们显然无法由此推断该基类还需要赋值运算符或拷贝构造函数 

**虚析构函数将阻止合成移动操作**



### 合成拷贝控制与继承

基类或派生类的合成拷贝控制成员的行为与其他合成的构造函数、赋值运算符或析构函数类似:
	它们对类本身的成员依次进行初始化、赋值或销毁的操作。
这些合成的成员还负责使用直接基类中对应的操作对一个对象的直接基类部分进行初始化、赋值或销毁

```c++
class B {
public:
    B();
    B(const B&) = delete;
    // 其他成员，不含有移动构造函数
};
class D : public B {
    // 没有声明任何构造函数
}; 

D d;				// 正确:D的合成默认构造函数使用B的默认构造函数
D d2(d);			// 错误:D的合成拷贝构造函数是被删除的
D d3(std::move(d));	// 错误:隐式地使用D的被删除的拷贝构造函数

//移动操作与继承
class Quote {
public:
    Quote() = default;						// 对成员依次进行默认初始化
    Quote(const Quote&) = default;			// 对成员依次拷贝
    Quote(Quote &&) = default;				// 对成员依次拷贝
    Quote& operator=(const Quote&) = default;	// 拷贝赋值
    Quote& operator=(Quote&&) = default;		// 移动赋值
    virtual ~Ouote() = default;
    // 其他成员与之前的版本一致
};
```

### 派生类的拷贝控制成员

派生类的拷贝和移动构造函数在拷贝和移动自有成员的同时，也要拷贝和移动基类部分的成员
派生类赋值运算符也必须为其基类部分的成员赋值

析构函数只负责销毁派生类自己分配的资源
对象的成员是被隐式销毁的
派生类对象的基类部分也是自动销毁的

```c++
//定义派生类的拷贝或移动构造函数
class Base { /* ... */ };
class D : public Base {
public:
	// 默认情况下，基类的默认构造函数初始化对象的基类部分
    // 要想使用拷贝或移动构造函数，我们必须在构造函数初始值列表中
    // 显式地调用该构造函数
	D(const D& d) : Base(d)			//拷贝基类成员
					/*D的成员的初始值*/ 	{ /* ... */ }
    D(D&& d) : Base(std::move(d))	//移动基类成员
					/*D的成员的初始值*/	{ /* ... */ }
};

//派生类赋值运算符
// Base::operator=(const Base&)不会被自动调用
D &D::operator=(const D &rhs)
{
    Base::operator=(rhs);	// 为基类部分赋值
    // 按照过去的方式为派生类的成员赋值
    // 酌情处理自赋值及释放已有资源等情况
    return *this;
}

//派生类析构函数
class D: public Base {
public:
    // Base::~Base被自动调用执行
    ~D(){ /*该处由用户定义清除派生类成员的操作 */ }
};
```

当我们构建一个对象时，需要把对象的类和构造函数的类看作是同一个；对虚函数的调用绑定正好符合这种把对象的类和构造函数的类看成同一个的要求:对于析构函数也是同样的道理。

如果构造函数或析构函数调用了某个虚函数，则我们应该执行与构造函数或析构函数**所属类型相对应**的虚函数版本。

### 继承的构造函数

一个类只初始化它的直接基类，出于同样的原因，一个类也只继承其直接基类的构造函数
类不能继承默认、拷贝和移动构造函数
如果派生类没有直接定义这些构造函数则编译器将为派生类合成它们

```c++
class Bulkquote : public Disc_quote {
public:
    using Disc_quote::Disc_quote;	// 继承Disc_quote的构造函数
    // Or
    Bulk_quote(const std::string& book, double price,
               std::size_t qty, double disc) : 
    	Disc_quote(book, price, qty, disc) { }
    
    double net_price(std::size_t) const;
}; 
```

对于基类的每个构造函数，编译器都在派生类中生成一个形参列表完全相同的构造函数:

```
derived(parms) : base(args){}
```

一个构造函数的using声明不会改变该构造函数的访问级别
using声明语句不能指定explicit或constexpr
当一个基类构造函数含有默认实参时，这些实参并不会被继承
	派生类将获得多个继承的构造函数，其中每个构造函数分别省略掉一个含有默认实参的形参



## 容器与继承

```c++
vector<Quote> basket;
basket.push_back(Quote("0-201-82470-1", 50));
// 正确:但是只能把对象的Quote部分拷贝给 basket
basket.push_back(Bulk_quote("0-201-54848-8", 50, 10, .25));
// 调用Quote定义的版本，打印750，即15 * $50
cout << basket.back().net_price(15) << endl;

//在容器中放置(智能)指针而非对象
vector<shared_ptr<Quote>> basket;
basket.push_back(make_shared<Quote>("0-201-82470-1", 50));
basket.push_back(make_shared<Bulk_quote>("0-201-54848-8", 50, 10, .25));
// 调用Quote定义的版本;打印562.5，即在15 * $50中扣除掉折扣金额
cout << basket.back()->net_price(15) << endl;
```

### 编写Basket类

```c++
class Basket{
public:
    // Basket 使用合成的默认构造函数和拷贝控制成员
    void add_item(const std::shared_ptr<Quote> &sale)
   		{ items.insert(sale); }
    // 打印每本书的总价和购物篮中所有书的总价
    double total_receipt(std::ostream&) const;
    
    void add_item(const Quote& sale);	// 拷贝给定的对象
    void add_item(Quote&& sale);		// 移动给定的对象
private:
    // 该函数用于比较shared_ptr，multiset 成员会用到它
    static bool compare(const std::shared ptr<Quote> &lhs, 
                        const std::shared ptr<Quote> &rhs) 
    	{ return lhs->isbn() < rhs->isbn(); }
    // multiset保存多个报价，按照compare成员排序
    std::multiset<std::shared_ptr<Quote>, decltype(compare)*> items { compaare };
};

double Basket::total_receipt(ostream &os) const
{
    double sum = 0.0;			// 保存实时计算出的总价格
    // iter指向ISBN相同的一批元素中的第一个
    // upper_bound返回一个迭代器，该迭代器指向这批元素的尾后位置
    for (auto iter = items.cbegin(); 
         iter != items.cend(); 
         iter = items.upper_bound(*iter)) {
        // 我们知道在当前的 Basket 中至少有一个该关键字的元素
        // 打印该书籍对应的项目
        sum += print_total(os, **iter, items.count(*iter));
    }
    os << "Total Sale: " << sum << endl;	 // 打印最终的总价格
    return sum;
}
```



# 模板与泛型编程

一个模板就是一个创建类或函数的蓝图

## 定义模板

### 函数模板

```c++
template <typename T>
int compare(const T &v1, const T &v2)
{
    if (v1 < v2) return -1;
    if (v2 < v1) return 1;
    return 0;
}
//实例化函数模板
// 编译器(通常)用函数实参来为我们推断模板实参
cout << compare(1, 0) << endl; // T为int

//模板类型参数
//可以将类型参数看作类型说明符，就像内置类型或类类型说明符一样使用
// 正确:返回类型和参数类型相同
template <typename T>T foo(T* p)
{
    T tmp = *p;		// tmp的类型将是指针p指向的类型
    // ...
    return tmp;
}
//类型参数前必须使用关键字class或typename
// 错误:U之前必须加上class或typename
template <typename T, U> T calc(const T&, const U&);
// 正确:在模板参数列表中，typename和class没有什么不同
template <typename T, class u> calc (const T&, const U&);

//非类型模板参数
// 非类型参数表示一个值而非一个类型
// 非类型模板参数的模板实参必须是常量表达式
template<unsigned N, unsigned M>
int compare(const char (ap1)[N], const char (&p2)[M])
{
    return strcmp(p1, p2);
}
compare("hi", "mom");	// int compare(const char (&p1)[3], const char (&p2)[4])

//inline和constexpr的函数模板
// 正确:inline说明符跟在模板参数列表之后
template <typename T> inline Tmin(const T&, const T&);
// 错误:inline说明符的位置不正确
inline template<typename T> Tmin(const T&, const T&);

//编写类型无关的代码
// 即使用于指针也正确的compare版本
template <typename T>int compare(const T &vl， const T &v2)
{
    if (less<T>()(v1, v2)) return -1;
    if (less<T>()(v2, v1)) return 1;
    return 0;
}
```

**模板编译**
当编译器遇到一个模板定义时，它并不生成代码。
只有当实例化出模板的一个特定版本时，编译器才会生成代码。

函数模板和类模板成员函数的定义通常放在头文件中

大多数编译错误在实例化期间报告



### 类模板

类模板(class template)是用来生成类的蓝图的
为了使用类模板，必须在模板名后的尖括号中提供额外信息用来代替模板参数的模板实参列表

```c++
//定义类模板
template <typename T>
class Blob{
public:
    typedef T value_type;
    typedef typename std::vector<T>::size_type size_type;
    // 构造函数
    Blob();
    Blob(std::initializer_list<T> il);
    // Blob中的元素数目
    size_type size() const { return data->size(); }
    bool empty() const{ return data->empty(); }
    // 添加和删除元素
    void push_back(const T &t) {data->push_back(t);}
    // 移动版本
    void push_back(T &&t) {data->push_back(std::move(t));} 
    void pop_back();
    // 元素访问
    T& back();
    T& operator[](size_type i);
private:
    std::shared_ptr<std::vector<T>> data;
    // 若data[i]无效，则抛出msg
    void check(size_type i, const std::string &msg) const;
};
template<typename T>
Blob<T>::Blob(): data(std::make_shared<std::vector<T>>()) { }
                                                          
template <typename T>
void Blob<T>::check(size_type i, const std::string &msg) const
{
    if(i >= data->size())
        throw std::out_of_range(msg);
}

template <typename T>
T& Blob<T>::back()
{
    check(0, "back onempty Blob");
    return data->back();
}

template <typename T>
T& Blob<T>::operator[](size_type i)
{
    // 如果i太大，check会抛出异常，阻止访问一个不存在的元素
    check(i, "subscript out of range");
    return (*data)[i];
}

template <typename T>
void Blob<T>::pop_back()
{
    check(0, "pop back on empty Blob");
    data->pop_back();
}

template<typename T>
Blob<T>::Blob(std::initializer_list<T> il) : 
	data(std::make_shared<std::vector<T>>(il)) { }

//实例化类模板
Blob<int> ia;						// 空Blob<int>
Blob<int> ia2 = {0, 1, 2, 3, 4};	// 有5个元素的Blob<int>
//下面的定义实例化出两个不同的 Blob类型
Blob<string> names;	// 保存string的Blob
Blob<double> prices;// 不同的元素类型

// 实例化Blob<int>和接受initializer_list<int>的构造函数
Blob<int> squares = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
// 实例化Blob<int>::size() const
for (size_t i = 0; i != squares.size(); ++i)
    squares[i] = i * i;	// 实例化Blob<int>::operator[](size_t)
```

**在类代码内简化模板类名的使用**

```c++
//若试图访问一个不存在的元素，BlobPtr 抛出一个异常
template <typename T> class BlobPtr {
public:
    BlobPtr() : curr(0) {}
    BlobPtr(Blob<T> &a, size_t sz = 0) : 
    	wptr(a.data), curr(sz) { }
    T& operator*() const
    { 
        auto p = check(curr, "dereference past end");
        return (*p)[curr];	// (*p)为本对象指向的vector
    }
    BlobPtr& operator++();	// 前置运算符
    BlobPtr& operator--();
private:
    // 若检查成功，check返回一个指向vector的shared_ptr
    std::shared_ptr<std::vector<T>>
        check(std::size_t, const std::string&) const;
    // 保存一个weak_ptr，表示底层vector可能被销毁
    std::weak_ptr<std::vector<T>> wptr;
    std::size_t curr;		//数组中的当前位置
};

// 后置:递增/递减对象但返回原值
template<typename T>
BlobPtr<T> BlobPtr<T>::operator++(int)
{
    // 此处无须检查:调用前置递增时会进行检查
    BlobPtr ret = *this;	// 保存当前值 
    ++*this;				// 推进一个元素;前置++检查递增是否合法
    return ret;				// 返回保存的状态
}
```

**类模板和友元**

```c++
//前置声明，在 Blob中声明友元所需要的
template <typename> class BlobPtr;
template <typename> class Blob;//运算符==中的参数所需要的
template <typename T>
	bool operator==(const Blob<T>&, const Blob<T>&);

template <typename> class Blob {
    // 每个Blob 实例将访问权限授予用相同类型实例化的 BlobPtr 和相等运算符
    friend class BlobPtr<T>;
    friend bool operator==<T>
        (const Blob<T>&, const Blob<T>&);
};

Blob<char> ca;	// BlobPtr<char>和operator==<char>都是本对象的友元
Blob<int> ia;	// BlobPtr<int>和operator==<int>都是本对象的友元
```

**通用和特定的模板友好关系**
一个类也可以将另一个模板的每个实例都声明为自己的友元，或者限定特定的实例为友元:

```c++
//前置声明，在将模板的一个特定实例声明为友元时要用到
template <typename T> class Pal;

class C {	// C是一个普通的非模板类
    friend class Pal<C>;		// 用类C实例化的Pal是C的一个友元
	// Pa12的所有实例都是C的友元:这种情况无须前置声明
    template <typename T> friend class Pal2;
};
template <typename T> class C2 {	// C2本身是一个类模板
    // C2的每个实例将相同实例化的 Pal声明为友元
    friend class Pal<T>;	// Pal的模板声明必须在作用域之内
    // Pal2的所有实例都是C2的每个实例的友元，不需要前置声明
    template <typename X> friend class Pal2;
    // Pal3是一个非模板类，它是C2所有实例的友元
    friend class Pal3;	// 不需要Pal3的前置声明
};
```

**令模板自己的类型参数成为友元**

```c++
template<typename Type>
class Bar{
    friend Type;	// 将访问权限授予用来实例化Bar的类型
	//..
};
```

**模板类型别名**

```c++
typedef Blob<string> StrBlob;
// 由于模板不是一个类型，不能定义一个typedef引用一个模板。即，无法定义一个typedef引用Blob<T>
template<typename T>using twin = pair<T, T>;
twin<string> authors;			// authors是一个pair<string, string>
twin<int> win_loss;				// win_loss是一个pair<int, int>
twin<double> area;				// area是一个pair<double, double>

template <typename T> using partNo = pair<T, unsigned>;
partNo<string> books;	// books是一个pair<string，unsigned>
partNo<Vehicle> cars;	// cars是一个pair<Vehicle，unsigned>
partNo<Student> kids;	// kids是一个pair<Student，unsigned>
```

**类模板的static成员**

```c++
template <typename T> 
class Foo {
public:
    static std::size_t count(){ return ctr; }	//其他接口成员
private:
    static std::size_t ctr;
    //其他实现成员
};
template<typename T>
size_t Foo<T>::ctr = 0;	//定义并初始化ctr

//实例化static成员Foo<string>::ctr和Eoo<string>::count
Foo<string> fs;
//所有三个对象共享相同的Foo<int>::ctr和Foo<int>::count 成员
Foo<int> fi, fi2, fi3;

Foo<int> fi;						// 实例化Eoo<int>类和static数据成员ctr
auto ct = Foo<int>::count(); 		// 实例化Foo<int>::count
ct = fi.count();					// 使用Foo<int>::count
ct = Foo::count();					// 错误:使用哪个模板实例的 count?
```

### 模板参数

```c++
template <typename Foo>
Foo calc(const Foo& a, const Foo& b)
{
    Foo tmp = a;	// tmp的类型与参数和返回类型一样
    // ..
    return tmp;		// 返回类型和参数类型一样
}
```

**模板参数与作用域**

```c++
typedef double A;
template <typename A, typename B>
void f(A a, B b)
{
    A tmp = a;		// tmp的类型为模板参数A的类型，而非double
    double B;		// 错误:重声明模板参数B
}
//错误:非法重用模板参数名 V
template <typename V, typename V>
```

**模板声明**

```c++
//声明但不定义compare和Blob
template <typename T> int compare(const T&, const T&);
template <typename T> class Blob;

//3个calc都指向相同的函数模板
template <typename T> T calc(const T&, const T&);//声明
template <typename U> U calc(const U&, const U&);//声明
//模板的定义
template<typename Type>
Type calc(const Type& a, const Type& b) { /*...*/ }
```

默认情况下，C++语言假定通过作用域运算符访问的名字**不是类型**
如果希望使用一个模板类型参数的类型成员，就必须显式告诉编译器该名字是一个类型
通过使用关键字typename来实现这一点:

```c++
// top函数期待一个容器类型的实参，它使用typename指明其返回类型并在c中没有元素时生成一个值初始化的元素返给调用者
template<typename T>
typename T::value_type top(const T& c)
{
    if (!c.empty())
    	return c.back();
    else
    	return typename T::value_type();
}
```

当我们希望通知编译器一个名字表示类型时，必须使用关键字 typename，而不能使用 class

**默认模板实参**

```c++
// compare 有一个默认模板实参less<T>和一个默认函数实参F()
template <typename T, typename F = less<T>>
int compare(const T &v1, const T &v2, F f = F())
{
	if (f(v1, v2)) return -1;
    if (f(v2, v1)) return 1;
    return 0;
}
// 在这段代码中，为模板添加了第二个类型参数，名为 F，表示可调用对象的类型
// 并定义了一个新的函数参数，绑定到一个可调用对象上

bool i = compare(0, 42);	//使用less;i为-1
// 结果依赖于item1和item2中的isbn
Sales_data item1(cin), item2(cin);
// 模板参数的类型从它们对应的函数实参推断而来
// 在此调用中，T的类型被推断为Sales_data，F被推断为compareIsbn的类型
bool j = compare(item1, item2, compareIsbn);
```

**模板默认实参与类模板**
如果一个类模板为其所有模板参数都提供了默认实参，且我们希望使用这些默认实参，就必须在模板名之后跟一个空尖括号对:

```c++
template <class T = int>
class Numbers {
public:
    Numbers(T v = 0): val(v) { }
    // 对数值的各种操作
private:
    T val;
}; // 默认为int
Numbers<long double> lots_of_precision;
Numbers<> average_precision;		// 空<>表示我们希望使用默认类型
```

### 成员模板

一个类(无论是普通类还是类模板)可以包含本身是模板的成员函数。这种成员被称为成员模板(member template)。成员模板不能是虚函数。

**普通(非模板)类的成员模板**

```c++
// 函数对象类，对给定指针执行delete
class DebugDelete {
public:
    DebugDelete(std::ostream &s = std::cerr): os(s) { }
    // 与任何函数模板相同，T 的类型由编译器推断
    template <typename T> void operator()(T *p) const {
        os << "deleting unique_ptr" << std::endl;	delete p;
    }
private:
    std::ostream &os;
};

double* p = new double;
DebugDelete d;	// 可像delete表达式一样使用的对象
d(p);			// 调用DebugDelete::operator()(double*)，释放p
int* ip = new int;
// 在一个临时DebugDelete对象上调用operator()(int*)
DebugDelete()(ip);

// 销毁p指向的对象
// 实例化DebugDelete::operator()<int>(int *)
unique_ptr<int, DebugDelete> p(new int, DebugDelete());
// 销毁sp指向的对象
// 实例化DebugDelete::operator()<string>(string*)
unique_ptr<string, DebugDelete> sp(new string, DebugDelete());
// DebugDelete的成员模板实例化样例
void DebugDelete::operator()(int *p) const { delete p; }
void DebugDelete::operator()(string *p) const { delete p; }
```

**类模板的成员模板**

```c++
template <typename T>
class Blob {
    template <typename It> Blob(It b, It e);
    //...
};

template <typename T>		// 类的类型参数
template <typename It>		// 构造函数的类型参数
Blob<T>::Blob(It b, It e) :
	data(std::make_shared<std::vector<T>>(b, e)) { }

//实例化与成员模板
int ia[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
vector<long> vi = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
list<const char*> w = {"now", "is", "the", "time"};
// 实例化Blob<int>类及其接受两个int*参数的构造函数
Blob<int> a1(begin(ia), end(ia));
//实例化Blob<int>类的接受两个vector<long>::iterator的构造函数
Blob<int> a2(vi.begin(), vi.end());
// 实例化Blob<string>及其接受两个list<const char*>::iterator参数的构造函数
Blob<string> a3(w.begin(), w.end());
```



### 控制实例化

当模板被使用时才会进行实例化这一特性意味着，相同的实例可能出现在多个对象文件中
	当两个或多个独立编译的源文件使用了相同的模板
	并提供了相同的模板参数时，每个文件中就都会有该模板的一个实例

通过显式实例化(explicit instantiation)来避免这种开销

```c++
extern template declaration;	// 实例化声明
template declaration;			// 实例化定义

//实例化声明与定义
// 可能有多个extern声明，但必须只有一个定义
extern template class Blob<string>;	// 声明
template int compare(const int&, const int&);		// 定义

// Application.cc
// 这些模板类型必须在程序其他位置进行实例化
extern template class Blob<string>;
extern template int compare(const int&, const int&);
Blob<string> sal, sa2;	// 实例化会出现在其他位置
// Blob<int>及其接受initializer_list的构造函数在本文件中实例化
Blob<int> a1 = {0, 1,2, 3, 4, 5, 6, 7, 8, 9};	
Blob<int> a2(al);	// 拷贝构造函数在本文件中实例化
int i = compare(a1[0], a2[0]);	// 实例化出现在其他位

// templateBuild.cc
// 实例化文件必须为每个在其他文件中声明为extern的类型和函数提供一个(非extern)的定义
template int compare(const int&, const int&);
template class Blob<string>;	// 实例化类模板的所有成员
```

在一个类模板的实例化定义中，所用类型必须能用于模板的所有成员函数



### 效率与灵活性

**在运行时绑定删除器**
在一个 shared_ptr 的生存期中，可以随时改变其删除器的类型
可以使用一种类型的删除器构造一个shared_ptr，随后使用reset赋予此shared_ptr另一种类型的删除器

**假定**shared_ptr将它管理的指针保存在一个成员p中，且删除器是通过一个名为del的成员来访问的，则shared_ptr的析构函数必须包含类似下面这样的语句:

```c++
// del的值只有在运行时才知道;通过一个指针来调用它
del ? del(p) : delete p;	// del(p)需要运行时跳转到del的地址
```

**在编译时绑定删除器**
由于删除器的类型是 unique_ptr 类型的一部分，因此删除器成员的类型在编译时是知道的，从而删除器可以直接保存在unique_ptr对象中

```c++
// del在编译时绑定;直接调用实例化的删除器
del(p);		// 无运行时额外开销
```



## 模板实参推断

从函数实参来确定模板实参的过程被称为模板实参推断(template argument deduction)

### 类型转换与模板类型参数

顶层 const 无论是在形参中还是在实参中都会被忽略
const 转换：可以将一个非 const 对象的引用(或指针)传递给一个 const 的引用(或指针)形参
数组或函数指针转换：如果函数形参不是引用类型，则可以对数组或函数类型的实参应用正常的指针转换
	一个数组实参可以转换为一个指向其首元素的指针
	一个函数实参可以转换为一个该函数类型的指针

```c++
template<typename T> Tfobj(T, T);					// 实参被拷贝
template <typename T> T fref(const T&, const T&);	// 引用
string s1("a value");
const string s2("another value");
fobj(s1, s2);		// 调用 fobj(string，string);const 被忽略
fref(s1, s2);		// 调用 fref(const string&, const string&)
					// 将s1转换为const是允许的
int a[10]，b[42];
fobj(a, b);			// 调用f(int*，int*)
fref(a, b);			// 错误:数组类型不匹配
```

**使用相同模板参数类型的函数形参**

```c++
long lng;
compare(lng, 1024);	// 错误:不能实例化compare(long, int)
```

```c++
// 实参类型可以不同，但必须兼容
template <typename A, typename B>
int flexibleCompare(const A& vl, const B& v2)
{
    if (v1 < v2) return -1;
    if (v2 < v1) return 1;
    return 0;
}

long lng;
flexibleCompare(lng, 1024);// 正确:调用flexibleCompare(long, int)
```

**正常类型转换应用于普通函数实参**
如果函数参数类型不是模板参数，则对实参进行正常的类型转换

```c++
template <typename T>
ostream &print(ostream &os, const T &obj)
{
    return os << obj;
}
print(cout, 42);		// 实例化print(ostream&, int)
ofstream f("output");
print(f, 10);			// 使用print(ostream&, int);将f转换为ostream&
```

### 函数模板显式实参

在某些情况下，编译器无法推断出模板实参的类型
其他一些情况下，希望允许用户控制模板实例化

**指定显式模板实参**

```c++
// 编译器无法推断T1，它未出现在函数参数列表中
template <typename T1, typename T2, typename T3>
T1 sum(T2, T3);
// T1是显式指定的，T2和T3是从函数实参类型推断而来的
auto val3 = sum<long long>(i, lng);		// long long sum(int, long)

// 糟糕的设计:用户必须指定所有三个模板参数
template <typename T1, typename T2, typename T3>
T3 alternative_sum(T2, T1);

// 错误:不能推断前几个模板参数
auto val3 = alternative_sum<long long>(i, lng);
// 正确:显式指定了所有三个参数
auto val2 = alternative_sum<long long, int, long>(i, lng);
```

**正常类型转换应用于显式指定的实参**

```c++
long lng;
compare(lng, 1024);				// 错误:模板参数不匹配
compare<long>(lng, 1024);		// 正确:实例化compare(long, long)
compare<int>(lng, 1024);		// 正确:实例化compare(int, int)
```

### 尾置返回类型与类型转换

编写一个函数，接受表示序列的一对迭代器和返回序列中一个元素的引用:

```c++
template <typename It>
??? &fcn(It beg, It end)
{
    // 处理序列
	return *beg;	// 返回序列中一个元素的引用
}

vector<int> vi = {1, 2, 3, 4, 5};
Blob<string> ca = {"hi", "bye"};
auto &i = fcn(vi.begin(), vi.end());	// fcn应该返回int&
auto &s = fcn(ca.begin(), ca.end());	// fcn应该返回string&

//尾置返回允许我们在参数列表之后声明返回类型
template <typename It>
auto fcn(It beg, It end) -> decltype(*beg)
{
    // 处理序列
    return *beg;	// 返回序列中一个元素的引用
}

```



**进行类型转换的标准库模板类**
希望编写一个类似 fcn 的函数，但返回一个元素的值而非引用
获得元素类型，可以使用标准库的类型转换(type transformation)模板

`remove_reference<decltype(*beg)>::type`

```c++
//为了使用模板参数的成员，必须用 typename
template <typename It>
auto fcn2(It beg, It end) ->
	typename remove_reference<decltype(*beg)>::type
{
    // 处理序列
	return *beg;		// 返回序列中一个元素的拷贝
}
```

|                      | 标准类型转换模板            |                   |
| -------------------- | --------------------------- | ----------------- |
| 对Mod<T>，其中Mod为  | 若T为                       | 则Mod<T>::type为  |
| remove_reference     | X& 或 X&&<br />否则         | X<br />T          |
| add_const            | X&、const X或函数<br />否则 | T<br />const T    |
| add_lvalue_reference | X&<br />X&&<br />否则       | T<br />X&<br />T& |
| add_rvalue_reference | X&或X&&<br />否则           | T<br />T&&        |
| remove_pointer       | X*<br />否则                | X<br />T          |
| add_pointer          | X&或X&&<br />否则           | X*<br />`T*`      |
| make_signed          | unsigned X<br />否则        | X<br />T          |
| make_unsigned        | 带符号类型<br />否则        | unsigend X<br />T |
| remove_extent        | X[n]<br />否则              | X<br />T          |
| remove_all_extents   | `X[n1][n2]...`<br />否则    | X<br />T          |

例如，如果是一个指针类型，则remove_pointer<T>::type是T指向的类型
如果T不是一个指针，则无须进行任何转换，从而 type 具有与T相同的类型

### 函数指针和实参推断

```c++
//函数指针
template <typename T> int compare(const T&, const T&);
// pf1指向实例int compare(const int&, const int&)
int (*pf1)(const int&, const int&) = compare;

//实参推断
// func的重载版本;每个版本接受一个不同的函数指针类型
void func(int(*)(const string&, const string&));
void func(int(*)(const int&, const int&));
func(compare);		// 错误:使用compare的哪个实例?
// 正确:显式指出实例化哪个compare版本
func(compare<int>);		// 传递compare(const int&, const int&)
```



### 模板实参推断和引用

```c++
template <typename T> void f(T &p);
```

**从左值引用函数参数推断类型**
当一个函数参数是模板类型参数的一个普通(左值)引用时(即，形如T&)
	只能传递给它一个左值(如，一个变量或一个返回引用类型的表达式)

实参可以是 const类型，也可以不是，如果实参是 const 的，则T将被推断为 const 类型

```c++
template <typename T> void f1(T&);		// 实参必须是一个左值
//对f1的调用使用实参所引用的类型作为模板参数类型
f1(i);		// i是一个int;模板参数类型T是int
f1(ci); 	// ci是一个const int;模板参数T是const int
f1(5);		// 错误:传递给一个&参数的实参必须是一个左值

template <typename T> void f2(const T&);	// 可以接受一个右值
// f2中的参数是const &;实参中的const是无关的
// 在每个调用中，f2的函数参数都被推断为const int&
f2(i);	// i是一个int;模板参数T是int
f2(ci);	// ci是一个const int，但模板参数T是int
f2(5);	// 一个const &参数可以绑定到一个右值;T是int
```

**从右值引用函数参数推断类型**

```c++
template <typename T> void f3(T&&);
f3(42);			// 实参是一个int 类型的右值;模板参数T是int
```

**引用折叠和右值引用参数**
通常我们不能将一个右值引用绑定到一个左值上
但是，C++语言在正常绑定规则之外定义了两个例外规则，允许这种绑定

	1. 将一个左值(如 i)传递给函数的右值引用参数，且此右值引用指向模板类型参数(如 T&&)时
	编译器推断模板类型参数为实参的左值引用类型
		因此，当我们调用f3(i)时，编译器推断T的类型为int&，而非int
	1. 如果间接创建一个引用的引用，则这些引用形成了“折叠”。
	在所有情况下(除了一个例外)，引用会折叠成一个普通的左值引用类型。
	在新标准中，折叠规则扩展到右值引用
		X& &、X& &&和X&& &都折叠成类型X&
		例外：类型X&& &&折叠成 X&&

​	**引用折叠只能应用于间接创建的引用的引用，如类型别名或模板参数**

```c++
f3(i);	// 实参是一个左值;模板参数T是int&
f3(ci); // 实参是一个左值;模板参数是一个const int&

// 无效代码，只是用于演示目的
void f3<int&>(int& &&);	// 当T是int&时，函数参数为int& &&
// To
void f3<int&>(int&);	// 当T是int&时，函数参数折叠为int&
```

- 如果一个函数参数是指向模板参数类型的右值引用(如，T&&，则可以传递给它任意类型的实参
- 如果将一个左值传递给这样的参数，则函数参数被实例化为一个普通的左值引用 (T&)

**编写接受右值引用参数的模板函数**
右值引用通常用于两种情况:模板转发其实参或模板被重载

```c++
template <typename T>
void f3(T&& val)
{
    T t = val;		// 拷贝还是绑定一个引用?
    t = fcn(t);		// 赋值只改变t还是既改变t又改变val?
	if (val == t){ /* */ }	// 若T是引用类型，则一直为 true
}

template <typename T> void f(T&&);			// 绑定到非const右值
template <typename T> void f(const T&); 	// 左值和const右值
```



### 理解std::move

**std::move 是如何定义的**

```c++
// 在返回类型和类型转换中也要用到 typename
template <typename T>
typename remove_reference<T>::type&& move(T&& t)
{
    return static_cast<typename remove_reference<T>::type&&>(t);
}
string sl("hi!"), s2;
s2 = std::move(string("bye!"));	// 正确:从一个右值移动数据
s2 = std::move(s1);				// 正确:但在赋值之后，s1的值是不确定的
```

**std::move是如何工作的**

```c++
s2 = std::move(string("bye!"));	// 正确:从一个右值移动数据
// - 推断出的T的类型为string
// - 因此，remove_reference用 string 进行实例化
// - remove_reference<string>的type成员是 string
// - move的返回类型是string&&
// - move的函数参数t的类型为string&&
// Equal
string&& move(string &&t)
```

```c++
s2 = std::move(s1);				// 正确:但在赋值之后，s1的值是不确定的
// - 推断出的T的类型为 string& (string 的引用，而非普通string)
// - 因此，remove_reference用string&进行实例化
// - remove_reference<string&>的type成员是string
// - move的返回类型仍是string&&
// - move的函数参数t实例化为string&&&，会折叠为string&
// Equaal
string&& move(string &t);
// 这个实例的函数体返回static_cast<string&&>(t)
// 在此情况下，t 的类型为 string&，cast将其转换为string&&。
```

**从一个左值static_cast到一个右值引用是允许的**



### 转发

某些函数需要将其一个或多个实参连同类型不变地转发给其他函数
	在此情况下，需要保持被转发实参的所有性质，包括实参类型是否是 const 的以及实参是左值还是右值

```c++
// 接受一个可调用对象和另外两个参数的模板
// 对“翻转”的参数调用给定的可调用对象
// flip1是一个不完整的实现:顶层const 和引用丢失了
template <typename F, typename T1, typename T2>
void flip1(F f, T1 tl, T2 t2)
{
    f(t2, t1);
}
// 希望用它调用一个接受引用参数的函数时就会出现问题
void f(int v1, int &v2) //注意v2是一个引用
{
    cout << v1 << " " << ++v2 << endl;
}
f(42, i);			// f改变了实参i
// void flip1(void(*fcn)(int, int&), int t1, int t2);
flip1(f, j, 42);	// 通过flip1调用f不会改变j
```

**定义能保持类型信息的函数参数**

```c++
template <typename F, typename T1, typename T2>
void flip2(F f, T1 &&tl, T2 &&t2)
{
    f(t2, t1);
}
```

这个版本的 flp2解决了一半问题。它对于接受一个左值引用的函数工作得很好，但不能用于接受右值引用参数的函数。例如:

```c++
void g(int &&i, int& j)
{
    cout << i <<  " " << j << endl;
}
flip2(g, i, 42);		// 错误:不能从一个左值实例化int&&
```

**在调用中使用std::forward保持类型信息**

forward返回该显式实参类型的右值引用。即，forward<T>的返回类型是 T&&。

通过其返回类型上的引用折叠，forward可以保持给定实参的左值/右值属性:

```c++
template <typename Type> intermediary(Type &&arg)
{
    finalFcn(std::forward<Type>(arg));
    // ...
}
```

当用于一个指向模板参数类型的右值引用函数参数(T&&)时，forward会保持实参类型的所有细节。

```c++
template <typename F, typename T1, typename T2>
void flip(F f, T1 &&t1, T2 &&t2)
{
    f(std::forward<T2>(t2), std::forward<T1>(t1));
}
```



## 重载与模板

### 编写重载模板

```c++
// 打印任何我们不能处理的类型
template <typename T> string debug_rep(const T &t)
{
    ostringstream ret;
    ret << t;	// 使用T的输出运算符打印七的一个表示形式
    return ret.str();	// 返回ret绑定的string的一个副本
}

// 打印指针的值，后跟指针指向的对象
// 注意:此函数不能用于char*
template <typename T> string debug_rep(T *p)
{
    ostringstream ret;
    ret << "pointer:" << p;	// 打印指针本身的值
    if(p)
        ret << " " << debug_rep(*p);	// 打印p指向的值
    else
        ret << "null pointer"; 	// 或指出p为空
    return ret.str();		// 返回ret绑定的string的一个副本
}

// 只有第一个版本的 debug rep 是可行的
// 第二个 debug_rep 版本要求一个指针参数，但在此调用中我们传递的是一个非指针对象
string s("hi");
cout << debug_rep(s) << endl;
// 第二个版本的 debug rep 的实例是此调用的精确匹配
// 第一个版本的实例需要进行普通指针到 const 指针的转换。
cout << debug rep(&s) << endl;

// 根据重载函数模板的特殊规则，此调用被解析为debug_rep(T*)，即，更特例化的版本。
const string *sp = &s;
cout << debug_rep(sp) << endl;
```

**非模板和模板重载**

```c++
// 打印双引号包围的string
string debug_rep(const string &s)
{
    return '"' + s + '"';
}
string s("hi");
cout << debug_rep(s) << endl;
// 当存在多个同样好的函数模板时，编译器选择最特例化的版本，编译器会选择非模板版本
```

**重载模板和类型转换**

```c++
cout << debug_rep("hi world!") << endl;	// 调用debug_rep(T*)
// 对给定实参来说，两个模板都提供精确匹配
// 第二个模板需要进行一次(许可的)数组到指针的转换，而对于函数匹配来说，这种转换被认为是精确匹配
// 非模板版本是可行的，但需要进行一次用户定义的类型转换，因此它没有精确匹配那么好
// 所以两个模板成为可能调用的函数
// 与之前一样，T*版本更加特例化，编译器会选择它

// 如果我们希望将字符指针按string 处理，可以定义另外两个非模板重载版本
// 将字符指针转换为 string，并调用string 版本的debug_rep
string debug_rep(char *p)
{
    return debug_rep(string(p));
}
string debug_rep(const char *p)
{
    return debug_rep(string(p));
}
```

当有多个重载模板对一个调用提供同样好的匹配时，应选择最特例化的版本
对于一个调用，如果一个非函数模板与一个函数模板提供同样好的匹配，则选择非模板版本
在定义任何函数之前，记得声明所有重载的函数版本
	这样就不必担心编译器由于未遇到希望调用的函数而实例化一个并非你所需的版本



## 可变参数模板

存在两种参数包:
	模板参数包template parameter packet)，表示零个或多个模板参数
	函数参数包(function parameter packet)，表示零个或多个函数参数

用一个省略号来指出一个模板参数或函数参数表示一个包

```c++
// Args是一个模板参数包;rest 是一个函数参数包
// Args表示零个或多个模板类型参数
// rest表示零个或多个函数参数
template <typename T, typename... Args>
void foo(const T&t, const Args& ... rest);

int i = 0; double d = 3.14; string s = "how now brown cow";
foo(i, s, 42, d);		// 包中有三个参数
foo(s, 42, "hi");		// 包中有两个参数
foo(d, s);				// 包中有一个参数
foo("hi");				// 空包
// 分别调用
void foo(const int&, const string&, const int&, const double&);
void foo(const string&, const int&, const char[3]&);
void foo(const double&, const string&);
void foo(const char[3]&);

//获取包中元素数目
// 不会对其实参求值
template<typename ... Args>
void g(Args ... args)
{
    cout << sizeof...(Args) << endl;	// 类型参数的数目
    cout << sizeof...(args) << endl;	// 函数参数的数目
}
```



### 编写可变参数函数模板

 可变参数函数通常是递归的
	第一步调用处理包中的第一个实参，然后用剩余实参调用自身
	为了终止递归，我们还需要定义一个非可变参数的函数

```c++
// 用来终止递归并打印最后一个元素的函数
// 此函数必须在可变参数版本的 print 定义之前声明
template<typename T>
ostream &print(ostream &os, const T &t)
{
    return os << t;		// 包中最后一个元素之后不打印分隔符
}
// 包中除了最后一个元素之外的其他元素都会调用这个版本的 print
template <typename T, typename... Args>
ostream &print(ostream &os, const T t, const Args&... rest)
{
    os << t << ", ";				// 打印第一个实参
    return print(os, rest...);		// 递归调用，打印其他实参
}
```

![](.\Picture\可变参数调用.png)



### 包扩展

对于一个参数包，除了获取其大小外，能对它做的唯一的事情就是扩展（expand）它。

扩展一个包就是将它分解为构成的元素，对每个元素应用模式，获得扩展后的列表
	通过在模式右边放一个省略号 (...)来触发扩展操作

```c++
template <typename T, typename... Args>
ostream& print(ostream &os, const T &t, const Args&...rest)	// 扩展Args
{
	os << t << ", ";
    return print(os, rest...);		// 扩展rest
}

// example
// ostream& print(ostream&, const int&, const string&, const int&);
print(cout, i, s, 42);		// 包中有两个参数
```

**理解包扩展**

```c++
//编写第二个可变参数函数，对其每个实参调用 debug_rep，然后调用print打印结果string
// 在print调用中对每个实参调用 debug_rep
template <typename... Args>
ostream &errorMsg(ostream &os, const Args&... rest)
{
    // print(os, debug_rep(a1), debug_rep(a2), ...debug_rep(an)
    return print(os, debug_rep(rest)...);
}

// print(cerr, debug_rep(fcnName), debug_rep(code.num()), 
//		debug_rep(otherData), debug_rep("otherData"), debug_rep(item));
errorMsg(cerr, fcnName, code.num(), otherData, "other", item);

// 将包传递给debug_rep;	print(os, debug_rep(a1, a2, ..., an))
// print(cerr, debug_rep(fcnName, code.num(), otherData, "otherData", item));
print(os, debug_rep(rest...));	// 错误:此调用无匹配函数
```



### 转发参数包

- 为了保持实参中的类型信息，必须将emplace_back 的函数参数定义为模板类型参数的右值引用
- 当emplace_back将这些实参传递给 construct 时，我们必须使用forward来保持实参的原始类型

```c++
class StrVec {
public:
    template <class... Args> void emplace_back(Args&&...);
};

template<class...Args>
inline void StrVec::emplace_back(Args&&... args)
{
    chk_n_alloc();	// 如果需要的话重新分配StrVec内存空间
    alloc.construct(first_free++, std::forward<Args>(args)...);
}

StrVec svec;
// StrVec::emplace_back(std::forward<int>(10), std::forward<char>(c))
svec.emplace back(10, 'c');		// 将cccccccccc添加为新的尾元素
```



## 模板特例化

当不能(或不希望)使用模板版本时，可以定义类或函数模板的个特例化版本。

```c++
// 第一个版本;可以比较任意两个类型
template <typename T>
int compare(const T&, const T&);
// 第二个版本处理字符串字面常量
template<size_t N, size_t M>
int compare(const char (&)[N], const char (&)[M]);

const char *pl = "hi", *p2 = "mom";
compare(p1, p2);		// 调用第一个模板
compare("hi", "mom");	// 调用有两个非类型参数的版本
```

**定义函数模板特例化**
使用关键字 template 后跟一个空尖括号对(<>)。空尖括号指出我们将为原模板的所有模板参数提供实参:

```c++
// compare的特殊版本，处理字符数组的指针
template<>
int compare(const char* const &p1, const char* const &p2)
{
    return strcmp(p1, p2);
}
// 当定义一个特例化版本时，函数参数类型必须与一个先前声明的模板中对应的类型匹配
// 希望定义此函数的一个特例化版本，其中为const char*。
```

**函数重载与模板特例化**
一个特例化版本本质上是一个实例，而非函数名的一个重载版本
一个非模板函数提供与函数模板同样好的匹配时，编译器会选择非模板版本

**类模板特例化**

```c++
// 将为标准库hash模板定义一个特例化版本，可以用它来将 Sales_data 对象保存在无序容器中
// 打开std命名空间，以便特例化 std::hash
namespace std {
template<>		// 正在定义一个特例化版本，模板参数为Sales_data
struct hash<Sales_data>
{
    // 用来散列一个无序容器的类型必须要定义下列类型
    typedef size_t result_type;
    typedef Sales_data argument_type;	// 默认情况下，此类型需要== 
    size_t operator()(const Sales_data& s) const;
    // 我们的类使用合成的拷贝控制成员和默认构造函数
};
size_t hash<Sales_data>::operator()(const Sales_data& s) const
{
    return hash<string>()(s.bookNo) ^
        hash<unsigned>()(s.units_sold) ^
         hash<double>()(s.revenue);
} 
}// 关闭std命名空间;注意:右花括号之后没有分号

template <class T> class std::hash;// 友元声明所需要的
class Sales_data {
	friend class std::hash<Sales_data>;
    // 其他成员定义，如前
};
```



**类模板部分特例化**
一个类模板的部分特例化(partial specialization)本身是一个模板
	使用它时用户还必须为那些在特例化版本中未指定的模板参数提供实参

只能部分特例化类模板，而不能部分特例化函数模板。

```c++
// 原始的、最通用的版本
template <class T> struct remove_reference {
    typedef T type;
}; 
// 部分特例化版本，将用于左值引用和右值引用
template <class T> struct remove_reference<T&> //左值引用
	{ typedef T type; };
template <class T> struct remove reference<T&&> //右值引用
	{ typedef T type; };

int i;
// decltype(42)为int，使用原始模板
remove_reference<decltype(42)>::type a;
// decltype(i)为int&，使用第一个(T&)部分特例化版本
remove_reference<decltype(i)>::type b;
// decltype(std::move(i))为int&&，使用第二个(即T&&)部分特例化版本
remove_reference<decltype(std::move(i))>::type c;
```



**特例化成员而不是类**

```c++
template <typename T> struct Foo {
    Foo(const T &t = T()) : mem(t) { }
    void Bar() { /* ...*/ }
    T mem;
    // Foo的其他成员
};

template<>		// 正在特例化一个模板
void Foo<int>::Bar()	// 正在特例化Foo<int>的成员Bar
{
    // 进行应用于int 的特例化处理
}

Foo<string> fs;		// 实例化Foo<string>::Foo()
fs.Bar();			// 实例化Foo<string>::Bar()
Foo<int> fi;		// 实例化Eoo<int>::Foo()
fi.Bar();			// 使用我们特例化版本的 Foo<int>::Bar()
```



# 标准库特殊设施

## tuple类型

不同 tuple 类型的成员类型不相同，可以有任意数量的成员

| tuple支持的操作                              |                                                              |
| -------------------------------------------- | ------------------------------------------------------------ |
| `tuple<T1, T2, ..·, Tn> t;`                  | t是一个tuple，成员数为n，第i个成员的类型为 Ti。所有成员都进行值初始化 |
| `tuple<T1, T2, ..., Tn> t(v1, v2, ..., vn);` | t是一个tuple，成员类型为 T1...Tn，每个成员用对应的初始值vi进行初始化。此构造函数是explicit 的 |
| `make_tuple(v1, v2, ..., vn)`                | 返回一个用给定初始值初始化的 tuple。tuple的类型从初始值的类型推断 |
| t1 == t2<br />t1 != t2                       | 当两个 tuple具有相同数量的成员且成员对应相等时两个tuple相等。这两个操作使用成员的==运算符来完成。一旦发现某对成员不等，接下来的成员就不用比较了 |
| t1 relop t2                                  | tuple的关系运算使用字典序(参见9.2.7节第304页)。两个tuple必须具有相同数量的成员。使用<运算符比较t1的成员和t2中的对应成员 |
| `get<i>(t)`                                  | 返回t的第个数据成员的引用:如果t是一个左值，结果是一个左值引用;否则，结果是一个右值引用。tuple的所有成员都是public的 |
| `tuple_size<tupleType>::value`               | 一个类模板，可以通过一个 tuple类型来初始化。它有一个名为value的public constexpr static数据成员，类型为size_t，表示给定tuple类型中成员的数量 |
| `tuple_element<i, tupleType>::type`          | 一个类模板，可以通过一个整型常量和一个 tuple 类型来初始化。它有一个名为 type的public成员，表示给定tuple类型中指定成员的类型 |

### 定义和初始化tuple

```c++
tuple<sizet, size_t, size_t> threeD;		// 三个成员都设置为0
tuple<string, vector<double>, int, list<int>>
    someVal("constants", {3.14, 2.718}, 42, {0,1,2,3,4,5});

tuple<size_t, size_t, size_t> threeD = {1, 2, 3};	// 错误
tuple<size_t, size_t, size_t> threeD{1, 2, 3};		// 正确

// 表示书店交易记录的 tuple，包含:ISBN、数量和每册书的价格
auto item = make_tuple("0-999-78345-X", 3, 20.00);
```

**访问tuple的成员**
使用一个名为 get的标准库函数模板
	为了使用 get，必须指定一个显式模板实参，它指出想要访问第几个成员

```c++
auto book = get<0>(item);		// 返回item的第一个成员
auto cnt = get<1>(item);		// 返回item的第二个成员
auto price = get<2>(item) / cnt;// 返回item的最后一个成员
get<2>(item) *= 0.8;			// 打折20号
```

**查询tuple成员的数量和类型**

```c++
typedef decltype(item) trans;		// trans是item的类型
//返回trans类型对象中成员的数量
size_t sz = tuple_size<trans>::value;	// 返回3
// cnt的类型与item中第二个成员相同
tuple_element<1, trans>::type cnt = get<1>(item);	// cnt是一个int
```

tuple_size有一个名为 value的public static数据成员，它表示给定tuple中成员的数量
tuple_element 模板除了一个 tuple 类型外，还接受一个索引值
	它有一个名为 type的 public 类型成员，表示给定 tuple 类型中指定成员的类型

**关系和相等运算符**

```c++
tuple<string, string> duo("1", "2");
tuple<size_t, size_t> twoD(1, 2);
bool b = (duo == twoD);	// 错误:不能比较sizet和string
tuple<size_t, size_t, size_t> threeD(1, 2, 3);
b = (twoD < threeD);	// 错误：成员类型不同
tuple<size_t, size_t> origin(0, 0);
b = (origin < twoD);	// 正确：b为true
```



### 使用tuple返回多个值

**返回tuple的函数**

```c++
// matches 有三个成员:一家书店的索引和两个指向书店vector元素的迭代器
typedef tuple<vector<Sales_data>::size_type,
	vector<Sales_data>::const_iterator, 
	vector<Sales_data>::const_iterator> matches;

// files保存每家书店的销售记录
// findBook返回一个 vector，每家销售了给定书籍的书店在其中都有一项
vector<matches> findBook(const vector<vector<Sales_data>> &files, const string &book)
{
    vector<matches> ret; // 初始化为空vector
    // 对每家书店，查找与给定书籍匹配的记录范围(如果存在的话)
    for (auto it = files.cbegin(); it != files.cend(); ++it) {
        //查找具有相同ISBN的Sales_data范围
        auto found = equal_range(it->cbegin(), it->cend(), book, compareIsbn);
        if (found.first != found.second)	// 此书店销售了给定书籍
            // 记住此书店的索引及匹配的范围
            ret.push_back(make_tuple(it - files.cbegin(), 
                                     found.first, found.second));
    }
    return ret;	// 如果未找到匹配记录的话，ret为空
}
```

**使用函数返回的tuple**

```c++
void reportResults(istream &in, ostream &os, 
                   const vector<vector<Sales data>> &files)
{
    string s;	// 要查找的书
    while (in >> s) {
        auto trans = findBook(files, s);	   // 销售了这本书的书店
        if (trans.empty()) {
            cout << s << "not found in any stores" << endl;
            continue; // 获得下一本要查找的书
        }
        for (const auto &store : trans) // 对每家销售了给定书籍的书店
            // get<n>返回store中tuple的指定的成员
            os << " store " << get<0>(store) << " sales: " 
            	<< accumulate(get<1>(store), get<2>(store), Sales_data(s))
            	<< endl;
    } 
}
```



## bitset类型

使得位运算的使用更为容易，并且能够处理超过最长整型类型大小的位集合

### 定义和初始化bitset

```c++
bitset<32> bitvec(1u);		// 32位;低位为1，其他位为0
```

| 初始化bitset的方法                    |                                                              |
| ------------------------------------- | ------------------------------------------------------------ |
| `bitset<n> b;`                        | b有n位;每一位均为0。此构造函数是一个constexpr                |
| `bitset<n> b(u); `                    | b是unsigned long long 值u的低n位的拷贝。如果n大于unsigned long long的大小,则b中超出unsigned long long 的高位被置为0。此构造函数是一个 constexpr |
| `bitset<n> b(s, pos, m, zero, one);`  | b是strings从位置pos 开始m个字符的拷贝。s只能包含字符zero或one;如果s包含任何其他字符，构造函数会抛出invalid_argument异常。字符在b中分别保存为 zero和one。pos 默认为0，m 默认为 `string::npos`，zero 默认为'0'，one默认为'1' |
| `bitset<n> b(cp, pos, m, zero, one);` | 与上一个构造函数相同，但从 cp 指向的字符数组中拷贝字符。如果未提供m，则cp必须指向一个C风格字符串。如果提供了m，则从cp开始必须至少有m个zero或one字符 |

接受一个string或一个字符指针的构造函数是explicit的。在新标准中增加了为0和1指定其他字符的功能。

**用unsigned值初始化bitset**

```c++
// bitvec1比初始值小;初始值中的高位被丢弃
bitset<13> bitvec1(0xbeef); //二进制位序列为1111011101111
// bitvec2比初始值大;它的高位被置为0
bitset<20> bitvec2(0xbeef); //二进制位序列为00001011111011101111
//在64位机器中，long long OULL是64个0比特，因此~0ULL是64个1
bitset<128> bitvec3(~0ULL); //0~63位为1;63~127位为0
```

**从一个string 初始化 bitset**

```c++
bitset<32> bitvec4("1100");		// 2、3两位为1，其余为0

string str("1111111000000011001101");
bitset<32> bitvec5(str, 5, 4);				// 从str[5]开始的四个二进制位，1100
bitset<32> bitvec6(str, str.size() - 4);	// 使用最后四个字符 1101
```



### bitset操作

|                                 |                                                              |
| ------------------------------- | ------------------------------------------------------------ |
| b.any()                         | b中是否存在置位的二进制位                                    |
| b.all()                         | b中所有位都置位了吗                                          |
| b.none()                        | b中不存在置位的二进制位吗                                    |
| b.count()                       | b中置位的位数                                                |
| b.size()                        | 一个 constexpr函数，返回b中的位数                            |
| b.test(pos)                     | 若 pos 位置的位是置位的，则返回 true，否则返回 false         |
| b.set(pos, v)<br />b.set()      | 将位置pos处的位设置为 bool值v。默认为 true。如果未传递实参，则将b 中所有位置位 |
| b.reset(pos)<br />b.reset()     | 将位置 pos 处的位复位或将 b 中所有位复位                     |
| b.flip(pos)<br />b.flip()       | 改变位置 pos处的位的状态或改变b中每一位的状态                |
| b[pos]                          | 访问b中位置 pos 处的位;如果b是 const 的，则当该位置位时 b[pos]返回一个bool值true，否则返回 false |
| b.to_ulong()<br />b.to_ullong() | 返回一个unsigned long或一个unsigned long long值其位模式与b相同。如果b中位模式不能放入指定的结果类型则抛出一个overflow_error异常 |
| b.to_string(zero, one)          | 返回一个string，表示b中的位模式。zero和one的默认值分别为0和1，用来表示b中的0和1 |
| os << b                         | 将b中二进制位打印为字符1或0，打印到流os                      |
| is >> b                         | 从is 读取字符存入b。当下一个字符不是1或0时，或是已经读入b.size()个位时，读取过程停止 |

```c++
bitset<32> bitvec(1u);				// 32位;低位为1，剩余位为0
bool is_set = bitvec.any();			// true，因为有1位置位
bool is_not_set = bitvec.none();	// false，因为有1位置位了
bool all_set = bitvec.all();		// false，因为只有1位置位
size_t onBits = bitvec.count();		// 返回1
size_t sz = bitvec.size();			// 返回32
bitvec.flip();						// 翻转bitvec中的所有位 
bitvec.reset();						// 将所有位复位
bitvec.set();						// 将所有位置位

bitvec.flip(0);		// 翻转第一位
bitvec.set(bitvec.size() - 1);	// 置位最后一位
bitvec.set(0, 0);		// 复位第一位
bitvec.reset(i);		// 复位第i位
bitvec.test(0);			// 返回 false，因为第一位是复位的

bitvec[0] = 0;			// 将第一位复位
bitvec[31] = bitvec[0];	// 将最后一位设置为与第一位一样
bitvec[0].flip();		// 翻转第一位
~bitvec[0];				// 等价操作，也是翻转第一位
bool b = bitvec[0];		// 将bitvec[0]的值转换为 bool类型
```

**提取bitset的值**

```c++
unsigned long ulong = bitvec3.to_ulong();
cout << "ulong = " << ulong << endl;
```

**bitset的IO运算符**

```c++
bitset<16> bits;
cin >> bits;	// 从cin读取最多16个0或1
cout << "bits: " << bits << endl;	// 打印刚刚读取的内容
```



## 正则表达式

## 随机数

## IO库再探



# 用于大型程序的工具

## 异常处理

异常处理(exception handling)机制允许程序中独立开发的部分能够在运行时就出现的问题进行通信并做出相应的处理。

### 抛出异常

当执行一个 throw时，跟在throw 后面的语句将不再被执行。相反，程序的控制权从throw 转移到与之匹配的catch 模块。该 catch 可能是同一个函数中的局部 catch,也可能位于直接或间接调用了发生异常的函数的另一个函数中。

**栈展开**
当throw出现在一个 try语句块 (try block)内时，检查与该try块关联的 catch 子句
	如果找到了匹配的 catch，就使用该 catch 处理异常
	如果这一步没找到匹配的catch 且该 try 语套在其他 try 块中，则继续检查与外层 try 匹配的catch 子句
		如果还是找不到匹配的 catch，则退出当前的函数，在调用当前函数的外层函数中继续寻找。
当找不到匹配的 catch时，程序将调用标准库函数 terminate，顾名思义，terminate 负责终止程序的执行过程。

**栈展开过程中对象被自动销毁**



### 捕获异常

如果 catch 接受的异常与某个继承体系有关,则最好将该 catch的参数定义成引用类型

**重新抛出**
一条 catch 语句通过重新抛出(rethrowing)的操作将异常传递给另外一个catch 语句。
这里的重新抛出仍然是一条throw语句，只不过不包含任何表达式:
`throw;`

```c++
catch (my_error &eObj) {		// 引用类型
	eObj.status = errCodes::severeErr;	// 修改了异常对象
    throw;					// 异常对象的status 成员是severeErr
} catch (other_error eObj) {	// 非引用类型
    eObj.status = errCodes::badErr;	// 只修改了异常对象的局部副本
    throw;					// 异常对象的 status 成员没有改变
}
```

**捕获所有异常的处理代码**
捕获所有异常 (catch-all)的处理代码，形如 catch(...)
如果catch(...)与其他几个catch 语句一起出现，则 catch(..)必须在最后的位置
	出现在捕获所有异常语句后面的 catch 语句将永远不会被匹配

```c++
void manip() {
    try {
        // 这里的操作将引发并抛出一个异常
    }
    catch (...) {
        // 处理异常的某些特殊操作
        throw;
    }
}
```

### 函数try 语句块与构造函数

因为在初始值列表抛出异常时构造函数体内的 try 语句块还未生效
	所以构造函数体内的 catch 语句无法处理构造函数初始值列表抛出的异常

要想处理构造函数初始值抛出的异常，必须将构造函数写成函数 try 语句块

这个 try 关联的 catch 既能处理构造函数体抛出的异常，也能处理成员初始化列表抛出的异常

```c++
template <typename T>
Blob<T>::Blob(std::initializer list<T> il) try :
	data(std::make_shared<std::vector<T>>(il)) {
     	/*空函数体*/   
} catch(const std::bad_alloc &e) { handle_out_of_memory(e); }
```



### noexcept异常说明

在C++11新标准中，我们可以通过提供 noexcept 说明(noexcept specification)指定某个函数不会抛出异常。

在 typedef 或类型别名中则不能出现 noexcept
在成员函数中，noexcept 说明符需要跟在 const 及引用限定符之后，在 final、override 或虚函数的=0之前

```c++
void recoup(int) noexcept;	// 不会抛出异常
void alloc(int);			// 可能抛出异常
```

**异常说明的实参**

```c++
void recoup(int) noexcept(true);		// recoup不会抛出异常
void alloc(int) noexcept(false);		// alloc可能抛出异常
```

**noexcept 运算符**
noexcept 运算符是一个一元运算符
	它的返回值是一个 bool类型的右值常量表达式用于表示给定的表达式是否会抛出异常
和 sizeof类似noexcept 也不会求其运算对象的值

```c++
noexcept(recoup(i)); // 如果recoup 不抛出异常则结果为 true;否则结果为 false
noexcept(e);		// 当e调用的所有函数都做了不抛出说明且e 本身不含有 throw 语句时，表达式为true;否则noexcept(e)返回false

void f() noexcept(noexcept(g()));	// f和g的异常说明一致
```

noexcept 有两层含义:
	当跟在函数参数列表后面时它是异常说明符;
	而当作为noexcept 异常说明的 bool实参出现时，它是一个运算符

**异常说明与指针、虚函数和拷贝控制**
函数指针及该指针所指的函数必须具有一致的异常说明

```c++
// recoup和pf1都承诺不会抛出异常
void (*pf1)(int) noexcept = recoup;
// 正确:recoup 不会抛出异常，pf2可能抛出异常，二者之间互不干扰
void (*pf2)(int) = recoup;
pf1 = alloc;// 错误:alloc可能抛出异常，但是 pf1已经说明了它不会抛出异常
pf2 = alloc;// 正确:pf2和alloc都可能抛出异常
```

如果一个虚函数承诺了它不会抛出异常，则后续派生出来的虚函数也必须做出同样的承诺;与之相反，如果基类的虚函数允许抛出异常，则派生类的对应函数既可以允许抛出异常，也可以不允许抛出异常:

```c++
class Base {
public:
    virtual double f1(double) noexcept;	// 不会抛出异常
    virtual int f2() noexcept(false);	// 可能抛出异常
    virtual void f3();					// 可能抛出异常
};

class Derived : public Base{
public:
	double f1(double);			// 错误:Base::f1承诺不会抛出异常
    int f2() noexcept(false);	// 正确:与Base::f2的异常说明一致
    void f3() noexcept;			// 正确:Derived的f3做了更严格的限定 这是允许的
};
```



### 异常类层次

exption
	bad_cast
	runtime_error
		overflow_error
		underflow_error
		range_error
	logic_error
		domain_error
		invalid_argument
		out_of_range
		length_error
	bad_alloc		

**自定义异常类**

```c++
// 为某个书店应用程序设定的异常类
class out_of_stock : public std::runtime_error {
public:
    explicit out_of_stock(const std::string &s) :
    			std::runtime_error(s) { }
};
class isbn_mismatch : public std::logic_error {
public:
    explicit isbn_mismatch(const std::string &s):
    	std::logic error(s) { }
    isbn_mismatch(const std::string &s, 
        	const std::string &lhs, const std::string &rhs):
    	std::logic_error(s), left(lhs), right(rhs) { }
    
    const std::string left, right;
};
```

**使用自定义异常类型**

```c++
// 如果参与加法的两个对象并非同一书籍，则抛出一个异常
Sales data& Sales_data::operator+=(const Sales_data& rhs)
{
    if (isbn() != rhs.isbn())
        throw isbn_mismatch("wrong isbns", isbn(), rhs.isbn());
    units_sold += rhs.units_sold;
    revenue += rhs.revenue;
    return *this;
}

// 使用之前设定的书店程序异常类
Sales dataitem1, item2, sum;
while (cin >> iteml >>item2) {		// 读取两条交易信息
    try {
        sum = item1 + item2;		// 计算它们的和
        // 此处使用sum
    } catch (const isbn mismatch &e) {
        cerr << e.what() << ": left isbn(" << e.left << 
            ") right isbn(" << e.right << ")" << endl;
    }   
}
```



## 命名空间

命名空间(namespace)为防止名字冲突提供了更加可控的机制。命名空间分割了全局命名空间，其中每个命名空间是一个作用域。通过在某个命名空间中定义库的名字，库的作者(以及用户)可以避免全局名字固有的限制。

### 命名空间定义

命名空间作用域后面无须分号。

**每个命名空间都是一个作用域**
**命名空间可以是不连续的**

**全局命名空间**
`::member_name`

**内联命名空间**
内联命名空间中的名字可以被外层命名空间直接使用
	无须在内联命名空间的名字前添加表示该命名空间的前缀，通过外层命名空间的名字就可以直接访问它

```c++
inline namespace FifthEd {
    // 该命名空间表示本书第 5版的代码
}

namespace FifthEd {		// 隐式内联
	class Query_base{ /*..*/ };	// 其他与Query有关的声明
}

namespace FourthEd {
    class Item_base { /*...*/ };
    class Query_base{ /*...*/ };
    // 本书第 4版用到的其他代码
}

// 因为 FifthEd 是内联的，所以形如 cplusplus primer::的代码可以直接获得FifthEd 的成员
// 如果想使用早期版本的代码，则必须加上完整的外层命名空间名字，比如cplusplus_primer::FourthEd::Query_base。
namespace cplusplus_primer{
    #include "FifthEd.h"
    #include "FourthEd.h"
}
```

**未命名的命名空间**
未命名的命名空间(unnamednamespace)是指关键字namespace后紧跟花括号括起来的一系列声明语句
未命名的命名空间中定义的变量拥有静态生命周期：它们在第一次使用前创建，并且直到程序结束才销毁
和其他命名空间不同，未命名的命名空间仅在特定的文件内部有效，其作用范围不会横跨多个不同的文件



### 使用命名空间成员

**命名空间的别名**

```c++
namespace cplusplus_primer { /* ... */ };
namespace primer = cplusplus_primer;

namespace Qlib = cplusplus_primer::QueryLib;
Qlib::Query q;
```

**using声明:扼要概述**
一条using声明(using declaration)语句一次只引入命名空间的一个成员
using 声明语句声明的是一个名字，而非一个特定的函数

```c++
using NS::print(int);		// 错误:不能指定形参列表
using NS::print;			// 正确:using声明只声明一个名字
```

**using 指示**
using 指示以关键字using 开始，后面是关键字namespace 以及命名空间的名字

```c++
namespace libs_R_us {
    extern void print(int);
    extern void print(double);
}
// 普通的声明
void print(const std::string &);
//这个using指示把名字添加到 print 调用的候选函数集
using namespace libs_R_us;
// print调用此时的候选函数包括:
// libs_R_us的print(int)
// libs_R_us的print(double)
// 显式声明的print(const std::string &)
void fooBar(int ival)
{
    print("Value:");		// 调用全局函数print(const string &)
    print(ival);			// 调用libsRus::print(int)
}
```

**头文件与using声明或指示**
头文件如果在其顶层作用域中含有 using 指示或using 声明，则会将名字注入到所有包含了该头文件的文件中

### 类、命名空间与作用域

**实参相关的查找与类类型形参**

**查找与std::move和std::forward**

**友元声明与实参相关的查找**
一个另外的未声明的类或函数如果第一次出现在友元声明中，则我们认为它是最近的外层命名空间的成员

```c++
namespace A {
	class C {
		// 两个友元，在友元声明之外没有其他的声明
        // 这些函数隐式地成为命名空间A的成员
        friend void f2();				// 除非另有声明，否则不会被找到
        friend void f(const C&);		// 根据实参相关的查找规则可以被找到
    };
}
int main()
{
    A::C cobj;			
    f(cobj);		// 正确:通过在A::C中的友元声明找到A::f
    f2();			// 错误:A::f2没有被声明
}
```



### 重载与命名空间

**与实参相关的查找与重载**
对于接受类类型实参的函数来说，其名字查找将在实参类所属的命名空间中进行

```c++
namespace NS {
    class Quote{ /*...*/ };
    void display(const Quote&) { /* ...*/ }
}
// Bulk_item的基类声明在命名空间NS中
class Bulk_item : public NS::Quote { /* ...*/ };
int main() {
    Bulk_item book1;
    display(book1);
    return 0;
} 
```



## 多重继承和虚继承

### 多重继承

```c++
class Bear : public ZooAnimal
class Panda : public Bear, public Endangered { /* ...*/ };
```

<img src=".\Picture\Panda对象结构.png" style="zoom:50%;" />

**派生类构造函数初始化所有基类**

```c++
// 显式地初始化所有基类
Panda::Panda(std::string name, bool onExhibit)
    : Bear(name, onExhibit, "Panda"),
	Endangered(Endangered::critical) { }
// 隐式地使用 Bear 的默认构造函数初始化 Bear子对象
Panda::Panda() : Endangered(Endangered::critic al) { }
```

**继承的构造函数与多重继承**
如果从多个基类中继承了相同的构造函数(即形参列表完全相同),则程序将产生错误:

```c++
struct Base1 {
    Base1() = default;
    Base1(const std::string&);
    Base1(std::shared_ptr<int>);
};

struct Base2 {
    Base2() = default;
    Base2(const std::string&);
    Base2(int);
};
// 错误:D1试图从两个基类中都继承D1::D1(const string&)
struct D1 : public Base1, public Base2{
    using Base1::Base1;		// 从Basel继承构造函数
	using Base2::Base2;		// 从Base2继承构造函数
};

// 如果一个类从它的多个基类中继承了相同的构造函数，则这个类必须为该构造函数定义它自己的版本:
struct D2: public Basel, public Base2 {
    using Base1::Base1;		// 从Basel继承构造函数
    using Base2::Base2;		// 从Base2继承构造函数
    // D2必须自定义一个接受 string 的构造函数
    D2(const string &s): Base1(s), Base2(s) { }
    D2() = default;		// 一旦D2定义了它自己的构造函数，则必须出现
};
```

**析构函数与多重继承**

析构函数的调用顺序正好与构造函数相反，
	析构函数的调用顺序是~Panda、~Endangered、~Bear和~ZooAnimal

### 类型转换与多个基类

```c++
// 接受 Panda的基类引用的一系列操作
void print(const Bear&);
void highlight(const Endangered&);
ostream& operator<<(ostream&, const ZooAnimal&);
Panda ying_yang("ying_yang");
print(ying_yang);					// 把一个Panda对象传递给一个Bear的引用
highlight(ying_yang);				// 把一个Panda对象传递给一个Endangered 的引用
cout << ying_yang << endl;			// 把一个Panda对象传递给一个ZooAnimal的引用
```



### 多重继承下的类作用域

要想避免潜在的二义性，最好的办法是在派生类中为该函数定义一个新版本。



### 虚继承

虚继承的目的是令某个类做出声明，承诺愿意共享它的基类
	其中，共享的基类子对象称为虚基类(virtual base class)
在这种机制下，不论虚基类在继承体系中出现了多少次，在派生类中都只包含唯一一个共享的虚基类子对象

```c++
// 关键字public和virtual的顺序随意
class Raccoon : public virtual ZooAnimal { /*...*/ };
class Bear : virtual public ZooAnimal { /*...*/ };

class Panda : public Bear, public Raccoon, public Endangered { };
```

### 构造函数与虚继承

在虚派生中，虚基类是由最低层的派生类初始化的
虚基类总是先于非虚基类构造，与它们在继承体系中的次序和位置无关

含有虚基类的对象的构造顺序与一般的顺序稍有区别:
	首先使用提供给最低层派生类构造函数的初始值初始化该对象的虚基类子部分
	接下来按照直接基类在派生列表中出现的次序依次对其进行初始化

编译器按照直接基类的声明顺序对其依次进行检查，以确定其中是否含有虚基类
	如果有，则先构造虚基类，然后按照声明的顺序逐一构造其他非虚基类。
和往常一样，对象的销毁顺序与构造顺序正好相反



# 特殊工具与技术

## 控制内存分配

应用程序需要重载 new 运算符和 delete 运算符以控制内存分配的过程

### 重载 new 和 delete

**使用new表达式**
	第一步，new表达式调用一个名为operator new(或者operator new[])的标准库函数
		该函数分配一块足够大的、原始的、未命名的内存空间以便存储特定类型的对象(或者对象的数组)
	第二步，编译器运行相应的构造函数以构造这些对象，并为其传入初始值
	第三步，对象被分配了空间并构造完成，返回一个指向该对象的指针

**使用delete表达式**
	第一步，对 sp 所指的对象或者 arr 所指的数组中的元素执行对应的析构函数
	第二步,编译器调用名为operator delete(或者operator delete[])的标准库函数释放内存空间。

如果应用程序希望控制内存分配的过程，则它们需要定义自己的operator new函数和operator delete 函数。

**查找operator new**
如果被分配(释放)的对象是类类型，则编译器首先在类及其基类的作用域中查找
编译器在全局作用域查找匹配的函数
	此时如果编译器找到了用户自定义的版本，则使用该版本执行 new 表达式或delete表达式
使用标准库定义的版本

**operator new 接口和operator delete 接口**

```c++
// 这些版本可能抛出异常
void *operator new(size_t);				// 分配一个对象
void *operator new[](size_t);			// 分配一个数组
void *operator delete(void*) noexcept;	// 释放一个对象
void *operator delete[](void*) noexcept;	// 释放一个数组

// 这些版本承诺不会抛出异常
void *operator new(size_t, nothrow_t&) noexcept;
void *operator new[](size_t, nothrow_t&) noexcept;
void *operator delete(void*, nothrow_t&) noexcept;
void *operator delete[](void*, nothrow_t&) noexcept;
```

类型nothrow_t是定义在new头文件中的一个struct，在这个类型中不包含任何成员

**operator new限制**
对于operator new 函数或者 operator new[]函数来说，
	它的返回类型必须是void*，第一个形参的类型必须是 size_t且该形参不能含有默认实参
当为一个对象分配空间时使用operator new；为一个数组分配空间时使用operator new[]
	当编译器调用operator new时，把存储指定类型对象所需的字节数传给size_t形参
	当调用operator new[]时，传入函数的则是存储数组中所有元素所需的空间

下面这个函数却无论如何不能被用户重载:

```c++
void *operator new(size_t, void*);	// 不允许重新定义这个版本
```

**operator delete限制**
对于operator delete 函数或者operator delete[]函数：
	返回类型必须是void，第一个形参的类型必须是 `void*`
	执行一条delete 表达式将调用相应的operator函数，并用指向待释放内存的指针来初始化`void*`形参

**malloc函数与free 函数**
malloc函数接受一个表示待分配字节数的size_t，返回指向分配空间的指针或者返回0以表示分配失败
free 函数接受一个 void*，它是malloc 返回的指针的副本free将相关内存返回给系统

```c++
void *operator new(size_t size) {
    if (void *mem = malloc(size))
        return mem;
    else
        throw bad_alloc();
}
void operator delete(void *mem) noexcept { free(mem); }
```

### 定位new表达式

new 的这种形式为分配函数提供了额外的信息。我们可以使用定位 new 传递一个地址，此时定位 new的形式如下所示:

```c++
new (place_address) type
new (place_address) type (initializers)
new (place_address) type [size]
new (place_address) type [size] { braced initializer list }
```

当仅通过一个地址值调用时，定位new 使用`operator new(size_t，void*)`“分配”它的内存
	这是一个无法自定义的operator new版本
该函数不分配任何内存，它只是简单地返回指针实参
然后由 new 表达式负责在指定的地址初始化对象以完成整个工作
	事实上，定位 new 允许在一个特定的、预先分配的内存地址上构造对象

**显式的析构函数调用**
调用析构函数可以清除给定的对象但是不会释放该对象所在的空间

```c++
string *sp = new string("a value");		// 分配并初始化一个string对象
sp->~string();
```



## 运行时类型识别

运行时类型识别(run-time type identification，RTTI)的功能由两个运算符实现:

- typeid运算符，用于返回表达式的类型
- dynamic_cast 运算符，用于将基类的指针或引用安全地转换成派生类的指针或引用

### dynamic_cast运算符

```c++
dynamic_cast<type*>(e);
dynamic_cast<type&>(e);
dynamic_cast<type&&>(e);
```

type 必须是一个类类型，并且通常情况下该类型应该含有虚函数
	在第一种形式中e必须是一个有效的指针
	在第二种形式中e必须是一个左值
	在第三种形式中，e不能是左值

e 的类型必须符合以下三个条件中的任意一个
	e的类型是目标 type 的公有派生类
	e的类型是目标 type 的公有基类
	e的类型就是目标ype 的类型
如果符合，则类型转换可以成功。否则，转换失败

如果一条 dynamic_cast 语句的转换目标是指针类型并且失败了，则结果为 0
如果转换目标是引用类型并且失败了，则dynamic_cast 运算符将抛出一个bad_cast 异常

**指针类型的dynamic_cast**

```c++
if (Derived *dp = dynamic_cast<Derived*>(bp))
{
    // 使用dp指向的Derived对象
} else {	// bp指向一个Base对象
    // 使用bp指向的Base对象
}
```

**引用类型的dynamic_cast**

```c++
void f(const Base &b)
{
    try {
        // 使用b引用的Derived对象
        const Derived &d = dynamic_cast<const Derived&>(b);	
    } catch (bad_cast) {
        // 处理类型转换失败的情况
    }
}
```



### typeid运算符

typeid 表达式的形式是 typeid(e)，其中e可以是任意表达式或类型的名字
typeid操作的结果是一个常量对象的引用，该对象的类型是标准库类型 type_info或者type_info的公有派生类型
type_info类定义在typeinfo头文件中

typeid运算符可以作用于任意类型的表达式
	顶层const被忽略
	如果表达式是一个引用，则 typeid 返回该引用所引对象的类型
	不过当 typeid作用于数组或函数时，并不会执行向指针的标准类型转换
		也就是说，如果我们对数组 a 执行 typeid(a)，则所得的结果是数组类型而非指针类型

**使用typeid运算符**

```c++
Derived *dp = new Derived;
Base *bp = dp;			// 两个指针都指向 Derived对象
// 在运行时比较两个对象的类型
if (typeid(*bp) == typeid(*dp)) {
    // bp和dp指向同一类型的对象
}
// 检查运行时类型是否是某种指定的类型
if (typeid(*bp) == typeid(Derived)) {
    // bp实际指向Derived对象
}

//下面的检查永远是失败的:bp的类型是指向 Base的指针
if (typeid(bp) == typeid(Derived)) {
    //此处的代码永远不会执行
}
```

typeid是否需要运行时检查决定了表达式是否会被求值
	只有当类型含有虚函数时编译器才会对表达式求值
	反之，如果类型不含有虚函数，则typeid返回表达式的静态类型
		编译器无须对表达式求值也能知道表达式的静态类型



### 使用RTTI

定义的相等运算符的形参是基类的引用，然后使用 typeid检查两个运算对象的类型是否一致
	如果运算对象的类型不一致，则==返回 false:类型一致才调用equal 函数
每个类定义的equal函数负责比较类型自己的成员
	这些运算符接受 Base&形参，但是在进行比较操作前先把运算对象转换成运算符所属的类类型

**类的层次关系**

```c++
class Base {
    friend bool operator==(const Base&, const Base&);
public:
    // Base的接口成员
protected:
    virtual bool equal(const Bases) const;
    // Base的数据成员和其他用于实现的成员
};
class Derived: public Base{
public:
    // Derived的其他接口成员
protected:
    bool equal(const Base&) const;
    // Derived的数据成员和其他用于实现的成员
};
```

**类型敏感的相等运算符**

```c++
bool operator==(const Base &lhs, const Base &rhs)
{
    //如果typeid不相同，返回false;否则虚调用equal
    return typeid(lhs) == typeid(rhs) && lhs.equal(rhs);
}
```

**虚equal函数**

```c++
bool Derived::equal(const Base &rhs) const
{
    // 我们清楚这两个类型是相等的，所以转换过程不会抛出异常
    auto r = dynamic_cast<const Derived&>(rhs);
    // 执行比较两个 Derived 对象的操作并返回结果
}
```

**基类equal函数**

```c++
bool Base::equal(const Base &rhs) const
{
    // 执行比较 Base对象的操作
}
```

### type_info类

| type_info的操作 |                                                              |
| --------------- | ------------------------------------------------------------ |
| t1==t2          | 如果typeinfo对象t1和t2表示同一种类型，返回true;否则返四false |
| t1 != t2        | 如果typeinfo对象t1和t2表示不同的类型，返回true;否则返false   |
| t.name()        | 返回一个C风格字符串，表示类型名字的可打印形式。类型名字的生成方式因系统而异 |
| t1.before(t2)   | 返回一个bool值，表示t1是否位于t2之前。before所采用的顺序关系是依赖于编译器的 |


typeinfo类的name成员函数返回一个C风格字符串，表示对象的类型名字

```c++
int arr[10];
Derived d;
Base *p = &d;

cout << typeid(42).name() << ", "
    << typeid(arr).name() << ", " 
    << typeid(Sales_data).name() << ", "
    << typeid(std::string).name() << ", "
    << typeid(p).name() << ", " 
    << typeid(*p).name() << endl;
// i, A10_i, 10Sales_data, Ss, P4Base, 7Derived 
```



## 枚举类型

C++包含两种枚举:
	限定作用域的
	不限定作用域的

C++11新标准引入了限定作用域的枚举类型(scoped enumeration)
定义限定作用域的枚举类型的一般形式是:
	首先是关键字enumclass(或者等价地使用enumstruct)，
	随后是枚举类型名字以及用花括号括起来的以逗号分隔的枚举成员(enumerator)列表，最后是一个分号:

```c++
// 限定作用域的枚举类型
enum class open_modes {input, output, append};

// 不限定作用域的枚举类型
enum color {red, yellow, green};
// 未命名的、不限定作用域的枚举类型
enum { floatPrec = 6, doublePrec = 10, double_doublePrec = 10};
```

**枚举成员**

```c++
enum color {red, yellow, green};			// 不限定作用域的枚举类型
enum stoplight { red, yellow, green };		// 错误:重复定义了枚举成员
enum class peppers { red, yellow, green };	// 正确:枚举成员被隐藏了

color eyes = green;	// 正确:不限定作用域的枚举类型的枚举成员位于有效的作用域中
peppers p = green;	// 错误:peppers的枚举成员不在有效的作用域中
					// color::qreen在有效的作用域中，但是类型错误
color hair = color::red;	// 正确:允许显式地访问枚举成员
peppers p2 = peppers::red;	// 正确:使用pappers的red

int i = color::red; 	// 正确:不限定作用域的枚举类型的枚举成员隐式地转换成int
int j = peppers::red;	// 错误:限定作用域的枚举类型不会进行隐式转换
```

**指定enum大小**

```c++
enum intValues : unsigned long long {
    charTyp = 255, 
    shortTyp = 65535,
    intTyp = 65535,
    longTyp = 4294967295UL,
    longlongTyp = 18446744073709551615ULL
};
```

**枚举类型的前置声明**

```c++
//不限定作用域的枚举类型intValues的前置声明
enum intValues : unsigned long long; 	// 不限定作用域的，必须指定成员类型
enum class open_modes;					// 限定作用域的枚举类型可以使用默认成员类型 int
```



## 类成员指针

```c++
class Screen {
public:
    typedef std::string::size_type pos;
    char get_cursor() const { return contents[cursor]; }
    char get() const;
    char get(pos ht, pos wd) const;
private:
    std::string contents;
    pos cursor;
    pos height, width;
};
```

### 数据成员指针

```c++
// pdata可以指向一个常量(非常量)Screen对象的string 成员
const string Screen::*pdata;
pdata = &Screen::contents;
auto pdata = &Screen::contents;

//使用数据成员指针
Screen myScreen, *pScreen = &myScreen;
// .*解引用pdata以获得myScreen 对象的contents成员
auto s = myScreen.*pdata;
// ->*解引用pdata以获得pScreen 所指对象的contents成员
s = pScreen->*pdata;

//返回数据成员指针的函数
class Screen {
public:
    // data是一个静态成员，返回一个成员指针
    static const std::string Screen::*data()
    	{ return &Screen::contents; }
    // 其他成员与之前的版本一致
};

// data()返回一个指向Screen类的contents成员的指针
// pdata 指向Screen 类的成员而非实际数据。要想使用pdata，必须把它绑定到Screen类型的对象上:
const string Screen::*pdata = Screen::data();
// 获得myScreen对象的contents成员
auto s = myScreen.*pdata;
```

### 成员函数指针

```c++
// pmf 是一个指针，它可以指向 Screen的某个常量成员函数
// 前提是该函数不接受任何实参，并且返回一个char
auto pmf = &Screen::get_cursor;

// 出于优先级的考虑，声明中Screen::*两端的括号必不可少
char (Screen::*pmf2)(Screen::pos, Screen::pos) const;
pmf2 = &Screen::get;

// pmf指向一个Screen成员，该成员不接受任何实参且返回类型是char
pmf = &Screen::get;	// 必须显式地使用取地址运算符
pmf = Screen::get;	// 错误:在成员函数和指针之间不存在自动转换规则

//使用成员函数指针
Screen myScreen, *pScreen = &myScreen;
// 通过pScreen所指的对象调用pmf所指的函数
char c1 = (pScreen->*pmf)();
// 通过myScreen 对象将实参0，0传给含有两个形参的get函数
char c2 = (myScreen.*pmf2)(0, 0);

//使用成员指针的类型别名
// Action是一种可以指向Screen成员函数的指针，它接受两个pos实参，返回一个char
using Action = char (Screen::*)(Screen::pos, Screen::pos) const;
Action get = &Screen::get; // get指向Screen的get成员
// action 接受一个Screen 的引用，和一个指向 Screen 成员函数的指针
Screen& action(Screen&, Action = &Screen::get);
Screen myScreen;
//等价的调用:
action(myScreen);				// 使用默认实参
action(myScreen, get);			// 使用我们之前定义的变量 get
action(myScreen, &Screen::get);	// 显式地传入地址
```

**成员指针函数表**

```c++
Class Screen {
public:
    // 其他接口和实现成员与之前一致
    Screen& home();
    Screen& forward();	// 光标移动函数
    Screen& back();
    Screen& up();
    Screen& down();
};

class Screen {
public:
    // 其他接口和实现成员与之前一致
    // Action是一个指针，可以用任意一个光标移动函数对其赋值
    using Action = Screen& (Screen::*)();
    // 指定具体要移动的方向
    enum Directions{ HOME, FORWARD, BACK, UP,DOWN };
    Screen& move(Directions);
private:
    static Action Menu[];		// 函数表
};

Screen& Screen::move(Directions cm) 
{
    // 运行this对象中索引值为cm的元素
    return (this->*Menu[cm])(); // Menu[cm]指向一个成员函数
}

Screen::Action Screen::Menu[] = {
    &Screen::home,
    &Screen::forward,
    &Screen::back,
    &Screen:;up,
    &Screen::down,
};

Screen myScreen;
myScreen.move(Screen::HOME);	// 调用myScreen.home
myScreen.move(Screen::DOWN);	// 调用myScreen.down
```



### 将成员函数用作可调用对象

```c++
auto fp = &string::empty;		// fp指向string的empty函数
// 错误，必须使用.*或->*调用成员指针
find_if(svec.begin(), svec.end(), fp);
```

**使用function生成一个可调用对象**

```c++
function<bool (const string&)> fcn = &string::empty;
find_if(svec.begin(), svec.end(), fcn);

// 假设it是find_if内部的迭代器，则*it 是给定范围内的一个对象
if (fcn(*it))	{ } // 假设fcn是find_if内部的一个可调用对象的名字
// To
// 假设it是findif内部的迭代器，则*it 是给定范围内的一个对象
if (((*it).*p)()) { }// 假设p是fcn内部的一个指向成员函数的指针

vector<string*> pvec;
function<bool (const string*)> fp = &string::empty;
//fp接受一个指向string的指针，然后使用->*调用empty
find_if(pvec.begin(), pvec.end(), fp);
```

**使用mem_fn生成一个可调用对象**
通过使用标准库功能mem_fn来让编译器负责推断成员的类型

```c++
find_if(svec.begin(), svec.end(), mem_fn(&string::empty));

auto f = mem_fn(&string::empty);	// f接受一个string或者一个string*
f(*svec.begin());		// 正确:传入一个string对象，f使用*调用empty
f(&svec[0]);			// 正确:传入一个string的指针,f使用->*调用empty
```

**使用bind生成一个可调用对象**

```c++
//选择范围中的每个string，并将其 bind到empty的第一个隐式实参上
auto it = find_if(svec.begin(), svec.end(), bind(&string::empty, _1));
auto f = bind(&string::empty, _1);
f(*svec.begin());	// 正确:实参是一个string，f使用.*调用empty
f(&svec[0]);		// 正确:实参是一个string的指针，f使用->*调用empty
```



## 嵌套类

一个类可以定义在另一个类的内部,前者称为嵌套类或嵌套类型

嵌套类的名字在外层类作用域中是可见的，在外层类作用域之外不可见
嵌套类的名字不会和别的作用域中的同一个名字冲突

嵌套类中成员的种类与非嵌套类是一样的
嵌套类也使用访问限定符来控制外界对其成员的访问权限
	外层类对嵌套类的成员没有特殊的访问权限
	嵌套类对外层类的成员也没有特殊的访问权限

嵌套类在其外层类中定义了一个类型成员
该类型的访问权限由外层类决定
	位于外层类 public 部分的嵌套类实际上定义了一种可以随处访问的类型
	位于外层类 protected 部分的嵌套类定义的类型只能被外层类及其友元和派生类访问
	位于外层类 private 部分的嵌套类定义的类型只能被外层类的成员和友元访问

```c++
//声明一个嵌套类
class TextQuery {
public:
    class QueryResult;		// 嵌套类稍后定义
};

//在外层类之外定义一个嵌套类
// QueryResult是TextQuery的成员，下面的代码负责定义QueryResult
class TextQuery::QueryResult {
    // 位于类的作用域内，因此我们不必对QueryResult 形参进行限定
    friend std::ostream& print(std::ostream&, const QueryResult&);
public:
    // 无须定义QueryResult::line_no
    // 嵌套类可以直接使用外层类的成员，无须对该成员的名字进行限定
    QueryResult(std::string,
               std::shared_ptr<std::set<line_no>>,
               std::shared_ptr<std::vector<std::string>>); 
};

//定义嵌套类的成员
// QueryResult类嵌套在TextQuery类中
// 下面的代码为QueryResult类定义名为QueryResult的成员
TextQuery::QueryResult::QueryResult(string s, 
                                    shared_ptr<set<lineno>> p,
                                    shared_ptr<vector<string>> f):
	sought(s), lines(p), file(f) { }

//嵌套类的静态成员定义
int TextQuery::QueryResult::static_mem = 1024;

// TextQuery的query成员可以直接使用名字QueryResult
```



## union:一种节省空间的类

一个union可以有多个数据成员，但是在任意时刻只有一个数据成员可以有值
分配给一个 union 对象的存储空间至少要能容纳它的最大的数据成员

union不能含有引用类型的成员
含有构造函数或析构函数的类类型也可以作为union的成员类型
union可以为其成员指定public、protected和private 等保护标记
	默认情况下，union 的成员都是公有的，这一点与struct相同

**定义union**

```c++
// Token 类型的对象只有一个成员，该成员的类型可能是下列类型中的任意一种
union Token{
    //默认情况下成员是公有的
    charc	cval;
    int		ival;
    double 	dval;
};

//使用union类型
Token first_token = {'a'};		// 初始化cval成员
Token last_token;				// 未初始化的Token对象
Token *pt = new Token;			// 指向一个未初始化的 Token 对象的指针
last_token.cval = 'z';
pt->ival = 42;

//匿名union
union {		// 匿名union
    char cval;
	int ival;
	double dval;
};	// 定义一个未命名的对象，我们可以直接访问它的成员
cval = 'c';	// 为刚刚定义的未命名的匿名union对象赋一个新值
ival = 42;	// 该对象当前保存的值是 42
```



## 局部类

类可以定义在某个函数的内部，我们称这样的类为局部类(local class)

**局部类不能使用函数作用域中的变量**



## 固有的不可移植的特性

### 位域

位域在内存中的布局是与机器相关的

### volatile限定符

> volatile的确切含义与机器有关，只能通过阅读编译器文档来理解。要想让使用了 volatile 的程序在移植到新机器或新编译器后仍然有效，通常需要对该程序进行某些改变

当对象的值可能在程序的控制或检测之外被改变时，应该将该对象声明为 volatile
关键字 volatile告诉编译器不应对这样的对象进行优化

### 链接指示:extern"C"

C++使用链接指示(linkage directive)指出任意非C++函数所用的语言
