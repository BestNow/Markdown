# 14  Sampling  采样

Many applications in graphics require “fair” sampling of unusual spaces, such as the space of all possible lines. For example, we might need to generate random edges within a pixel, or random sample points on a pixel that vary in density according to some density function. This chapter provides the machinery for such probability operations. These techniques will also prove useful for numerically evaluating complicated integrals using Monte Carlo integration, also covered in this chapter.
图形中的许多应用程序需要对异常空间进行“公平”采样，例如所有可能的线条的空间。 例如，我们可能需要在像素内生成随机边缘，或者在像素上生成密度根据某种密度函数变化的随机样本点。 本章提供了此类概率运算的机制。 这些技术对于使用蒙特卡罗积分对复杂积分进行数值计算也很有用，本章也将对此进行介绍。

## 14.1 Integration 集成 

Although the words “integral” and “measure” often seem intimidating, they relate to some of the most intuitive concepts found in mathematics, and they should not be feared. For our very non-rigorous purposes, a measure is just a function that maps subsets to $\R^+$ in a manner consistent with our intuitive notions of length, area, and volume. For example, on the 2D real plane $\R^2$, we have the area measure A which assigns a value to a set of points in the plane. Note that A is just a function that takes pieces of the plane and returns area. This means the domain of A is all possible subsets of $\R^2$, which we denote as the power set $ P(\R^2)$. Thus, we can characterize A in arrow notation:
尽管“积分”和“度量”这两个词常常看起来令人生畏，但它们与数学中一些最直观的概念相关，因此不应该害怕。 对于我们非常不严格的目的来说，度量只是一个函数，它以与我们直观的长度、面积和体积概念一致的方式将子集映射到 $\R^+$。 例如，在 2D 真实平面 $\R^2$ 上，我们有面积度量 A，它为平面上的一组点分配一个值。 请注意，A 只是一个获取平面碎片并返回面积的函数。 这意味着 A 的域是 $\R^2$ 的所有可能子集，我们将其表示为幂集 $P(\R^2)$。 因此，我们可以用箭头表示法来表征 A：
$A : P(\R^2) → \R^+.  $

An example of applying the area measure shows that the area of the square with side length one is one:
应用面积测量的示例显示边长为 1 的正方形的面积为 1：
$A([a, a + 1] × [b, b + 1]) = 1,  $

where $(a, b)$ is just the lower left-hand corner of the square. Note that a single point such as $(3, 7)$ is a valid subset of $\R^2$ and has zero area: $A((3, 7)) = 0$. The same is true of the set of points $S$ on the x-axis, $S = (x, y)$ such that $(x, y) ∈ \R^2$ and $y = 0$, i.e., $A(S) = 0$. Such sets are called zero measure sets.
其中 $(a, b)$ 就是正方形的左下角。 请注意，单个点（例如 $(3, 7)$）是 $\R^2$ 的有效子集，并且面积为零：$A((3, 7)) = 0$。 x 轴上的点集 $S$ 也是如此，$S = (x, y)$ 使得 $(x, y) ∈ \R^2$ 且 $y = 0$，即 $A(S) = 0$。 这样的集合称为零测量集。

To be considered a measure, a function has to obey certain area-like properties. For example, we have a function $μ : P( \mathbb{S}) → \R^+$. For $μ$ to be a measure, the following conditions must be true:
要被视为一种度量，函数必须遵循某些类似区域的属性。 例如，我们有一个函数 $μ : P( \mathbb{S}) → \R^+$。 要使 $μ$ 成为度量，必须满足以下条件：

1. The measure of the empty set is zero: $μ(∅) = 0$,
   空集的测度为零：$μ(∅) = 0$，
2. The measure of two distinct sets together is the sum of their measure alone. This rule with possible intersections is
   两个不同集合的测度是它们单独测度的总和。 这条可能有交集的规则是
   $μ(A ∪ B) = μ(A) + μ(B) - μ(A ∩ B),  $
   where ∪ is the set union operator and ∩ is the set intersection operator. 
   其中 ∪ 是集合并运算符，∩ 是集合交运算符。 

When we actually compute measures, we usually use integration. We can think of integration as really just notation:
当我们实际计算度量时，我们通常使用积分。 我们可以将积分视为真正的符号：
$A(S) = \int_x∈S dA(\bold{x})$

You can informally read the right-hand side as “take all points x in the region S, and sum their associated differential areas.” The integral is often written other ways including
您可以将右侧非正式地理解为“获取区域 S 中的所有点 x，并对它们相关的微分面积求和”。 积分通常以其他方式编写，包括
$\int_S dA, \ \ \ \int_{\bold{x}∈S}d\bold{x}, \ \ \ \int_{\bold{x}∈S}dA_\bold{x}, \ \ \ \int_{\bold{x}}d\bold{x}, \ \ \   \\ $

All of the above formulas represent “the area of region S.” We will stick with the first one we used, because it is so verbose it avoids ambiguity. To evaluate such integrals analytically, we usually need to lay down some coordinate system and use our bag of calculus tricks to solve the equations. But have no fear if those skills have faded, as we usually have to numerically approximate integrals, and that requires only a few simple techniques which are covered later in this chapter.
以上公式均表示“区域S的面积”。 我们将坚持使用我们使用的第一个，因为它非常冗长，可以避免歧义。 为了分析地评估此类积分，我们通常需要建立一些坐标系并使用我们的微积分技巧来求解方程。 但是，如果这些技能已经消失，请不要担心，因为我们通常必须对积分进行数值近似，而这只需要一些简单的技术，本章稍后将介绍这些技术。

Given a measure on a set $ \mathbb{S}$, we can always create a new measure by weighting with a nonnegative function $w :  \mathbb{S} → \R^+$. This is best expressed in integral notation. For example, we can start with the example of the simple area measure on $[0, 1]^2$:
给定集合$ \mathbb{S}$上的一个测度，我们总是可以用一个非负函数$w: \mathbb{S}→\R^+$加权来创建一个新的测度。这最好用积分符号表示。例如，我们可以从$[0,1]^2$上的简单面积度量的例子开始:
$\int_{\bold{x}∈[0,1]^2} dA(x)\\$

and we can use a “radially weighted” measure by inserting a weighting function of radius squared:
我们可以通过插入半径平方的加权函数来使用“径向加权”度量： 
$\int_{\bold{x}∈[0,1]^2} \|\bold{x}\|^2dA(x) \\$

To evaluate this analytically, we can expand using a Cartesian coordinate system with $dA ≡ dx dy$:
为了进行分析评估，我们可以使用笛卡尔坐标系 $dA ≡ dx dy$ 进行扩展： 
$\int_{\bold{x}∈[0,1]^2} \|\bold{x}\|^2dA(x) = \int^1_{x=0}\int^1_{y=0}dxdy \\$

The key thing here is that if you think of the $\|\bold{x}\|^2$ term as married to the $dA$ term, and that these together form a new measure, we can call that measure $ν$. This would allow us to write $ν(S)$ instead of the whole integral. If this strikes you as just a bunch of notation and bookkeeping, you are right. But it does allow us to write down equations that are either compact or expanded depending on our preference.
这里的关键是，如果您认为 $\|\bold{x}\|^2$ 项与 $dA$ 项结合在一起，并且它们一起形成一个新的度量，我们可以将该度量称为 $ν $。 这将允许我们写 $ν(S)$ 而不是整个积分。 如果您觉得这只是一堆符号和簿记，那么您是对的。 但它确实允许我们根据我们的喜好写下紧凑或扩展的方程。

### 14.1.1 Measures and Averages 测量值和平均值 

Measures really start paying off when taking averages of a function. You can only take an average with respect to a particular measure, and you would like to select a measure that is “natural” for the application or domain. Once a measure is chosen, the average of a function f over a region S with respect to measure μ is
当对函数取平均值时，措施才真正开始得到回报。 您只能针对特定度量取平均值，并且您希望选择对于应用程序或域来说“自然”的度量。 一旦选择了测量值，区域 S 上的函数 f 相对于测量值 μ 的平均值为
$average(f) ≡  \frac{\int_{x∈S}f(\bold{x})dμ(\bold{x})}{\int_{x∈S}dμ(\bold{x})} \\$

For example, the average of the function $f(x, y) = x^2$ over $[0, 2]^2$ with respect to the area measure is
例如，函数 $f(x, y) = x^2$ 在 $[0, 2]^2$ 上相对于面积度量的平均值为
$average(f) ≡  \frac{\int^2_{x=0}\int^2_{y=0}x^2dxdy}{\int^2_{x=0}\int^2_{y=0}dxdy} = \frac{4}{3}\\$

This machinery helps solve seemingly hard problems where choosing the measure is the tricky part. Such problems often arise in integral geometry, a field that studies measures on geometric entities, such as lines and planes. For example, one might want to know the average length of a line through $[0, 1]^2$. That is, by definition,
这种机制有助于解决看似困难的问题，而选择措施是棘手的部分。 此类问题经常出现在积分几何中，该领域研究几何实体（例如直线和平面）的测量。 例如，人们可能想知道通过 $[0, 1]^2$ 的线的平均长度。 也就是说，根据定义，
$average(length) =  \frac{\int_{lines\ L\ through\ [0, 1]^2}length(L)dμ(L)}{\int_{lines\ L\ through\ [0, 1]^2}dμ(L)  } \\$

All that is left, once we know that, is choosing the appropriate μ for the application. This is dealt with for lines in the next section.
一旦我们知道了这一点，剩下的就是为应用选择合适的μ。 这将在下一节中针对行进行处理。

### 14.1.2 Example: Measures on the Lines in the 2D Plane 示例：2D 平面上的直线测量

What measure μ is “natural”?
什么度量 μ 是“自然的”？

If you parameterize the lines as $y = mx + b$, you might think of a given line as a point $(m, b)$ in “slope-intercept” space. An easy measure to use would be $dm\ db$, but this would not be a “good” measure in that not all equal size “bundles”  of lines would have the same measure. More precisely, the measure would not be invariant with respect to change of coordinate system. For example, if you took all lines through the square $[0, 1]^2$, the measure of lines through it would not be the same as the measure through a unit square rotated 45 degrees. What we would really like is a “fair” measure that does not change with rotation or translation of a set of lines. This idea is illustrated in Figures 14.1 and 14.2.
如果将线参数化为 $y = mx + b$，您可能会将给定线视为“斜截距”空间中的点 $(m, b)$。 一个容易使用的度量是 $dm\ db$，但这不是一个“好的”度量，因为并非所有相同大小的线“束”都具有相同的度量。 更准确地说，该测量不会随着坐标系的变化而保持不变。 例如，如果您将所有直线穿过正方形 $[0, 1]^2$，则穿过该正方形的直线的测量值将与穿过旋转 45 度的单位正方形的测量值不同。 我们真正想要的是一种“公平”的度量，它不会随着一组线的旋转或平移而改变。 这个想法如图 14.1 和 14.2 所示。
![Figure 14.1](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 14.1.png)
Figure 14.1. These two bundles of lines should have the same measure. They have different intersection lengths with the y-axis so using $db$ would be a poor choice for a differential measure.
图 14.1。 这两束线应该具有相同的尺寸。 它们与 y 轴的交叉长度不同，因此使用 $db$ 对于差分测量来说是一个糟糕的选择。
![Figure 14.2](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 14.2.png)
Figure 14.2. These two bundles of lines should have the same measure. Since they have different values for change in slope, using dm would be a poor choice for a differential measure.
图 14.2。 这两束线应该具有相同的尺寸。 由于它们的斜率变化具有不同的值，因此使用 dm 作为差分测量并不是一个好的选择。

To develop a natural measure on the lines, we should first start thinking of them as points in a dual space. This is a simple concept: the line $y = mx + b$ can be specified as the point $(m, b)$ in a slope-intercept space. This concept is illustrated in Figure 14.3. It is more straightforward to develop a measure in $(φ, b)$ space. In that space b is the y-intercept, while φ is the angle the line makes with the x-axis, as shown in Figure 14.4. Here, the differential measure $dφ\ db$ almost works, but it would not be fair due to the effect shown in Figure 14.1. To account for the larger span b that a constant width bundle of lines makes, we must add a cosine factor:
为了发展直线上的自然测度，我们首先应该把直线看作对偶空间中的点。这是一个简单的概念:直线$y = mx + b$可以指定为斜率-截距空间中的点$(m, b)$。图14.3说明了这个概念。在$(φ， b)$空间中建立一个测度更为直接。其中，b为y轴截距，φ为直线与x轴夹角，如图14.4所示。这里，差分度量$dφ\ db$几乎可以工作，但由于图14.1所示的效果，它可能不公平。为了解释恒定宽度的线束形成的更大的跨度b，我们必须添加余弦因子:

$dμ = cos φ dφ db.  $
![Figure 14.3](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 14.3.png)
Figure 14.3. The set of points on the line $y = m x + b$ in $(x, y)$ space can also be represented by a single point in $(m, b)$ space so the top line and the bottom point represent the same geometric entity: a 2D line.
图14.3。$(x, y)$空间中$y = m x + b$上的点的集合也可以用$(m, b)$空间中的单个点来表示，因此顶部的线和底部的点表示相同的几何实体:一条2D线。
![Figure 14.4](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 14.4.png)
Figure 14.4. In angle-intercept space we parameterize the line by angle $φ ∈ [−π/2, π/2)$ rather than slope.
图 14.4。 在角截距空间中，我们通过角度 $φ ∈ [−π/2, π/2)$ 而不是斜率来参数化直线。

It can be shown that this measure, up to a constant, is the only one that is invariant with respect to rotation and translation.
可以证明，这一度量在达到常数的情况下是唯一相对于旋转和平移不变的度量。

This measure can be converted into an appropriate measure for other parameterizations of the line. For example, the appropriate measure for $(m, b)$ space is
该测量可以转换为适合生产线其他参数化的测量。 例如，$(m, b)$ 空间的适当度量是
$dμ =  \frac{dm db}{(1+m^2)^{\frac{3}{2}}} \\$

For the space of lines parameterized in $(u, v)$ space,
对于 $(u, v)$ 空间中参数化的线空间，
$ux + vy + 1 = 0,  $

the appropriate measure is
适当的措施是
$dμ =  \frac{du dv}{(u^2 + v^2)^{\frac{3}{2}}} \\ $

For lines parameterized in terms of (a, b), the x-intercept and y-intercept, the measure is
对于根据 (a, b)、x 截距和 y 截距参数化的线，测量为
$dμ =  \frac{ab\ da\ db}{(a^2 + b^2)^{\frac{3}{2}}} \\$

Note that any of those spaces are equally valid ways to specify lines, and which is best depends upon the circumstances. However, one might wonder whether there exists a coordinate system where the measure of a set of lines is just an area in the dual space. In fact, there is such a coordinate system, and it is delightfully simple; it is the normal coordinates which specify a line in terms of the normal distance from the origin to the line, and the angle the normal of the line makes with respect to the x-axis (Figure 14.5). The implicit equation for such lines is
请注意，任何这些空格都是指定行的同等有效方式，具体哪种方式最好取决于具体情况。 然而，人们可能想知道是否存在一个坐标系，其中一组线的度量只是对偶空间中的一个区域。 事实上，确实有这样一个坐标系，而且简单得令人高兴； 它是法线坐标，根据从原点到线的法线距离以及线的法线相对于 x 轴的角度来指定线（图 14.5）。 此类直线的隐式方程为
$x \cos θ + y \sin θ - p = 0.  $
![Figure 14.5](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 14.5.png)
Figure 14.5. The normal coordinates of a line use the normal distance to the origin and an angle to specify a line.
图 14.5。 直线的法线坐标使用到原点的法线距离和角度来指定直线。

And, indeed, the measure in that space is
事实上，该空间的度量是
$dμ = dp\ dθ.$

We shall use these measures to choose fair random lines in a later section. 
我们将在后面的部分中使用这些措施来选择公平的随机线。 

### 14.1.3 Example: Measure of Lines in 3D 示例：3D 线的测量

In 3D there are many ways to parameterize lines. Perhaps, the simplest way is to use their intersection with a particular plane along with some specification of their orientation. For example, we could chart the intersection with the $xy$ plane along with the spherical coordinates of its orientation. Thus, each line would be specified as a $(x, y, θ, φ)$ quadruple. This shows that lines in 3D are 4D entities, i.e., they can be described as points in a 4D space.
在 3D 中，有多种方法可以对线进行参数化。 也许，最简单的方法是使用它们与特定平面的交集以及它们的方向的某些规范。 例如，我们可以绘制与 $xy$ 平面的交点及其方向的球面坐标。 因此，每条线将被指定为 $(x, y, θ, φ)$ 四元组。 这表明 3D 中的线是 4D 实体，即它们可以描述为 4D 空间中的点。

The differential measure of a line should not vary with (x, y), but bundles of lines with equal cross section should have equal measure. Thus, a fair differential measure is
一条线的微分测量不应随 (x, y) 变化，但具有相同横截面的线束应具有相同的测量。 因此，公平的差别措施是
$dμ = dx\ dy \sin θ dθ dφ.$

Another way to parameterize lines is to chart the intersection with two parallel planes. For example, if the line intersects the plane $z = $0 at $(x = u, y = v)$ and the plane $z = 1$ at $(x = s, y = t)$, then the line can be described by the quadruple $(u, v, s, t)$. Note, that like the previous parameterization, this one is degenerate for lines parallel to the $xy$ plane. The differential measure is more complicated for this parameterization although it can be approximated as
参数化线的另一种方法是绘制与两个平行平面的交线。 例如，如果直线在 $(x = u, y = v)$ 处与平面 $z = $0 相交，并在 $(x = s, y = t)$ 处与平面 $z = 1$ 相交，则直线可以 由四元组$(u, v, s, t)$描述。 请注意，与之前的参数化一样，对于平行于 $xy$ 平面的线，此参数化是退化的。 对于这种参数化，微分测量更加复杂，尽管它可以近似为
$dμ ≈ du\ dv\ a\ ds\ dt,  $

for bundles of lines nearly parallel to the z-axis. This is the measure often implicitly used in image-based rendering.
对于几乎平行于 z 轴的线束。 这是基于图像的渲染中经常隐式使用的度量。 

For sets of lines that intersect a sphere, we can use the parameterization of the two points where the line intersects the sphere. If these are in spherical coordinates, then the point can be described by the quadruple $(θ_1, φ_1, θ_2, φ_2)$ and the measure is just the differential area associated with each point:
对于与球体相交的线组，我们可以使用线与球体相交的两个点的参数化。 如果这些是在球坐标中，则该点可以用四元组 $(θ_1, φ_1, θ_2, φ_2)$ 来描述，并且度量只是与每个点相关的微分面积：
$dμ = \sin θ_1 dθ_1 dφ_1 \sin θ_2 dθ_2 dφ_2.  $

This implies that picking two uniform random endpoints on the sphere results in a line with uniform density. This observation was used to compute form-factors by Mateu Sbert in his dissertation (Sbert, 1997).
这意味着在球体上选取两个均匀的随机端点会产生密度均匀的线。 Mateu Sbert 在他的论文中使用这一观察结果来计算形状因子（Sbert，1997）。

Note that sometimes we want to parameterize directed lines, and sometimes we want the order of the endpoints not to matter. This is a bookkeeping detail that is especially important for rendering applications where the amount of light flowing along a line is different in the two directions along the line.
请注意，有时我们想要参数化有向线，有时我们希望端点的顺序无关紧要。 这是一个记录细节，对于渲染应用程序尤其重要，因为沿着一条线流动的光量在沿线的两个方向上是不同的。

## 14.2 Continuous Probability 连续概率

Many graphics algorithms use probability to construct random samples to solve integration and averaging problems. This is the domain of applied continuous probability which has basic connections to measure theory. 
许多图形算法使用概率来构造随机样本来解决积分和平均问题。 这是应用连续概率的领域，与测度论有基本联系。

### 14.2.1 One-Dimensional Continuous Probability Density Functions 一维连续概率密度函数 

Loosely speaking, a continuous random variable $x$ is a scalar or vector quantity that “randomly” takes on some value from the real line $\R = (−∞, +∞)$. The behavior of x is entirely described by the distribution of values it takes. This distribution of values can be quantitatively described by the probability density function (pdf), p, associated with $x$ (the relationship is denoted $x ∼ p$). The probability that x assumes a particular value in some interval $[a, b]$ is given by the following integral:
宽松地说，连续随机变量 $x$ 是一个标量或向量，它“随机”从实数线 $\R = (−∞, +∞)$ 中获取一些值。 x 的行为完全由它所取值的分布来描述。 这种值的分布可以通过与 $x$ 相关的概率密度函数 (pdf) p 来定量描述（该关系表示为 $x ∼ p$）。 x 在某个区间 $[a, b]$ 中取特定值的概率由以下积分给出：
$$
Probability(x ∈ [a, b]) = \int^a_bp(x)dx \ \ \ \ (14.1)
$$
Loosely speaking, the probability density function p describes the relative likelihood of a random variable taking a certain value; if $p(x_1) = 6.0$ and $p(x_2) = 3.0$, then a random variable with density p is twice as likely to have a value “near” $x_1$ than it is to have a value near $x_2$. The density p has two characteristics:
广义地说，概率密度函数p描述了一个随机变量取某一值的相对似然;如果是$p(x_1) = 6.0$和$p(x_2) = 3.0$，那么密度p的随机变量在$x_1$附近的概率是在$x_2$附近的概率的两倍。密度p有两个特点:
$$
p(x) ≥ 0 (probability\ is\ nonnegative), \ \ \ \ \ (14.2) \\
\int^{+∞}_{-∞}p(x)dx = 1 (Probability(x ∈ \R) = 1). \ \ \ \ \  (14.3)
$$
As an example, the canonical random variable ξ takes on values between zero (inclusive) and one (non-inclusive) with uniform probability (here uniform simply means each value for ξ is equally likely). This implies that the probability density function q for ξ is
作为一个例子，规范随机变量ξ以均匀的概率取0(包括)和1(不包括)之间的值(这里均匀仅仅意味着ξ的每个值都是等可能的)。这意味着ξ的概率密度函数q是
$$
q(ξ) = \begin{cases}
1\ \  \ \ \ \ if\ 0 ≤ ξ < 1, \\
0\ \ \ \ \ \ otherwise
\end{cases}
$$
The space over which ξ is defined is simply the interval $[0, 1)$. The probability that ξ takes on a value in a certain interval $[a, b] ∈ [0, 1)$ is
定义ξ的空间就是区间$[0, 1)$。ξ在某一区间$[a, b] ∈ [0, 1)$取值的概率是
$$
Probability(a ≤ ξ ≤ b) = \int^b_a1dx = b-a.
$$

### 14.2.2 One-Dimensional Expected Value 一维期望值

The average value that a real function f of a one-dimensional random variable with underlying pdf $p$ will take on is called its expected value, $E(f(x))$ (sometimes written $Ef(x))$:
具有基础 pdf $p$ 的一维随机变量的实函数 f 所取的平均值称为其期望值 $E(f(x))$ （有时写作 $Ef(x))$：
$E(f(x)) = \int f(x)p(x)dx \\$

The expected value of a one-dimensional random variable can be calculated by setting $f(x) = x$. The expected value has a surprising and useful property: the expected value of the sum of two random variables is the sum of the expected values of those variables:
一维随机变量的期望值可以通过设置 $f(x) = x$ 来计算。 期望值有一个令人惊讶且有用的属性：两个随机变量之和的期望值是这些变量的期望值之和：
$E(x + y) = E(x) + E(y),$

for random variables x and y. Because functions of random variables are themselves random variables, this linearity of expectation applies to them as well:
对于随机变量 x 和 y。 因为随机变量的函数本身就是随机变量，所以这种期望的线性也适用于它们： 
$E(f(x) + g(y)) = E(f(x)) + E(g(y)).  $

An obvious question to ask is whether this property holds if the random variables being summed are correlated (variables that are not correlated are called independent). This linearity property in fact does hold whether or not the variables are independent! This summation property is vital for most Monte Carlo applications.
一个明显的问题是，如果求和的随机变量是相关的（不相关的变量称为独立的），这个属性是否成立。 事实上，无论变量是否独立，这种线性属性都成立！ 此求和属性对于大多数蒙特卡罗应用至关重要。

### 14.2.3 Multidimensional Random Variables 多维随机变量

The discussion of random variables and their expected values extends naturally to multidimensional spaces. Most graphics problems will be in such higher-dimensional spaces. For example, many lighting problems are phrased on the surface of the hemisphere. Fortunately, if we define a measure $μ$ on the space the random variables occupy, everything is very similar to the one-dimensional case. Suppose the space S has associated measure $μ$; for example S is the surface of a sphere and $μ$ measures area. We can define a pdf $p : S \mapsto \R$, and if $x$ is a random variable with $x ∼ p$, then the probability that x will take on a value in some region $S_i ⊂ S$ is given by the integral
对随机变量及其期望值的讨论自然延伸到多维空间。 大多数图形问题都出现在这样的高维空间中。 例如，许多照明问题都是在半球表面上表述的。 幸运的是，如果我们在随机变量占据的空间上定义一个度量$μ$，那么一切都与一维情况非常相似。 假设空间S有关联测度$μ$； 例如，S 是球体的表面，$μ$ 测量面积。 我们可以定义一个 pdf $p : S \mapsto \R$，如果 $x$ 是一个 $x ∼ p$ 的随机变量，那么 x 在某个区域 $S_i ⊂ S$ 取值的概率为 由积分给出
$Probability(x ∈ Si) = \int_{S_i} p(x)dμ.\\$

Here Probability (event ) is the probability that event is true, so the integral is the probability that x takes on a value in the region $S_i$. 
这里的概率 (event ) 是事件为真的概率，因此积分是 x 在 $S_i$ 区域中取值的概率。

In graphics, S is often an area $(dμ = dA = dxdy)$ or a set of directions (points on a unit sphere: $dμ = dω = sin θ dθ dφ$). As an example, a two-dimensional random variable $α$ is a uniformly distributed random variable on a disk of radius R. Here uniformly means uniform with respect to area, e.g., the way a bad dart player’s hits would be distributed on a dart board. Since it is uniform, we know that $p(α)$ is some constant. From the fact that the area of the disk is $πr^2$ and that the total probability is one, we can deduce that
在图形中，S 通常是一个面积 $(dμ = dA = dxdy)$ 或一组方向（单位球面上的点：$dμ = dω = sin θ dθ dφ$）。 举个例子，二维随机变量 $α$ 是半径为 R 的圆盘上均匀分布的随机变量。这里均匀意味着面积均匀，例如，糟糕的飞镖玩家的命中在飞镖上的分布方式 木板。 由于它是一致的，我们知道 $p(α)$ 是某个常数。 根据圆盘面积为 $πr^2$ 且总概率为 1 的事实，我们可以推断出
$p(α) =  \frac{1}{πR^2}\\$

This means that the probability that α is in a certain subset $S_1$ of the disk is just
这意味着 α 位于磁盘的某个子集 $S_1$ 中的概率为
$Probability(α ∈ S_1) = \int_{S_1}\frac{1}{πR^2}dA \\$

This is all very abstract. To actually use this information, we need the integral in a form we can evaluate. Suppose $S_i$ is the portion of the disk closer to the center than the perimeter. If we convert to polar coordinates, then $α$ is represented as a $(r, φ)$ pair, and $S_1$ is the region where $r < R/2$. Note, that just because $α$ is uniform, it does not imply that $φ$ or $r$ are necessarily uniform (in fact, $φ$ is uniform, and $r$ is not uniform). The differential area $dA$ is just $r\ dr\ dφ$. Thus,
这一切都非常抽象。 为了实际使用这些信息，我们需要采用可以计算的形式进行积分。 假设 $S_i$ 是圆盘上比周边更靠近中心的部分。 如果我们转换为极坐标，则$α$表示为$(r, φ)$对，$S_1$是$r < R/2$的区域。 请注意，仅仅因为 $α$ 是一致的，并不意味着 $φ$ 或 $r$ 一定是一致的（事实上，$φ$ 是一致的，而 $r$ 不是一致的）。 微分面积$dA$就是$r\ dr\ dφ$。 因此，
$Probability (r < R^2 ) = \int^{2\pi}_0\int^{(\frac{R}{2})}_0 \frac{1}{\pi R^2}r\ dr\ dφ = 0.25\\ $

The formula for expected value of a real function applies to the multidimensional case:
实函数期望值的公式适用于多维情况：
$E(f(x)) = \int_S f(x)p(x)dμ, \\ $

where $x ∈ S$ and $f : S \mapsto \R$, and $p : S \mapsto \R$. For example, on the unit square $S = [0, 1] × [0, 1]$ and $p(x, y) = 4xy$, the expected value of the $x$ coordinate for $(x, y) ∼ p$ is
比如$x ∈ S$$f : S \mapsto \R$和$p : S \mapsto \R$。例如，在单位方格$S = [0, 1] × [0, 1]$和$p(x, y) = 4xy$上，$(x, y) ∼ p$的$x$坐标的期望值为
$$
E(x) = \int_S f(x, y)p(x, y)dA \\
= \int^1_0\int^1_0 4x^2y dx dy \\
= \frac{2}{3}
$$
Note that here $f(x, y) = x$.
注意这里$f(x, y) = x$。 

### 14.2.4 Variance 方差

The variance, V (x), of a one-dimensional random variable is, by definition, the expected value of the square of the difference between x and E(x):
根据定义，一维随机变量的方差 V (x) 是 x 和 E(x) 之差的平方的期望值：
$V (x) ≡ E([x - E(x)]^2)  $

Some algebraic manipulation gives the non-obvious expression:
一些代数运算给出了不明显的表达式：
$V (x) = E(x^2) - [E(x)]^2 .  $

The expression $E([x − E(x)]^2)$ is more useful for thinking intuitively about variance, while the algebraically equivalent expression $E(x^2) − [E(x)]^2$ is usually convenient for calculations. The variance of a sum of random variables is the sum of the variances if the variables are independent. This summation property of variance is one of the reasons it is frequently used in analysis of probabilistic models. The square root of the variance is called the standard deviation, $σ$, which gives some indication of expected absolute deviation from the expected value.
表达式 $E([x − E(x)]^2)$ 对于直观地思考方差更有用，而代数等效表达式 $E(x^2) − [E(x)]^2$ 通常更方便 计算。 如果变量是独立的，则随机变量之和的方差是方差之和。 方差的求和性质是它经常用于概率模型分析的原因之一。 方差的平方根称为标准差 $σ$，它给出了与预期值的预期绝对偏差的一些指示。

### 14.2.5 Estimated Means 估计平均值

Many problems involve sums of independent random variables $x_i$, where the variables share a common density p. Such variables are said to be independent identically distributed (iid) random variables. When the sum is divided by the number of variables, we get an estimate of $E(x)$:
许多问题涉及独立随机变量 $x_i$ 的总和，其中变量共享公共密度 p。 这些变量被称为独立同分布（iid）随机变量。 当总和除以变量数量时，我们得到 $E(x)$ 的估计值：
$E(x) ≈ \frac{1}{N}\sum^N_{i=1}x_i \\$

As N increases, the variance of this estimate decreases. We want $N$ to be large enough so that we have confidence that the estimate is “close enough.” However, there are no sure things in Monte Carlo; we just gain statistical confidence that our estimate is good. To be sure, we would have to have $N = ∞$. This confidence is expressed by the Law of Large Numbers:
随着 N 的增加，该估计的方差会减小。 我们希望 $N$ 足够大，以便我们有信心估计值“足够接近”。 然而，蒙特卡洛没有确定的事情； 我们只是获得了统计上的信心，相信我们的估计是好的。 可以肯定的是，我们必须有 $N = ∞$。 这种信心由大数定律表达：
$Probability[E(x) = \lim_{N\rightarrow ∞} \frac{1}{N}\sum^N_{i=1}x_i] = 1 \\$ 

## 14.3 Monte Carlo Integration 蒙特卡罗积分

In this section, the basic Monte Carlo solution methods for definite integrals are outlined. These techniques are then straightforwardly applied to certain integral problems. All of the basic material of this section is also covered in several of the classic Monte Carlo texts. (See the Notes section at the end of this chapter.)
本节概述定积分的基本蒙特卡罗求解方法。 然后，这些技术可以直接应用于某些积分问题。 本节的所有基本材料也包含在一些经典的蒙特卡罗文本中。 （参见本章末尾的注释部分。）

As discussed earlier, given a function $f : S \mapsto \R$ and a random variable $x ∼ p$, we can approximate the expected value of f(x) by a sum:
如前所述，给定函数 $f : S \mapsto \R$ 和随机变量 $x ∼ p$，我们可以通过总和来近似 f(x) 的期望值：
$$
E(f(x)) = \int_{x∈S} f(x)p(x)dμ ≈ \frac{1}{N}\sum^N_{i=1}f(x_i) \ \ \ (14.4)
$$
Because the expected value can be expressed as an integral, the integral is also approximated by the sum. The form of Equation (14.4) is a bit awkward; we would usually like to approximate an integral of a single function g rather than a product $fp$. We can accomplish this by substituting $g = fp$ as the integrand:
由于期望值可以表示为积分，因此积分也可以通过总和来近似。 方程（14.4）的形式有点尴尬； 我们通常希望近似单个函数 g 的积分，而不是乘积 $fp$。 我们可以通过替换 $g = fp$ 作为被积函数来实现这一点：
$$
\int_{x∈S} = g(x)dμ ≈ \frac{1}{N}\sum^{N}_{i=1}\frac{g(x_i)}{p(x_i)} \ \ \ (14.5)
$$
For this formula to be valid, p must be positive when g is nonzero.
为了使该公式有效，当 g 不为零时，p 必须为正。

So to get a good estimate, we want as many samples as possible, and we want the $g/p$ to have a low variance ($g$ and $p$ should have a similar shape). Choosing $p$ intelligently is called importance sampling, because if $p$ is large where $g$ is large, there will be more samples in important regions. Equation (14.4) also shows the fundamental problem with Monte Carlo integration: diminishing return. Because the variance of the estimate is proportional to $1/N$, the standard deviation is proportional to $1/\sqrt{N}$. Since the error in the estimate behaves similarly to the standard deviation, we will need to quadruple $N$ to halve the error. 
因此，为了获得良好的估计，我们需要尽可能多的样本，并且希望 $g/p$ 具有较低的方差（$g$ 和 $p$ 应该具有相似的形状）。 智能地选择$p$称为重要性采样，因为如果$p$很大而$g$很大，那么重要区域会有更多的样本。 方程（14.4）还显示了蒙特卡罗积分的基本问题：收益递减。 由于估计的方差与 $1/N$ 成正比，因此标准差与 $1/\sqrt{N}$ 成正比。 由于估计误差的表现与标准差类似，因此我们需要将 $N$ 翻四倍才能将误差减半。

Another way to reduce variance is to partition $S$, the domain of the integral, into several smaller domains $S_i$, and evaluate the integral as a sum of integrals over the Si. This is called stratified sampling, the technique that jittering employs in pixel sampling (Chapter 4). Normally only one sample is taken in each $S_i$ (with density $p_i$), and in this case the variance of the estimate is:
减少方差的另一种方法是将积分域 $S$ 划分为几个较小的域 $S_i$，并将积分评估为 Si 上的积分之和。 这称为分层采样，即抖动在像素采样中采用的技术（第 4 章）。 通常，每个 $S_i$ 中仅抽取一个样本（密度为 $p_i$），在这种情况下，估计的方差为：
$$
var(\sum^N_{i=1}\frac{g(x_i)}{p_i(x_i)}) = \sum^N_{i = 1}var(\frac{g(x_i)}{p_i(x_i)})  \ \ \ \ (14.6)
$$
It can be shown that the variance of stratified sampling is never higher than unstratified if all strata have equal measure: 
可以证明，如果所有层具有相同的度量，则分层抽样的方差永远不会高于未分层抽样的方差：
$\int_{S_i} p(x)dμ =  \frac{1}{N}\int_Sp(x)dμ\\$

The most common example of stratified sampling in graphics is jittering for pixel sampling as discussed in Section 13.4.
图形中分层采样最常见的例子是像素采样的抖动，如第 13.4 节所述。

As an example of the Monte Carlo solution of an integral I, set $g(x)$ equal to $x$ over the interval $(0, 4)$:
作为积分 I 的蒙特卡洛解的示例，设置 $g(x)$ 在区间 $(0, 4)$ 上等于 $x$：
$$
I = \int^4_0xdx = 8 \ \ \ \ \ (14.7)
$$
The impact of the shape of the function p on the variance of the $N$ sample estimates is shown in Table 14.1. Note that the variance is reduced when the shape of $p$ is similar to the shape of $g$. The variance drops to zero if $p = g/I$, but I is not usually known or we would not have to resort to Monte Carlo. One important principle illustrated in Table 14.1 is that stratified sampling is often far superior to importance sampling (Mitchell, 1996). Although the variance for this stratification on $I$ is inversely proportional to the cube of the number of samples, there is no general result for the behavior of variance under stratification. There are some functions for which stratification does no good. One example is a white noise function, where the variance is constant for all regions. On the other hand, most functions will benefit from stratified sampling, because the variance in each subcell will usually be smaller than the variance of the entire domain.
函数 p 的形状对 $N$ 样本估计方差的影响如表 14.1 所示。 请注意，当 $p$ 的形状与 $g$ 的形状相似时，方差会减小。 如果 $p = g/I$，则方差降至零，但 I 通常不知道，否则我们不必求助于蒙特卡洛。 表 14.1 中说明的一个重要原则是分层抽样通常远远优于重要性抽样（Mitchell，1996）。 尽管 $I$ 上的这种分层的方差与样本数量的立方成反比，但分层下的方差行为没有一般结果。 对于某些功能，分层没有什么好处。 一个例子是白噪声函数，其中所有区域的方差都是恒定的。 另一方面，大多数函数将受益于分层采样，因为每个子单元中的方差通常小于整个域的方差。

|   Method   | Sampling function |   Variance   | Samples needed for standard error of 0.008 |
| :--------: | :---------------: | :----------: | :----------------------------------------: |
| importance |   (6 - x)/(16)    | $56.8N^{-1}$ |                  887,500                   |
| importance |        1/4        | $21.3N^{-1}$ |                  332,812                   |
| importance |    (x + 2)/16     | $6.3N^{-1}$  |                   98,437                   |
| importance |        x/8        |      0       |                     1                      |
| stratified |        1/4        | $21.3N^{-3}$ |                     70                     |

Table 14.1. Variance for Monte Carlo estimate of $\int^4_0xdx$.
表 14.1。 $\int^4_0xdx$ 的蒙特卡罗估计方差。

### 14.3.1 Quasi–Monte Carlo Integration 准蒙特卡罗积分

A popular method for quadrature is to replace the random points in Monte Carlo integration with quasi-random points. Such points are deterministic, but are in some sense uniform. For example, on the unit square $[0, 1]^2$, a set of N quasi-random points should have the following property on a region of area A within the square:
一种流行的求积方法是用准随机点代替蒙特卡罗积分中的随机点。 这些点是确定性的，但在某种意义上是一致的。 例如，在单位正方形 $[0, 1]^2$ 上，一组 N 个准随机点在该正方形内面积 A 的区域上应具有以下性质
$number\ of\ points\ in\ the\ region ≈ AN  $

For example, a set of regular samples in a lattice has this property.
例如，晶格中的一组规则样本就具有此属性。

Quasi-random points can improve performance in many integration applications. Sometimes care must be taken to make sure that they do not introduce aliasing. It is especially nice that, in any application where calls are made to random or stratified points in $[0, 1]^d$, one can substitute d-dimensional quasi-random points with no other changes. 
准随机点可以提高许多集成应用程序的性能。 有时必须小心确保它们不会引入混叠。 特别好的一点是，在任何调用 $[0, 1]^d$ 中的随机或分层点的应用程序中，我们可以替换 d 维准随机点而无需其他更改。

The key intuition motivating quasi–Monte Carlo integration is that when estimating the average value of an integrand, any set of sample points will do, provided they are “fair.”
激发准蒙特卡罗积分的关键直觉是，在估计被积函数的平均值时，任何样本点集都可以，只要它们是“公平的”。

## 14.4 Choosing Random Points 选择随机点

We often want to generate sets of random or pseudorandom points on the unit square for applications such as distribution ray tracing. There are several methods for doing this, e.g., jittering (see Section 13.4). These methods give us a set of N reasonably equidistributed points on the unit square $[0, 1]^2$ : $(u_1, v_1)$ through $(u_N , v_N)$. 
我们经常希望在单位正方形上生成随机或伪随机点集，以用于分布光线追踪等应用。 有几种方法可以做到这一点，例如抖动（参见第 13.4 节）。 这些方法为我们提供了单位正方形 $[0, 1]^2$ 上一组 N 个合理均匀分布的点：$(u_1, v_1)$ 到 $(u_N , v_N)$。

Sometimes, our sampling space may not be square (e.g., a circular lens), or may not be uniform (e.g., a filter function centered on a pixel). It would be nice if we could write a mathematical transformation that would take our equidistributed points $(u_i, v_i)$ as input and output a set of points in our desired sampling space with our desired density. For example, to sample a camera lens, the transformation would take $(u_i, v_i)$ and output $(r_i, φ_i)$ such that the new points are approximately equidistributed on the disk of the lens. While we might be tempted to use the transform
有时，我们的采样空间可能不是正方形的（例如，圆形透镜），或者可能不均匀（例如，以像素为中心的滤波器函数）。 如果我们可以编写一个数学变换，将均匀分布的点 $(u_i, v_i)$ 作为输入，并以所需的密度输出所需采样空间中的一组点，那就太好了。 例如，要对相机镜头进行采样，变换将采用 $(u_i, v_i)$ 并输出 $(r_i, φ_i)$ ，以便新点近似均匀分布在镜头圆盘上。 虽然我们可能会想使用转换
$$
φ_i = 2πu_i, \\
r_i = v_iR,
$$
it has a serious problem. While the points do cover the lens, they do so nonuniformly (Figure 14.6). What we need in this case is a transformation that takes equal-area regions to equal-area regions—one that takes uniform sampling distributions on the square to uniform distributions on the new domain.
它有一个严重的问题。 虽然这些点确实覆盖了镜头，但它们的覆盖并不均匀（图 14.6）。 在这种情况下，我们需要的是一种将等面积区域转换为等面积区域的转换，即将正方形上的均匀采样分布转换为新域上的均匀分布。 
![Figure 14.6](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 14.6.png)
Figure 14.6. The transform that takes the horizontal and vertical dimensions uniformly to $(r, φ)$ does not preserve relative area; not all of the resulting areas are the same.
图 14.6。 将水平和垂直尺寸统一为 $(r, φ)$ 的变换不会保留相对面积； 并非所有生成的区域都是相同的。

There are several ways to generate such nonuniform points or uniform points on non-rectangular domains, and the following sections review the three most often used: function inversion, rejection, and Metropolis.
有多种方法可以在非矩形域上生成此类非均匀点或均匀点，以下部分回顾最常用的三种：函数求逆、拒绝和 Metropolis。

### 14.4.1 Function Inversion 函数反转

If the density $f(x)$ is one-dimensional and defined over the interval $x ∈ [x_{min}, x_{max}]$, then we can generate random numbers $α_i$ that have density $f$ from a set of uniform random numbers $ξ_i$, where $ξ_i ∈ [0, 1]$. To do this, we need the cumulative probability distribution function $P(x)$:
如果密度 $f(x)$ 是一维的，并且定义在区间 $x ∈ [x_{min}, x_{max}]$ 上，那么我们可以生成密度为 $f$ 的随机数 $α_i$ 一组均匀随机数$ xi_i $，其中$ xi_i ∈ [0, 1] $。 为此，我们需要累积概率分布函数 $P(x)$：
$Probability(α < x) = P (x) =  \int^x_{x_{min}}f(x')dμ.  \\ $

To get $α_i$, we simply transform $ξ_i$:
为了得到$α_i$，我们只需变换$ψ_i$： 
$α_i = P^{-1}(ξ_i),  $

where $P^{−1}$ is the inverse of $P$. If $P$ is not analytically invertible, then numerical methods will suffice, because an inverse exists for all valid probability distribution functions.
其中 $P^{−1}$ 是 $P$ 的倒数。 如果 $P$ 在分析上不可逆，那么数值方法就足够了，因为所有有效的概率分布函数都存在逆函数。

Note that analytically inverting a function is more confusing than it should be due to notation. For example, if we have the function
请注意，由于符号的原因，分析求逆函数比应有的情况更令人困惑。 例如，如果我们有函数
$y=x^2$

for $x > 0$, then the inverse function is expressed in terms of $y$ as a function of $x$:
对于 $x > 0$，则反函数用 $y$ 表示为 $x$ 的函数：
$x = \sqrt{y}$  

When the function is analytically invertible, it is almost always that simple. However, things are a little more opaque with the standard notation:
当函数在解析上是可逆的时，它几乎总是那么简单。 然而，使用标准符号时事情有点不透明：
$f(x) = x^2, \\
f^{-1}(x) = \sqrt{x}.  $

Here x is just a dummy variable. You may find it easier to use the less standard notation:
这里x只是一个虚拟变量。 您可能会发现使用不太标准的符号更容易：
$y = x^2,\\
x = \sqrt{y},  $

while keeping in mind that these are inverse functions of each other.
同时请记住，它们是彼此的反函数。

For example, to choose random points $x_i$ that have density
例如，选择具有密度的随机点 $x_i$
$p(x) = \frac{3x^2}{2}\\$

on [-1, 1], we see that
在 [-1, 1] 上，我们看到
$P(x) = \frac{x^3+1}{2}\\$

and
和
$P^{-1}(x) = \sqrt[3]{2x-1}  $

so we can “warp” a set of canonical random numbers $(ξ_1, · · · , ξ_N)$ to the properly distributed numbers
所以我们可以将一组规范随机数$(ξ_1, · · · , ξ_N)$”扭曲”为正确分布的数字
$(x_1, · · · , x_N) = (\sqrt[3]{2ξ_1 - 1}, · · · , \sqrt[3]{2ξ_N - 1}).  $

Of course, this same warping function can be used to transform “uniform” jittered samples into nicely distributed samples with the desired density. 
当然，同样的扭曲函数可用于将“均匀”的抖动样本转换为具有所需密度的良好分布的样本。

If we have a random variable $α = (α_x, α_y)$ with two-dimensional density $(x, y)$ defined on $[x_{min}, x_{max}] × [y_{min}, y_{max}]$, then we need the two-dimensional distribution function:
如果我们有一个随机变量 $α = (α_x, α_y)$，其二维密度 $(x, y)$ 定义在 $[x_{min}, x_{max}] × [y_{min}, y_{ max}]$，那么我们需要二维分布函数：
$Probability(α_x < x\ and\ α_y < y) = F(x, y) = \int^y_{y_{min}}\int^x_{x_{min}}f(x', y')dμ(x', y').   \\$

We first choose an xi using the marginal distribution $F(x, y_{max})$ and then choose $y_i$ according to $F(x_i, y)/F(x_i, y_{max})$. If $f(x, y)$ is separable (expressible as $g(x)h(y)$), then the one-dimensional techniques can be used on each dimension.
我们首先使用边际分布 $F(x, y_{max})$ 选择 xi，然后根据 $F(x_i, y)/F(x_i, y_{max})$ 选择 $y_i$。 如果 $f(x, y)$ 是可分离的（可表示为 $g(x)h(y)$），则可以在每个维度上使用一维技术。

Returning to our earlier example, suppose we are sampling uniformly from the disk of radius $R$, so $p(r, φ) = 1/(πR^2)$. The two-dimensional distribution function is
回到我们之前的例子，假设我们从半径为 $R$ 的圆盘上均匀采样，因此 $p(r, φ) = 1/(πR^2)$。 二维分布函数为
$Probability(r < r_0\ and\ φ < φ_0) = F(r_0, φ_0) = \int^{φ_0}_0\int^{r_0}_{0} 
\frac{rdrdφ}{πR^2} = \frac{φr^2}{2πR^2}\\ $

This means that a canonical pair $(ξ_1, ξ_2)$ can be transformed to a uniform random point on the disk:
这意味着规范对 $(xi_1, xi_2)$ 可以转换为磁盘上的均匀随机点： 
$φ = 2πξ_1,\\
r = R\sqrt{ξ_2}.  $

This mapping is shown in Figure 14.7.
该映射如图 14.7 所示。
![Figure 14.7](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 14.7.png)
Figure 14.7. A mapping that takes equal area regions in the unit square to equal area regions in the disk.
图 14.7。 将单位正方形中的等面积区域映射到磁盘中的等面积区域。

To choose reflected ray directions for some realistic rendering applications, we choose points on the unit hemisphere according to the density:
为了为某些真实渲染应用选择反射光线方向，我们根据密度选择单位半球上的点：
$p(θ, φ) =  \frac{n+1}{2\pi} \cos^n θ  \\$

where n is a Phong-like exponent, $θ$ is the angle from the surface normal and $θ ∈ [0, π/2]$ (is on the upper hemisphere) and $φ$ is the azimuthal angle ($φ ∈ [0, 2π]$). The cumulative distribution function is
其中 n 是 Phong 型指数，$θ$ 是与表面法线的角度，$θ ∈ [0, π/2]$（位于上半球），$φ$ 是方位角（$φ ε [0, 2π]$)。 累积分布函数为
$$
P(θ, φ) = \int^φ_0\int^θ_0 p(θ', φ') \sin θ'dθ'dφ'. (14.8)
$$
The $\sin θ'$ term arises because, on the sphere, $dω = \cos θdθdφ$. When the marginal densities are found, $p$ (as expected) is separable, and we find that a $(ξ_1, ξ_2)$ pair of canonical random numbers can be transformed to a direction by
$\sin θ'$ 项的出现是因为在球面上，$dω = \cos θdθdφ$。 当找到边际密度时，$p$（如预期）是可分离的，并且我们发现$(Ψ_1，Ψ_2)$一对规范随机数可以转换为一个方向：
$θ = \arccos ((1 - ξ_1)^{\frac{1}{n+1}}) , \\
φ = 2πξ_2.  $

Again, a nice thing about this is that a set of jittered points on the unit square can be easily transformed to a set of jittered points on the hemisphere with the desired distribution. Note that if n is set to 1, we have a diffuse distribution, as is often needed.
同样，这样做的一个好处是，单位正方形上的一组抖动点可以轻松地转换为具有所需分布的半球上的一组抖动点。 请注意，如果 n 设置为 1，我们将得到扩散分布，这正是经常需要的。

Often we must map the point on the sphere into an appropriate direction with respect to a $uvw$ basis. To do this, we can first convert the angles to a unit vector $\vec{a}$:
通常我们必须将球体上的点映射到相对于 $uvw$ 基础的适当方向。 为此，我们首先可以将角度转换为单位向量 $\vec{a}$：
$\bold{a} = (\cos φ \sin θ, \sin φ \sin θ, \cos θ)  $

As an efficiency improvement, we can avoid taking trigonometric functions of inverse trigonometric functions (e.g., $\cos (\arccos θ)$). For example, when $n = 1$ (a diffuse distribution), the vector $\bold{a}$ simplifies to
为了提高效率，我们可以避免采用反三角函数的三角函数（例如，$\cos (\arccos θ)$）。 例如，当 $n = 1$ （扩散分布）时，向量 $\bold{a}$ 简化为
$\bold{a} = (\cos (2πξ_1)\sqrt{ξ_2}, \sin (2πξ_1)\sqrt{ξ_2}, \sqrt{1 - ξ_2})  $

### 14.4.2 Rejection 拒绝

A rejection method chooses points according to some simple distribution and rejects some of them that are in a more complex distribution. There are several scenarios where rejection is used, and we show some of these by example.
拒绝方法根据一些简单分布选择点并拒绝其中一些更复杂分布的点。 有多种使用拒绝的场景，我们通过示例展示其中一些场景。

Suppose we want uniform random points within the unit circle. We can first choose uniform random points $(x, y) ∈ [−1, 1]^2$ and reject those outside the circle. If the function r() returns a canonical random number, then the procedure is:
假设我们想要单位圆内均匀的随机点。 我们可以首先选择均匀的随机点 $(x, y) ∈ [−1, 1]^2$ 并拒绝那些在圆之外的点。 如果函数 r() 返回规范随机数，则过程为：

> done = false
> while (not done) do
> 	x = -1 + 2r()
> 	y = -1 + 2r()
> 	if $(x^2 + y^2 < 1)$ then
> 		done = true  

If we want a random number $x ∼ p$ and we know that $p : [a, b] \mapsto \R$, and that for all $x, p(x) < m$, then we can generate random points in the rectangle $[a, b] × [0, m]$ and take those where $y < p(x)$:
如果我们想要一个随机数 $x ∼ p$ 并且我们知道 $p : [a, b] \mapsto \R$，并且对于所有 $x，p(x) < m$，那么我们可以生成随机点 在矩形 $[a, b] × [0, m]$ 中并取 $y < p(x)$ 处的值：

> done = false
> while (not done) do
> 	x = a + r()(b - a)
> 	y = r()m
> 	if (y < p(x)) then
> 		done = true  

This same idea can be applied to take random points on the surface of a sphere. To pick a random unit vector with uniform directional distribution, we first pick a random point in the unit sphere and then treat that point as a direction vector by taking the unit vector in the same direction:
同样的想法可以应用于在球体表面上随机取点。 为了选取具有均匀方向分布的随机单位向量，我们首先在单位球体中选取一个随机点，然后通过在同一方向上取单位向量将该点视为方向向量：

> done = false
> while (not done) do
> 	x = -1 + 2r()
> 	y = -1 + 2r()
> 	z = -1 + 2r()
> 	if $((l = \sqrt{x^2 + y^2 + z^2}) < 1)$ then
> 		done = true
> x = x/l
> y = y/l
> z = z/l

Although the rejection method is usually simple to code, it is rarely compatible with stratification. For this reason, it tends to converge more slowly and should thus be used mainly for debugging, or in particularly difficult circumstances.
尽管拒绝方法通常编写起来很简单，但它很少与分层兼容。 因此，它往往收敛得更慢，因此应主要用于调试或特别困难的情况下。

### 14.4.3 Metropolis 大都会

The Metropolis method uses random mutations to produce a set of samples with a desired density. This concept is used extensively in the Metropolis Light Transport algorithm referenced in the chapter notes. Suppose we have a random point $x_0$ in a domain $S$. Further, suppose for any point $x$, we have a way to generate random $y ∼ p_x$. We use the marginal notation $p_x(y) ≡ p(x → y)$ to denote this density function. Now, suppose we let $x_1$ be a random point in $S$ selected with underlying density $p(x_0 → x_1)$. We generate $x_2$ with density $p(x_1 → x_0)$ and so on. In the limit, where we generate an infinite number of samples, it can be proved that the samples will have some underlying density determined by p regardless of the initial point $x_0$. 
Metropolis 方法使用随机突变来生成一组具有所需密度的样本。 这个概念在章节注释中引用的 Metropolis Light Transport 算法中被广泛使用。 假设我们在域 $S$ 中有一个随机点 $x_0$。 此外，假设对于任何点 $x$，我们有办法生成随机 $y ∼ p_x$。 我们使用边际符号 $p_x(y) ≡ p(x → y)$ 来表示该密度函数。 现在，假设我们让 $x_1$ 为 $S$ 中的一个随机点，选择的基础密度为 $p(x_0 → x_1)$。 我们生成密度为 $p(x_1 → x_0)$ 的 $x_2$ 等等。 在极限情况下，我们生成无限数量的样本，可以证明样本将具有由 p 确定的潜在密度，无论初始点 $x_0$ 如何。

Now, suppose we want to choose $p$ such that the underlying density of samples to which we converge is proportional to a function $f(x)$ where f is a nonnegative function with domain $S$. Further, suppose we can evaluate $f$, but we have little or no additional knowledge about its properties (such functions are common in graphics). Also, suppose we have the ability to make “transitions” from $x_i$ to $x_{i+1}$ with underlying density function $t(x_{i} → x_{i+1})$. To add flexibility, further suppose we add the potentially nonzero probability that $x_i$ transitions to itself, i.e., $x_{i+1} = x_i$. We phrase this as generating a potential candidate $y ∼ t(x_i → y)$ and “accepting” this candidate (i.e., $x_{i+1} = y$) with probability $a(x_i → y)$ and rejecting it (i.e., $x_{i+1} = x_i$) with probability $1−a(x_i → y)$. Note that the sequence $x_0, x_1, x_2, . . .$ will be a random set, but there will be some correlation among samples. They will still be suitable for Monte Carlo integration or density estimation, but analyzing the variance of those estimates is much more challenging. 
现在，假设我们要选择 $p$，使得我们收敛到的样本的基础密度与函数 $f(x)$ 成正比，其中 f 是域为 $S$ 的非负函数。 此外，假设我们可以评估 $f$，但我们对其属性知之甚少或根本不了解（此类函数在图形中很常见）。 另外，假设我们有能力使用底层密度函数 $t(x_{i} → x_{i+1})$ 进行从 $x_i$ 到 $x_{i+1}$ 的“转换”。 为了增加灵活性，进一步假设我们添加 $x_i$ 转换到自身的潜在非零概率，即 $x_{i+1} = x_i$。 我们将其表述为生成一个潜在候选 $y ∼ t(x_i → y)$ 并以 $a(x_i → y)$ 概率“接受”该候选（即 $x_{i+1} = y$）并拒绝 它（即 $x_{i+1} = x_i$）的概率为 $1−a(x_i → y)$。 请注意，序列 $x_0, x_1, x_2, . . .$ 将是一个随机集，但样本之间会有一些相关性。 它们仍然适用于蒙特卡罗积分或密度估计，但分析这些估计的方差更具挑战性。

Now, suppose we are given a transition function $t(x → y)$ and a function $f(x)$ of which we want to mimic the distribution, can we use $a(y → x)$ such that the points are distributed in the shape of $f$ ? Or more precisely,
现在，假设我们有一个转换函数 $t(x → y)$ 和一个我们想要模拟分布的函数 $f(x)$，我们可以使用 $a(y → x)$ 使得点 以 $f$ 的形式分布？ 或者更准确地说，
${x0, x1, x2, . . .} ∼ \frac{f}{\int_sf}\\$

It turns out this can be forced by making sure the xi are stationary in some strong sense. If you visualize a huge collection of sample points $x$, you want the “flow” between two points to be the same in each direction. If we assume the density of points near $x$ and $y$ are proportional to $f(x)$ and $f(y)$, respectively, then the flow in the two directions should be the same:
事实证明，这可以通过确保 xi 在某种强意义上是静止的来强制实现。 如果您可视化大量样本点 $x$，您希望两点之间的“流量”在每个方向上都相同。 如果我们假设$x$和$y$附近的点的密度分别与$f(x)$和$f(y)$成正比，那么两个方向上的流量应该是相同的：
$flow(x → y) = kf(x)t(x → y)a(x → y), \\
flow(y → x) = kf(y)t(y → x)a(y → x),  $

where $k$ is some positive constant. Setting these two flows constant gives a constraint on $a$: 
其中 $k$ 是某个正常数。 将这两个流设置为常数会给 $a$ 带来约束：
$\frac{a(y → x)}{a(x → y)} = \frac{f(x)t(x → y)}{f(y)t(y → x)}\\$

Thus, if either $a(y → x)$ or $a(x → y)$ is known, so is the other. Making them larger improves the chance of acceptance, so the usual technique is to set the larger of the two to 1. 
因此，如果 $a(y → x)$ 或 $a(x → y)$ 已知，则另一个也已知。 使它们更大可以提高接受的机会，因此通常的技术是将两者中较大的设置为 1。

A difficulty in using the Metropolis sample generation technique is that it is hard to estimate how many points are needed before the set of points is “good.” Things are accelerated if the first n points are discarded, although choosing $n$ wisely is nontrivial.
使用 Metropolis 样本生成技术的一个困难在于，很难估计在点集“良好”之前需要多少个点。 如果前 n 个点被丢弃，事情就会加速，尽管明智地选择 $n$ 是很重要的。

### 14.4.4 Example: Choosing Random Lines in the Square 示例：在正方形中选择随机线

As an example of the full process of designing a sampling strategy, consider the problem of finding random lines that intersect the unit square $[0, 1]^2$. We want this process to be fair; that is, we would like the lines to be uniformly distributed within the square. Intuitively, we can see that there is some subtlety to this problem; there are “more” lines at an oblique angle than in horizontal or vertical directions. This is because the cross section of the square is not uniform.
作为设计采样策略的完整过程的示例，请考虑查找与单位正方形 $[0, 1]^2$ 相交的随机线的问题。 我们希望这个过程是公平的； 也就是说，我们希望线条均匀分布在正方形内。 直观上，我们可以看出这个问题有一些微妙之处； 倾斜方向的线比水平或垂直方向的线“更多”。 这是因为正方形的横截面不均匀。

Our first goal is to find a function-inversion method, if one exists, and then to fall back on rejection or Metropolis if that fails. This is because we would like to have stratified samples in line space. We try using normal coordinates first, because the problem of choosing random lines in the square is just the problem of finding uniform random points in whatever part of $(r, θ)$ space corresponds to lines in the square.
我们的第一个目标是找到一种函数反转方法（如果存在），然后在失败时求助于拒绝或 Metropolis。 这是因为我们希望在行空间中有分层样本。 我们首先尝试使用法线坐标，因为在正方形中选择随机线的问题就是在 $(r, θ)$ 空间的任意部分中找到与正方形中的线相对应的均匀随机点的问题。

Consider the region where $−π/2 < θ < 0$. What values of r correspond to lines that hit the square? For those angles, $r < cos θ$ are all the lines that hit the square as shown in Figure 14.8. Similar reasoning in the other four quadrants finds the region in $(r, θ)$ space that must be sampled, as shown in Figure 14.9. The equation of the boundary of that region $r_{max}(θ)$ is
考虑 $−π/2 < θ < 0$ 的区域。 r 的什么值对应于击中正方形的线？ 对于这些角度，$r < cos θ$ 是击中正方形的所有线，如图 14.8 所示。 其他四个象限中的类似推理找到了$(r,θ)$空间中必须采样的区域，如图14.9所示。 该区域的边界方程 $r_{max}(θ)$ 为
![Figure 14.8](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 14.8.png)
Figure 14.8. The largest distance $r$ corresponds to a line hitting the square for $θ ∈ [ − π/2, 0 ]$. Because the square has sidelength one, $r = cos θ$.
图 14.8。 最大距离 $r$ 对应于 $θ ∈ [ − π/2, 0 ]$ 的正方形的一条线。 因为正方形的边长为 1，所以 $r = cos θ$。

![Figure 14.9](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 14.9.png)
Figure 14.9. The maximum radius for lines hitting the unit square $[0,1]^2$ as a function of $θ$.  
图 14.9。 到达单位正方形 $[0,1]^2$ 的线的最大半径作为 $θ$ 的函数。
$$
r_{max}(θ) = \begin{cases}
0\ \ \ \ \ \  \ \ \ \ \ \ \  \ if\ θ ∈ [−π, −π/2 ], \\
\cos θ\ \ \ \ \ \ \ \  if\ θ ∈ [−π/2 , 0], \\
\sqrt{2}\cos(θ − π/4) \ \ \ \  \ \ if\ θ ∈ [0, π/2 ], \\
\sin θ\ \ \ \  \ \ \ \ \  if\ θ ∈ [ π/2 , π].
\end{cases}
$$
Because the region under $r_{max}(θ)$ is a simple function bounded below by $r = 0$, we can sample it by first choosing $θ$ according to the density function:
因为 $r_{max}(θ)$ 下的区域是一个简单函数，其边界为 $r = 0$，所以我们可以通过首先根据密度函数选择 $θ$ 来对其进行采样：
$p(θ) = \frac{r_{max}(θ)}{\int^π_{-π}r_{max}(θ)dθ}\\$

The denominator here is 4. Now, we can compute the cumulative probability distribution function: 
这里的分母是 4。现在，我们可以计算累积概率分布函数：
$P (θ) =  \begin{cases}
0\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \  \ \ \ \ \ \ \ \ \ \ \ \ \ \ if\ θ ∈ [-π, - π/2 ], \\
(1 + sin θ)/4\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ if\ θ ∈ [-π/2 , 0], \\
(1 + \frac{\sqrt{2}}{2} sin(θ - π/4 ))/2\ \ \ if\ θ ∈ [0, π/2 ], \\
(3 - cos θ)/4\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ if\ θ ∈ [ π/2 , π].  
\end{cases}$

We can invert this by manipulating $ξ_1 = P(θ)$ into the form $θ = g(ξ_1)$. This yields
我们可以通过将 $Σ_1 = P(θ)$ 转换为 $θ = g(Σ_1)$ 的形式来反转它。 这产生
$θ = \begin{cases}
\arcsin(4ξ_1 - 1)\ \ \ \ \ \ if\ ξ_1 < \frac{1}{4}, \\
\arcsin(\frac{\sqrt{2}}{2}(2ξ_1 - 1)) + \frac{\pi}{4}\ \ \ \ \ if\ ξ_1 ∈ [\frac{1}{4}, \frac{3}{4}], \\
\arccos(3 - 4ξ_1)\ \ \ \ \ \ \ \ \ \  if ξ_1 > \frac{3}{4}.  
\end{cases}$

Once we have $θ$, then $r$ is simply: 
一旦我们有了 $θ$，那么 $r$ 就很简单：
$r = ξ_2r_{max}(θ)  $

As discussed earlier, there are many parameterizations of the line, and each has an associated “fair” measure. We can generate random lines in any of these spaces as well. For example, in slope-intercept space, the region that hits the square is shown in Figure 14.10. By similar reasoning to the normal space, the density function for the slope is
如前所述，生产线有许多参数化，每个参数化都有一个关联的“公平”度量。 我们也可以在任何这些空间中生成随机线。 例如，在斜截空间中，碰到正方形的区域如图 14.10 所示。 通过与正常空间类似的推理，斜率的密度函数为
$p(m) =  \frac{1+|m|}{4}\\$

![Figure 14.10](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 14.10.png)
Figure 14.10. The region of $(m,b)$ space that contains lines that intersect the unit square $[0,1]^2$.
图 14.10。 $(m,b)$ 空间的区域，包含与单位正方形 $[0,1]^2$ 相交的线。 

with respect to the differential measure
关于差分测量
$dμ = \frac{dm}{(1 + m^2)^{\frac{3}{2}}}\\$

This gives rise to the cumulative distribution function:
这就产生了累积分布函数：
$P(m) = \begin{cases} 
\frac{1}{4} + \frac{m+1}{4\sqrt{1+m^2}} \ \ \ \ if\ m < 0 \\ 
\frac{3}{4} + \frac{m-1}{4\sqrt{1+m^2}} \ \ \ \ if\ m ≥ 0 \\ 
\end{cases}$

These can be inverted by solving two quadratic equations. Given an m generated using $ξ_1$, we then have
这些可以通过求解两个二次方程来反转。 给定使用$ xi_1 $生成的m，我们有
$b =  \begin{cases} 
(1 + m)ξ_2 \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ if\ ξ < \frac{1}{2} \\
-m + (1 + m) ξ_2 \ \ \ \ \ \ \ \ otherwise
\end{cases}$

This is not a better way than using normal coordinates; it is just an alternative way.
这并不是比使用普通坐标更好的方法； 这只是一种替代方式。 

## Frequently Asked Questions 经常问的问题

### This chapter discussed probability but not statistics. What is the distinction? 本章讨论概率但不讨论统计。 有什么区别？

Probability is the study of how likely an event is. Statistics infers characteristics of large, but finite, populations of random variables. In that sense, statistics could be viewed as a specific type of applied probability. 
概率是对事件发生可能性的研究。 统计推断出大量但有限的随机变量群体的特征。 从这个意义上说，统计学可以被视为一种特定类型的应用概率。

### Is Metropolis sampling the same as the Metropolis Light Transport Algorithm? Metropolis 采样与 Metropolis 轻传输算法相同吗？

No. The Metropolis Light Transport (Veach & Guibas, 1997) algorithm uses Metropolis sampling as part of its procedure, but it is specifically for rendering, and it has other steps as well. 
不会。Metropolis Light Transport（Veach & Guibas，1997）算法使用 Metropolis 采样作为其过程的一部分，但它专门用于渲染，并且还有其他步骤。

## Notes 注释

The classic reference for geometric probability is Geometric Probability (Solomon, 1978). Another method for picking random edges in a square is given in Random–Edge Discrepancy of Supersampling Patterns (Dobkin & Mitchell, 1993). More information on quasi-Monte Carlo methods for graphics can be found in Efficient Multidimensional Sampling (Kollig & Keller, 2002). Three classic and very readable books on Monte Carlo methods are Monte Carlo Methods (Hammersley & Handscomb, 1964), Monte Carlo Methods, Basics (Kalos & Whitlock, 1986), and The Monte Carlo Method (Sobel, Stone, & Messer, 1975).
几何概率的经典参考文献是《几何概率》（Solomon，1978）。 超级采样模式的随机边缘差异（Dobkin & Mitchell，1993）中给出了另一种在正方形中选取随机边缘的方法。 有关图形的准蒙特卡罗方法的更多信息可以在高效多维采样（Kollig & Keller，2002）中找到。 关于蒙特卡罗方法的三本经典且非常可读的书籍是《蒙特卡罗方法》（Hammersley & Handscomb，1964 年）、《蒙特卡罗方法基础》（Kalos & Whitlock，1986 年）和《蒙特卡罗方法》（Sobel、Stone 和 Messer，1975 年） 。

## Exercises 练习

1. What is the average value of the function $xyz$ in the unit cube $(x, y, z) ∈ [0, 1]^3$? 
   单位立方体$(x, y, z) ∈ [0, 1]^3$中函数$xyz$的平均值是多少？

2. What is the average value of $r$ on the unit-radius disk: $(r, φ) ∈ [0, 1] × [0, 2π)$?
   单位半径圆盘上 $r$ 的平均值是多少：$(r, φ) ∈ [0, 1] × [0, 2π)$？
3. Show that the uniform mapping of canonical random points $(ξ_1, ξ_2)$ to the barycentric coordinates of any triangle is: $β = 1 - \sqrt{1 - ξ_1}$, and $γ = (1 - u)ξ_2$.
   证明正则随机点 $(ξ_1, ξ_2)$ 到任意三角形重心坐标的均匀映射为：$β = 1 - \sqrt{1 - ξ_1}$，且 $γ = (1 - u)ξ_2$。
4. What is the average length of a line inside the unit square? Verify your answer by generating ten million random lines in the unit square and averaging their lengths.
   单位正方形内的线的平均长度是多少？ 通过在单位正方形中生成一千万条随机线并平均它们的长度来验证您的答案。
5. What is the average length of a line inside the unit cube? Verify your answer by generating ten million random lines in the unit cube and averaging their lengths.
   单位立方体内的一条线的平均长度是多少？ 通过在单位立方体中生成一千万条随机线并平均它们的长度来验证您的答案。
6. Show from the definition of variance that $V(x) = E(x^2) - [E(x)]^2$ . 
   根据方差的定义证明 $V(x) = E(x^2) - [E(x)]^2$ 。