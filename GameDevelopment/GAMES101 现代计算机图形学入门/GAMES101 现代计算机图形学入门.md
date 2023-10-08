# 课程网址

https://www.bilibili.com/video/BV1X7411F744/?spm_id_from=333.337.search-card.all.click&vd_source=1b732552b2e7da5edcc8398add8181dd

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

  <img src="\Images\Vector Addition.png" alt="Vector Addition" style="zoom:67%;" />

### Cartesian Coordinates

笛卡儿坐标

X and Y can be any (usually orthogonal unit) vectors
X和Y可以是任意(通常是正交的单位)向量
$$
A = \begin{pmatrix}x \\y \\\end{pmatrix} \ \ \ \
A^T = \begin{pmatrix}x & y \\\end{pmatrix} \ \ \ \
||A|| = \sqrt{x^2 + y^2}
$$
<img src="\Images\Cartesian Coordinates.png" alt="Cartesian Coordinates" style="zoom:67%;" />

### Vector Multiplication

- Dot product 点乘
- Cross product 叉乘
- Orthonormal bases and coordinate frames 标准正交基和坐标系

#### Dot product

向量点乘是一个数

用法：算出两个向量之间的夹角

<img src="\Images\Dot Product.png" alt="Dot Product" style="zoom:33%;" />
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

<img src="G:\笔记\Markdown\GameDevelopment\GAMES101 现代计算机图形学入门\Images\Dot Product for Projection.png" alt="Dot Product for Projection" style="zoom:50%;" />

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

<img src="\Images\Determine Forward Backward.png" alt="Determine Forward Backward" style="zoom:50%;" />

#### Cross product

<img src="\Images\Cross Product.png" alt="Cross Product" style="zoom:50%;" />

- Cross product is orthogonal to two initial vectors
  向量积与两个初始向量正交
- Direction determined by right-hand rule
  方向由右手定则(右手顺时针旋转)决定
- Useful in constructing coordinate systems (later)
  用于构造坐标系统(稍后)

$$
\vec{a} \cross {\vec{b}} = \begin{pmatrix}
	y_bz_b - y_bz_a \\
	z_ax_b - x_az_b \\
	x_ay_b - y_ax_b
\end{pmatrix} \\

\vec{a} \cross {\vec{b}} = A\vec{b} = \begin{pmatrix}
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

<img src="\Images\Cross Product in Graphics.png" alt="Cross" style="zoom: 50%;" />

左图在右手坐标系下，使用顺时针旋转，$\vec{b}$ 在$\vec{a}$的左侧，$\vec{a} \cross \vec{b} > 0$
右图，$\overrightarrow{AB} \cross \overrightarrow{AP}、\overrightarrow{BC} \cross \overrightarrow{BP}、\overrightarrow{CA} \cross \overrightarrow{CP}$，如果全为正/负，则P点在内部，否则在外部



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
\vec{w} = \vec{u} \cross \vec{v} \ \ \  (right-handed) \\
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
I_{3 \cross 3} = \begin{pmatrix}
	1 & 0 & 0 \\
	0 & 1 & 0 \\
    0 & 0 & 1
\end{pmatrix} \\ 
AA^{-1} = A^{-1}A = I \\
(AB)^{-1} = B^{-1}A^{-1} 
$$



# Transformation

