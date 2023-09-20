C++提供四种不同而又相辅相成的编程范型：

- procedural-based	基于程序
- object-based			基于对象
- object-oriented		面向对象
- generics					泛型



# 导读

忠告大致分为两类:
	一般性的设计策略
	带有具体细节的特定语言特性

目的是要强调那些常常被漠视的 C++ 编程方向与观点

## 术语

**声明式**(declaration)是告诉编译器某个东西的名称和类型(type)

```c++
extern int x;						// 对象 (object)声明式
std::size_t numDigits(int number);	// 函数(function)声明式
class Widget;						// 类(class)声明式
template<typename T>				// 模板(temmplate)声明式
class GraphNode;
```

每个函数的声明揭示其**签名式**(signature)，也就是**参数**和**返回类型**
	`numDigits` 函数的签名是 std::size_t (int)，
		也就是说“这函数获得一个int并返回一个std::size_t”
C++ 对签名式的**官方定义**并**不包括函数的返回类型**，不过本书把返回类型视为签名的一部分，这样比较有帮助

**定义式**(definition)的任务是提供编译器一些声明式所遗漏的细节
	对对象而言，定义式是编译器为此对象拨发内存的地点
	对 function 或 function template而言，定义式提供了代码本体
	对 class 或class template 而言,定义式列出它们的成员

```c++
int x;										//对象的定义式
std::size_t numDigits(int number)			//函数的定义式
{											//此函数返回其参数的数字个数
    std::size_t digitsSoFar = 1;			//例如十位数返回2，百位数返回3.
    while ((number /= 10) != 0) ++digitsSoFar;
    return digitsSoFar;
}
class Widget {					//class的定义式
public:
    Widget();
    ~Widget();
    // ...
};
template<typename T>			//template的定义式
class GraphNode {
public:
    GraphNode();
    ~GraphNode();
    // ...
};
```

**初始化** (initialization)是“给予对象初值”的过程
	对用户自定义类型的对象而言，初始化由构造函数执行

```c++
class A {
public:
    A();			//default构造函数
};

class B {
public:
    //explicit：阻止它们被用来执行隐式类型转换
    //被声明为 explicit 的构造函数通常比其 non-explicit 兄弟更受欢迎
    explicit B(int x = 0, bool b = true);		//default构造函数;
};

class C {
public:
    explicit C(int x);		//不是 default 构造函数
};

void doSomething(B bObject);		//函数，接受一个类型为 B的对象
B bObj1;
doSomething(bObj1);
B bObj2(28);						
doSomething(28);					//错误! DoSomething 应该接受一个B
doSomethinq(B(28));					//没问题，使用B 构造函数将 int 显式转换
```

**copy构造函数**被用来“以同型对象初始化自我对象”
**copy assignment操作符**被用来“从另一个同型对象中拷贝其值到自我对象”

```c++
class Widget {
public:
    Widget();					//default构造函数
    Widget(const widget& rhs);	//copy构造函数
    Widget& operator=(const widget& rhs);	//copy assignment操作符
    //...
};

Widget w1;		//调用default构造函数
Widget w2(w1);	//调用copy构造函数
w1 = w2;		//调用copy assignment操作符
Widget w3 = w2;	//调用copy构造函数!!!
//Pass-by-reference-to-const往往是比较好的选择
```

**STL**是所谓标准模板库(Standard Template Library)，是C++ 标准程序库的一部分，致力于：
	容器(如 vector,list,set,map等等)
	选代器(如`vector<int>::iterator`, `set<string>::iterator`等等)、
	算法(如 for_each, find, sort 等等及相关机能
许多相关机能以函数对象 (function objects)实现，那是“行为像函数”的对象
	这样的对象来自于重载 operator()(function call操作符)的classes

**接口**完全是指一般性的设计观念

**客户** (client)是指某人或某物，他(或它)使用你写的代码(通常是些接口)

在程序批注中提到构造函数和析构函数时，有时我会使用缩写字 **ctor** 和 **dtor**



## 命名习惯

## TR1和 Boost

TR1(”Technical Report 1")是一份规范，描述加入 C++ 标准程序库的诸多新机能
	这些机能以新的class templates 和 function templates 形式体现
		针对的题目有 hash tables, reference-counting smart pointers, regular expressions，以及更多
所有TR1 组件都被置于命名空间 tr1内，后者套于命名空间 std 内

Boost 是个组织，亦是一个网站 (http://boost.org)，提供可移植、同僚复审、源码开放的 C++ 程序库。



# 让自己习惯C++

## 条款01:视 C++ 为一个语言联邦

View C++ as a federation of languages

C++是个多重范型编程语言 (multiparadigm programming language)，一个同时支持
	**过程形式**(procedural)
	**面向对象形式**(object-oriented)
	**函数形式**(functional)
	**泛型形式**(generic)
	**元编程形式**(metaprogramming)
的语言

为了理解 C++，你必须认识其主要的**次语言**。幸运的是总共只有四个:

- **C**：区块 (blocks)、语句 (statements)、预处理器(preprocessor)、内置数据类型 (built-in data types) 、数组 (arrays)指针(pointers)等统统来自C
- **Object-Oriented C++**：classes (包括构造函数和析构函数)，封装 (encapsulation)、继承 (inheritance)、多态(polymorphism)、virtual函数(动态绑定)······等等
- **Template C++**：实际上由于 templates 威力强大，它们带来崭新的编程范型(programming paradigm)，也就是所谓的 template metaprogramming(TMP，模板元编程)
- **STL**：STL 是个 template 程序库。它对容器(containers)、代器(iterators)、算法(algorithms)以及函数对象(function objects)的规约有极佳的紧密配合与协调，然而 templates 及程序库也可以其他想法建置出来

### 总结：

**C++ 高效编程守则视状况而变化，取决于你使用 C++ 的哪一部分**



## 条款02:尽量以const,enum,inline 替换 #define

Prefer consts, enums, and inlines to #defines.

```c++
#define ASPECT_RATIO 1.653
```

记号名称 ASPECT RATIO也许从未被编译器看见
	也许在编译器开始处理源码之前它就被预处理器移走了
	于是记号名称 ASPECT_RATIO 有可能没进入记号表(symbol table)内

解决之道是以一个常量替换上述的宏 (#define)：

```c++
const double AspectRatio = 1.653;	//大写名称通常用于宏
									//因此这里改变名称写法
```

由于常量定义式通常被放在头文件内(以便被不同的源码含)
	因此有必要将**指针**(而不只是指针所指之物)声明为 const

```c++
const char* const authorName = "Scott Meyers";
//更好的做法
const std::string authorName("Scott Meyers");
```

**class 专属常量**
	为了将常量的作用域(scope)限制于 class内，你必须让它成为 class 的一个成员 (member)
	而为确保此常量至多只有一份实体，你必须让它成为一个 static 成员:

```c++
class GamePlayer {
private:
	static const int NumTurns = 5;		//常量声明式
    int scores[NumTurns];				//使用该常量
};

```

只要不取class专属常量的地址可以声明并使用它们而无须提供定义式
但如果取某个 class 专属常量的地址或纵使不取其地址而编译器却(不正确地)坚持要看到一个定义式，就必须另外提供定义式如下:

```c++
const int GamePlayer::NumTurns;	//NumTurns 的定义;
// 请把这个式子放进一个实现文件而非头文件
// 由于 class 常量已在声明时获得初值(例如先前声明 numTurns 时为它设初值5)，因此定义时不可以再设初值
```

旧式编译器也许不支持上述语法，它们不允许 static 成员在其声明式上获得初值。
此外所谓的“in-class 初值设定”也只允许对整数常量进行。
如果编译器不支持上述语法，可以将初值放在定义式:

```c++
class CostEstimate {
private:
    static const double FudgeFactor;		//static class 常量声明
    // ...									//位于头文件内
};
const double CostEstimate::FudgeFactor = 1.35;	//static class 常量定义，位于实现文件内
```

万一编译器(错误地)不允许“static 整数型class 常量”完成“in class 初值设定”，可改用所谓的“the enum hack”补偿做法。

```c++
class GamePlayer {
private:
    enum { NumTurns = 5 };//"the enum hack"
    int scores[NumTurns];
    // ...
};
```



另一个常见的#define误用情况是以它**实现宏**(macros)。宏看起来像函数，但不会招致函数调用(function call)带来的额外开销。

```c++
//以a和b的较大值调用f
#define CALL_WITH_MAX(a, b) f((a) > (b) ? (a) : (b))

//替代方案：template inline 函数
template<typename T>
inline void calWithMax(const T& a, const T& b)		// pass by reference-to-const
{
    f( a > b ? a : b);
}
```

### 总结：

**对于单纯常量，最好以 const 对象或 enums 替换#defines。**
**对于形似函数的宏 (macros)，最好改用inline函数替换#defines。**



## 条款03:尽可能使用const

Use const whenever possible.

```c++
char greeting[] = "Hello";
char* p = greeting;				//non-const pointer, non-const data
const char* p = greeting;		//non-const pointer, const data
char* const p = greeting;		//const pointer, non-const data
const char* const p = greeting;	//const pointer, const data
```

如果关键字 const 出现在星号左边，表示被指物是常量
如果出现在星号右边，表示指针自身是常量
如果出现在星号两边，表示被指物和指针两者都是常量

如果被指物是常量
	将关键字 const 写在类型之前
	把它写在类型之后、星号之前

```c++
//pw获得一个指针，指向一个常量的(不变的)widget对象，f2也是
void f1(const Widget* pw);
void f2(Widget const * pw);
```

STL 迭代器系以指针为根据塑模出来，所以迭代器的作用就像个 T*指针

```c++
std::vector<int> vec;
// ...
const std::vector<int>::iterator iter = vec.begin();	//iter的作用像个T* const
*iter = 10;		//没问题，改变iter 所指物
++iter;			//错误! iter是const
std::vector<int>::const_iterator cIter = vec.begin();	//cIter的作用像个 const T*
*cIter = 10;	//错误!*cIter 是const
++cIter;		//没问题，改变 cIter
```



### const成员函数

将 const实施于成员函数的目的，是为了确认该成员函数可作用于 const 对象身上
	它们使 class 接口比较容易被理解
		这是因为，得知哪个函数可以改动对象内容而哪个函数不行，很是重要。
	它们使“操作 const 对象”成为可能。这对**编写高效代码**是个关键
		改善c++程序效率的一个根本办法是以 pass by reference-to-const方式传递对象
			而此技术可行的前提是，我们有const成员函数

两个成员函数如果只是常量性 (constness)不同，**可以被重载**

```c++
class TextBlock {
public:
    //...
    // non-const operator[] 的返回类型是个 reference to char
    const char& operator[](std::size_t position) const	 //operator[] for const 对象
    { return text[position]; }
    char& operator[](std::size_t position)				//operator[] for non-const 对象
    { return text[position]; }
private:
    std::string text;
};
```



成员函数如果是 const 意味着:
	**bitwise constness** (又称 physical constness)
		成员函数只有在不更改对象之任何成员变量(static除外)时才可以说是 const
	**logical constness**
		一个 const 成员函数可以修改它所处理的对象内的某些 bits，但只有在客户端侦测不出的情况下才得如此

```c++
class CTextBlock {
public:
    //...
    std::size_t length() const;
private:
    char* pText;
    std::size_t textLength;	//最近一次计算的文本区块长度
    bool lengthIsValid;		//目前的长度是否有效
};
std::size_t CTextBlock::length() const
{
    if (!lengthIsValid) {
        //错误!在const 成员函数内不能赋值给 textLength和lengthIsValid。
        textLength = std::strlen(pText);	
        lengthIsValid = true;
    }
    return textLength;
}
```

**mutable**释放掉 non-static 成员变量的 bitwise constness 约束

```c++
class CTextBlock {
public:
    // ...
    std::size_t length() const;
private:
    char* pText;
    mutable std::size_t textLength;
    mutable bool lengthIsValid;
};

std::size_t CTextBlock::length() const
{
    if (!lengthIsValid) {
        textLength = std::strlen(pText);		// 正确
        lengthIsValid = true;
    }
    return textLength;
}
```



令 non-const operator[]调用其 const兄弟是一个避免代码重复的**安全做法**一一即使过程中需要一个转型动作

```c++
class TextBlock {
public:
    //...
    const char& operator[](std::size_t position) const //一如既往
    {
        // ...
        return text[position];
    }
    char& operator[](std::size_t position)		//现在只调用 const op[]
    {
        return
            const_cast<char&>(			//将op[]返回值的const转除
            	static_cast<const TextBlock&>(*this)[position]		//为*this加上const
        	);
    }
};
```

两个转型动作：
	第一次用来为 *this 添加 const (这使接下来调用 operator[]时得以调用const版本)
	第二次则是从 const operator[]的返回值中移除 const

const 成员函数调用non-const 成员函数是一种错误行为

### 总结：

将某些东西声明为 const 可帮助编译器侦测出错误用法
	const 可被施加于任何作用域内的对象、函数参数、函数返回类型、成员函数本体
编译器强制实施 bitwise constness，但编写程序时应该使用“概念上的常量性”(conceptual constness) 
当const 和 non-const 成员函数有着实质等价的实现时
	令 non-const 版本调用 const版本可避免代码重复



## 条款04:确定对象被使用前已先被初始化

Make sure that objects are initialized before they're used.

确保每一个构造函数都将对象的每一个成员初始化

规定**总是在初值列中列出所有成员变量**，
	以免还得记住哪些成员变量(如果它们在初值列中被遗漏的话)可以无需初值

构造函数的一个较佳写法是，使用所谓的 member initialization list (**成员初值列**)替换赋值动作:

```c++
ABEntry::ABEntry(const std::string& name, const std::string& address, 
                 const std::list<PhoneNumber>& phones)
    :theName (name),				//现在，这些都是初始化 (initializations)
	theAddress (address),
	thePhones (phones),
	numTimesConsulted(0)
    { }			//现在，构造函数本体不必有任何动作
```

比起先调用 default构造函数然后再调用 copy assignment操作符，单只调用一次 copy 构造函数是比较高效的，有时甚至高效得多



C++ 有着十分固定的“成员初始化次序”
	base classes更早于其 derived classes 被初始化(见条款 12)
	而 class 的成员变量总是以其声明次序被初始化
当在成员初值列中条列各个成员时，最好总是以其声明次序为次序



### 不同编译单元内定义之non-local static对象的初始化次序

**static 对象**
其寿命从被构造出来直到程序结束为止，因此 stack 和heap-based 对象都被排除
这种对象包括
	global对象
	定义于namespace作用域内的对象
	在 classes 内、在函数内、以及在 file 作用域内被声明为 static的对象

函数内的static对象称为 local static 对象(因为它们对函数而言是 local)
其他static对象称为 non-local static 对象
程序结束时 static 对象会被自动销毁，也就是它们的析构函数会**在main()结束时被自动调用**

**编译单元 (translation unit)**
指产出单一目标文件 (single object file)的那些源码
基本上它是单一源码文件加上其所含入的头文件 (#include files)

> 如果某编译单元内的某个non-local static 对象的初始化动作使用了另一编译单元内的某个 non-local static对象，它所用到的这个对象可能尚未被初始化，因为 C++ 对“定义于不同编译单元内的non-local static 对象”的初始化次序并无明确定义

```c++
class FileSystem {		//来自你的程序库
public:
    std::size_t numDisks() const;	//众多成员函数之一
};
extern FileSystem tfs;	//预备给客户使用的对象

class Directory { 		//由程序库客户建立
public:
	Directory( params );
};
Directory::Directory( params )
{
    //除非 tfs 在 tempDir之前先被初始化
    // 否则temoDir的构造函数会用到尚未初始化的tfs
    std::size_t disks = tfs.numDisks();		//使用tfs对象
}

//使用singleton模式
class FileSystem { ...};
FileSystem& tfs(){
    //任何一种non-const static 对象，不论它是local或non-local，
    // 在多线程环境下“等待某事发生”都会有麻烦
    static FileSystem fs;
	return fs;
}
class Directory { ... };
Directorv::Directory( params)
{
    std::size t disks = tfs().numDisks( );
}
Directorys& tempDir()
{
    static Directory td;
    return td;
}
```

### 总结：

- 为内置型对象进行手工初始化，因为 C++不保证初始化它们
- 构造函数最好使用成员初值列(member initialization list)
  而不要在构造函数本体内使用赋值操作(assignment)
  初值列列出的成员变量，其排列次序应该和它们在 class 中的声明次序相同
- 为免除“跨编译单元之初始化次序”问题，请以local static 对象替换 non local static 对象



# 构造/析构/赋值运算

## 条款 05:了解 C++ 默默编写并调用哪些函数

Know what functions C++ silently writes and calls.

编译器就会为**空类**声明(编译器版本的)
	一个copy构造函数
	一个copy assignment操作符
	一个析构函数
	一个 default构造函数
所有这些函数都是 public且inline
惟有当这些函数被需要(被调用)，它们才会被编译器创建出来
编译器产出的析构函数是个nonvirtual(见条款7)，
	除非这个class的base class自身声明有virtual析构函数

```c++
class Empty { };
//编译器处理后
class Empty {
public:
    Empty() { /* ... */ };
    Empty(const Empty& rhs) { /* ... */ };
    ~Empty() { /* ... */ };
    Empty& operator=(const Empty& rhs) { /* ... */ };
}；
```

如果打算在一个“**内含reference成员**”的class内**支持赋值操作**(assignment)，必须自己定义 copy assignment操作符

### 总结：

编译器可以暗自为class创建default构造函数、copy构造函数、copy assignment 操作符，以及析构函数



## 条款 06:若不想使用编译器自动生成的函数，就该明确拒绝

Explicitly disallow the use of compiler-generated functions you do not want

可以将copy构造函数或copy assignment操作符声明为private
	由明确声明一个成员函数，阻止了编译器暗自创建其专属版本
	而令这些函数为 private，成功阻止人们调用它

```c++
class HomeForSale{
public:
    // ...
private:
    HomeForSale(const HomeForSale&);			//只有声明
    HomeForSales operator=(const HomeForSale&);
};

class Uncopyable {
protected:			//允许 derived 对象构造和析构
    Uncopyable() {}
    ~Uncopyable() {}
private:
    Uncopyable(const Uncopyables);			//但阻止 copying
    Uncopyable& operator=(const Uncopyable&);
};
```

### 总结：

为驳回编译器自动(暗自)提供的机能，可将应的成员函数声明为 private 并且不予实现
	使用像 Uncopyable这样的 base class 也是一种做法



## 条款07:为多态基类声明virtual析构函数

Declare destructors virtual in polymorphic base classes.

C++ 明白指出：
	当derived class 对象经由一个base class指针被删除，而该base class 带着一个**non-virtual析构函数**
		其结果未有定义
实际执行时通常发生的是对象的 derived 成分没被销毁

如果 class 不含 virtual 函数，通常表示它并不意图被用做一个 base class
当 class不企图被当作base class，令其析构函数为virtual往往是个馊主意

欲实现出 virtual 函数，对象必须携带某些信息，主要用来在运行期决定哪一个virtual函数该被调用

有时候令class带一个pure virtual析构函数可能颇为便利
	pure virtual函数导致 abstract (抽象) classes也就是不能被实体化 (instantiated)的class

```c++
class AWOV{
public:
    virtual ~AWOV() = 0;	//声明pure virtual析构函数
};
```

有一个 pure virtual函数，所以它是个抽象class
又由于它有个 virtual析构函数，所以你不需要担心析构函数的问题
必须为这个pure virtual析构函数提供一份定义:

```c++
AWOV::~AWOV()  {} //pure virtual析构函数的定义
```

### 总结：

- polymorphic(带多态性质的) base classes 应该声明一个 virtual 析构函数。如果class 带有任何 virtual函数，它就应该拥有一个 virtual析构函数。
- Classes 的设计目的如果不是作为 base classes 使用，或不是为了具备多态性(polymorphically)，就不该声明virtual析构函数。



## 条款08:别让异常逃离析构函数

Prevent exceptions from leaving destructors

只要析构函数吐出异常，即使并非使用容器或 arrays，程序也可能过早结束或出现不明确行为

```c++
class DBConn {
public:
    void close()		//供客户使用的新函数
    {
        db.close( );
        closed = true;
    }
    ~DBConn()
    {
        if (!closed) {
            try {		//关闭连接(如果客户不那么做的话)
                db.close( );
            }
        } catch (...) {								 //如果关闭动作失败，		
            // 制作运转记录, 记下对close的调用失败		// 记录下来并结束程序
        }											 // 或吞下异常。
    }
private:
	DBConnection db;
	bool closed;
};
```

如果某个操作可能在失败时抛出异常，而又存在某种需要必须处理该异常，那么这个异常必须来自析构函数以外的某个函数

### 总结：

- 析构函数绝对不要吐出异常。如果一个被析构函数调用的函数可能抛出异常，析构函数应该捕捉任何异常，然后吞下它们(不传播) 或结束程序。
- 如果客户需要对某个操作函数运行期间抛出的异常做出反应，那么 class 应该提供一个普通函数(而非在析构函数中)执行该操作。



## 条款09:绝不在构造和析构过程中调用virtual函数

Never call virtual functions during construction or destruction.

在base class 构造期间，virtual函数不是virtual函数
	由于base class构造函数的执行更早于derived class构造函数
	当base class构造函数执行时derived class的成员变量尚未初始化
在 derived class 对象的 base class 构造期间，对象的类型是 base class 而不是 derived class

相同道理也适用于析构函数 

### 总结：

在构造和析构期间不要调用virtual函数
	因为这类调用从不下降至derived class(比起当前执行构造函数和析构函数的那层)



## 条款10:令operator= 返回一个 reference to *this

Have assignment operators return a reference to *this

为了实现“连锁赋值”，赋值操作符必须返回一个 reference 指向操作符的左侧实参。

### 总结：

令赋值 (assignment)操作符返回一个reference to *this



## 条款11:在operator= 中处理“自我赋值

Handle assignment to self in operator=

```c++
class Widget { ... };
Widget w;
W = W;	//赋值给自己
```

```c++
Widget& Widget;:operator=(const Widget& rhs)	//一份不安全的operator= 实现版本
{
    delete pb;
    pb = new Bitmap(*rhs.pb);
    return *this;
}
// 检验自赋值
Widget& Widget::operator=(const Widget& rhs)
{
    if (this == &rhs) return *this;
    delete pb;
    // 如果“new Bitmap”copy构造函数抛出异常)，Widget 最终会持有一个指针指向一块被删除的Bitmap。
    pb = new Bitmap(*rhs.pb) ;
    return *this;
}
Widget& Widget::operator=(const widget& rhs)
{
    Bitmap* pOrig = pb;
    pb = new Bitmap(*rhs.pb);
    delete pOrig;
    return *this;
}
// 使用 copy and swap 技术
```

### 总结：

- 确保当对象自我赋值时 operator= 有良好行为。其中技术包括比较“来源对象和“目标对象”的地址、精心周到的语句顺序、以及 copy-and-swap
- 确定任何函数如果操作一个以上的对象，而其中多个对象是同一个对象时，其行为仍然正确



## 条款12:复制对象时勿忘其每一个成分

Copy all parts of an object.

当你编写一个 copying函数，请确保
	(1) 复制所有 local 成员变量
	(2) 调用所有 base classes 内的适当的copying函数

### 总结：

- Copying函数应该确保复制“对象内的所有成员变量”及“所有 base class 成分
- 不要尝试以某个copying函数实现另一个 copying函数
  应该将共同机能放进第三个函数中，并由两个 coping函数共同调用



# 资源管理

## 条款13:以对象管理资源

Use objects to manage resources.

```c++
class Investment { /*...*/ };		//“投资类型” 继承体系中的root class

//假设这个程序库系通过一个工厂函数 (factory function，见条款7)供应我们某特定的Investment 对象:
//返回指针，指向 Investment 继承体系内的动态分配对象，调用者有责任删除它
Investment* createInvestment();	
				
void f()
{
    Investment* pInv = createInvestment( );	//调用 factory 函数
    // 随时可能终止
    delete pInv;		//释放pInv所指对象
}
// 应该在控制流离开那个区块或函数时被释放
// 标准程序库提供的 auto_ptr 正是针对这种形势而设计的特制产品
void f()
{
    //auto_ptrs有一个不寻常的性质:
    // 若通过copy构造函数或copy assignment操作符复制它们，它们会变成null
    // 而复制所得的指针将取得资源的唯一拥有权
    std::auto_ptr<Investment> pInv(createInvestment());
    //调用 factory 函数
    //一如以往地使用pInv
    //经由auto_ptr的析构函数自动删除pInv
}
```

- 获得资源后立刻放进管理对象
  "以对象管理资源"的观念常被称为“资源取得时机便是初始化时机” (Resource Acquisition Is Initialization; RAIl)
- 管理对象(managing object)运用析构函数确保资源被释放
- 

auto_ptr的替代方案是“引用计数型智慧指针”(reference-counting smart pointer；RCSP)
	所谓 RCSP 也是个智能指针，持续追踪共有多少对象指向某笔资源，并在无人指向它时自动删除该资源

### 总结：

- 为防止资源泄漏，请使用 RAII对象，它们在构造函数中获得资源并在析构函数中释放资源
- 两个常被使用的RAII classes 分别是 tr1::shared_ptr和auto_ptr
  前者通常是较佳选择，因为其 copy行为比较直观
  若选择 auto_ptr,复制动作会使它(被复制物)指向null



## 条款14:在资源管理类中小心coping 行为

Think carefully about copying behavior in resource-managing classes.

```c++
void lock(Mutex* pm);		//锁定pm所指的互斥器
void unlock(Mutex* pm) ;	//将互斥器解除锁定

// 建立一个 class用来管理机锁
class Lock {
public:
    explicit Lock(Mutex* pm): mutexPtr(pm)
    { lock(mutexPtr); }		//获得资源
    ~Lock() { unlock(mutexPtr); }	//释放资源
private:
	Mutex *mutexPtr;
};
//修改

```

当一个 RAII 对象被复制，会发生什么事?
	禁止复制
	对底层资源祭出“引用计数法”(reference-count)
	复制底部资源
	转移底部资源的拥有权

### 总结：

- 复制 RAII对象必须一并复制它所管理的资源
  所以资源的 copying 行为决定RAII对象的copying行为
- 普遍而常见的 RAII class copying 行为是:抑制 copying、施行引用计数法(reference counting)。不过其他行为也都可能被实现



## 条款15:在资源管理类中提供对原始资源的访问

Provide access to raw resources in resource-managing classes.

许多 APIS 直接指涉资源，所以除非永不录用这样的APIS，
	否则只得绕过资源管理对象 (resource-managing obiects)直接访问原始资源 (raw resources)

```c++
std::tr1::shared_ptr<Investment> pInv(createInvestment());	//见条款13
int daysHeld(const Investment* pi);		//返回投资天数
int days = daysHeld(pInv);				//错误!
//将 RAII class 对象(本例为 tr1::shared_ptr)转换为其所内含之原始资源
int days = daysHeld(pInv.get());		//很好，将pInv内的原始指针,传给 daysHeld
```

tr1::shared_ptr和auto_ptr都提供一个 get 成员函数
	用来执行显式转换也就是它会返回智能指针内部的原始指针(的复件) :

tr1::shared_ptr 和 auto_ptr 也重载了指针取值(pointer dereferencing)操作符 (operator->和 operator*)，
	它们允许隐式转换至底部原始指针

是否该提供一个显式转换函数(例如 get 成员函数)将 RAII cass 转换为其底部资源，或是应该提供隐式转换，答案主要取决于RAI class 被设计执行的特定工作，以及它被使用的情况。

### 总结：

- APIs 往往要求访问原始资源 (raw resources)
  所以每一个RAII class 应该提供一个“取得其所管理之资源”的办法
- 对原始资源的访问可能经由显式转换或隐式转换
  一般而言显式转换比较安全但隐式转换对客户比较方便



## 条款16:成对使用new和delete时要采取相同形式

Use the same form in corresponding uses of new and delete.

如果调用 new 时使用[]，你必须在对应调用 delete 时也使用 []
如果调用new 时没有使用[]，那么也不该在对应调用 delete 时使用[]

```c++
std::string* stringPtr1 = new std::string;
std::string* stringPtr2 = new std::string[100];

delete stringPtr1;		//删除一个对象
delete [] stringPtr2;	//删除一个由对象组成的数组
```

typedef 的作者必须说清楚，当程序员以 new 创建该种 typedef 类型对象时，该以哪一种 delete形式删除

```c++
typedef std::string AddressLines[4];		//每个人的地址有4行，每行是一个string
std::string* pal = new AddressLines;
delete pal;		//行为未有定义!
delete [] pal;	//很好。
```

### 总结：

如果在new表达式中使用[]，必须在相应的delete表达式中也使用[]
如果在new表达式中不使用[]，一定不要在相应的delete表达式中使用[]



## 条款17:以独立语句将 new ed 对象置入智能指针

Store newed objects in smart pointers in standalone statements.

```c++
int priority();
void processWidget(std::tr1::shared_ptr<widget> pw, int priority);
//无法通过编译
// tr1::shared_ptr构造函数需要一个原始指针(raw pointer)，但该构造函数是个explicit构造函数
processWidget(new Widget, priority());

//可以通过编译
// 调用可能泄漏资源
processWidget(std::tr1::shared_ptr<Widget>(new Widget), priority());
```

processWidget需要做以下三个事情：

- 调用 priority
- 执行“new widget"
- 调用 tr1::shared ptr构造函数

一个可能的顺序：

- 执行“new widget"
- 调用 priority
- 调用 trl::shared ptr 构造函数

如果priority函数调用异常，则会**资源泄漏**

避免这类问题：

```c++
std::tr1::shared_ptr<Widget> pw(new Widget);
processWidget(pw, priority());//这个调用动作绝不至于造成泄漏
```

### 总结：

以独立语句将newed 对象存储于(置入)智能指针内
	如果不这样做，一旦异常被抛出，有可能导致难以察觉的资源泄漏



# 设计与声明

## 条款18:让接口容易被正确使用，不易被误用

Make interfaces easy to use correctly and hard to use incorrectly

function 接口、class 接口、template 接口······每一种接口都是客户与你的代码互动的手段

```c++
//假设你为一个用来表现日期的 class 设计构造函数
class Date {
public:
    Date(int month, int day, int year);
};
Date d(30, 3, 1995);		// 以错误的次序传递参数
Date d(2, 30, 1995);		// 传递一个无效的月份或天数
```

导入简单的外覆类型(wrapper types)来区别天数、月份和年份，然后于 Date构造函数中使用这些类型:

```c++
struct Day {
    explicit Day(int d) : val(d){ }
    int val;
};

struct Month {
    explicit Month(int m): val(m) { }
	int val;
};

struct Year {
    explicit Year(int y) : val(y) {}
    int val;
};

class Date {
public:
    Date(const Month& m, const Day& d, const Year& y);
};
Date d(30, 3, 1995);					//错误!不正确的类型
Date d(Day(30), Month(3), Year(1995));	//错误!不正确的类型
Date d(Month(3), Day(30), Year(1995));	//OK类型正确

// 比较安全的解法是预先定义所有有效的Months:
class Month {
public:
    static Month Jan() { return Month(1); }
    static Month Feb() { return Month(2); }
    // ...
    static Month Dec() { return Month(12); }
private:
    explicit Month(int m);	//阻止生成新的月份
};
Date d(Month::Mar(), Day(30), Year(1995));
```

限制类型内什么事可做，什么事不能做

```c++
//以 const 修饰 operator* 的返回类型”可阻止客户因“用户自定义类型”而犯错
if (a * b = c)
    //...
```

让 types 容易被正确使用，不容易被误用
	除非有好理由，否则应该尽量令 types 的行为与内置types 一致

任何接口如果要求客户必须记得做某些事情，就是有着“不正确使用”的倾向，因为客户可能会忘记做那件事。

```c++
//至少开启了两个客户错误机会
// 没有删除指针
// 删除同一个指针超过一次
Investment* createInvestment();
//To
std::tr1::shared_ptr<Investment> createInvestment();

std::tr1::shared_ptr<Investment> createInvestment()
{
    // getRidOfInvestment 删除函数
    std::tr1::shared_ptr<Investment> retVal(
        static_cast<Investment* >(0), getRidOfInvestment);
    retVal = /*...*/;		//令 retVal指向正确对象
    return retVal;
}
```

cross-DLL problem：
	这个问题发生于“对象在动态连接程序库(DLL)中被 new创建，却在另一个 DLL 内被 delete销毁”
tr1::shared_ptr没有这个问题

### 总结：

- 好的接口很容易被正确使用，不容易被误用，你应该在你的所有接口中努力达成这些性质
- “促进正确使用”的办法包括接口的一致性，以及与内置类型的行为兼容
- “阻止误用”的办法包括建立新类型、限制类型上的操作，束缚对象值，以及消除客户的资源管理责任
- tr1::shared_ptr支持定制型删除器 (custom deleter)。这可防范DLL问题，可被用来自动解除互斥锁(mutexes；见条款14)等等



## 条款19:设计 class 犹如设计 type

Treat class design as type design.

身为 C++ 序员，许多时间主要用来扩张类型系统 (typesystem)
这意味并不只是 class 设计者，还是type 设计者
	重载 (overloading)函数和操作符、控制内存的分配和归还、定义对象的初始化和终结
因此应该带着和“**语言设计者当初设计语言内置类型时**”一样的谨慎来研讨 class 的设计

面对以下提问：

- **新 type的对象应该如何被创建和销毁?**
  这会影响到你的 class 的**构造函数和析构函数以及内存分配函数和释放函数**(operator new, operator new[], operator delete和operator delete[])的设计，当然前提是如果打算撰写它们。
- **对象的初始化和对象的赋值该有什么样的差别?** 
  这个答案决定你的**构造函数和赋值(assignment)操作符的行为**，以及其间的差异
  很重要的是区别了“初始化和“赋值”，因为它们对应于不同的函数调用 (见条款4)
- **新type的对象如果被passed by value(以值传递)，意味什么?**
  记住，**copy构造函数**用来定义一个type的 pass-by-value该如何实现。
- **什么是新 type 的“合法值”?**
  对 class 的成员变量而言，通常只有某些数值集是有效的
- **新type 需要配合某个继承图系 (imheritance graph)吗?**
  如果继承自某些有的 classes，就受到那些 classes 的设计的束缚
  如果允许其他classes 继承你的class，那会影响所声明的函数，尤其是析构函数是否为 virtual(见条款7)
- **你的新 type 需要什么样的转换?** 
  如果希望允许类型 T1之物被隐式转换为类型T2
  	就必须在 class T1内写一个类型转换函数 (operator T2)
  	或在 class T2内写一个non-explicit-one-argument (可被单一实参调用)的构造函数
  如果只允许explicit构造函数存在
  	就得写出专门负责执行转换的函数
  	且不得为类型转换操作符(typeconversion operators)或non-explicit-one-argument 构造函数
  	(条款15有隐式和显式转换函数的范例)
- **什么样的操作符和函数对此新 type 而言是合理的?** 
  这个问题的答案决定将为class 声明哪些函数。其中某些该是 member 函数，某些则否(见条款232446)
- **什么样的标准函数应该驳回?** 
  那些正是必须声明为 private 者(见条款6)
- **谁该取用新 type的成员?**
  这个提问可以帮助你决定哪个成员为 public，哪个为protected，哪个为 private
  它也帮助你决定哪一个 classes 和/或 functions 应该是fiends，以及将它们嵌套于另一个之内是否合理
- **什么是新 type的“未声明接口” (undeclared interface)?**
  它对效率、异常安全性(见条款29)以及资源运用(例如多任务锁定和动内存)提供何种保证?
  在这些方面提供的保证将为 class 实现代码加上相应的约束条件
- **新type有多么一般化?**
  或许其实并非定义一个新type，而是定义一整个types家族
  果真如此就不该定义一个新 class，而是应该定义一个新的 class template
- **真的需要一个新 type 吗?**
  如果只是定义新的derived class 以便为既有的class 添加机能
  那么说不定单纯定义一或多个 non-member 函数或templates，更能够达到目标

### 总结：

Class 的设计就是 type 的设计。在定义一个新 ype 之前，请确定你已经考虑过本条款覆盖的所有讨论主题



## 条款20:宁以pass-by-reference-to-const 替换 pass-by-value

Prefer pass-by-reference-to-const to pass-by-value.

缺省情况下C++ 以 by value方式 (一个继承自C的方式)传递对象至(或来自) 函数。
	参数的传递成本是“一次copy构造函数调用，加一次析构函数调用”

如果窥视 C++ 编译器的底层
	references 往往以指针实现出来，因此pass by reference**通常意味真正传递的是指针**
因此如果有个对象属于**内置类型**(例如int)
	pass by value往往比 pass by reference的效率高些
也适用于 STL 的选代器和函数对象，因为习惯上它们都被设计为passed by value
	迭代器和函数对象的实践者有责任看看它们是否高效且不受切割问题(slicing problem)的影响
		这是“规则之改变取决于你使用哪一部分C++(见条款1)”的一个例子

一般而言，你可以合理假设“pass-by-value 并不昂贵”的唯一对象就是**内置类型**和**STL的选代器**和**函数对象**
至于其他任何东西都请遵守本条款的忠告，尽量以pass-by-reference-to-const 替换pass-by-value

### 总结：

- 尽量以pass-by-reference-to-const 替换 pass-by-value
  前者通常比较高效，并可避免切割问题(slicing problem)
- 以上规则并**不适用**于**内置类型**，以及 **STL 的迭代器**和**函数对象**
  对它们而言pass-by-value往往比较适当



## 条款21:必须返回对象时，别妄想返回其reference

Don't try to return a reference when you must return an object.

函数创建新对象的途径有二：
	在 stack 空间或在 heap 空间创建
如果定义一个local变量，就是在stack 空间创建对象，local对象在函数退出前被销毁了

```c++
inline const Rational operator * (const Rational& lhs, const Rational& rhs)
{
    return Rational(lhs.n * rhs.n, lhs.d * rhs.d);
}
```

### 总结：

绝不要返回 pointer 或reference 指向一个 **loca stack** 对象，
或返回 reference 时指向个 **heap-allocated** 对象，
或当有可能同时需要多个这样的对象时，返回 pointer 或 reference 时指向一个 **local static** 对象
条款4已经为“在单线程环境中合理返回 reference指向一个 local static 对象”提供了一份设计实例



## 条款22:将成员变量声明为private

Declare data members private.

- 语法一致性(条款 18)
  如果成员变量不是 public，客户唯一能够访问对象的办法就是通过成员函数，调用时总是使用小括号
- 使用函数可以对成员变量的处理有更精确的控制
- 封装
  如果通过函数访问成员变量，日后可改以某个计算替换这个成员变量
  而 class 客户一点也不会知道 class 的内部实现已经起了变化
  成员变量的封装性与“成员变量的内容改变时所破坏的代码数量”成反比
  private(提供封装)和其他(不提供封装)

### 总结：

- 切记将成员变量声明为 private
  这可赋予客户访问数据的一致性、可细微划分访问控制、允诺约束条件获得保证
  并提供 class 作者以充分的实现弹性
- protected 并不比public 更具封装性



## 条款23:宁以non-member、non-friend 替换member函数

Prefer non-member non-friend functions to member functions.

```c++
class WebBrowser{
public:
	void clearCache();
    void clearHistory();
    void removeCookies();    
};

class WebBrowser{
public:
    void clearEverything();	//调用 clearCache, clearHistory 和 removeCookies
};
//Or
void clearBrowser(WebBrowser& wb)
{
    wb.clearCache();
    wb.clearHistory();
    wb.removeCookies();
}
```

愈多函数可访问的数据，数据的封装性就愈低
	friends函数对class private 成员的访问权力和member 函数相同，因此两者对封装都有负面影响
封装性而让函数“成为class的non-member，并不意味它“不可以是另一个 class 的 member”

标准程序库并不是拥有单一、整体庞大的 <C++ standard library> 头文件，并在其中内含 std 命名空间内的每一样东西
	而是有数十个头文件(`<vector>,<algorithm>,<memory>`等等)，每个头文件声明 std 的某些机能
	如果客户只想使用 vector 相关机能，不需要 #include <memory>

### 总结：

宁可拿non-membernon-friend函数替换member函数
	这样做可以增加封装性、包裹弹性(packaging flexibility)和机能扩充性



## 条款 24:若所有参数皆需类型转换，请为此采用non-member函数

Declare non-member functions when type conversions should apply to all parameters.

```c++
class Rational {
public:
    //构造函数刻意不为explicit;允许int-to-Rational隐式转换。
    Rational(int numerator = 0, int denominator = 1);
    int numerator() const;			//分子(numerator)和分母(denominator)
    int denominator() const;		//的访问函数 (accessors)-见条款 22。
    
    //创建一个乘法操作
    // 返回一个const by-value 结果但接受一个 reference-toconst实参，请参考条款3,20和21
    // 只支持result = oneHalf * 2;
    // 不支持result = 2 * oneHalf;
    const Rational operator* (const Rational& rhs) const;
private:
    // ...
};

//将乘法操作变为 non-member函数
const Rational operator*(const Rational& lhs, const Rational& rhs)
{
    return Rational(
        lhs.numerator() * rhs.numerator(), 
        lhs.denominator() * rhs.denominator()
    );
}
// operator* 不应该成为Rational class 的一个 fiend 函数
// 无论何时如果可以避免 fiend 函数就该避免
```

### 总结：

如果需要为某个函数的所有参数(包括被 ths 指针所指的那个隐喻参数)进行类型转换
	那么这个函数必须是个 non-member



## 条款 25:考虑写出一个不抛异常的 swap 函数

Consider support for a non-throwing swap

**讨论**default swap、member swaps、non-member swaps、std::swap特化版本、以及对 swap的调用

所谓swap(置换)两对象值，意思是将两对象的值彼此赋予对方

```c++
namespace std {
    template<typename T>			//std::swap 的典型实现
    void swap( T& a, T& b)			//置换a和b的值
    {
        T temp(a);
        a = b;
        b = temp;
    }
}
```

如果swap的缺省实现码对 class 或class template 提供可接受的效率，不需要额外做任何事
	任何尝试置换 (swap)那种对象的人都会取得缺省版本，而那将有良好的运作

如果 swap 缺省实现版的效率不足(那几乎总是意味你的 cass 或 template使用了某种 pimpl 手法)：

- 提供一个public swap成员函数，让它高效地置换你的类型的两个对象值。这个函数绝不该抛出异常
- 在class或template所在的命名空间内提供一个non-member swap，并令它调用上述 swap 成员函数
- 如果正编写一个 class (而非 class template)，为你的 class 特化 std::swap。并令它调用你的 swap成员函数。

调用swap：
	请确定包含一个using声明式，以便让 std::swap在函数内曝光可见
	然后不加任何 namespace修饰符，赤裸裸地调用 swap

想让“class 专属版”swap在尽可能多的语境下被调用
	需得同时在**该class所在命名空间**内写一个**non-member 版本**以及一个 **std::swap特化版本**

**成员版 swap 绝不可抛出异常**



```c++
// 以指针指向一个对象，内含真正数据”那种类型
// 这种设计的常见表现形式是所谓“pimpl手法”(pimpl是"pointer to implementation”的缩写)
class WidgetImpl {		//针对 widget 数据而设计的 class;
public:
    // ...
private:
    // ...				//可能有许多数据
};

//要置换两个 Widget 对象值，我们唯一需要做的就是置换其 pImp 指针，但缺省的 swap 算法不知道这一点
class Widget {
public:
    Widget(const Widget& rhs);
    Widgets operator=(const widget& rhs)
    {
        //...
        *pImpl = *(rhs.pImpl);	//复制widget 时，令它复制其 WidgetImpl对象
        //...
    }
private:
	WidgetImpl* pImpl;
};

// 令 widget 声明一个名为 swap 的 public 成员函数做真正的置换工作
// 然后将 std::swap特化，令它调用该成员函数
class Widget {								//与前同，唯一差别是增加 swap 函数
public:
    void swap(Widget& other){
        using std::swap;					//这个声明之所以必要，稍后解释。
        swap(pImpl, other.pImpl);			//若要置换 widgets 就置换其pImpl指针
    }
};
namespace std {								//修订后的 std::swap特化版本
    template<>
    void swap<Widget>(Widget& a, Widget& b)
    {
        a.swap(b);							//若要置换widgets，调用其swap成员函数。
    }
}
```

```c++
//假设 Widget 和widgetImpl都是 class templates 而非 classes
// 偏特化，错误的， C++ 只允许对 class templates 偏特化，function templates 不能偏特化
namespace std {
    template<typename T>
    void swap< Widget<T> >(Widget<T>& a, Widget<T>& b)	//错误!不合法!
    { a.swap(b); }
} 
// 错误的，可以全特化std内的templates，不可以添加新的templates
namespace std {
    template<typename T>
    void swap(Widget<T>& a, Widget<T>& b)	// "swap”之后没"<...>"
    {
        a.swap(b);
    }
}
// 正确的，将偏特化的模板声明到自己的命名空间
namespace WidgetStuff {
    template<typename T>
    void swap(Widget<T>& a, Widget<T>& b)
    {
        a.swap(b);
    }
}
```

```c++
//正确调用
template<typename T>
void doSomething(T& obj1, T& obj2)
{
    using std::swap;	//令 std::swap在此函数内可用
    //...
    swap(obj1, obj2);	//为T型对象调用最佳swap版本
    //...
}
```

总结：

- 当 std::swap 对类型效率不高时，提供一个 swap 成员函数，并确定这个函数不抛出异常
- 如果提供一个member swap，也该提供一个non-member swap用来调用前者
  对于 classes (而非 templates)，也请特化 std::swap
- 调用swap时应针对std::swap使用using声明式，然后调用swap并且不带任何“命名空间资格修饰”
- 为“用户定义类型”进行 std templates 全特化是好的，但千万不要尝试在std内加入某些对std而言全新的东西



# 实现

## 条款26:尽可能延后变量定义式的出现时间

Postpone variable definitions as long as possible.

不只应该延后变量的定义，直到非得使用该变量的前一刻为止，
甚至应该尝试延后这份定义直到能够给它初值实参为止
	如果这样，不仅能够避免构造(和析构)非必要对象，还可以避免无意义的 default构造行为
	更深一层说，以“具明显意义之初值”将变量初始化，还可以附带说明变量的目的

```c++
//方法A:定义于循环外
Widget w;
for (int i = 0; i < n; ++i) {
    w = 取决于的某个值;
}

//方法B:定义于循环内
for (int i = 0; i < n; ++i) {
    Widget w(取决于的某个值);
}

//如果 classes的一个赋值成本低于一组构造+析构成本，做法A大体而言比较高效，尤其当n值很大的时候。否则做法 B 或许较好。
```

### 总结：

尽可能延后变量定义式的出现。这样做可增加程序的清晰度并改善程序效率。



## 条款27:尽量少做转型动作

Minimize casting

```c++
//转型语法
// 旧型转换
(T)expression;			//C 风格的转型动作
T(expression);			//函数风格的转型动作
// 新型转换
const_cast<T>(expression);
dynamic_cast<T>(expression);
reinterpret_cast<T>(expression);
static_cast<T>(expression);
```

- **const_cast**通常被用来将对象的常量性转除 (cast away the constness)
  它也是唯一有此能力的C++-style 转型操作符
- **dynamic_cast**主要用来执行“安全向下转型”(safe downcasting)
  用来决定某对象是否归属继承体系中的某个类型
  它是唯一无法由旧式语法执行的动作，也是唯一可能耗费重大运行成本的转型动作
- **reinterpret_cast** 意图执行低级转型
  实际动作(及结果)可能取决于编译器，这也就表示它不可移植
  例如将一个 pointer to int 转型为一个 int。这一类转型在低级代码以外很少见
- **static_cast**用来强迫隐式转换 (implicit conversions)
  例如将 non-const对象转为 const对象(就像条款3 所为)，或将 int 转为 double等等
  它也可以用来执行上述多种转换的反向转换
  例如将 void* 指针转为 typed 指针，将pointer-to-base 转为 pointer-to-derived
  但它无法将 const转为 non-const，这个只有 const cast 才办得到

如果发现打算转型，那活脱是个警告信号:
	可能正将局面发展至错误的方向上，如果用的是 dynamic_cast 更是如此

什么时候需要 dynamic_cast？
	通常是因为想在一个认定为 derived class 对象身上执行derived class操作函数
	但手上却只有一个“指 base”的 pointer或reference，只能靠它们来处理对象
有两个一般性做法可以避免这个问题
	使用容器并在其中存储直接指向 derived class 对象的指针
	在 base class 内提供 virtual函数 做想对各个派生类做的事

绝对必须避免的一件事是所谓的“连串 (cascading) dynamic casts”:

```c++
class Window {  /*...*/ };			//derived classes 定义在这里
typedef std::vector<std::tr1::shared_ptr<window> > VPW;
VPW winPtrs;
for(VPw::iterator iter = winPtrs.begin(); iter != winPtrs.end(); ++iter)
{
    if (Specialwindow1 * psw1 = dynamic_cast<SpecialWindow1*>(iter->get())) { /*...*/ }
    else if (Specialwindow2 * psw2 = dynamic_cast<SpecialWindow2*>(iter->get())) {  }
    else if (Specialwindow3 * psw3 = dynamic_cast<SpecialWindow3*>(iter->get())) {  }
    //... 
}
```

### 总结：

- 如果可以，尽量避免转型，特别是在注重效率的代码中避免 dynamic_casts
  如果有个设计需要转型动作，试着发展无需转型的替代设计
- 如果转型是必要的，试着将它隐藏于某个函数背后
  客户随后可以调用该函数而不需将转型放进他们自己的代码内
- 宁可使用 C++-style(新式)转型，不要使用旧式转型
  前者很容易辨识出来而且也比较有着分门别类的职掌



## 条款 28:避免返回 handles 指向对象内部成分

Avoid returning "handles" to object internals.

References、指针和选代器统统都是所谓的 handles (号码牌，用来取得某个对象)
而返回一个“代表对象内部数据”的handle，随之而来的便是“降低对象封装性”的风险

成员变量的**封装性**最多只等于“返回其reference”的**函数的访问级别**
如果const成员函数传出一个reference，后者所指数据与对象自身有关联，而它又被存储于对象之外，那么这个函数的调用者可以修改那笔数据references

### 总结：

避免返回handles (包括 references、指针、选代器)指向对象内部。
遵守这个条款可增加封装性，帮助 const 成员函数的行为像个 const，并将发生“虚吊号码牌”(dangling handles)的可能性降至最低



## 条款 29:为“异常安全”而努力是值得的

Strive for exception-safe code.

当异常被抛出时，带有异常安全性的函数会：

- **不泄漏任何资源**
- **不允许数据败坏**

```c++
//有个互斥器(mutex)作为并发控制(concurrency control)之用
class PrettyMenu {
public:
    void changeBackground(std::istream& imgSrc);		//改变背景图像
private:
    Mutex mutex;				//互斥器
    Image* bgImage;				//目前的背景图像
    int imageChanges;			//背景图像被改变的次数
};

//一旦“newImage(imgSrc)”致异常，对 unlock的调用就绝不会执行，于是互斥器就永远被把持住了
//如果“new Image(imgSrc)”抛出异常，bgImage就是指向-个已被删除的对象，
// imagechanges也已被累加，而其实并没有新的图像被成功安装起来
void PrettyMenu::changeBackground(std::istream& imgSrc)
{
    lock(&mutex)					//取得互斥器
	delete bgImage;					//摆脱旧的背景图像
	++imageChanges;					//修改图像变更次数
	bgImage = new Image(imgSrc);	//安装新的背景图像
    unlock(&mutex);					//释放互斥器
}

void PrettyMenu::changeBackground(std::istream& imgSrc)
{
    Lock ml(&mutex);
    delete bgImage;
    ++imageChanges;
    bgImage = new Image(imgSrc);
}
```

异常安全函数(Exception-safe functions)提供以下三个保证之一:

- **基本承诺**：如果异常被抛出，程序内的任何事物仍然保持在有效状态下。
  没有任何对象或数据结构会因此而败坏，所有对象都处于一种内部前后一致的状态(例如所有的 class 约束条件都继续得满足)。
- **强烈保证**：如果异常被抛出，程序状态不改变。
  调用这样的函数需有这样的认知：如果函数成功，就是完全成功，如果函数失败，程序会回复到“调用函数之前”的状态
- **不抛掷 (nothrow)保证**：承诺绝不抛出异常，因为它们总是能够完成它们原先承诺的功能
  作用于内置类型(例如 ints，指针等等)身上的所有操作都提供nothrow 保证
  这是异常安全函数中一个必不可少的关键基础材料

```c++
class PrettyMenu{
    std::tr1::shared_ptr<Image> bgImage;
};
void PrettyMenu::changeBackground(std::istream& imgSrc)
{
    Lock ml(&mutex);
    //如果Image构造函数抛出异常，有可能输入流imgSrc(input stream)的读取记号(read marker)已被移走，
    // 而这样的搬移对程序其余部分是一种可见的状态改变 
    bgImage.reset(new Image(imgSrc));//以"new Image”的执行结果，设定bgImage内部指针
    ++imageChanges;
}
```

```c++
struct PMImpl {
    std::tr1::shared_ptr<Image> bgImage;
    int imaaeChanges;
};

class PrettyMenu {
    //...
private:
    Mutex mutex;
    std::tr1::shared_ptr<PMImpl> pImpl;
};

//copy and swap (pimpl idiom)
// 原则很简单:打算修改的对象(原件)做出一份副本，然后在那副本身上做一切必要修改
// 若有任何修改动作抛出异常，原对象仍保持未改变状态
// 	待所有改变都成功后，再将修改过的那个副本和原对象在一个不抛出异常的操作中置换 (swap)
void PrettyMenu::changeBackground(std::istream& imgSrc)
{
    using std::swap;
    Lock ml(&mutex);
    std::tr1::shared_ptr<PMImp1> pNew(new PMImpl(*pImpl));
    pNew->bgImage.reset(new Image(imgSrc));	 //修改副本
    ++pNew->imageChanges;
    swap(pImpl, pNew);
}
```

### 总结：

- 异常安全函数(Exception-safe functions)即使发生异常也不会泄漏资源或允许任何数据结构败坏
  这样的函数区分为三种可能的保证:基本型、强烈型、不抛异常型。
- “强烈保证”往往能够以 copy-and-swap 实现出来，但“强烈保证”并非对所有函数都可实现或具备现实意义
- 函数提供的“异常安全保证”通常最高只等于其所调用之各个函数的“异常安全保证”中的最弱者



## 条款30:透彻了解inlining的里里外外

Understand the ins and outs of inlining

**优点：**
看起来像函数，动作像函数，比宏好得多(见条款 2)
可以调用它们又不需蒙受函数调用所招致的额外开销
inline某个函数，或许编译器就因此有能力对它(函数本体)执行语境相关最优化

**缺点：**
可能增加你的目标码 (object code)大小
过度热衷 inlining 会造成程序体积太大(对可用空间而言)
inline 造成的代码膨胀亦会导致额外的换页行为(paging)
降低指令高速缓存装置的击中率 (instruction cache hit rate)

inline 只是对编译器的一个申请，不是强制命令
一个表面上看似inline 的函数是否真是inline取决于建置环境，主要取决于编译器
	编译器通常不对“通过函数指针而进行的调用”实施inlining

inline函数无法随着程序库的升级而升级
	换句话说如果 f 是程序内的一个 inline 函数，客户将“函数本体”编进其程序中
	一旦程序库设计者决定改变 ，所有用到的客户端程序都必须重新编译

大部分调试器面对 imnline函数都束手无策



这项申请可以隐喻提出，也可以明确提出：

```c++
// 隐喻方式是将函数定义于class 定义式内
class Person {
public:
    int age() const { return theAge; }		//一个隐喻的imline 申请
private:
    int theAge;
};

// 明确声明inline函数的做法则是在其定义式前加上关键字 inline
template<typename T>
inline const Ta std::max(const T& a, const T& b)
	{ return a < b ? b : a; }
```

### 总结：

- 将大多数imnlining 限制在小型、被频繁调用的函数身上
  这可使日后的调试过程和二进制升级(binary upgradability)更容易，也可使潜在的代码膨胀问题最小化，使程序的速度提升机会最大化
- 不要只因为function templates出现在头文件，就将它们声明为inline



## 条款31:将文件间的编译依存关系降至最低

Minimize compilation dependencies between files

“将对象实现细目隐藏于一个指针背后”
	分割为两个classes，一个只提供接口（接口类），另一个负责实现该接口（实现类）

```c++
#include <string>			//标准程序库组件不该被前置声明
#include <memory>			//此乃为了 tr1::shared ptr 而含入;详后

class PersonImpl;			//Person实现类的前置声明。
class Date;					//Person接口用到的 classes 的前置声明
class Address;

class Person {
public:
    Person(const std::string& name, const Date& birthday, const Address& addr);
    std::string name() const;
    std::string birthDate() const;
    std::string address() const;
private:
    std::tr1::shared_ptr<PersonImpl> pImpl;	 //指针，指向实现物;
};	
```

这个分离的关键在于以“声明的依存性”替换“定义的依存性”，那正是编译依存性最小化的本质:
	**现实中让头文件尽可能自我满足**，万一做不到，则让它与其他文件内的**声明式(**而非定义式)相依

- **如果使用 object references 或 object pointers 可以完成任务，就不要使用objects**
  可以只靠一个类型声明式就定义出指向该类型的 references 和pointers
  但如果定义某类型的 obects，就需要用到该类型的定义式
- **如果能够，尽量以 class 声明式替换 class 定义式**

```c++
class Date;							//class 声明式。
Date today() ;						// 这里不需要定义式
void clearAppointments(Date d);		// Date的定义式
```

- **为声明式和定义式提供不同的头文件**



像 Person这样使用 pimpl idiom的 classes，被称为 **Handle classes**

```c++
#include "Person.h"
#include "PersonImpl.h"
//Person、PersonImpl完全相同的成员函数，两者接口完全相同
Person::Person(const std::string& name, const Date& birthday, 
               const Addresss addr)
    : pImpl(new PersonImpl(name, birthday, addr))	{}

std::string Person::name() const
{
    return pImpl->name();
}
```

另一个制作 Handle class 的办法是，令 Person 成为一种特殊的 **abstract base class**(抽象基类)，称为**Interface class**

```c++
class Person {
public:
    virtual ~Person();
    virtual std::string name() const = 0;
    virtual std::string birthDate() const = 0;
    virtual std::string address() const = 0;
    
    //interface class 的客户必须有办法为这种 class 创建新对象
    // factory (工厂)函数
    static std::tr1::shared_ptr<Person> create(
        const std::string& name, 
        const Date& birthday, 
        const Address& addr);
    
};

class RealPerson: public Person {
public:
    RealPerson(const std::string& name, const Date& birthday, const Address& addr) :
    	theName(name), theBirthDate(birthday), theAddress(addr) {}
    virtual ~RealPerson() { }
    std::string name() const;
    std::string birthDate() const;
    std::string address() const;
private:
    std::string theName;
    Date theBirthDate;
    Address theAddress;
};

std::tr1::shared_ptr<Person> Person::create(
    const std::string& name, 
    const Dates birthday,
    const Addresss addr)
{
    return
        std::tr1::shared_ptr<Person>(new RealPerson(name, birthday, addr));
}
```

### 总结：

- 支持“编译依存性最小化”的-般构想是
  相依于声明式，不要相依于定义式基于此构想的两个手段是Handle classes 和Interface classes
- 程序库**头文件**应该以“**完全且仅有声明式**” (fulland declaration-only forms)的形式存在。这种做法不论是否涉及 templates 都适用



# 继承与面向对象设计

## 条款32:确定你的 public 继承塑模出is-a关系

Make sure public inheritance models "is-a."

### 总结：

public 继承”意味is-a。适用于 base classes 身上的每一件事情一定也适用于derived classes 身上，因为每一个 derived class 对象也都是一个 base class 对象



## 条款 33:避免遮掩继承而来的名称

Avoid hiding inherited names

```c++
class Base {
public:
    virtual void mf1() = 0;
    virtual void mf1(int);//与前同
};


class Derived : private Base {	//转交函数 (forwarding function), 暗自成为inline
public:
    virtual void mf1() 
    { Base::mf1(); }
};
Derived d;
int x;
d.mf1();		//很好，调用的是 Derived::mf1
d.mfl(x);		//错误!Base::mf1()被遮掩了
```



### 总结：

- derived classes 内的名称会遮掩 base classes 内的名称。在 public 继承下从来没有人希望如此
- 为了让被遮掩的名称再见天日，可使用 using 声明式或转交函数(forwarding functions)



## 条款 34: 区分接口继承和实现继承

Differentiate between inheritance of interface and inheritance of implementation.

public 继承概念，由两部分组成：
	**函数接口**(function interfaces)继承和**函数实现** (function implementations继承

- 成员函数的接口总是会被继承
- 声明一个纯虚(pure virtual)函数的目的是为了**让derived classes 只继承函数接口**

- 声明非纯虚(impure virtual)函数的目的，是**让derived classes 继承该函数的接口和缺省实现**

- 声明non-virtual函数的目的是为了**令derived classes 继承函数的接口及一份强制性实现**

### 总结：

- 接口继承和实现继承不同。在public 继承之下，derived classes 总是继承base class的接口
- pure virtual函数只具体指定接口继承
- 非纯(impure virtual)函数具体指定接口继承及缺省实现继承
- non-virtual函数具体指定接口继承以及强制性实现继承



## 条款35:考虑virtual函数以外的其他选择

Consider alternatives to virtual functions.

### 藉由Non-Virtual-Interface 手法实现 Template Method设计模式

(与C++templates 并无关联)

```c++
class GameCharacter {
public:
    virtual int healthValue() const;		//返回人物的健康指数;
    										//derived classes 可重新定义它
};
//保留 healthvalue 为 public 成员函数，但让它成为non-virtual
// 并调用一个 private virtual函数(例如doHealthValue)进行实际工作:
//  也就是“令客户通过public non-virtual成员函数间接调用privatevirtual函数”，
//  称为 non-virtual-interface(NVI)手法。
//  它是所谓 Template Method设计模式(与C++templates 并无关联)的一个独特表现形式。
//  我把这个non-virtual函数(healthValue)称为 virtual函数的外覆器(wrapper)
class GameCharacter {
public:
    int healthValue() const
    {
        // ...
        int retVal = doHealthValue();
        // ...
        return retVal;
    }
//有些 class 继承体系要求 derivedclass 在 virtual函数的实现内必须调用其 base class 的对应兄弟
// 而为了让这样的调用合法，virtual 函数必须是 protected
private:	
    virtual int doHealthValue() const	//derived classes 可重新定义它
    {
        //缺省算法，计算健康指数
    }
};
```



### 藉由 Function Pointers 实现 Strategy 模式

```c++
//可能会要求每个人物的构造函数接受一个指针，
// 指向一个健康计算函数，可以调用该函数进行实际计算:
class GameCharacter;			//前置声明(forward declaration)
//以下函数是计算健康指数的缺省算法
int defaultHealthCalc(const GameCharacter& gc);
class GameCharacter {
public:
    typedef int (*HealthCalcFunc)(const GameCharacter&);
    explicit GameCharacter(HealthCalcFunc hcf = defaultHealthCalc)
        : healthFunc(hcf)
    {}
    int healthValue() const
        { return healthFunc(*this); }
private:
    HealthCalcFunc healthFunc;
};
```

提供了某些有趣弹性:

```c++
class EvilBadGuy: public GameCharacter {
public:
    explicit EvilBadGuy(HealthCalcFunc hcf = defaultHealthCalc) 
        : GameCharacter(hcf)
    { /*...*/ }
};
//1 同一人物类型之不同实体可以有不同的健康计算函数
int loseHealthQuickly(const GameCharacter&);	//健康指数计算函数1
int loseHealthSlowly(const GameCharacter&);		//健康指数计算函数2
EvilBadGuy ebgl(loseHealthQuickly);				//相同类型的人物搭配
EvilBadGuy ebg2(loseHealthSlowly);				//不同的健康计算方式

//2 某已知人物之健康指数计算函数可在运行期变更
// 例如Gamecharacter 可提供一个成员函数 setHealthalculator，用来替换当前的健康指数计算函数
```

运用函数指针替换 virtual 函数，其**优点**
	“每个对象可各自拥有自己的健康计算函数”
	“可在运行期改变计算函数”
是否以补缺点
	可能必须降低Gamecharacter封装性
是必须根据每个设计情况的不同而抉择的

### 藉由tr1::function 完成 Strategy 模式

tr1::function 的对象
	可持有(保存)任何可用物 (callable entity，也就是函数指针、函数对象、或成员函数指针)，
	只要其签名式兼容于需求端（就像条款 54 所说）

```c++
class GameCharacter;				//如前
int defaultHealthCalc(const GameCharacter& gc);	//如前
class GameCharacter {
public:
    //HealthCalcFunc可以是任何“可调用物” (callable entity)，可被调用并接受
	//任何兼容于GameCharacter 之物，返回任何兼于 int 的东西。详下。
    typedef std::tr1::function<int (const GameCharacter&)> HealthCalcFunc;
    explicit GameCharacter(HealthCalcFunc hcf = defaultHealthCalc)
        : healthFunc(hcf) { }
    int healthValue() const
    { return healthFunc( * this); }
private:
    HealthCalcFunc healthFunc;
};


short calcHealth(const GameCharactera);		//健康计算函数;注意其返回类型为 non-int
struct HealthCalculator {					//为计算健康而设计的函数对象
    int operator() (const GameCharacter&) const { /*...*/ }
};
class GameLevel {
public:
    float health(const GameCharacter&) const;	//成员函数，用以计算健康
};

class EvilBadGuy: public GameCharacter {};
class EyeCandyCharacter: public GameCharacter {};

EvilBadGuy ebg1(calcHealth);				//人物1，使用某个，函数计算健康指数
EyeCandyCharacter ecc1(HealthCalculator()); //人物2，使用某个函数对象计算健康指数
GameLevel currentLevel;						//人物3，使用某个成员函数计算健康指数
EvilBadGuy ebg2(std::tr1::bind(&GameLevel::health, currentLevel, _1) );
```

### 古典的 Strategy模式

传统(典型)的Strategy做法会将健康计算函数做成一个分离的继承体系中的virtual成员函数

<img src=".\Picture\Strategy模式.png" style="zoom:50%;" />

 Gamecharacter 是某个继承体系的根类，体系中的EvilBadGuy和EyeCandyCharacter都是derived classes；HealthCalcFunc 是另一个继承体系的根类，体系中的 SlowHealthLoser 和FastHealthLoser都是 derived classes，每一个 GameCharacter 对象都内含一个指针，指向一个来自HealthCalcEunc继承体系的对象。

```c++
class GameCharacter;			//前置声明 forward declaration
class HealthCalcFunc {
public:
    virtual int calc(const GameCharacter& gc) const { /*...*/ }
};

HealthCalcFunc defaultHealthCalc;

class GameCharacter {
public:
    explicit GameCharacter(HealthCalcFunc* phcf = &defaultHealthCalc)
        : pHealthCalc(phcf) { }
    int healthValue() const
        { return pHealthCalc->calc(*this); }
private:
    HealthCalcFunc* pHealthCalc;
};
```

### Strategy模式总结：

- 使用**non-virtualinterface(NVI)**手法，那是**Template Method**设计模式的一种特殊形式
  它以public non-virtual成员函数包裹较低访问性(private 或protected)的 virtual函数
- 将virtual函数替换为**“函数指针成员变量”**，这是strategy设计模式的一种分解表现形式
- 以**tr1::function** 成员变量替换 virtual函数，因而允许使用任何可调用物(callable entity)搭配一个兼容于需求的签名式。这也是 Strategy 设计模式的某种形式。
- 将**继承体系内的 virtual** 函数替换为**另一个继承体系内的 virtual** 函数。这是Strategy设计模式的传统实现手法。



### 总结：

- virtual函数的替代方案包括NVI手法及Strategy设计模式的多种形式。NVI手法自身是一个特殊形式的 Template Method设计模式。
- 将机能从成员函数移到 class 外部函数，带来的一个缺点是，非成员函数无法访问class的non-public成员
- tr1::function 对象的行为就像一般函数指针。这样的对象可接纳“与给定之目标签名式(target signature)兼容”的所有可调用物 (callableentities)



## 条款36:绝不重新定义继承而来的non-virtual函数

Never redefine an inherited non-virtual function.

## 条款37:绝不重新定义继承而来的缺省参数值

Never redefine a function's inherited default parameter value

```c++
class Shape {
public:
    enum ShapeColor { Red, Green. Blue };
    void draw(ShapeColor color = Red) const
    {
        doDraw(color);
    }
private:
    virtual void doDraw(ShapeColor color) const = 0;	//真正的工作,在此处完成
    
};
class Rectangle: public Shape {
public:
    // ...
private:
	virtual void doDraw(ShapeColor color) const;//缺省参数值
};
```

### 总结：

- 绝对不要重新定义一个继承而来的缺省参数值，因为缺省参数值都是静态绑定

-  virtual函数是动态绑定

  

## 条款 38:通过复合塑模出 has-a 或"根据某物实现出

Model "has-a"or "is-implemented-in-terms-of" through composition.

复合 (composition)是类型之间的一种关系，当某种类型的对象**内含它种类型的对象**，便是这种关系。

```c++
class Address { }；				//某人的住址
class PhoneNumber { };
class Person {
public:
    // ...
private:
	std::string name;		//复合(composed object)
	Address address;		//同上
	PhoneNumber voiceNumber;//同上
    PhoneNumber faxNumber;//同上
};
```

复合(composition)这个术语有许多同义词
	包括 layering(分层)、containment(内含)、aggregation(聚合)和embedding(内嵌)

复合意味 **has-a**(有一个)或**is-implemented-in-terms-of**(根据某物实现出)
	has-a 关系：Person有一个名称，一个地址，以及语音和传真两笔电话号码
	**is-implemented-in-terms-of**(根据某物实现出)

```c++
//is-implemented-in-terms-of(根据某物实现出)
template<class T>			//将 list 应用于 set。正确做法
class Set {
public:
    bool member(const T& item)const;
    void insert(const T& item);
    void remove(const T& item);
    std::size_t size() const;
private:
    std::list<T> rep;		//用来表述set的数据
};

template<typename T>
bool Set<T>::member(const T& item) const
{
    return std::find(rep.begin(), rep.end(), item) != rep.end();
}

template<typename T>
void Set<T>::insert(const T& item)
{
    if(!member(item)) rep.push_back(item);
}

template<typename T>
void Set<T>::remove(const T& item)
{
    typename std::list<T>::iterator it = 
        std::find(rep.begin(), rep.end(), item);
    if (it != rep.end()) rep,erase(it);
}

template<typename T>
std::size_t Set<T>::size() const
{
    return rep.size();
}
```

### 总结：

- 复合(composition)的意义和 public 继承完全不同。
- 在应用域 (application domain)，复合意味 hasa(有一个)。在实现域(implementation domain)，复合意味isimplemented-in-terms-of(根据某物实现出)。



## 条款39:明智而审慎地使用 private继承

Use private inheritance judiciously

Private 继承意味 is-implemented-in-terms-of (根据某物实现出)
因为条款 38 才刚指出复合 (composition)的意义也是这样
	你如何在两者之间取舍?答案很简单：尽可能**使用复合**，必要时才使用 private 继承

什么时候使用private继承：
	主要是当 protected 成员和/或 virtual 函数牵扯进来的时候
	其实还有一种激进情况，那是当空间方面的利害关系足以踢翻 private 继承的支柱时



### 总结：

- Private 继承意味is-implemented-in-terms of (根据某物实现出)。它通常比复合(composition)的级别低。但是当 derived class 需要访问 protected base class 的成员，或需要重新定义继承而来的 virtual 函数时，这么设计是合理的。
- 和复合(composition)不同，private继承可以造成empty base 最优化。这对致力于“对象尺寸最小化”的程序库开发者而言，可能很重要



## 条款40:明智而审慎地使用多重继承

Use multiple inheritance judiciously

多重继承(multiple inheritance; MI)

当MI进入设计景框程序有可能从一个以上的 base classes 继承相同名称(如函数、typedef等等)
那会导致较多的歧义(ambiguity)机会

```c++
// File会被复制两次
class File { };
class InputFile: public File { };
class OutputFile: public File { };
class IOFile: 
	public InputFile, 
	public OutputFile { };

// 修改
class File { };
class InputFile: virtual public File { };
class OutputFile: virtual public File { };
class IOFile: 
	public InputFile,
	public OutputFile
{ };
```

第一，非必要不使用 virtual bases。平常请使用non-virtual继承
第二，如果你必须使用 virtual base classes，尽可能避免在其中放置数据

### 总结：

- 多重继承比单一继承复杂。它可能导致新的歧义性，以及对 virtual 继承的需要
- virtual继承会增加大小、速度、初始化(及赋值)复杂度等等成本
  如果 virtual base classes 不带任何数据，将是最具实用价值的情况
- 多重继承的确有正当用途
  其中一个情节涉及“public 继承某个Interface class和“ private继承某个协助实现的class”的两相组合



# 模板与泛型编程

Templates and Generic Programming

## 条款 41:了解隐式接口和编译期多态

Understand implicit interfaces and compile-time polymorphism.

面向对象编程世界总是以显式接口 (explicit interfaces)和运行期多态(runtimepolymorphism)解决问题。

Templates 及泛型编程的世界，与面向对象有根本上的不同
在此世界中显式接口和运行期多态仍然存在，但重要性降低
反倒是隐式接口(implicit interfaces)和编译期多态(compile-time polymorphism)移到前头了

通常**显式接口**由函数的签名式(也就是函数名称、参数类型、返回类型)构成：

```c++
class Widget {
public:
    Widget();
    virtual ~Widget();
    virtual std::size_t size() const;
    virtual void normalize();
    void swap(Widget& other);
};
```

**隐式接口**并不基于函数签名式，而是由有效表达式 (validexpressions)组成：

```c++
template<typename T>
void doProcessing(T& w)
{
    if (w.size() > 10 && w != someNastyWidget)
    {
        T temp(w);
        temp.normalize();
        temp.swap(w);
    }
}
// w必须支持哪一种接口，系由 template 中执行于w身上的操作来决定
// 涉及w的任何函数调用，例如operator>和operator!=,有可能造成template具现化 (instantiated)，使这些调用得以成功
```

加诸于 template 参数身上的隐式接口，就像加诸于 class 对象身上的显式接口样真实，而且两者都在编译期完成检查。



### 总结：

- classes 和 templates 都支持接口 (interfaces)和多态(polymorphism)
- 对 classes 而言接口是显式的(explicit),以函数签名为中心。多态则是通过 virtual函数发生于运行期。
- 对 template 参数而言，接口是隐式的 (implicit)，奠基于有效表达式。多态则是通过template具现化和函数重载解析(function overloading resolution)发生于编译期。



## 条款42:了解 typename 的双重意义

Understand the two meanings of typename.

class 和 typename 相同

```c++
template<class T> class widget;			//使用class
template<typename T> class Widget;		//使用"typename"
```

有时候一定得使用typename

C++ 有个规则可以解析(resolve)此一歧义状态:
	如果解器在 template 中遭遇一个嵌套从属名称，它便假设这名称不是个类型，除非你告诉它是。

template 内出现的名称如果相依于某个 template 参数，称之为**从属名称**(dependent names)
如果从属名称在 class内呈嵌套状，称它为**嵌套从属名称**(nested dependent name)

```c++
template<typename C>
void print2nd(const C& container)
{
    if(container.size() >= 2)
    {
        C::const_iterator iter(container.begin());	// 嵌套从属名称
        ++iter;
        int value = *iter;
        std::cout << value;
    }
}

template<typename C>
void print2nd(const C& container)
{
    //这是合法的C++代码
	if (container.size() >= 2) 
    {
        // C::const_iterator 是个类型
        typename C::const_iterator iter(container.begin());		
    }
}

//typename只被用来验明套从属类型名称;其他名称不该有它存在
template<typename C>			//允许使用“typename”(或class”)
void f(const C& container,		//不允许使用“typename"
	typename C::iterator_iter);	//一定要使用"typename"
```

typename 不可以出现在 base classes list 内的套从属类型名称之前，
也不可在member initialization list (成员初值列)中作为 base class 修饰符。例如:

```c++
template<typename T>
class Derived: public Base<T>::Nested {	//base class list 中不允许“typename”
public:
    explicit Derived(int x)		
        : Base<T>::Nested(x)	//mem init list 中 //不允许"typename"嵌套从属类型名称
    {
        //既不在 base class list 中也不在 mem
        // initlist 中作为一个base class 修饰符需加上typename
        typename Base<T>::Nested temp;
    }
};
```

### 总结：

- 声明template 参数时，前缀关键字 class typename 可互换。
- 请使用关键字 typename标识嵌套从属类型名称
  但不得在 base class lists(基类列)或member initialization list (成员初值列)内以它作为base class修饰符



## 条款 43:学习处理模板化基类内的名称

Know how to access names in templatized base classes.

```c++
class CompanyA {
public:
    void sendCleartext(const std::string& msg);
    void sendEncrypted(const std::string& msg);
};

class CompanyB {
public:
    void sendCleartext(const std::string& msg);
    void sendEncrypted(const std::string& msg);
};

class MsgInfo { };	//这个 class 用来保存信息，以备将来产生信息

template<typename Company>
class MsgSender {
public:
    // 构造函数、析构函数等等
    void sendClear(const MsgInfo& info)
    {
        std::string msg;
        Company c;
        c.sendCleartext(msg);
    }
    void sendSecret(const MsgInfo& info) 
    {
        std::string msg;
        Company c;
        c.sendEncrypted(msg);
    }
};

//假设有时候想要在每次送出信息时志记(log)某些信息，但会编译错误
// 当编译器遭遇 class template LoggingMsgSender 定义式时，并不知道它继承什么样的 class。当然它继承的是 MsgSender<Company>，但其中的 Company是个 template 参数，不到后来(当 LoggingMsgSender 被具现化)无法确切知道它是什么。而如果不知道Company是什么，就无法知道 class MsgSender<Company>看起来像什么,更明确地说是没办法知道它是否有个 sendclear函数。
template<typename Company>
class LoggingMsgSender: public MsgSender<Company> {
public:
    //构造函数、析构函数 等等
    
    void sendClearMsg(const MsqInfo& info)
    {
        // 将“传送前”的信息写至 1og;
        sendClear(info);	//调用 base class 函数;这段码无法通过编译
        // 将“传送后”的信息写至 lg;
    }
};

//为什么会编译错误？
// 特化版本可能不提供和一般性template 相同的接口。
// 假如有个 class Companyz 坚持使用加密通讯:
class CompanyZ {	//这个class 不提供，sendCleartext 函数
public:
	void sendEncrypted(const std::string& msg);
};

//针对 companyZ产生一个 MsgSender特化版:
// 对于LoggingMsgSender，如果Company==CompanyZ，sendClear函数不存在
template<>		//一个全特化的
class MsgSender<CompanyZ> {	//它和一般template 相同，差别只在于它删掉了sendClear。
public:
	void sendSecret(const MsgInfo& info) { }
};

//解决方法，三个办法
//每一个解法做的事情都相同对编译器承诺：
// “base class template 的任何特化版本都将支持其一般(泛化)版本所提供的接口”

// 第一是在 base class 函数调用动作之前加上"this->”:
template<typename Company>
class LoggingMsgSender: public MsgSender<Company>{
public:
    void sendClearMsg(const MsgInfo& info)
    {
        //将“传送前”的信息写至log;
        this->sendClear(info);		//成立，假设 sendClear 将被继承
        //将“传送后”的信息写至log;
    }
};
// 第二是使用 using声明式。
template<typename Company>
class LoggingMsgSender: public MsgSender<Company> {
public:
    using MsgSender<Company>::sendClear;	//告诉编译器，请它假设sendClear位于base class 内
    void sendClearMsg(const MsgInfo& info) 
    {
        sendClear(info);		// 0K，假设 sendClear 将被继承下来
    }
};
// 第三个做法是，明白指出被调用的函数位于 base class 内:
template<typename Company>
class LoggingMsgSender: public MsgSender<Company> {
public:
    void sendClearMsg(const MsgInfo& info)
    {
        // 但这往往是最不让人满意的一个解法，因为如果被调用的是 virtual函数，
		// 明确资格修饰(explicit qualification)会关闭“virtual绑定行为”。
        MsgSender<Company>::sendClear(info);//0K，假设 sendClear将被继承下来。
    }
};

//但如果这个承诺最终未被实践出来，往后的编译最终还是会还给事实一个公道
LoggingMsgSender<Companyz> zMsgSender;
MsgInfo msgData;					//在msgData 内放置信息
zMsgSender.sendClearMsg(msgData);	//错误!无法通过编译
```

面对“指涉 base class members”之无效references编译器的诊断时间
	 可能发生在早期(当解析 derived class template 的定义式时)
	也可能发生在晚期(当那些 templates 被特定之 template 实参具现化时)
C++的政策是宁愿较早诊断
	这就是为什么“当base classes 从 templates 中被具现化时”，它假设它对那些 base classes 的内容毫无所悉的缘故。

### 总结：

- 可在 derived class templates 内通过“this-”指涉 base class templates 内的成员名称，或藉由一个明白写出的“base class 资格修饰符”完成。



## 条款44:将与参数无关的代码抽离

 templatesFactor parameter-independent code out of templates

使用 templates 可能会导致代码膨胀(code bloat)：其二进制码带着重复(或几乎重复)的代码、数据。

**共性与变性分析 (commonality andvariabilityanalysis)**

```c++
template<typename T, std::size_t n>
class SquareMatrix {
public:
    void invert();	//求逆矩阵
};
// 这是template引出代码膨胀的一个典型例子
SquareMatrix<double, 5> sml;
sml.invert();				//调用SquareMatrix<double, 5>::invert
SquareMatrix<double, 10> sm2;
sm2.invert();				//调用SquareMatrix<double, 10>::invert

//SquareMatrix 的第一次修改:
// SquareMSp:;invert无法知道哪个特定矩阵的数据在哪儿，只有 derived class 知道
template<typename T>
class SquareMatrixBase {					//与尺寸无关的base class，用于正方矩阵
protected:
    void invert(std::size_t matrixSize);	//以给定的尺寸求逆矩阵
};
template<typename T, std::size_t n>
class SquareMatrix: private SquareMatrixBase<T> {
private:
    using SquareMatrixBase<T>::invert;		//避免掩 base 版的invert;见条款33
public:
    //制造一个inline 调用，调用base class版的invert。
    void invert() { this->invert(n); }
};
```

### 总结：

- Templates 生成多个 classes 和多个函数，所以任何 template代码都不该与某个造成膨胀的template 参数产生相依关系。

- 因非类型模板参数(non-type template parameters)而造成的代码膨胀，往往可消除，做法是以函数参数或 class 成员变量替换template 参数。

- 因类型参数(type parameters)而造成的代码膨胀，往往可降低，做法是让带有完全相同二进制表述(binary representations)的具现类型(instantiation types)共享实现码。

  

## 条款45:运用成员函数模板接受所有兼容类型

Use member function templates to accept "all compatible types.

```c++
class Top { /*...*/ };
class Middle: public Top { /*...*/ };
class Bottom: public Middle { /*...*/ };
Top* pt1 = new Middle;		//将Midale* 转换为 Top*
Top* pt2 = new Bottom;		//将Bottom* 转换为 Top*
const Top* pct2 = pt1;		//将Top* 转换为 const Top*

//在用户自定的智能指针中模拟上述转换
template<typename T>
class SmartPtr {
public:
    //智能指针通常以内置(原始)指针完成初始化
    explicit SmartPtr(T* realPtr);
};
//将 SmartPtr<Midale> 转换为 SmartPtr<Top>
SmartPtr<Top> pt1 = SmartPtr<Middle>(new Middle);
//将 SmartPtr<Bottom> 转换为 SmartPtr<Top>
SmartPtr<Top> pt2 = SmartPtr<Bottom>(new Bottom);
//将SmartPtr<Top> 转换为 SmartPtr<const Top>
SmartPtr<const Top> pct2 = pt1;
```

但是，同一个template 的不同具现体(instantiations)之间并不存在什么与生俱来的固有关系
	(译注：这里意指如果以带有 base-derived 关系的 B，D两类型分别具现化某个 template，
		产生出来的两个具现体并不带有 base-derived 关系)
所以编译器视 SmartPtr<Middle> 和 SmartPtr<Top> 为完全不同的 classes
	它们之间的关系与 vector<float>和Widget 更密切
为了获得我们希望获得的 SmartPtr classes 之间的转换能力必**须将它们明确地编写出来**

### Templates 和泛型编程(Generic Programming)

永远无法写出需要的所有构造函数

需要的不是为 SmartPtr写一个构造函数，而是为它写一个构造模板
	模板(templates)是所谓member function templates(常简称为 member templates)，其作用是为 class 生成函数

```c++
//对任何类型T和任何类型u这里可以根据Smartptr<u>生成一个SmartPtr<T>
// 因为Smartptr<T>有个构造函数接受一个SmartPtr<U>参数。
//这一类构造函数根据对象 u 创建对象t(例如根据 SmartPtr<U>创建一个SmartPtr<T>)，
// 而u和v的类型是同一个 template 的不同具现体，有时我们称之为泛化(generalized) copy构造函数
template<typename T>
class SmartPtr {
public:
    template<typename U>		//member template.为了生成copy构造函数
    SmartPtr(const SmartPtr<U>& other);
};

//这个为 Smartptr而写的“泛化copy构造函数”提供的东西比需要的更多
// 希望根据一个 SmartPtr<Bottom>创建一个SmartPtr<Top>，
// 却不希望根据一个SmartPtr<Top>创建一个SmartPtrBottorm
//  因为那对 public 继承而言(见条款 32)是矛盾的
//可以在“构造模板”实现代码中约束转换行为:
template<typename T>
class SmartPtr {
public:
    //在“构造模板”实现代码中约束转换行为
    template<typename U>
    SmartPtr(const SmartPtr<U>& other)
    	: heldPtr(other.get())	{ /*...*/ }	 //以other的heldPtr 初始化 this的heldPtr
    T* get() const { return heldPtr; }
private:
	T* heldPtr;				//这个SmartPtr 持有的内置(原始)指针
};
```

member function templates(成员函数模板)另一个角色是**支持赋值操作**

```c++
template<class T>
class shared_ptr {
public:
    template<class Y>
        explicit shared_ptr(Y* p);				//构造，来自任何兼容的内置指针
    template<class Y>
        shared_ptr(shared_ptr<Y> const& r);		//构造，来自任何兼容的shared_ptr
    template<class Y>
        explicit shared_ptr(weak_ptr<Y> const& r);//构造，来自任何兼容的weak_ptr
    template<class Y>
        explicit shared_ptr(auto_ptr<Y>& r);	//构造，来自任何兼容的auto_ptr
    template<class Y>
        shared_ptr& operator=(shared_ptr<Y> const& r);	//赋值，来自任何兼容的shared_ptr
    template<class Y>
        shared_ptr& operator=(auto_ptr<Y>& r);		//赋值，来自任何兼容的auto_ptr
};
```

上述所有构造函数都是 explicit，惟有“泛化 copy构造函数”除外
	意味从某个 shared_ptr类型隐式转换至另一个 shared_ptr类型是被允许的
	但从某个内置指针或从其他智能指针类型进行隐式转换则不被认可
		(如果是显式转换如 cast强制转型动作倒是可以)
另一个趣味点是传递给 tr1::shared_ptr 构造函数和 assignment 操作符的 auto_ptrs 并未被声明为 const，
与之形成对比的则是trl::shared_ptrs 和 tr1::weak_ptrs 都以 const 传递
	这是因为条款13 说过**复制一个auto_ptrs**，它们其实**被改动了**

member templates 并不改变语言规则
	在 class内声明泛化copy构造函数(是个member template)并不会阻止编译器生成它们自己的copy构造函数(一个non-template)
所以如果想要控制copy构造的方方面面，必须同时声明泛化 copy 构造函数和“正常的”copy 构造函数
相同规则也适用于赋值 (assignment)操作

```c++
template<class T>
class shared_ptr { 
public:
    shared_ptr(shared_ptr const& r);	//copy构造函数
    
    template<class Y>
    shared_ptr(shared_ptr<Y> const& r);	//泛化 copy构造函数
    
    shared_ptr& operator=(shared_ptr const& r);	//copy assignment.
    
    template<class Y>
    shared_ptr& operator=(shared_ptr<Y> const& r);	//泛化 copy assignment.
};
```

### 总结：

- 请使用member function templates(成员函数模板)生成“可接受所有兼容类型的函数。
- 如果你声明member templates 用于“泛化copy构造或“泛化assignment操作”你还是需要声明正常的copy构造函数和copy assignment操作符。



## 条款46:需要类型转换时请为模板定义非成员函数

Define non-member functions inside templates when type conversions are desired

```c++
template<typename T>
class Rational {
public:
    Rational(const T& numerator = 0,
             const T& denominator = 1);	//条款20：参数以passed by reference方式传递
    const T numerator() const;			//条款28：以passed by value方式传递。
    const T denominator() const;		//条款3： 它们是const
};
template<typename T>
const Rational<T>& operator* (const Rational<T>& lhs, 
                              const Rational<T>& rhs)
{ /*...*/ }

Rational<int> oneHalf(1, 2);
Rational<int> result = oneHalf * 2;	//错误!无法通过编译。

//因为在 template 实参推导过程中从不将隐式类型转换函数纳入考虑
// 编译器不会使用 Rational<int> 的non-explicit构造函数将2转换为Rational<int>，进而将T推导为 int
//template class内的 friend 声明式可以指涉某个特定函数
template<typename T>
class Rational {
public:
    //为当对象 oneHalf 被声明为一个Rational<int>
    // class Rational<int>于是被具现化出来，而作为过程的部分
    // friend函数operator*(接受 Rational<int>参数)也就被自动声明出来
    friend const Rational operator*(const Rational& lhs,
                                    const Rational& rhs);
};
template<typename T>
const Rational<T> operator* (const Rational<T>& lhs,
                             const Rational<T>& rhs)
{ /*...*/ }


//但那个函数只被声明于Rational内，并没有被定义出来。连接器找不到它!
template<typename T> class Rational;
//若有必要，在头文件内定义
template<typename T>
const Rational<T> doMultiply(const Rational<T>& lhs, 
                             const Rational<T>& rhs)
{
    return Rational<T>(lhs.numerator() * rhsnumerator(), 
                       lhs.denominator() * rhs.denominator());
}
template<typename T>
class Rational {
public:
    friend const Rational<T> operator*(const Rational<T>& lhs, 
                                       const Rational<T>& rhs) 
    { return doMultiply(lhs, rhs); }	//令 fiend 调用 helper
};
```

### 总结：

- 当我们编写一个class template，而它所提供之“与此template 相关的”函数支持“所有参数之隐式类型转换”时，请将那些函数定义为“class template 内部的 friend函数”



## 条款47:请使用traits classes(特性类)表现类型信息

Use traits classes for information about types.

```c++
//advance，用来将某个迭代器移动某个给定距离

template<typename IterT, typename DistT>
void advance(IterT& iter, DistT d);	//将迭代器向前移动 d单位, 如果d<0则向后移动
//观念上advance 只是做 iter += d动作，但其实不可以全然那么实践，
// 因为只有randomaccess(随机访问)选代器才支持 +=操作
// 面对其他威力不那么强大的迭代器种类，advance 必须反复施行 ++ 或--，共d次

//希望的是以这种方式实现 advance:
template<typename IterT, typename DistT>
void advance(IterT& iter, DistT d)
{
    if (iter is a random access iterator)
    {
        iter += d;		//针对randomaccess 迭代器使用选代器算术运算
    }
    else {
        if (d >= 0) { while (d--) ++iter; }
        else { while (d++) --iter; }		//针对其他选代器分类反复调用++或--
    }
}
```

Traits 并不是 C++ 关键字或一个预先定义好的构件，它们是一种技术，也是一个 C++ 程序员共同遵守的协议
这个技术的要求之一是，它对内置 (built-in)类型和用户自定义(user-defined)类型的表现必须一样好
	举个例子，如果上述advance收到的实参是一个指针(例如 const char*)和一个int，
		上述advance仍然必须有效运作，那意味 traits 技术必须也能够**施行于内置类型如指针身上**

```c++
//习惯上 traits 总是被实现为structs，但它们却又往往被称为 traits classes
template<typename IterT>
struct iterator_traits;		//template，用来处理迭代器分类的相关信息
// iterator_traits的运作方式是
//  针对每一个类型 IterT，在struct iterator_traits<IterT>内
//   一定声明某个 typedef 名为 iterator_category。这个 typedef 用来确认 IterT的迭代器分类。

//例子：声明iterator_category
template <...>		//略而未写template参数
class deque {
public:
    class iterator {
        public:
        	typedef random_access_iterator_tag iterator_category;
    };
};
template <...>		//略而未写template参数
class list {
public:
    class iterator {
    public:
        typedef bidirectional_iterator_tag iterator_category;
    };
};
template<typename IterT>
struct iterator_traits {
    typedef typename IterT::iterator_category iterator_category;
};
//为了支持指针迭代器， iterator_traits 特别针对指针类型提供一个偏特化版本
template<typename IterT>
struct iterator_traits<IterT*>		//template偏特化，针对内置指针
{
    typedef random_access_iterator_tag iterator_category;
}

//可以对 advance实践先前的伪码(pseudocode)，会导致编译问题:
//IterT类型在编译期间获知所以iterator_traits<IterT>::iterator_category也可在编译期间确定。
//但if语句却是在运行期才会核定
// 为什么将可在编译期完成的事延到运行期才做呢?
//   这不仅浪费时间，也造成可执行文件膨胀
template<typename IterT, typename DistT>
void advance(IterT& iter, DistT d)
{
    if (typeid(typename std::iterator_traits<IterT>::iterator_category)
        == typeid(std::random_access_iterator_tag))
        //....
}

//当重载某个函数 f，你必须详细叙述各个重载件的参数类型
//当调用 f，编译器便根据传来的实参选择最适当的重载件
// //这份实现用于random access迭代器
template<typename IterT, typename DistT>
void doAdvance(IterT& iter, DistT d, std::random_access_iterator_tag)
{
    iter += d;
}
//这份实现用于 bidirectional 选代器
template<typename IterT, typename DistT>
void doAdvance(IterT iter, DistT d, std::bidirectional_iterator_tag) 
{
    if (d >= 0) { while (d--) ++iter; }
    else { while (d++) --iter; }
}
//这份实现用于input迭代器
template<typename IterT, typename DistT>
void doAdvance(IterT& iter, DistT d, std::input_iterator_tag)
{
    if(d < 0){ throw std::out_of_range("Negative distance"); }
    while (d--) ++iter;
}

//advance实现
template<typename IterT, typename DistT>
void advance(IterT& iter, DistT d)
{
    doAdvance(	//调用的 doAdvance 版本，对 iter之迭代器分类而言必须是适当的
    	iter, d,
        typename std::iterator_traits<IterT>::iterator_category()
    );
}
```

现在我们可以总结如何使用一个 traits class 了：

- 建立一组重载函数(身份像劳工)或函数模板(例如 doAdvance)，彼此间的差异只在于各自的traits 参数。
  令每个函数实现码与其接受之 traits 信息相应和
- 建立一个控制函数(身份像工头)或函数模板(例如 advance)，它调用上述那些“劳工函数”并传递traits class 所提供的信息

### 总结：

- Traits classes 使得“类型相关信息”在编译期可用。它们以templates 和“templates特化”完成实现
- 整合重载技术(overloading)后，traits classes 有可能在**编译期**对类型执行if...else测试



## 条款48:认识 template 元编程

Be aware of template metaprogramming.

所谓template metaprogram(模板元程序)是以C++ 写成、执行于 C++ 编译器内的程序
一旦TMP 程序结束执行其输出，也就是从 templates 具现出来的若干 C++ 源码，便会一如往常地被编译

TMP并没有真正的循环构件，所以循环效果系藉由递归 (recursion)完成。

### 总结：

- Template metaprogramming(TMP，模板元编程)可将工作由运行期移往编译期因而得以实现早期错误侦测和更高的执行效率。
- TMP可被用来生成“基于政策选择组合”(based on combinations of policychoices)的客户定制代码，也可用来避免生成对某些特殊类型并不适合的代码



# 定制new和 delete

## 条款49:了解new-handler 的行为

Understand the behavior of the new-handler.

当 operator new 抛出异常以反映**一个未获满足的内存需求**之前，它会先调用一个客户指定的错误处理函数，一个所谓的new-handler
	为了指定这个“用以处理内存不足”的函数，客户必须调用 set_new_handler，
		那是声明于 <new>的个标准程序库函数:

```c++
namespace std {
    typedef void (*new_handler)();
    new_handler set_new_handler(new_handler p) throw();
}

//以下是当operator new 无法分配足够内存时，该被调用的函数
void outOfMem() {
    std::cerr << "Unable to satisfy request for memory\n";
    std::abort();
}
int main() {
    std::set_new_handler(outOfMem);
    int* pBigDataArray = new int[100000000L];
}
```

可以为不同类提供不同的new

### 总结：

- set_new_handler 允许客户指定一个函数，在内存分配无法获得满足时被调用
- Nothrow new是一个颇为局限的工具，因为它只适用于内存分配；后继的构造函数调用还是可能抛出异常



## 条款50:了解 new 和 delete 的合理替换时机

Understand when it makes sense to replace new and delete.

### 为什么替换编译器提供的 operatornew或 operator delete

- 用来检测运用上的错误
- 为了强化效能
  - 为了增加分配和归还的速度
  - 为了降低缺省内存管理器带来的空间额外开销
  - 为了弥补缺省分配器中的非最佳齐位
- 为了收集使用上的统计数据
- 为了将相关对象成簇集中
- 为了获得非传统的行为

### 总结：

有许多理由需要写个自定的 new和 delete，包括改善效能、对heap 运用错误进行调试、收集 heap 使用信息。



## 条款 51:编写 new和 delete 时需固守常规

Adhere to convention when writing new and delete.

实现一致性 operator new必得：
	返回正确的值
	内存不足时必得调用new-handling函数(见条款49)，
	必须有对付零内存需求的准备，
	还需避免不慎掩盖正常形式的 new 

### 总结：

- operator new应该内含一个无穷循环，并在其中尝试分配内存，如果它无法满足内存需求，就该调用 new-handler。它也应该有能力处理0 bytes 申请。Class专属版本则还应该处理“比正确大小更大的(错误)申请”
- operator delete应该在收到 null 指针时不做任何事。Class 专属版本则还应该处理“比正确大小更大的(错误)申请”



## 条款52:写了placement new也要写placement delete

Write placement delete if you write placement new.

如果 operator new接受的参数除了一定会有的那个 size_t之外还有其他，这便是个所谓的placement new

### 总结：

- 当写一个 placement operator new，请确定也写出了对应的 placementoperator delete。如果没有这样做，你的程序可能会发生隐微而时断时续的内存泄漏。
- 当你声明 placement new和 placement delete，请确定不要无意识(非故意)地遮掩了它们的正常版本。



# 杂项讨论

## 条款 53:不要轻忽编译器的整告

Pay attention to compiler warnings.

### 总结：

- 严肃对待编译器发出的警告信息。努力在你的编译器的最高(最严)警告级别下争取“无任何警告”的荣誉。
- 不要过度倚赖编译器的报警能力，因为不同的编译器对待事情的态度并不相同一旦移植到另一个编译器上，你原本倚赖的警告信息有可能消失



