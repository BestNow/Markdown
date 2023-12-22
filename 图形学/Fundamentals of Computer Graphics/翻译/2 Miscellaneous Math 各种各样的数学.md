# 2 Miscellaneous Math 各种各样的数学

Much of graphics is just translating math directly into code. The cleaner the math,the cleaner the resulting code; so much of this book concentrates on using just theright math for the job. This chapter reviews various tools from high school andcollege mathematics and is designed to be used more as a reference than as a tu-torial. It may appear to be a hodge-podge of topics and indeed it is; each topicis chosen because it is a bit unusual in “standard’ math curricula, because it isof central importance in graphics, or because it is not typically treated from a ge-ometric standpoint. In addition to establishing a review of the notation used inthe book, the chapter also emphasizes a few points that are sometimes skippedin the standard undergraduate curricula, such as barycentric coordinates on tri-angles. This chapter is not intended to be a rigorous treatment of the material;instead intuition and geometric interpretation are emphasized. A discussion oflinear algebra is deferred until Chapter 5 just before transformation matrices arediscussed. Readers are encouraged to skim this chapter to familiarize themselveswith the topics covered and to refer back to it as needed. The exercises at the endof the chapter may be useful in determining which topics need a refresher.
图形学的很大一部分就是将数学直接转化为代码。数学越清晰，得到的代码就越清晰；因此，本书的很大一部分集中在选择适合工作的正确数学上。本章回顾了高中和大学数学的各种工具，旨在作为参考而非教程使用。它可能看起来是一个杂乱无章的主题集合，而事实上确实如此；每个主题的选择是因为它在“标准”数学课程中有些不寻常，因为它在图形学中至关重要，或者因为它通常不从几何的角度加以处理。除了建立本书中使用的符号的回顾之外，本章还强调了一些在标准本科课程中有时会被忽略的要点，比如三角形上的重心坐标。本章不旨在对材料进行严格的处理；相反，强调直觉和几何解释。对线性代数的讨论将推迟到第5章，就在讨论变换矩阵之前。鼓励读者略读本章以熟悉所涵盖的主题，并在需要时返回查阅。章末的练习可能有助于确定哪些主题需要温习。

## 2.1 Sets and Mappings 集合和映射

Mappings, also called functions, are basic to mathematics and programming. Likea function in a program, a mapping in math takes an argument of one type and maps it to (returns) an object of a particular type. In a program we say “type; inmath we would identify the set. When we have an object that is a member of aset, we use the $\in$ symbol. For example, $a \in \bold{S} $, can be read "a is a member of set $\bold{S}$." Given any two sets **A** and **B**, we can createa third set by taking the Cartesian product of the two sets, denoted $\bold{A} \cross \bold{B}$. This set $\bold{A} \cross \bold{B}$ is composed of all possible ordered pairs (a, b) where $a \in \bold{A} $ and $b \in \bold{B} $. As a shorthand, we use the notation $\bold{A}^2$to denote $\bold{A} \cross \bold{A} $. We can extendthe Cartesian product to create a set of all possible ordered triples from three sets and so on for arbitrarily long ordered tuples from arbitrarily many sets.
映射，又称为函数，在数学和编程中都是基本的概念。类似于程序中的函数，在数学中，<u>映射接受一种类型的参数并将其映射到（返回）特定类型的对象</u>。在程序中我们说“类型”；而在数学中我们则会确定这个集合。当我们有一个属于某个集合的对象时，我们使用符号 $\in$。例如，$a \in \bold{S}$，可解读为“a是集合 $\bold{S}$ 的成员”。给定任意两个集合 **A** 和 **B**，我们可以通过取这两个集合的笛卡尔积来创建第三个集合，表示为 $\bold{A} \times \bold{B}$。这个集合 $\bold{A} \times \bold{B}$ 包含所有可能的有序对 (a, b)，其中 $a \in \bold{A}$ 且 $b \in \bold{B}$。作为一种简写，我们使用符号 $\bold{A}^2$ 表示 $\bold{A} \times \bold{A}$。我们可以扩展笛卡尔积的概念，从三个集合创建所有可能的有序三元组，以此类推，构建来自任意多个集合的任意长有序元组。

Common sets of interest include
常见的感兴趣的集合包括：

- $\R$ — the real numbers;
- $\R^+$ — the nonnegative real numbers (includes zero)
- $\R^2$ — the ordered pairs in the real 2D plane;
- $\R^n$ — the points in n-dimensional Cartesian space;
- $\Z$ —  the integers;
- $S^2$ — the set of 3D points (points in $\R^3$ ) on the unit sphere.
- $\R$ — 实数;
- $\R$ — 非负实数(包括零)
- $\R^2$ — 实二维平面上的有序对;
- $\R^n$  — n维笛卡尔空间中的点;
- $\Z$  — 整数;
- $S^2$ — 单位球面上的3D点($\R^3$中的点)的集合。

Note that although $S^2$ is composed of points embedded in three-dimensional space, they are on a surface that can be parameterized with two variables, so it can be thought of as a 2D set. Notation for mappings uses the arrow and a colon,for example:
请注意，尽管 $S^2$ 由嵌入在三维空间中的点组成，但它们位于一个可以用两个变量参数化的表面上，因此可以被视为一个二维集合。映射的符号使用箭头和冒号，例如：
$f:\R \mapsto \Z$

which you can read as “There is a function called $f$ that takes a real number as input and maps it to an integer." Here, the set that comes before the arrow is called the domain of the function, and the set on the right-hand side is called the target. Computer programmers might be more comfortable with the following equivalent language: “There is a function called $f$ which has one real argument and returns an integer." In other words, the set notation above is equivalent to the common programming notation:
你可以理解为：“存在一个名为 $f$ 的函数，接受一个实数作为输入，并将其映射到一个整数。” 在这里，箭头前面的集合被称为函数的定义域，右侧的集合被称为目标集。对于计算机程序员来说，下面的等价语言可能更为熟悉：“存在一个名为 $f$ 的函数，它有一个实数参数并返回一个整数。” 换句话说，上面的集合表示法与常见的编程表示法是等价的：
$integer\ f(real) \leftarrow equivalent \rightarrow f:\R \mapsto \Z.$

So the colon-arrow notation can be thought of as a programming syntax. It’s that simple.
所以冒号箭头符号可以被看作是一种编程语法。就是这么简单。

The point $f(a)$ is called the image of $a$, and the image of a set $A$ (a subset of the domain) is the subset of the target that contains the images of all points in $A$. The image of the whole domain is called the range of the function. 
点 $f(a)$ 被称为 $a$ 的像，而集合 $A$（定义域的子集）的像是目标中包含 $A$ 中所有点的子集。整个定义域的像被称为函数的值域。

### 2.1.1 Inverse Mappings 逆映射

If we have a function $f:\bold{A} \mapsto \bold{B}$, there may exist an inverse function $f^{-1}:\bold{B} \mapsto \bold{A}$, which is defined by the rule $f^{-1}(b) = a$ where $b = f(a)$. This definition only works if every $b \in \bold{B}$ is an image of some point under $f$ (that is, the range equals the target) and if there is only one such point (that is, there is only one $a$ for which $f(a) = b$). Such mappings or functions are called bijections. A bijection maps every $a \in A$ to a unique $b \in \bold{B}$, and for every $b \in \bold{B}$, there is exactly one $a \in \bold{A}$ such that $f(a) = b$ (Figure 2.1). A bijection between a group of riders and horses indicates that everybody rides a single horse, and every horse is ridden. The two functions would be rider(horse) and horse(rider). These are inverse functions of each other. Functions that are not bijections have no inverse (Figure 2.2).
如果我们有一个函数 $f: \bold{A} \mapsto \bold{B}$，可能存在一个逆函数 $f^{-1}: \bold{B} \mapsto \bold{A}$，其定义规则为 $f^{-1}(b) = a$，其中 $b = f(a)$。这个定义只有在每个 $b \in \bold{B}$ 都是 $f$ 下某一点的像（即，值域等于目标）且只有一个这样的点（即，只有一个 $a$ 使得 $f(a) = b$）时才成立。这样的映射或函数被称为双射。双射将每个 $A$ 中的 $a$ 映射到唯一的 $B$ 中的 $b$，对于每个 $B$ 中的 $b$，恰好存在一个 $A$ 中的 $a$ 使得 $f(a) = b$（图2.1）。在骑手和马之间存在双射表明每个人骑一匹马，每匹马都被骑。这两个函数分别是 rider(horse) 和 horse(rider)。它们是彼此的逆函数。不是双射的函数没有逆函数（图2.2）。

<img src=".\Images\Figure 2.1.png" alt="Figure 2.1" style="zoom: 67%;" />
Figure 2.1. A bijection $f$ and the inverse function $f^{-1}$. Note that $f^{–1}$ is also a bijection. 
图2.1. 一个双射$f$和反函数$f^{-1}$。注意$f^{-1}$也是一个双射。
![Figure 2.1](.\Images\Figure 2.2.png)
Figure 2.2.The function $g$ does not have an inverse be-cause two elements of $\bold{d}$ map to the same element of $\bold{E}$. The function h has no inverse be-cause element $T$ of $\bold{F}$ has no element of $\bold{d}$ mapped to it.
图2.2. 函数$g$没有逆，因为$\bold{d}$的两个元素映射到$\bold{E}$的同一个元素。函数h没有逆，因为$\bold{F}$的$T$没有$\bold{d}$的元素映射到它。

An example of a bijection is $f : \R \mapsto \R$, with $f(x) = x^3$. The inverse function is $f^{-1}(x) = \sqrt[3]{x}$. This example shows that the standard notation can be somewhat awkward because $x$ is used as a dummy variable in both $f$ and $f^{-1}$. It is sometimes more intuitive to use different dummy variables, with $y = f(x)$ and $x = f^{-1}(y)$. This yields the more intuitive $y = x^3$ and $x = \sqrt[3]{y}$. An example of a function that does not have an inverse is $sqr : \R \mapsto \R$, where $sqr(x) = x^2$. This is true for two reasons: first $x^2 = (-x)^2$, and second no members of the domain map to the negative portions of the target. Note that we can define an inverse if we restrict the domain and range to $\R ^+$. Then  $\sqrt{x}$ is a valid inverse.
一个双射的例子是 $f : \R \mapsto \R$，其中 $f(x) = x^3$。逆函数是 $f^{-1}(x) = \sqrt[3]{x}$。这个例子显示了标准符号可能有些不太自然，因为 $x$ 在 $f$ 和 $f^{-1}$ 中都被用作虚拟变量。有时使用不同的虚拟变量更直观，如 $y = f(x)$ 和 $x = f^{-1}(y)$。这导致更直观的表示 $y = x^3$ 和 $x = \sqrt[3]{y}$。一个没有逆函数的函数的例子是 $sqr : \R \mapsto \R$，其中 $sqr(x) = x^2$。这是因为有两个原因：首先 $x^2 = (-x)^2$，其次定义域的成员没有映射到目标的负部分。请注意，如果我们将定义域和值域限制为 $\R ^+$，那么我们就可以定义一个逆函数，即 $\sqrt{x}$。

### 2.1.2 Intervals 区间

Often we would like to specify that a function deals with real numbers that are restricted in value. One such constraint is to specify an interval. An example of an interval is the real numbers between zero and one, not including zero or one We denote this $(0, 1)$. Because it does not include its endpoints, this is referred to as an open interval. The corresponding closed interval, which does contain its endpoints,is denoted with square brackets: $[0, 1]$ . This notation can be mixed, i.e. $[0, 1)$ includes zero but not one. When writing an interval $[a, b]$, we assume that $a \le b$. The three common ways to represent an interval are shown in Figure 2.3.The Cartesian products of intervals are often used. For example, to indicate that a point x is in the unit cube in 3D, we say $x \in [0, 1]^3$.
通常，我们希望指定函数处理受限制的实数。其中一种约束是指定区间。区间的一个例子是介于零和一之间的实数，不包括零或一，我们用$(0, 1)$表示。因为它不包括其端点，所以称为开区间。相应的闭区间，它包含其端点，用方括号表示：$[0, 1]$ 。这个符号可以混合使用，即$[0, 1)$包括零但不包括一。在写区间$[a, b]$时，我们假设$a \le b$。表示区间的三种常见方法如图2.3所示。区间的笛卡尔积经常被使用。例如，要表示点x在三维单位立方体中，我们说$x \in [0, 1]^3$。
![Figure 2.3](.\Images\Figure 2.3.png)
Figure 2.3. Three equivalent ways to denote the interval from a to b that includes b but not a.
图2.3. 表示包括b但不包括a的区间a到b的三种等效方法。

Intervals are particularly useful in conjunction with set operations: intersection, union, and difference. For example, the intersection of two intervals is the set of points they have in common. The symbol $\cap$ is used for intersection. For ex-ample, $[3, 5) \cap [4, 6] = [4, 5)$. For unions, the symbol $\cup$ is used to denote points in either interval. For example, $[3, 5) \cup [4, 6] = [3, 6]$. Unlike the first two operators, the difference operator produces different results depending on argument order. The minus sign is used for the difference operator, which returns the points in the left interval that are not also in the right. For example, $[3, 5) - [4, 6] = [3, 4)$ and $[4, 6] - [3, 5) = [5, 6]$. These operations are particularly easy to visualize using interval diagrams (Figure 2.4).
区间在与集合操作结合时特别有用：交集、并集和差集。例如，两个区间的交集是它们共有的点组成的集合。符号 $\cap$ 被用于表示交集。例如，$[3, 5) \cap [4, 6] = [4, 5)$。对于并集，符号 $\cup$ 表示属于任一区间的点。例如，$[3, 5) \cup [4, 6] = [3, 6]$。与前两个运算符不同，差集运算符根据参数顺序产生不同的结果。减号用于表示差集运算符，它返回左区间中而右区间中没有的点。例如，$[3, 5) - [4, 6] = [3, 4)$ 和 $[4, 6] - [3, 5) = [5, 6]$。利用区间图表（图2.4）可以更容易地可视化这些操作。
<img src=".\Images\Figure 2.4.png" alt="Figure 2.3" style="zoom:67%;" />
Figure 2.4. Interval operations on [3,5) and [4,6].
图2.4 在[3,5)和[4,6]上的区间运算。

### 2.1.3 Logarithms 对数

Although not as prevalent today as they were before calculators, logarithms are often useful in problems where equations with exponential terms arise. By definition, every logarithm has $a\ base\ a$. The "log base a" of $x$ is written $\log_a{x}$ and is defined as "the exponent to which a must be raised to get $x$," i.e.,
虽然在计算器出现之前，对数已经不那么普遍了，但在出现指数项方程的问题中，对数还是很有用的。根据定义，每个对数都是"以a为底"。x的“以a为底的对数”写为$\log_a{x}$，并定义为“a的几次方等于x”，即
$y = \log_ax \Leftrightarrow a^y = x$

Note that the logarithm base a and the function that raises a to a power are inverses of each other. This basic definition has several consequences:
注意，以a为底数的对数函数和将a提高到幂的函数是彼此的反函数。这个基本定义有几个后果：
$$
a^{\log_ax} = x \\
\log_a(a^x) = x \\
\log_a(xy) = \log_ax + \log_ay \\
\log_a(x/y) = \log_ax - \log_ay \\
\log_ax = \log_ab\log_bx
$$
When we apply calculus to logarithms, the special number $e = 2.718...$ often turns up. The logarithm with base e is called the natural logarithm. We adopt the common shorthand ln to denote it:
当我们把微积分应用于对数时，经常会出现一个特殊的数字$e = 2.718...$。以e为底的对数称为自然对数。我们采用常见的简写ln来表示它:
$\ln x \equiv \log_ex$

Note that the “$\equiv$” symbol can be read “is equivalent by definition." Like $\pi$, the special number e arises in a remarkable number of contexts. Many fields use a particular base in addition to e for manipulations and omit the base in their notation, i.e., $\log x$. For example, astronomers often use base 10 and theoretical computer scientists often use base 2. Because computer graphics borrows technology from many fields we will avoid this shorthand.
请注意，“$\equiv$”符号可以读作“根据定义是等效的”。像$\pi$一样，特殊数字e在很多情况下都会出现。许多字段使用除e之外的特定基数进行操作，并且在其符号中省略了基数，例如$\log x$。例如，天文学家通常使用10为基数，理论计算机科学家通常使用2为基数。由于计算机图形学借鉴了许多领域的技术，我们将避免这种简写。

The derivatives of logarithms and exponents illuminate why the natural logarithm is “natural’.
对数和指数的导数说明了为什么自然对数是“自然的”。
$$
\frac{d}{dx}\log_ax = \frac{1}{x\ln a} \\
\frac{d}{dx}a^x = a^x\ln a
$$
The constant multipliers above are unity only for $a \equiv e$
上述常数乘数仅在$a \equiv e$时为1。

## 2.2 Solving Quadratic Equations 解二次方程

A quadratic equation has the form
二次方程有这样的形式
$Ax^2 + Bx + C = 0$,
where a is a real unknown, and $A$, $B$, and $C$ are known constants. If you think of a 2D $xy$ plot with $y = Ax^2 + Bx + C$, the solution is just whatever $x$ values are “zero crossings" in $y$. Because $y = Ax^2 + Bx + C$ is a parabola, there will be zero, one, or two real solutions depending on whether the parabola misses, grazes, or hits the x-axis (Figure 2.5).
其中，$a$是一个实数未知数，$A$、$B$和$C$是已知常数。如果你想象一个二维$xy$图，其中$y = Ax^2 + Bx + C$，那么解就是$y$中的“零点”$x$值。因为$y = Ax^2 + Bx + C$是一个抛物线，所以根据抛物线是否与$x$轴相交，会有零个、一个或两个实数解（图2.5）。
<img src=".\Images\Figure 2.5.png" alt="Figure 2.5" style="zoom:67%;" />
Figure 2.5. The geometric interpretation of the roots of a quadratic equation is the intersection points of a parabola with the x-axis
图2.5 二次方程的根的几何解释是抛物线与x轴的交点

To solve the quadratic equation analytically, we first divide by $A$:
为了解析解二次方程，我们首先除以$A$:
$x^2 + \frac{B}{A}x + \frac{C}{A} = 0$

Then we “complete the square“ to group terms:
然后我们“完成平方”来分组项:
$\left(x + \frac{B}{2A} \right)^2 - \frac{B^2}{4A^2} + \frac{C}{A} = 0 \\$

Moving the constant portion to the right-hand side and taking the square root gives
把常数部分移到右边开方得到
$x + \frac{B}{2A} = \pm \sqrt{\frac{B^2}{4A^2} - \frac{C}{A}} \\$

Subtracting $B/(2A)$ from both sides and grouping terms with the denominator $2A$ gives the familiar form:
将$B/(2A)$从两边减去并将分母为$2A$的项分组，得到熟悉的形式：

$x = \frac{-B \pm \sqrt{B^2 - 4AC}}{2A}  \ \ \ (2.1) \\ $

> A robust implementation will use the equivalent expression $2C/(-B \mp \sqrt{B^2 - 4AC})$ to compute one of the roots, depending on the sign of $B$(Exercise 7).
> 一种强健的实现将使用等效表达式$2C/(-B \mp \sqrt{B^2 - 4AC})$来计算其中一个根，具体取决于B的符号（练习7）。

Here the "$\pm$" symbol means there are two solutions, one with a plus sign and one with a minus sign. Thus $3\pm1$ equals “two or four.” Note that the term that determines the number of real solutions is
这里的 "$\pm$" 符号表示有两个解，一个带正号，一个带负号。因此，$3\pm1$ 等于 "二或四"。注意，决定实数解个数的术语是

$$D \equiv B^2 -4AC$$

which is called the discriminant of the quadratic equation. If $D > 0$, there are two real solutions (also called roots). If $D = 0$, there is one real solution (a “double" root). If $D < 0$, there are no real solutions.
这被称为二次方程的判别式。如果$D > 0$，则有两个实数解（也称为根）。如果$D = 0$，则有一个实数解（“双重”根）。如果$D < 0$，则没有实数解。

For example, the roots of $2.2 + 6x + 4 = 0$ are $x = -1$ and $x = -2$, and the equation $x^2+x+1$ has no real solutions. The discriminants of these equations are $D = 4$ and $D = -3$, respectively, so we expect the number of solutions given. In programs, it is usually a good idea to evaluate $D$ first and return “no roots" without taking the square root if $D$ is negative.
例如，$2.2 + 6x + 4 = 0$的根为$x = -1$和$x = -2$，而方程$x^2+x+1$ 没有实数解。这些方程的判别式分别为$D = 4$和$D = -3$，因此我们期望给出解的数量。在程序中，通常最好先计算$D$，如果$D$为负，则返回“无解”而不进行平方根运算。

## 2.3 Trigonometry 三角函数

In graphics we use basic trigonometry in many contexts. Usually, it is nothing too fancy, and it often helps to remember the basic definitions.
在图形学中，我们在很多情况下使用基本的三角函数。通常，它不会太花哨，而且它通常有助于记住基本定义。

### 2.3.1 Angles 角度

Although we take angles somewhat for granted, we should return to their definition so we can extend the idea of the angle onto the sphere. An angle is formed between two half-lines (infinite rays stemming from an origin) or directions, and some convention must be used to decide between the two possibilities for the angle created between them as shown in Figure 2.6. An angle is defined by the length of the arc segment it cuts out on the unit circle. A common convention is that the smaller arc length is used, and the sign of the angle is determined by the order in which the two half-lines are specified. Using that convention, all angles are in the range $[-\pi, \pi]$.
虽然我们有点理所当然地考虑角度，但我们应该回到它们的定义，以便我们可以将角度的概念扩展到球体上。 角度是由两个半线（源自原点的无限射线）或方向之间形成的，必须使用某种约定来决定它们之间创建的角度的两种可能性，如图2.6所示。 角度由它在单位圆上切出的弧段长度定义。 通常的约定是使用较小的弧长，并通过指定两个半线的顺序来确定角度的符号。 使用该约定，所有角度都在$[-\pi, \pi]$范围内。
![Figure 2.6](.\Images\Figure 2.6.png)
Figure 2.6 Two half-lines cut the unit circle into two arcs. The length of either arc is a valid angle “between” the two half-lines. Either we can use the convention that the smaller length is the angle, or that the two half-lines are specified in a certain order and the arc that determines angle $\varphi$ is the one swept out counterclockwise from the first to the second half-line. 
图2.6 两条半射线将**单位圆**分割成两个弧。**任一弧的长度都是两条半射线之间有效的角度**。我们可以采用较小长度为角度的约定，或者规定两条半射线的顺序，并且确定角度 $\varphi$ 的弧是从第一条半射线逆时针扫过到第二条半射线的弧。

Each of these angles is the length of the arc of the unit circle that is “cut” by the two directions. Because the perimeter of the unit circle is $2\pi$, the two possible angles sum to $2\pi$. The unit of these arc lengths is radians. Another common unit is degrees, where the perimeter of the circle is 360 degrees. Thus, an angle that is $\pi$ radians is 180 degrees, usually denoted 180◦. The conversion between degrees and radians is 
每个角度都是由两个方向“切割”的单位圆的弧的长度。由于单位圆的周长为$2\pi$，因此两个可能的角度之和为$2\pi$。这些弧长的单位是弧度。另一个常见的单位是度，其中圆的周长为360度。因此，一个$\pi$弧度的角度是180度，通常表示为180◦。度和弧度之间的转换公式为
$$
degrees = \frac{180}{\pi} radians; \\
radians = \frac{\pi}{180} degrees.\\
$$

### 2.3.2 Trigonometric Functions 三角函数

Given a right triangle with sides of length $a$, $o$, and $h$, where h is the length of the longest side (which is always opposite the right angle), or hypotenuse, an important relation is described by the Pythagorean theorem:
考虑一个直角三角形，其三边长度分别为 $a$、$o$ 和 $h$，其中 $h$ 是最长边的长度（始终位于直角的对边），也称为斜边。这时，一个重要的关系由毕达哥拉斯定理（勾股定理）描述：
$a^2 + o^2 = h^2$

You can see that this is true from Figure 2.7, where the big square has area $(a+o)^2$, the four triangles have the combined area $2ao$, and the center square has area $h^2$.
从图2.7中可以看出，大正方形的面积为$(a+o)^2$，四个三角形的总面积为$2ao$，中心正方形的面积为$h^2$。![Figure 2.7](.\Images\Figure 2.7.png)
Figure 2.7.A geometric demonstration of the Pythagorean theorem.
图2.7 毕达哥拉斯定理的几何证明。

Because the triangles and inner square subdivide the larger square evenly, we have $2ao + h^2 = (a + o)^2$, which is easily manipulated to the form above.
因为三角形和内正方形平均地细分了较大的正方形，我们得到$2ao + h^2 = (a + o)^2$，这很容易被处理成上面的形式。

We define sine and cosine of $\varphi$, as well as the other ratio-based trigonometric expressions:
我们定义$\varphi$的正弦和余弦，以及其他基于比率的三角表达式:
$$
\sin{\varphi}  ≡ o/h; \\
\csc{\varphi} ≡ h/o; \\
\cos{\varphi} ≡ a/h; \\
\sec{\varphi} ≡ h/a; \\
\tan{\varphi} ≡ o/a; \\
\cot{\varphi} ≡ a/o \\
$$
These definitions allow us to set up polar coordinates, where a point is coded as a distance from the origin and a signed angle relative to the positive x-axis(Figure 2.8). Note the convention that angles are in the range $\varphi \in (-\pi, \pi] $, and that the positive angles are counterclockwise from the positive x-axis. This convention that counterclockwise maps to positive numbers is arbitrary, but it is used in many contexts in graphics so it is worth committing to memory.
这些定义使我们能够建立极坐标系，其中一个点的编码是相对于原点的距离和相对于正 x 轴的有符号角度（图2.8）。请注意，角度的约定是 $\varphi \in (-\pi, \pi]$ 范围内，正角是相对于正 x 轴逆时针方向的。逆时针映射到正数的这种约定是任意的，但在许多图形上下文中都被使用，因此值得记住。
![Figure 2.8](.\Images\Figure 2.8.png)
Figure 2.8. Polar coordinates for the point $(x_a, y_a) = (1, \sqrt{3})$ is $(r_a, \varphi_a) = (2, \pi/3)$.
图2.8.  点$(x_a, y_a) = (1, \sqrt{3})$ 的极坐标为$(r_a, \varphi_a) = (2, \pi/3)$。

Trigonometric functions are periodic and can take any angle as an argument. For example, $\sin(A) = \sin(A + 2)$. This means the functions are not invertible when considered with the domain $\R$. This problem is avoided by restricting the range of standard inverse functions, and this is done in a standard way in almost all modern math libraries (e.g., (Plauger, 1991)). The domains and ranges are:
三角函数是周期性的，可以将任何角度作为参数。例如，$\sin(A) = \sin(A + 2\pi)$。这意味着在定义域$\R$上，这些函数不可逆。这个问题可以通过限制标准反函数的范围来避免，这在几乎所有现代数学库中都是以标准方式完成的（例如，（Plauger，1991））。定义域和值域如下：
$$
\asin: [-1, 1] \mapsto [-\pi/2, \pi/2] \\
\acos: [-1, 1] \mapsto [0, \pi] \\
\atan: \R \mapsto [-\pi/2, \pi/2] \\
\atan2: \R^2 \mapsto [-\pi, \pi] \\
$$
The last function, $\atan2(s, c)$ is often very useful. It takes an $s$ value proportional to $\sin A$ and a $c$ value that scales $\cos A$ by the same factor and returns $A$. The factor is assumed to be positive. One way to think of this is that it returns the angle of a 2D Cartesian point $(s, c)$ in polar coordinates (Figure 2.9).
最后一个函数，$\atan2(s, c)$，通常非常有用。它接受一个与 $\sin A$ 成比例的 $s$ 值和一个通过相同因子缩放 $\cos A$ 的 $c$ 值，并返回 $A$。假定该因子为正。可以将其理解为返回极坐标中二维笛卡尔坐标点 $(s, c)$ 的角度（图2.9）。
![Figure 2.9](.\Images\Figure 2.9.png)
Figure 2.9. The function $\atan2(s,c)$ returns the angle $A$ and is often very useful in graphics 
图2.9 函数$\atan2(s,c)$返回角度$A$，在图形中通常非常有用

### 2.3.3 Useful Identities 有用的公式

This section lists without derivation a variety of useful trigonometric identities.
本节不加推导地列出了各种有用的三角恒等式。
$$
Shifting\ identities:正负号转换 \\
\sin(−A) = − \sin A \\
\cos(−A) = \cos A	\\
\tan(−A) = − \tan A	\\
\sin(\pi/2 − A) = \cos A	\\
\cos(\pi/2 − A) = \sin A	\\
\tan(\pi/2 − A) = \cot A	\\
$$

$$
Pythagorean\ identities: 
毕达哥拉斯恒等式：\\
\sin^2 A + \cos^2 A = 1 \\
\sec^2 A − \tan^2 A = 1 \\
\csc^2 A − \cot^2 A = 1 \\
$$

$$
Addition\ and\ subtraction\ identities: 加法与减法恒等式：\\
\sin(A + B) = \sin A \cos B + \sin B \cos A \\
\sin(A − B) = \sin A \cos B − \sin B \cos A \\
\sin(2A) = 2\sin A \cos A \\
\cos(A + B) = \cos A \cos B − \sin A \sin B \\
\cos(A − B) = \cos A \cos B + \sin A \sin B \\
\cos(2A) = \cos^2 A − \sin^2 A \\
\tan(A + B) = \frac{\tan A + \tan B}{1 − \tan A \tan B} \\
\tan(A − B) = \frac{\tan A − \tan B}{1 + \tan A \tan B} \\
\tan(2A) = \frac{2 tan A}{ 1 − tan^2A} \\
$$

$$
Half-angle\ identities: \\
\sin^2(A/2) = (1 − \cos A)/2 \\
\cos^2(A/2) = (1 + \cos A)/2 \\
$$

$$
Product\ identities: \\
\sin A \sin B = −(\cos(A + B) − \cos(A − B))/2 \\
\sin A \cos B = (\sin(A + B) + \sin(A − B))/2 \\
\cos A \cos B = (\cos(A + B) + \cos(A − B))/2 \\
$$

The following identities are for arbitrary triangles with side lengths $a$, $b$, and $c$,each with an angle opposite it given by $A$, $B$, $C$, respectively (Figure 2.10):
下列恒等式适用于边长为$a$， $b$和$c$的任意三角形，每个三角形的对角分别为$a$， $b$， $c$(图2.10):![Figure 2.10](.\Images\Figure 2.10.png)
Figure 2.10. Geometry for triangle laws 
图2.10 三角形定律的几何
$$
\frac{\sin A}{a} = \frac{\sin B}{b} = \frac{\sin C}{c} \ \ (Law\ of\ sines) \\
c^2 = a^2 + b^2 - 2ab\cos C \ \ \ (Law\ of\ cosines) \\
\frac{a + b}{a - b} = \frac{\tan{(\frac{A+B}{2})}}{\tan{(\frac{A-B}{2})}} \ \ \ (Law\ of\ tangents)
$$
The area of a triangle can also be computed in terms of these side lengths: 
三角形的面积也可以用这些边长来计算:
$triangle\ area = \frac{1}{4}\sqrt{ (a + b + c)(-a + b + c)(a - b + c)(a + b - c)} \\  $



## 2.4 Vectors 向量

A vector describes a length and a direction. It can be usefully represented by an arrow. Two vectors are equal if they have the same length and direction even if we think of them as being located in different places (Figure 2.11). As much as possible, you should think of a vector as an arrow and not as coordinates or numbers. At some point we will have to represent vectors as numbers in our programs, but even in code they should be manipulated as objects and only the low-level vector operations should know about their numeric representation (DeRose, 1989). Vectors will be represented as bold characters, e.g., $\bold{a}$. A vector's length is denoted $\|\bold{a}\|$ . A unit vector is any vector whose length is one. The zero vector is the vector of zero length. The direction of the zero vector is undefined.
矢量描述长度和方向。它可以通过箭头有益地表示。如果两个矢量具有相同的长度和方向，即使我们认为它们位于不同的位置，它们也是相等的（图2.11）。在尽可能的情况下，你应该将矢量看作箭头，而不是坐标或数字。在程序中，我们将不得不将矢量表示为数字，但即使在代码中，它们也应该作为对象进行操作，只有低级别的矢量操作应该知道它们的数值表示（DeRose，1989）。矢量将用粗体字符表示，例如，$\bold{a}$。矢量的长度表示为 $|\bold{a}|$。单位矢量是长度为一的任意矢量。零矢量是零长度的矢量，其方向未定义。
![Figure 2.11](.\Images\Figure 2.11.png)
Figure 2.11. These two vectors are the same because they have the same length and direction.
图2.11 这两个向量是相同的因为它们有相同的长度和方向

Vectors can be used to represent many different things. For example, they can be used to store an offset, also called a displacement. If we know “the treasure is buried two paces east and three paces north of the secret meeting place, then we know the offset, but we don't know where to start. Vectors can also be used to store a location, another word for position or point. Locations can be represented as a displacement from another location, Usually there is some understood origin location from which all other locations are stored as offsets. Note that locations are not vectors. As we shall discuss, you can add two vectors. However, it usually does not make sense to add two locations unless it is an intermediate operation when computing weighted averages of a location (Goldman, 1985). Adding two offsets does make sense, so that is one reason why offsets are vectors. But this emphasizes that a location is not an offset; it is an offset from a specific origin location. The offset by itself is not the location.
向量可以用来表示许多不同的东西。例如，它们可用于存储偏移量，也称为位移。如果我们知道“宝藏埋在秘密聚会地点向东两步，向北三步的地方”，那么我们就知道了偏移，但我们不知道从哪里开始。向量也可以用来存储位置，也就是位置或点。位置可以表示为从另一个位置的位移，通常有一个可理解的原点位置，所有其他位置都以偏移量的形式存储。注意，位置不是向量。正如我们将要讨论的，你可以将两个向量相加。然而，除非在计算一个位置的加权平均值时是一个中间操作，否则通常没有意义添加两个位置(Goldman, 1985)。添加两个偏移量是有意义的，这就是为什么偏移量是向量的原因之一。但这强调了位置不是偏移量;它是特定原点位置的偏移量。偏移量本身不是位置。

### 2.4.1 Vector Operations 向量操作

Vectors have most of the usual arithmetic operations that we associate with real numbers. Two vectors are equal if and only if they have the same length and direction. Two vectors are added according to the parallelogram rule. This rule states that the sum of two vectors is found by placing the tail of either vector against the head of the other (Figure 2.12). The sum vector is the vector that “completes the triangle" started by the two vectors. The parallelogram is formed by taking the sum in either order. This emphasizes that vector addition is commutative:
向量具有与实数相关的大多数常用算术运算。两个向量相等当且仅当它们有相同的长度和方向。根据平行四边形规则将两个向量相加。这条规则指出，两个向量的和是通过将任意一个向量的尾部与另一个向量的头部相抵得到的(图2.12)。和向量是由这两个向量开始的“完成三角形”的向量。平行四边形由任意顺序的和构成。这强调了向量加法是可交换的:
$\bold{a} + \bold{b} = \bold{b} + \bold{a} $
![Figure 2.12](.\Images\Figure 2.12.png)
Figure 2.12. Two vectors are added by arranging them head to tail. This can be done in either order 
图2.12 两个向量通过首尾相连的方式相加。这可以按两种顺序进行

Note that the parallelogram rule just formalizes our intuition about displacements. Think of walking along one vector, tail to head, and then walking along the other.  The net displacement is just the parallelogram diagonal. You can also create a unary minus for a vector: $-\bold{a}$ (Figure 2.13) is a vector with the same length as  $\bold{a}$ but opposite direction. This allows us to also define subtraction:
注意平行四边形法则只是形式化了我们对位移的直觉。想象一下沿着一个矢量，从头到尾走，然后沿着另一个矢量走。净位移就是平行四边形的对角线。您还可以为矢量创建一元减号:$-\bold{a}$(图2.13)是一个与$\bold{a}$长度相同但方向相反的矢量。这也允许我们定义减法:
$\bold{b} - \bold{a} \equiv -\bold{a} + \bold{b}$
![Figure 2.13](.\Images\Figure 2.13.png)
Figure 2.13. The vector $-\bold{a}$ has the same length but opposite direction of the vector $\bold{a}$ 
图2.13 向量$-\bold{a}$与向量$\bold{a}$的长度相同，但方向相反

You can visualize vector subtraction with a parallelogram (Figure 2.14). We can write 
你可以用一个平行四边形来可视化向量减法(图2.14)。我们可以写
$\bold{a} + (\bold{b} - \bold{a}) = \bold{b}$
![Figure 2.14](.\Images\Figure 2.14.png)
Figure 2.14. Vector subtraction is just vector addition with a reversal of the second argument 
图2.14 向量减法就是向量加法加上第二个参数的反转

Vectors can also be multiplied. In fact, there are several kinds of products involving vectors. First, we can scale the vector by multiplying it by a real number k. This just multiplies the vector's length without changing its direction. For example, $3.5\bold{a}$ is a vector in the same direction as a but it is 3.5 times as long as a. We discuss two products involving two vectors, the dot product and the cross product, later in this section, and a product involving three vectors, the determinant, in Chapter 5.
向量也可以相乘。事实上，有几种与向量相关的乘积。首先，我们可以把向量乘以一个实数k，这只是乘以向量的长度，而不改变它的方向。例如，$3.5\bold{a}$是与$\bold{a}$方向相同的向量，但它是$\bold{a}$的3.5倍长。我们将在本节后面讨论涉及两个向量的两个乘积，即点积和叉积，以及涉及三个向量的一个乘积，即行列式，在第5章。

### 2.4.2 Cartesian Coordinates of a Vector 向量的笛卡尔坐标

A 2D vector can be written as a combination of any two nonzero vectors which are not parallel. This property of the two vectors is called linear independence. Two linearly independent vectors form a 2D basis, and the vectors are thus referred toas basis vectors. For example, a vector $\bold{c}$ may be expressed as a combination of two basis vectors $\bold{a}$ and $\bold{b}$ (Figure 2.15):
一个二维矢量可以写成任意两个非平行的非零矢量的组合。这两个矢量的这一性质被称为线性独立。两个线性独立的矢量构成一个二维基，因此这些矢量被称为基矢量。例如，一个矢量 $\bold{c}$ 可以表示为两个基矢量 $\bold{a}$ 和 $\bold{b}$ 的组合（图2.15）：
$\bold{c} = a_c\bold{a} + b_c\bold{b} \ \ \ \ \ \ (2.3)$.
<img src=".\Images\Figure 2.15.png" alt="Figure 2.15" style="zoom:80%;" />
Figure 2.15. Any 2D vector $\bold{c}$ is a weighted sum of any two nonparallel 2D vectors $\bold{a}$ and $\bold{b}$.
图2.15 任意二维向量$\bold{c}$是任意两个非平行二维向量$\bold{a}$和$\bold{b}$的加权和。

Note that the weights $a_c$ and $b_c$ are unique. Bases are especially useful if the two vectors are orthogonal, i.e., they are at right angles to each other. It is even more useful if they are also unit vectors in which case they are orthonormal. If we assume two such “special" vectors $\bold{x}$ and $\bold{y}$ are known to us, then we can use them to represent all other vectors in a Cartesian coordinate system, where each vector is represented as two real numbers. For example, a vector $\bold{a}$ might be represented as
注意，权重$a_c$和$b_c$是唯一的。如果两个向量是正交的，即它们彼此成直角，基就特别有用。如果它们也是单位向量的话就更有用了在这种情况下它们是**标准正交**的。如果我们假设两个这样的“特殊向量”$\bold{x}$和$\bold{y}$是已知的，那么我们可以用它们来表示笛卡尔坐标系中的所有其他向量，其中每个向量都用两个实数表示。例如，向量$\bold{a}$可以表示为
$\bold{a} = x_a\bold{x} + y_a\bold{y}$,

where $x_a$ and $y_a$ are the real Cartesian coordinates of the 2D vector $\bold{a}$ (Figure 2.16). Note that this is not really any different conceptually from Equation (2.3), where the basis vectors were not orthonormal. But there are several advantages to a Cartesian coordinate system. For instance, by the Pythagorean theorem, the length of $\bold{a}$ is
其中，$x_a$ 和 $y_a$ 分别是二维矢量 $\bold{a}$ 的实际笛卡尔坐标（图2.16）。请注意，从概念上讲，这与方程（2.3）并没有太大不同，其中基矢量不是正交的。但笛卡尔坐标系有几个优势。例如，根据毕达哥拉斯定理，矢量 $\bold{a}$ 的长度是
$\|\bold{a}\| = \sqrt{x_a^2 + y_a^2}$
<img src=".\Images\Figure 2.16.png" alt="Figure 2.16" style="zoom:80%;" />
Figure 2.16. A 2D Cartesian basis for vectors.
图2.16 向量的二维笛卡尔基

It is also simple to compute dot products, cross products, and coordinates of vectors in Cartesian systems, as we'll see in the following sections.
在笛卡尔坐标系中计算点积、叉积和向量坐标也很简单，我们将在接下来的章节中看到。

By convention we write the coordinates of a either as an ordered pair $(x_a, y_a)$or a column matrix:
按照惯例，我们将$\bold{a}$的坐标写成有序对$(x_a, y_a)$或列矩阵:
$\bold{a} = \begin{bmatrix} x_a \\ y_a \end{bmatrix}$

The form we use will depend on typographic convenience. We will also occasionally write the vector as a row matrix, which we will indicate as $\bold{a}^T$.
我们使用的形式将取决于排版的便利性。我们偶尔也会将向量写成行矩阵，我们将其表示为$\bold{a}^T$。
$\bold{a}^T = \begin{bmatrix} x_a & y_a \end{bmatrix}$

We can also represent 3D, 4D, etc., vectors in Cartesian coordinates. For the 3D case, we use a basis vector z that is orthogonal to both x and y.
我们也可以用笛卡尔坐标表示3D, 4D等向量。对于三维情况，我们使用一个基向量$\bold{z}$，它与$\bold{x}$和$\bold{y}$都正交。



### 2.4.3 Dot Product 点积

The simplest way to multiply two vectors is the dot product. The dot product of $\bold{a}$ and $\bold{b}$ is denoted $\bold{a} \cdot \bold{b}$ and is often called the scalar product because it returns a scalar. The dot product returns a value related to its arguments' lengths and the angle $\varphi$ between them (Figure 2.17):
两个向量相乘最简单的方法是点积。$\bold{a}$和$\bold{b}$的点积表示为$\bold{a} \cdot \bold{b}$，通常称为标量积，因为它返回一个标量。点积返回的值与参数的长度和它们之间的夹角$\varphi$有关(图2.17):
$\bold{a} \cdot \bold{b} = \|\bold{a}\| \|\bold{b}\|\cos\varphi$          (2.4)
![Figure 2.17](.\Images\Figure 2.17.png)
Figure 2.17. The dot product is related to length and angle and is one of the most important formulas in graphics.
图2.17 点积与长度和角度有关，是图形学中最重要的公式之一

The most common use of the dot product in graphics programs is to compute the cosine of the angle between two vectors.
点积在图形程序中最常用的用法是**计算两个向量夹角的余弦值**。

The dot product can also be used to find the projection of one vector onto another. This is the length $\bold{a} \rightarrow \bold{b}$ of a vector $\bold{a}$ that is projected at right angles onto a vector $\bold{b}$ (Figure 2.18):
点积也可以用来求一个向量在另一个向量上的投影。这是向量$\bold{a}$以直角投影到向量$\bold{b}$上的长度$\bold{a} \rightarrow \bold{b}$(图2.18):
$\bold{a} \rightarrow \bold{b} 
	= \|\bold{a}\| \cos\varphi 
	= \frac{\bold{a} \cdot \bold{b}} {\|\bold{b}\|}\\ 
$ （2.5）
![Figure 2.18](.\Images\Figure 2.18.png)
Figure 2.18.The projection of $\bold{a}$ onto $\bold{b}$ is a length found by Equation (2.5).
图2.18 $\bold{a}$到$\bold{b}$的投影是由式(2.5)找到的长度

The dot product obeys the familiar associative and distributive properties we have in real arithmetic:
点积符合我们在实算术中熟悉的结合律和分配律:  (2.6)
$$
\bold{a} \cdot \bold{b} = \bold{b} \cdot \bold{a} \\
\bold{a} \cdot (\bold{b} + \bold{c}) = \bold{a} \cdot \bold{b} + \bold{a} \cdot \bold{c}\\
(k\bold{a}) \cdot \bold{b} = \bold{a} \cdot (k\bold{b}) = k\bold{a}\cdot \bold{b}
$$
If 2D vectors $\bold{a}$ and $\bold{b}$ are expressed in Cartesian coordinates, we can take advantage of $\bold{x} \cdot \bold{x} = \bold{y} \cdot \bold{y} = 1$ and $\bold{x} \cdot \bold{y} = 0$ to derive that their dot product is
如果二维向量$\bold{a}$和$\bold{b}$用笛卡尔坐标表示，我们可以利用$\bold{x} \cdot \bold{x} = \bold{y} \cdot \bold{y} = 1$和$\bold{x} \cdot \bold{y} = 0$推导出它们的点积为
$$
\bold{a} \cdot \bold{b} = (x_a\bold{x} + y_a\bold{y}) \cdot (x_b\bold{x} + y_b\bold{y})\\
= x_ax_b(\bold{x} \cdot \bold{x}) + x_ay_b(\bold{x}\cdot\bold{y}) + x_by_a(\bold{y}\cdot\bold{x}) + y_ay_b(\bold{y} \cdot \bold{y}) \\ 
 = x_ax_b + y_ay_b
$$
Similarly in 3D we can find
在3D中我们也可以发现
$\bold{a} \cdot \bold{b} = x_ax_b +y_ay_b + z_az_b$

### 2.4.4 Cross Product 叉乘

The cross product $\bold{a} \cross \bold{b}$ is usually used only for three-dimensional vectors; generalized cross products are discussed in references given in the chapter notes. The cross product returns a 3D vector that is perpendicular to the two arguments of the cross product. The length of the resulting vector is related to $\sin\varphi$:
叉乘$\bold{a} \cross \bold{b}$通常只用于三维向量；在本章附注的参考文献中讨论了广义叉积。**叉乘返回一个垂直于叉乘的两个参数的三维向量**。结果向量的长度与$\sin\varphi$有关:
$\|\bold{a} \cross \bold{b}\| = \|\bold{a}\|\|\bold{b}\|\sin\varphi$

The magnitude $\|\bold{a} \cross \bold{b}\|$ is equal to the area of the parallelogram formed by vectors $\bold{a}$ and $\bold{b}$. In addition, $\bold{a} \cross \bold{b}$ is perpendicular to both $\bold{a}$ and $\bold{b}$ (Figure 2.19). Note that there are only two possible directions for such a vector. By definition, the vectors in the direction of the x-, y- and z-axes are given by
$\|\bold{a} \cross \bold{b}\|$ 的大小等于由向量 $\bold{a}$ 和 $\bold{b}$ 形成的平行四边形的面积。 此外，$\bold{a} \cross \bold{b}$ 垂直于$\bold{a}$ 和$\bold{b}$（图2.19）。 请注意，这样的向量只有两个可能的方向。 根据定义，x、y 和 z 轴方向上的向量由下式给出
$$
\bold{x} = (1, 0, 0) \\
\bold{y} = (0, 1, 0) \\
\bold{z} = (0, 0, 1) \\
$$
<img src=".\Images\Figure 2.19.png" alt="Figure 2.19" style="zoom:80%;" />
Figure 2.19.The cross product $\bold{a} \cross \bold{b}$ is a 3D vector perpendicular to both 3D vectors $\bold{a}$ and $\bold{b}$, and its length is equal to the area of the parallelogram shown.
图2.19 叉积是一个$\bold{a} \cross \bold{b}$垂直于3D向量$\bold{a}$和$\bold{b}$的三维向量，它的长度等于所示平行四边形的面积

and we set as a convention that $\|\bold{x} \cross \bold{y}\|$must be in the plus or minus z direction. The choice is somewhat arbitrary, but it is standard to assume that
我们设定$\|\bold{x} \cross \bold{y}\|$必须在正负$\bold{z}$方向上。这个选择有些武断，但这是标准的假设
$\bold{z} = \bold{x} \cross \bold{y}$

All possible permutations of the three Cartesian unit vectors are
三个笛卡尔单位向量的所有可能的排列是
$$
\bold{x} × \bold{y} = +\bold{z} ,\\
\bold{y} × \bold{x} = -\bold{z} ,\\
\bold{y} × \bold{z} = +\bold{x} ,\\
\bold{z} × \bold{y} = -\bold{x} ,\\
\bold{z} × \bold{x} = +\bold{y} ,\\
\bold{x} × \bold{z} = -\bold{y} .\\
$$
Because of the $\sin\varphi$ property, we also know that a vector cross itself is the zero-vector, so $\bold{x} \cross \bold{x} = \bold{0}$ and so on. Note that the cross product is not commutative, i.e., $\bold{x} \cross \bold{y} \ne \bold{y} \cross \bold{x}$. The careful observer will note that the above discussion does not allow us to draw an unambiguous picture of how the Cartesian axes relate. More specifically, if we put $\bold{x}$ and $\bold{y}$ on a sidewalk, with $\bold{x}$ pointing east and $\bold{y}$ pointing north, then does $\bold{z}$ point up to the sky or into the ground? The usual convention is to have $\bold{z}$ point to the sky. This is known as a right-handed coordinate system. This name comes from the memory scheme of “grabbing” $\bold{x}$ with your right palm and fingers and rotating it toward $\bold{y}$. The vector $\bold{z}$ should align with your thumb. This is illustrated in Figure 2.20.
由于 $\sin\varphi$ 属性，我们也知道一个向量与其自身的叉积是零向量，因此 $\bold{x} \cross \bold{x} = \bold{0}$ 等等。请注意，叉积不是可交换的，即 $\bold{x} \cross \bold{y} \ne \bold{y} \cross \bold{x}$。细心的观察者会注意到上面的讨论并未让我们明确地描绘出笛卡尔坐标轴之间的关系。更具体地说，如果我们将 $\bold{x}$ 和 $\bold{y}$ 放在水平面上，使 $\bold{x}$ 指向东方，$\bold{y}$ 指向北方，那么 $\bold{z}$ 是指向天空还是地面呢？通常的约定是让 $\bold{z}$ 指向天空。这被称为右手坐标系。这个名字来自于“用右手掌和手指”抓住 $\bold{x}$ 并将其朝着 $\bold{y}$ 旋转的记忆方案。向量 $\bold{z}$ 应该与您的大拇指对齐。这在图2.20中有所说明。
<img src=".\Images\Figure 2.20.png" alt="Figure 2.20" style="zoom:67%;" />
Figure 2.20. The “right-hand rule" for cross products. Imagine placing the base your right palm where $\bold{a}$ and $\bold{b}$ join at their tails, and pushing the arrow of $\bold{a}$ toward $\bold{b}$. Your extended right thumb should point toward $\bold{a} \cross \bold{b}$.
图2.20. 叉乘的“右手法则”。想象一下，将您的右掌的底部放在$\bold{a}$和$\bold{b}$尾部相接的地方，然后将$\bold{a}$的箭头推向$\bold{b}$。您伸出的右手拇指应指向$\bold{a} \cross \bold{b}$。

The cross product has the nice property that
外积有一个很好的性质
$\bold{a} \cross (\bold{b} + \bold{c}) = \bold{a} \cross \bold{b} + \bold{a} \cross \bold{c}$
$\bold{a} \cross (k\bold{b}) = k(\bold{a} \cross \bold{b})$

However,a consequence of the right-hand rule is
然而，右手法则的一个结论是
$\bold{a} \cross \bold{b} = -(\bold{b} \cross \bold{a})$

In Cartesian coordinates, we can use an explicit expansion to compute the cross product:
在笛卡尔坐标系中，我们可以使用显式展开来计算叉乘: (2.7)
$$
\bold{a} \cross \bold{b} 
= 	(x_a\bold{x} + y_a\bold{y} +z_a\bold{z}) 
	\cross 
	(x_b\bold{x} + y_b\bold{y} +z_b\bold{z}) \\
=	x_ax_b\bold{x} \cross \bold{x} + x_ay_b\bold{x} \cross \bold{y}  + x_az_b\bold{x} \cross \bold{z} \\
	 + y_ax_b\bold{y} \cross \bold{x} + y_ay_b\bold{y} \cross \bold{y}  + y_az_b\bold{y} \cross \bold{z} \\
	 + z_ax_b\bold{z} \cross \bold{x} + z_ay_b\bold{z} \cross \bold{y}  + z_az_b\bold{z} \cross \bold{z} \\
= 	(y_az_b - z_ay_b)\bold{x} + (z_ax_b - x_az_b)\bold{y} + (x_ay_b - y_ax_b)\bold{z}
$$
So, in coordinate form,
在坐标形式中，(2.8)
$$
\bold{a} \cross \bold{b} = (y_az_b - z_ay_b,\ z_ax_b - x_az_b,\ x_ay_b - y_ax_b)
$$

### 2.4.5 Orthonormal Bases and Coordinate Frames 标准正交基和坐标框架

Managing coordinate systems is one of the core tasks of almost any graphics program; the key to this is managing orthonormal bases. Any set of two 2D vectors $\bold{u}$ and $\bold{v}$ form an orthonormal basis provided that they are orthogonal (at right angles) and are each of unit length. Thus,
管理坐标系统是几乎所有图形程序的核心任务之一；关键是处理标准正交基。任意两个二维向量$\bold{u}$和$\bold{v}$组成一个正交基，只要它们正交(成直角)且各为单位长度。因此,
$\|\bold{u}\| = \|\bold{v}\| = 1$
$\bold{u} \cdot \bold{v} = 0$

In 3D, three vectors $\bold{u}$, $\bold{v}$, and $\bold{w}$ form an orthonormal basis if 
在三维空间中，三个向量$\bold{u}$， $\bold{v}$和$\bold{w}$构成一个标准正交基
$\|\bold{u}\| = \|\bold{v}\| = \|\bold{w}\| = 1$
$\bold{u} \cdot \bold{v} = \bold{v} \cdot \bold{w} = \bold{w} \cdot \bold{u} = 0$

This orthonormal basis is right-handed provided 
这个标准正交基是右手性的条件是
$\bold{w} = \bold{u} \cdot \bold{v}$

and otherwise it is left-handed.
否则它就是左手的。

Note that the Cartesian canonical orthonormal basis is just one of infinitely many possible orthonormal bases. What makes it special is that it and its implicit origin location are used for low-level representation within a program. Thus,the vectors $\bold{x}$, $\bold{y}$, and $\bold{z}$ are never explicitly stored and neither is the canonical origin location $\bold{o}$. The global model is typically stored in this canonical coordinate system, and it is thus often called the global coordinate system. However, if we want to use another coordinate system with origin $\bold{p}$ and orthonormal basis vectors $\bold{u}$, $\bold{v}$, and $\bold{w}$, then we do store those vectors explicitly. Such a system is called a frame of reference or coordinate frame. For example, in a flight simulator, we might want to maintain a coordinate system with the origin at the nose of the plane, and the orthonormal basis aligned with the airplane. Simultaneously, we would have the master canonical coordinate system (Figure 2.21). The coordinate system associated with a particular object, such as the plane, is usually called a local coordinate system.
注意笛卡尔标准正交基只是无限多可能的标准正交基之一。它的特殊之处在于它和它的隐式原始位置用于程序中的低级表示。因此，向量$\bold{x}$、$\bold{y}$和$\bold{z}$永远不会被显式存储，规范的起始位置$\bold{o}$也不会被显式存储。全局模型通常存储在这个规范坐标系中，因此它通常被称为全局坐标系。然而，如果我们想使用另一个坐标系，它的原点$\bold{p}$和标准正交基向量$\bold{u}$， $\bold{v}$和$\bold{w}$，那么我们需要显式地存储这些向量。这样的系统称为参照系或座标系。例如，在飞行模拟器中，我们可能希望维护一个原点位于飞机机头的坐标系，并且标准正交基与飞机对齐。同时，我们将拥有主规范坐标系(图2.21)。与特定物体(如平面)相关联的坐标系通常称为局部坐标系。<img src=".\Images\Figure 2.21.png" alt="Figure 2.21" style="zoom:50%;" />
Figure 2.21. There is always a master or canonical” coordinate system with origin $\bold{o}$ and orthonormal basis $\bold{x}$, $\bold{y}$, and $\bold{z}$. This coordinate system is usually defined to be aligned to the global model and is thus often called the “global" or “world" coordinate system, This origin and basis vectors are never stored explicitly. All other vectors and locations are stored with coordinates that relate them to the global frame. The coordinate system associated with the plane are explicitly stored in terms of global coordinates.
图2.21 总有一个主或规范的“坐标系”，其原点$\bold{o}$和标准正交基$\bold{x}$、$\bold{y}$和$\bold{z}$。这个坐标系通常被定义为与全局模型对齐，因此通常被称为“全局”或“世界”坐标系。这个原点和基向量从未被显式存储。所有其他向量和位置都存储在与全局框架相关的坐标中。与平面相关的坐标系统以全局坐标的形式显式存储。

At a low level, the local frame is stored in canonical coordinates. For example, if $\bold{u}$ has coordinates $(x_u, y_u, z_u)$,
在较低的层次上，局部帧以规范坐标存储。例如，如果$\bold{u}$具有坐标$(x_u, y_u, z_u)$，

A location implicitly includes an offset from the canonical origin:
一个位置隐式地包含了标准原点的偏移量:
$\bold{p} = \bold{o} + x_p\bold{x} + y_p\bold{y} + z_p\bold{z} $

where$(x_p, y_p, z_p)$ are the coordinates of $\bold{p}$.
其中$(x_p, y_p, z_p)$为$\bold{p}$的坐标。

Note that if we store a vector a with respect to the $\bold{u}-\bold{v}-\bold{w}$ frame, we store a triple $(u_a, v_a, w_a)$ which we can interpret geometrically as
注意，如果我们存储一个向量a相对于$\bold{u}-\bold{v}-\bold{w}$框架，我们存储的是一个三元组$(u_a, v_a, w_a)$，我们可以将其几何解释为
$\bold{a} = u_a\bold{u} + v_a\bold{v} + w_a\bold{w}$

To get the canonical coordinates of a vector $\bold{a}$ stored in the $\bold{u}-\bold{v}-\bold{w}$ coordinate system, simply recall that $\bold{u}$, $\bold{v}$, and $\bold{w}$ are themselves stored in terms of Cartesian coordinates, so the expression $u_a\bold{u} + v_a\bold{v} + w_a\bold{w}$ is already in Cartesian coordinates if evaluated explicitly. To get the $\bold{u}-\bold{v}-\bold{w}$ coordinates of a vector $\bold{b}$ stored in the canonical coordinate system, we can use dot products:
为了得到存储在$\bold{u}-\bold{v}-\bold{w}$坐标系中的向量$\bold{a}$的规范坐标，只需回忆一下$\bold{u}$、$\bold{v}$和$\bold{w}$本身都是用笛卡尔坐标存储的，因此表达式$u_a\bold{u} + v_a\bold{v} + w_a\bold{w}$如果显式求值，就已经是笛卡尔坐标了。为了得到存储在规范坐标系中的向量$\bold{u}-\bold{v}-\bold{w}$的坐标，我们可以使用点积:
$$
u_b = \bold{u} \cdot \bold{b} \\
v_b = \bold{v} \cdot \bold{b} \\
w_b = \bold{w} \cdot \bold{b} \\
$$
This works because we know that for some $u_b$, $v_b$, and $w_b$
这是可行的，因为我们知道对于一些$u_b$， $v_b$和$w_b$
$u_b\bold{u} + v_b\bold{v} + w_b\bold{w} = \bold{b}$

and the dot product isolates the $u_b$ coordinate: 
并且点积隔离了$u_b$坐标:
$\bold{u} \cdot \bold{b} = u_b(\bold{u} \cdot \bold{u}) + v_b(\bold{u} \cdot \bold{v}) + w_b(\bold{u} \cdot \bold{w}) = u_b$

This works because $\bold{u}$, $\bold{v}$, and $\bold{w}$ are orthonormal.
这是因为$\bold{u}$、$\bold{v}$和$\bold{w}$是标准正交的。

Using matrices to manage changes of coordinate systems is discussed in Sections 6.2.1 and 6.5.
使用矩阵来管理坐标系统的变化将在6.2.1节和6.5节中讨论。

### 2.4.6 Constructing a Basis from a Single Vector 从单个向量构造基

Often we need an orthonormal basis that is aligned with a given vector. That is, given a vector $\bold{a}$, we want an orthonormal $\bold{u}$, $\bold{v}$, and $\bold{w}$ such that $\bold{w}$ points in the same direction as $\bold{a}$ (Hughes & Moller, 1999), but we don't particularly care what $\bold{u}$ and $\bold{v}$ are. One vector isn't enough to uniquely determine the answer; we just need a robust procedure that will find any one of the possible bases.
通常我们需要与给定向量对齐的标准正交基。 也就是说，给定一个向量 $\bold{a}$，我们需要一个正交的 $\bold{u}$、$\bold{v}$ 和 $\bold{w}$ 使得 $\bold{w}$ 指向同一方向为 $\bold{a}$ (Hughes & Moller, 1999)，但我们并不特别关心 $\bold{u}$ 和 $\bold{v}$ 是什么。 一个向量不足以唯一地确定答案； 我们只需要一个强大的过程来找到任何一个可能的基。

This can be done using cross products as follows. First make $\bold{w}$ a unit vector in the direction of $\bold{a}$:
这可以使用如下的叉积来实现。首先使$\bold{w}$为$\bold{a}$方向的单位向量:
$\bold{w} = \frac{\bold{a}}{\|\bold{a}\|} \\$

> This same procedure can,of course, be used to con-struct the three vectors in any order; just pay attention to the order of the cross products to ensure the basis is right-handed.
> 当然，同样的过程也可以用来以任意顺序构造这三个向量;只要注意外积的顺序以确保基是右手性的。

Then choose any vector $\bold{t}$ not collinear with $\bold{w}$, and use the cross product to build a unit vector $\bold{u}$ perpendicular to $\bold{w}$:
然后选择任意不与$\bold{w}$共线的向量$\bold{t}$，用叉乘建立一个垂直于$\bold{w}$的单位向量$\bold{u}$:
$\bold{u} = \frac{\bold{t} \cross \bold{w}}{\|\bold{t} \cross \bold{w}\|}\\$

If $\bold{t}$ is collinear with $\bold{w}$ the denominator will vanish, and if they are nearly collinear the results will have low precision. A simple procedure to find a vector sufficiently different from $\bold{w}$ is to start with $\bold{t}$ equal to $\bold{w}$ and change the smallest magnitude component of $\bold{t}$ to 1. For example, if $\bold{w} = (1/\sqrt{2}, -1/ \sqrt{2}, 0)$ then $\bold{t} = (1/\sqrt{2}, -1/ \sqrt{2}, 1)$. Once $\bold{w}$ and $\bold{u}$ are in hand, completing the basis is simple:
如果 $\bold{t}$ 与 $\bold{w}$ 共线，则分母将消失，如果它们几乎共线，则结果的精度将很低。 找到一个与 $\bold{w}$ 足够不同的向量的简单过程是，从 $\bold{t}$ 等于 $\bold{w}$ 开始，并将 $\bold{t}$ 的最小幅度分量更改为 1。 例如，如果 $\bold{w} = (1/\sqrt{2}, -1/ \sqrt{2}, 0)$，则 $\bold{t} = (1/\sqrt{2}, -1/ \sqrt{2}, 1)$。 一旦 $\bold{w}$ 和 $\bold{u}$ 准备就绪，完成基础就很简单了：
$\bold{v} = \bold{w} \cross \bold{u}$

An example of a situation where this construction is used is surface shading, where a basis aligned to the surface normal is needed but the rotation around the normal is often unimportant.
使用这种构造的一个例子是表面着色，其中需要一个与表面法线对齐的基，但围绕法线的旋转通常不重要。

> ChatGPT：
>
> 从单个向量构造基的过程涉及到线性代数中的一些基本概念。一个基是向量空间中的一组线性无关的向量，这组向量能够生成整个向量空间。对于三维空间，我们通常使用三个线性无关的基向量来构造基。下面是从单个向量构造基的一种方法：
>
> 假设我们有一个非零向量 $\bold{v}$，我们希望构造一组基，使得这个向量是这组基的一部分。
>
> 1. **单位化：** 首先，将向量 $\bold{v}$ 单位化，即将其长度归一化为1。我们可以通过将向量除以其长度得到单位向量 $\hat{v}$。
>
>    $\hat{v} = \frac{\bold{v}}{\|\bold{v}\|} \\$
>
> 2. **正交化：** 然后，我们需要构造与 $\hat{v}$ 正交的向量。这可以通过在空间中选择与 $\hat{v}$ 正交的向量 $\bold{u}$ 来实现。
>
>    $\bold{u}=任意选择与\hat{v}正交的向量$
>
> 3. **叉乘得到第三个基向量：** 对于三维空间，我们可以使用叉乘来得到第三个与前两个向量都正交的向量。如果我们选择 $\bold{u}$ 和 $\hat{v}$，那么第三个基向量 $\bold{w}$ 可以通过叉乘计算得到：
>
>    $\bold{w} = \bold{u} \cross \hat{v}$
>
> 现在，我们得到了一组基向量 ${\hat{v}, \bold{u}, \bold{w}}$，它们是线性无关的，且 $\bold{v}$ 可以表示为这组基的线性组合。这是一种方法，实际上，我们可以通过多种方式构造基，具体取决于问题的背景和要求。

> 正交化是一种线性代数中的操作，目的是将一组线性相关的向量转换为一组线性无关的正交或规范正交向量。在正交化的过程中，通过一系列操作，使得得到的向量之间的内积为零，从而增加了向量集合的数学性质。
>
> 有两种常见的正交化方法：Gram-Schmidt 正交化和施密特正交化。
>
> 1. **Gram-Schmidt 正交化：** 对于给定的向量集合 ${\bold{v}_1, \bold{v}_2, \ldots, \bold{v}_n}$，Gram-Schmidt 正交化的步骤如下：
>
>    - 第一个向量不变。
>    - 对于后续的每个向量 $\bold{v}_i$，将其投影到前面所有已经正交化的向量上并从原始向量中减去投影，得到正交化后的向量 $\bold{u}_i$。
>    - 归一化得到单位向量 $\hat{u}_i$。
>
>    这样得到的向量集合 ${\hat{u}_1, \hat{u}_2, \ldots, \hat{u}_n}$ 是一组正交或规范正交向量。
>
> 2. **施密特正交化：** 与Gram-Schmidt类似，但采用了一种递归的方式。对于给定的向量集合 ${\bold{v}_1, \bold{v}_2, \ldots, \bold{v}_n}$，施密特正交化的步骤如下：
>
>    - 对第一个向量 $\bold{v}_1$ 归一化得到单位向量 $\hat{u}_1$。
>    - 对于后续的每个向量 $\bold{v}_i$，将其与前面所有已经正交化的向量进行投影运算，然后减去投影得到正交化后的向量 $\bold{u}_i$。
>    - 归一化得到单位向量 $\hat{u}_i$。
>
>    这样也得到一组正交或规范正交向量。



### 2.4.7 Constructing a Basis from Two Vectors 从两个向量构造基

The procedure in the previous section can also be used in situations where the rotation of the basis around the given vector is important. A common example is building a basis for a camera: it's important to have one vector aligned in the direction the camera is looking, but the orientation of the camera around that vector is not arbitrary, and it needs to be specified somehow. Once the orientation is pinned down, the basis is completely determined. 
上一节中的过程也可用于基础围绕给定向量的旋转很重要的情况。 一个常见的例子是为相机构建基础：将一个向量与相机观察的方向对齐很重要，但相机围绕该向量的方向不是任意的，需要以某种方式指定。 一旦确定了方向，基座标就完全确定了。

A common way to fully specify a frame is by providing two vectors $\bold{a}$ (which specifies $\bold{w}$) and $\bold{b}$ (which specifies $\bold{v}$). If the two vectors are known to be perpendicular it is a simple matter to construct the third vector by $\bold{u} = \bold{b} \cross \bold{a}$.
完全指定框架的常见方法是提供两个向量 $\bold{a}$ （指定 $\bold{w}$）和 $\bold{b}$ （指定 $\bold{v}$） 。 如果已知两个向量是垂直的，那么通过 $\bold{u} = \bold{b} \cross \bold{a}$ 构造第三个向量就很简单了。

> $\bold{u} = \bold{a} \cross \bold{b}$ also produces an orthonormal basis, but it is left-handed.
> $\bold{u} = \bold{a} \cross \bold{b}$也产生一个标准正交基，但它是左手基。

To be sure that the resulting basis really is orthonormal, even if the input vectors weren't quite, a procedure much like the single-vector procedure is advisable:
为了确保结果基确实是标准正交的，即使输入向量不是完全正交的，建议使用类似于单向量过程的过程:
$$
\bold{w} = \frac{\bold{a}}{\|\bold{a}\|} \\
\bold{u} = \frac{\bold{b} \cross \bold{w}}{\|\bold{b} \cross \bold{w} \|} \\ 
\bold{v} = \bold{w} \cross \bold{u}
$$
In fact, this procedure works just fine when $\bold{a}$ and $\bold{b}$ are not perpendicular. In this case, $\bold{w}$ will be constructed exactly in the direction of $\bold{a}$, and $\bold{v}$ is chosen to be the closest vector to $\bold{b}$ among all vectors perpendicular to $\bold{w}$. 
事实上，当$\bold{a}$和$\bold{b}$不垂直时，这个过程工作得很好。在这种情况下，$\bold{w}$将完全按照$\bold{a}$的方向构造，并且$\bold{v}$被选为垂直于$\bold{w}$的所有向量中最接近$\bold{b}$的向量。

This procedure won't work if $\bold{a}$ and $\bold{b}$ are collinear. In this case $\bold{b}$ is of no help in choosing which of the directions perpendicular to $\bold{a}$ we should use: it is perpendicular to all of them.
如果$\bold{a}$和$\bold{b}$共线，此过程将不起作用。在这种情况下，$\bold{b}$对于选择我们应该使用哪个垂直于$\bold{a}$的方向没有帮助:它垂直于所有方向。

In the example of specifying camera positions (Section 4.3), we want to construct a frame that has $\bold{w}$ parallel to the direction the camera is looking, and $\bold{v}$ should point out the top of the camera. To orient the camera upright, we build the basis around the view direction, using the straight-up direction as the reference vector to establish the camera's orientation around the view direction. Setting $\bold{v}$ as close as possible to straight up exactly matches the intuitive notion of “holding the camera straight.”
在指定摄像机位置的示例中（第4.3节），我们希望构建一个坐标系，使得$\bold{w}$与摄像机所朝向的方向平行，而$\bold{v}$应指向相机的顶部。为了使摄像机保持竖直，我们围绕视角方向构建基础，利用垂直方向作为参考向量，以确定摄像机在视角方向周围的方向。将$\bold{v}$尽量设置为垂直向上，与“保持摄像机平直”的直观概念完全相符。

> If you want me to set $\bold{w}$ and $\bold{v}$ to two nonperpendicular directions, something has to give-with this scheme I'll set everything the way you want, except I'll make the smallest change to $\bold{v}$ so that it is in fact perpendicular to $\bold{w}$.
> 如果你想让我把$\bold{w}$和$\bold{v}$设置为两个不垂直的方向，就必须做出一些让步——在这个方案中，我将按照你想要的方式设置所有内容，除了我将对$\bold{v}$做最小的改变，使它实际上垂直于$\bold{w}$。
>
> What will go wrong with the computation if $\bold{a}$ and $\bold{b}$ are parallel?
> 如果$\bold{a}$和$\bold{b}$是平行的，计算会出现什么问题?

### 2.4.8 Squaring Up a Basis 建立基坐标

Occasionally you may find problems caused in your computations by a basis that is supposed to be orthonormal but where error has crept in-due to rounding error in computation, or to the basis having been stored in a file with low precision, for instance.
有时，您可能会发现计算中出现的问题是由本应正交的基导致的，但由于计算中的舍入误差，或者基被存储在低精度文件中，错误已经悄然出现。

The procedure of the previous section can be used; simply constructing the basis anew using the existing $\bold{w}$ and $\bold{v}$ vectors will produce a new basis that is orthonormal and is close to the old one.
前一节的步骤可以被使用；仅仅通过利用已有的$\bold{w}$和$\bold{v}$向量重新构建基础，就能够生成一个新的正交归一基，且与旧基接近。

This approach is good for many applications, but it is not the best available. It does produce accurately orthogonal vectors, and for nearly orthogonal starting bases the result will not stray far from the starting point. However, it is asymmetric: it “favors” $\bold{w}$ over $\bold{v}$ and $\bold{v}$ over $\bold{u}$ (whose starting value is thrown away).It chooses a basis close to the starting basis but has no guarantee of choosing the closest orthonormal basis. When this is not good enough, the SVD (Section 5.4.1)can be used to compute an orthonormal basis that is guaranteed to be closest to the original basis.
这种方法在许多应用中是可行的，但并非最佳选择。它确实能够生成准确正交的向量，对于初始基近乎正交的情况，结果不会偏离初始点太远。然而，它是不对称的：它“偏向”$\bold{w}$而非$\bold{v}$，并且$\bold{v}$优于$\bold{u}$（其初始值被丢弃）。它选择一个接近初始基的基础，但无法保证选择到最接近的正交基。当这还不够好时，可以使用奇异值分解（第5.4.1节）来计算一个确保最接近原始基础的正交基。

## 2.5 Curves and Surfaces 曲线和曲面

The geometry of curves, and especially surfaces, plays a central role in graphics. and here we review the basics of curves and surfaces in 2D and 3D space.
曲线的几何，尤其是曲面，在图形学中起着核心作用。在这里，我们回顾曲线和曲面在二维和三维空间的基础知识。

### 2.5.1 2D Implicit Curves 二维隐式曲线

Intuitively, a curve is a set of points that can be drawn on a piece of paper without lifting the pen. A common way to describe a curve is using an implicit equation. An implicit equation in two dimensions has the form
直观地说，曲线是一组点，不用动笔就可以在纸上画出来。描述曲线的一种常用方法是使用隐式方程。一个二维隐式方程有这样的形式
$f(x,y) = 0$.

The function $f(x,y)$ returns a real value. Points $(x,y)$ where this value is zero are on the curve, and points where the value is nonzero are not on the curve. For example, let's say that $f(x, y)$ is
函数 $f(x,y)$ 返回一个实值。 该值为零的点 $(x,y)$ 位于曲线上，该值非零的点不在曲线上。 例如，假设 $f(x, y)$ 是
$f(x,y)=(x -x_c)^2 + (y - y_c)^2 -r^2$

where $(x_c, y_c)$ is a 2D point and $r$ is a nonzero real number. If we take $f(x, y) = 0$, the points where this equality holds are on the circle with center $(x_c, y_c)$ and radius $r$. The reason that this is called an “implicit” equation is that the points $(x,y)$ on the curve cannot be immediately calculated from the equation and instead must be determined by solving the equation. Thus, the points on the curve are not generated by the equation explicitly, but they are buried somewhere implicitly in the equation.
其中 $(x_c, y_c)$ 是 2D 点，$r$ 是非零实数。 如果我们取 $f(x, y) = 0$，则该等式成立的点位于以 $(x_c, y_c)$ 为圆心、以 $r$ 为半径的圆上。 之所以将其称为“隐式”方程，是因为曲线上的点 $(x,y)$ 无法立即从方程中计算出来，而必须通过求解方程来确定。 因此，曲线上的点不是由方程显式生成的，而是隐式地隐藏在方程中的某个位置。

It is interesting to note that $f$ does have values for all $(x, y)$. We can think of $f$ as a terrain, with sea level at $f = 0$ (Figure 2.22). The shore is the implicit curve. The value of $f$ is the altitude. Another thing to note is that the curve partitions space into regions where $f > 0$, $f < 0$, and $f = 0$. So you evaluate $f$ to decide whether a point is “inside" a curve. Note that $f(x,y) = c$ is a curve for any constant $c$, and $c = 0$ is just used as a convention. For example, if $f(x, y) = x^2 +y^2 - 1$, varying $c$ just gives a variety of circles centered at the origin (Figure 2.23).
有趣的是，我们可以注意到$f$对于所有的$(x, y)$都有值。我们可以将$f$看作是一个地形，其中$f = 0$时为海平面（见图2.22）。海岸线即为隐式曲线，而$f$的值则表示海拔高度。另一个需要注意的地方是，该曲线将空间划分为$f > 0$、$f < 0$和$f = 0$的区域。因此，通过评估$f$的值，我们可以确定一个点是否在曲线的“内部”。需要注意的是，对于任何常数$c$，$f(x, y) = c$都是一条曲线，而$c = 0$只是一种惯例。例如，如果$f(x, y) = x^2 + y^2 - 1$，改变$c$只会得到以原点为中心的各种圆形（见图2.23）。
<img src=".\Images\Figure 2.22.png" alt="Figure 2.22" style="zoom:67%;" />
Figure 2.22. An implicit function $f(x,y) = 0$ can be thought of as a height field where $f$ is the height (top). A path where the height is zero is the implicit curve (bottom).
图 2.22。 隐式函数 $f(x,y) = 0$ 可以被视为高度字段，其中 $f$ 是高度（顶部）。 高度为零的路径是隐式曲线（底部）。

![Figure 2.23](.\Images\Figure 2.23.png)
Figure 2.23. The various circles represented by $f(x, y) = x^2 + y^2 - 1.$
图2.23：由$f(x, y) = x^2 + y^2 - 1$ 表示的各种圆形。

We can compress our notation using vectors. If we have $\bold{c} = (x_c, y_c)$ and $\bold{p} = (x, y)$, then our circle with center c and radius r is defined by those position vectors that satisfy
我们可以使用向量来压缩我们的符号。 如果我们有 $\bold{c} = (x_c, y_c)$ 和 $\bold{p} = (x, y)$，那么以 c 为中心、以 r 为半径的圆由满足以下条件的位置向量定义：
$(\bold{p} - \bold{c} )\cdot (\bold{p} - \bold{c}) -r^2 = 0$

This equation, if expanded algebraically, will yield Equation (2.9), but it is easier to see that this is an equation for a circle by “reading” the equation geometrically. It reads, “points $\bold{p}$ on the circle have the following property: the vector from $\bold{c}$ to $\bold{p}$ when dotted with itself has value $r^2$." Because a vector dotted with itself is just its own length squared, we could also read the equation as, “points $\bold{p}$ on the circle have the following property: the vector from $\bold{c}$ to $\bold{p}$ has squared length $r^2$."
这个方程，如果代数上展开，将得到方程（2.9），但通过在几何上“阅读”方程，我们更容易看出这是一个描述圆的方程。它的含义是：“圆上的点 $\bold{p}$ 具有以下特性：从 $\bold{c}$ 到 $\bold{p}$ 的向量与自身点乘的结果为 $r^2$。”由于向量与自身点乘的结果就是它的长度的平方，我们也可以将这个方程理解为：“圆上的点 $\bold{p}$ 具有以下特性：从 $\bold{c}$ 到 $\bold{p}$ 的向量的平方长度为 $r^2$。”

Even better, is to observe that the squared length is just the squared distance from $\bold{c}$ to $\bold{p}$, which suggests the equivalent form
更好的是，观察到平方长度只是从 $\bold{c}$ 到 $\bold{p}$ 的平方距离，这表明了等效形式
$\|\bold{p} - \bold{c}\|^2 - r^2 = 0$

and, of course, this suggests
当然，这表明
$\|\bold{p} - \bold{c}\| - r = 0$

The above could be read “the points $\bold{p}$ on the circle are those a distance $r$ from the center point $\bold{c}$,which is as good a definition of circle as any. This illustrates that the vector form of an equation often suggests more geometry and intuition than the equivalent full-blown Cartesian form with $x$ and $y$. For this reason, itis usually advisable to use vector forms when possible. In addition, you can support a vector class in your code; the code is cleaner when vector forms are used. The vector-oriented equations are also less error prone in implementation: once you implement and debug vector types in your code, the cut-and-paste errors involving $x$, $y$, and $z$ will go away. It takes a little while to get used to vectors in these equations, but once you get the hang of it, the payoff is large.
上述内容可以解读为‘圆上的点 $\bold{p}$ 是距离中心点 $\bold{c}$ 为 $r$ 的点，这是对圆的一种非常恰当的定义。这表明，方程的向量形式往往比具有 $x$ 和 $y$ 的等效笛卡尔形式更容易理解。因此，通常建议在可能的情况下使用向量形式。此外，在您的代码中使用向量形式可以支持向量类；使用向量形式时，代码更为清晰。基于向量的方程在实现中也更不容易出错：一旦您在代码中实现并调试了向量类型，涉及 $x$、$y$ 和 $z$ 的剪切粘贴错误将不再存在。适应在这些方程中使用向量可能需要一些时间，但一旦掌握，带来的回报是十分可观的。

### 2.5.2 The 2D Gradient 二维梯度

If we think of the function $f(x, y)$ as a height field with $height = f(x,y)$, the gradient vector points in the direction of maximum upslope, i.e., straight uphill. The gradient vector $\nabla f(x, y)$ is given by 
如果我们将函数$f(x, y)$视为一个高度场，其中$height = f(x, y)$，那么斜率向量指向最大上坡的方向，即笔直上山的方向。斜率向量$\nabla f(x, y)$由以下表达式给出：
$\nabla f(x, y) = \left(\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}\right) \\$ 

The gradient vector evaluated at a point on the implicit curve $f(x,y) = 0$ is perpendicular to the tangent vector of the curve at that point. This perpendicular vector is usually called the normal vector to the curve. In addition, since the gradient points uphill, it indicates the direction of the $f(x, y) > 0$ region.
在隐式曲线 $f(x,y) = 0$ 上的一点处计算的斜率向量垂直于该点处曲线的切向量。 该垂直矢量通常称为曲线的法向矢量。 另外，由于梯度指向上坡，因此它指示$f(x,y) > 0$区域的方向。

In the context of height fields, the geometric meaning of partial derivatives and gradients is more visible than usual. Suppose that near the point $(a, b)$, $f(x, y)$ is a plane (Figure 2.24). There is a specific uphill and downhill direction. At right angles to this direction s a direction that is level with respect to the plane. Any intersection between the plane and the $f(x,y) = 0$ plane will be in the direction that is level. Thus the uphill/downhill directions will be perpendicular to the line of intersection $f(x, y) = 0$. To see why the partial derivative has something to do with this, we need to visualize its geometric meaning. Recall that the conventional derivative of a 1D function $y = g(x)$ is
在高度场的语境中，偏导数和梯度的几何意义比平常更为明显。假设在点$(a, b)$附近，$f(x, y)$是一个平面（见图2.24）。存在特定的上坡和下坡方向。与这个方向垂直的是相对于平面水平的方向。平面与$f(x, y) = 0$平面的任何交点将在水平方向上。因此，上坡和下坡方向将与交线$f(x, y) = 0$的方向垂直。为了理解偏导数与此的关系，我们需要直观地看到其几何意义。回想一维函数$y = g(x)$的常规导数是
$$
\frac{dy}{dx} = \lim\limits_{\Delta x\to 0}\frac{\Delta y}{\Delta x} = 
\lim\limits_{\Delta x\to 0}\frac{g(x + \Delta x) - g(x)}{\Delta x} \ \ \ \ (2.10)
$$
<img src=".\Images\Figure 2.24.png" alt="Figure 2.24" style="zoom:67%;" />
Figure 2.24. A surface $height = f(x, y)$ is locally planar near $(x,y) = (a,b)$. The gradient is a projection of the up-hill direction onto the $height = 0$ plane.
图2.24. 在点$(x,y) = (a,b)$附近，表面$height = f(x, y)$在局部是平面的。梯度是上坡方向在$height = 0$平面上的投影。

This measures the slope of the tangent line to $g$ (Figure 2.25)
这测量了 $g$ 切线的斜率（图 2.25）
![Figure 2.25](.\Images\Figure 2.25.png)
Figure 2.25. The derivative of a 1D function measures the slope of the line tangent to the curve.
图 2.25  一维函数的导数测量与曲线相切的直线的斜率

The partial derivative is a generalization of the 1D derivative. For a 2D function $f(x,y)$, we can't take the same limit for $x$ as in Equation (2.10), because $f$ can change in many ways for a given change in $x$. However, if we hold $y$ constant, we can define an analog of the derivative, called the partial derivative(Figure 2.26):
偏导数是一维导数的推广。 对于 2D 函数 $f(x,y)$，我们不能对 $x$ 采取与等式 (2.10) 中相同的限制，因为对于 $x$ 的给定变化，$f$ 可以以多种方式变化。 然而，如果我们**保持 $y$ 不变**，我们可以定义导数的模拟，称为偏导数（图 2.26）：
$\frac{\Delta f}{\Delta x} = 
\lim\limits_{\Delta x\to 0}\frac{f(x + \Delta x, y) - f(x, y)}{\Delta x} \\$
![Figure 2.26](.\Images\Figure 2.26.png)
Figure 2.26.The partial derivative of a function $f$ with respect to $x$ must hold $y$ constant to have a unique value, as shown by the dark point. The hollow points show other values of $f$ that do not hold $y$ constant.
图 2.26. 函数 $f$ 对 $x$ 的偏导数必须保持 $y$ 恒定才能具有唯一值，如黑点所示。 空心点显示不保持 $y$ 恒定的 $f$ 的其他值

Why is it that the partial derivatives with respect to $x$ and $y$ are the components of the gradient vector? Again, there is more obvious insight in the geometry than in the algebra. In Figure 2.27, we see the vector $\bold{a}$ travels along a path where $\bold{f}$ does not change. Note that this is again at a small enough scale that the surface height $(x,y) = f(x, y)$ can be considered locally planar. From the figure, we see that the vector $\bold{a} = (\Delta x, \Delta y)$.
为什么$x$和$y$的偏导数是梯度向量的分量？ 同样，几何中的洞察力比代数中的洞察力更明显。 在图 2.27 中，我们看到向量 $\bold{a}$ 沿着 $\bold{f}$ 不变的路径行进。 请注意，这也是在足够小的尺度上，表面高度 $(x,y) = f(x, y)$ 可以被视为局部平面。 从图中我们看到向量$\bold{a} = (\Delta x, \Delta y)$。
![Figure 2.27](.\Images\Figure 2.27.png)
Figure 2.27.The vector $\bold{a}$ points in a direction where $f$ has no change and is thus perpendicular to the gradient vector $\nabla f$.
图 2.27.向量 $\bold{a}$ 指向 $f$ 没有变化的方向，因此垂直于梯度向量 $\nabla f$。


Because the uphill direction is perpendicular to $\bold{a}$, we know the dot product is equal to zero:
因为上坡方向垂直于$\bold{a}$，所以我们知道点积等于0：
$(\nabla f) · \bold{a} ≡ (x_∇, y_∇) \cdot (x_a, y_a) = x_∇Δx + y_∇Δy = 0.  \ \ \ \  \ \ (2.11)$

We also know that the change in $f$ in the direction $(x_a, y_a)$ equals zero: 
我们还知道 $f$ 在 $(x_a, y_a)$ 方向上的变化为零：
$Δf = \frac{∂f}{∂x}Δx + \frac{∂f}{∂y} Δy ≡ \frac{∂f}{∂x}x_a + \frac{∂f}{∂y}y_a = 0   \\$

Given any vectors $(x, y)$ and $(x', y')$ that are perpendicular, we know that the angle between them is 90 degrees, and thus their dot product equals zero (recall that the dot product is proportional to the cosine of the angle between the two vectors). Thus, we have $xx' + yy' = 0$. Given $(x, y)$, it is easy to construct valid vectors whose dot product with $(x, y)$ equals zero, the two most obvious being $(y, -x)$ and $(-y, x)$; you can verify that these vectors give the desired zero dot product with $(x, y)$. A generalization of this observation is that $(x, y)$ is perpendicular to $k(y, -x)$ where $k$ is any nonzero constant. This implies that
给定任何垂直的向量 $(x, y)$ 和 $(x', y')$，我们知道它们之间的角度为 90 度，因此它们的点积为零（回想一下，点积与 为两个向量之间角度的余弦）。 因此，我们有 $xx' + yy' = 0$。 给定 $(x, y)$，很容易构造有效向量，其与 $(x, y)$ 的点积等于 0，最明显的两个是 $(y, -x)$ 和 $(-y, x) )$; 您可以验证这些向量是否与 $(x, y)$ 提供了所需的零点积。 这一观察的概括是 $(x, y)$ 垂直于 $k(y, -x)$，其中 $k$ 是任何非零常数。 这意味着
$$
(x_a, y_a) = k\left(\frac{∂f}{∂y}, −\frac{∂f}{∂x} \right)  \ \ \ \ (2.12)
$$
Combining Equations (2.11) and (2.12) gives
结合方程（2.11）和（2.12）得出
$(x_∇, y_∇) = k'\left(\frac{∂f}{∂x} ,\frac{∂f}{∂y} \right)\\ $

where $k'$ is any nonzero constant. By definition,“uphill" implies a positive change in $f$, so we would like $k' > 0$, and $k' = 1$ is a perfectly good convention.
其中 $k'$ 是任何非零常数。 根据定义，“上坡”意味着 $f$ 发生积极变化，因此我们希望 $k' > 0$，而 $k' = 1$ 是一个非常好的约定。

As an example of the gradient, consider the implicit circle $x^2 + y^2 - 1 = 0$ with gradient vector $(2x,2y)$, indicating that the outside of the circle is the positive region for the function $f(x,y) = x^2 + y^2 - 1$. Note that the length of the gradient vector can be different depending on the multiplier in the implicit equation. For example, the unit circle can be described by $Ax^2 + Ay^2 - A = 0$ for any nonzero $A$. The gradient for this curve is $(2Ax, 2Ay)$. This will be normal (perpendicular) to the circle, but will have a length determined by $A$. For $A > 0$, the normal will point outward from the circle, and for $A < 0$, it will point inward. This switch from outward to inward is as it should be, since the positive region switches inside the circle. 
作为梯度的一个例子，考虑隐式圆 $x^2 + y^2 - 1 = 0$，其梯度向量为 $(2x, 2y)$，表明圆的外部是函数 $f(x, y) = x^2 + y^2 - 1$ 的正区域。请注意，梯度向量的长度可能会因隐式方程中的乘数而异。例如，单位圆可以用 $Ax^2 + Ay^2 - A = 0$ 描述，其中 $A$ 是任意非零常数。该曲线的梯度为 $(2Ax, 2Ay)$。这将是与圆正交的法向量，但其长度由 $A$ 决定。对于 $A > 0$，法向量将指向圆外，而对于 $A < 0$，法向量将指向圆内。这从外向内的转变是合理的，因为正区域在圆内部发生了变化。

In terms of the height-field view, $h = Ax^2 + Ay^2 - A$, and the circle is at zero altitude. For $A > 0$, the circle encloses a depression, and for $A < 0$, the circle encloses a bump. As $A$ becomes more negative, the bump increases in height, but the $h = 0$ circle doesn't change. The direction of maximum uphill doesn't change, but the slope increases. The length of the gradient reflects this change in degree of the slope. So intuitively, you can think of the gradient's direction as pointing uphill and its magnitude as measuring how uphill the slope is.
从高度场的角度来看，$h = Ax^2 + Ay^2 - A$，而圆位于零高度。对于 $A > 0$，圆围绕着一个凹陷，而对于 $A < 0$，圆围绕着一个凸起。随着 $A$ 变得更加负数，凸起的高度增加，但 $h = 0$ 圆不发生变化。最大上坡的方向不变，但坡度增加。梯度的长度反映了坡度程度的这种变化。因此，直观地说，你可以将梯度的方向视为指向上坡，其大小测量坡度有多陡。

> **二维梯度**是一个矢量，表示一个二维函数在某一点上的变化率和方向。对于二维函数$f(x, y)$，其梯度通常表示为$\nabla f(x, y)$或者$\langle \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y} \rangle$。
>
> 计算二维函数在某一点的梯度可以通过计算偏导数来实现。假设有一个二维函数$f(x, y)$，则在某一点$(a, b)$处的梯度$\nabla f(a, b)$计算如下：
> $$
> ∇f(a,b)= \langle\frac{∂f}{∂x}(a, b), \frac{∂f}{∂y}(a, b)\rangle
> $$
> 其中，$\frac{\partial f}{\partial x}$表示对$x$的偏导数，$\frac{\partial f}{\partial y}$表示对$y$的偏导数。这两个偏导数分别给出了函数在$(a, b)$点上沿$x$轴和$y$轴方向的变化率。
>
> 梯度的方向是变化最快的方向，而梯度的大小则表示变化率的大小。在二维空间中，梯度向量的大小可以通过以下公式计算：
> $$
> ∣∇f(a,b)∣=\sqrt{(\frac{∂f}{∂x}(a, b))^ 2 + (\frac{∂f}{∂y}(a, b))^ 2}
> $$
> 这个大小表示函数在$(a, b)$点上的变化率的大小。

> 偏导数是多元函数对其中一个变量的偏微分。在数学中，当一个函数依赖于多个变量时，我们可以计算它对其中一个变量的变化率，而保持其他变量不变。这就是偏导数的概念。
>
> 对于一个具有两个或更多变量的函数，如果我们想要了解函数在某个特定点上对其中一个变量的变化率，就会使用偏导数。偏导数通常用符号$∂$表示，后面跟着变量的名称。例如，对于一个具有两个变量$x$和$y$的函数f(x, y)，它的偏导数可以写成∂f/∂x表示对x的偏导数，或者$∂f/∂y$表示对y的偏导数。
>
> 数学上，偏导数的定义是通过极限来描述的。对于一个函数f(x, y)，在某一点(x₀, y₀)处对x的偏导数定义为：
> $$
> \frac{∂f}{∂x}(x_0, y_0) = \lim_{Δx→0} \frac{f(x_0 + Δx, y_0)−f(x_0, y_0)}{Δx}
> $$
> 
>
> 类似地，对y的偏导数定义为：
> $$
> \frac{∂f}{∂y}(x_0, y_0) = \lim_{Δy→0} \frac{f(x_0, y_0 + Δy)−f(x_0, y_0)}{Δy}
> $$
> 偏导数在微积分和数学建模中非常重要，用于分析多变量函数的性质和行为。



#### Implicit 2D Lines 隐式二维直线

> "Implicit 2D Lines" 指的是在平面上描述直线的隐式方程。直线的隐式方程通常以一种形式表示，其中不直接给出 $y$ 关于 $x$ 的显式表达式，而是通过一个等式来定义直线。
>
> 一般而言，一条直线可以表示为 $Ax + By + C = 0$，其中 $A$、$B$、$C$ 是常数，而 $(x, y)$ 是直线上的点。这是直线的标准形式，也是一个隐式方程。在这个方程中，直线上的每个点都满足这个等式，而不需要显式地解出 $y$。
>
> 对于 "Implicit 2D Lines"，我们可以通过这个方程来表达一条直线。考虑两个点 $(x_0, y_0)$ 和 $(x_1, y_1)$，我们可以使用这两点构建直线的隐式方程。首先，计算出直线的斜率 $m$：
> $$
> m = \frac{y_1-y_0}{x_1-x_0}
> $$
> 
>
> 然后，选择一个垂直于直线的向量 $(A, B)$。一个简单的选择是 $(A, B) = (y_0 - y_1, x_1 - x_0)$。有了这个向量，我们可以得到隐式方程：
> $$
> (y_0−y_1)x+(x_1−x_0)y+(x_0y_1−x_1y_0)=0
> $$
> 这就是通过两点构建的直线的隐式方程。对于这个方程中的每个点 $(x, y)$，等式都成立，因此它描述了整条直线。
>
> 这种表示方法的优势在于，即使直线是垂直或平行于坐标轴的，这个方程仍然有效。而且，这种形式更容易用于某些数学运算和几何推导。

The familiar “slope-intercept” form of the line is
熟悉的直线“斜截距”形式是
$$
y = mx + b \ \ \ \ (2.13)
$$
This can be converted easily to implicit form (Figure 2.28):
这可以很容易地转换为隐式形式（图 2.28）：
$$
y - mx - b = 0 \ \ \ \ \ (2.14)
$$
![Figure 2.28](.\Images\Figure 2.28.png)
Figure 2.28.A 2D line can be described by the equation $y - mx - b = 0$.
图 2.28.  二维线可以用方程 $y - mx - b = 0$ 来描述。

Here $m$ is the “slope" (ratio of rise to run) and $b$ is the $y$ value where the line crosses the y-axis, usually called the y-intercept. The line also partitions the 2D plane, but here “inside" and “outside" might be more intuitively called “over“ and ”under.“
这里 $m$ 是“斜率”（上升与运行的比率），$b$ 是直线与 y 轴相交处的 $y$ 值，通常称为 y 截距。该直线还划分了 2D 平面， 但这里的“内部”和“外部”可能更直观地称为“上方”和“下方”。

Because we can multiply an implicit equation by any constant without changing the points where it is zero, $kf(x,y) = 0$ is the same curve for any nonzero $k$. This allows several implicit forms for the same line, for example,
因为我们可以将隐式方程乘以任何常数而不改变它为零的点，所以对于任何非零 $k$，$kf(x,y) = 0$ 是相同的曲线。 这允许同一行有多种隐式形式，例如，
$2y - 2mx - 2b = 0$

One reason the slope-intercept form is sometimes awkward is that it can't represent some lines such as $x = 0$ because $m$ would have to be infinite. For this reason, a more general form is often useful for real numbers $A$, $B$, $C$:
斜率截距形式有时显得不太方便的一个原因是，它无法表示一些线，比如 $x = 0$，因为斜率 $m$ 将不得不是无穷大。因此，为了这个原因，对于实数 $A$、$B$、$C$，通常会使用更一般的形式：
$$
Ax + By + C = 0 \ \ \ \ \ (2.15)
$$
Suppose we know two points on the line, $(x_0, y_0)$ and $(x_1, y_1)$. What $A$, $B$ and $C$ describe the line through these two points? Because these points lie on the line, they must both satisfy Equation (2.15):
假设我们知道直线上的两个点，$(x_0, y_0)$ 和 $(x_1, y_1)$。 $A$、$B$ 和 $C$ 描述了穿过这两个点的线？ 因为这些点位于直线上，所以它们必须都满足方程（2.15）：
$Ax_0 + By_0 + C = 0 \\
Ax_1 + By_1 + C = 0$

Unfortunately we have two equations and three unknowns: $A$, $B$, and $C$. This problem arises because of the arbitrary multiplier we can have with an implicit equation. We could set $C = 1$ for convenience:
不幸的是，我们有两个方程和三个未知数：$A$、$B$ 和 $C$。 这个问题的出现是因为我们可以用隐式方程得到任意乘数。 为了方便起见，我们可以设置 $C = 1$：
$Ax + By + 1 = 0$

but we have a similar problem to the infinite slope case in slope-intercept form: lines through the origin would need to have $A(0) + B(0) + 1 = 0$, which is a contradiction. For example, the equation for a 45-degree line through the origin can be written $x - y = 0$, or equally well $y - x = 0$, or even $17y - 17x = 0$, but it cannot be written in the form $Ax + By + 1 = 0$.
但是我们有一个与斜截形式的无限斜率情况类似的问题：通过原点的线需要有 $A(0) + B(0) + 1 = 0$，这是一个矛盾。 例如，通过原点的 45 度线的方程可以写为 $x - y = 0$，或者同样可以写为 $y - x = 0$，甚至 $17y - 17x = 0$，但不能写为 写成 $Ax + By + 1 = 0$ 的形式。

Whenever we have such pesky algebraic problems, we try to solve the problems using geometric intuition as a guide. One tool we have, as discussed in Section 2.5.2, is the gradient. For the line $Ax + By + C = 0$, the gradient vector is $(A, B)$. This vector is perpendicular to the line (Figure 2.29), and points to the side of the line where $Ax + By + C$ is positive. Given two points on the line $(x_0, y_0)$ and $(x_1, y_1)$, we know that the vector between them points in the same direction as the line. This vector is just $(x_1 - x_0, y_1 - y_0)$, and because it is parallel to the line, it must also be perpendicular to the gradient vector $(A, B)$. Recall that there are an infinite number of $(A, B, C)$ that describe the line because of the arbitrary scaling property of implicits. We want any one of the valid $(A, B, C)$.
每当我们遇到此类烦人的代数问题时，我们都会尝试使用几何直觉作为指导来解决问题。 正如第 2.5.2 节中所讨论的，我们拥有的一种工具是梯度。 对于线 $Ax + By + C = 0$，梯度向量为 $(A, B)$。 该向量垂直于直线（图 2.29），并指向 $Ax + By + C$ 为正的直线一侧。 给定直线 $(x_0, y_0)$ 和 $(x_1, y_1)$ 上的两个点，我们知道它们之间的向量与直线指向相同的方向。 这个向量就是$(x_1 - x_0, y_1 - y_0)$，并且因为它平行于直线，所以它也必须垂直于梯度向量$(A, B)$。 回想一下，由于隐式的任意缩放属性，有无数个 $(A, B, C)$ 来描述这条线。 我们想要有效的 $(A, B, C)$ 中的任何一个。
![Figure 2.29](.\Images\Figure 2.29.png)
Figure 2.29.The gradient vector $(A, B)$ is perpendicular to the implicit line $Ax + By + C = 0$.
图 2.29. 梯度向量 $(A, B)$ 垂直于隐式直线 $Ax + By + C = 0$。

We can start with any $(A, B)$ perpendicular to $(x_1 - x_0, y_1 - y_0)$. Such a vector is just $(A, B) = (y_0 - y_1, x_1 - x_0)$ by the same reasoning as in Section 2.5.2. This means that the equation of the line through $(x_0, y_0)$ and $(x_1, y_1)$ is
我们可以从任意垂直于 $(x_1 - x_0, y_1 - y_0)$ 的向量 $(A, B)$ 开始。根据2.5.2节中相同的推理，这样的一个向量就是 $(A, B) = (y_0 - y_1, x_1 - x_0)$。这意味着通过 $(x_0, y_0)$ 和 $(x_1, y_1)$ 的直线方程是：
$$
(y_0 - y_1)x + (x_1 - x_0) + C = 0 \ \ \ \ \ (2.16)
$$
Now we just need to find $C$. Because $(x_0, y_0)$ and $(x_1, y_1)$ are on the line, they must satisfy Equation (2.16). We can plug either value in and solve for $C$. Doing this for $(x_0, y_0)$ yields $C = x_0y_1 - x_1y_0$, and thus the full equation for the line is
现在我们只需要找到$C$。 由于 $(x_0, y_0)$ 和 $(x_1, y_1)$ 在线上，因此它们必须满足方程（2.16）。 我们可以代入任一值并求解 $C$。 对 $(x_0, y_0)$ 执行此操作会产生 $C = x_0y_1 - x_1y_0$，因此该线的完整方程为
$$
(y_0 - y_1)x + (x_1 - x_0)y + x_0y_1 - x_1y_0 = 0 \ \ \ \ \ (2.17)
$$
Again, this is one of infinitely many valid implicit equations for the line through two points, but this form has no division operation and thus no numerically de-generate cases for points with finite Cartesian coordinates. A nice thing about Equation (2.17) is that we can always convert to the slope-intercept form (when it exists) by moving the non-$y$ terms to the right-hand side of the equation and dividing by the multiplier of the $y$ term:
同样，这是通过两点的直线的无限多个有效隐式方程之一，但这种形式没有除法运算，因此对于具有有限笛卡尔坐标的点不存在数值退化情况。 方程 (2.17) 的一个好处是，我们始终可以通过将非 $y$ 项移动到方程的右侧并除以 $y$ 术语：
$$
y = \frac{y_1 - y_0}{x_1 - x_0}x + \frac{x_1y_0 - x_0y_1}{x_1 - x_0}
$$
An interesting property of the implicit line equation is that it can be used to find the signed distance from a point to the line. The value of $Ax + By + C$ is proportional to the distance from the line (Figure 2.30). As shown in Figure 2.31.the distance from a point to the line is the length of the vector $k( A, B)$, which is
隐式直线方程的一个有趣的特性是它可以用来求从点到直线的有符号距离。 $Ax + By + C$ 的值与距直线的距离成正比（图 2.30）。 如图2.31所示，点到直线的距离就是向量$k(A,B)$的长度，即
$$
distance = k\sqrt{A^2 + B^2} \ \ \ \ \ \ (2.18)
$$
![Figure 2.30](Images\Figure 2.30.png)
Figure 2.30.The value of the implicit function $f(x,y) =Ax + By + C$ is a constant times the signed distance from $Ax + By + C= 0$
图 2.30.  隐式函数 $f(x,y) =Ax + By + C$ 的值是常数乘以距 $Ax + By + C= 0$ 的有符号距离

![Figure 2.31](.\Images\Figure 2.31.png)
Figure 2.31.The vector $k(A,B)$ connects a point $(x,y)$ on the line closest toa point not on the line. The distance is proportional to $k$.
图 2.31.向量 $k(A,B)$ 连接线上最接近非线上点的点 $(x,y)$。 距离与$k$成正比

For the point $(x,y) + k(A, B)$, the value of $f(x, y) = Ax + By + C$ is
对于点 $(x,y) + k(A, B)$，$f(x, y) = Ax + By + C$ 的值为
$$
f(x + kA, y + kB)= Ax + kA^2 + By + kB^2 + C = k(A^2 + B^2) \ \ \ \ (2.19)
$$
The simplification in that equation is a result of the fact that we know $(x, y)$ is on the line, so $Ax + By + C = 0$. From Equations (2.18) and (2.19), we can see that the signed distance from line $Ax + By + C = 0$ to a point $(a, b)$ is
该方程的简化是因为我们知道 $(x, y)$ 在线，因此 $Ax + By + C = 0$。 从方程（2.18）和（2.19）中我们可以看出，从线 $Ax + By + C = 0$ 到点 $(a, b)$ 的符号距离为
$distance = \frac{f(a,b)}{\sqrt{A^2 + B^2}}\\$

Here “signed distance" means that its magnitude (absolute value) is the geometric distance, but on one side of the line, distances are positive and on the other they are negative. You can choose between the equally valid representations $f(x,y) = 0$ and $-f(x,y) = 0$ if your problem has some reason to prefer a particular side being positive. Note that if $(A, B)$ is a unit vector, then $f(a,b)$ is the signed distance. We can multiply Equation (2.17) by a constant that ensures that $(A, B)$ is a unit vector:
这里的“有符号距离”意味着它的大小（绝对值）是几何距离，但在线的一侧，距离为正，另一侧为负。您可以在同等有效的表示形式 $f(x, y) = 0$ 和 $-f(x,y) = 0$ 如果您的问题有某种原因希望特定的一侧为正。请注意，如果 $(A, B)$ 是单位向量，则 $f( a,b)$ 是有符号距离。我们可以将方程 (2.17) 乘以一个常数，以确保 $(A, B)$ 是单位向量：
$$
f(x, y) = \frac{y_0 - y_1}{\sqrt{(x_1 - x_0)^2 + (y_0 - y_1)^2}}x \\
+ 
\frac{x_1- x_0}{\sqrt{(x_1 - x_0)^2 + (y_0 -y_1)^2}}y \\
+ \frac{x_0y_1 - x_1y_0}{\sqrt{(x_1 - x_0)^2 + (y_0 - y_1)^2}} = 0 \\
(2.20)
$$
Note that evaluating $f(x, y)$ in Equation (2.20) directly gives the signed distance, but it does require a square root to set up the equation. Implicit lines will turnout to be very useful for triangle rasterization (Section 8.1.2). Other forms for 2Dlines are discussed in Chapter 14.
请注意，在方程 (2.20) 中计算 $f(x, y)$ 直接给出有符号距离，但它确实需要平方根来建立方程。 隐式线对于三角形光栅化非常有用（第 8.1.2 节）。 二维线的其他形式将在第 14 章中讨论。

#### Implicit Quadric Curves 隐式二次曲线

In the previous section we saw that a linear function $f(x, y)$ gives rise to an implicit line $f(x,y) = 0$. If f is instead a quadratic function of $x$ and $y$, with the general form
在上一节中，我们看到线性函数 $f(x, y)$ 产生隐式直线 $f(x,y) = 0$。 如果 f 是 $x$ 和 $y$ 的二次函数，具有一般形式
$Ax^2 + Bxy + Cy^2 + Dx + Ey + F = 0$

the resulting implicit curve is called a quadric. Two-dimensional quadric curves include ellipses and hyperbolas, as well as the special cases of parabolas, circles, and lines.
由此产生的隐式曲线称为二次曲线。 二维二次曲线包括椭圆和双曲线，以及抛物线、圆和直线的特殊情况。

Examples of quadric curves include the circle with center $(x_c, y_c)$ and radius $r$,
二次曲线的示例包括以 $(x_c, y_c)$ 为圆心、以 $r$ 为半径的圆，
$(x - x_c)^2 + (y - y_c)^2 - r^2 = 0,$

and axis-aligned ellipses of the form
和轴对齐的椭圆形

$\frac{(x - x_c)^2}{a^2} + \frac{(y - y_c)^2}{b^2} - 1 = 0\\$

where $(x_c, y_c)$ is the center of the ellipse, and $a$ and $b$ are the minor and major semi-axes(Figure 2.32)
其中$(x_c, y_c)$是椭圆的中心，$a$和$b$是短半轴和长半轴（图2.32）
![Figure 2.32](.\Images\Figure 2.32.png)
Figure 2.32.The ellipse with center $(x_c, y_c)$ and semiaxes of length $a$ and $b$.
图 2.32. 中心为 $(x_c, y_c)$ 且半轴长度为 $a$ 和 $b$ 的椭圆。

> Try setting $a = b = r$ in the ellipse equation and compare to the circle equation.
> 尝试在椭圆方程中设置 $a = b = r$ 并与圆方程进行比较。

### 2.5.3 3D Implicit Surfaces 三维隐式表面

Just as implicit equations can be used to define curves in 2D, they can be used to define surfaces in 3D. As in 2D, implicit equations implicitly define a set of points that are on the surface:
正如隐式方程可用于定义 2D 曲线一样，它们也可用于定义 3D 曲面。 与 2D 中一样，隐式方程隐式定义表面上的一组点：
$f(x, y, z) = 0$

Any point $(x, y, z)$ that is on the surface results in zero when given as an argument to $f$. Any point not on the surface results in some number other than zero. You can check whether a point is on the surface by evaluating $f$, or you can check which side of the surface the point lies on by looking at the sign of $f$, but you cannot always explicitly construct points on the surface. Using vector notation,we will write such functions of $\bold{p} = (x,y,z)$ as
当作为 $f$ 的参数给出时，表面上的任何点 $(x, y, z)$ 都会导致零。 不在表面上的任何点都会产生非零的数字。 您可以通过评估 $f$ 来检查点是否在曲面上，也可以通过查看 $f$ 的符号来检查点位于曲面的哪一侧，但您不能总是在曲面上显式构造点。 使用向量表示法，我们将 $\bold{p} = (x,y,z)$ 的函数写为
$f(\bold{p}) = 0$

### 2.5.4 Surface Normal to an Implicit Surface 隐式表面的法向量

A surface normal (which is needed for lighting computations, among other things)is a vector perpendicular to the surface. Each point on the surface may have a different normal vector. In the same way that the gradient provides a normal to an implicit curve in 2D, the surface normal at a point $\bold{p}$ on an implicit surface is given by the gradient of the implicit function
表面法线（除其他外，照明计算所需）是垂直于表面的向量。 表面上的每个点可能具有不同的法向量。 与梯度提供 2D 隐式曲线法线的方式相同，隐式曲面上点 $\bold{p}$ 处的曲面法线由隐式函数的梯度给出
$\bold{n} = \nabla f(\bold{p}) = \left(\frac{\partial f(\bold{p})}{\partial x }, \frac{\partial f(\bold{p})}{\partial y }, \frac{\partial f(\bold{p})}{\partial z }\right)\\$

The reasoning is the same as for the 2D case: the gradient points in the direction of fastest increase in $f$, which is perpendicular to all directions tangent to the surface, in which $f$ remains constant. The gradient vector points toward the side of the surface where $f(\bold{p}) > 0$, which we may think of as “into" the surface or “out from” the surface in a given context. If the particular form of $f$ creates inward-facing gradients, and outward-facing gradients are desired, the surface $-f(\bold{p}) = 0$ is the same as surface $f(\bold{p}) = 0$ but has directionally reversed gradients, i.e., $-\nabla f(p) =  \nabla (-f(p))$.
这一推理与二维情形相同：梯度指向 $f$ 增加最快的方向，即垂直于与表面相切的所有方向，这些方向中 $f$ 保持恒定。梯度向量指向表面上 $f(\bold{p}) > 0$ 的一侧，我们可以在特定语境中将其理解为进入表面或者离开表面。如果 $f$ 的具体形式导致内向梯度，而我们期望得到外向梯度，那么表面 $-f(\bold{p}) = 0$ 与表面 $f(\bold{p}) = 0$ 梯度值相同，但其梯度方向相反，即 $-\nabla f(p) = \nabla (-f(p))$。

### 2.5.5 Implicit Planes 隐式平面

As an example, consider the infinite plane through point $\bold{a}$ with surface normal $\bold{n}$. The implicit equation to describe this plane is given by
例如，考虑通过点 $\bold{a}$ 且表面法线 $\bold{n}$ 的无限平面。 描述该平面的隐式方程由下式给出
$$
(\bold{p} - \bold{a})\cdot \bold{n} = 0 \ \ \ \ \ (2.21) 
$$
Note that $\bold{a}$ and $\bold{n}$ are known quantities. The point $\bold{p}$ is any unknown point that satisfies the equation. In geometric terms this equation says “the vector from $\bold{a}$ to $\bold{p}$ is perpendicular to the plane normal.” If $\bold{p}$ were not in the plane, then $(\bold{p} - \bold{a})$ would not make a right angle with $\bold{n}$ (Figure 2.33).
请注意，$\bold{a}$ 和$\bold{n}$ 是已知量。 点 $\bold{p}$ 是满足方程的任意未知点。 用几何术语来说，这个方程表示“从 $\bold{a}$ 到 $\bold{p}$ 的向量垂直于平面法线。” 如果 $\bold{p}$ 不在平面内，则 $(\bold{p} - \bold{a})$ 不会与 $\bold{n}$ 形成直角（图 2.33）。
![Figure 2.33](.\Images\Figure 2.33.png)
Figure 2.33. Any of the points $\bold{p}$ shown are in the plane with normal vector $\bold{n}$ that includes point $\bold{a}$ if Equation (2.2) is satisfied.
图 2.33 如果满足方程 (2.2)，则显示的任何点 $\bold{p}$ 都位于包含点 $\bold{a}$ 的法线向量 $\bold{n}$ 的平面中。

Sometimes we want the implicit equation for a plane through points $\bold{a}$, $\bold{b}$, and $\bold{c}$. The normal to this plane can be found by taking the cross product of any two vectors in the plane. One such cross product is
有时我们需要通过点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 的平面的隐式方程。 通过取平面中任意两个向量的叉积可以找到该平面的法线。 一种这样的叉积是
$\bold{n} = (\bold{b} - \bold{a})\cross (\bold{c} - \bold{a}).$

This allows us to write the implicit plane equation:
这允许我们写出隐式平面方程：
$$
(\bold{p} - \bold{a}) \cdot ((\bold{b} - \bold{a}) \cross (\bold{c} - \bold{a})) = 0 \ \ \  \ \ (2.22)
$$
A geometric way to read this equation is that the volume of the parallelepiped defined by $\bold{p} - \bold{a}$, $\bold{b} - \bold{a}$, and $\bold{c} - \bold{a}$ is zero, i.e., they are coplanar. This can only be true if $\bold{p}$ is in the same plane as $\bold{a}$, $\bold{b}$, and $\bold{c}$. The full-blown Cartesian representation for this is given by the determinant (this is discussed in more detail in Section 5.3):
从几何学的角度来解读这个方程，即由 $\bold{p} - \bold{a}$、$\bold{b} - \bold{a}$ 和 $\bold{c} - \bold{a}$ 定义的平行六面体的体积为零，也就是它们共面。这只有在 $\bold{p}$ 与 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 所在平面上时才成立。这在完整的笛卡尔表示中通过行列式给出（更详细地讨论在第5.3节）：
$$
\begin{vmatrix}
	x - x_a & y - y_a & z - z_a \\
	x_b - x_a & y_b - y_a & z_b - z_a \\
	x_c - x_a & y_c - y_a & z_c - z_a \\
\end{vmatrix} = 0  \ \ \ \ \ \ \ (2.23)
$$
The determinant can be expanded (see Section 5.3 for the mechanics of expanding determinants) to the bloated form with many terms.
行列式可以扩展到（有关扩展行列式的机制，请参阅第 5.3 节）到具有许多项的膨胀形式。

Equations (2.22) and (2.23) are equivalent, and comparing them is instructive. Equation (2.22) is easy to interpret geometrically and will yield efficient code. In addition, it is relatively easy to avoid a typographic error that compiles into incorrect code if it takes advantage of debugged cross and dot product code. Equation (2.23) is also easy to interpret geometrically and will be efficient pro-vided an efficient 3 x 3 determinant function is implemented. It is also easy to implement without a typo if a function $determinant(\bold{a}, \bold{b}, \bold{c})$ is available. It will be especially easy for others to read your code if you rename the determinant function volume. So both Equations (2.22) and (2.23) map well into code. The full expansion of either equation into $x-$, $y-$, and $z-$components is likely to generate typos. Such typos are likely to compile and, thus, to be especially pesky. This is an excellent example of clean math generating clean code and bloated math generating bloated code.
方程 (2.22) 和 (2.23) 是等价的，将它们进行比较是有益的。方程 (2.22) 在几何上易于解释，并且可以生成高效的代码。此外，它相对容易避免排版错误，如果利用已调试过的叉积和点积代码，就可以避免编译出错误的代码。方程 (2.23) 也在几何上易于解释，并且在实现了高效的 $3 \times 3$ 行列式函数的情况下将是高效的。如果有一个名为 $determinant(\bold{a}, \bold{b}, \bold{c})$ 的函数可用，实现它也是相对容易的，并且如果将这个函数重命名为 volume，那么对于他人阅读您的代码也会更加容易理解。因此，无论是方程 (2.22) 还是 (2.23) 都可以很好地映射到代码中。将任一方程完全展开为 $x$、$y$ 和 $z$ 分量可能会产生排版错误。这样的排版错误有可能编译通过，因此尤其让人头疼。这是一个干净的数学产生干净代码，而臃肿的数学产生臃肿代码的绝佳例子。

#### 3D Quadric Surfaces 3D 二次曲面

Just as quadratic polynomials in two variables define quadric curves in 2D, quadratic polynomials in $x$, $y$, and $z$ define quadric surfaces in 3D. For instance, a sphere can be written as
正如两个变量中的二次多项式定义 2D 中的二次曲线一样，$x$、$y$ 和 $z$ 中的二次多项式定义 3D 中的二次曲面。 例如，球体可以写为
$f(\bold{p}) = (\bold{p} - \bold{c})^2 - r^2 = 0$

and an axis-aligned ellipsoid may be written as
轴对齐的椭球体可以写为
$f(\bold{p}) = \frac{(x - x_c)^2}{a^2} + \frac{(y - y_c)^2}{b^2} + \frac{(z - z_c)^2}{c^2} - 1 = 0\\$

#### 3D Curves from Implicit Surfaces 隐式曲面的 3D 曲线

One might hope that an implicit 3D curve could be created with the form $f(\bold{p}) = 0$. However, all such curves are just degenerate surfaces and are rarely useful in practice. A 3D curve can be constructed from the intersection of two simultaneous implicit equations:
人们可能希望可以使用 $f(\bold{p}) = 0$ 的形式创建一条隐式 3D 曲线。 然而，所有这些曲线都只是简并曲面，在实践中很少有用。 3D 曲线可以通过两个联立隐式方程的交集构建：
$f(\bold{p}) = 0\\
g(\bold{p}) = 0$

For example, a 3D line can be formed from the intersection of two implicit planes. Typically, it is more convenient to use parametric curves instead; they are dis-cussed in the following sections.
例如，3D 线可以由两个隐式平面的交集形成。 通常，使用参数曲线更方便； 以下各节将讨论它们。

### 2.5.6 2D Parametric Curves 2D 参数曲线

A parametric curve is controlled by a single parameter that can be considered a sort of index that moves continuously along the curve. Such curves have the form
参数曲线由单个参数控制，该参数可以被视为一种沿着曲线连续移动的索引。 这样的曲线具有以下形式
$\begin{bmatrix}x \\ y \end{bmatrix} = \begin{bmatrix}g(t) \\ h(t) \end{bmatrix}$

Here $(x, y)$ is a point on the curve, and t is the parameter that influences the curve. For a given $t$, there will be some point determined by the functions $g$ and $h$. For continuous $g$ and $h$, a small change in $t$ will yield a small change in $x$ and $y$. Thus, as $t$ continuously changes, points are swept out in a continuous curve. This is a nice feature because we can use the parameter $t$ to explicitly construct points on the curve. Often we can write a parametric curve in vector form,
这里$(x,y)$是曲线上的点，t是影响曲线的参数。对于给定的$t$，存在由函数$g$和$h$确定的某个点。对于连续的 $g$ 和 $h$，$t$ 的微小变化将导致 $x$ 和 $y$ 的微小变化。 因此，随着 $t$ 不断变化，点会以连续曲线的形式被扫出。这是一个很好的功能，因为我们可以使用参数 $t$ 显式地构造曲线上的点。通常我们可以写出矢量形式的参数曲线，
$\bold{p} = f(t)$

where $f$ is a vector-valued function， $f :\R \mapsto \R^2$ .Such vector functions can generate very clean code, so they should be used when possible.
其中 $f$ 是向量值函数， $f :\R \mapsto \R^2$ 。此类向量函数可以生成非常干净的代码，因此应尽可能使用它们。

We can think of the curve with a position as a function of time. The curve can go anywhere and could loop and cross itself. We can also think of the curve as having a velocity at any point. For example, the point $\bold{p}(t)$ is traveling slowly near $t = -2$ and quickly between $t = 2$ and $t = 3$. This type of “moving point“ vocabulary is often used when discussing parametric curves even when the curve is not describing a moving point.
我们可以将具有时间位置函数的曲线看作是随时间变化的。这条曲线可以在任何地方运动，甚至可以环绕并交叠自身。我们还可以将曲线在任意点变化看作是有速度的。例如，在 $t = -2$ 附近，点 $\bold{p}(t)$ 移动缓慢，而在 $t = 2$ 到 $t = 3$ 之间移动迅速。这种“移动点”词汇经常在讨论参数曲线时使用，即使曲线并不描述一个实际移动的点。

#### 2D Parametric Lines 2D 参数线

A parametric line in 2D that passes through points $\bold{p}_0 = (x_0, y_0)$ and $\bold{p}_1 =(x_1, y_1)$ can be written as
穿过点 $\bold{p}_0 = (x_0, y_0)$ 和 $\bold{p}_1 =(x_1, y_1)$ 的二维参数线可以写为

$\begin{bmatrix}x \\y \\\end{bmatrix} = \begin{bmatrix}x_0 + t(x_1 - x_0) \\y_0 + t(y_1 - y_0) \\\end{bmatrix}$

Because the formulas for $x$ and $y$ have such similar structure, we can use the vector form for $\bold{p} = (x, y)$ (Figure 2.34): 
由于 $x$ 和 $y$ 的公式具有相似的结构，因此我们可以使用向量形式 $\bold{p} = (x, y)$（图 2.34）：
$\bold{p}(t) = \bold{p}_0 + t(\bold{p}_1 - \bold{p}_0)$
<img src=".\Images\Figure 2.34.png" alt="Figure 2.34" style="zoom:80%;" />
Figure 2.34. A 2D para-metric line through $\bold{p}_0$ and $\bold{p}_1$. The line segment defined by $t \in [0,1]$ is shown in bold.
图 2.34 通过 $\bold{p}_0$ 和 $\bold{p}_1$ 的 2D 参数线。 $t \in [0,1]$ 定义的线段以粗体显示。

You can read this in geometric form as: “start at point $\bold{p}_0$ and go some distance toward $\bold{p}_1$ determined by the parameter $t$." A nice feature of this form is that $\bold{p}(0) = \bold{p}_0$ and $\bold{p}(1) = \bold{p}_1$. Since the point changes linearly with $t$, the value oft between $\bold{p}_0$ and $\bold{p}_1$; measures the fractional distance between the points. Points with $t < 0$ are to the “far" side of $\bold{p}_0$, and points with $t > 1$ are to the “far" side of $\bold{p}_1$.
您可以将其以几何形式解读为：“从点 $\bold{p}_0$ 开始，向由参数 $t$ 确定的 $\bold{p}_1$ 走一段距离。”这种形式的一个很好的功能是 $\bold{p}(0) = \bold{p}_0$ 和 $\bold{p}(1) = \bold{p}_1$. 由于该点随 $t$ 线性变化，因此 t 的值 $\bold{p}_0$ 和 $\bold{p}_1$ 之间；测量点之间的分数距离。$t < 0$ 的点位于 $\bold{p}_0$ 的“远”侧 ，$t > 1$ 的点位于 $\bold{p}_1$ 的“远”侧。

Parametric lines can also be described as just a point $\bold{o}$ and a vector $\bold{d}$:
参数线也可以被描述为一个点 $\bold{o}$ 和一个向量 $\bold{d}$：
$\bold{p}(t) = \bold{o} + t(\bold{d})$

When the vector $\bold{d}$ has unit length, the line is arc-length parameterized. This means $t$ is an exact measure of distance along the line. Any parametric curve can be arc-length parameterized, which is obviously a very convenient form, but no tall can be converted analytically.
当向量 $\bold{d}$ 具有单位长度时，该线是弧长参数化的。 这意味着 $t$ 是沿线距离的精确测量。 任何参数曲线都可以进行弧长参数化，这显然是一种非常方便的形式，但没有高的可以解析转换。

#### 2D Parametric Circles 2D 参数圆

A circle with center $(x_c, y_c)$ and radius $r$ has a parametric form:
以 $(x_c, y_c)$ 为圆心、以 $r$ 为半径的圆具有参数形式：
$\begin{bmatrix}x \\y \\\end{bmatrix} = \begin{bmatrix}x_c + r\cos \varphi \\ y_c + r\sin \varphi\\\end{bmatrix}$

To ensure that there is a unique parameter $\varphi$ for every point on the curve, we can restrict its domain: $\varphi \in [0, 2\pi)$ or  $\varphi \in (-\pi, \pi]$ or any other half-open interval of length $2\pi$.
为了确保曲线上的每个点都有唯一的参数 $\varphi$，我们可以限制其域： $\varphi \in [0, 2\pi)$ 或 $\varphi \in (-\pi, \pi]$ 或任何其他长度为 $2\pi$ 的半开区间。

An axis-aligned ellipse can be constructed by scaling the $x$ and $y$ parametric equations separately:
轴对齐的椭圆可以通过分别缩放 $x$ 和 $y$ 参数方程来构造：
$\begin{bmatrix}x \\y \\\end{bmatrix} = \begin{bmatrix}x_c + a\cos \varphi \\ y_c + b\sin \varphi\\\end{bmatrix}$

### 2.5.7 3D Parametric Curves 3D 参数曲线

A 3D parametric curve operates much like a 2D parametric curve:
3D 参数曲线的运行方式与 2D 参数曲线非常相似：
$x = f(t) \\
y = g(t) \\
z = h(t) \\$

For example, a spiral around the z-axis is written as:
例如，绕 z 轴的螺旋线可写为：
$ x = \cos t \\
y = \sin t \\
z =  t \\$

As with 2D curves, the functions $f$, $g$, and $h$ are defined on a domain $D \subset \R$ if we want to control where the curve starts and ends. In vector form we can write
与 2D 曲线一样，如果我们想要控制曲线的起点和终点，则函数 $f$、$g$ 和 $h$ 是在域 $D \subset \R$ 上定义的。 我们可以用向量形式写出
$\begin{bmatrix}x \\y\\z\\\end{bmatrix} = \bold{p}(t)$

In this chapter we only discuss 3D parametric lines in detail. General 3D parametric curves are discussed more extensively in Chapter 15.
在本章中，我们仅详细讨论 3D 参数线。 第 15 章更广泛地讨论了一般 3D 参数曲线。

> The parametric curve is the range of $\bold{p}: \R \rightarrow \R^3$
> 参数曲线的范围是$\bold{p}：\R \rightarrow \R^3$

#### 3D Parametric Lines 3D 参数线 

A 3D parametric line can be written as a straightforward extension of the 2D parametric line,e.g.,
3D 参数线可以写为 2D 参数线的直接延伸，例如，
$x = 2+7t,\\
y = 1 + 2t\\
z = 3 - 5t.$

This is cumbersome and does not translate well to code variables, so we will write it in vector form:
这很麻烦，并且不能很好地转换为代码变量，因此我们将其写为向量形式：
$\bold{p} = \bold{o} + t\bold{d}$

where, for this example, $\bold{o}$ and $\bold{d}$ are given by
其中，对于本例，$\bold{o}$ 和 $\bold{d}$ 由下式给出
$\bold{o} = (2, 1, 3) \\
\bold{d} = (7, 2, -5)$

Note that this is very similar to the 2D case. The way to visualize this is to imagine that the line passes through $\bold{o}$ and is parallel to $\bold{d}$. Given any value of $t$, you get some point $\bold{p}(t)$ on the line. For example, at $t = 2$, $p(t) = (2, 1, 3) +2(7, 2, -5) = (16, 5, -7)$. This general concept is the same as for two dimensions(Figure 2.30).
请注意，这与 2D 情况非常相似。 形象化的方法是想象这条线穿过 $\bold{o}$ 并与 $\bold{d}$ 平行。 给定 $t$ 的任何值，您都会得到线上的某个点 $\bold{p}(t)$ 。 例如，当 $t = 2$ 时，$p(t) = (2, 1, 3) +2(7, 2, -5) = (16, 5, -7)$。 这个一般概念与二维相同（图 2.30）。

As in 2D, a line segment can be described by a 3D parametric line and an interval $t \in [t_a, t_b]$. The line segment between two points $\bold{a}$ and $\bold{b}$ is given by $\bold{p}(t) = \bold{a} + t(\bold{b} - \bold{a})$ with $t \in [0, 1]$. Here $\bold{p}(0) = \bold{a}$, $\bold{p}(1) = \bold{b}$, and $\bold{p}(0.5) = (\bold{a} + \bold{b})/2$, the midpoint between $\bold{a}$ and $\bold{b}$.
与 2D 中一样，线段可以通过 3D 参数线和区间 $t \in [t_a, t_b]$ 来描述。 两点 $\bold{a}$ 和 $\bold{b}$ 之间的线段由下式给出： $\bold{p}(t) = \bold{a} + t(\bold{b} - \bold {a})$ 与 $t \in [0, 1]$。 这里$\bold{p}(0) = \bold{a}$，$\bold{p}(1) = \bold{b}$，$\bold{p}(0.5) = (\bold{ a} + \bold{b})/2$，$\bold{a}$ 和 $\bold{b}$ 之间的中点。

A ray, or half-line, is a 3D parametric line with a half-open interval, usually $[0, \infty)$. From now on we will refer to all lines, line segments, and rays as “rays.” This is sloppy, but corresponds to common usage and makes the discussion simpler.
射线或半线是具有半开区间的 3D 参数线，通常为 $[0, \infty)$。 从现在开始，我们将所有直线、线段和射线称为“射线”。 这很草率，但符合常见用法并使讨论更简单。

### 2.5.8 3D Parametric Surfaces 3D 参数化曲面 

The parametric approach can be used to define surfaces in 3D space in much the same way we define curves, except that there are two parameters to address the two-dimensional area of the surface. These surfaces have the form
参数化方法可用于定义 3D 空间中的曲面，其方式与定义曲线的方式大致相同，只是有两个参数来处理曲面的二维区域。 这些表面具有以下形式
$x = f(u, v) \\
y = g(u, v) \\
z = h(u, v)$

or, in vector form,
或者，以向量形式，
$\begin{bmatrix}x \\y \\z \\\end{bmatrix} = \bold{p}(u, v)$

> The parametric surface isthe range of the function $\bold{p}: \R^2 \rightarrow \R^3$
> 参数曲面是函数$\bold{p}的范围：\R^2\rightarrow\R^3$

**Example**. For example, a point on the surface of the Earth can be described by the two parameters longitude and latitude. If we define the origin to be at the center of the Earth, and let r be the radius of the Earth, then a spherical coordinate system centered at the origin (Figure 2.35), lets us derive the parametric equations
**例子**。 例如，地球表面的一个点可以用经度和纬度两个参数来描述。 如果我们将原点定义为地球中心，并令 r 为地球半径，则在以原点为中心的球坐标系（图 2.35）中，我们可以推导出参数方程
$$
x = r \cos\varphi \sin \theta \\
y = r \sin\varphi \sin \theta  \ \ \ \ \ (2.24)\\
z = r \cos \theta \\
$$
![Figure 2.35](.\Images\Figure 2.35.png)
Figure 2.35. The geometry for spherical coordinates.
图 2.35 球坐标的几何

> Pretend for the sake of argument that the Earth is exactly spherical.
> 为了论证的目的，假装地球是正球形的。

> The θ and φ here may or may not seem reversed depending on your background; the use of these symbols varies across disciplines. In this book we will always assume the meaning of θ and φ used in Equation (2.24) and depicted in Figure 2.35 
> 这里的 θ 和 φ 可能看起来颠倒，也可能不颠倒，具体取决于您的背景； 这些符号的使用因学科而异。 在本书中，我们将始终假设方程 (2.24) 中使用的 θ 和 φ 的含义，如图 2.35 所示

Ideally, we'd like to write this in vector form, but it isn't feasible for this particular parametric form.
理想情况下，我们希望以向量形式编写它，但对于这种特定的参数形式来说这是不可行的。

We would also like to be able to find the $(\theta, \varphi)$ for a given $(x, y, z)$. If we assume that $\varphi \in (-\pi, \pi])$,  this is easy to do using the $atan2$ function from Equation 2.2):
我们还希望能够找到给定 $(x, y, z)$ 的 $(\theta, \varphi)$。 如果我们假设 $\varphi \in (-\pi, \pi])$，则可以使用公式 2.2 中的 $atan2$ 函数轻松实现：
$$
θ = acos(z/\sqrt{x^2 + y^2 + z^2}),  \\
φ = atan2(y, x). \ \ \  \ \ \ \ (2.25)
$$
With implicit surfaces, the derivative of the function $f$ gave us the surface normal. With parametric surfaces, the derivatives of $\bold{p}$ also give information about the surface geometry.
对于隐式曲面，函数 $f$ 的导数为我们提供了曲面法线。 对于参数化曲面，$\bold{p}$ 的导数还提供有关曲面几何形状的信息。

Consider the function $\bold{q}(t) = \bold{p}(t, v_0)$. This function defines a parametric curve obtained by varying $u$ while holding $v$ fixed at the value $v_0$. This curve, called an isoparametric curve (or sometimes “isoparm” for short) lies in the sur-face. The derivative of $\bold{q}$ gives a vector tangent to the curve, and since the curve lies in the surface the vector $\bold{q}'$ also lies in the surface. Since it was obtained by varying one argument of $\bold{p}$, the vector $\bold{q}'$ is the partial derivative of $\bold{p}$ with respect to $u$, which we'll denote $\bold{p}_u$. A similar argument shows that the partial derivative $\bold{p}_v$ gives the tangent to the isoparametric curves for constant $u$, which is a second tangent vector to the surface.
考虑函数 $\bold{q}(t) = \bold{p}(t, v_0)$。 该函数定义了一条参数曲线，该曲线通过改变 $u$ 同时将 $v$ 固定在值 $v_0$ 来获得。 这条曲线称为等参曲线（有时简称为“等参曲线”），位于表面。 $\bold{q}$ 的导数给出与曲线相切的向量，并且由于曲线位于曲面中，因此向量 $\bold{q}'$ 也位于曲面中。 由于它是通过改变 $\bold{p}$ 的一个参数获得的，因此向量 $\bold{q}'$ 是 $\bold{p}$ 相对于 $u$ 的偏导数，我们将其 表示$\bold{p}_u$。 类似的论点表明，偏导数 $\bold{p}_v$ 给出了常数 $u$ 的等参曲线的切线，它是曲面的第二个切向量。

The derivative of $\bold{p}$, then, gives two tangent vectors at any point on the sur-face. The normal to the surface may be found by taking the cross product of these vectors: since both are tangent to the surface, their cross product, which is perpendicular to both tangents, is normal to the surface. The right-hand rule for cross products provides a way to decide which side is the front, or outside, of the surface; we will use the convention that the vector points toward the outside of the surface.
因此，$\bold{p}$ 的导数在曲面上的任意点处给出两个切向量。曲面的法向量可以通过对这些向量进行叉积来找到：因为两者都切于曲面，它们的叉积即垂直于这两个切向量的法向量也就垂直于曲面。对于叉积的右手规则提供了一种决定哪一侧是曲面的前面或外侧的方法；我们将使用向量指向曲面外侧的约定。

$\bold{n} = \bold{p}_u \cross \bold{p}_v$

### 2.5.9 Summary of Curves and Surfaces 曲线和曲面总结

Implicit curves in 2D or surfaces in 3D are defined by scalar-valued functions of two or three variables, $f : \R^2 \rightarrow \R$ or $f : \R^3 \rightarrow \R$, and the surface consists of all points where the function is zero:
在二维中的隐式曲线，或在三维中的隐式曲面，由关于两个或三个变量的标量值函数定义，即 $f : \R^2 \rightarrow \R$ 或 $f : \R^3 \rightarrow \R$。曲面包含所有使得函数值为零的点：
$S = \{\bold{p} | f(\bold{p}) = 0\}$

Parametric curves in 2D or 3D are defined by vector-valued functions of one variable, $\bold{p} : D  \subset \R \rightarrow \R^2$ or $\bold{p} : D \subset \R \rightarrow \R^3$, and the curve is swept out as $t$ varies over all of $D$:
在二维或三维中，参数曲线由关于一个变量的向量值函数定义，即 $\bold{p} : D \subset \R \rightarrow \R^2$ 或 $\bold{p} : D \subset \R \rightarrow \R^3$，而曲线是当 $t$ 在 $D$ 的所有取值范围内变化时所绘制的：
$S = \{\bold{p}(t)| t\in D\}.$

Parametric surfaces in 3D are defined by vector-valued functions of two variables, $\bold{p} : D \subset \R^2 \rightarrow \R^3$, and the surface consists of the images of all points $(u, v)$ in the domain:
在三维中，参数曲面由关于两个变量的向量值函数定义，即 $\bold{p} : D \subset \R^2 \rightarrow \R^3$，而曲面包括域内所有点 $(u, v)$ 的图像：
$S = \{\bold{p}(t)| (u,v) \in D\}.$

For implicit curves and surfaces, the normal vector is given by the derivative of $f$ (the gradient), and the tangent vector (for a curve) or vectors (for a surface) can be derived from the normal by constructing a basis.
 对于隐式曲线和曲面，法向量由 $f$ 的导数（梯度）给出，而切向量（对于曲线）或切向量组（对于曲面）可以通过构建一个基于法向量的基来导出。 

For parametric curves and surfaces, the derivative of $\bold{p}$ gives the tangent vector(for a curve) or vectors (for a surface), and the normal vector can be derived from the tangents by constructing a basis.
对于参数曲线和曲面，$\bold{p}$ 的导数给出了切向量（对于曲线）或切向量组（对于曲面），而法向量可以通过构建一个基于切向量的基来导出。

## 2.6 Linear Interpolation 线性插值

Perhaps the most common mathematical operation in graphics is linear interpolation. We have already seen an example of linear interpolation of position to form line segments in 2D and 3D, where two points $\bold{a}$ and $\bold{b}$ are associated with a parameter $t$ to form the line $\bold{p} = (1 - t)\bold{a} + t\bold{b}$. This is interpolation because $\bold{p}$ goes through $\bold{a}$ and $\bold{b}$ exactly at $t = 0$ and $t = 1$. It is linear interpolation because the weighting terms $t$ and $1 - t$ are linear polynomials of $t$.
在图形学中，或许最常见的数学运算就是线性插值。我们已经看到了在二维和三维中通过位置的线性插值形成线段的例子，其中两个点 $\bold{a}$ 和 $\bold{b}$ 与参数 $t$ 相关联，形成直线 $\bold{p} = (1 - t)\bold{a} + t\bold{b}$。这是插值，因为在 $t = 0$ 和 $t = 1$ 时，$\bold{p}$ 正好经过 $\bold{a}$ 和 $\bold{b}$。它是线性插值，因为权重项 $t$ 和 $1 - t$ 是 $t$ 的线性多项式。

Another common linear interpolation is among a set of positions on the x-axis: $x_0, x_1, ..., x_n$, and for each $x_i$ we have an associated height, $y_i$. We want to create a continuous function $y = f(x)$ that interpolates these positions, so that $f$ goes through every data point, i.e., $f(x_i) = y_i$. For linear interpolation, the points$(x_i, y_i)$ are connected by straight line segments. It is natural to use parametric line equations for these segments. The parameter $t$ is just the fractional distance between $x_i$ and $x_{i+1}$:
另一种常见的线性插值是在x轴上一组位置之间进行的：$x_0, x_1, ..., x_n$，对于每个$x_i$，我们有一个关联的高度$y_i$。我们想要创建一个连续的函数$y = f(x)$，使其插值这些位置，以便$f$通过每个数据点，即$f(x_i) = y_i$。对于线性插值，点$(x_i, y_i)$由直线段连接。使用这些线段的参数方程是很自然的。参数$t$正好是$x_i$和$x_{i+1}$之间的分数距离：
$$
f(x) = y_i + \frac{x - x_i}{x_{i+1} - x_i}(y_{i + 1} - y_i) \ \ \ \ \ \ (2.26)
$$
Because the weighting functions are linear polynomials of $x$, this is linear interpolation.
因为加权函数是 $x$ 的线性多项式，所以这是线性插值。

The two examples above have the common form of linear interpolation. We create a variable $t$ that varies from 0 to 1 as we move from data item $A$ to data item $B$. Intermediate values are just the function $(1 - t)A + tB$. Notice that Equation (2.26) has this form with
上面的两个例子具有线性插值的常见形式。 我们创建一个变量 $t$，当我们从数据项 $A$ 移动到数据项 $B$ 时，该变量从 0 变化到 1。 中间值就是函数 $(1 - t)A + tB$。 请注意，方程 (2.26) 具有以下形式：
$t = \frac{x - x_i}{x_{x + i} - x_i} \\$



## 2.7 Triangles 三角形

Triangles in both 2D and 3D are the fundamental modeling primitive in many graphics programs. Often information such as color is tagged onto triangle vertices, and this information is interpolated across the triangle. The coordinate system that makes such interpolation straightforward is called barycentric coordinates; we will develop these from scratch. We will also discuss 2D triangles, which must be understood before we can draw their pictures on 2D screens.
2D 和 3D 三角形是许多图形程序中的基本建模基元。 通常，诸如颜色之类的信息被标记到三角形顶点上，并且该信息在三角形上进行插值。 使这种插值变得简单的坐标系称为重心坐标； 我们将从头开始开发这些。 我们还将讨论 2D 三角形，在我们可以在 2D 屏幕上绘制它们的图片之前必须先了解这些三角形。

### 2.7.1 2D Triangles 2D 三角形

If we have a 2D triangle defined by 2D points $\bold{a}$, $\bold{b}$ and $\bold{c}$. we can first find its area:
如果我们有一个由二维点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 定义的二维三角形，我们首先可以找到它的面积：
$$
area = \frac{1}{2}
\begin{vmatrix}x_b - x_a & x_c - x_a \\ y_b - y_a& y_c - y_a\\\end{vmatrix}
 = \frac{1}{2}(x_ay_b + x_by_c + x_cy_a - x_ay_c - x_by_a - x_cy_b) \ \ \ (2.27)
$$
The derivation of this formula can be found in Section 5.3. This area will have a positive sign if the points $\bold{a}$, $\bold{b}$, and $\bold{c}$ are in counterclockwise order and a negative sign,otherwise.
这个公式的推导可以在5.3节中找到。 如果点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 按逆时针顺序，则该区域的符号为正，否则符号为负。

Often in graphics, we wish to assign a property, such as color, at each triangle vertex and smoothly interpolate the value of that property across the triangle. There are a variety of ways to do this, but the simplest is to use barycentric coordinates. One way to think of barycentric coordinates is as a nonorthogonal coordinate system as was discussed briefly in Section 2.4.2. Such a coordinate system is shown in Figure 2.36, where the coordinate origin is a and the vectors from $\bold{a}$, $\bold{b}$, and $\bold{c}$ are the basis vectors. With that origin and those basis vectors, any point $\bold{p}$ can be written as
通常在图形中，我们希望在每个三角形顶点分配一个属性，例如颜色，并在整个三角形上平滑地插入该属性的值。 有多种方法可以做到这一点，但最简单的是使用**重心坐标**。 考虑重心坐标的一种方法是将其视为非正交坐标系，如第 2.4.2 节中简要讨论的那样。 这样的坐标系如图2.36所示，其中坐标原点为a，来自$\bold{a}$、$\bold{b}$和$\bold{c}$的向量是基向量。 有了原点和基向量，任何点 $\bold{p}$ 都可以写成
$$
\bold{p} = \bold{a} + β(\bold{b} − \bold{a}) + γ(\bold{c} − \bold{a})\ \ \ \ \ (2.28)
$$
<img src=".\Images\Figure 2.36.png" alt="Figure 2.36" style="zoom:80%;" />

Figure 2.36.  A 2D triangle with vertices $\bold{a}$, $\bold{b}$, $\bold{c}$  can be used to set up a nonorthogonal coordinate system with origin $\bold{a}$ and basis vectors $(\bold{b} – \bold{a})$ and $(\bold{c} – \bold{a})$. A point is then represented by an ordered pair $(β, γ)$. For example, the point $\bold{p} = (2.0, 0.5)$, i.e., $\bold{p} = \bold{a} + 2.0 (\bold{b} – \bold{a}) + 0.5(\bold{c} – \bold{a})$. 
图 2.36  具有顶点 $\bold{a}$、$\bold{b}$、$\bold{c}$ 的二维三角形可用于建立具有原点 $\bold{a}$ 和基向量的非正交坐标系 $(\bold{b} – \bold{a})$ 和 $(\bold{c} – \bold{a})$。 然后，一个点由有序对 $(β, γ)$ 表示。 例如，点 $\bold{p} = (2.0, 0.5)$，即 $\bold{p} = \bold{a} + 2.0 (\bold{b} – \bold{a}) + 0.5 (\bold{c} – \bold{a})$。

Note that we can reorder the terms in Equation (2.28) to get 
请注意，我们可以对方程（2.28）中的项进行重新排序，得到
$\bold{p} = (1 - β - γ)\bold{a} + β\bold{b} + γ\bold{c}  $

Often people define a new variable α to improve the symmetry of the equations: 
人们常常定义一个新变量 α 来提高方程的对称性：
$α ≡ 1 - β - γ  $

which yields the equation
得出方程
$$
\bold{p}(α, β, γ) = α\bold{a} + β\bold{b} + γ\bold{c} \ \ \  \ \ (2.29)
$$
with the constraint that
的约束条件是
$$
α + β + γ = 1 \ \ \ \ (2.30)
$$
Barycentric coordinates seem like an abstract and unintuitive construct at first, but they turn out to be powerful and convenient. You may find it useful to think of how street addresses would work in a city where there are two sets of parallel streets, but where those sets are not at right angles. The natural system would essentially be barycentric coordinates, and you would quickly get used to them. Barycentric coordinates are defined for all points on the plane. A particularly nice feature of barycentric coordinates is that a point $\bold{p}$ is inside the triangle formed by $\bold{a}$, $\bold{b}$, and $\bold{c}$ if and only if 
重心坐标乍看起来是一种抽象而不直观的构造，但事实证明它们是强大且方便的。你可以设想一下，在一个城市中，有两组平行的街道，但这两组街道并不呈直角。自然的系统本质上就是重心坐标，而你会很快适应它们。重心坐标适用于平面上的所有点。重心坐标的一个特别好的特性是，点 $\bold{p}$ 在由 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 形成的三角形内当且仅当
$0 < α < 1, \\
0 < β < 1,\\
0 < γ < 1  $

If one of the coordinates is zero and the other two are between zero and one, then you are on an edge. If two of the coordinates are zero, then the other is one, and you are at a vertex. Another nice property of barycentric coordinates is that Equation (2.29) in effect mixes the coordinates of the three vertices in a smooth way. The same mixing coefficients $(α, β, γ)$ can be used to mix other properties, such as color, as we will see in the next chapter.
如果其中一个坐标为零，而另外两个坐标介于零和一之间，那么你就在一条边上。如果两个坐标为零，那么另一个坐标为一，你就在一个顶点上。重心坐标的另一个良好性质是，方程（2.29）实际上以一种平滑的方式混合了三个顶点的坐标。相同的混合系数 $(α, β, γ)$ 可以用于混合其他属性，比如颜色，我们将在下一章中看到。

Given a point p, how do we compute its barycentric coordinates? One way is to write Equation (2.28) as a linear system with unknowns $β$ and $γ$, solve, and set $α = 1 - β - γ$. That linear system is 
给定一个点 p，我们如何计算它的重心坐标？ 一种方法是将方程 (2.28) 写为具有未知数 $β$ 和 $γ$ 的线性系统，求解并设置 $α = 1 - β - γ$。 该线性系统是
$$
\begin{bmatrix}x_b - x_a & x_c - x_a \\y_b - y_a & y_c - y_a \\\end{bmatrix} \begin{bmatrix}\beta \\ \gamma \end{bmatrix}
= \begin{bmatrix}x_p - x_a \\ y_p - y_a \end{bmatrix} \ \ \ \ \ (2.31)
$$
Although it is straightforward to solve Equation (2.31) algebraically, it is often fruitful to compute a direct geometric solution.
虽然用代数方法求解方程（2.31）很简单，但计算直接的几何解通常是富有成效的。

One geometric property of barycentric coordinates is that they are the signed scaled distance from the lines through the triangle sides, as is shown for $\beta$ in Figure 2.37. Recall from Section 2.5.2 that evaluating the equation $f(x, y)$ for the line $f(x,y) = 0$ returns the scaled signed distance from $(x,y)$ to the line. Also recall that if $f(x,y) = 0$ is the equation for a particular line, so is $kf(x, y) = 0$ for any nonzero $k$. Changing $k$ scales the distance and controls which side of the line has positive signed distance, and which negative. We would like to choose $k$ such that, for example, $kf(x,y) = \beta$. Since $k$ is only one unknown, we can force this with one constraint, namely that at point $\bold{b}$ we know $\beta = 1$. So if the line $f_{ac}(x, y) = 0$ goes through both $\bold{a}$ and $\bold{c}$, then we can compute $\beta$ for a point $(x, y)$ as follows:
重心坐标的一个几何特性是，它们**是通过三角形边缘的直线的带符号的缩放距离**，正如在图2.37中展示的 $\beta$ 那样。回顾一下第2.5.2节，对于线 $f(x, y) = 0$，计算方程 $f(x, y)$ 的值返回从 $(x, y)$ 到该线的带符号的缩放距离。还要记得，如果 $f(x, y) = 0$ 是特定直线的方程，那么对于任何非零的 $k$，$kf(x, y) = 0$ 也是该直线的方程。改变 $k$ 将缩放距离，并控制着直线的哪一侧具有正的带符号距离，哪一侧是负的。我们希望选择 $k$，使得，例如，$kf(x, y) = \beta$。由于 $k$ 是唯一未知数，我们可以通过一个约束来强制实现这一点，即在点 $\bold{b}$ 处我们知道 $\beta = 1$。因此，如果线 $f_{ac}(x, y) = 0$ 通过 $\bold{a}$ 和 $\bold{c}$，那么我们可以计算点 $(x, y)$ 的 $\beta$ 如下：
$$
\beta = \frac{f_{ac}(x, y)}{f_{ac}(x_b, y_b)} \ \ \ \ \ (2.32) \\
$$
![Figure 2.37](.\Images\Figure 2.37.png)
Figure 2.37. The barycentric coordinate $β$ is the signed scaled distance from the line through $\bold{a}$ and $\bold{c}$ 
图 2.37  重心坐标 $β$ 是距通过 $\bold{a}$ 和 $\bold{c}$ 的线的带符号缩放距离

and we can compute $γ$ and $α$ in a similar fashion. For efficiency, it is usually wise to compute only two of the barycentric coordinates directly and to compute the third using Equation (2.30).
我们可以用类似的方式计算 $γ$ 和 $α$。 为了提高效率，通常明智的做法是直接计算两个重心坐标，并使用方程（2.30）计算第三个。

To find this “ideal” form for the line through $\bold{p}_0$ and $\bold{p}_1$, we can first use the technique of Section 2.5.2 to find some valid implicit lines through the vertices. Equation (2.17) gives us 
为了找到通过 $\bold{p}_0$ 和 $\bold{p}_1$ 的直线的“理想”形式，我们可以首先使用 2.5.2 节的技术来找到一些通过顶点的有效隐式直线。 方程（2.17）给出了我们
$f_{ab}(x, y) ≡ (y_a - y_b)x + (x_b - x_a)y + x_ay_b - x_by_a = 0  $

Note that $f_{ab}(x_c, y_c)$ probably does not equal one, so it is probably not the ideal form we seek. By dividing through by $f_{ab}(x_c, y_c)$ we get
请注意，$f_{ab}(x_c, y_c)$ 可能不等于 1，因此它可能不是我们寻求的理想形式。 除以 $f_{ab}(x_c, y_c)$ 我们得到
$γ =  \frac{(y_a - y_b)x + (x_b - x_a)y + x_ay_b - x_by_a  }{(y_a - y_b)x_c + (x_b - x_a)y_c + x_ay_b - x_by_a  }\\$

The presence of the division might worry us because it introduces the possibility of divide-by-zero, but this cannot occur for triangles with areas that are not near zero. There are analogous formulas for $α$ and $β$, but typically only one is needed: 
除法的存在可能会让我们担心，因为它引入了被零除的可能性，但对于面积不接近零的三角形来说，这种情况不会发生。 $α$ 和 $β$ 有类似的公式，但通常只需要一个：
$β =  \frac{(y_a - y_c)x + (x_c - x_a)y + x_ay_c - x_cy_a  }{(y_a - y_c)x_b + (x_c - x_a)y_b + x_ay_c - x_cy_a  } \\
α = 1 - β - γ  $

Another way to compute barycentric coordinates is to compute the areas $A_a$, $A_b$, and $A_c$, of subtriangles as shown in Figure 2.38. Barycentric coordinates obey  the rule 
计算重心坐标的另一种方法是计算子三角形的面积 $A_b$、$A_b$ 和 $Ac$，如图 2.38 所示。 重心坐标遵守规则
$$
α = A_a/A, \\
β = A_b/A, \\
γ = A_c/A, \ \ \ \ (2.33)
$$
![Figure 2.38](.\Images\Figure 2.38.png)
Figure 2.38. The barycentric coordinates are proportional to the areas of the three subtriangles shown 
图 2.38  重心坐标与所示的三个子三角形的面积成正比

where $A$ is the area of the triangle. Note that $A = A_a + A_b + A_c$, so it can be computed with two additions rather than a full area formula. This rule still holds for points outside the triangle if the areas are allowed to be signed. The reason for this is shown in Figure 2.39. Note that these are signed areas and will be computed correctly as long as the same signed area computation is used for both $A$ and the subtriangles $A_a, A_b, $ and $ A_c$. 
其中 $A$ 是三角形的面积。 请注意，$A = A_a + A_b + A_c$，因此可以通过两次加法而不是完整的面积公式来计算。 如果允许对三角形外的区域进行签名，则该规则仍然适用于三角形之外的点。 其原因如图 2.39 所示。 请注意，这些是有符号面积，只要对 $A$ 和子三角形 $A_a、A_b $和$ A_c$ 使用相同的有符号面积计算，就可以正确计算。
![Figure 2.39](.\Images\Figure 2.39.png)
Figure 2.39. The area of the two triangles shown is base times height and are thus the same, as is any triangle with a vertex on the $β = 0.5$ line. The height and thus the area is proportional to $β$ 
图 2.39  显示的两个三角形的面积是底乘以高度，因此是相同的，就像任何顶点位于 $β = 0.5$ 线上的三角形一样。 高度和面积与 $β$ 成正比



### 2.7.2 3D Triangles 3D 三角形

One wonderful thing about barycentric coordinates is that they extend almost transparently to 3D. If we assume the points $\bold{a}$, $\bold{b}$, and $\bold{c}$ are 3D, then we can still use the representation 
重心坐标的一大优点是它们几乎透明地延伸到 3D。 如果我们假设点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 是 3D，那么我们仍然可以使用表示
$\bold{p} = (1 - β - γ)\bold{a} + β\bold{b} + γ\bold{c}$

Now, as we vary $β$ and $γ$, we sweep out a plane. 
现在，当我们改变 $β$ 和 $γ$ 时，我们扫出了一个平面。

The normal vector to a triangle can be found by taking the cross product of any two vectors in the plane of the triangle (Figure 2.40). It is easiest to use two of the three edges as these vectors, for example, 
三角形的法向量可以通过三角形平面中任意两个向量的叉积来找到（图 2.40）。 最简单的是使用三个边中的两个作为这些向量，例如，
![Figure 2.40](.\Images\Figure 2.40.png)
Figure 2.40. The normal vector of the triangle is perpendicular to all vectors in the plane of the triangle, and thus perpendicular to the edges of the triangle 
图 2.40 三角形的法向量垂直于三角形平面内的所有向量，因此也垂直于三角形的边
$$
\bold{n} = (\bold{b} − \bold{a}) \cross (\bold{c} − \bold{a}). \ \ \ (2.34)
$$
Note that this normal vector is not necessarily of unit length, and it obeys the right-hand rule of cross products. 
请注意，该法向量不一定是单位长度，并且它遵循叉积的右手定则。

The area of the triangle can be found by taking the length of the cross product: 
三角形的面积可以通过叉积的长度求得：
$$
area = \frac{1}{2}\| (\bold{b} − \bold{a}) × (\bold{c} − \bold{a}) \| \ \ \ \ (2.35)
$$
Note that this is not a signed area, so it cannot be used directly to evaluate barycentric coordinates.  However, we can observe that a triangle with a “clockwise” vertex order will have a normal vector that points in the opposite direction to the normal of a triangle in the same plane with a “counterclockwise” vertex order. Recall that 
请注意，这不是带符号的区域，因此不能直接使用它来评估重心坐标。 然而，我们可以观察到，具有“顺时针”顶点顺序的三角形的法线向量将指向与同一平面中具有“逆时针”顶点顺序的三角形法线相反的方向。 回想起那个
$\bold{a} \cdot \bold{b} = \|a\| \|b\| \cos φ  $

where $φ$ is the angle between the vectors. If $\bold{a}$ and $\bold{b}$ are parallel, then $\cos φ = ±1$, and this gives a test of whether the vectors point in the same or opposite directions. This, along with Equations (2.33), (2.34), and (2.35), suggest the formulas
其中 $φ$ 是向量之间的角度。 如果 $\bold{a}$ 和 $\bold{b}$ 平行，则 $\cos φ = ±1$，这可以测试向量是否指向相同或相反的方向。 这与方程 (2.33)、(2.34) 和 (2.35) 一起得出以下公式
$α =  \frac{\bold{n} · \bold{n}_a  }{\|\bold{n}\|^2} \\
β =  \frac{\bold{n} · \bold{n}_b  }{\|\bold{n}\|^2} \\
γ =  \frac{\bold{n} · \bold{n}_c  }{\|\bold{n}\|^2}$

where $\bold{n}$ is Equation (2.34) evaluated with vertices $\bold{a}$, $\bold{b}$, and $\bold{c}$; $\bold{n}_a$ is Equation (2.34) evaluated with vertices $\bold{b}$, $\bold{c}$, and $\bold{p}$, and so on, i.e., 
其中 $\bold{n}$ 是用顶点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 计算的方程 (2.34)； $\bold{n}_a$ 是用顶点 $\bold{b}$、$\bold{c}$ 和 $\bold{p}$ 计算的方程 (2.34)，依此类推，即
$$
\bold{n}_a = (\bold{c} − \bold{b}) × (\bold{p} − \bold{b}) \\
\bold{n}_b = (\bold{a} − \bold{c}) × (\bold{p} − \bold{c}) \\
\bold{n}_c = (\bold{b} − \bold{a}) × (\bold{p} − \bold{a}) \\
(2.36)
$$

## Frequently Asked Questions 经常问的问题

### Why isn’t there vector division? 为什么没有向量除法？

It turns out that there is no “nice” analogy of division for vectors. However, it is possible to motivate the quaternions by examining this question in detail (see Hoffmann’s book referenced in the chapter notes).  事实证明，向量的除法没有“好的”类比。 然而，通过详细研究这个问题是可以激发四元数的（参见章节注释中引用的霍夫曼的书）。

### Is there something as clean as barycentric coordinates for polygons with more than three sides?  对于具有三个以上边的多边形，是否有像重心坐标一样清晰的东西？

Unfortunately there is not. Even convex quadrilaterals are much more complicated. This is one reason triangles are such a common geometric primitive in graphics. 
不幸的是没有。 即使凸四边形也要复杂得多。 这就是三角形在图形中如此常见的几何基元的原因之一。

### Is there an implicit form for 3D lines? 3D 线是否有隐式形式？

No. However, the intersection of two 3D planes defines a 3D line, so a 3D line can be described by two simultaneous implicit 3D equations.
不会。但是，两个 3D 平面的交集定义了一条 3D 线，因此 3D 线可以通过两个联立隐式 3D 方程来描述。

## Notes 注释

The history of vector analysis is particularly interesting. It was largely invented by Grassman in the mid-1800s but was ignored and reinvented later (Crowe.1994). Grassman now has a following in the graphics field of researchers who are developing Geometric Algebra based on some of his ideas (Doran & Lasenby.2003). Readers interested in why the particular scalar and vector products are in some sense the right ones, and why we do not have a commonly used vector division, will find enlightenment in the concise About Vectors (Hoffmann, 1975)Another important geometric tool is the quaternion invented by Hamilton in the mid-1800s. Quaternions are useful in many situations, but especially where orientations are concerned (Hanson.2005)
矢量分析的历史特别有趣。 它主要是由 Grassman 在 1800 年代中期发明的，但后来被忽视并被重新发明（Crowe.1994）。 Grassman 现在在图形领域拥有一批研究人员，他们正在根据他的一些想法开发几何代数（Doran & Lasenby.2003）。 对为什么特定的标量和向量积在某种意义上是正确的，以及为什么我们没有常用的向量除法感兴趣的读者会在简明的关于向量（Hoffmann，1975）中找到启发。另一个重要的几何工具是四元数 由汉密尔顿于 1800 年代中期发明。 四元数在许多情况下都很有用，特别是在涉及方向时 (Hanson.2005)

## Exercises 练习

1. The cardinality of a set is the number of elements it contains. Under IEEE floating point representation (Section 1.5), what is the cardinality of the floats? 
   集合的基数是它包含的元素的数量。 在 IEEE 浮点表示（第 1.5 节）下，浮点数的基数是多少？
2. Is it possible to implement a function that maps 32-bit integers to 64-bit integers that has a well-defined inverse? Do all functions from 32-bit integers to 64-bit integers have well-defined inverses? 
   是否可以实现一个将 32 位整数映射到具有明确定义的逆的 64 位整数的函数？ 从 32 位整数到 64 位整数的所有函数都具有明确定义的逆函数吗？
3. Specify the unit cube (x-, y-, and z-coordinates all between 0 and 1 inclusive) in terms of the Cartesian product of three intervals. 
   根据三个区间的笛卡尔积指定单位立方体（x、y 和 z 坐标均在 0 和 1 之间（包括 0 和 1））。
4. If you have access to the natural log function $\ln(x)$, specify how you could use it to implement a $\log(b, x)$ function where $b$ is the base of the log. What should the function do for negative $b$ values? Assume an IEEE floating point implementation. 
   如果您有权使用自然对数函数 $\ln(x)$，请指定如何使用它来实现 $\log(b, x)$ 函数，其中 $b$ 是对数的基数。 对于负 $b$ 值，函数应该做什么？ 假设采用 IEEE 浮点实现。
5. Solve the quadratic equation $2x^2 + 6x + 4 = 0$. 
   求解二次方程 $2x^2 + 6x + 4 = 0$。
6. Implement a function that takes in coefficients $A$, $B$, and $C$ for the quadratic equation $Ax^2 + Bx + C = 0$ and computes the two solutions. Have the function return the number of valid (not NaN) solutions and fill in the return arguments so the smaller of the two solutions is first.
   实现一个函数，该函数接受二次方程 $Ax^2 + Bx + C = 0$ 的系数 $A$、$B$ 和 $C$ 并计算两个解。 让函数返回有效（非 NaN）解决方案的数量并填写返回参数，以便两个解决方案中较小的一个位于第一个。
7. Show that the two forms of the quadratic formula on page 17 are equivalent (assuming exact arithmetic) and explain how to choose one for each root in order to avoid subtracting nearly equal floating point numbers, which leads to loss of precision
   证明第 17 页的二次公式的两种形式是等价的（假设精确算术），并解释如何为每个根选择一个形式，以避免减去几乎相等的浮点数，从而导致精度损失
8. Show by counterexample that it is not always true that for 3D vectors $\bold{a}$, $\bold{b}$, and $\bold{c}$, $\bold{a} × (\bold{b} × \bold{c}) = (\bold{a} × \bold{b}) × \bold{c}$
   通过反例证明，对于 3D 向量 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$，$\bold{a} × (\bold {b} × \bold{c}) = (\bold{a} × \bold{b}) × \bold{c}$
9. Given the nonparallel 3D vectors $\bold{a}$ and $\bold{b}$, compute a right-handed orthonormal basis such that $\bold{u}$ is parallel to $\bold{a}$ and $\bold{v}$ is in the the plane defined by $\bold{a}$ and $\bold{b}$.
   给定非平行 3D 向量 $\bold{a}$ 和 $\bold{b}$，计算右手正交基，使得 $\bold{u}$ 与 $\bold{a}$ 平行，并且 $\bold{v}$ 位于由 $\bold{a}$ 和 $\bold{b}$ 定义的平面内。
10. What is the gradient of $f(x, y, z) = x^2 + y - 3z^3$?
    $f(x, y, z) = x^2 + y - 3z^3$ 的梯度是多少？
11. What is a parametric form for the axis-aligned 2D ellipse?
    轴对齐的二维椭圆的参数形式是什么？
12. What is the implicit equation of the plane through 3D points $(1, 0, 0)$,$(0, 1, 0)$, and $(0, 0, 1)$? What is the parametric equation? What is the normal vector to this plane?
    通过 3D 点 $(1, 0, 0)$、$(0, 1, 0)$ 和 $(0, 0, 1)$ 的平面隐式方程是什么？ 参数方程是什么？ 该平面的法向量是多少？
13. Given four 2D points $\bold{a}_0$, $\bold{a}_1$, $\bold{b}_0$, and $\bold{b}_1$, design a robust procedure to determine whether the line segments $\bold{a}_0\bold{a}1$ and $\bold{b}_0\bold{b}1$ intersect.
    给定四个 2D 点 $\bold{a}_0$、$\bold{a}_1$、$\bold{b}_0$ 和 $\bold{b}_1$，设计一个稳健的过程来确定是否 线段 $\bold{a}_0\bold{a}1$ 和 $\bold{b}_0\bold{b}1$ 相交。
14. Design a robust procedure to compute the barycentric coordinates of a 2D point with respect to three 2D non-collinear points. 
    设计一个稳健的程序来计算 2D 点相对于三个 2D 非共线点的重心坐标。