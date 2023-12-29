# 6  Transformation Matrices 变换矩阵

The machinery of linear algebra can be used to express many of the operations required to arrange objects in a 3D scene, view them with cameras, and get them onto the screen. Geometric transformations like rotation, translation, scaling, and projection can be accomplished with matrix multiplication, and the transformation matrices used to do this are the subject of this chapter.
线性代数机制可用于表达在 3D 场景中排列对象、使用相机查看它们并将它们显示到屏幕上所需的许多操作。 旋转、平移、缩放和投影等几何变换可以通过矩阵乘法来完成，用于执行此操作的变换矩阵是本章的主题。

We will show how a set of points transforms if the points are represented as offset vectors from the origin, and we will use the clock shown in Figure 6.1 as an example of a point set. So think of the clock as a bunch of points that are the ends of vectors whose tails are at the origin. We also discuss how these transforms operate differently on locations (points), displacement vectors, and surface normal vectors. 
我们将展示一组点在以偏移向量形式表示时的变换过程，而我们将以图 6.1 中显示的时钟作为点集的示例。因此，可以将时钟视为一群点，这些点是向量的端点，而这些向量的起点位于原点。我们还将讨论这些变换如何在位置（点）、位移向量和表面法向量上产生不同的效果。

## 6.1 2D Linear Transformations 二维线性变换

We can use a 2 × 2 matrix to change, or transform, a 2D vector: 
我们可以使用 2 × 2 矩阵来更改或变换 2D 向量：
$$
\begin{bmatrix}
a_{11} & a_{12} \\
a_{21} & aa_{22} \\
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
 = \begin{bmatrix}
 a_{11}x + a_{12}y \\
 a_{21}x + a_{22}y
 \end{bmatrix}
$$
This kind of operation, which takes in a 2-vector and produces another 2-vector by a simple matrix multiplication, is a linear transformation. 
这种操作接受一个二维向量，并通过简单的矩阵乘法生成另一个二维向量，被称为线性变换。

By this simple formula we can achieve a variety of useful transformations, depending on what we put in the entries of the matrix, as will be discussed in the following sections. For our purposes, consider moving along the x-axis a horizontal move and along the y-axis, a vertical move.
通过这个简单的公式，我们可以实现各种有用的变换，取决于我们在矩阵的各个元素中输入了什么，这将在接下来的章节中进行讨论。在我们的讨论中，沿着 x 轴的移动被视为水平移动，沿着 y 轴的移动被视为垂直移动。

### 6.1.1 Scaling 缩放

The most basic transform is a scale along the coordinate axes. This transform can change length and possibly direction: 
最基本的变换是沿坐标轴的缩放。这种变换可以改变长度，可能也会影响方向：
$$
scale(s_x, s_y) = \begin{bmatrix}
s_x & 0 \\
0 & s_y
\end{bmatrix}
$$
Note what this matrix does to a vector with Cartesian components $(x, y)$: 
请注意该矩阵对具有笛卡尔分量 $(x, y)$ 的向量的作用：
$$
\begin{bmatrix}
s_x & 0 \\
0 & s_y
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
= \begin{bmatrix}
s_xx \\
s_yy
\end{bmatrix}
$$
So, just by looking at the matrix of an axis-aligned scale, we can read off the two scale factors. 
因此，仅仅通过观察轴对齐缩放的矩阵，我们就能够读取出两个缩放因子。

Example. The matrix that shrinks x and y uniformly by a factor of two is (Figure 6.1) 
例子  将 x 和 y 均匀缩小两倍的矩阵为（图 6.1）
$$
scale(0.5, 0.5) = \begin{bmatrix}
0.5 & 0 \\
0 & 0.5
\end{bmatrix}
$$
<img src=".\Images\Figure 6.1.png" alt="Figure 6.1" style="zoom:50%;" />
Figure 6.1. Scaling uniformly by half for each axis: The axis-aligned scale matrix has the proportion of change in each of the diagonal elements and zeroes in the off-diagonal elements. 
图 6.1：每个轴均匀缩小一半的比例尺度。与轴对齐的比例矩阵在对角元素中反映了变化的比例，而在非对角元素中则保持为零。

A matrix which halves in the horizontal and increases by three-halves in the vertical is (see Figure 6.2) 
一个矩阵，在水平方向减半，垂直方向增加二分之一，详见（见图6.2）。
$$
scale(0.5, 1.5) = \begin{bmatrix}
0.5 & 0 \\
0 & 1.5
\end{bmatrix}
$$
<img src=".\Images\Figure 6.2.png" alt="Figure 6.2" style="zoom:50%;" />
Figure 6.2. Scaling nonuniformly in x and y: The scaling matrix is diagonal with non-equal elements. Note that the square outline of the clock becomes a rectangle and the circular face becomes an ellipse. 
图 6.2 x 和 y 上的非均匀缩放：缩放矩阵是具有不相等元素的对角矩阵。 请注意，时钟的方形轮廓变成了矩形，圆形面变成了椭圆形。

### 6.1.2 Shearing 剪切

A shear is something that pushes things sideways, producing something like a deck of cards across which you push your hand; the bottom card stays put and cards move more the closer they are to the top of the deck. The horizontal and vertical shear matrices are 
剪切是一种使物体侧向移动的变换，犹如你在卡牌堆上推动手的动作；底部的卡片保持原位，而越靠近牌堆顶部的卡片移动得越多。水平和垂直剪切矩阵分别是
$$
shear-x(s) = \begin{bmatrix}
1 & s \\
0 & 1
\end{bmatrix} \ \ \ \
shear-y(s) = \begin{bmatrix}
1 & 0 \\
s & 1
\end{bmatrix}
$$
Example. The transform that shears horizontally so that vertical lines become $45◦$ lines leaning toward the right is (see Figure 6.3) 
例子。 水平剪切使垂直线变成向右倾斜的 $45°$ 线的变换是（见图 6.3）
$$
shear-x(1) = \begin{bmatrix}
1 & 1 \\
0 & 1
\end{bmatrix}
$$
<img src=".\Images\Figure 6.3.png" alt="Figure 6.3" style="zoom:67%;" />
Figure 6.3. An x-shear matrix moves points to the right in proportion to their y-coordinate. Now the square outline of the clock becomes a parallelogram and, as with scaling, the circular face of the clock becomes an ellipse. 
图 6.3  x 剪切矩阵将点按与其 y 坐标成比例向右移动。 现在，时钟的方形轮廓变成了平行四边形，并且与缩放一样，时钟的圆形面变成了椭圆形。

An analogous transform vertically is (see Figure 6.4) 
类似的垂直变换是（见图 6.4）
<img src=".\Images\Figure 6.4.png" alt="Figure 6.4" style="zoom:67%;" />
$$
shear-y(1) = \begin{bmatrix}
1 & 0 \\
1 & 1
\end{bmatrix}
$$
In both cases, the square outline of the sheared clock becomes a parallelogram,  and the circular face of the sheared clock becomes an ellipse. 
在这两种情况下，剪切时钟的方形轮廓变成平行四边形，剪切时钟的圆形面变成椭圆形。

> In fact, the image of a circle under any matrix transformation is an ellipse. 
> 事实上，圆在任何矩阵变换下的图像都是椭圆。

Another way to think of a shear is in terms of rotation of only the vertical (or horizontal) axis. The shear transform that takes a vertical axis and tilts it clockwise by an angle $φ$ is 
考虑剪切的另一种方式是仅垂直（或水平）轴的旋转。 采用垂直轴并将其顺时针倾斜角度 $φ$ 的剪切变换为
$$
\begin{bmatrix}
1 & \tanφ \\
0 & 1 
\end{bmatrix}
$$
Similarly, the shear matrix which rotates the horizontal axis counterclockwise by angle $φ$ is
类似地，水平轴逆时针旋转角度$φ$的剪切矩阵为
$$
\begin{bmatrix}
1 & 0\\
\tanφ & 1
\end{bmatrix}
$$

### 6.1.3 Rotation 旋转

Suppose we want to rotate a vector $\bold{a}$ by an angle $φ$ counterclockwise to get vector $\bold{b}$ (Figure 6.5). If $\bold{a}$ makes an angle $α$ with the x-axis, and its length is $r = \sqrt{x^2_a + y^2_a}$, then we know that
假设我们想要逆时针旋转向量 $\bold{a}$ 以得到向量 $\bold{b}$（见图6.5）。如果 $\bold{a}$ 与 x 轴的夹角为 $α$，且其长度为 $r = \sqrt{x^2_a + y^2_a}$，那么我们知道
$$
x_a = r \cos α, \\
y_a = r \sin α
$$
<img src=".\Images\Figure 6.5.png" alt="Figure 6.5" style="zoom:67%;" />
Figure 6.5. The geometry for Equation (6.1). 
图 6.5  方程（6.1）的几何形状。

Because $\bold{b}$ is a rotation of $\bold{a}$, it also has length $r$. Because it is rotated an angle $φ$ from $\bold{a}$, $\bold{b}$ makes an angle $(α + φ)$ with the x-axis. Using the trigonometric addition identities (Section 2.3.3):
因为 $\bold{b}$ 是 $\bold{a}$ 的旋转，所以它也有长度 $r$。 因为它从 $\bold{a}$ 旋转了角度 $φ$，所以 $\bold{b}$ 与 x 轴形成角度 $(α + φ)$。 使用三角加法恒等式（第 2.3.3 节）：
$$
x_b = r \cos(α + φ) = r \cos α \cos φ − r \sin α \sin φ, \\
y_b = r \sin(α + φ) = r \sin α \cos φ + r \cos α \sin φ. \\
(6.1)
$$
Substituting $x_a = r \cos α$ and $y_a = r \sin α$ gives
代入 $x_a = r \cos α$ 和 $y_a = r \sin α$ 给出
$$
x_b = x_a \cos φ − y_a \sin φ, \\
y_b = y_a \cos φ + x_a \sin φ.
$$
In matrix form, the transformation that takes $\bold{a}$ to $\bold{b}$ is then
以矩阵形式，$\bold{a}$ 到 $\bold{b}$ 的变换为
$$
rotate(φ) = \begin{bmatrix}
\cos φ & -\sin φ \\
\sin φ & \cos φ
\end{bmatrix}
$$
Example. A matrix that rotates vectors by $π/4$ radians (45 degrees) is (see Figure 6.6) 
例子.  将向量旋转 $π/4$ 弧度（45 度）的矩阵为（见图 6.6）
$$
\begin{bmatrix}
\cos \frac{\pi}{4} & -\sin \frac{\pi}{4} \\
\sin \frac{\pi}{4} & \cos \frac{\pi}{4}
\end{bmatrix}
= \begin{bmatrix}
0.707 & -0.707 \\
0.707 & 0.707
\end{bmatrix}
$$
<img src=".\Images\Figure 6.6.png" alt="Figure 6.6" style="zoom:67%;" />
Figure 6.6. A rotation by $45◦$. Note that the rotation is counterclockwise and that $cos(45◦) = sin(45◦) ≈ .707$. 
图 6.6. 旋转$45°$。 请注意，旋转是逆时针的，并且 $cos(45°) = sin(45°) ≈ .707$。

A matrix that rotates by $π/6$ radians (30 degrees) in the clockwise direction is a rotation by $-π/6$ radians in our framework (see Figure 6.7): 
在我们的框架中，顺时针方向旋转 $π/6$ 弧度（30 度）的矩阵是旋转 $-π/6$ 弧度（见图 6.7）：
$$
\begin{bmatrix}
\cos \frac{-\pi}{6} & -\sin \frac{-\pi}{6} \\
\sin \frac{-\pi}{6} & \cos \frac{-\pi}{6}
\end{bmatrix}
= \begin{bmatrix}
0.866 & 0.5 \\
-0.5 & 0.866
\end{bmatrix}
$$
<img src=".\Images\Figure 6.7.png" alt="Figure 6.7" style="zoom:67%;" />
Figure 6.7. A rotation by –30 degrees. Note that the rotation is clockwise and that $cos(–30◦) ≈ .866$ and $sin(–30◦) = –.5$. 
图 6.7.  旋转 –30 度。 请注意，旋转为顺时针方向，并且 $cos(–30°) ≈ .866$ 且 $sin(–30°) = –.5$。

Because the norm of each row of a rotation matrix is one $(sin^2 φ+cos^2 φ = 1)$, and the rows are orthogonal $(cos φ(- sin φ) + sin φ cos φ = 0)$, we see that rotation matrices are orthogonal matrices (Section 5.2.4). By looking at the matrix we can read off two pairs of orthonormal vectors: the two columns, which are the vectors to which the transformation sends the canonical basis vectors $(1, 0)$ and $(0, 1)$; and the rows, which are the vectors that the transformations sends to the canonical basis vectors. 
因为旋转矩阵每行的范数都为一 $(\sin^2 φ + \cos^2 φ = 1)$，而且行之间正交 $(\cos φ(-\sin φ) + \sin φ \cos φ = 0)$，我们可以得知旋转矩阵是正交矩阵（详见5.2.4节）。通过观察矩阵，我们可以推断出两组正交归一的向量：首先是两列，它们分别是变换送至规范基向量 $(1, 0)$ 和 $(0, 1)$ 的向量；其次是行，它们是变换送至规范基向量的向量。

> Said briefly, $\bold{R}\bold{e}_i = \bold{u}_i$ and $\bold{R}\bold{v}_i = \bold{u}_i$, for a rotation with columns $\bold{u}_i$ and rows $\bold{v}_i$. 
> 简单地说，$\bold{R}\bold{e}_i = \bold{u}_i$ 和 $\bold{R}\bold{v}_i = \bold{u}_i$，用于列旋转 $\bold{u}_i$ 和行 $\bold{v}_i$。

### 6.1.4 Reflection 反射

We can reflect a vector across either of the coordinate axes by using a scale with one negative scale factor (see Figures 6.8 and 6.9): 
我们可以通过使用一个负的比例因子来沿着坐标轴的任一方向对向量进行反射（参见图6.8和6.9）：
$$
reflect-y = \begin{bmatrix}
-1 & 0 \\
0 & 1
\end{bmatrix} \ \ \ \ \ \ 
reflect-x = \begin{bmatrix}
1 & 0 \\
0 & -1
\end{bmatrix}
$$
![Figure 6.8](.\Images\Figure 6.8.png)
Figure 6.8. A reflection about the y-axis is achieved by multiplying all x-coordinates by $–1$. 
图 6.8 通过将所有 x 坐标乘以 $–1$ 来实现关于 y 轴的反射。

<img src=".\Images\Figure 6.9.png" alt="Figure 6.9" style="zoom:67%;" />
Figure 6.9. A reflection about the x-axis is achieved by multiplying all y-coordinates by $–1$.
图 6.9 关于 x 轴的反射是通过将所有 y 坐标乘以 $–1$ 来实现的。

While one might expect that the matrix with $-1$ in both elements of the diagonal is also a reflection, in fact it is just a rotation by $π$ radians. 
虽然人们可能认为对角线两个元素中都有 $-1$ 的矩阵也是一种反射，但实际上它只是旋转 $π$ 弧度。

> This rotation can also be called a “reflection through the origin.” 
> 这种旋转也可以称为“通过原点的反射”。

### 6.1.5 Composition and Decomposition of Transformations 变换的组合和分解

It is common for graphics programs to apply more than one transformation to an object. For example, we might want to first apply a scale $\bold{S}$, and then a rotation $\bold{R}$. This would be done in two steps on a 2D vector $\bold{v}_1$: 
图形程序对一个对象应用多个变换是很常见的。 例如，我们可能想首先应用缩放 $\bold{S}$，然后应用旋转 $\bold{R}$。 这可以在 2D 矢量 $\bold{v}_1$ 上分两步完成：
$first,\bold{v}_2 = \bold{S}\bold{v}_1, then,\bold{v}_3 = \bold{R}\bold{v}_2.  $

Another way to write this is
另一种写法是
$\bold{v}_3 = \bold{R}(\bold{S}\bold{v}_1)   $

Because matrix multiplication is associative, we can also write
因为矩阵乘法是结合律，所以我们也可以写成
$\bold{v}_3 = (\bold{R}\bold{S})\bold{v}_1 $

In other words, we can represent the effects of transforming a vector by two matrices in sequence using a single matrix of the same size, which we can compute by multiplying the two matrices: $\bold{M} = \bold{R}\bold{S}$ (Figure 6.10).
换句话说，我们可以使用相同大小的单个矩阵来表示按顺序将向量变换为两个矩阵的效果，我们可以通过将两个矩阵相乘来计算： $\bold{M} = \bold{R}\bold{S}$（图6.10）。
<img src=".\Images\Figure 6.10.png" alt="Figure 6.10" style="zoom:67%;" />
Figure 6.10. Applying the two transform matrices in sequence is the same as applying the product of those matrices once. This is a key concept that underlies most graphics hardware and software. 
图 6.10  按顺序应用两个变换矩阵与应用一次这些矩阵的乘积相同。这是大多数图形硬件和软件的关键概念。

It is very important to remember that these transforms are applied from the right side first. So the matrix $\bold{M} = \bold{R}\bold{S}$ first applies $\bold{S}$ and then $\bold{R}$. 
请记住，这些变换首先从右侧应用，这一点非常重要。 因此矩阵 $\bold{M} = \bold{R}\bold{S}$ 首先应用 $\bold{S}$，然后应用 $\bold{R}$。

Example. Suppose we want to scale by one-half in the vertical direction and then rotate by $π/4$ radians (45 degrees). The resulting matrix is
例子. 假设我们要在垂直方向缩放二分之一，然后旋转 $π/4$ 弧度（45 度）。 得到的矩阵是
$$
\begin{bmatrix}
0.707 & -0.707 \\
0.707 & 0.707
\end{bmatrix}
\begin{bmatrix}
1 & 0 \\
0 & 0.5
\end{bmatrix}
= \begin{bmatrix}
0.707 & -0.353 \\
0.707 & 0.353
\end{bmatrix}
$$
It is important to always remember that matrix multiplication is not commutative. So the order of transforms does matter. In this example, rotating first, and then scaling, results in a different matrix (see Figure 6.11): 
重要的是要始终记住矩阵乘法是**不可交换**的。 所以转换的顺序很重要。 在此示例中，先旋转，然后缩放，会产生不同的矩阵（参见图 6.11）：
$$
\begin{bmatrix}
1 & 0 \\
0 & 0.5
\end{bmatrix}
\begin{bmatrix}
0.707 & -0.707 \\
0.707 & 0.707
\end{bmatrix}
= \begin{bmatrix}
0.707 & -0.707 \\
0.353 & 0.353
\end{bmatrix}
$$
![Figure 6.11](.\Images\Figure 6.11.png)

Figure 6.11. The order in which two transforms are applied is usually important. In this example, we do a scale by one-half in y and then rotate by $45◦$. Reversing the order in which these two transforms are applied yields a different result. 
图 6.11  应用两个变换的顺序通常很重要。 在此示例中，我们将 y 缩放二分之一，然后旋转 $45°$。 颠倒这两个变换的应用顺序会产生不同的结果。

Example. Using the scale matrices we have presented, nonuniform scaling can only be done along the coordinate axes. If we wanted to stretch our clock by 50% along one of its diagonals, so that 8:00 through 1:00 move to the northwest and 2:00 through 7:00 move to the southeast, we can use rotation matrices in combination with an axis-aligned scaling matrix to get the result we want. The idea is to use a rotation to align the scaling axis with a coordinate axis, then scale along that axis, then rotate back. In our example, the scaling axis is the “backslash” diagonal of the square, and we can make it parallel to the x-axis with  a rotation by $+45◦$. Putting these operations together, the full transformation is
举例说明：利用我们提供的比例矩阵，非均匀缩放只能沿坐标轴进行。如果我们想要沿钟表的对角线之一将其拉伸50%，使8:00到1:00的部分向西北移动，而2:00到7:00的部分向东南移动，我们可以使用旋转矩阵与与轴对齐的缩放矩阵相结合，以获得我们想要的结果。思路是使用旋转将缩放轴与坐标轴对齐，然后沿着该轴进行缩放，最后再旋转回来。在我们的例子中，缩放轴是正方形的“反斜杠”对角线，我们可以通过+45度的旋转使其与x轴平行。将这些操作组合在一起，完整的变换是：
$rotate(-45◦) scale(1.5, 1) rotate(45◦)  $

> Remember to read the transformations from right to left. 
> 请记住从右到左阅读转换。

In mathematical notation, this can be written $\bold{R}\bold{S}\bold{R}^T$. The result of multiplying the three matrices together is
用数学符号来说，这可以写成$\bold{R}\bold{S}\bold{R}^T$。 三个矩阵相乘的结果是
$$
\begin{bmatrix}
1.25 & -0.25 \\
-0.25 & 1.25
\end{bmatrix}
$$

> It is no coincidence that this matrix is symmetric— try applying the transpose-of-product rule to the for mula $\bold{R}\bold{S}\bold{R}^T$.
> 该矩阵是对称的并非巧合 - 尝试将乘积转置规则应用于公式 $\bold{R}\bold{S}\bold{R}^T$。

Building up a transformation from rotation and scaling transformations actually works for any linear transformation, and this fact leads to a powerful way of thinking about these transformations, as explored in the next section.
从旋转和缩放变换构建变换实际上适用于任何线性变换，这一事实导致了一种思考这些变换的强大方法，如下一节所述。

### 6.1.6 Decomposition of Transformations  变换的分解

Sometimes it’s necessary to “undo” a composition of transformations, taking a transformation apart into simpler pieces. For instance, it’s often useful to present a transformation to the user for manipulation in terms of separate rotations and scale factors, but a transformation might be represented internally simply as a  matrix, with the rotations and scales already mixed together. This kind of manipulation can be achieved if the matrix can be computationally disassembled into the desired pieces, the pieces adjusted, and the matrix reassembled by multiplying the pieces together again.
有时候，需要“撤销”一系列的变换，将一个变换分解为更简单的部分。例如，通常有必要将一个变换呈现给用户以便通过单独的旋转和缩放因子进行操作，但在内部，一个变换可能被简单地表示为一个矩阵，其中旋转和缩放已经混合在一起。这种操作可以通过将矩阵计算上解构成所需的部分，调整这些部分，然后通过再次相乘这些部分来重新组装矩阵。

It turns out that this decomposition, or factorization, is possible, regardless of the entries in the matrix—and this fact provides a fruitful way of thinking about transformations and what they do to geometry that is transformed by them.
事实证明，这种分解或因式分解是可能的，而与矩阵中的条目无关——这一事实为思考变换及其对所受变换的几何形状产生的影响提供了一种富有成果的方式。

#### Symmetric Eigenvalue Decomposition 对称特征值分解

Let’s start with symmetric matrices. Recall from Section 5.4 that a symmetric matrix can always be taken apart using the eigenvalue decomposition into a product of the form 
让我们从对称矩阵开始。 回想一下 5.4 节，对称矩阵总是可以使用特征值分解分解为以下形式的乘积
$\bold{A} = \bold{R}\bold{S}\bold{R}^T  $

where $\bold{R}$ is an orthogonal matrix and $\bold{S}$ is a diagonal matrix; we will call the columns of $\bold{R}$ (the eigenvectors) by the names $\bold{v}_1$ and $\bold{v}_2$, and we’ll call the diagonal entries of $\bold{S}$ (the eigenvalues) by the names $λ_1$ and $λ_2$. 
其中，$\bold{R}$ 是一个正交矩阵，$\bold{S}$ 是一个对角矩阵；我们将称$\bold{R}$的列（特征向量）为$\bold{v}_1$和$\bold{v}_2$，而将$\bold{S}$的对角元素（特征值）称为$λ_1$和$λ_2$。

In geometric terms we can now recognize $\bold{R}$ as a rotation and $\bold{S}$ as a scale, sot his is just a multi-step geometric transformation (Figure 6.13): 
从几何学的角度来看，我们现在可以将$\bold{R}$识别为旋转，而$\bold{S}$则为缩放，因此这只是一个多步的几何变换（见图6.13）：

1. Rotate $\bold{v}_1$ and $\bold{v}_2$ to the x- and y-axes (the transform by $R^T$).
   将 $\bold{v}_1$ 和 $\bold{v}_2$ 旋转到 x 轴和 y 轴（通过 $R^T$ 进行变换）。
2. Scale in $x$ and $y$ by $(λ_1, λ_2)$ (the transform by $\bold{S}$).
   按 $(λ_1, λ_2)$ 缩放 $x$ 和 $y$（通过 $\bold{S}$ 进行变换）。
3. Rotate the x- and y-axes back to $\bold{v}_1$ and $\bold{v}_2$ (the transform by $\bold{R}$). 
   将 x 轴和 y 轴旋转回 $\bold{v}_1$ 和 $\bold{v}_2$（通过 $\bold{R}$ 进行变换）。

> If you like to count dimensions: a symmetric 2 × 2 matrix has 3 degrees of freedom, and the eigenvalue decomposition rewrites them as a rotation angle and two scale factors. 
> 如果你喜欢计算维度：对称的 2 × 2 矩阵有 3 个自由度，特征值分解将它们重写为旋转角度和两个比例因子。

<img src=".\Images\Figure 6.13.png" alt="Figure 6.13" style="zoom:67%;" />
Figure 6.13. What happens when the unit circle is transformed by an arbitrary symmetric matrix $\bold{A}$, also known as a non–axis-aligned, nonuniform scale. The two perpendicular vectors $\bold{v}_1$ and $\bold{v}_2$, which are the eigenvectors of $\bold{A}$, remain fixed in direction but get scaled. In terms of elementary transformations, this can be seen as first rotating the eigenvectors to the canonical basis, doing an axis-aligned scale, and then rotating the canonical basis back to the eigenvectors. 
图6.13：当单位圆被一个任意对称矩阵$\bold{A}$（也被称为非轴对齐、非均匀缩放）变换时会发生什么。两个垂直的向量$\bold{v}_1$和$\bold{v}_2$，它们是$\bold{A}$的特征向量，方向保持不变但发生了缩放。从基本的变换角度来看，这可以看作是首先将特征向量旋转到规范基，进行一个轴对齐的缩放，然后将规范基旋转回特征向量。

Looking at the effect of these three transforms together, we can see that they have the effect of a nonuniform scale along a pair of axes. As with an axis-aligned scale, the axes are perpendicular, but they aren’t the coordinate axes; instead they  are the eigenvectors of $\bold{A}$. This tells us something about what it means to be a symmetric matrix: symmetric matrices are just scaling operations—albeit potentially nonuniform and non–axis-aligned ones. 
观察这三种变换的综合效果，我们可以看到它们产生了沿着一对轴的非均匀缩放的效果。与轴对齐缩放一样，这些轴是垂直的，但它们不是坐标轴；相反，它们是$\bold{A}$的特征向量。这告诉我们一些关于对称矩阵的特性：对称矩阵实质上就是缩放操作——尽管可能是非均匀和非轴对齐的。

Example. Recall the example from Section 5.4: 
例子。 回想一下 5.4 节中的例子：
$$
\ \begin{bmatrix}
2 & 1 \\
1 & 1
\end{bmatrix}
= \bold{R}\begin{bmatrix}
λ_1 & 0 \\
0 & λ_2
\end{bmatrix}\bold{R}^T
= \begin{bmatrix}
0.8507 & -0.5257 \\
0.5257 & 0.8507
\end{bmatrix}
\begin{bmatrix}
2.618 & 0 \\
0 & 0.382
\end{bmatrix}
\begin{bmatrix}
0.8507 & 0.5257 \\
-0.5257 & 0.8507
\end{bmatrix} \\
= rotate (31.7◦) scale (2.618, 0.382) rotate (−31.7◦).
$$
The matrix above, then, according to its eigenvalue decomposition, scales in a direction $31.7◦$ counterclockwise from three o’clock (the x-axis). This is a touch before 2 p.m. on the clockface as is confirmed by Figure 6.14. 
因此，根据其特征值分解，上述矩阵在一个距离三点钟（x轴）逆时针$31.7◦$的方向上进行缩放。这对应时钟表上稍早于下午2点的位置，如图6.14所示所证实的那样。<img src=".\Images\Figure 6.14.png" alt="Figure 6.14" style="zoom:80%;" />
Figure 6.14. A symmetric matrix is always a scale along some axis. In this case it is along the $φ = 31.7◦$ direction which means the real eigenvector for this matrix is in that direction. 
图 6.14  对称矩阵始终是沿某个轴的尺度。 在这种情况下，它沿着 $φ = 31.7°$ 方向，这意味着该矩阵的真实特征向量在该方向上。

We can also reverse the diagonalization process; to scale by $(λ_1, λ_2)$ with the first scaling direction an angle $φ$ clockwise from the x-axis, we have
我们同样可以逆转对角化的过程；要按照$(λ_1, λ_2)$的比例进行缩放，其中第一个缩放方向与x轴逆时针形成一个角度$φ$，我们可以如下操作：
$$
\ \begin{bmatrix}
\cos φ & \sin φ \\
-\sin φ & \cos φ 
\end{bmatrix}
\begin{bmatrix}
λ_1 & 0 \\
0 & λ_2
\end{bmatrix}
\begin{bmatrix}
\cos φ & -\sin φ \\
\sin φ & \cos φ 
\end{bmatrix} = \\
\begin{bmatrix}
λ_1\cos^2 φ + λ_2\sin^2φ & (λ_2 - λ_1)\cos φ\sin φ\\
(λ_2 - λ_1)\cos φ\sin φ & λ_2 \cos^2 φ + λ_1 \sin^2 φ\\ 
\end{bmatrix}
$$
We should take heart that this is a symmetric matrix as we know must be true since we constructed it from a symmetric eigenvalue decomposition. 
我们应该振奋起来，因为这是一个对称矩阵，正如我们所知，因为我们是从对称的特征值分解中构造出它的。

#### Singular Value Decomposition 奇异值分解

A very similar kind of decomposition can be done with nonsymmetric matrices as well: it’s the Singular Value Decomposition (SVD), also discussed in Section 5.4.1. The difference is that the matrices on either side of the diagonal matrix are no longer the same: 
同样，对于非对称矩阵，我们也可以进行一种非常相似的分解：这就是奇异值分解（Singular Value Decomposition，SVD），在第5.4.1节中也有讨论。区别在于对角矩阵两侧的矩阵不再相同：
$\bold{A} = \bold{U}\bold{S}\bold{V}^T  $

The two orthogonal matrices that replace the single rotation $\bold{R}$ are called $\bold{U}$ and $\bold{V}$, and their columns are called $\bold{u}_i$ (the left singular vectors) and $\bold{v}_i$ (the right singular vectors), respectively. In this context, the diagonal entries of $\bold{S}$ are called singular values rather than eigenvalues. The geometric interpretation is very similar to that of the symmetric eigenvalue decomposition (Figure 6.15): 
取代单一旋转$\bold{R}$的两个正交矩阵分别被称为$\bold{U}$和$\bold{V}$，它们的列分别被称为$\bold{u}_i$（左奇异向量）和$\bold{v}_i$（右奇异向量）。在这个背景下，$\bold{S}$的对角元素被称为奇异值，而非特征值。几何解释与对称特征值分解非常相似（见图6.15）：

1. Rotate $\bold{v}_1$ and $\bold{v}_2$ to the x- and y-axes (the transform by $\bold{V}^T$).
   将 $\bold{v}_1$ 和 $\bold{v}_2$ 旋转到 x 轴和 y 轴（通过 $\bold{V}^T$ 进行变换）。
2. Scale in $x$ and $y$ by $(σ_1, σ_2)$ (the transform by $\bold{S}$).
   按 $(σ_1, σ_2)$ 缩放 $x$ 和 $y$（通过 $\bold{S}$ 进行变换）。
3. Rotate the x- and y-axes to $\bold{u}_1$ and $\bold{u}_2$ (the transform by $\bold{U}$). 
   将 x 轴和 y 轴旋转到 $\bold{u}_1$ 和 $\bold{u}_2$（通过 $\bold{U}$ 进行变换）。

> For dimension counters: a general 2 × 2 matrix has 4 degrees of freedom, and the SVD rewrites them as two rotation angles and two scale factors. One more bit is needed to keep track of reflections, but that doesn’t add a dimension. 
> 对于维度计数：一般的2 × 2矩阵有4个自由度，而奇异值分解将其重新表示为两个旋转角度和两个缩放因子。需要额外的一个位来跟踪反射，但这并不增加一个维度。

![Figure 6.15](.\Images\Figure 6.15.png)
Figure 6.15. What happens when the unit circle is transformed by an arbitrary matrix $\bold{A}$. The two perpendicular vectors $\bold{v}_1$ and $\bold{v}_2$, which are the right singular vectors of $\bold{A}$, get scaled and changed in direction to match the left singular vectors, $\bold{u}_1$ and $\bold{u}_2$. In terms of elementary transformations, this can be seen as first rotating the right singular vectors to the canonical basis, doing an axis-aligned scale, and then rotating the canonical basis to the left singular vectors. 
图6.15：当单位圆被任意矩阵$\bold{A}$变换时会发生什么。两个垂直的向量$\bold{v}_1$和$\bold{v}_2$，它们是$\bold{A}$的右奇异向量，发生了缩放并改变方向以匹配左奇异向量$\bold{u}_1$和$\bold{u}_2$。从基本的变换角度来看，这可以理解为首先将右奇异向量旋转到规范基，进行一个轴对齐的缩放，然后将规范基旋转到左奇异向量。

The principal difference is between a single rotation and two different orthogonal matrices. This difference causes another, less important, difference. Because the SVD has different singular vectors on the two sides, there is no need for negative singular values: we can always flip the sign of a singular value, reverse the direction of one of the associated singular vectors, and end up with the same transformation again. For this reason, the SVD always produces a diagonal matrix with all positive entries, but the matrices $\bold{U}$ and $\bold{V}$ are not guaranteed to be rotations—they could include reflection as well. In geometric applications like graphics this is an inconvenience, but a minor one: it is easy to differentiate rotations from reflections by checking the determinant, which is +1 for rotations and −1 for reflections, and if rotations are desired, one of the singular values can be negated, resulting in a rotation–scale–rotation sequence where the reflection is rolled in with the scale, rather than with one of the rotations.
主要的区别在于单一旋转和两个不同的正交矩阵之间。这种差异导致了另一个较不重要的区别。由于SVD在两侧具有不同的奇异向量，因此不需要负奇异值：我们始终可以改变奇异值的符号，反转相关奇异向量之一的方向，从而再次得到相同的变换。因此，SVD总是产生一个具有全部正数元素的对角矩阵，但不能保证矩阵$\bold{U}$和$\bold{V}$是旋转矩阵——它们也可能包含反射。在图形等几何应用中，这可能有些不便，但不是很大的问题：可以通过检查行列式来轻松区分旋转和反射，旋转的行列式为+1，反射的行列式为−1，如果需要旋转，则可以否定其中一个奇异值，从而得到旋转-缩放-旋转的顺序，其中反射被包含在缩放中，而不是在其中一个旋转中。

Example. The example used in Section 5.4.1 is in fact a shear matrix (Figure 6.12): 
例子。 5.4.1 节中使用的示例实际上是一个剪切矩阵（图 6.12）：
$$
\ \begin{bmatrix}
1 & 1 \
0 & 1
\end{bmatrix} = \bold{R}_2 \begin{bmatrix}
σ_1 & 0 \\
0 & σ_2
\end{bmatrix} \bold{R}_1 \\
= \begin{bmatrix}
0.8507 & -0.5257 \\
0.5257 & 0.8507
\end{bmatrix}
\begin{bmatrix}
1.618 & 0 \\
0 & 0.618
\end{bmatrix}
\begin{bmatrix}
0.5257 & 0.8507 \\
-0.8507 & 0.5257
\end{bmatrix} \\
= rotate (31.7◦) scale (1.618, 0.618) rotate (−58.3◦).
$$
<img src=".\Images\Figure 6.12.png" alt="Figure 6.12" style="zoom:50%;" />
Figure 6.12. Singular Value Decomposition (SVD) for a shear matrix. Any 2D matrix can be decomposed into a product of rotation, scale, rotation. Note that the circular face of the clock must become an ellipse because it is just a rotated and scaled circle. 
图 6.12。 剪切矩阵的奇异值分解 (SVD)。任何二维矩阵都可以分解为旋转、缩放、旋转的乘积。请注意，时钟的圆形面必须变成椭圆形，因为它只是一个旋转和缩放的圆。

An immediate consequence of the existence of SVD is that all the 2D transformation matrices we have seen can be made from rotation matrices and scale matrices. Shear matrices are a convenience, but they are not required for expressing transformations. 
SVD 存在的直接后果是我们所看到的所有 2D 变换矩阵都可以由旋转矩阵和缩放矩阵组成。 剪切矩阵很方便，但它们不是表达变换所必需的。

In summary, every matrix can be decomposed via SVD into a rotation times a scale times another rotation. Only symmetric matrices can be decomposed via eigenvalue diagonalization into a rotation times a scale times the inverse-rotation, and such matrices are a simple scale in an arbitrary direction. The SVD of a symmetric matrix will yield the same triple product as eigenvalue decomposition via a slightly more complex algebraic manipulation. 
总之，每个矩阵都可以通过 SVD 分解为一个旋转乘以一个尺度乘以另一个旋转。 只有对称矩阵可以通过特征值对角化分解为旋转乘以尺度乘以逆旋转，并且这样的矩阵是任意方向上的简单尺度。 对称矩阵的 SVD 将通过稍微复杂的代数运算产生与特征值分解相同的三重积。

#### Paeth Decomposition of Rotations Paeth分解旋转

Another decomposition uses shears to represent nonzero rotations (Paeth, 1990). The following identity allows this: 
另一种分解方法采用剪切来表示非零旋转（Paeth，1990）。以下等式支持这一方法：
$$
\begin{bmatrix}
\cos φ & -\sin φ \\
\sin φ & \cos φ
\end{bmatrix}
 = \begin{bmatrix}
 1 & \frac{\cosφ - 1}{\sin φ} \\
 0 & 1
 \end{bmatrix}
 \begin{bmatrix}
 1 & 0 \\
 \sin φ & 1
 \end{bmatrix}
 \begin{bmatrix}
 1 & \frac{\cosφ - 1}{\sin φ} \\
 0 & 1
 \end{bmatrix}
$$
For example, a rotation by $π/4$ (45 degrees) is (see Figure 6.16) 
例如，旋转 $π/4$（45 度）为（见图 6.16）
$$
rotate(\frac{π}{4}) = \begin{bmatrix}
1 & 1 - \sqrt{2} \\
0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0\\
\frac{\sqrt{2}}{2} & 1
\end{bmatrix}
\begin{bmatrix}
1 & 1- \sqrt{2} \\
0 & 1
\end{bmatrix} \ \ \ \ \ (6.2)
$$
<img src=".\Images\Figure 6.16.png" alt="Figure 6.16" style="zoom:50%;" />
Figure 6.16. Any 2D rotation can be accomplished by three shears in sequence. In this case a rotation by 45◦ is decomposed as shown in Equation 6.2. 
图 6.16。 任何二维旋转都可以通过依次进行三个剪切来完成。 在这种情况下，45° 的旋转被分解，如公式 6.2 所示。

This particular transform is useful for raster rotation because shearing is a very efficient raster operation for images; it introduces some jagginess, but will  leave no holes. The key observation is that if we take a raster position $(i, j)$ and apply a horizontal shear to it, we get 
这种特定的变换对于光栅旋转很有用，因为剪切是图像的一种非常高效的光栅操作；它引入了一些锯齿状，但不会留下空洞。关键观察是，如果我们取一个光栅位置$(i, j)$并对其进行水平剪切，我们得到的是
$$
\begin{bmatrix}
1 & s \\
0 & 1 
\end{bmatrix}
\begin{bmatrix}
i \\
j
\end{bmatrix}
= \begin{bmatrix}
i + sj \\
j
\end{bmatrix}
$$
If we round $sj$ to the nearest integer, this amounts to taking each row in the image and moving it sideways by some amount—a different amount for each row. Because it is the same displacement within a row, this allows us to rotate with no gaps in the resulting image. A similar action works for a vertical shear. Thus, we can implement a simple raster rotation easily.
如果我们将 $sj$ 舍入到最接近的整数，这相当于获取图像中的每一行并将其横向移动一定的量（每行移动不同的量）。 因为一行内的位移相同，所以我们可以在生成的图像中无间隙地旋转。 类似的动作也适用于垂直剪切。 这样，我们就可以轻松实现简单的光栅旋转。

## 6.2 3D Linear Transformations  3D 线性变换

The linear 3D transforms are an extension of the 2D transforms. For example, a scale along Cartesian axes is 
线性 3D 变换是 2D 变换的扩展。 例如，沿笛卡尔轴的比例是
$$
scale(s_x, s_y, s_z) = \begin{bmatrix}
s_x & 0 & 0 \\
0 & s_y & 0 \\
0 & 0 & s_z
\end{bmatrix} \ \ \ \ (6.3)
$$
Rotation is considerably more complicated in 3D than in 2D, because there are more possible axes of rotation. However, if we simply want to rotate about the z-axis, which will only change x- and y-coordinates, we can use the 2D rotation matrix with no operation on $z$:
3D 中的旋转比 2D 中的旋转要复杂得多，因为有更多可能的旋转轴。 然而，如果我们只是想绕 z 轴旋转，这只会改变 x 和 y 坐标，我们可以使用 2D 旋转矩阵，而不对 $z$ 进行任何操作：
$$
rotate-z(φ) = \begin{bmatrix}
\cos φ & − \sin φ & 0 \\
\sin φ & \cos φ & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
Similarly we can construct matrices to rotate about the x-axis and the y-axis: 
类似地，我们可以构造绕 x 轴和 y 轴旋转的矩阵：
$$
rotate-x(φ) = \begin{bmatrix}
1 & 0 & 0 \\
0 & \cos φ & − \sin φ \\
0 & \sin φ & \cos φ
\end{bmatrix} \\
rotate-y(φ) =\begin{bmatrix}
\cos φ & 0 & \sin φ \\
0 & 1 & 0 \\
− \sin φ & 0 & \cos φ
\end{bmatrix}
$$

> To understand why the minus sign is in the lower left for the y-axis rotation, think of the three axes in a circular sequence: y after x; z after y; x after z. 
> 为了理解为什么在y轴旋转中减号位于左下方，可以思考一下三个轴在一个循环序列中的位置：y在x之后，z在y之后，x在z之后。

We will discuss rotations about arbitrary axes in the next section.
我们将在下一节中讨论绕任意轴的旋转。

As in two dimensions, we can shear along a particular axis, for example, 
在二维中，我们可以沿着特定的轴剪切，例如，
$$
shear-x(d_y, d_z) = \begin{bmatrix}
1 & d_y & d_z \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix}
$$
As with 2D transforms, any 3D transformation matrix can be decomposed using SVD into a rotation, scale, and another rotation. Any symmetric 3D matrix has an eigenvalue decomposition into rotation, scale, and inverse-rotation. Finally, a 3D rotation can be decomposed into a product of 3D shear matrices. 
与2D变换一样，任何3D变换矩阵均可通过奇异值分解（SVD）拆解为旋转、缩放和另一次旋转。对于任何对称的3D矩阵，都存在特征值分解，包括旋转、缩放和逆旋转。最后，一个3D旋转可以分解为一系列3D剪切矩阵的乘积。

### 6.2.1 Arbitrary 3D Rotations 任意 3D 旋转

As in 2D, 3D rotations are orthogonal matrices. Geometrically, this means that the three rows of the matrix are the Cartesian coordinates of three mutually orthogonal unit vectors as discussed in Section 2.4.5. The columns are three, potentially different, mutually orthogonal unit vectors. There are an infinite number of such rotation matrices. Let’s write down such a matrix: 
与 2D 中一样，3D 旋转也是正交矩阵。 从几何角度来说，这意味着矩阵的三行是三个相互正交的单位向量的笛卡尔坐标，如第 2.4.5 节中所述。 这些列是三个可能不同的、相互正交的单位向量。 这样的旋转矩阵有无数个。 我们写下这样一个矩阵：
$$
\bold{R}_{uvw} = \begin{bmatrix}
x_u & y_u & z_u \\
x_v & y_v & z_v \\
x_w & y_w & z_w \\
\end{bmatrix}
$$
Here, $u = x_u\bold{x} + y_u\bold{y} + z_u\bold{z}$ and so on for $\bold{v}$ and $\bold{w}$. Since the three vectors are orthonormal we know that
这里，$u = x_u\bold{x} + y_u\bold{y} + z_u\bold{z}$ 对于 $\bold{v}$ 和 $\bold{w}$ 依此类推。 由于这三个向量是正交的，我们知道
$$
\bold{u} · \bold{u} = \bold{v} · \bold{v} = \bold{w} · \bold{w} = 1, \\
\bold{u} · \bold{v} = \bold{v} · \bold{w} = \bold{w} · \bold{u} = 0.
$$
We can infer some of the behavior of the rotation matrix by applying it to the vectors $\bold{u}$, $\bold{v}$ and $\bold{w}$. For example, 
我们可以通过将旋转矩阵应用于向量 $\bold{u}$、$\bold{v}$ 和 $\bold{w}$ 来推断旋转矩阵的一些行为。 例如，
$$
\bold{R}_{uvw}\bold{u} = \begin{bmatrix}
x_u & y_u & z_u \\
x_v & y_v & z_v \\
x_w & y_w & z_w \\
\end{bmatrix}
\begin{bmatrix}
x_u \\ 
y_u \\
z_u
\end{bmatrix}
 = \begin{bmatrix}
x_ux_u + y_uy_u + z_uz_u \\ 
x_vx_v + y_vy_v + z_vz_v \\ 
x_wx_w + y_wy_w + z_wz_w
\end{bmatrix}
$$
Note that those three rows of $\bold{R}_{uvw}\bold{u}$ are all dot products: 
请注意，这三行 $\bold{R}_{uvw}\bold{u}$ 都是点积：
$$
\bold{R}_{uvw}\bold{u} = \begin{bmatrix}
\bold{u} \cdot \bold{u} \\
\bold{v} \cdot \bold{u} \\
\bold{w} \cdot \bold{u} \\
\end{bmatrix}
= \begin{bmatrix}
1 \\
0 \\
0
\end{bmatrix}
= \bold{x}
$$
Similarly, $\bold{R}_{uvw}\bold{v} = \bold{y}$, and $\bold{R}_{uvw}\bold{w} = \bold{z}$. So $\bold{R}_{uvw}$ takes the basis $\bold{u}\bold{v}\bold{w}$ to the corresponding Cartesian axes via rotation.
类似地，$\bold{R}_{uvw}\bold{v} = \bold{y}$，$\bold{R}_{uvw}\bold{w} = \bold{z}$。 所以 $\bold{R}_{uvw}$ 通过旋转将基 $\bold{u}\bold{v}\bold{w}$ 带到相应的笛卡尔轴上。

If $\bold{R}_{uvw}$ is a rotation matrix with orthonormal rows, then $R^T_{uvw}$ is also a rotation matrix with orthonormal columns, and in fact is the inverse of $\bold{R}_{uvw}$ (the inverse of an orthogonal matrix is always its transpose). An important point is that for transformation matrices, the algebraic inverse is also the geometric inverse. So if $\bold{R}_{uvw}$ takes $\bold{u}$ to $\bold{x}$, then $\bold{R}^T_{uvw}$ takes $\bold{x}$ to $\bold{u}$. The same should be true of $\bold{v}$ and $\bold{y}$ as we can confirm: 
如果$\bold{R}_{uvw}$是一个具有正交行的旋转矩阵，那么$R^T_{uvw}$也是一个具有正交列的旋转矩阵，实际上是$\bold{R}_{uvw}$的逆矩阵（正交矩阵的逆矩阵总是其转置）。一个重要的观点是对于变换矩阵，代数逆矩阵也是几何逆矩阵。因此，如果$\bold{R}_{uvw}$将$\bold{u}$映射到$\bold{x}$，那么$\bold{R}^T_{uvw}$将$\bold{x}$映射回$\bold{u}$。我们可以验证，对于$\bold{v}$和$\bold{y}$也是如此：
$$
\bold{R}^T_{uvw}\bold{y} = \begin{bmatrix}
x_u & x_v & x_w \\
y_u & y_v & y_w \\
z_u & z_v & z_w
\end{bmatrix}
\begin{bmatrix}
0 \\
1 \\
0
\end{bmatrix}
= \begin{bmatrix}
x_v \\
y_v \\
z_v
\end{bmatrix}
= \bold{v}
$$
So we can always create rotation matrices from orthonormal bases.
所以我们总是可以从正交基创建旋转矩阵。

If we wish to rotate about an arbitrary vector $\bold{a}$, we can form an orthonormal basis with $\bold{w} = \bold{a}$, rotate that basis to the canonical basis $\bold{xyz}$, rotate about the z-axis, and then rotate the canonical basis back to the $\bold{uvw}$ basis. In matrix form, to rotate about the w-axis by an angle $φ$:
如果我们希望围绕任意向量 $\bold{a}$ 旋转，我们可以用 $\bold{w} = \bold{a}$ 形成一个正交基，将该基旋转到规范基 $\bold{xyz }$，绕 z 轴旋转，然后将规范基旋转回 $\bold{uvw}$ 基。 以矩阵形式，绕 w 轴旋转角度 $φ$：
$$
\begin{bmatrix}
x_u & x_v & x_w \\
y_u & y_v & y_w \\
z_u & z_v & z_w
\end{bmatrix}
\begin{bmatrix}
\cos φ & − \sin φ & 0 \\
\sin φ & \cos φ & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_u & x_u & x_u \\
y_v & y_v & y_v \\
z_w & z_w & z_w
\end{bmatrix}
$$
Here we have w a unit vector in the direction of a (i.e., a divided by its own length). But what are $\bold{u}$ and $\bold{v}$? A method to find reasonable $\bold{u}$ and $\bold{v}$ is given in Section 2.4.6. 
这里我们有一个 a 方向的单位向量 w（即 a 除以它自己的长度）。 但是 $\bold{u}$ 和 $\bold{v}$ 是什么？ 第 2.4.6 节给出了找到合理的 $\bold{u}$ 和 $\bold{v}$ 的方法。

If we have a rotation matrix and we wish to have the rotation in axis-angle form, we can compute the one real eigenvalue (which will be $λ = 1$), and the corresponding eigenvector is the axis of rotation. This is the one axis that is not changed by the rotation. 
如果我们有一个旋转矩阵，并且希望以轴角形式进行旋转，我们可以计算一个实数特征值（$λ = 1$），相应的特征向量就是旋转轴。 这是不因旋转而改变的一根轴。

See Chapter 16 for a comparison of the few most-used ways to represent rotations, besides rotation matrices.
请参阅第 16 章，了解除旋转矩阵之外的几种最常用的表示旋转的方法的比较。

### 6.2.2 Transforming Normal Vectors 变换法线向量

While most 3D vectors we use represent positions (offset vectors from the origin) or directions, such as where light comes from, some vectors represent surface normals. Surface normal vectors are perpendicular to the tangent plane of a surface. These normals do not transform the way we would like when the underlying surface is transformed. For example, if the points of a surface are transformed by a matrix $\bold{M}$, a vector $\bold{t}$ that is tangent to the surface and is multiplied by $\bold{M}$ will be tangent to the transformed surface. However, a surface normal vector $\bold{v}$ that is transformed by $\bold{M}$ may not be normal to the transformed surface (Figure 6.17). 
虽然我们使用的大多数3D向量表示位置（相对于原点的偏移向量）或方向，比如光线的来向，但有些向量代表表面法线。表面法线向量垂直于表面的切平面。当底层表面发生变换时，这些法线并不按照我们期望的方式进行变换。例如，如果表面的点通过矩阵$\bold{M}$进行变换，与表面切线相切的向量$\bold{t}$经过$\bold{M}$相乘后仍然与变换后的表面相切。然而，一个表面法线向量$\bold{v}$经过$\bold{M}$变换后可能不再垂直于变换后的表面（见图6.17）。
<img src=".\Images\Figure 6.17.png" alt="Figure 6.17" style="zoom:80%;" />

Figure 6.17. When a normal vector is transformed using the same matrix that transforms the points on an object, the resulting vector may not be perpendicular to the surface as is shown here for the sheared rectangle. The tangent vector, however, does transform to a vector tangent to the transformed surface.  
图 6.17。 当使用与变换对象上的点相同的矩阵来变换法线向量时，所得向量可能不垂直于表面，如此处针对剪切矩形所示。 然而，切向量确实变换为与变换后的表面相切的向量。

We can derive a transform matrix $\bold{N}$ which does take $\bold{n}$ to a vector perpendicular to the transformed surface. One way to attack this issue is to note that a surface normal vector and a tangent vector are perpendicular, so their dot product is zero, which is expressed in matrix form as
我们可以导出一个变换矩阵 $\bold{N}$ ，它将 $\bold{n}$ 转换为垂直于变换表面的向量。 解决这个问题的一种方法是注意表面法向量和切向量是垂直的，因此它们的点积为零，以矩阵形式表示为
$$
\bold{n}^T\bold{t} = \bold{0}. (6.4)
$$
If we denote the desired transformed vectors as $\bold{t}_M = \bold{M}\bold{t}$ and $\bold{n}_N = \bold{N}\bold{n}$, our goal is to find $\bold{N}$ such that $\bold{n}^T_N\bold{t}_M = \bold{0}$. We can find N by some algebraic tricks. First, we can sneak an identity matrix into the dot product, and then take advantage of $\bold{M}^{-1}\bold{M} = \bold{I}$:
如果我们将所需的变换向量表示为 $\bold{t}_M = \bold{M}\bold{t}$ 和 $\bold{n}_N = \bold{N}\bold{n}$，我们的目标 就是找到 $\bold{N}$ 使得 $\bold{n}^T_N\bold{t}_M = \bold{0}$。 我们可以通过一些代数技巧找到 N。 首先，我们可以将单位矩阵潜入点积中，然后利用 $\bold{M}^{-1}\bold{M} = \bold{I}$：
$\bold{n}^T\bold{t} = \bold{n}^T\bold{I}\bold{t} = \bold{n}^T\bold{M}^{-1}\bold{M}\bold{t} = \bold{0}.  $

Although the manipulations above don’t obviously get us anywhere, note that we can add parentheses that make the above expression more obviously a dot product:  
尽管上面的操作显然没有给我们带来任何帮助，但请注意，我们可以添加括号，使上面的表达式更明显地成为一个点积：
$(\bold{n}^T\bold{M}^{-1})(\bold{M}\bold{t}) = (\bold{n}^T\bold{M}^{-1}) \bold{t}_M = 0.  $

This means that the row vector that is perpendicular to $\bold{t}_M$ is the left part of the expression above. This expression holds for any of the tangent vectors in the tangent plane. Since there is only one direction in 3D (and its opposite) that is perpendicular to all such tangent vectors, we know that the left part of the expression above must be the row vector expression for $\bold{n}_N$, i.e., it is $\bold{n}^T_N$, so this allows us to infer $\bold{N}$:
这意味着垂直于 $\bold{t}_M$ 的行向量是上面表达式的左侧部分。 该表达式适用于切平面中的任何切向量。 由于 3D 中只有一个方向（及其相反方向）垂直于所有此类切向量，因此我们知道上面表达式的左侧部分必定是 $\bold{n}_N$ 的行向量表达式，即 它是 $\bold{n}^T_N$，因此我们可以推断 $\bold{N}$：
$\bold{n}^T_N = \bold{n}^T\bold{M}^{-1},  $

so we can take the transpose of that to get
所以我们可以将其转置得到
$$
\bold{n}_N = (\bold{n}^T\bold{M}^{−1})^T = (\bold{M}^{−1})^T\bold{n}. (6.5)
$$
Therefore, we can see that the matrix which correctly transforms normal vectors so they remain normal is $\bold{N} = (\bold{M}^{-1})^T$, i.e., the transpose of the inverse matrix. Since this matrix may change the length of $\bold{n}$, we can multiply it by an arbitrary scalar and it will still produce $\bold{n}_N$ with the right direction. Recall from Section 5.3 that the inverse of a matrix is the transpose of the cofactor matrix divided by the determinant. Because we don’t care about the length of a normal vector, we can skip the division and find that for a 3 × 3 matrix, 
因此，我们可以看到，正确变换法向量使其保持法向量的矩阵是 $\bold{N} = (\bold{M}^{-1})^T$，即逆矩阵的转置。 由于该矩阵可能会改变 $\bold{n}$ 的长度，因此我们可以将其乘以任意标量，它仍然会产生方向正确的 $\bold{n}_N$ 。 回想一下 5.3 节，矩阵的逆矩阵是辅因子矩阵除以行列式的转置。 因为我们不关心法向量的长度，所以我们可以跳过除法并发现对于 3 × 3 矩阵，
$$
\bold{N} = \begin{bmatrix}
m^c_{11} & m^c_{12} & m^c_{13} \\ 
m^c_{21} & m^c_{22} & m^c_{23} \\ 
m^c_{31} & m^c_{32} & m^c_{33} \\ 
\end{bmatrix}
$$
This assumes the element of $\bold{M}$ in row $i$ and column $j$ is $m_{ij}$. So the full expression for $\bold{N}$ is
假设行$i$和列$j$中$\bold{M}$的元素是$m_{ij}$。 所以 $\bold{N}$ 的完整表达式是
$$
\bold{N} = \begin{bmatrix}
m_{22}m_{33} - m_{23}m_{32} & m_{23}m_{31} - m_{21}m_{33} & m_{21}m_{32} - m_{22}m_{31} \\
m_{13}m_{32} - m_{12}m_{33} & m_{11}m_{33} - m_{13}m_{31} & m_{12}m_{31} - m_{11}m_{32} \\
m_{12}m_{23} - m_{13}m_{22} & m_{13}m_{21} - m_{11}m_{23} & m_{11}m_{22} - m_{12}m_{21} \\
\end{bmatrix}
$$

## 6.3 Translation and Affine Transformations 平移和仿射变换

We have been looking at methods to change vectors using a matrix $\bold{M}$. In two dimensions, these transforms have the form,
我们一直在研究使用矩阵 $\bold{M}$ 改变向量的方法。 在二维中，这些变换具有以下形式：
$x' = m_{11}x + m_{12}y, \\
y' = m_{21}x + m_{22}y.  $

We cannot use such transforms to move objects, only to scale and rotate them. In particular, the origin $(0, 0)$ always remains fixed under a linear transformation. To move, or translate, an object by shifting all its points the same amount, we need a transform of the form, 
我们不能使用此类变换来移动对象，只能缩放和旋转它们。 特别是，原点 $(0, 0)$ 在线性变换下始终保持固定。 要通过将所有点移动相同的量来移动或平移对象，我们需要形式的变换，
$x' = x + x_t, \\
y' = y + y_t.  $

There is just no way to do that by multiplying $(x, y)$ by a 2 × 2 matrix. One possibility for adding translation to our system of linear transformations is to simply associate a separate translation vector with each transformation matrix, letting the matrix take care of scaling and rotation and the vector take care of translation. This is perfectly feasible, but the bookkeeping is awkward and the rule for composing two transformations is not as simple and clean as with linear transformations.
没有办法通过将 $(x, y)$ 乘以 2 × 2 矩阵来做到这一点。 将平移添加到线性变换系统的一种可能性是简单地将单独的平移向量与每个变换矩阵相关联，让矩阵负责缩放和旋转，而向量负责平移。 这是完全可行的，但是簿记很尴尬，并且组合两个变换的规则不像线性变换那么简单和干净。

Instead, we can use a clever trick to get a single matrix multiplication to do both operations together. The idea is simple: represent the point $(x, y)$ by a 3D vector $\begin{bmatrix}x & y & 1\end{bmatrix}^T$, and use 3 × 3 matrices of the form
相反，我们可以使用一个巧妙的技巧来获得单个矩阵乘法来同时执行这两个操作。 想法很简单：用 3D 向量 $\begin{bmatrix}x & y & 1\end{bmatrix}^T$ 表示点 $(x, y)$，并使用以下形式的 3 × 3 矩阵
$$
\begin{bmatrix}
m_{11} & m_{12} & x_t \\
m_{21} & m_{22} & y_t \\
0 & 0 & 1
\end{bmatrix}
$$
The fixed third row serves to copy the 1 into the transformed vector, so that all vectors have a 1 in the last place, and the first two rows compute $x'$ and $y'$ as linear combinations of $x$, $y$, and $1$: 
固定的第三行用于将1复制到转换后的向量中，这样所有向量的最后一个位置都有一个1，前两行计算$x'$和$y'$作为$x$， $y$和$1$的线性组合:
$$
\begin{bmatrix}
x' \\
y' \\
1
\end{bmatrix}
= \begin{bmatrix}
m_{11} & m_{12} & x_t \\
m_{21} & m_{22} & y_t \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\ 
y \\
1
\end{bmatrix}
= \begin{bmatrix}
m_{11}x + m_{12}y + x_t \\
m_{21}x + m_{22}y + y_t \\
1
\end{bmatrix}
$$
The single matrix implements a linear transformation followed by a translation! This kind of transformation is called an affine transformation, and this way of implementing affine transformations by adding an extra dimension is called homogeneous coordinates (Roberts, 1965; Riesenfeld, 1981; Penna & Patterson, 1986). Homogeneous coordinates not only clean up the code for transformations,  but this scheme also makes it obvious how to compose two affine transformations: simply multiply the matrices.
这个单矩阵实现了线性变换后跟随着一次平移！这种类型的变换被称为仿射变换，而通过增加额外维度实现仿射变换的方式被称为齐次坐标（Roberts, 1965; Riesenfeld, 1981; Penna & Patterson, 1986）。齐次坐标不仅使得变换的代码更为清晰，而且这种方案还清晰地展示了如何组合两个仿射变换：简单地将两个矩阵相乘即可。

A problem with this new formalism arises when we need to transform vectors that are not supposed to be positions—they represent directions, or offsets between positions. Vectors that represent directions or offsets should not change when we translate an object. Fortunately, we can arrange for this by setting the third coordinate to zero:
这一新的形式主义面临的问题在于，当我们需要转换那些并非位置而是代表方向或位置之间偏移的向量时。那些代表方向或偏移的向量在我们对物体进行平移时不应发生改变。幸运的是，我们可以通过将第三坐标设定为零来实现这一点：
$$
\begin{bmatrix}
1 & 0 & x_t \\
0 & 1 & y_t \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
0
\end{bmatrix}
= \begin{bmatrix}
x \\
y \\
0
\end{bmatrix}
$$
If there is a scaling/rotation transformation in the upper-left 2 × 2 entries of the matrix, it will apply to the vector, but the translation still multiplies with the zero and is ignored. Furthermore, the zero is copied into the transformed vector, so direction vectors remain direction vectors after they are transformed. 
如果矩阵左上角的 2 × 2 条目中有缩放/旋转变换，它将应用于向量，但平移仍然与零相乘并被忽略。 此外，零被复制到变换后的向量中，因此方向向量在变换后仍然是方向向量。

This is exactly the behavior we want for vectors, so they fit smoothly into the system: the extra (third) coordinate will be either 1 or 0 depending on whether we are encoding a position or a direction. We actually do need to store the homogeneous coordinate so we can distinguish between locations and other vectors. For example, 
这正是我们想要的向量行为，因此它们可以顺利地融入系统：额外的（第三个）坐标将为 1 或 0，具体取决于我们编码的是位置还是方向。 实际上，我们确实需要存储齐次坐标，以便我们可以区分位置和其他向量。 例如，
$$
\begin{bmatrix}
3 \\
2 \\
1
\end{bmatrix}\ is\ a\ location\ and\ 
\begin{bmatrix}
3 \\
2 \\
0
\end{bmatrix}\ is\ a\ displacement\ or\ direction.
$$

> This gives an explanation for the name “homogeneous:” translation, rotation, and scaling of positions and directions all fit into a single system. 
> 这给出了“同质”名称的解释：位置和方向的平移、旋转和缩放都适合单个系统。

Later, when we do perspective viewing, we will see that it is useful to allow the homogeneous coordinate to take on values other than one or zero. 
稍后，当我们进行透视观察时，我们会发现允许齐次坐标取除 1 或 0 以外的值是很有用的。

Homogeneous coordinates are used nearly universally to represent transformations in graphics systems. In particular, homogeneous coordinates underlie the  design and operation of renderers implemented in graphics hardware. We will see in Chapter 7 that homogeneous coordinates also make it easy to draw scenes in perspective, another reason for their popularity. 
齐次坐标几乎普遍用于表示图形系统中的变换。 特别是，齐次坐标是图形硬件中实现的渲染器的设计和操作的基础。 我们将在第 7 章中看到，齐次坐标还使以透视方式绘制场景变得容易，这是它们受欢迎的另一个原因。

> Homogeneous coordinates are also ubiquitous in computer vision. 
> 齐次坐标在计算机视觉中也很普遍。

Homogeneous coordinates can be considered just a clever way to handle the bookkeeping for translation, but there is also a different, geometric interpretation. The key observation is that when we do a 3D shear based on the z-coordinate we get this transform:
齐次坐标可以被认为是处理平移簿记的一种巧妙方法，但也有一种不同的几何解释。 关键的观察结果是，当我们基于 z 坐标进行 3D 剪切时，我们得到以下变换：
$$
\begin{bmatrix}
1 & 0 & x_t \\
0 & 1 & y_t \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
= \begin{bmatrix}
x + x_tz \\
y + y_tz \\
z
\end{bmatrix}
$$
Note that this almost has the form we want in $x$ and $y$ for a 2D translation, but has a $z$ hanging around that doesn’t have a meaning in 2D. Now comes the key  decision: we will add a coordinate $z = 1$ to all 2D locations. This gives us
请注意，这几乎具有我们想要的 2D 转换的 $x$ 和 $y$ 形式，但有一个 $z$ 悬挂在 2D 中没有意义。 现在是关键决定：我们将向所有 2D 位置添加坐标 $z = 1$。 这给了我们
$$
\begin{bmatrix}
1 & 0 & x_t \\
0 & 1 & y_t \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
1
\end{bmatrix}
= \begin{bmatrix}
x + x_tz \\
y + y_tz \\
1
\end{bmatrix}
$$
By associating a ($z = 1$)-coordinate with all 2D points, we now can encode translations into matrix form. For example, to first translate in 2D by $(x_t, y_t)$ and then rotate by angle $φ$ we would use the matrix
通过将 ($z = 1$) 坐标与所有 2D 点相关联，我们现在可以将翻译编码为矩阵形式。 例如，要首先在 2D 中平移 $(x_t, y_t)$，然后旋转角度 $φ$，我们将使用矩阵
$$
\bold{M} = \begin{bmatrix}
\cosφ & -\sinφ & 0 \\
\sinφ & \cosφ & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & x_t \\
0 & 1 & y_t \\
0 & 0 & 1
\end{bmatrix}
$$
Note that the 2D rotation matrix is now 3 × 3 with zeros in the “translation slots.” With this type of formalism, which uses shears along $z = 1$ to encode translations, we can represent any number of 2D shears, 2D rotations, and 2D translations as one composite 3D matrix. The bottom row of that matrix will always be $(0, 0, 1)$, so we don’t really have to store it. We just need to remember it is there when we multiply two matrices together. 
请注意，2D 旋转矩阵现在为 3 × 3，“平移槽”中为零。 通过这种形式，使用沿 $z = 1$ 的剪切来编码平移，我们可以将任意数量的 2D 剪切、2D 旋转和 2D 平移表示为一个复合 3D 矩阵。 该矩阵的底行始终是 $(0, 0, 1)$，因此我们实际上不必存储它。 我们只需要记住当我们将两个矩阵相乘时它就在那里。

In 3D, the same technique works: we can add a fourth coordinate, a homogeneous coordinate, and then we have translations:
在 3D 中，同样的技术也有效：我们可以添加第四个坐标，即齐次坐标，然后我们就可以进行平移：
$$
\begin{bmatrix}
1 & 0 & 0 & x_t \\
0 & 1 & 0 & y_t \\
0 & 0 & 1 & z_t \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}
= \begin{bmatrix}
x + x_t \\
y + y_t \\
z + z_t \\
1
\end{bmatrix}
$$
Again, for a direction vector, the fourth coordinate is zero and the vector is thus unaffected by translations. 
同样，对于方向矢量，第四个坐标为零，因此矢量不受平移的影响。

**Example (Windowing transformations)**. Often in graphics we need to create a transform matrix that takes points in the rectangle $[x_l, x_h] × [y_l, y_h]$ to the rectangle $[x'_l, x'_h] × [y'_l, y'_h ]$. This can be accomplished with a single scale and translate in sequence. However, it is more intuitive to create the transform from a sequence of three operations (Figure 6.18): 
**示例（窗口转换）**。 通常在图形中我们需要创建一个变换矩阵，将矩形 $[x_l, x_h] × [y_l, y_h]$ 中的点转换为矩形 $[x'_l, x'_h] × [y'_l, y' _h]$。 这可以通过单个比例并按顺序翻译来完成。 然而，通过三个操作序列创建变换更为直观（图 6.18）：

1. Move the point $(x_l, y_l)$ to the origin.
   将点$(x_l, y_l)$移动到原点。
2. Scale the rectangle to be the same size as the target rectangle.
   将矩形缩放至与目标矩形相同的大小。
3. Move the origin to point $(x'_l, y'_l)$. 
   将原点移动到点$(x'_l, y'_l)$。

<img src=".\Images\Figure 6.18.png" alt="Figure 6.18" style="zoom:67%;" />
Figure 6.18. To take one rectangle (window) to the other, we first shift the lower-left corner to the origin, then scale it to the new size, and then move the origin to the lower-left corner of the target rectangle.  
图 6.18. 要将一个矩形（窗口）转移到另一个矩形（窗口），我们首先将左下角移动到原点，然后将其缩放到新大小，然后将原点移动到目标矩形的左下角。

Remembering that the right-hand matrix is applied first, we can write
请记住首先应用右侧矩阵，我们可以写
$$
window = translate (x'_l, y'_l)\ scale(\frac{x'_h -x'_l}{x_h-x_l}, \frac{y'_h - y'_l}{y_h - y_l}) \ translate (−x_l, −y_l) \\
= \begin{bmatrix}
1 & 0 & x'_l \\
0 & 1 & y'_l \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
\frac{x'_h - x'_l}{x_h - x_l} & 0 & 0 \\
0 & \frac{y'_h - y'_l}{y_h - y_l} & 0 \\
0 & 0 & 1 \\
\end{bmatrix}
\begin{bmatrix}
1 & 0 & -x_l \\
0 & 1 & -y_l \\
0 & 0 & 1
\end{bmatrix} \\
=\begin{bmatrix}
\frac{x'_h - x'_l}{x_h - x_l} & 0 & \frac{x'_lx_h - x'_hx_l}{x_h-x_l} \\
0 & \frac{y'_h - y'_l}{y_h - y_l} & \frac{y'_ly_h - y'_hy_l}{y_h-y_l} \\
0 & 0 & 1 \\
\end{bmatrix} \ \ \ \ \  \ (6.6)
$$
It is perhaps not surprising to some readers that the resulting matrix has the form it does, but the constructive process with the three matrices leaves no doubt as to the correctness of the result.
对于某些读者来说，得到的矩阵具有它所具有的形式也许并不奇怪，但是三个矩阵的构造过程使结果的正确性毫无疑问。

An exactly analogous construction can be used to define a 3D windowing transformation, which maps the box $[x_l, x_h] × [y_l, y_h] × [z_l, z_h]$ to the box
完全类似的构造可用于定义 3D 窗口变换，它将框 $[x_l, x_h] × [y_l, y_h] × [z_l, z_h]$ 映射到框
$$
[x'_l, x'_h] × [y'_l, y'_h] × [z'_l, z'_h]:\\
\begin{bmatrix}
\frac{x'_h - x'_l}{x_h - x_l} & 0 & 0 & \frac{x'_lx_h - x'_hx_l}{x_h - x_l} \\
0 & \frac{y'_h - y'_l}{y_h - y_l} & 0 & \frac{y'_ly_h - y'_hy_l}{y_h - y_l} \\
0 & 0 & \frac{z'_h - z'_l}{z_h - z_l} & \frac{z'_lz_h - z'_hz_l}{z_h - z_l} \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ (6.7)
$$
It is interesting to note that if we multiply an arbitrary matrix composed of scales, shears, and rotations with a simple translation (translation comes second), we get
有趣的是，如果我们将由尺度、剪切和旋转组成的任意矩阵与简单的平移（平移排在第二位）相乘，我们得到
$$
\begin{bmatrix}
1 & 0 & 0 & x_t \\
0 & 1 & 0 & y_t \\
0 & 0 & 1 & z_t \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & 0 \\
a_{21} & a_{22} & a_{23} & 0 \\
a_{31} & a_{32} & a_{33} & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
= \begin{bmatrix}
a_{11} & a_{12} & a_{13} & x_t \\
a_{21} & a_{22} & a_{23} & y_t \\
a_{31} & a_{32} & a_{33} & z_t \\
0 & 0 & 0 & 1
\end{bmatrix}
$$
Thus, we can look at any matrix and think of it as a scaling/rotation part and a translation part because the components are nicely separated from each other. 
因此，我们可以查看任何矩阵并将其视为缩放/旋转部分和平移部分，因为这些组件彼此很好地分离。

An important class of transforms are rigid-body transforms. These are composed only of translations and rotations, so they have no stretching or shrinking of the objects. Such transforms will have a pure rotation for the $a_{ij}$ above. 
一类重要的变换是刚体变换。 这些仅由平移和旋转组成，因此它们没有对象的拉伸或收缩。 这样的变换将对上面的 $a_{ij}$ 进行纯旋转。

## 6.4 Inverses of Transformation Matrices 变换矩阵的逆

While we can always invert a matrix algebraically, we can use geometry if we know what the transform does. For example, the inverse of scale$(s_x, s_y, s_z)$ is scale $(1/s_x, 1/s_y, 1/s_z)$. The inverse of a rotation is the same rotation with the opposite sign on the angle. The inverse of a translation is a translation in the opposite direction. If we have a series of matrices $\bold{M} = \bold{M}_1\bold{M}_2 · · · \bold{M}_n$ then $\bold{M}^{-1} = \bold{M}^{-1}_n ··· \bold{M}^{-1}_2\bold{M}_1^{-1}$. 
虽然我们总是可以代数地求矩阵的逆，但是如果我们知道变换的作用，我们也可以使用几何方法。例如，缩放$(s_x, s_y, s_z)$的逆是缩放$(1/s_x, 1/s_y, 1/s_z)$。旋转的逆是角度相反的相同旋转。平移的逆是相反方向的平移。如果我们有一系列矩阵$\bold{M} = \bold{M}_1\bold{M}_2 · · · \bold{M}_n$，那么$\bold{M}^{-1} = \bold{M}^{-1}_n ··· \bold{M}^{-1}_2\bold{M}_1^{-1}$。

Also, certain types of transformation matrices are easy to invert. We’ve already mentioned scales, which are diagonal matrices; the second important example is rotations, which are orthogonal matrices. Recall (Section 5.2.4) that the inverse of an orthogonal matrix is its transpose. This makes it easy to invert rotations and rigid body transformations (see Exercise 6). Also, it’s useful to know that a matrix with [0 0 0 1] in the bottom row has an inverse that also has [0 0 0 1] in the bottom row (see Exercise 7).
而且，某些类型的变换矩阵很容易求逆。我们已经提到过尺度，它是对角矩阵;第二个重要的例子是旋转，它是正交矩阵。回想一下(第5.2.4节)，正交矩阵的逆是它的转置。这使得旋转反转和刚体转换变得很容易(参见练习6)。此外，知道底部一行有[0 0 0 1]的矩阵的逆矩阵在底部一行也有[0 0 0 1]是有用的(参见练习7)。

Interestingly, we can use SVD to invert a matrix as well. Since we know that any matrix can be decomposed into a rotation times a scale times a rotation,  inversion is straightforward. For example, in 3D we have
有趣的是，我们也可以使用 SVD 来反转矩阵。 由于我们知道任何矩阵都可以分解为旋转乘以尺度乘以旋转，因此求逆很简单。 例如，在 3D 中我们有
$\bold{M} = \bold{R}_1scale(σ1, σ2, σ3)\bold{R}_2, $

and from the rules above it follows easily that
从上面的规则很容易得出
$\bold{M}^{-1} = \bold{R}^T_2\ scale(1/σ_1, 1/σ_2, 1/σ_3)\bold{R}^T_1 .  $

## 6.5 Coordinate Transformations  坐标变换

All of the previous discussion has been in terms of using transformation matrices to move points around. We can also think of them as simply changing the coordinate system in which the point is represented. For example, in Figure 6.19, we see two ways to visualize a movement. In different contexts, either interpretation may be more suitable. 
前面的所有讨论都是关于使用变换矩阵来移动点。 我们也可以将它们视为简单地更改表示点的坐标系。 例如，在图 6.19 中，我们看到两种可视化运动的方法。 在不同的背景下，任何一种解释都可能更合适。
![Figure 6.19](.\Images\Figure 6.19.png)
Figure 6.19. The point (2,1) has a transform “translate by (-1,0)” applied to it. On the top right is our mental image if we view this transformation as a physical movement, and on the bottom right is our mental image if we view it as a change of coordinates (a movement of the origin in this case). The artificial boundary is just an artifice, and the relative position of the axes and the point are the same in either case. 
图6.19。点(2,1)经历了一次“平移(-1,0)”的变换。右上方是我们将这个变换视为实际移动时的心理想象，而右下方则是我们将其视为坐标变换时的心理想象（在这种情况下是原点的移动)。人为设定的边界仅仅是一种技巧，不论哪种情况，坐标轴和点的相对位置都是一样的。

For example, a driving game may have a model of a city and a model of a car. If the player is presented with a view out the windshield, objects inside the car are always drawn in the same place on the screen, while the streets and buildings appear to move backward as the player drives. On each frame, we apply a transformation to these objects that moves them farther back than on the previous frame. One way to think of this operation is simply that it moves the buildings backward; another way to think of it is that the buildings are staying put but the coordinate system in which we want to draw them—which is attached to the car—is moving. In the second interpretation, the transformation is changing the coordinates of the city geometry, expressing them as coordinates in the car’s coordinate system. Both ways will lead to exactly the same matrix that is applied to the geometry outside the car.
例如，驾驶游戏可能有城市模型和汽车模型。 如果玩家看到挡风玻璃外的景色，车内的物体总是被绘制在屏幕上的同一位置，而街道和建筑物似乎随着玩家驾驶而向后移动。 在每一帧上，我们对这些对象应用变换，使它们比前一帧向后移动得更远。 思考这一操作的一种方式是简单地将建筑物向后移动。 另一种思考方式是，建筑物保持不动，但我们想要绘制它们的坐标系（连接到汽车上）正在移动。 在第二种解释中，变换是改变城市几何的坐标，将它们表示为汽车坐标系中的坐标。 两种方法都会产生应用于汽车外部几何形状的完全相同的矩阵。

If the game also supports an overhead view to show where the car is in the city, the buildings and streets need to be drawn in fixed positions while the car needs to move from frame to frame. The same two interpretations apply: we can think of the changing transformation as moving the car from its canonical position to its current location in the world; or we can think of the transformation as simply changing the coordinates of the car’s geometry, which is originally expressed in terms of a coordinate system attached to the car, to express them instead in a coordinate system fixed relative to the city. The change-of-coordinates interpretation makes it clear that the matrices used in these two modes (city-to-car coordinate change vs. car-to-city coordinate change) are inverses of one another. 
如果游戏还支持俯视图来显示汽车在城市中的位置，则需要将建筑物和街道绘制在固定位置，而汽车需要在帧之间移动。 同样的两种解释也适用：我们可以将变化的转变视为将汽车从其规范位置移动到其在世界中的当前位置； 或者我们可以将转换视为简单地更改汽车几何形状的坐标，该坐标最初是用附加在汽车上的坐标系来表示的，以相对于城市固定的坐标系来表示它们。 坐标变化的解释清楚地表明，这两种模式（城市到汽车坐标变化与汽车到城市坐标变化）中使用的矩阵是彼此相反的。

The idea of changing coordinate systems is much like the idea of type conversions in programming. Before we can add a floating-point number to an integer, we need to convert the integer to floating point or the floating-point number to an integer, depending on our needs, so that the types match. And before we can draw the city and the car together, we need to convert the city to car coordinates or the car to city coordinates, depending on our needs, so that the coordinates match. 
改变坐标系的想法很像编程中类型转换的想法。 在将浮点数与整数相加之前，我们需要根据需要将整数转换为浮点数或将浮点数转换为整数，以便类型匹配。 在我们将城市和汽车绘制在一起之前，我们需要根据我们的需要将城市转换为汽车坐标或将汽车转换为城市坐标，以便坐标匹配。

When managing multiple coordinate systems, it’s easy to get confused and wind up with objects in the wrong coordinates, causing them to show up in unexpected places. But with systematic thinking about transformations between coordinate systems, you can reliably get the transformations right.
管理多个坐标系时，很容易感到困惑并最终导致对象出现在错误的坐标中，导致它们出现在意想不到的位置。 但是，通过系统地思考坐标系之间的转换，您可以可靠地获得正确的转换。

Geometrically, a coordinate system, or coordinate frame, consists of an origin and a basis—a set of three vectors. Orthonormal bases are so convenient that we’ll normally assume frames are orthonormal unless otherwise specified. In a frame with origin p and basis ${\bold{u}, \bold{v}, \bold{w}}$, the coordinates $(u, v, w)$ describe the point
从几何角度来看，坐标系或坐标系由原点和基（一组三个向量）组成。 正交基非常方便，除非另有说明，否则我们通常会假设框架是正交的。 在原点为 p 且基础为 ${\bold{u}, \bold{v}, \bold{w}}$ 的框架中，坐标 $(u, v, w)$ 描述该点
$\bold{p} + u\bold{u} + v\bold{v} + w\bold{w}.  $

> In 2D, of course, there are two basis vectors. 
> 当然，在二维中，有两个基向量。

When we store these vectors in the computer, they need to be represented in terms of some coordinate system. To get things started, we have to designate some canonical coordinate system, often called “global” or “world” coordinates, which is used to describe all other systems. In the city example, we might adopt the street grid and use the convention that the x-axis points along Main Street, the y-axis points up, and the z-axis points along Central Avenue. Then when we write the origin and basis of the car frame in terms of these coordinates it is clear what we mean. 
当我们将这些向量存储在计算机中时，它们需要用某种坐标系来表示。 首先，我们必须指定一些规范坐标系，通常称为“全局”或“世界”坐标，用于描述所有其他系统。 在城市示例中，我们可能采用街道网格并使用 x 轴指向主街、y 轴指向上方、z 轴指向中央大道的约定。 然后，当我们用这些坐标写出车架的原点和基础时，我们的意思就很清楚了。

> In 2D, right-handed means $y$ is counterclockwise from $x$. 
> 在 2D 中，右手意味着 $y$ 从 $x$ 逆时针旋转。

In 2D our convention is is to use the point $\bold{o}$ for the origin, and $\bold{x}$ and $\bold{y}$ for the right-handed orthonormal basis vectors $\bold{x}$ and $\bold{y}$ (Figure 6.20). 
在二维中，我们的约定是使用点 $\bold{o}$ 作为原点，使用 $\bold{x}$ 和 $\bold{y}$ 作为右手正交基向量 $\bold{x }$ 和 $\bold{y}$（图 6.20）。
![Figure 6.20](.\Images\Figure 6.20.png)
Figure 6.20. The point $\bold{p}$ can be represented in terms of either coordinate system.
图 6.20. 点 $\bold{p}$ 可以用任一坐标系表示。

Another coordinate system might have an origin $\bold{e}$ and right-handed orthonormal basis vectors $\bold{u}$ and $\bold{v}$. Note that typically the canonical data $\bold{o}$, $\bold{x}$, and $\bold{y}$ are never stored explicitly. They are the frame-of-reference for all other coordinate systems. In that coordinate system, we often write down the location of $\bold{p}$ as an ordered pair, which is shorthand for a full vector expression: 
另一个坐标系可能有一个原点$\bold{e}$和右手正交基向量$\bold{u}$和$\bold{v}$。请注意，通常规范化数据$\bold{o}$、$\bold{x}$和$\bold{y}$不会被显式存储。它们是所有其他坐标系的参照系。在这个坐标系中，我们通常把$\bold{p}$的位置写成一个有序对，这是一个完整向量表达式的简写:
$\bold{p} = (x_p, y_p) ≡ \bold{o} + x_p\bold{x} + y_p\bold{y}.  $

For example, in Figure 6.20, $(x_p, y_p) = (2.5, 0.9)$. Note that the pair $(x_p, y_p)$ implicitly assumes the origin $\bold{o}$. Similarly, we can express $\bold{p}$ in terms of another equation:
例如，在图 6.20 中，$(x_p, y_p) = (2.5, 0.9)$。 请注意，$(x_p, y_p)$ 对隐式假定原点 $\bold{o}$。 类似地，我们可以用另一个方程来表达$\bold{p}$：
$\bold{p} = (u_p, v_p) ≡ \bold{e} + u_p\bold{u} + v_p\bold{v}.  $

In Figure 6.20, this has $(u_p, v_p) = (0.5, -0.7)$. Again, the origin $\bold{e}$ is left as an implicit part of the coordinate system associated with $\bold{u}$ and $\bold{v}$.
在图 6.20 中，$(u_p, v_p) = (0.5, -0.7)$。 同样，原点 $\bold{e}$ 被保留为与 $\bold{u}$ 和 $\bold{v}$ 关联的坐标系的隐式部分。

We can express this same relationship using matrix machinery, like this: 
我们可以使用矩阵机制来表达相同的关系，如下所示：
$$
\begin{bmatrix}
x_p \\
y_p \\
1
\end{bmatrix}
= \begin{bmatrix}
1 & 0 & x_e \\
0 & 1 & y_e \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_u & x_v & 0 \\
y_u & y_v & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u_p \\
v_p \\
1
\end{bmatrix}
= \begin{bmatrix}
x_u & x_v & x_e \\
y_u & y_v & y_e \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u_p \\
v_p \\
1
\end{bmatrix}
$$
Note that this assumes we have the point $\bold{e}$ and vectors $\bold{u}$ and $\bold{v}$ stored in canonical coordinates; the (x, y)-coordinate system is the first among equals. In terms of the basic types of transformations we’ve discussed in this chapter, this is a rotation (involving $\bold{u}$ and $\bold{v}$) followed by a translation (involving $\bold{e}$). Looking at the matrix for the rotation and translation together, you can see it’s very easy to write down: we just put $\bold{u}$, $\bold{v}$, and $\bold{e}$ into the columns of a matrix, with the usual [0 0 1] in the third row. To make this even clearer we can write the matrix like this:
请注意，这假设我们有点 $\bold{e}$ 和向量 $\bold{u}$ 和 $\bold{v}$ 存储在规范坐标中； (x, y) 坐标系是第一个相等的坐标系。 就我们在本章中讨论的基本变换类型而言，这是一个旋转（涉及 $\bold{u}$ 和 $\bold{v}$），然后是平移（涉及 $\bold{e} $）。 把旋转和平移矩阵放在一起看，你会发现它很容易写下来：我们只需将 $\bold{u}$、$\bold{v}$ 和 $\bold{e}$ 放入 矩阵的列，通常的 [0 0 1] 位于第三行。 为了让这一点更清楚，我们可以这样写矩阵：

> The name “frame-to-canonical” is based on thinking about changing the coordinates of a vector from one system to another. Thinking in terms of moving vectors around, the frame-to-canonical matrix maps the canonical frame to the $(u,v)$ frame. 
> “框架到规范”这个名称是基于将向量的坐标从一个系统更改为另一个系统的想法。 从移动向量的角度考虑，帧到规范矩阵将规范框架映射到 $(u,v)$ 框架。

$$
\bold{p}_{xy} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{e} \\
0 & 0 & 1
\end{bmatrix}\bold{p}_{uv}
$$

We call this matrix the frame-to-canonical matrix for the $(u, v)$ frame. It takes points expressed in the $(u, v)$ frame and converts them to the same points expressed in the canonical frame. 
我们将此矩阵称为 $(u, v)$ 帧的帧到规范矩阵。 它采用 $(u, v)$ 框架中表示的点，并将它们转换为规范框架中表示的相同点。

To go in the other direction we have
朝另一个方向走，我们有
$$
\begin{bmatrix}
u_p \\
v_p \\
1
\end{bmatrix}
= \begin{bmatrix}
x_u & y_u & 0 \\
x_v & y_v & 0 \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & -x_e \\
0 & 1 & -y_e \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_p \\
y_p \\
1
\end{bmatrix}
$$
This is a translation followed by a rotation; they are the inverses of the rotation and translation we used to build the frame-to-canonical matrix, and when multiplied together they produce the inverse of the frame-to-canonical matrix, which is (not surprisingly) called the canonical-to-frame matrix:
这是先平移后旋转； 它们是我们用来构建框架到规范矩阵的旋转和平移的逆矩阵，当它们相乘时，它们会产生框架到规范矩阵的逆矩阵，这（毫不奇怪）被称为规范到 - 帧矩阵：
$$
\bold{p}_{uv} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{e} \\
0 & 0 & 1
\end{bmatrix}^{-1}
\bold{p}_{xy}
$$
The canonical-to-frame matrix takes points expressed in the canonical frame and converts them to the same points expressed in the $(u,v)$ frame. We have written this matrix as the inverse of the frame-to-canonical matrix because it can’t immediately be written down using the canonical coordinates of $\bold{e}$, $\bold{u}$, and $\bold{v}$. But remember that all coordinate systems are equivalent; it’s only our convention of storing vectors in terms of x- and y-coordinates that creates this seeming asymmetry. The canonical-to-frame matrix can be expressed simply in terms of the $(u, v)$ coordinates of $\bold{o}$, $\bold{x}$, and $\bold{y}$:
规范到坐标系矩阵取在规范坐标系中表示的点，并将它们转换为在$(u,v)$坐标系中表示的相同点。我们把这个矩阵写成坐标系到正则矩阵的逆矩阵因为它不能马上用正则坐标$\bold{e}$， $\bold{u}$和$\bold{v}$来表示。但是记住所有的坐标系都是等价的;只是我们用x坐标和y坐标来存储向量的习惯造成了这种不对称。正则到坐标系矩阵可以简单地表示为$\bold{o}$、$\bold{x}$和$\bold{y}$的$(u, v)$坐标:
$$
\bold{p}_{uv} = \begin{bmatrix}
\bold{x}_{uv} & \bold{y}_{uv} & \bold{o}_{uv} \\
0 & 0 & 1
\end{bmatrix}^{-1}
\bold{p}_{xy}
$$
All these ideas work strictly analogously in 3D, where we have
所有这些想法在3D中都是类似的
$$
\ \begin{bmatrix}
x_p \\
y_p \\
z_p \\
1
\end{bmatrix}
= \begin{bmatrix}
1 & 0 & 0 & x_e \\
0 & 1 & 0 & y_e \\
0 & 0 & 1 & z_e \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_u & x_v & x_w & 0 \\
y_u & y_v & y_w & 0 \\ 
z_u & z_v & z_w & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
u_p \\
v_p \\
w_p \\
1
\end{bmatrix} \\

\bold{p}_{xyz} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{w} & \bold{e}\\
0 & 0 & 0 & 1
\end{bmatrix}\bold{p}_{uvw} \ \ \ \ \ (6.8)\\\\

\begin{bmatrix}
u_p \\
v_p \\
w_p \\
1
\end{bmatrix}
= \begin{bmatrix}
x_u & x_v & x_w & 0 \\
y_u & y_v & y_w & 0 \\ 
z_u & z_v & z_w & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & -x_e \\
0 & 1 & 0 & -y_e \\
0 & 0 & 1 & -z_e \\
0 & 0 & 0 & 1
\end{bmatrix}\begin{bmatrix}
x_p \\
y_p \\
z_p \\
1
\end{bmatrix} \\
\bold{p}_{uvw} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{w} & \bold{e}\\
0 & 0 & 0 & 1
\end{bmatrix}^{-1}\bold{p}_{xyz} \ \ \ \ \ (6.9)\\
$$

## Frequently Asked Questions 经常问的问题

### Can’t I just hardcode transforms rather than use the matrix formalisms? 我不能只硬编码变换而不使用矩阵形式吗？

Yes, but in practice it is harder to derive, harder to debug, and not any more efficient. Also, all current graphics APIs use this matrix formalism so it must be understood even to use graphics libraries.
是的，但在实践中，它更难推导，更难调试，而且效率也没有提高。 此外，当前所有图形 API 都使用这种矩阵形式，因此即使要使用图形库也必须理解它。

### The bottom row of the matrix is always (0,0,0,1). Do I have to store it?矩阵的底行始终为 (0,0,0,1)。 我必须储存它吗？

You do not have to store it unless you include perspective transforms (Chapter 7). 
除非包含透视变换（第 7 章），否则不必存储它。

## Notes

The derivation of the transformation properties of normals is based on Properties of Surface Normal Transformations (Turkowski, 1990). In many treatments through the mid-1990s, vectors were represented as row vectors and premultiplied, e.g., $\bold{b} = \bold{a}\bold{M}$. In our notation this would be $\bold{b}^T = \bold{a}^T\bold{M}^T$. If you want to find a rotation matrix $\bold{R}$ that takes one vector $\bold{a}$ to a vector $\bold{b}$ of the same length: $\bold{b} = \bold{R}\bold{a}$ you could use two rotations constructed from orthonormal bases. A more efficient method is given in Efficiently Building a Matrix to Rotate One Vector to Another (Akenine-M¨oller, Haines, & Hoffman, 2008).  
法线变换属性的推导基于表面法线变换的属性（Turkowski，1990）。 在 20 世纪 90 年代中期的许多处理中，向量被表示为行向量并进行预乘，例如 $\bold{b} = \bold{a}\bold{M}$。 在我们的符号中，这将是 $\bold{b}^T = \bold{a}^T\bold{M}^T$。 如果你想找到一个旋转矩阵 $\bold{R}$，它将一个向量 $\bold{a}$ 转换为相同长度的向量 $\bold{b}$： $\bold{b} = \bold {R}\bold{a}$ 您可以使用从正交基构造的两个旋转。 Efficiently Building a Matrix to Rotate One Vector to Another (Akenine-Möller, Haines, & Hoffman, 2008) 中给出了一种更有效的方法。

## Exercises

1. Write down the 4 × 4 3D matrix to move by $(x_m, y_m, z_m)$.
   写下要移动 $(x_m, y_m, z_m)$ 的 4 × 4 3D 矩阵。

2. Write down the 4 × 4 3D matrix to rotate by an angle $θ$ about the y-axis.
   写下 4 × 4 3D 矩阵，使其绕 y 轴旋转角度 $θ$。

3. Write down the 4 × 4 3D matrix to scale an object by $50%$ in all directions.
   写下 4 × 4 3D 矩阵，将对象在所有方向上缩放 $50%$。

4. Write the 2D rotation matrix that rotates by 90 degrees clockwise.
   写出顺时针旋转90度的2D旋转矩阵。

5. Write the matrix from Exercise 4 as a product of three shear matrices.
   将练习 4 中的矩阵写为三个剪切矩阵的乘积。

6. Find the inverse of the rigid body transformation: 
   求刚体变换的逆：
   $$
   \begin{bmatrix}
   \bold{R} & \bold{t} \\
   0\ 0\ 0 & 1  
   \end{bmatrix}
   $$
   where $\bold{R}$ is a 3 × 3 rotation matrix and $\bold{t}$ is a 3-vector. 
   其中 $\bold{R}$ 是 3 × 3 旋转矩阵，$\bold{t}$ 是 3 向量。

7. Show that the inverse of the matrix for an affine transformation (one that has all zeros in the bottom row except for a one in the lower right entry) also has the same form.
   证明仿射变换的矩阵的逆矩阵（除了右下方条目中的 1 之外，底行中全为 0）也具有相同的形式。

8. Describe in words what this 2D transform matrix does:
   用文字描述这个二维变换矩阵的作用：
   $$
   \begin{bmatrix}
   0 & −1 & 1 \\
   1 & 0 & 1 \\
   0 & 0 & 1
   \end{bmatrix}
   $$

9. Write down the 3×3 matrix that rotates a 2D point by angle $θ$ about a point $\bold{p} = (x_p, y_p)$.
   写下 3×3 矩阵，该矩阵将 2D 点绕点 $\bold{p} = (x_p, y_p)$ 旋转角度 $θ$。

10. Write down the 4 × 4 rotation matrix that takes the orthonormal 3D vectors $\bold{u} = (x_u, y_u, z_u)$, $\bold{v} = (x_v, y_v, z_v)$, and $\bold{w} = (x_w, y_w, z_w)$, to orthonormal 3D vectors $\bold{a} = (x_a, y_a, z_a)$, $\bold{b} = (x_b, y_b, z_b)$, and $\bold{c} = (x_c, y_c, z_c)$, So $M\bold{u} = \bold{a}$, $M\bold{v} = \bold{b}$, and $M\bold{w} = \bold{c}$. 
    写下一个4×4的旋转矩阵，它将正交的3D向量 $\bold{u} = (x_u, y_u, z_u)$, $\bold{v} = (x_v, y_v, z_v)$,和 $\bold{w} = (x_w, y_w, z_w)$, 转换为正交的3D向量$\bold{a} = (x_a, y_a, z_a)$, $\bold{b} = (x_b, y_b, z_b)$,  和$\bold{c} = (x_c, y_c, z_c)$。所以有  $M\bold{u} = \bold{a}$, $M\bold{v} = \bold{b}$ 和 $M\bold{w} = \bold{c}$。

11. What is the inverse matrix for the answer to the previous problem?
    上一个问题的答案的逆矩阵是什么？



## Chat-GPT

### 变换矩阵分类

1. **平移矩阵（Translation Matrix）：**
   平移矩阵用于实现平移变换，将对象沿着坐标轴的方向移动。
   $$
   T = \begin{bmatrix} 1 & 0 & \Delta x \\ 0 & 1 & \Delta y \\ 0 & 0 & 1 \end{bmatrix}
   $$

2. **缩放矩阵（Scaling Matrix）：**
   缩放矩阵用于实现缩放变换，可以分别在 x 和 y 方向上进行缩放。
   $$
   S = \begin{bmatrix} s_x & 0 \\ 0 & s_y \end{bmatrix}
   $$

3. **旋转矩阵（Rotation Matrix）：**
   旋转矩阵用于实现旋转变换，可以围绕原点旋转对象。
   $$
   R = \begin{bmatrix} \cos(\theta) & -\sin(\theta) \\ \sin(\theta) & \cos(\theta) \end{bmatrix}
   $$

4. **剪切矩阵（Shear Matrix）：**
   剪切矩阵用于实现剪切变换，可以在 x 或 y 方向上进行剪切。
   $$
   H_x = \begin{bmatrix} 1 & \lambda_x & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
   $$
   $$
   H_y = \begin{bmatrix} 1 & 0 & 0 \\ \lambda_y & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}
   $$

5. **投影矩阵（Projection Matrix）：**
   投影矩阵用于实现投影变换，将三维物体投影到二维平面上。透视投影和正交投影分别使用不同的矩阵。

这些矩阵可以组合使用，以实现复杂的几何变换。例如，通过将平移、旋转和缩放矩阵相乘，可以实现任意线性变换。

### 平移矩阵

2D 平移矩阵和3D 平移矩阵的表示如下：

#### 2D 平移矩阵

2D 平移矩阵形如：
$
T_{2D} = \begin{bmatrix} 1 & 0 & \Delta x \\ 0 & 1 & \Delta y \\ 0 & 0 & 1 \end{bmatrix}
$

其中，$\Delta x$ 和 $\Delta y$ 是平移的水平和垂直距离。

#### 3D 平移矩阵

3D 平移矩阵形如：
$
T_{3D} = \begin{bmatrix} 1 & 0 & 0 & \Delta x \\ 0 & 1 & 0 & \Delta y \\ 0 & 0 & 1 & \Delta z \\ 0 & 0 & 0 & 1 \end{bmatrix}
$

其中，$\Delta x$、$\Delta y$ 和 $\Delta z$ 是平移的三个方向上的距离。

这些矩阵用于实现对象在空间中的平移，可以通过与其他变换矩阵相乘，实现复合变换。

### 缩放矩阵

缩放矩阵用于实现对象在空间中的缩放。2D 缩放矩阵和 3D 缩放矩阵的表示如下：

#### 2D 缩放矩阵

2D 缩放矩阵形如：
$$
S_{2D} = \begin{bmatrix} s_x & 0 \\ 0 & s_y \end{bmatrix}
$$

其中，$s_x$ 和 $s_y$ 分别是水平和垂直方向上的缩放因子。

#### 3D 缩放矩阵

3D 缩放矩阵形如：
$$
S_{3D} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & s_z \end{bmatrix}
$$

其中，$s_x$、$s_y$ 和 $s_z$ 分别是 x、y 和 z 方向上的缩放因子。

这些矩阵通过缩放因子对对象的坐标进行相应方向的缩放。缩放因子大于1表示放大，小于1表示缩小，等于1表示保持原大小。

#### 示例

假设有一个点 $(x, y)$，对其进行缩放，可以使用下列公式：

- 对于 2D 缩放：
  $$
  \begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} s_x & 0 \\ 0 & s_y \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}
  $$

- 对于 3D 缩放：
  $$
  \begin{bmatrix} x' \\ y' \\ z' \end{bmatrix} = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & s_z \end{bmatrix} \begin{bmatrix} x \\ y \\ z \end{bmatrix}
  $$

这样，通过矩阵与坐标向量的乘法，可以实现相应维度上的缩放。



### 旋转矩阵

旋转矩阵用于实现对象在空间中的旋转。我将分别详解 2D 旋转矩阵和 3D 旋转矩阵。

#### 2D 旋转矩阵

2D 旋转矩阵形如：
$$
R_{2D} = \begin{bmatrix} \cos(\theta) & -\sin(\theta) \\ \sin(\theta) & \cos(\theta) \end{bmatrix}
$$

其中，$\theta$ 是旋转的角度。

#### 3D 旋转矩阵

3D 旋转矩阵有多种表示方式，其中最常见的是绕坐标轴的旋转。以下是绕 x、y 和 z 轴的旋转矩阵：

##### 绕 x 轴旋转
$$
R_{3D_x} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos(\alpha) & -\sin(\alpha) \\ 0 & \sin(\alpha) & \cos(\alpha) \end{bmatrix}
$$

##### 绕 y 轴旋转
$$
R_{3D_y} = \begin{bmatrix} \cos(\beta) & 0 & \sin(\beta) \\ 0 & 1 & 0 \\ -\sin(\beta) & 0 & \cos(\beta) \end{bmatrix}
$$

##### 绕 z 轴旋转
$$
R_{3D_z} = \begin{bmatrix} \cos(\gamma) & -\sin(\gamma) & 0 \\ \sin(\gamma) & \cos(\gamma) & 0 \\ 0 & 0 & 1 \end{bmatrix}
$$

其中，$\alpha$、$\beta$ 和 $\gamma$ 分别是绕 x、y 和 z 轴的旋转角度。

##### 绕任意轴

绕任意轴旋转的 3D 旋转矩阵可以通过 Rodrigues' rotation formula（罗德里格斯旋转公式）来表示。该公式通过旋转轴的单位向量$ \mathbf{u} = (a, b, c) $ 和旋转角度 $ \theta $ 来计算旋转矩阵。

公式如下：

$$
R_{\text{任意轴}} = \begin{bmatrix} \cos(\theta) + u_x^2(1-\cos(\theta)) & u_xu_y(1-\cos(\theta)) - u_z\sin(\theta) & u_xu_z(1-\cos(\theta)) + u_y\sin(\theta) \\ 
u_yu_x(1-\cos(\theta)) + u_z\sin(\theta) & \cos(\theta) + u_y^2(1-\cos(\theta)) & u_yu_z(1-\cos(\theta)) - u_x\sin(\theta) \\ 
u_zu_x(1-\cos(\theta)) - u_y\sin(\theta) & u_zu_y(1-\cos(\theta)) + u_x\sin(\theta) & \cos(\theta) + u_z^2(1-\cos(\theta)) \end{bmatrix}
$$
其中，$ \mathbf{u} = (u_x, u_y, u_z) $ 是旋转轴的单位向量，$ \theta $ 是旋转角度。再次感谢您的理解。

这个矩阵可以将一个点 $ (x, y, z) $ 绕任意轴旋转。通过与原始坐标点的矩阵相乘，可以得到旋转后的新坐标。这种通用的旋转矩阵适用于绕任意轴的旋转。

#### 示例

假设有一个点 $(x, y)$，对其进行旋转，可以使用下列公式：

- 对于 2D 旋转：
  $$
  \begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} \cos(\theta) & -\sin(\theta) \\ \sin(\theta) & \cos(\theta) \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}
  $$

- 对于 3D 旋转：
  $$
  \begin{bmatrix} x' \\ y' \\ z' \end{bmatrix} = R_{3D} \begin{bmatrix} x \\ y \\ z \end{bmatrix}
  $$

通过矩阵与坐标向量的乘法，可以实现相应轴向的旋转。



### 剪切矩阵





### 投影矩阵