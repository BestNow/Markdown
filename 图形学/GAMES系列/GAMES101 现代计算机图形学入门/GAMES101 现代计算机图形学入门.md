# 课程网址

https://www.bilibili.com/video/BV1X7411F744/?spm_id_from=333.337.search-card.all.click&vd_source=1b732552b2e7da5edcc8398add8181dd

# 预备知识

信号学、光学、[虎书](.\..\..\..\..\..\书籍\游戏相关\计算机图形学\Fundamentals of Computer Graphics 4th.pdf)

# Overview

## What is Computer Graphics？

computer graphics The use of computers to synthesize and manipulate visual information.
计算机图形学使用计算机来合成和处理视觉信息。

## Why study Computer Graphics?

- Applications	应用程序
  Video Game、Movies、Animations、Design、Visualization、Virtual Reality、Digital Illustration、Simulation、Graphical User Interfaces、Typography
  视频游戏、电影、动画、设计、可视化、虚拟现实、数字插图、仿真、图形用户界面、排版

  > The Quick Brown Over Fox Jumps The Lazy Dog

- Fundamental Intellectual Challenges 基本智力挑战
  Creates and interacts with realistic virtual world 创造并与现实的虚拟世界互动
  Requires understanding of all aspects of physical world 需要了解物质世界的方方面面
  New computing methods, displays, technologies 新的计算方法、显示器和技术

- Technical Challenges 技术挑战
  Math of (perspective) projections, curves, surfaces (透视)投影、曲线、曲面的数学
  Physics of lighting and shading 物理照明和阴影
  Representing / operating shapes in 3D 在3D中表示/操作形状
  Animation / simulation 动画/模拟
  ~~3D graphics software programming and hardware~~ 三维图形的软件编程和硬件设计

## Course Topics

- Rasterization 光栅化
  Project geometry primitives (3D triangles / polygons) onto the screen
  将几何原语(3D三角形/多边形)投影到屏幕上
  Break projected primitives into fragments (pixels) 
  将投影基元分解为片段(像素)
  Gold standard in Video Games (Real-time Applications) 
  电子游戏的黄金标准(实时应用)

- Curves and Meshes 曲线和网格
  How to represent geometry in Computer Graphics
  如何在计算机图形学中表示几何

- Ray Tracing 射线跟踪
  Shoot rays from the camera though each pixel 从相机发射光线通过每个像素

  - Calculate intersection and shading 计算交点和阴影
  - Continue to bounce the rays till they hit light sources 继续反射光线，直到它们击中光源

  Gold standard in Animations / Movies (Offline Applications)  动画/电影的黄金标准(离线应用程序)

- Animation / Simulation 动画/模拟
  Key frame Animation 关键帧动画 
  Mass-spring System 质量弹簧系统

## Course Logistics 

课程组织

GAMES101 is NOT about GAMES101**不是关于**

- Using OpenGL / DirectX / Vulkan  使用OpenGL / DirectX / Vulkan 
- The syntax of Shaders 着色器的语法
- We learn Graphics， not Graphics APIs! 我们学习图形，而不是图形api ! 
- After this course.you'll be able to learn theseby yourself (l promise) 在这门课之后。你可以自己学会这些(我保证)
- 3D modeling using Maya / 3DS MAX / Bender, orVR / game development using Unity / Unreal Engine(where can Ilearn them?) 使用Maya / 3DS MAX / Bender进行3D建模，或使用Unity /虚幻引擎进行vr /游戏开发(我在哪里可以学到它们?)
- Computer Vision / Deep Learning topics, e.g.XYZ-GAN(where can i learn them?) 计算机视觉/深度学习主题，例如xyz - gan(我可以在哪里学习它们?)

### The difference between computer graphics and computer vision

计算机图形学和计算机视觉的区别

作者自己的认知：

![](.\Images\ModelAndImage.png)

No clear boundaries 没有明确的界限 
And I can't define Computer Graphics 我无法定义计算机图形学

### General Information 

一般信息

Modern Course 现代课程
	Comprehensive but without hardware programming 全面但没有硬件编程
	Pace / contents subject to change 进度/内容可能会有所变化

Course Website 课程网站
	http://www.cs.ucsb.edu/-linggi/teaching/games101.html
	Has all the needed information 所有需要的信息都有
	Syllabus, slides, reading materials, etc. 教学大纲、幻灯片、阅读材料等。

### References

<img src=".\Images\Fundamentals of Computer Graphics.png" style="zoom:50%;" align="left"/>



# Review of Linear Algebra

线性代数回顾

## Graphics’ Dependencies

图形的依赖关系

- Basic mathematics 基本的数学
  - Linear algebra, calculus, statistics 线性代数，微积分，统计学
- Basic physics 基础物理
  - Optics,Mechanics 光学、力学
- Misc 混杂的
  - Signal processing 信号处理
  - Numerical analysis 数值分析
- a bit of aesthetics 一点点美学



## Vector

向量

- Usually written as $\stackrel{\rightarrow}{a}$ or in bold **a**
- Or using start and end points $\overrightarrow{AB}$ = B - A
- Direction and length 方向和长度
- No absolute starting position 没有绝对起始位置

<img src=".\Images\Vecotrs.png" alt="Vecotrs" style="zoom:50%;" />

### Vector Normalization

- Magnitude (length) of a vector written as $||\vec{a}||$

- Unit vector

  - A vector with magnitude of 1 一个大小为1的向量

  - Finding the unit vector of a vector (normalization):   $\hat{a} = \vec{a} / ||\vec{a}||$ 求向量的单位向量(归一化)
  - Used to represent directions 用于表示方向

### Vector Addition

- Geometrically: Parallelogram law & Triangle law 几何:平行四边形定律和三角形定律

- Algebraically: Simply add coordinates 代数:简单地添加坐标

  <img src=".\Images\Vector Addition.png" alt="Vector Addition" style="zoom:67%;" />

### Cartesian Coordinates

笛卡儿坐标

X and Y can be any (usually orthogonal unit) vectors
X和Y可以是任意(通常是正交的单位)向量
$$
A = \begin{pmatrix}x \\y \\\end{pmatrix} \ \ \ \
A^T = \begin{pmatrix}x & y \\\end{pmatrix} \ \ \ \
||A|| = \sqrt{x^2 + y^2}
$$
<img src=".\Images\Cartesian Coordinates.png" alt="Cartesian Coordinates" style="zoom:67%;" />

### Vector Multiplication

- Dot product 点乘
- Cross product 叉乘
- Orthonormal bases and coordinate frames 标准正交基和坐标系

#### Dot product

向量点乘是一个数

用法：算出两个向量之间的夹角

<img src=".\Images\Dot Product.png" alt="Dot Product" style="zoom:33%;" />
$$
\vec{a} \cdot \vec{b} = ||\vec{a}||\ ||\vec{b}||\cos{\theta} \ \ \\
\cos{\theta} = \frac{ \vec{a} \cdot \vec{b}} { ||\vec{a}||\ ||\vec{b}||} \\ 
For\ Unit\ Vector:\cos{\theta} = \vec{a} \cdot \vec{b} \\
$$

##### Dot Product in CartesianCoordinates

笛卡尔坐标下的点积

Component-wise multiplication, then adding up 组件式乘法，然后相加
$$
2D:\vec{a} \cdot \vec{b} = 
	\begin{pmatrix}x_a \\y_a \\\end{pmatrix} 
	\cdot 
	\begin{pmatrix}x_b \\y_b \\\end{pmatrix}
	= x_ax_b + y_ay_b \\ 
	\\
3D:\vec{a} \cdot \vec{b} = \begin{pmatrix}x_a \\y_a \\z_a \\\end{pmatrix} 
	\cdot 
	\begin{pmatrix}x_b \\y_b \\z_b \\\end{pmatrix}
	= x_ax_b + y_ay_b + z_az_b \\
$$

##### Dot Product in Graphics

- Find angle between two vectors(e.g. cosine of angle between light source and surface)
  找出两个向量之间的夹角(例如:光源与表面夹角余弦)
- Finding projection of one vector on another
  求一个向量在另一个向量上的投影

Dot Product for Projection 投影的点积

<img src=".\Images\Dot Product for Projection.png" alt="Dot Product for Projection" style="zoom:50%;" />

$\vec{b}_\perp$：projection of  $\vec{b}$ onto $\vec{a}$

​	$\vec{b}$ must be along $\vec{a}$ (or along $\hat{a}$)
​		$\vec{b}_\perp = k\hat{a} $
​	What's its magnitude k? 大小k是多少?
​		$k = ||\vec{b}_\perp|| = ||\vec{b}||\cos{\theta}$

- Measure how close two directions are
  测量两个方向的距离
- Decompose a vector
  分解向量
- Determine forward /backward
  确定向前/向后

<img src=".\Images\Determine Forward Backward.png" alt="Determine Forward Backward" style="zoom:50%;" />

#### Cross product

<img src=".\Images\Cross Product.png" alt="Cross Product" style="zoom:50%;" />

- Cross product is orthogonal to two initial vectors
  向量积与两个初始向量正交
- Direction determined by right-hand rule
  方向由右手定则(右手顺时针旋转)决定
- Useful in constructing coordinate systems (later)
  用于构造坐标系统(稍后)

$$
\vec{a} \times {\vec{b}} = \begin{pmatrix}
	y_bz_b - y_bz_a \\
	z_ax_b - x_az_b \\
	x_ay_b - y_ax_b
\end{pmatrix} \\

\vec{a} \times {\vec{b}} = A\vec{b} = \begin{pmatrix}
	0 & -z_a & y_a \\
	z_a & 0 & -x_a \\
	-y_a & x_a & 0
\end{pmatrix}
\begin{pmatrix}
x_b \\
y_b \\
z_b
\end{pmatrix}
$$

##### Cross Product in Graphics

- Determine left / right 确定左/右
- Determine inside / outside 确定内/外

<img src=".\Images\Cross Product in Graphics.png" alt="Cross" style="zoom: 50%;" />

左图在右手坐标系下，使用顺时针旋转，$\vec{b}$ 在$\vec{a}$的左侧，$\vec{a} \times \vec{b} > 0$
右图，$\overrightarrow{AB} \times \overrightarrow{AP}、\overrightarrow{BC} \times \overrightarrow{BP}、\overrightarrow{CA} \times \overrightarrow{CP}$，如果全为正/负，则P点在内部，否则在外部



#### Orthonormal bases and coordinate frames 

- lmportant for representing points, positions, locations 对于表示点、位置和位置很重要
- Often, many sets of coordinate systems 通常，有许多套坐标系统
  -  Global, local, world, model, parts of model (headhands,...)
- Critical issue is transforming between these systems/bases 
  关键问题是在这些系统之间进行转换/基础坐标系
  - A topic for next week

##### Orthonormal Coordinate Frames

Any set of 3 vectors (in 3D) that
$$
||\vec{u}|| = ||\vec{v}|| = ||\vec{w}|| = 1 \\
\vec{u} \cdot \vec{v} = \vec{v} \cdot \vec{w} = \vec{u} \cdot \vec{w} = 0 \\
\vec{w} = \vec{u}  \vec{v} \ \ \  (right-handed) \\
any\ vector\ \vec{p}: 
\vec{p} = (\vec{p} \cdot \vec{u})\vec{u} + (\vec{p} \cdot \vec{v})\vec{v} + (\vec{p} \cdot \vec{w})\vec{w}
$$


## Matrices

- Magical 2D arrays that haunt in every CS course 每个CS课程中都会出现的神奇2D数组
- In Graphics, pervasively used to represent transformations 在图形学中，普遍用于表示转换
  - Translation, rotation, shear, scale(more details in the next lecture) 
    平移，旋转，剪切，缩放(更多细节在下一讲)

### What is a matrix

Array of numbers (m x n = m rows, n columns) 数字数组(m x n = m行，n列)
$$
\begin{pmatrix}
	0 & -z_a & y_a \\
	z_a & 0 & -x_a \\
	-y_a & x_a & 0
\end{pmatrix}
$$
Addition and multiplication by a scalar are trivial:element by element
一个标量的加法和乘法是微不足道的:一个元素一个元素

### Matrix-Matrix Multiplication

#(number of) columns in A must = # rows in B：(MxN)(NxP) = (MxP)
$$
\begin{pmatrix}
	1 & 3 \\
	5 & 2 \\
	0 & 4
\end{pmatrix}
\begin{pmatrix}
	3 & 6 & 9 & 4 \\
	2 & 7 & 8 & 3
\end{pmatrix}
$$

#### Properties

- Non-commutative
  (AB and BA are different in general)
- Associative and distributive
  - (AB)C=A(BC)
  - A(B + C) = AB + AC
  - (A + B)C = AC + BC

Treat vector as a column matrix (mx1) 将向量视为列矩阵(mx1)
Key for transforming points (next lecture) 变换点的关键



### Transpose of a Matrix

- Switch rows and columns (ij -> ji)
  $$
  \begin{pmatrix}
  	1 & 2 \\
  	3 & 4 \\
  	5 & 6
  \end{pmatrix}^T = 
  \begin{pmatrix}
  	1 & 3 & 5 \\
  	2 & 4 & 6 
  \end{pmatrix}
  $$

- Property
  $$
  (AB)^T = B^TA^T
  $$

### ldentity Matrix and Inverses

$$
I_{3 \times 3} = \begin{pmatrix}
	1 & 0 & 0 \\
	0 & 1 & 0 \\
    0 & 0 & 1
\end{pmatrix} \\ 
AA^{-1} = A^{-1}A = I \\
(AB)^{-1} = B^{-1}A^{-1}
$$



# Transformation

## 2D Transforms

### Linear Transforms

#### Scale

<img src=".\Images\2DScale.png" alt="2DScale" style="zoom:50%;" />
$$
\begin{cases}
x' = sx \\
y' = sy
\end{cases} 
\ \ \ => \ \ \ 
\begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}s & 0\\0 & s\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix}
$$

#### Scale(Non-Uniform)

<img src=".\Images\2DScaleNonUniform.png" alt="2DScaleNonUniform" style="zoom:50%;" />
$$
\begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}s_x & 0\\0 & s_y\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix}
$$

#### Reflection Matrix

<img src=".\Images\Reflection Matrix.png" style="zoom:50%;" />
$$
\begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}-1& 0\\0 & 1\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix}
$$

#### Shear Matrix

<img src=".\Images\2D Shear Matrix.png" alt="2D Shear Matrix" style="zoom:50%;" />
$$
\begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}1 & a\\0 & 1\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix}
$$

#### Rotate

(about the origin (0, 0), CCW by default) 
(关于原点(0,0)，默认为CCW(反时针方向))

<img src=".\Images\2D Rotate.png" alt="2D Rotate" style="zoom:50%;" />
$$
R_\theta
	= \begin{bmatrix}cos\theta & -sin\theta\\sin\theta & cos\theta\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix}
$$
**Linear Transforms = Matrices (of the same dimension)**
**线性变换=矩阵(相同维数)**
$$
\ \begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}a & b\\c & d\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix} \\
		x' = Mx
$$

### Homogenous Coordinates

Add a third coordinate (w-coordinate)
添加第三个坐标(w坐标)
$$
2D\ point = (x, y, 1)^T \\
2D\ vector = (x, y, 0)^T
$$
Valid operation if w-coordinate of result is 1 or 0

- vector + vector = vector
- point - point = vector
- point + vector = point
- point + point = center of two point


$$
In\ homogeneous\ coordinates, \\
\begin{pmatrix}x \\y \\w \\\end{pmatrix}\ is\ the\ 2D\ point
\begin{pmatrix}x/w \\y/w \\1 \\\end{pmatrix}, 
w ≠ 0
$$

#### Translation

平移

<img src=".\Images\2D Traanslation.png" alt="2D Traanslation" style="zoom:50%;" />

Translation cannot be represented in matrix form
平移不能用2维矩阵的形式表示
$$
\ \begin{bmatrix}x' \\y'\end{bmatrix} 
	= \begin{bmatrix}a & b\\c & d\end{bmatrix}
		\begin{bmatrix}x \\y \end{bmatrix} 
		+ \begin{bmatrix}t_x \\t_y \end{bmatrix}
$$
Matrix representation of translations
平移的矩阵表示
$$
\begin{pmatrix}x' \\y' \\z' \\\end{pmatrix}
= \begin{pmatrix}1 & 0 & t_x \\0 & 1 & t_y \\0 & 0 & 1 \\\end{pmatrix} \cdot 
\begin{pmatrix}x \\y \\1 \\\end{pmatrix}
= \begin{pmatrix}x + t_x \\y +t_y \\1 \\\end{pmatrix}
$$

#### Scale

$$
S(s_x, s_y)
=  \begin{pmatrix}s_x & 0 & 0 \\0 & s_y & 0 \\0 & 0 & 1 \\\end{pmatrix}
$$

#### Rotation

$$
R(\alpha)
=  \begin{pmatrix}cos\alpha & -sin\alpha & 0 \\sin\alpha & cos\alpha & 0 \\0 & 0 & 1 \\\end{pmatrix}
$$

#### Translation

$$
T(t_x, t_y) = \begin{pmatrix}1 & 0 & t_x \\0  & 1 & t_y \\0 & 0 & 1 \\\end{pmatrix}
$$

### Inverse Transform

$M^{-1}$ is the inverse of transform M in both a matrix and geometric sense

<img src=".\Images\2D Inverse Transform.png" alt="2D Inverse Transform" style="zoom:50%;" />

### Composite Transform

<img src=".\Images\Translate Then Rotate.png" alt="Translate Then Rotate" style="zoom:50%;" />

<img src=".\Images\Rotate Then Translate.png" alt="Translate Then Rotate" style="zoom:50%;" />

Matrix multiplication is not commutative

Note that matrices are applied right to left：
$$
T_{(1, 0)} \cdot R_{45} \begin{bmatrix}x \\y \\1 \\\end{bmatrix} = 
\begin{bmatrix}1 & 0 & 1 \\0 & 1 & 0 \\0 & 0 & 1 \\\end{bmatrix}
\begin{bmatrix}cos45° & -sin45° & 0 \\sin45° & cos45° & 0 \\0 & 0 & 1 \\\end{bmatrix}
 \begin{bmatrix}x \\y \\1 \\\end{bmatrix}
$$

## 3D Transforms

Use homogeneous coordinates again:
$$
3D\ point = (x, y, z, 1)^T \\
3D\ vector = (x, y, z, 0)^T
$$
Use 4x4 matrices for affine transformations:
$$
\begin{pmatrix}x' \\y' \\z' \\ 1 \\\end{pmatrix} 
= \begin{pmatrix}
	a & b & c & t_x \\
	d & e & f & t_y \\
	g & h & i & t_z \\
    0 & 0 & 0 & 1\\
\end{pmatrix}\cdot
\begin{pmatrix}x \\y \\z \\1 \\\end{pmatrix}
$$

### Scale

$$
S(s_x, s_y, s_z) = \begin{pmatrix}
	s_x & 0 & 0 & 0 \\
	0 & s_y & 0 & 0 \\
	0 & 0 & s_z & 0 \\
    0 & 0 & 0 & 1\\
\end{pmatrix}
$$

### Translation

$$
T(t_x, t_y, t_z) = \begin{pmatrix}
	1 & 0 & 0 & t_x \\
	0 & 1 & 0 & t_y \\
	0 & 0 & 1 & t_z \\
    0 & 0 & 0 & 1\\
\end{pmatrix}
$$

### Rotation

$$
R_x(\alpha) = \begin{pmatrix}
	1 & 0 & 0 & 0 \\
	0 & cos\alpha & -sin\alpha & 0 \\
	0 & sin\alpha & cos\alpha & 0 \\
    0 & 0 & 0 & 1\\
\end{pmatrix} \\
R_y(\alpha) = \begin{pmatrix}
	cos\alpha & 0 & sin\alpha & 0 \\
	0 & 1 & 0 & 0 \\
	-sin\alpha & 0 & cos\alpha & 0 \\
    0 & 0 & 0 & 1\\
\end{pmatrix} \\
R_z(\alpha) = \begin{pmatrix}
	cos\alpha & -sin\alpha & 0 & 0 \\
	sin\alpha & cos\alpha & 0 & 0 \\
	0 & 0 & 1 & 0 \\
    0 & 0 & 0 & 1\\
\end{pmatrix} \\
$$

#### Euler angles

Compose any 3D rotation from $R_x, R_y, R_z$?
$R_{xyz}(\alpha, \beta,\gamma) = R_x(\alpha)R_y(\beta)R_z(\gamma)$

- So-called Euler angles
- Often used in flight simulators: roll, pitch, yaw

#### Rodrigues Rotation Fermula ??

罗德里格斯旋转公式

Rotation by angle a around axis n
$$
R(\bold{n},\alpha) = cos(\alpha)\bold{I} + (1 - cos(\alpha))\bold{nn}^T + sin(\alpha) \\
N = \begin{pmatrix}
	0 & -n_z & n_y \\
	n_z & 0 & -n_x \\
	-n_y & n_x & 0 \\
\end{pmatrix}
$$

## View/Camera Transformation

### What is view transformation?

Think about how to take a photo

  - Find a good place and arrange people (model transformation)
  - Find a good “angle” to put the camera (view transformation)
  - Cheese! (projection transformation)

### How to perform view transformation?

Define the camera first

- Position $\stackrel{\rightarrow}{e}$
- Look-at / gaze direction $\hat{g}$
- Up direction $\hat{t}$   (assuming perp. to look-at)

<img src=".\Images\View Transformation.png" alt="View Transformation" style="zoom:50%;" />

- Key observation
  lf the camera and all objects move together, the“photo” will be the same

<img src=".\Images\View Transformation2.png" alt="View Transformation" style="zoom:50%;" />

- How about that we always transform the camera to
  - The origin, up at Y, look at -Z
  - And transform the objects along with the camera

<img src=".\Images\View Transformation3.png" alt="View Transformation" style="zoom:50%;" />

- Transform the camera by $M_{view}$

  - So it's located at the origin, up at Y look at -Z

    <img src=".\Images\View Transformation4.png" alt="View Transformation" style="zoom:50%;" />

- $M_{view}$ in math desc?
  - Translates e to origin
  - Rotates g to -Z
  - Rotates t to Y
  - Rotates (g x t) To X
  - Difficult to write!

<img src=".\Images\View Transformation5.png" alt="View Transformation" style="zoom:50%;" />

- $M_{view}$ in math

  - Let's write $M_{view} = R_{view}T_{view}$

  - Translate e to origin
    $$
    T_{view} = \begin{bmatrix}
    	1 & 0 & 0 & -x_e \\
    	0 & 1 & 0 & -y_e \\
    	0 & 0 & 1 & -z_e \\ 
    	0 & 0 & 0 & 1 \\\end{bmatrix}
    $$

  - Rotate g to -Z, t to Y, (g x t) To X

  - Consider its inverse rotation: X to (g x t), Y to t, Z to -g

$$
R^{-1}_{view} = \begin{bmatrix}
	x_{\hat{g} \cross \hat{t}} & x_t & x_{-g} & 0 \\
	y_{\hat{g} \cross \hat{t}} & y_t & y_{-g} & 0 \\
	z_{\hat{g} \cross \hat{t}} & z_t & z_{-g} & 0 \\ 
	0 & 0 & 0 & 1 \\\end{bmatrix} \\
R_{view} = \begin{bmatrix}
	x_{\hat{g} \cross \hat{t}} & y_{\hat{g} \cross \hat{t}} & z_{\hat{g} \cross \hat{t}}  & 0 \\
	x_t & y_t & z_t & 0 \\
	x_{-g} & y_{-g} & z_{-g} & 0 \\ 
	0 & 0 & 0 & 1 \\\end{bmatrix}
$$

- Summary
  - Transform objects together with the camera-
  - Until camera's at the origin, up at Y, look at -Z



## Projection Transformation ??

- Projection in Computer Graphics
  - 3D to 2D
  - Orthographic projection
  - Perspective projection

<img src=".\Images\Projection Transformation.png" alt="Projection Transformation" style="zoom:50%;" />

<img src=".\Images\Projection Transformation1.png" alt="Projection Transformation" style="zoom: 80%;" />

### Orthographic Projection

- A simple way of understanding

  - Camera located at origin, looking at -Z, up at Y (looks familiar?)

  - Drop Z coordinate
  - Translate and scale the resulting rectangle to$[-1, 1]^2$

<img src=".\Images\Orthographic Projection.png" alt="Orthographic Projection" style="zoom: 80%;" />

- In genera
  - We want to map a cuboid [l, r] x [b, t] x [f, n] to the“canonical(正则、规范、标准)”cube$[-1, 1]^3$
    <img src=".\Images\Orthographic Projection1.png" alt="Orthographic Projection" style="zoom: 80%;" />

### Perspective Projection

- Most common in Computer Graphics, art, visual system
- Further objects are smaller
- Parallel lines not parallel; converge to single point

<img src=".\Images\Perspective Projection.png" alt="Perspective Projection" style="zoom:67%;" />



# Rasterization (Triangles)

## What's after MVP?

- Model transformation (placing objects)
- View transformation (placing camera)
- Projection transformation
  - Orthographic projection (cuboid to “canonical” cube $[-1, 1]^3$
  - Perspective projection (frustum to “canonica” cube)
- Canonical cube to ?

## Canonical Cube to Screen

- What is a screen?
  - An array of pixels
  - Size of the array: resolution
  - A typical kind of raster display

- Raster == screen in German
  - Rasterize == drawing onto the screen

- Pixel (FYl, short for“picture element””)
  - For now: A pixel is a little square with uniform color
  - Color is a mixture of (red, green, blue)

- Defining the screen space
  - Slightly different from the “tiger book'

<img src=".\Images\Canonical Cube to Screen.png" alt="Canonical Cube to Screen" style="zoom:67%;" />

​	Pixels’ indices are in the form of (x, y), where both x and y are integers
​	Pixels’ indices are from(0, 0) to (width - 1, height - 1)
​	Pixel (x, y) is centered at(x + 0.5, y + 0.5)
​	The screen covers range(0, 0) to (width, height)

### Canonicalcube to Screern

- Irrelevant to z

- Transform in xy plane: $[-1, 1]^2$ to [0, width] x [0, height]

- Viewport transform matrix:
  $$
  M_{viewport} = \begin{pmatrix}
  	width / 2 & 0 & 0 & width / 2 \\
  	0 & height / 2 & 0 & height / 2 \\
  	0 & 0 & 1 & 0 \\
  	0 & 0 & 0 & 1 \\
  \end{pmatrix}
  $$

## Antialiasing

抗锯齿

### Aliasing

<img src=".\Images\Anliasing.png" alt="Aliasing" style="zoom: 50%;" />



### Sampling theory 

抽样理论

Sampling is Ubiquitous inComputer Graphics

Sampling Artifacts (Errors / Mistakes /lnaccuracies) in Computer Graphics
计算机图形学中的采样伪影(错误/错误/不准确)

Recap: iesting in/out 🔺 at pixels'centers<img src=".\Images\Testing in&out.png" alt="Testing in&out" style="zoom: 33%;" />

Pixels are uniformly-colored squares<img src=".\Images\Pixels are uniformly-colored squares.png" alt="Testing in&out" style="zoom: 33%;" />

Compare: The Continuous Triangle Function<img src=".\Images\Compare The Continuous Triangle Function.png" alt="Testing in&out" style="zoom: 33%;" />

### Artifacts due to sampling - "Aliasing"

采样产生的伪影——“混叠”

#### Jaggies(Staircase Pattern)

锯齿(楼梯模式)

<img src=".\Images\Jaggies.png" alt="Jaggies" style="zoom: 50%;" />

Antialiasing

<img src=".\Images\Antialiasing.png" alt="Antialiasing" style="zoom: 50%;" />

#### Moire Patterns in lmaging

成像中的云纹模式

<img src=".\Images\Moire Patterns in lmaging.png" alt="Jaggies" style="zoom: 50%;" />

Behind the Aliasing Artifacts
	Signals are changing too fast (high frequency)but sampled too slowly

#### Point Sampling vs Antialiasing

<img src=".\Images\Point Sampling vs Antialiasing.png" alt="Point Sampling vs Antialiasing" style="zoom: 50%;" />

#### Antiatiasing vs Blurred Aliasing

<img src=".\Images\Antiatiasing vs Blurred Aliasing.png" alt="Point Sampling vs Antialiasing" style="zoom: 50%;" />



### Frequency Domain

频域

#### Sines and Cosines

<img src=".\Images\Sines and Cosines.png" alt="Point Sampling vs Antialiasing" style="zoom: 50%;" />

#### Frequencies

$cos2\pi fx$ ， Frequencies：$f$

<img src=".\Images\Frequencies.png" alt="Frequencies" style="zoom: 50%;" />

### Fourier Transform

傅里叶变换

Represent a function as a weighted sum of sines and cosines
将函数表示为正弦和余弦的加权和

<img src=".\Images\Fourier Transform.png" alt="Fourier Transform"  />

$f(x) = \frac{A}{2} + \frac{2Acos(tw)}{\pi}$

<img src=".\Images\Fourier Transform1.png" alt="Fourier Transform"  />

$f(x) = \frac{A}{2} + \frac{2Acos(tw)}{\pi} - \frac{2Acos(3tw)}{3\pi}$

<img src=".\Images\Fourier Transform2.png" alt="Fourier Transform"  />

$f(x) = \frac{A}{2} + \frac{2Acos(tw)}{\pi} - \frac{2Acos(3tw)}{3\pi} + \frac{2Acos(5tw)}{5\pi}$

......

#### Fourier Transform Decomposes A SignalInto Frequencies

傅里叶变换将信号分解成频率

<img src=".\Images\Fourier Transform Decomposes A SignalInto Frequencies.png" alt="Fourier Transform Decomposes A SignalInto Frequencies" style="zoom: 50%;" />

$e^{ix} = cosx + isinx$



#### Higher Frequencies Need Faster Sampling

更高的频率需要更快的采样

<img src=".\Images\Higher Frequencies Need Faster Sampling.png" alt="Higher Frequencies Need Faster Sampling" style="zoom: 50%;" />



#### Undersampling Creates Frequency Aliases

<img src=".\Images\Undersampling Creates Frequency Aliases.png" alt="Higher Frequencies Need Faster Sampling" style="zoom: 67%;" />

High-frequency signal is insufficiently sampled: samples erroneously appear to be from a low-frequency signal
高频信号采样不足:采样错误地显示为来自低频信号

Two frequencies that are indistinguishable at a given sampling are called “aliases"
在给定采样中无法区分的两个频率称为“别名”。

#### Filtering

滤波

Getting rid ofcertain frequency contents
去除某些频率内容

**Visualizing image Frequency Content** 可视化图像频率内容

<img src=".\Images\Visualizing image Frequency Content.png" alt="Visualizing image Frequency Content" style="zoom: 50%;" />

**Filter Out Low Frequencies Only (Edges) **仅滤除低频(边缘)

<img src=".\Images\Filter Out Low Frequencies Only.png" alt="Visualizing image Frequency Content" style="zoom: 50%;" />

**Filter Out High Frequencies (Blur)**  滤除高频(模糊)

<img src=".\Images\Filter Out High Frequencies.png" alt="Filter Out High Frequencies" style="zoom: 50%;" />

**Filte Out Low and High Frequencies** 滤除低频和高频

<img src=".\Images\Filte Out Low and High Frequencies.png" alt="Filte Out Low and High Frequencies" style="zoom: 50%;" />

<img src=".\Images\Filte Out Low and High Frequencies1.png" alt="Filte Out Low and High Frequencies" style="zoom: 50%;" />

**Filtering = Convolution (= Averaging)** 滤波 = 卷积 ( = 平均)



#### Convolution

<img src=".\Images\Convolution.png" alt="Convolution" style="zoom: 33%;" />

Point-wise local averaging in a “siding window"

##### Convolution Theorem

卷积定理

Convolution in the spatial domain is equal to multiplicationin the frequency domain, and vice versa
空间域中的卷积等于频域中的乘法，反之亦然

**Option 1:**
	Filter by convolution in the spatial domain
**Option 2:**
	Transform to frequency domain (Fourier transform)
	Multiply by Fourier transform of convolution kernel
	Transform back to spatial domain (inverse Fourier)

**选项1:**
	在空间域中通过卷积滤波

**选项2:**
	变换到频域(傅里叶变换)
	乘以卷积核的傅里叶变换
	变换回空间域(傅里叶反变换)

<img src=".\Images\Convolution Theorem.png" alt="Convolution Theorem" style="zoom: 33%;" />

<img src=".\Images\Box Function.png" alt="Box Function" style="zoom: 33%;" />

<img src=".\Images\Box Function1.png" alt="Box Function" style="zoom: 33%;" />



#### Sampling 

Sampling = Repeating Frequency Contents
采样=重复频率内容

<img src=".\Images\Sampling.png" alt="Sampling" style="zoom: 60%;" />

**Aliasing = Mixed Frequency Contents**
混叠=混合频率内容

Dense sampling:<img src=".\Images\Dense sampling.png" alt="Dense sampling" style="zoom: 60%;" />

Sparse sampling:<img src=".\Images\Sparse sampling.png" alt="Sparse sampling" style="zoom: 60%;" />



#### How Can We Reduce Aliasing Error?

Option 1:Increase sampling rate

- Essentially increasing the distance between replicas in the Fourier domain
- Higher resolution displays, sensors, framebuffers...
- But: costly & may need very high resolution

选项1:提高采样率

- 本质上增加了傅立叶域中副本之间的距离

- 更高分辨率的显示器，传感器，帧缓冲区…

- 但是:昂贵并且可能需要非常高的分辨率

Option 2: Antialiasing

- Making Fourier contents “narrower” before repeating
- i.e. Filtering out high frequencies before sampling

选项2:抗锯齿

- 在重复之前使傅里叶内容“更窄”

- 即在采样前滤除高频

<img src=".\Images\Antialiasing1.png" alt="Antialiasing" style="zoom: 50%;" />



### Antialiasing in practice 

实践中的抗混叠

#### Antialiasing ldea:Blurring (Pre-Filtering) Before Sampling

抗混叠思想:在采样前模糊(预滤波)

**Rasterization: Point Sampling in Space**

<img src=".\Images\Rasterization Point Sampling in Space.png" alt="Jaggies" style="zoom: 50%;" />

Note jaggies in rasterized trianglewhere pixel values are pure red or white
注意栅格化三角形中的锯齿，其中像素值是纯红色或白色

**Rasterization: Antialiased Sampling**

<img src=".\Images\Rasterization Antialiased Sampling.png" alt="Jaggies" style="zoom: 50%;" />

Note antialiased edges in rasterized trianglewhere pixel values take intermediate values
注意栅格化三角形的抗锯齿边缘，其中像素值采用中间值



#### A Practical Pre-Filter

A 1 pixel-width box filter (low pass, blurring)
<img src=".\Images\A Practical Pre-Filter.png" alt="A Practical Pre-Filter" style="zoom: 50%;" />

Antialiasing By Averaging Values in Pixel Area

Solution:

- Convolve f(x, y) by a 1-pixel box-blur
  - Recall: convolving = filtering = averaging
- Then sample at every pixel's center

In rasterizing one triangle, the average value inside a pixel area of f(x,y) = inside(triangle,x,y) is equal to the area of the pixel covered by the triangle.
在栅格化一个三角形时，f(x, y) = inside(triangle, x, y)在像素区域内的平均值等于该三角形所覆盖的像素面积。
<img src=".\Images\Antialiasing2.png" alt="Antialiasing By Averaging Values in Pixel Area" style="zoom: 50%;" />



#### Antialiasing By Supersampling(MSAA)

Approximate the effect of the 1-pixel box filter by samplingmultiple locations within a pixel and averaging their values
通过采样一个像素内的多个位置并平均它们的值来近似1像素盒滤波器的效果

<img src=".\Images\Supersampling.png" alt="Supersampling" style="zoom: 50%;" />

<img src=".\Images\Supersampling1.png" alt="Supersampling" style="zoom: 50%;" />

<img src=".\Images\Supersampling2.png" alt="Supersampling" style="zoom: 50%;" />

<img src=".\Images\Supersampling3.png" alt="Supersampling" style="zoom: 50%;" />



#### FXAA(Fast Approximate AA)

#### TAA(Temporal AA)

#### Super resolution / super sampling

- From low resolution to high resolution
- Essentially still “not enough samples” problem
- DLSS (Deep Learning Super Sampling)



## Visibility / occlusion

### Z-Buffer

This is the algorithm that eventually won.

Idea:

- Store current min. z-value for each sample (pixel)
- Needs an additional buffer for depth values
  - frame buffer stores color values
  - depth buffer (z-buffer) stores depth

IMPORTANT: For simplicity we suppose, z is always positive, smaller z -> closer, larger z -> further)

这就是最终的算法。

想法:

- 存储每个样本(像素)的当前最小z值
- 需要一个额外的深度值缓冲区

- 帧缓冲区存储颜色值

- 深度缓冲区(z-buffer)存储深度

重要：为了简单起见，我们假设z总是正的，较小的z ->更近，更大z ->更远)

#### Z-Buffer Algorithm

```python
for(each triangle T)
	for(each sample(x, y, z) in T)
		if(z < zbuffer[x,y])				// closest sample so far
			framebuffer[x,y] = rgb;			// update color
			zbuffer[x,y] = z;				// update depth
 		else
			;							// do nothing, this sample is occluded
			
```

<img src=".\Images\Z-Buffer Algorithm.png" alt="Z-Buffer Algorithm" style="zoom: 50%;" />

#### Z-Buffer Complexity

O(n) for n triangles (assuming constant coverage)



## Shadows

### Shadow mapping

An lmage-space Algorithm
	no knowledge of scene's geometry during shadowcomputation
	must deal with aliasing artifacts
一种图像空间算法
	在阴影计算过程中不了解场景的几何形状
	必须处理混叠工件

Key idea:
	the points NOT in shadow must be seen bothby the light and by the camera
核心思想:
	不在阴影中的点必须在光线和相机中都能看到

#### Pass 1: Render from Light

Depth image from light source
<img src=".\Images\Render from Light.png" alt="Render from Light" style="zoom: 50%;" />

#### Pass 2A: Render from Eye

Standard image (with depth) from eye
<img src=".\Images\Render from Eye.png" alt="Render from Eye" style="zoom: 50%;" />

#### Pass 2B: Project to light

Project visible points in eye view back to light source
<img src=".\Images\Project to light.png" alt="Project to light" style="zoom: 50%;" />

### Visualizing Shadow Mapping

A fairly complex scene with shadows
<img src=".\Images\Visualizing Shadow Mapping.png" alt="Visualizing Shadow Mapping" style="zoom: 50%;" />

The scene from the light's point-of-view
<img src=".\Images\The scene from the light's point-of-view.png" alt="The scene from the light's point-of-view" style="zoom: 50%;" />

Comparing Dist(light, shading point) with shadow map
<img src=".\Images\Visualizing Shadow Mapping1.png" alt="Visualizing Shadow Mapping" style="zoom: 50%;" />
Green is where the distance(light,shading point) ≈ depth on the shadow map
Non-green is where shadows should be
绿色表示距离(光，阴影点) ≈ 在阴影图上的深度
非绿色是阴影应该出现的地方

### Hard shadows vs. soft shadows

<img src=".\Images\Hard shadows vs. soft shadows.png" alt="Hard shadows vs. soft shadows" style="zoom: 70%;" align="left"/>



# Shading

The process of applying a material to an object.
将材料应用到物体上的过程。

## Blinn-Phong Reflectance Mode

<img src=".\Images\Blinn-Phong Reflectance Mode.png" alt="Blinn-Phong Reflectance Mode" style="zoom: 50%;" />

Compute light reflected toward cameraat a specific shading point
计算光线反射到相机的一个特定的阴影点

Inputs:

- Viewer direction,v
- Surface normal, n
- Light direction, l(for each of many lights)
- Surface parameters(color, shininess, ...)

<img src=".\Images\Shading is Local.png" alt="Shading is Local" style="zoom: 50%;" />

No shadows will be generated! (shading ≠shadow)
<img src=".\Images\Shading is Local1.png" alt="Shading is Local" style="zoom: 50%;" />

### Diffuse Reflection

Light is scattered uniformly in all directions
	Surface color is the same for all viewing directions
光在各个方向均匀地散射
	表面颜色是相同的所有观看方向
<img src=".\Images\Diffuse Reflection.png" alt="Diffuse Reflection" style="zoom: 50%;" />

Lambert's cosine law
朗伯余弦定律

Top face of cube receives a certain amount of light
立方体的顶面接收一定量的光<img src=".\Images\Diffuse Reflection1.png" alt="Diffuse Reflection" style="zoom: 50%;" />

Top face of 60° rotated cube intercepts half the light
60°旋转立方体的顶面拦截了一半的光<img src=".\Images\Diffuse Reflection2.png" alt="Diffuse Reflection" style="zoom: 50%;" />
In general, light per unit area is proportional to $cos\theta = l \cdot n$
一般来说，单位面积的光与$cos\theta = l \cdot n$成正比<img src=".\Images\Diffuse Reflection3.png" alt="Diffuse Reflection" style="zoom: 50%;" />

Light Falloff
<img src=".\Images\Light Falloff.png" alt="Diffuse Reflection" style="zoom: 30%;" />

Shading independent of view direction
着色独立于视图方向

<img src=".\Images\Diffuse Shading.png" alt="Diffuse Shading" style="zoom: 60%;" />
$$
L_d = k_d(I/r^2)max(0, n\cdot l)\\ 
\\
L_d:diffusely\ reflected\ light \\
k_d:diffuse\ coefficient (color)\\
I/r^2: energy\ arrived\ at\ the\ shading\ point \\
max(0, n\cdot l): energy\ recived\ by\ the\ shading\ point
$$

### Specular Term(Blinn-Phong)

Intensity depends on view direction
	Bright near mirror reflection direction
强度取决于观察方向
	明亮的近镜反射方向
<img src=".\Images\Specular Term.png" alt="Specular Term" style="zoom: 50%;" />

V close to mirror direction <=> half vector near normal
	Measure “near" by dot product of unit vectors
V接近镜面方向 <=> 近法线半向量
	用单位向量的点积来度量“n”
<img src=".\Images\Specular Term1.png" alt="Specular Term" style="zoom: 50%;" />
$$
\bold{h} = bisector(\bold{v}, \bold{l}) = \frac{\bold{v} + \bold{l}}{||\bold{v} + \bold{l}||} \\
L_s = k_s(I/r^2)max(0, cos\alpha)^p  = k_s(I/r^2)max(0, \bold{n} \cdot \bold{h})^p \\
L_s: specularly\ reflected\ light \\
k_s: specular\ coefficient
$$
p的含义<img src=".\Images\Cosine Power Plots.png" alt="Cosine Power Plots" style="zoom: 50%;" />
<img src=".\Images\Specular Term2.png" alt="Specular Term" style="zoom: 50%;" />



### Ambient Term

Shading that does not depend on anything
	Add constant color to account for disregardedillumination and fill in black shadows
	This is approximate / fake!
阴影不依赖于任何东西
	添加恒定的颜色来解释忽略的照明和填充黑色阴影
	这是近似的/假的!

<img src=".\Images\Ambient Term.png" alt="Ambient Term" style="zoom: 50%;" />
$$
L_a = k_aI_a \\
L_a: reflected\ ambient\ light \\
k_a: aambient\ coefficient
$$

### Blinn-Phong Reflection Model

<img src=".\Images\Blinn-Phong Reflectance Model.png" alt="Blinn-Phong Reflection Model" style="zoom: 50%;" />
$$
L_s = L_a + L_d + L_s = k_aI_a + k_a(I/r^2) max(0,\bold{n} \cdot \bold{l}) + k_s(I/r^2)max(0, \bold{n} \cdot \bold{h})^p
$$


## Shading Frequencies

<img src=".\Images\Shading Frequencies.png" alt="Shading Frequencies" style="zoom: 50%;" />

### Shade each triangle (flat shading)

Flat shading
	Triangle face is flat - one normal vector
	Not good forsmooth surfaces
平的阴影
	三角形面是平的：一个法向量
	不适合光滑的表面

<img src=".\Images\Shade each triangle.png" alt="Shade each triangle" style="zoom: 60%;" />

### Shade each vertex (Gouraud shading)

Gouraud shading
	Interpolate colorsfrom vertices across triangle
	Each vertex has anormal vector(how?)
高洛德着色
	从三角形的顶点插值颜色
	每个顶点都有法向量(如何?)

<img src=".\Images\Shade each vertex.png" alt="Shade each vertex" style="zoom: 60%;" />

### Shade each pixel(Phong shading)

Phong shading
	Interpolate normal vectors across each triangle
	Compute full shading model at each pixel
	Not the Blinn-Phong Reflectance Model
冯氏阴影
	在每个三角形上插入法向量
	在每个像素处计算完整的阴影模型
	不是Blinn-Phong反射模型
<img src=".\Images\Shade each pixel.png" alt="Shade each pixel" style="zoom: 60%;" />

<img src=".\Images\Shading Frequency Face,Vertex or Pixel.png" alt="Shading Frequency Face,Vertex or Pixel" style="zoom: 60%;" />



## Graphics (Real-time Rendering) Pipeline

### Graphics Pipeline

<img src=".\Images\Graphics Pipeline.png" alt="Graphics Pipeline" style="zoom: 60%;" />

  

## Shader Programs

Program vertex and fragment processing stages
Describe operation on a single vertex (or fragment)
程序顶点和片段处理阶段
描述对单个顶点(或片段)的操作

Example GLSL fragment shader program
示例GLSL片段着色程序

```glsl
uniform sampler2D myTexture;
uniform vec3 lightDir;
varying vec2 uv;
varying vec3 norm;
void diffuseShader()
{
    vec3 kd;
    kd = texture2d(myTexture, uv);
    kd *= clamp(dot(-lightDir, norm), 0.0, 1.0);
    gl_FragColor = vec4(kd, 1.0);
}
```

Shader function executes once per fragment.
Outputs color of surface at the current fragment'sscreen sample position.
This shader performs a texture lookup to obtain the surface's material color at this point, then performs a diffuse lighting calculation.
Shader函数每个片段执行一次。
输出当前片段屏幕样本位置表面的颜色。
这个着色器执行纹理查找以获得表面的材质颜色，然后执行漫射照明计算。

Procedurally modeled, 800 line shader. http://shadertoy.com/view/ld3Gz2



## Texture Mapping

### Surfaces are 2D

Surface lives in 3D world space
Every 3D surface point also has a place where it goes in the 2D image (texture)
表面生活在三维世界空间
每个3D表面点在2D图像中也有一个位置(纹理)
<img src=".\Images\Surfaaces are 2D.png" alt="Surfaaces are 2D" style="zoom: 60%;" />

### Texture Applied to Surface

<img src=".\Images\Texture AApplied to Surface.png" alt="Texture AApplied to Surface" style="zoom: 50%;" />

Visuaiization of Texture Coordinates
Each triangle vertex is assigned a texture coordinate (u, v)
<img src=".\Images\Visualization of Texture Coordinates.png" alt="Visualization of Texture Coordinates" style="zoom: 50%;" />



### Barycentric coordinates

重心坐标

#### Interpolation Across Triangles

跨三角形插值

Why do we want to interpolate?
	Specify values at vertices
	Obtain smoothly varying values across triangles
为什么要进行插值呢?
	指定顶点处的值
	在三角形上获得平滑变化的值

What do we want to interpolate?
	Texture coordinates, colors, normal vectors...
我们想要插入什么?
	纹理坐标，颜色，法向量...

How do we interpolate?
	Barycentric coordinates
我们如何插入呢?
	重心坐标

A coordinate system for triangles $(\alpha, \beta, \gamma)$
<img src=".\Images\Barycentric Coordinates.png" alt="Barycentric Coordinates" style="zoom: 70%;" />
<img src=".\Images\Barycentric Coordinates1.png" alt="Barycentric Coordinates" style="zoom: 70%;" />

Geometric viewpoint - proportional areas
几何视点-比例面积
<img src=".\Images\Barycentric Coordinates2.png" alt="Barycentric Coordinates" style="zoom: 70%;" />

<img src=".\Images\Barycentric Coordinates3.png" alt="Barycentric Coordinates" style="zoom: 50%;" />

<img src=".\Images\Barycentric Coordinates4.png" alt="Barycentric Coordinates" style="zoom: 50%;" />

Linearly interpolate values at vertices
在顶点处线性插值值
<img src=".\Images\Barycentric Coordinates5.png" alt="Barycentric Coordinates" style="zoom: 50%;" />

However, barycentric coordinates are not invariant under projection!
然而，质心坐标在投影下不是不变的!

### Applying Textures

for each rasterized screen sample (x,y): (Usually a pixel's center)
	(u,v) = evaluate texture coordinate at (x,y) (Using barycentric coordinates!)
	texcolor = texture.sample(u,v);
	set sample's color to texcolor; (Usually the diffuse albedo Kd(recall the Blinn-Phong reflectance model))
对于每个栅格化的屏幕样本(x,y):(通常是一个像素的中心)
	(u,v) = 在(x,y)处计算纹理坐标(使用质心坐标!)
	Texcolor = texture.sample(u,v);
	设置样本的颜色为texcolor; (通常是漫反射反照率Kd(回想一下Blinn-Phong反射模型))

#### Texture Magnification - Easy Case

纹理放大-简单情况

Generally don't want this - insufficient texture resolution
A pixel on a texture -atexel(纹理元素、纹素)
<img src=".\Images\Texture Magnification.png" alt="Texture Magnification" style="zoom:67%;" />

##### Bilinear interpolation

<img src=".\Images\Bilinear interpolation.png" alt="Bilinear interpolation" style="zoom:27%;" />
Want to sampletexture value f(x,y) at red point
Black points indicate texture sample locations
想要在红点采样纹理值f(x,y)
黑点表示纹理样本的位置

<img src=".\Images\Bilinear interpolation1.png" alt="Bilinear interpolation" style="zoom:25%;" />
$lerp(x,v_0,v_1) = v_0 + x(v_1 - v_0)$



#### Texture Magnification (hard case)

What if the texture is too large?

**Point Sampling Textures - Problem**
<img src=".\Images\Point Sampling Textures.png" alt="Point Sampling Textures" style="zoom:45%;" />
<img src=".\Images\Point Sampling Textures1.png" alt="Point Sampling Textures" style="zoom:45%;" />
Will supersampling work?
	Yes, high quality, but costly
	When highly minified, many texels in pixel footprint
	Signal frequency too large in a pixel
	Need even higher sampling frequency
超采样有效吗?
	是的，质量很好，但是很贵
	当高度缩小时，许多像素占用空间
	一个像素的信号频率太大
	需要更高的采样频率

Let's understand this problem in another way
	What if we don't sample?
	Just need to get the average value within a range!
让我们用另一种方式来理解这个问题
	如果我们不取样呢?
	只需要得到一个范围内的平均值!

##### Mipmap

Allowing (fast, approx., square) range queries

<img src=".\Images\Mipmap.png" alt="Mipmap" style="zoom:45%;" />

##### Computing Mipmap Level D

<img src=".\Images\Computing Mipmap Level D.png" alt="Computing Mipmap Level D" style="zoom:45%;" />

<img src=".\Images\Computing Mipmap Level D1.png" alt="Computing Mipmap Level D" style="zoom:65%;" />
$$
D = log_2L \\
L = max(
	\sqrt{(\frac{du}{dx})^2 + (\frac{dv}{dx})^2}, 
	\sqrt{(\frac{du}{dy})^2 + (\frac{dv}{dy})^2}
)
$$

##### Trilinear interpolation

<img src=".\Images\Trilinear interpolation.png" alt="Trilinear interpolation" style="zoom:65%;" />

<img src=".\Images\Point Sampling1.png" alt="Point Sampling" style="zoom:45%;" />
<img src=".\Images\Supersampling 512x.png" alt="Supersampling 512x" style="zoom:45%;" />
<img src=".\Images\Mipmap trilinear sampling.png" alt="Mipmap trilinear sampling" style="zoom:45%;" />



##### Anisotropic Filtering

Ripmaps and summed area tables
	Can look up axis-aligned rectangular zones
	Diagonal footprints still a problem
Ripmaps和求和面积表
	可以查找轴对齐的矩形区域吗
	对角脚印仍然是个问题
<img src=".\Images\Anisotropic Filtering.png" alt="Anisotropic Filtering" style="zoom:45%;" />
<img src=".\Images\Irregular Pixel Footprint in Texture.png" alt="Irregular Pixel Footprint in Texture" style="zoom:45%;" />

##### EWA filtering

Use multiple lookups
Weighted average
Mipmap hierarchy still helps
Can handle irregular footprints
<img src=".\Images\EWA filtering.png" alt="EWA filtering" style="zoom:75%;" />



## Many Uses for Texturing

In modern GPUs, texture = memory + range query (filtering)
	General method to bring data to fragment calculations
在现代gpu中，纹理=内存+范围查询(过滤)
	将数据带入片段计算的一般方法

Many applications
	Environment lighting
	Store microgeometry
	Procedural textures
	Solid modeling
	Volume rendering
许多应用程序
	环境照明
	商店microgeometry
	程序上的纹理
	坚实的建模
	体绘制



# Geometry

## Many Ways to Represent Geometry

Implicit
	algebraic surface
	level sets
	distance functions
隐式的
	代数曲面
	水平集
	距离函数

Explicit
	point cloud
	polygon mesh
	subdivision,NURBS
显式的
	点云
	多边形网格
	细分,NURBS

### Implicit

Based on classifying points
	Points satisfy some specified relationship
	E.g. sphere: all points in 3D, where $x^2+y^2+z^2 = 1$
基于分类点
	点满足某种特定的关系

<img src=".\Images\Implicit.png" alt="Implicit" style="zoom:75%;" />


<img src=".\Images\Implicit1.png" alt="Implicit" style="zoom:75%;" />

#### Distance Functions (implicit)

Instead of Booleans, gradually blend surfaces together using
Distance functions:
	giving minimum distance (could be signed distance)from anywhere to object
而不是布尔值，逐渐混合曲面在一起使用
距离函数:
	给出从任何地方到对象的最小距离(可以标记为距离)
<img src=".\Images\Distance Function.png" alt="Distance Function" style="zoom:75%;" />

<img src=".\Images\Distance Function1.png" alt="Distance Function" style="zoom:55%;" />
Can blend any two distance functions d1, d2: 
<img src=".\Images\Distance Function2.png" alt="Distance Function" style="zoom:55%;" />

#### Level Set Methods (Also implicit)

Closed-form equations are hard to describe complex shapes
Alternative: store a grid of values approximating function
封闭形式的方程很难描述复杂的形状
备选方案:存储一个网格值逼近函数

#### Fractals (implicit)

Exhibit self-similarity, detail at all scales
" Language" for describing natural phenomena
Hard to control shape!
展示自相似性，所有尺度的细节
描述自然现象的“语言”
难以控制形状!
<img src=".\Images\Fractals.png" alt="Fractals" style="zoom:55%;" />

Implicit Pros:
	compact description (e.g., a function)
	certain queries easy (inside object, distance to surface)
	good for ray-to-surface intersection (more later)
	for simple shapes, exact description / no sampling error
	easy to handle changes in topology (e.g., fluid)

Implicit Cons:
	difficult to model complex shapes



### Explicit

All points are given directly or via parameter mapping
所有的点都是直接或通过参数映射给出的

<img src=".\Images\Explicit.png" alt="Explicit" style="zoom:55%;" />

$f(u,v) =((2 + \cos u) \cos v,(2 + \cos u)\sin v, \sin u)$

#### Point Cloud (Explicit)

Easiest representation: list of points (x,y,z)
Easily represent any kind of geometry
Useful for L ARGE datasets (>> 1 point/pixel)
Often converted into polygon mesh
Difficult to draw in undersampled regions
最简单的表示:点列表(x,y,z)
很容易表示任何几何形状
对大型数据集有用(>>1点/像素)
通常转换成多边形网格
在采样不足的区域难以绘制
<img src=".\Images\Point Cloud.png" alt="Point Cloud" style="zoom:35%;" />

#### Polygon Mesh (Explicit)

Store vertices & polygons (often triangles or quads)
Easier to do processing / simulation, adaptive sampling
More complicated data structures
Perhaps most common representation in graphics
存储顶点和多边形(通常是三角形或四边形)
更容易做处理/模拟，自适应采样
更复杂的数据结构
也许是图形中最常见的表示
<img src=".\Images\Polygon Mesh.png" alt="Polygon Mesh" style="zoom:35%;" />

#### The Wavefront Object File (.obj) Format

Commonly used in Graphics research
Just a text file that specifies vertices, normals, texture coordinates and their connectivities
通常用于图形研究
只是一个文本文件，指定顶点，法线，纹理坐标和它们的连接<img src=".\Images\obj.png" alt="Polygon Mesh" style="zoom:65%;" />



## Curves

### Bezier Curves

#### Defining Cubic Bezier Curve With Tangents

<img src=".\Images\Defining Cubic Bezier Curve With Tangents.png" alt="Defining Cubic Bezier Curve With Tangents" style="zoom:45%;" />

<img src=".\Images\Bezier Curves.png" alt="Bezier Curves" style="zoom:45%;" />

### Spline

a continuous curve constructed so as to pass through a given setof points and have a certain number of continuous derivatives
In short, a curve under control
一种连续曲线，它通过一组给定的点，并有一定数量的连续导数
简而言之，这是一条可控的曲线

#### B-splines

Short for basis splines
Require more information than Bezier curves
Satisfy all important properties that Bezier curves have (i.e superset)
基样条的简称
需要比贝塞尔曲线更多的信息
满足贝塞尔曲线的所有重要性质(即超集)

To learn more / deeper, you are welcome to refer toProf. Shi-Min Hu's course: https://www.bilibili.com/video/av66548502?from=search&seid=65256805876131485

## Surfaces

### Bezier Surfaces

<img src=".\Images\Bezier Surface.png" alt="Bezier Surfaces" style="zoom:45%;" />

## Subdivision

### Loop Subdivision

Common subdivision rule for triangle meshes
First, create more triangles (vertices)
Second, tune their positions

Split each triangle into four
<img src=".\Images\Split.png" alt="Split" style="zoom:45%;" />

Assign new vertex positions according to weights-
	New / old vertices updated differently

### Catmull-Clark Subdivision (General Mesh)

<img src=".\Images\Catmull-Clark Subdivision.png" alt="Catmull-Clark Subdivision (General Mesh).png" style="zoom:45%;" />
Each subdivision step:
	Add vertex in each face
	Add midpoint on each edge
	Connect all new vertices

<img src=".\Images\Catmull-Clark Subdivision1.png" alt="Catmull-Clark Subdivision (General Mesh).png" style="zoom:45%;" />
After one subdivision:
	How many extraordinary vertices?
	What are their degrees?
	How many non-quad faces?

## Mesh Simplification

Goal: reduce number of mesh elements while maintaining the overall shape
目标:在保持整体形状的同时减少网格元素的数量
<img src=".\Images\Mesh Simplification.png" alt="Mesh Simplification" style="zoom:45%;" />

### Collapsing An Edge

Suppose we simplify a mesh using edge collapsing

<img src=".\Images\Collapsing An Edge.png" alt="Collapsing An Edge" style="zoom:45%;" />

Quadric Error Metrics
	How much geometric error is introduced by simplification?
	Not a good idea to perform local averaging of vertices
	Quadric error: new vertex should minimize its sum of square distance (L2 distance) to previously related triangle planes!
二次误差度量
	化简会带来多少几何误差?
	对顶点进行局部平均不是一个好主意
	二次误差:新顶点到之前相关三角形平面的平方和(L2距离)应该最小化!



# Ray Tracing

Rasterization couldn't handle global effects well
	(Soft) shadows
	And especially when the light bounces more than once
栅格化不能很好地处理全局效果
	(软)阴影
	尤其是当光线反射不止一次的时候

Ray tracing is accurate, but is very slow
	Rasterization: real-time, ray tracing: offline
	~10K CPU core hours to render one frame in production
光线追踪是准确的，但速度很慢
	光栅化:实时，光线追踪:离线
	~10K CPU核心小时来渲染一帧

## Basic Ray-Tracing Algorithm

### Ray Casting - Shading Pixels (Local Only)

Pinhole Camera Model
<img src=".\Images\Pinhole Camera Model.png" alt="Pinhole Camera Model" style="zoom:45%;" />

### Recursive(Whitted-Style) Ray Tracing

<img src=".\Images\Recursive(Whitted-Style) Ray Tracing.png" alt="Recursive(Whitted-Style) Ray Tracing" style="zoom:45%;" />

### Light Rays

Three ideas about light rays

1. Light travels in straight lines (though this is wrong)
2. Light rays do not “collide" with each other if they cross(though this is still wrong)
3. Light rays travel from the light sources to the eye (butthe physics is invariant under path reversal - reciprocity)

关于光线的三个观点

1. 光沿直线传播(虽然这是错误的)
2. 光线交叉时不会相互“碰撞”(尽管这仍然是错误的)
3. 光线从光源传播到眼睛(但物理是不变的路径反转-互惠)

### Ray-Surface Intersection

#### Ray Equation

Ray is defined by its origin and a direction vector
<img src=".\Images\Ray Equation.png" alt="Ray Equation" style="zoom:100%;" />

$r(t) = o + td \ \ (0 ≤ t < \infty)$

#### Plane Equation

Plane is defined by normal vector and a point on plane
<img src=".\Images\Plane Equation.png" alt="Plane Equation" style="zoom:60%;" />
$p:(p-p')\cdot N = 0$
$ax + by + cz + d = 0$

#### Ray Intersection With Sphere

Ray: $r(t) = o + td \ \ (0 ≤ t < \infty)$
Sphere: $p:(p-c)^2 - R^2 = 0$
Solve for intersection:$(o + td - c)^2 - R^2 = 0$
<img src=".\Images\Ray Intersection.png" alt="Ray lntersection" style="zoom:100%;" />

#### Ray Intersection With Implicit Surface

Ray: $r(t) = o + td \ \ (0 ≤ t < \infty)$
General implicit surface: $p:f(p) = 0$
Substitute ray equation: $f(o+td) = 0$

#### Ray lntersection With Triangle Mesh

Rendering: visibility, shadows,lighting ...
Geometry: inside/outside test
渲染:可见性，阴影，照明…
几何:内/外测试

Let's break this down:
	Simple idea: just intersect ray with each triangle
	Simple, but slow (acceleration?)
	Note: can have 0, 1 intersections(ignoring multiple intersections)
让我们来分析一下:
	简单的想法:让射线与每个三角形相交
	简单，但慢(加速?)
	注:可以有0,1个交叉口(忽略多个交叉口)

#### Ray Intersection With Plane

Ray equation: $r(t) = o + td, 0 ≤ t < \infty$
Plane equation: $p:(p - p')\cdot N = 0$

Solve for intersection
	Set p = r(t) and solve for t
	$(p - p') \cdot N = (o + td - p') \cdot N = 0$
	$t = \frac{(p' - o)\cdot N}{d\cdot N} \\ $
<img src=".\Images\Ray Intersection With Plane.png" alt="Ray Intersection With Plane" style="zoom:50%;" />

#### Moller Trumbore Algorithm

A faster approach, giving barycentric coordinate directly
一个更快的方法，直接给出重心坐标

### Bounding Volumes

<img src=".\Images\Bounding Volumes.png" alt="Bounding Volumes" style="zoom:50%;" />

#### Ray-Intersection With Box

Understanding: box is the intersection of 3 pairs of slabs
<img src=".\Images\Ray Intersection With Box.png" alt="Ray-Intersection With Box" style="zoom:50%;" />

Specifically: We often use anAxis-AlignedBounding Box(AABB)(轴对齐包盒)
i.e. any side of the BBis along either x, y, or zaxis
具体来说:我们经常使用anAxis-AlignedBounding Box(AABB)(轴)
也就是说，BBis沿着x, y或z轴的任何一边

#### Ray Intersection with Axis-Aligned Box

2D example;3D is the same! Compute intersections with slabsand take intersection of $t_{min}/t_{max}$ intervals
<img src=".\Images\Ray Intersection With Axis-Aligned Box.png" alt="Ray Intersection With Axis-Aligned Box" style="zoom:50%;" />

Recall: a box (3D) = three pairs of infinitely large slabs
回想一下:一个盒子(3D) =三对无限大的板

Key ideas
	The ray enters the box only when it enters all pairs of slabs
	The ray exits the box as long as it exits any pair of slabs
关键思想
	光线只有在进入所有对平板时才能进入盒子
	射线离开盒子的时间和离开任何一对平板的时间一样长

For each pair, calculate the tmin and tmax (negative is fine)
对于每一对，计算tmin和tmax(负数也可以)

For the 3D box, $t_{enter} = max\{t_{min}\}$,  $t_{exit} = min\{t_{max}\}$
3D的盒子, $t_{enter} = max\{t_{min}\}$,  $t_{exit} = min\{t_{max}\}$

lf $t_{enter}$< $t_{exit}$, we know the ray stays a while in the boxso they must intersect!) (not done yet, see the next slide)



## Using AABBs to accelerate ray tracing

### Uniform Spatial Partitions (Grids)

统一空间分区(网格)

#### Preprocess - Build Acceleration Grid

预处理-构建加速网格
<img src=".\Images\Preprocess - Build Acceleration Grid.png" alt="Preprocess - Build Acceleration Grid" style="zoom:50%;" />

1. Find bounding box 查找边界框
2. Create grid 创建网格
3. Store each object in overlapping cells 将每个对象存储在重叠的单元格中


<img src=".\Images\Ray-Scene Intersection.png" alt="Ray-Scene Intersection" style="zoom:50%;" />

Step through grid in raytraversal order

For each grid cell
	Test intersection
	with all objects
	stored at that cell

按光线遍历顺序步进网格

对于每个网格单元
	测试的十字路口
	对所有对象
	存储在那个单元格中



<img src=".\Images\OneCell.png" alt="One Cell" style="zoom:20%;" /><img src=".\Images\Too many cells.png" alt="Too many cells" style="zoom:20%;" /><img src=".\Images\Heuristic.png" alt="Heuristic" style="zoom:20%;" />

Heuristic:
	#cells = C * #objs
	C ≈ 27 in 3D



### Spatial Partitions

<img src=".\Images\Spatial Partitioning Examples.png" alt="Spatial Partitioning Examples" style="zoom:60%;" />



## Obiect Partitions & Bounding Volume Hierarchy (BVH)

### Bounaing Volume Hierarchy (BVH)

<img src=".\Images\Bounaing Volume Hierarchy (BVH).png" alt="Bounaing Volume Hierarchy (BVH)" style="zoom:60%;" />

Find bounding box
Recursively split set ofobjects in two subsets
Recompute the boundingbox of the subsets
Stop when necessary
Store objects in each leaf node
查找边界框
递归地将一组对象分成两个子集
重新计算子集的边界框
必要时停止
在每个叶节点中存储对象



## Basic radiometry 

(辐射度量学)

### Radiometry

Measurement system and units for illumination
Accurately measure the spatial properties of light
	New terms: Radiant flux, intensity, irradiance, radiance
照明测量系统和单位
精确测量光的空间特性
	新术语:辐射通量，强度，辐照度，辐射度

**Why, What then How?**

#### Radiant Energy and Flux(Power)

Definition: Radiant energy is the energy of electromagnetic radiation. lt is measured in units of joules, and denoted by the symbol:
定义:辐射能是电磁辐射的能量。Lt的单位是焦耳，用符号表示:
$Q[J = Joule]$

Definition: Radiant flux (power) is the energy emitted, reflected, transmitted or received, per unit time.
定义:辐射通量(功率)是单位时间内发射、反射、发射或接收的能量。
$\Phi = \frac{dQ}{dt}[W = Watt][lm = lumen]^*\\ $



#### Important Light Measurements of Interest

<img src=".\Images\Important Light Measurements of Interest.png" alt="Important Light Measurements of Interest" style="zoom:60%;" />



#### Irradiance

Definition: The irradiance is the power per (perpendicular/projected) unit area incident on a surface point.
定义:辐照度是每(垂直/投影)单位面积入射到表面点上的功率

$E(x) = \frac{d\varPhi(x)}{dA}\\$
$[\frac{W}{m^2}] [\frac{lm}{m^2} = lux]\\$
<img src=".\Images\Irradiance.png" alt="Irradiance" style="zoom:60%;" />

#### Bidirectional Reflectance Distribution Function (BRDF)
