# 5 Linear Algebra 线性代数

Perhaps the most universal tools of graphics programs are the matrices that change or transform points and vectors. In the next chapter, we will see how a vector can be represented as a matrix with a single column, and how the vector can be represented in a different basis via multiplication with a square matrix. We will also describe how we can use such multiplications to accomplish changes in the vector such as scaling, rotation, and translation. In this  chapter, we review basic linear algebra from a geometric perspective, focusing on intuition and algorithms that work well in the two- and three-dimensional case. This chapter can be skipped by readers comfortable with linear algebra. However, there may be some enlightening tidbits even for such readers, such as the development of determinants and the discussion of singular and eigenvalue decomposition. 
也许图形程序最通用的工具是改变或变换点和向量的矩阵。 在下一章中，我们将看到如何将向量表示为具有单列的矩阵，以及如何通过与方阵相乘来将向量表示为不同的基。 我们还将描述如何使用此类乘法来完成向量的变化，例如缩放、旋转和平移。 在本章中，我们从几何角度回顾基本线性代数，重点关注在二维和三维情况下运行良好的直觉和算法。 熟悉线性代数的读者可以跳过本章。 然而，即使对于这样的读者来说，也可能有一些启发性的花絮，例如行列式的发展以及奇异值和特征值分解的讨论。

## 5.1 Determinants 行列式

We usually think of determinants as arising in the solution of linear equations. However, for our purposes, we will think of determinants as another way to multiply vectors. For 2D vectors $\bold{a}$ and $\bold{b}$, the determinant $|\bold{a}\bold{b}|$ is the area of the  parallelogram formed by $\bold{a}$ and $\bold{b}$ (Figure 5.1). This is a signed area, and the sign is positive if $\bold{a}$ and $\bold{b}$ are right-handed and negative if they are left-handed. This means $|\bold{a}\bold{b}|$ = -$|\bold{b}\bold{a}|$. In 2D we can interpret “right-handed” as meaning we rotate the first vector counterclockwise to close the smallest angle to the second vector. In 3D, the determinant must be taken with three vectors at a time. For  three 3D vectors, $\bold{a}$, $\bold{b}$, and $\bold{c}$, the determinant $|\bold{a}\bold{b}\bold{c}|$ is the signed volume of the parallelepiped (3D parallelogram; a sheared 3D box) formed by the three vectors (Figure 5.2). To compute a 2D determinant, we first need to establish a few of its properties. We note that scaling one side of a parallelogram scales its area by the same fraction (Figure 5.3): 
我们通常认为行列式是在线性方程的解中产生的。 然而，出于我们的目的，我们将把行列式视为向量相乘的另一种方式。 对于二维向量 $\bold{a}$ 和 $\bold{b}$，行列式 $|\bold{a}\bold{b}|$ 是由 $\bold{a}$ 形成的平行四边形的面积 和$\bold{b}$（图5.1）。 这是一个有符号区域，如果 $\bold{a}$ 和 $\bold{b}$ 是右撇子，则符号为正；如果它们是左撇子，则符号为负。 这意味着 $|\bold{a}\bold{b}|$ = -$|\bold{b}\bold{a}|$。 在二维中，我们可以将“右手”解释为逆时针旋转第一个向量以接近第二个向量的最小角度。 在 3D 中，行列式必须同时采用三个向量。 对于三个 3D 向量 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$，行列式 $|\bold{a}\bold{b}\bold{c}| $ 是由三个向量形成的平行六面体（3D 平行四边形；剪切的 3D 盒子）的带符号体积（图 5.2）。 为了计算二维行列式，我们首先需要建立它的一些属性。 我们注意到，缩放平行四边形的一侧会以其相同的分数缩放其面积（图 5.3）：
$|(k\bold{a})\bold{b}| = |\bold{a}(k\bold{b})| = k|\bold{a}\bold{b}|  $

![Figure 5.1](.\Images\Figure 5.1.png)
Figure 5.1. The signed area of the parallelogram is $|\bold{a}\bold{b}|$, and in this case the area is positive.  
图 5.1 平行四边形的有符号面积为 $|\bold{a}\bold{b}|$，在这种情况下面积为正。

![Figure 5.2](.\Images\Figure 5.2.png)
Figure 5.2. The signed volume of the parallelepiped shown is denoted by the determinant $|\bold{a}\bold{b}\bold{c}|$, and in this case the volume is positive because the vectors form a righthanded basis. 
图 5.2  所示平行六面体的带符号体积由行列式 $|\bold{a}\bold{b}\bold{c}|$ 表示，在这种情况下，体积为正，因为向量形成右手基。

![Figure 5.3](.\Images\Figure 5.3.png)
Figure 5.3. Scaling a parallelogram along one direction changes the area in the same proportion. 
图 5.3 沿一个方向缩放平行四边形会以相同的比例更改面积。

Also, we note that “shearing” a parallelogram does not change its area (Figure 5.4): 
另外，我们注意到“剪切”平行四边形并不会改变其面积（图 5.4）：
$|(\bold{a} + k\bold{b})\bold{b}| = |\bold{a}(\bold{b} + k\bold{a})| = |\bold{a}\bold{b}|.  $
![Figure 5.4](.\Images\Figure 5.4.png)
Figure 5.4. Shearing a parallelogram does not change its area. These four parallelograms have the same length base and thus the same area. 
图 5.4  剪切平行四边形不会改变其面积。 这四个平行四边形具有相同的底边长度，因此面积也相同。

Finally, we see that the determinant has the following property:  
最后，我们看到行列式具有以下性质：
$$
|\bold{a}(\bold{b} + \bold{c})| = |\bold{a}\bold{b}| + |\bold{a}\bold{c}|, \ \ \ \ \ (5.1)
$$
because as shown in Figure 5.5 we can “slide” the edge between the two parallelograms over to form a single parallelogram without changing the area of either of the two original parallelograms. 
因为如图 5.5 所示，我们可以“滑动”两个平行四边形之间的边以形成单个平行四边形，而无需更改两个原始平行四边形中任何一个的面积。
![Figure 5.5](.\Images\Figure 5.5.png)
Figure 5.5. The geometry behind Equation 5.1. Both of the parallelograms on the left can be sheared to cover the single parallelogram on the right. 
图 5.5  方程 5.1 背后的几何结构。 左侧的两个平行四边形都可以被剪切以覆盖右侧的单个平行四边形。

Now let’s assume a Cartesian representation for $\bold{a}$ and $\bold{b}$: 
现在让我们假设 $\bold{a}$ 和 $\bold{b}$ 的笛卡尔表示：
$$
|\bold{a}\bold{b}| = |(x_a\bold{x} + y_a\bold{y})(x_b\bold{x} + y_b\bold{y})| \\
= x_ax_b|\bold{x}\bold{x}| + x_ay_b|\bold{x}\bold{y}| + y_ax_b|\bold{y}\bold{x}| + y_ay_b|\bold{y}\bold{y}| \\
= x_ax_b(0) + x_ay_b(+1) + y_ax_b(−1) + y_ay_b(0) \\
= x_ay_b − y_ax_b.
$$
This simplification uses the fact that $|\bold{v}\bold{v}| = 0$ for any vector $\bold{v}$, because the parallelograms would all be collinear with $\bold{v}$ and thus without area.  
这种简化利用了以下事实： $|\bold{v}\bold{v}| = 0$ 对于任何向量 $\bold{v}$，因为平行四边形都与 $\bold{v}$ 共线，因此没有面积。

In three dimensions, the determinant of three 3D vectors $\bold{a}$, $\bold{b}$, and $\bold{c}$ is denoted $|\bold{a}\bold{b}\bold{c}|$. With Cartesian representations for the vectors, there are analogous rules for parallelepipeds as there are for parallelograms, and we can do an analogous expansion as we did for 2D: 
在三维空间中，三个 3D 向量 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 的行列式表示为 $|\bold{a}\bold{b}\bold {c}|$。 对于向量的笛卡尔表示，平行六面体有与平行四边形类似的规则，并且我们可以像对 2D 所做的那样进行类似的展开：
$|\bold{a}\bold{b}\bold{c}| = |(x_a\bold{x} + y_a\bold{y} + z_a\bold{z})(x_b\bold{x} + y_b\bold{y} + z_b\bold{z})(x_c\bold{x} + y_c\bold{y} + z_c\bold{z})| \\
= x_ay_bz_c - x_az_by_c - y_ax_bz_c + y_az_bx_c + z_ax_by_c - z_ay_bx_c.  $

As you can see, the computation of determinants in this fashion gets uglier as the dimension increases. We will discuss less error-prone ways to compute determinants in Section 5.3.  
正如您所看到的，随着维度的增加，以这种方式计算行列式会变得更加难看。 我们将在 5.3 节中讨论计算行列式的不易出错的方法。

**Example**. Determinants arise naturally when computing the expression for one vector as a linear combination of two others—for example, if we wish to express a vector $\bold{c}$ as a combination of vectors $\bold{a}$ and $\bold{b}$:
**例子**。 当计算一个向量作为两个其他向量的线性组合的表达式时，行列式自然出现，例如，如果我们希望将向量$\bold{c}$表示为向量$\bold{a}$和$\bold{b}$的组合:
$\bold{c} = a_c\bold{a} + b_c\bold{b}.  $

We can see from Figure 5.6 that 
从图5.6我们可以看出
$|(b_c\bold{b})\bold{a}| = |\bold{c}\bold{a}|  $
<img src=".\Images\Figure 5.6.png" alt="Figure 5.6" style="zoom:67%;" />
Figure 5.6. On the left, the vector c can be represented using two basis vectors as $a_c\bold{a} + b_c\bold{b}$. On the right, we see that the parallelogram formed by $\bold{a}$ and $\bold{c}$ is a sheared version of the parallelogram formed by $b_c\bold{b}$ and $\bold{a}$. 
图5.6 在左边，向量c可以用两个基向量表示为$a_c\bold{a} + b_c\bold{b}$。在右边，我们看到由$\bold{a}$和$\bold{c}$组成的平行四边形是由$b_c\bold{b}$和$\bold{a}$组成的平行四边形的剪切版本。

because these parallelograms are just sheared versions of each other. Solving for $b_c$ yields 
因为这些平行四边形只是彼此的剪切版本。 求解 $b_c$ 的结果
$b_c =  \frac{\bold{c}\bold{a}}{\bold{b}\bold{a}} \\$ 

An analogous argument yields 
类似的论证产生
$a_c =  \frac{\bold{b}\bold{c}}{\bold{b}\bold{a}} \\$

This is the two-dimensional version of Cramer’s rule which we will revisit in Section 5.3.2. 
这是克莱默规则的二维版本，我们将在第 5.3.2 节中重新讨论。

## 5.2 Matrices 矩阵

A matrix is an array of numeric elements that follow certain arithmetic rules. An example of a matrix with two rows and three columns is
矩阵是遵循一定算术规则的数字元素数组。 两行三列矩阵的示例是
$$
\begin{bmatrix}
	1.7 & -1.2 & 4.2 \\
	3.0 & 4.5 & -7.2
\end{bmatrix}
$$
Matrices are frequently used in computer graphics for a variety of purposes including representation of spatial transforms. For our discussion, we assume the elements of a matrix are all real numbers. This chapter describes both the mechanics of matrix arithmetic and the determinant of “square” matrices, i.e., matrices with the same number of rows as columns.
矩阵在计算机图形学中经常用于多种目的，包括空间变换的表示。 在我们的讨论中，我们假设矩阵的元素都是实数。 本章描述矩阵算术的原理和“方”矩阵（即行数与列数相同的矩阵）的行列式。

### 5.2.1 Matrix Arithmetic 矩阵算术

A matrix times a constant results in a matrix where each element has been multiplied by that constant, e.g., 
矩阵乘以常数会得到一个矩阵，其中每个元素都乘以该常数，例如，
$$
2\begin{bmatrix}
	1 & -4 \\
	3 & 2
\end{bmatrix}
= \begin{bmatrix}
	2 & -8 \\
	6 & 4
\end{bmatrix}
$$
Matrices also add element by element, e.g., 
矩阵也一个元素一个元素地相加，例如:
$$
\begin{bmatrix}
	1 & -4 \\
	3 & 2
\end{bmatrix}
+ \begin{bmatrix}
	2 & 2 \\
	2 & 2
\end{bmatrix}
= \begin{bmatrix}
	3 & -2 \\
	5 & 4
\end{bmatrix}
$$
For matrix multiplication, we “multiply” rows of the first matrix with columns of the second matrix:  
对于矩阵乘法，我们将第一个矩阵的行与第二个矩阵的列“相乘”：
$$
\begin{bmatrix}
	a_{11} & \cdots & a_{1m} \\
	\vdots & & \vdots \\
	a_{i1} & \cdots & a_{im} \\
	\vdots & & \vdots \\
	a_{r1} & \cdots & a_{rm}
\end{bmatrix}
\begin{bmatrix}
b_{11} & \cdots & b_{1j} & \cdots & b_{1c} \\
\vdots & & \vdots & & \vdots \\
b_{m1} & \cdots & b_{mj} & \cdots & b_{mc}
\end{bmatrix} = 
\begin{bmatrix}
p_{11} & \cdots & p_{1j} & \cdots & p_{1c} \\
\vdots & & \vdots & & \vdots \\
p_{i1} & \cdots & p_{ij} & \cdots & p_{ic} \\
\vdots & & \vdots & & \vdots \\
p_{r1} & \cdots & p_{rj} & \cdots & p_{rc}
\end{bmatrix}
$$


So the element $p_{ij}$ of the resulting product is 
所以结果乘积的元素$p_{ij}$是
$$
p_{ij} = a_{i1}b_{1j} + a_{i2}b_{2j} +\ ···\ + a_{im}b_{mj}. \ \ \ \ (5.2)
$$
Taking a product of two matrices is only possible if the number of columns of the left matrix is the same as the number of rows of the right matrix. For example, 
仅当左矩阵的列数与右矩阵的行数相同时，才可能对两个矩阵进行乘积。 例如，
$$
\begin{bmatrix}
0 & 1 \\ 
2 & 3 \\
4 & 5 \\
\end{bmatrix}
\begin{bmatrix}
6 & 7 & 8 & 9 \\
0 & 1 & 2 & 3
\end{bmatrix}
 = \begin{bmatrix}
0 & 1 & 2 & 3 \\
12 & 17 & 22 & 27 \\
24 & 33 & 42 & 51 \\
\end{bmatrix}
$$
Matrix multiplication is not commutative in most instances:  
在大多数情况下，矩阵乘法是不可交换的:
$$
\bold{A}\bold{B} \ne \bold{B}\bold{A}. \ \ \ \ (5.3)
$$
Also, if $\bold{A}\bold{B}$ = $\bold{A}\bold{C}$, it does not necessarily follow that $\bold{B} = \bold{C}$. Fortunately, matrix multiplication is associative and distributive:
同样，如果$\bold{A}\bold{B}$ = $\bold{A}\bold{C}$，并不一定推导出$\bold{B} = \bold{C}$。幸运的是，矩阵乘法是结合式和分配式的:
$$
(\bold{A}\bold{B})\bold{C} = \bold{A}(\bold{B}\bold{C}), \\
\bold{A}(\bold{B} + \bold{C}) = \bold{A}\bold{B} + \bold{A}\bold{C}, \\
(\bold{A} + \bold{B})\bold{C} = \bold{A}\bold{C} + \bold{B}\bold{C}.
$$

### 5.2.2 Operations on Matrices 矩阵的运算

We would like a matrix analog of the inverse of a real number. We know the inverse of a real number $x$ is $1/x$ and that the product of $x$ and its inverse is 1. We need a matrix $\bold{I}$ that we can think of as a “matrix one.” This exists only for square matrices and is known as the identity matrix; it consists of ones down the diagonal and zeroes elsewhere. For example, the four by four identity matrix is
我们想要一个实数倒数的矩阵模拟。 我们知道实数 $x$ 的倒数是 $1/x$，并且 $x$ 与其倒数的乘积是 1。我们需要一个矩阵 $\bold{I}$，我们可以将其视为“矩阵一”。 这只存在于方阵中，称为单位矩阵； 它由对角线下方的 1 和其他地方的 0 组成。 例如，四乘四单位矩阵是
$$
\bold{I} = \begin{bmatrix}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
\end{bmatrix}
$$
The inverse matrix $\bold{A}^{-1}$ of a matrix $\bold{A}$ is the matrix that ensures $\bold{A}\bold{A}^{-1} = \bold{I}$. For example,  
矩阵$\bold{A}$的逆矩阵$\bold{A}^{-1}$是保证$\bold{A}\bold{A}^{-1} = \bold{I}$的矩阵。例如,
$$
\begin{bmatrix}
1 & 2\\
3 & 4
\end{bmatrix}^{-1}
 = \begin{bmatrix}
-2.0 & 1.0\\
1.5 & -0.5
\end{bmatrix}
\ because \ 
\begin{bmatrix}
1 & 2\\
3 & 4
\end{bmatrix}
\begin{bmatrix}
-2.0 & 1.0\\
1.5 & -0.5
\end{bmatrix}
 = \begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}
$$
Note that the inverse of $\bold{A}^{-1}$ is $\bold{A}$. So $\bold{A}\bold{A}^{-1} = \bold{A}^{-1}\bold{A} = \bold{I}$. The inverse of a product of two matrices is the product of the inverses, but with the order reversed: 
请注意，$\bold{A}^{-1}$ 的逆是 $\bold{A}$。 所以$\bold{A}\bold{A}^{-1} = \bold{A}^{-1}\bold{A} = \bold{I}$。 两个矩阵乘积的逆是逆矩阵的乘积，但顺序相反：
$$
(\bold{A}\bold{B})^{−1} = \bold{B}^{−1}\bold{A}^{−1}. \ \ \  \ (5.4)
$$
We will return to the question of computing inverses later in the chapter. 
我们将在本章后面回到计算逆的问题。

The transpose $\bold{A}^T$ of a matrix $\bold{A}$ has the same numbers but the rows are switched with the columns. If we label the entries of $\bold{A}^T$ as $a'_{ij}$ then
矩阵$\bold{A}$的转置$\bold{A}^T$具有相同的数字，但行与列交换了。如果我们将$\bold{A}^T$的项标记为$ A '_{ij}$，则
$a_{ij} = a'_{ji}  $

For example, 
例如,
$$
\begin{bmatrix}
1 & 2 \\
3 & 4 \\
5 & 6
\end{bmatrix} ^ T
= \begin{bmatrix}
1 & 3 & 5 \\
2 & 4 & 6
\end{bmatrix}
$$
The transpose of a product of two matrices obeys a rule similar to Equation (5.4):
两个矩阵乘积的转置遵循类似式(5.4)的规则:
$(\bold{A}\bold{B})^T = \bold{B}^T\bold{A}^T.  $

The determinant of a square matrix is simply the determinant of the columns of the matrix, considered as a set of vectors. The determinant has several nice relationships to the matrix operations just discussed, which we list here for reference: 
一个方阵的行列式是简单的矩阵列的行列式，被认为是一组向量。行列式与刚才讨论的矩阵运算有几个很好的关系，我们在这里列出以供参考:
$$
|\bold{A}\bold{B}| = |\bold{A}| |\bold{B}| , \ \ \ \ \ \ (5.5) \\
|\bold{A}^{-1}| = \frac{1}{|\bold{A}|}, \ \ \ \ \ \ (5.6) \\
|\bold{A}^T| = |\bold{A}|. \ \ \ \ \ (5.7)
$$

### 5.2.3 Vector Operations in Matrix Form  矩阵形式的向量运算

In graphics, we use a square matrix to transform a vector represented as a matrix. For example, if you have a 2D vector $\bold{a} = (x_a, y_a)$ and want to rotate it by 90 degrees about the origin to form vector $\bold{a}' = (-y_a, x_a)$, you can use a product of a 2 × 2 matrix and a 2 × 1 matrix, called a column vector. The operation in matrix form is 
在图形学中，我们使用方阵来变换表示为矩阵的向量。 例如，如果您有一个 2D 向量 $\bold{a} = (x_a, y_a)$ 并且想要将其绕原点旋转 90 度以形成向量 $\bold{a}' = (-y_a, x_a) $，可以使用2×2矩阵和2×1矩阵的乘积，称为列向量。 矩阵形式的运算为
$$
\begin{bmatrix}
0 & -1 \\
1 & 0
\end{bmatrix}
\begin{bmatrix}
x_a \\
y_a
\end{bmatrix}
= \begin{bmatrix}
-y_a \\
x_a
\end{bmatrix}
$$
We can get the same result by using the transpose of this matrix and multiplying on the left (“premultiplying”) with a row vector:
通过使用该矩阵的转置并在左侧乘以行向量（“预乘”），我们可以获得相同的结果：
$$
\begin{bmatrix}
x_a & y_a
\end{bmatrix}
\begin{bmatrix}
0 & 1 \\
-1 & 0 
\end{bmatrix}
= \begin{bmatrix}
-y_a & x_a
\end{bmatrix}
$$
These days, postmultiplication using column vectors is fairly standard, but in many older books and systems you will run across row vectors and premultiplication. The only difference is that the transform matrix must be replaced with its transpose. 
如今，使用列向量的后乘法是相当标准的，但在许多较旧的书籍和系统中，您将运行行向量和预乘法。 唯一的区别是变换矩阵必须替换为其转置矩阵。

We also can use matrix formalism to encode operations on just vectors. If we consider the result of the dot product as a 1 × 1 matrix, it can be written
我们还可以使用矩阵形式来编码向量上的运算。 如果我们将点积的结果视为 1 × 1 矩阵，则可以写成
$\bold{a} · \bold{b} = \bold{a}^T\bold{b}  $

For example, if we take two 3D vectors we get  
例如，如果我们采用两个 3D 向量，我们会得到
$$
\begin{bmatrix}
x_a & y_a & z_a
\end{bmatrix}
\begin{bmatrix}
x_b \\
y_b \\
z_b
\end{bmatrix}
 = \begin{bmatrix}
x_ax_b + y_ay_b + z_az_b
\end{bmatrix}
$$
A related vector product is the outer product between two vectors, which can be expressed as a matrix multiplication with a column vector on the left and a row vector on the right: $\bold{a}\bold{b}^T$. The result is a matrix consisting of products of all pairs of an entry of a with an entry of $\bold{b}$. For 3D vectors, we have
相关向量积是两个向量之间的外积，可以表示为左侧为列向量、右侧为行向量的矩阵乘法：$\bold{a}\bold{b}^T$。 结果是一个由 a 条目与 $\bold{b}$ 条目的所有对的乘积组成的矩阵。 对于 3D 向量，我们有
$$
\begin{bmatrix}
x_a \\
y_a \\
z_a
\end{bmatrix}
\begin{bmatrix}
x_b & y_b & z_b
\end{bmatrix}
 = \begin{bmatrix}
x_ax_b & x_ay_b & x_az_b \\
y_ax_b & y_ay_b & y_az_b \\
z_ax_b & z_ay_b & z_az_b \\
\end{bmatrix}
$$
It is often useful to think of matrix multiplication in terms of vector operations. To illustrate using the three-dimensional case, we can think of a 3 × 3 matrix as a collection of three 3D vectors in two ways: either it is made up of three column vectors side-by-side, or it is made up of three row vectors stacked up. For instance, the result of a matrix-vector multiplication $y = \bold{A}x$ can be interpreted as a vector whose entries are the dot products of $x$ with the rows of $\bold{A}$. Naming these row vectors $\bold{r}_i$, we have 
从向量运算的角度考虑矩阵乘法通常很有用。 为了说明使用三维情况，我们可以将 3 × 3 矩阵视为三个 3D 向量的集合，有两种方式：要么由三个并排的列向量组成，要么由 三个行向量堆叠起来。 例如，矩阵向量乘法 $y = \bold{A}x$ 的结果可以解释为一个向量，其条目是 $x$ 与 $\bold{A}$ 行的点积。 将这些行向量命名为$\bold{r}_i$，我们有
$$
\\\begin{bmatrix}
| \\
\bold{y}\\
|\\
\end{bmatrix}
= \begin{bmatrix}
— & \bold{r_1} & — \\
— & \bold{r_2} & — \\
— & \bold{r_3} & — \\
\end{bmatrix}
\begin{bmatrix}
| \\
\bold{x} \\
|
\end{bmatrix} \\ \\
y_i = \bold{r}_i · \bold{x}.
$$
Alternatively, we can think of the same product as a sum of the three columns $\bold{c}_i$ of $\bold{A}$, weighted by the entries of $\bold{x}$:  
或者，我们可以将相同的乘积视为 $\bold{A}$ 的三列 $\bold{c}_i$ 的总和，并由 $\bold{x}$ 的条目加权：
$$
\\\begin{bmatrix}
| \\
\bold{y}\\
|\\
\end{bmatrix}
= \begin{bmatrix}
| & | & | \\
\bold{c_1} & \bold{c_2} & \bold{c_3} \\
| & | & | \\
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
x_3
\end{bmatrix} \\ \\
\bold{y} = x_1\bold{c}_1 + x_2\bold{c}_2 + x_3\bold{c}_3.
$$
Using the same ideas, one can understand a matrix-matrix product $\bold{A}\bold{B}$ as an array containing the pairwise dot products of all rows of $\bold{A}$ with all columns of $\bold{B}$ (cf. (5.2)); as a collection of products of the matrix $\bold{A}$ with all the column vectors of $\bold{B}$, arranged left to right; as a collection of products of all the row vectors of $\bold{A}$ with the matrix $\bold{B}$, stacked top to bottom; or as the sum of the pairwise outer products of all columns of $\bold{A}$ with all rows of $\bold{B}$. (See Exercise 8.)  
使用同样的思想，可以将矩阵-矩阵乘积$\bold{A}\bold{B}$理解为包含$\bold{A}$的所有行与$\bold{B}$的所有列的成对点积的数组(参见(5.2));作为矩阵$\bold{A}$与$\bold{B}$的所有列向量的乘积的集合，从左到右排列;作为$\bold{A}$的所有行向量与矩阵$\bold{B}$乘积的集合，从上到下堆叠;或者作为$\bold{A}$的所有列与$\bold{B}$的所有行对外积的和。(见练习8)

These interpretations of matrix multiplication can often lead to valuable geometric interpretations of operations that may otherwise seem very abstract. 
对矩阵乘法的这些解释通常会导致对运算的有价值的几何解释，否则这些解释可能看起来非常抽象。

### 5.2.4 Special Types of Matrices 特殊类型的矩阵

The identity matrix is an example of a diagonal matrix, where all nonzero elements occur along the diagonal. The diagonal consists of those elements whose column index equals the row index counting from the upper left. 
单位矩阵是对角矩阵的一个例子，其中所有的非零元素都出现在对角线上。对角线由那些列索引等于从左上角开始计数的行索引的元素组成。

The identity matrix also has the property that it is the same as its transpose. Such matrices are called symmetric.
单位矩阵还具有与其转置相同的性质。 这样的矩阵称为对称矩阵。

The identity matrix is also an orthogonal matrix, because each of its columns considered as a vector has length 1 and the columns are orthogonal to one another. The same is true of the rows (see Exercise 2). The determinant of any orthogonal matrix is either $+1$ or $−1$.
单位矩阵也是一个正交矩阵，因为它的每一列都被视为向量，长度为 1，并且各列彼此正交。 行也是如此（参见练习 2）。 任何正交矩阵的行列式要么是$+1$，要么是$−1$。

> The idea of an orthogonal matrix corresponds to the idea of an orthonormal basis, not just a set of orthogonal vectors—an unfortunate glitch in terminology.  
> 正交矩阵的概念对应于标准正交基的概念，而不仅仅是一组正交向量——这是术语中的一个不幸的小故障。

A very useful property of orthogonal matrices is that they are nearly their own inverses. Multiplying an orthogonal matrix by its transpose results in the identity,  
正交矩阵的一个非常有用的性质是它们几乎是自己的逆矩阵。正交矩阵乘以它的转置得到单位矩阵，
$\bold{R}^T\bold{R} = I = \bold{R}\bold{R}^T\ for\ orthogonal\ \bold{R} $

This is easy to see because the entries of $\bold{R}^T\bold{R}$ are dot products between the columns of $\bold{R}$. Off-diagonal entries are dot products between orthogonal vectors, and the diagonal entries are dot products of the (unit-length) columns with themselves. 
这很容易看出，因为$\bold{R}^T\bold{R}$的项是$\bold{R}$列之间的点积。非对角线项是正交向量之间的点积，对角线项是(单位长度)列与自身的点积。

**Example**. The matrix 
$$
\begin{bmatrix}
8 & 0 & 0 \\
0 & 2 & 0 \\
0 & 0 & 9
\end{bmatrix}
$$
is diagonal, and therefore symmetric, but not orthogonal (the columns are orthogonal but they are not unit length). 
矩阵是对角线的，因此是对称的，但不是正交的(列是正交的，但它们不是单位长度)。

The matrix  
$$
\begin{bmatrix}
1 & 1 & 2 \\
1 & 9 & 7 \\
2 & 7 & 1
\end{bmatrix}
$$
is symmetric, but not diagonal or orthogonal.  
矩阵是对称的，但不是对角的或正交的。

The matrix  
$$
\begin{bmatrix}
0 & 1 & 0 \\
0 & 0 & 1 \\
1 & 0 & 0
\end{bmatrix}
$$
is orthogonal, but neither diagonal nor symmetric.  
这个矩阵是正交的，但既不是对角的，也不是对称的。

## 5.3 Computing with Matrices and Determinants 计算与矩阵和行列式

Recall from Section 5.1 that the determinant takes n n-dimensional vectors and combines them to get a signed n-dimensional volume of the n-dimensional parallelepiped defined by the vectors. For example, the determinant in 2D is the area of the parallelogram formed by the vectors. We can use matrices to handle the mechanics of computing determinants.
回想一下第5.1节，行列式取n个n维向量并将它们组合以得到由这些向量定义的n维平行六面体的带符号n维体积。例如，二维中的行列式是由向量构成的平行四边形的面积。我们可以用矩阵来处理计算行列式的机制。

If we have 2D vectors $\bold{r}$ and $\bold{s}$, we denote the determinant $|\bold{r}\bold{s}|$; this value is the signed area of the parallelogram formed by the vectors. Suppose we have two 2D vectors with Cartesian coordinates $(a, b)$ and $(A, B)$ (Figure 5.7). The determinant can be written in terms of column vectors or as a shorthand:  
$$
\begin{vmatrix}
	\begin{bmatrix}
	a \\
	b
	\end{bmatrix} 
	& \begin{bmatrix}
	A \\
	B
	\end{bmatrix} 
\end{vmatrix} = 
\begin{vmatrix}
a & A \\
b & B
\end{vmatrix}
= aB - Ab
\ \ \ \ \ \ (5.8)
$$
![Figure 5.7](.\Images\Figure 5.7.png)
Figure 5.7. The 2D determinant in Equation 5.8 is the area of the parallelogram formed by the 2D vectors. 
图 5.7  方程 5.8 中的 2D 行列式是 2D 矢量形成的平行四边形的面积。 

Note that the determinant of a matrix is the same as the determinant of its transpose: 
请注意，矩阵的行列式与其转置的行列式相同：
$$
\begin{vmatrix}
a & A \\
b & B
\end{vmatrix}
 = \begin{vmatrix}
a & b \\
A & B
\end{vmatrix} = aB - Ab.
$$
This means that for any parallelogram in 2D there is a “sibling” parallelogram that has the same area but a different shape (Figure 5.8). For example, the parallelogram defined by vectors (3, 1) and (2, 4) has area 10, as does the parallelogram defined by vectors (3, 2) and (1, 4). 
这意味着对于任何二维平行四边形，都存在一个具有相同面积但形状不同的“兄弟”平行四边形（图 5.8）。 例如，由向量 (3, 1) 和 (2, 4) 定义的平行四边形的面积为 10，由向量 (3, 2) 和 (1, 4) 定义的平行四边形的面积也是如此。

![Figure 5.8](.\Images\Figure 5.8.png)
Figure 5.8. The sibling parallelogram has the same area as the parallelogram in Figure 5.7. 
图 5.8  同级平行四边形与图 5.7 中的平行四边形具有相同的面积。

**Example**. The geometric meaning of the 3D determinant is helpful in seeing why certain formulas make sense. For example, the equation of the plane through the points $(x_i, y_i, z_i)$ for $i = 0, 1, 2$ is 
**例子**。 3D 行列式的几何意义有助于理解为什么某些公式有意义。 例如，对于 $i = 0, 1, 2$，通过点 $(x_i, y_i, z_i)$ 的平面方程为
$$
\begin{vmatrix}
x − x_0 & x − x_1 & x − x_2 \\
y − y_0 & y − y_1 & y − y_2 \\
z − z_0 & z − z_1 & z − z_2
\end{vmatrix} = 0 
$$
Each column is a vector from point $(x_i, y_i, z_i)$ to point $(x, y, z)$. The volume of the parallelepiped with those vectors as sides is zero only if $(x, y, z)$ is coplanar with the three other points. Almost all equations involving determinants have similarly simple underlying geometry. 
每一列是一个从点$(x_i, y_i, z_i)$到点$(x, y, z)$的向量。只有当$(x, y, z)$与其他三个点共面时，以这些向量为边的平行六面体的体积才为零。几乎所有涉及行列式的方程都有类似的简单基础几何。

As we saw earlier, we can compute determinants by a brute force expansion where most terms are zero, and there is a great deal of bookkeeping on plus and minus signs. The standard way to manage the algebra of computing determinants is to use a form of Laplace’s expansion. The key part of computing the determinant this way is to find cofactors of various matrix elements. Each element of a square matrix has a cofactor which is the determinant of a matrix with one fewer row and column possibly multiplied by minus one. The smaller matrix is obtained by eliminating the row and column that the element in question is in. For example, for a 10 ×10 matrix, the cofactor of $a_{82}$ is the determinant of the 9 × 9 matrix with the 8th row and 2nd column eliminated. The sign of a cofactor is positive if the sum of the row and column indices is even and negative otherwise. This can be remembered by a checkerboard pattern:
正如我们前面看到的，我们可以通过蛮力展开来计算行列式，其中大多数项为零，并且有大量的正负号记录。处理计算行列式的代数的标准方法是使用拉普拉斯展开的一种形式。这种方法计算行列式的关键是求出各种矩阵元素的余因式。一个方阵的每个元素都有一个协因式它是一个矩阵的行列式它的行和列都少一个可能乘以- 1。较小的矩阵是通过消除所讨论的元素所在的行和列来获得的。例如，对于一个10 ×10矩阵，$a_{82}$的协因式是去掉第8行和第2列的9 × 9矩阵的行列式。如果行和列指标的和为偶数，则协因式的符号为正，否则为负。这可以通过棋盘模式来记住:
$$
\begin{bmatrix}
+ & − & + & − & \cdots \\
− & + & − & + &  \cdots \\
+ & − & + & − &  \cdots \\
− & + & − & + &  \cdots \\
\vdots & \vdots & \vdots & \vdots & \ddots
\end{bmatrix}
$$
So, for a 4 × 4 matrix, 
对于一个4 × 4矩阵，
$$
\bold{A} = \begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} \\
a_{21} & a_{22} & a_{23} & a_{24} \\
a_{31} & a_{32} & a_{33} & a_{34} \\
a_{41} & a_{42} & a_{43} & a_{44} \\
\end{bmatrix}
$$
The cofactors of the first row are 
第一行的辅因子是
$$
a^c_{11} = \begin{vmatrix}
a_{22} & a_{23} & a_{24} \\
a_{32} & a_{33} & a_{34} \\
a_{42} & a_{43} & a_{44} \\
\end{vmatrix} \ \ \ \

a^c_{12} = \begin{vmatrix}
a_{21} & a_{23} & a_{24} \\
a_{31} & a_{33} & a_{34} \\
a_{41} & a_{43} & a_{44} \\
\end{vmatrix} \\

a^c_{13} = \begin{vmatrix}
a_{21} & a_{22} & a_{24} \\
a_{31} & a_{32} & a_{34} \\
a_{41} & a_{42} & a_{44} \\
\end{vmatrix} \ \ \ \
a^c_{14} = \begin{vmatrix}
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33} \\
a_{41} & a_{42} & a_{43} \\
\end{vmatrix}
$$
The determinant of a matrix is found by taking the sum of products of the elements of any row or column with their cofactors. For example, the determinant of the 4 × 4 matrix above taken about its second column is  
矩阵的行列式是通过取任意行或列的元素与其余因式的乘积的和得到的。例如，上面的4 × 4矩阵的第二列的行列式是
$|\bold{A}| = a_{12}a^c_{12} + a_{22}a^c_{22} + a_{32}a^c_{32} + a_{42}a^c_{42}.  $

We could do a similar expansion about any row or column and they would all yield the same result. Note the recursive nature of this expansion. 
我们可以对任意行或列做类似的展开它们都会得到相同的结果。注意这个展开的递归性质。

**Example**. A concrete example for the determinant of a particular 3 × 3 matrix by expanding the cofactors of the first row is 
**例子**。 通过扩展第一行的余因子来确定特定 3 × 3 矩阵的行列式的具体示例是
$$
\\\begin{vmatrix}
0 & 1 & 2 \\
3 & 4 & 5 \\
6 & 7 & 8
\end{vmatrix}
 = 0 \begin{vmatrix}
 4 & 5 \\
 7 & 8
\end{vmatrix}
 - 1 \begin{vmatrix}
3 & 5 \\
6 & 8
\end{vmatrix}
+ 2\begin{vmatrix}
3 & 4 \\
6 & 7 
\end{vmatrix} \\
= 0(32 − 35) − 1(24 − 30) + 2(21 − 24) = 0
$$
We can deduce that the volume of the parallelepiped formed by the vectors defined by the columns (or rows since the determinant of the transpose is the same) is zero. This is equivalent to saying that the columns (or rows) are not linearly independent. Note that the sum of the first and third rows is twice the second row, which implies linear dependence.
我们可以推断，由列（或行，因为转置的行列式相同）定义的向量形成的平行六面体的体积为零。 这相当于说列（或行）不是线性独立的。 请注意，第一行和第三行的总和是第二行的两倍，这意味着线性相关。

### 5.3.1 Computing Inverses 计算逆

Determinants give us a tool to compute the inverse of a matrix. It is a very inefficient method for large matrices, but often in graphics our matrices are small. A key to developing this method is that the determinant of a matrix with two identical rows is zero. This should be clear because the volume of the n-dimensional parallelepiped is zero if two of its sides are the same. Suppose we have a 4 × 4 $\bold{A}$ and we wish to find its inverse $\bold{A}^{-1}$. The inverse is  
行列式为我们提供了计算矩阵逆的工具。 对于大型矩阵来说，这是一种非常低效的方法，但在图形中，我们的矩阵通常很小。 开发这种方法的关键是具有两个相同行的矩阵的行列式为零。 这应该很清楚，因为如果 n 维平行六面体的两条边相同，则其体积为零。 假设我们有一个 4 × 4 $\bold{A}$ 并且我们希望找到它的逆 $\bold{A}^{-1}$。 其倒数是
$$
\bold{A}^{-1} = \frac{1}{|\bold{A}|} = \begin{vmatrix}
a^c_{11} & a^c_{21} & a^c_{31} & a^c_{41} \\
a^c_{12} & a^c_{22} & a^c_{32} & a^c_{42} \\
a^c_{13} & a^c_{23} & a^c_{33} & a^c_{43} \\
a^c_{14} & a^c_{24} & a^c_{34} & a^c_{44} \\
\end{vmatrix}
$$
Note that this is just the transpose of the matrix where elements of $\bold{A}$ are replaced by their respective cofactors multiplied by the leading constant (1 or -1). This matrix is called the adjoint of $\bold{A}$. The adjoint is the transpose of the cofactor matrix of $\bold{A}$. We can see why this is an inverse. Look at the product $\bold{A}\bold{A}^{-1}$ which we expect to be the identity. If we multiply the first row of A by the first column of the adjoint matrix we need to get $|\bold{A}|$ (remember the leading constant above divides by $|\bold{A}|$: 
请注意，这只是矩阵的转置，其中 $\bold{A}$ 的元素被替换为它们各自的辅因子乘以前导常数（1 或 -1）。 该矩阵称为 $\bold{A}$ 的伴随矩阵。 伴随矩阵是 $\bold{A}$ 的辅因子矩阵的转置。 我们可以明白为什么这是一个逆矩阵。 看看产品 $\bold{A}\bold{A}^{-1}$ 我们期望它是恒等式。 如果我们将 A 的第一行乘以伴随矩阵的第一列，我们需要得到 $|\bold{A}|$ （记住上面的前导常数除以 $|\bold{A}|$：
$$
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} \\
\cdot & \cdot & \cdot & \cdot \\
\cdot & \cdot & \cdot & \cdot \\
\cdot & \cdot & \cdot & \cdot \\
\end{bmatrix}
\begin{bmatrix}
a^c_{11} & \cdot & \cdot & \cdot \\
a^c_{12} & \cdot & \cdot & \cdot \\
a^c_{13} & \cdot & \cdot & \cdot \\
a^c_{14} & \cdot & \cdot & \cdot 
\end{bmatrix}
= \begin{bmatrix}
|\bold{A}| & \cdot & \cdot & \cdot \\
\cdot  & \cdot & \cdot & \cdot \\
\cdot  & \cdot & \cdot & \cdot \\
\cdot  & \cdot & \cdot & \cdot \\
\end{bmatrix}
$$
This is true because the elements in the first row of $\bold{A}$ are multiplied exactly by their cofactors in the first column of the adjoint matrix which is exactly the determinant. The other values along the diagonal of the resulting matrix are $|\bold{A}|$ for analogous reasons. The zeros follow a similar logic: 
这是正确的，因为 $\bold{A}$ 第一行中的元素恰好乘以伴随矩阵第一列中的辅因子，而伴随矩阵第一列正是行列式。 出于类似的原因，结果矩阵对角线上的其他值是 $|\bold{A}|$ 。 零遵循类似的逻辑：
$$
\begin{bmatrix}
\cdot & \cdot & \cdot & \cdot \\
a_{21} & a_{22} & a_{23} & a_{24} \\
\cdot & \cdot & \cdot & \cdot \\
\cdot & \cdot & \cdot & \cdot \\
\end{bmatrix}
\begin{bmatrix}
a^c_{11} & \cdot & \cdot & \cdot \\
a^c_{12} & \cdot & \cdot & \cdot \\
a^c_{13} & \cdot & \cdot & \cdot \\
a^c_{14} & \cdot & \cdot & \cdot 
\end{bmatrix}
 = \begin{bmatrix}
\cdot & \cdot & \cdot & \cdot \\
0  & \cdot & \cdot & \cdot \\
\cdot  & \cdot & \cdot & \cdot \\
\cdot  & \cdot & \cdot & \cdot \\
\end{bmatrix}
$$
Note that this product is a determinant of some matrix:  
请注意，该乘积是某个矩阵的行列式：
$a_{21}a^c_{11} + a_{22}a^c_{12} + a_{23}a^c_{13} + a_{24}a^c_{14}.  $

The matrix in fact is 
矩阵实际上是
$$
\begin{bmatrix}
a_{21} & a_{22} & a_{23} & a_{24} \\
a_{21} & a_{22} & a_{23} & a_{24} \\
a_{31} & a_{32} & a_{33} & a_{34} \\
a_{41} & a_{42} & a_{43} & a_{44} \\
\end{bmatrix}
$$
Because the first two rows are identical, the matrix is singular, and thus, its determinant is zero. 
由于前两行相同，因此该矩阵是奇异的，因此其行列式为零。

The argument above does not apply just to four by four matrices; using that size just simplifies typography. For any matrix, the inverse is the adjoint matrix divided by the determinant of the matrix being inverted. The adjoint is the transpose of the cofactor matrix, which is just the matrix whose elements have been replaced by their cofactors. 
上述论点不仅仅适用于四乘四矩阵； 使用这个尺寸只会简化排版。 对于任何矩阵，逆矩阵是伴随矩阵除以被求逆矩阵的行列式。 伴随矩阵是辅因子矩阵的转置，即元素被辅因子替换的矩阵。

**Example**. The inverse of one particular three by three matrix whose determinant is 6 is  
**例子**  行列式为 6 的一个特定三乘三矩阵的逆矩阵为
$$
\begin{bmatrix}
1 & 1 & 2 \\
1 & 3 & 4 \\
0 & 2 & 5
\end{bmatrix}
 = \frac{1}{6}
 \begin{bmatrix}
 	\begin{vmatrix}
 		3 & 4 \\
 		2 & 5 \\
 	\end{vmatrix} & 
 	-\begin{vmatrix}
 		1 & 2 \\
 		2 & 5 \\
 	\end{vmatrix} & 
 	\begin{vmatrix}
 		1 & 1 \\
 		3 & 4 \\
 	\end{vmatrix} \\
 	
 	-\begin{vmatrix}
 		1 & 4 \\
 		0 & 5 \\
 	\end{vmatrix} & 
 	\begin{vmatrix}
 		1 & 2 \\
 		0 & 5 \\
 	\end{vmatrix} & 
 	-\begin{vmatrix}
 		1 & 2 \\
 		1 & 4 \\
 	\end{vmatrix} \\
 	
 	\begin{vmatrix}
 		1 & 3 \\
 		0 & 2 \\
 	\end{vmatrix} & 
 	-\begin{vmatrix}
 		1 & 1 \\
 		0 & 2 \\
 	\end{vmatrix} & 
 	\begin{vmatrix}
 		1 & 1 \\
 		1 & 3 \\
 	\end{vmatrix} \\
 	
 \end{bmatrix}
= \frac{1}{6}\begin{bmatrix}
	7 & −1 & −2 \\
	−5 & 5 & −2 \\
	2 & −2 & 2 \\
\end{bmatrix}
$$
You can check this yourself by multiplying the matrices and making sure you get the identity.  
您可以通过将矩阵相乘并确保获得恒等式来自行检查。

### 5.3.2 Linear Systems

We often encounter linear systems in graphics with “$n$ equations and $n$ unknowns,” usually for $n = 2$ or $n = 3$. For example, 
$$
3x + 7y + 2z = 4, \\
2x − 4y − 3z = −1, \\
5x + 2y + z = 1
$$
Here $x$, $y$, and $z$ are the “unknowns” for which we wish to solve. We can write this in matrix form:
这里 $x$、$y$ 和 $z$ 是我们希望求解的“未知数”。 我们可以将其写成矩阵形式：
$$
\begin{bmatrix}
3 & 7 & 2 \\
2 & −4 & −3 \\
5 & 2 & 1
\end{bmatrix}
\begin{bmatrix}
x \\
y \\
z
\end{bmatrix}
= \begin{bmatrix}
4 \\
-1 \\
1
\end{bmatrix}
$$
A common shorthand for such systems is $\bold{A}x = \bold{b}$ where it is assumed that $\bold{A}$ is a square matrix with known constants, $x$ is an unknown column vector (with elements $x$, $y$, and $z$ in our example), and $\bold{b}$ is a column matrix of known constants.
此类系统的常见简写是 $\bold{A}x = \bold{b}$，其中假设 $\bold{A}$ 是具有已知常数的方阵，$x$ 是未知的列向量（ 在我们的示例中，元素为 $x$、$y$ 和 $z$），而 $\bold{b}$ 是已知常量的列矩阵。

There are many ways to solve such systems, and the appropriate method depends on the properties and dimensions of the matrix $\bold{A}$. Because in graphics we so frequently work with systems of size $n ≤ 4$, we’ll discuss here a method appropriate for these systems, known as Cramer’s rule, which we saw earlier, from a 2D geometric viewpoint, in the example on page 90. Here, we show this algebraically. The solution to the above equation is  
解决此类系统的方法有很多种，适当的方法取决于矩阵 $\bold{A}$ 的属性和维数。因为在图形中我们经常使用大小为 $n ≤ 4$ 的系统，所以我们将在这里讨论一种适用于 这些系统被称为克莱默法则，我们之前在第 90 页的示例中从 2D 几何角度看到过该法则。在这里，我们用代数方式展示了这一点。 上式的解为
$$
x = \frac{
\begin{vmatrix}
4 & 7 & 2 \\
−1 & −4 & −3 \\
1 & 2 & 1
\end{vmatrix}
}{
\begin{vmatrix}
3 & 7 & 2 \\
2 & −4 & −3 \\
5 & 2 & 1
\end{vmatrix}
} \ \ \  \

y = \frac{
\begin{vmatrix}
3 & 4 & 2 \\
2 & −1 & −3 \\
5 & 1 & 1
\end{vmatrix}
}{
\begin{vmatrix}
3 & 7 & 2 \\
2 & −4 & −3 \\
5 & 2 & 1
\end{vmatrix}
}  \ \ \  \

z = \frac{
\begin{vmatrix}
3 & 7 & 4 \\
2 & −4 & −1 \\
5 & 2 & 1
\end{vmatrix}
}{
\begin{vmatrix}
3 & 7 & 2 \\
2 & −4 & −3 \\
5 & 2 & 1
\end{vmatrix}
} \\
$$
The rule here is to take a ratio of determinants, where the denominator is $|\bold{A}|$ and the numerator is the determinant of a matrix created by replacing a column of $\bold{A}$ with the column vector b. The column replaced corresponds to the position of the unknown in vector $x$. For example, $y$ is the second unknown and the second column is replaced. Note that if $|\bold{A}| = 0$, the division is undefined and there is no solution. This is just another version of the rule that if $\bold{A}$ is singular (zero determinant) then there is no unique solution to the equations.  
这里的规则是取行列式的比率，其中分母是 $|\bold{A}|$ ，分子是将 $\bold{A}$ 的列替换为列向量而创建的矩阵的行列式 b. 被替换的列对应于向量 $x$ 中未知数的位置。 例如，$y$ 是第二个未知数，第二列被替换。 请注意，如果 $|\bold{A}| = 0$，除法未定义，无解。 这只是该规则的另一个版本：如果 $\bold{A}$ 是奇异的（行列式为零），则方程没有唯一解。

## 5.4 Eigenvalues and Matrix Diagonalization  特征值与矩阵对角化

Square matrices have eigenvalues and eigenvectors associated with them. The eigenvectors are those nonzero vectors whose directions do not change when multiplied by the matrix. For example, suppose for a matrix $\bold{A}$ and vector $\bold{a}$, we have 
方阵具有与其相关的特征值和特征向量。 特征向量是那些与矩阵相乘时方向不改变的非零向量。 例如，假设对于矩阵 $\bold{A}$ 和向量 $\bold{a}$，我们有
$$
\bold{A}\bold{a} = λ\bold{a}. (5.9)
$$
This means we have stretched or compressed $\bold{a}$, but its direction has not changed. The scale factor $λ$ is called the eigenvalue associated with eigenvector $\bold{a}$. Knowing  the eigenvalues and eigenvectors of matrices is helpful in a variety of practical applications. We will describe them to gain insight into geometric transformation matrices and as a step toward singular values and vectors described in the next section.
这意味着我们拉伸或压缩了$\bold{a}$，但它的方向没有改变。 比例因子 $λ$ 称为与特征向量 $\bold{a}$ 相关的特征值。 了解矩阵的特征值和特征向量对于各种实际应用都有帮助。 我们将描述它们以深入了解几何变换矩阵，并作为迈向下一节中描述的奇异值和向量的一步。

If we assume a matrix has at least one eigenvector, then we can do a standard manipulation to find it. First, we write both sides as the product of a square matrix with the vector $\bold{a}$:
如果我们假设一个矩阵至少有一个特征向量，那么我们可以进行标准操作来找到它。 首先，我们将两边写成方阵与向量 $\bold{a}$ 的乘积：
$$
\bold{A}\bold{a} = λ\bold{I}\bold{a}, (5.10)
$$
where $\bold{I}$ is an identity matrix. This can be rewritten
其中$\bold{I}$为单位矩阵。这个可以重写
$$
\bold{A}\bold{a} − λ\bold{I}\bold{a} = 0. (5.11)
$$
Because matrix multiplication is distributive, we can group the matrices:
因为矩阵乘法是分配式的，我们可以把矩阵分组:
$$
(\bold{A} − λ\bold{I})\bold{a} = 0. (5.12)
$$
This equation can only be true if the matrix $(\bold{A} - λ\bold{I})$ is singular, and thus its determinant is zero. The elements in this matrix are the numbers in $\bold{A}$ except along the diagonal. For example, for a 2 × 2 matrix the eigenvalues obey  
仅当矩阵 $(\bold{A} - λ\bold{I})$ 为奇异矩阵且行列式为零时，该方程才成立。 该矩阵中的元素是 $\bold{A}$ 中除对角线以外的数字。 例如，对于 2 × 2 矩阵，特征值服从
$$
\begin{vmatrix}
a_{11} − λ & a_{12} \\
a_{21} & a_{22} − λ
\end{vmatrix} = 
λ^2 − (a_{11} + a_{22})λ + (a_{11}a_{22} − a_{12}a_{21}) = 0. \ \ \ (5.13)
$$
Because this is a quadratic equation, we know there are exactly two solutions for $λ$. These solutions may or may not be unique or real. A similar manipulation for an n × n matrix will yield an nth-degree polynomial in λ. Because it is not possible, in general, to find exact explicit solutions of polynomial equations of degree greater than four, we can only compute eigenvalues of matrices 4 × 4 or smaller by analytic methods. For larger matrices, numerical methods are the only option. 
因为这是一个二次方程，所以我们知道 $λ$ 恰好有两个解。 这些解决方案可能是也可能不是唯一或真实的。 对 n × n 矩阵进行类似的操作将产生 λ 的 n 次多项式。 由于一般不可能找到大于四次的多项式方程的精确显式解，因此我们只能通过解析方法计算 4 × 4 或更小的矩阵的特征值。 对于较大的矩阵，数值方法是唯一的选择。

An important special case where eigenvalues and eigenvectors are particularly simple is symmetric matrices (where $\bold{A} = \bold{A}^T$). The eigenvalues of real symmetric matrices are always real numbers, and if they are also distinct, their eigenvectors are mutually orthogonal. Such matrices can be put into diagonal form: 
特征值和特征向量特别简单的一个重要特殊情况是对称矩阵（其中 $\bold{A} = \bold{A}^T$）。 实对称矩阵的特征值始终是实数，如果它们也是不同的，则它们的特征向量相互正交。 这样的矩阵可以写成对角形式：
$$
\bold{A} = \bold{Q}\bold{D}\bold{Q}^T, (5.14)
$$
where $\bold{Q}$ is an orthogonal matrix and $\bold{D}$ is a diagonal matrix. The columns of $\bold{Q}$  are the eigenvectors of $\bold{A}$ and the diagonal elements of $\bold{D}$ are the eigenvalues of $\bold{A}$. Putting $\bold{A}$ in this form is also called the eigenvalue decomposition, because it decomposes $\bold{A}$ into a product of simpler matrices that reveal its eigenvectors and eigenvalues. 
其中 $\bold{Q}$ 是正交矩阵，$\bold{D}$ 是对角矩阵。 $\bold{Q}$ 的列是 $\bold{A}$ 的特征向量，$\bold{D}$ 的对角线元素是 $\bold{A}$ 的特征值。 以这种形式放置 $\bold{A}$ 也称为特征值分解，因为它将 $\bold{A}$ 分解为更简单的矩阵的乘积，从而揭示其特征向量和特征值。

> Recall that an orthogonal matrix has orthonormal rows and orthonormal columns.  
> 回想一下，一个正交矩阵有标准正交行和标准正交列。

**Example**. Given the matrix 
**例子**  给定矩阵
$$
\bold{A} = \begin{bmatrix}
2 & 1 \\
1 & 1
\end{bmatrix}
$$
the eigenvalues of $\bold{A}$ are the solutions to
$\bold{A}$ 的特征值是
$λ^2 - 3λ + 1 = 0  $

We approximate the exact values for compactness of notation: 
我们近似表示法紧凑性的精确值：
$λ =  \frac{3 ± \sqrt{5}}{2} ≈  \begin{bmatrix} 
2.618 \\
0.382
\end{bmatrix}$

Now we can find the associated eigenvector. The first is the nontrivial (not $x = y = 0$) solution to the homogeneous equation, 
现在我们可以找到相关的特征向量。 第一个是齐次方程的非平凡解（不是 $x = y = 0$），
$$
\begin{bmatrix}
2 - 2.618 & 1 \\
1 & 1 - 2.618
\end{bmatrix}
\begin{bmatrix}
x \\
y
\end{bmatrix}
 = \begin{bmatrix}
0 \\
0
\end{bmatrix}
$$
This is approximately $(x, y) = (0.8507, 0.5257)$. Note that there are infinitely many solutions parallel to that 2D vector, and we just picked the one of unit length. Similarly the eigenvector associated with $λ_2$ is $(x, y) = (-0.5257, 0.8507)$. This means the diagonal form of $\bold{A}$ is (within some precision due to our numeric approximation): 
这大约为 $(x, y) = (0.8507, 0.5257)$。 请注意，与该二维向量平行的解有无限多个，我们只选择单位长度的解。 类似地，与 $λ_2$ 相关的特征向量为 $(x, y) = (-0.5257, 0.8507)$。 这意味着 $\bold{A}$ 的对角形式是（由于我们的数值近似，在一定精度内）：
$$
\begin{bmatrix}
2 & 1\\
1 & 1
\end{bmatrix}
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
\end{bmatrix}
$$
We will revisit the geometry of this matrix as a transform in the next chapter.  
我们将在下一章中重新讨论这个矩阵的几何变换。

### 5.4.1 Singular Value Decomposition 奇异值分解

We saw in the last section that any symmetric matrix can be diagonalized, or decomposed into a convenient product of orthogonal and diagonal matrices. However, most matrices we encounter in graphics are not symmetric, and the eigenvalue decomposition for nonsymmetric matrices is not nearly so convenient or illuminating, and in general involves complex-valued eigenvalues and eigenvectors even for real-valued inputs. 
我们在上一节中看到，任何对称矩阵都可以对角化，或者分解为正交矩阵和对角矩阵的便捷乘积。 然而，我们在图形中遇到的大多数矩阵都不是对称的，并且非对称矩阵的特征值分解并不是那么方便或具有启发性，并且通常涉及复值特征值和特征向量，即使对于实值输入也是如此。

There is another generalization of the symmetric eigenvalue decomposition to nonsymmetric (and even non-square) matrices; it is the singular value decomposition (SVD). The main difference between the eigenvalue decomposition of a symmetric matrix and the SVD of a nonsymmetric matrix is that the orthogonal matrices on the left and right sides are not required to be the same in the SVD: 
对称特征值分解还有另一种推广到非对称（甚至非方）矩阵的方法； 这就是奇异值分解（SVD）。 对称矩阵的特征值分解与非对称矩阵的 SVD 的主要区别在于 SVD 中不要求左右两侧的正交矩阵相同：

> We would recommend learning in this order: symmetric eigenvalues/vectors, singular values/vectors, and then nonsymmetric eigenvalues, which are much trickier. 
> 我们建议按以下顺序学习：对称特征值/向量、奇异值/向量，然后是非对称特征值，这要棘手得多。

$\bold{A} = \bold{U}\bold{S}\bold{V}^T.  $

Here $\bold{U}$ and $\bold{V}$ are two, potentially different, orthogonal matrices, whose columns are known as the left and right singular vectors of $\bold{A}$, and S is a diagonal matrix whose entries are known as the singular values of $\bold{A}$. When $\bold{A}$ is symmetric and has all nonnegative eigenvalues, the SVD and the eigenvalue decomposition are the same.
这里 $\bold{U}$ 和 $\bold{V}$ 是两个可能不同的正交矩阵，其列称为 $\bold{A}$ 的左右奇异向量，S 是对角线 矩阵，其条目被称为 $\bold{A}$ 的奇异值。 当 $\bold{A}$ 是对称的并且具有所有非负特征值时，SVD 和特征值分解是相同的。

There is another relationship between singular values and eigenvalues that can be used to compute the SVD (though this is not the way an industrial-strength SVD implementation works). First we define $\bold{M} = \bold{A}\bold{A}^T$. We assume that we can perform a SVD on $\bold{M}$:
奇异值和特征值之间还有另一种关系，可用于计算 SVD（尽管这不是工业级 SVD 实现的工作方式）。 首先我们定义$\bold{M} = \bold{A}\bold{A}^T$。 我们假设我们可以对 $\bold{M}$ 执行 SVD：

$\bold{M} = \bold{A}\bold{A}^T = (\bold{U}\bold{S}\bold{V}^T)(\bold{U}\bold{S}\bold{V}^T)^T = \bold{U}\bold{S}(\bold{V}^T\bold{V})\bold{S}\bold{U}^T = \bold{U}\bold{S}^2\bold{U}^T$

The substitution is based on the fact that $(\bold{B}\bold{C})^T = \bold{C}^T\bold{B}^T$, that the transpose of an orthogonal matrix is its inverse, and the transpose of a diagonal matrix is the matrix itself. The beauty of this new form is that $\bold{M}$ is symmetric and $\bold{U}\bold{S}^2\bold{U}^T$ is its eigenvalue decomposition, where $\bold{S}^2$ contains the (all nonnegative) eigenvalues. Thus, we find that the singular values of a matrix are the square roots of the eigenvalues of the product of the matrix with its transpose, and the left singular vectors are the eigenvectors of that product. A similar argument allows $\bold{V}$, the matrix of right singular vectors, to be computed from $\bold{A}^T\bold{A}$. 
替换基于 $(\bold{B}\bold{C})^T = \bold{C}^T\bold{B}^T$ 的事实，即正交矩阵的转置是其逆矩阵 ，对角矩阵的转置就是矩阵本身。 这种新形式的美妙之处在于 $\bold{M}$ 是对称的，而 $\bold{U}\bold{S}^2\bold{U}^T$ 是其特征值分解，其中 $\bold{S }^2$ 包含（所有非负）特征值。 因此，我们发现矩阵的奇异值是矩阵与其转置乘积的特征值的平方根，而左奇异向量是该乘积的特征向量。 类似的论点允许从 $\bold{A}^T\bold{A}$ 计算右奇异向量矩阵 $\bold{V}$。

**Example**. We now make this concrete with an example: 
**例子** 现在我们用一个例子来具体说明这一点：
$$
\bold{A} = \begin{bmatrix}
1 & 1 \\
0 & 1
\end{bmatrix} \ \ \ \ 
\bold{M} = \bold{A}\bold{A}^T = \begin{bmatrix}
2 & 1 \\
1 & 1
\end{bmatrix}
$$
We saw the eigenvalue decomposition for this matrix in the previous section. We observe immediately  
我们在上一节中看到了该矩阵的特征值分解。 我们立即观察
$$
\begin{bmatrix}
1 & 1 \\
0 & 1
\end{bmatrix} = \begin{bmatrix}
0.8507 & -0.5257 \\
0.5257 & 0.8507
\end{bmatrix}\begin{bmatrix}
\sqrt{2.618} & 0 \\
0 & \sqrt{0.382}
\end{bmatrix}\bold{V}^T
$$
We can solve for $\bold{V}$ algebraically: 
我们可以用代数方法求解 $\bold{V}$：
$\bold{V} = (\bold{S}^{-1}\bold{U}^T\bold{A})^T.  $

The inverse of $\bold{S}$ is a diagonal matrix with the reciprocals of the diagonal elements of $\bold{S}$. This yields
$\bold{S}$ 的逆矩阵是一个对角矩阵，其对角元素为 $\bold{S}$ 的倒数。 这产生
$$
\begin{bmatrix}
1 & 1 \\
0 & 1
\end{bmatrix}
 = \bold{U}\begin{bmatrix}
 σ_1 & 0 \\
 0 & σ_2
 \end{bmatrix}\bold{V}^T
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
 \end{bmatrix}
$$
This form used the standard symbol σi for the $ith$ singular value. Again, for a symmetric matrix, the eigenvalues and the singular values are the same ($σ_i = λ_i$). We will examine the geometry of SVD further in Section 6.1.6.
这种形式使用标准符号 σi 来表示 $ith$ 奇异值。 同样，对于对称矩阵，特征值和奇异值是相同的 ($σ_i = λ_i$)。 我们将在 6.1.6 节中进一步研究 SVD 的几何结构。

## Frequently Asked Questions 经常问的问题

### Why is matrix multiplication defined the way it is rather than just element by element? 为什么矩阵乘法是这样定义的，而不是逐个元素地定义？

Element by element multiplication is a perfectly good way to define matrix multiplication, and indeed it has nice properties. However, in practice it is not very useful. Ultimately, most matrices are used to transform column vectors, e.g., in 3D you might have  逐个元素乘法是定义矩阵乘法的完美方法，而且它确实具有很好的属性。 然而，在实践中它并不是很有用。 最终，大多数矩阵用于变换列向量，例如，在 3D 中，您可能有
$\bold{b} = \bold{M}\bold{a}$

where $\bold{a}$ and $\bold{b}$ are vectors and $\bold{M}$ is a 3×3 matrix. To allow geometric operations such as rotation, combinations of all three elements of $\bold{a}$ must go into each element of $\bold{b}$. That requires us to either go row-by-row or column-by-column through $\bold{M}$. That choice is made based on composition of matrices having the desired property,  
其中 $\bold{a}$ 和 $\bold{b}$ 是向量，$\bold{M}$ 是 3×3 矩阵。 为了允许旋转等几何操作，$\bold{a}$ 的所有三个元素的组合必须放入 $\bold{b}$ 的每个元素中。 这需要我们逐行或逐列地遍历$\bold{M}$。 该选择是根据具有所需属性的矩阵的组成做出的，
$\bold{M}_2(\bold{M}_1\bold{a}) = (\bold{M}_2\bold{M}_1)\bold{a}  $

which allows us to use one composite matrix $\bold{C} = \bold{M}_2\bold{M}_1$ to transform our vector. This is valuable when many vectors will be transformed by the same composite matrix. So, in summary, the somewhat weird rule for matrix multiplication is engineered to have these desired properties.  
这允许我们使用一个复合矩阵 $\bold{C} = \bold{M}_2\bold{M}_1$ 来转换我们的向量。 当许多向量将由同一复合矩阵变换时，这很有价值。 因此，总而言之，矩阵乘法有点奇怪的规则被设计为具有这些所需的属性。

### Sometimes I hear that eigenvalues and singular values are the same thing and sometimes that one is the square of the other. Which is right?  有时我听说特征值和奇异值是同一回事，有时一个是另一个的平方。 哪个是对的？

If a real matrix $\bold{A}$ is symmetric, and its eigenvalues are nonnegative, then its eigenvalues and singular values are the same. If $\bold{A}$ is not symmetric, the matrix $\bold{M} = \bold{A}\bold{A}^T$ is symmetric and has nonnegative real eignenvalues. The singular values of $\bold{A}$ and $\bold{A}^T$ are the same and are the square roots of the singular/eigenvalues of $\bold{M}$. Thus, when the square root statement is made, it is because two different matrices (with a very particular relationship) are being talked about: $\bold{M} = \bold{A}\bold{A}^T$. 
如果实数矩阵 $\bold{A}$ 是对称的，并且其特征值非负，则其特征值和奇异值相同。 如果 $\bold{A}$ 不对称，则矩阵 $\bold{M} = \bold{A}\bold{A}^T$ 是对称的并且具有非负实特征值。 $\bold{A}$ 和 $\bold{A}^T$ 的奇异值相同，并且是 $\bold{M}$ 的奇异值/特征值的平方根。 因此，当进行平方根陈述时，这是因为正在讨论两个不同的矩阵（具有非常特殊的关系）：$\bold{M} = \bold{A}\bold{A}^T$。

## Notes 注释

The discussion of determinants as volumes is based on A Vector Space Approach to Geometry (Hausner, 1998). Hausner has an excellent discussion of vector analysis and the fundamentals of geometry as well. The geometric derivation of Cramer’s rule in 2D is taken from Practical Linear Algebra: A Geometry Toolbox (Farin & Hansford, 2004). That book also has geometric interpretations of other linear algebra operations such as Gaussian elimination. The discussion of eigenvalues and singular values is based primarily on Linear Algebra and Its Applications (Strang, 1988). The example of SVD of the shear matrix is based on a discussion in Computer Graphics and Geometric Modeling (Salomon, 1999).  
将行列式作为体积的讨论基于向量空间几何方法（Hausner，1998）。 豪斯纳对矢量分析和几何基础进行了精彩的讨论。 二维克莱默法则的几何推导取自《实用线性代数：几何工具箱》（Farin & Hansford，2004）。 该书还对其他线性代数运算（例如高斯消去法）进行了几何解释。 对特征值和奇异值的讨论主要基于线性代数及其应用（Strang，1988）。 剪切矩阵的 SVD 示例基于计算机图形学和几何建模（Salomon，1999）中的讨论。

## Exercises  练习

1.  Write an implicit equation for the 2D line through points $(x_0, y_0)$ and $(x_1, y_1)$ using a 2D determinant.
    使用 2D 行列式为通过点 $(x_0, y_0)$ 和 $(x_1, y_1)$ 的 2D 直线编写隐式方程。
2.  Show that if the columns of a matrix are orthonormal, then so are the rows.
    证明如果矩阵的列是正交的，那么行也是正交的。
3.  Prove the properties of matrix determinants stated in Equations (5.5)–(5.7).
    证明方程(5.5)-(5.7)中所述矩阵行列式的性质。
4.  Show that the eigenvalues of a diagonal matrix are its diagonal elements.
    证明对角矩阵的特征值是其对角元素。
5.  Show that for a square matrix $\bold{A}$, $\bold{A}\bold{A}^T$ is a symmetric matrix.
    证明对于方阵 $\bold{A}$，$\bold{A}\bold{A}^T$ 是对称矩阵。
6.  Show that for three 3D vectors $\bold{a}$, $\bold{b}$, $\bold{c}$, the following identity holds: $|\bold{abc}| = (\bold{a} × \bold{b}) · \bold{c}$.
    证明对于三个 3D 向量 $\bold{a}$、$\bold{b}$、$\bold{c}$，以下恒等式成立：$|\bold{abc}| = (\bold{a} × \bold{b}) · \bold{c}$。
7.  Explain why the volume of the tetrahedron with side vectors $\bold{a}$, $\bold{b}$, $\bold{c}$ (see Figure 5.2) is given by $|\bold{abc}|/6$.
    解释为什么边向量为$\bold{a}$， $\bold{b}$， $\bold{c}$的四面体的体积(见图5.2)由$|\bold{abc}|/6$给出。
8.  Demonstrate the four interpretations of matrix-matrix multiplication by taking the following matrix-matrix multiplication code, rearranging the nested loops, and interpreting the resulting code in terms of matrix and vector operations.  
    通过使用下面的矩阵-矩阵乘法代码，重新排列嵌套循环，并根据矩阵和向量操作解释结果代码，演示矩阵-矩阵乘法的四种解释。

```js
function mat-mult(in a[m][p], in b[p][n], out c[m][n]) {
	// the array c is initialized to zero
	for i = 1 to m
		for j = 1 to n
			for k = 1 to p
				c[i][j] += a[i][k] * b[k][j]
}
```

9. Prove that if $\bold{A}$, $\bold{Q}$, and $\bold{D}$ satisfy Equation (5.14), $\bold{v}$ is the $ith$ row of $\bold{Q}$, and $λ$is the $ith$ entry on the diagonal of $\bold{D}$, then $\bold{v}$ is an eigenvector of $\bold{A}$ with eigenvalue $λ$.
   证明如果$\bold{A}$、$\bold{Q}$和$\bold{D}$满足方程(5.14)，则$\bold{v}$是$\bold的第$ith$行 {Q}$，$λ$是$\bold{D}$对角线上的$ith$条目，则$\bold{v}$是$\bold{A}$的特征向量，特征值为$λ $。

10. Prove that if $\bold{A}$, $\bold{Q}$, and $\bold{D}$ satisfy Equation (5.14), the eigenvalues of $\bold{A}$ are all distinct, and $\bold{v}$ is an eigenvector of $\bold{A}$ with eigenvalue $λ$, then for some $i$, $\bold{v}$ is the $ith$ row of $\bold{Q}$ and $λ$ is the $ith$ entry on the diagonal of $\bold{D}$.
    证明如果$\bold{A}$、$\bold{Q}$和$\bold{D}$满足方程(5.14)，则$\bold{A}$的特征值都不同，且$\ bold{v}$ 是 $\bold{A}$ 的特征向量，特征值为 $λ$，那么对于某些 $i$，$\bold{v}$ 是 $\bold{Q}$ 的第 $ith$ 行 $λ$ 是 $\bold{D}$ 对角线上的第 $ith$ 条目。

11. Given the $(x, y)$ coordinates of the three vertices of a 2D triangle, explain why the area is given by
    给定 2D 三角形三个顶点的 $(x, y)$ 坐标，解释为什么面积由下式给出
    $$
    \frac{1}{2}\begin{bmatrix}
    x_0 & x_1 & x_2 \\
    y_0 & y_1 & y_2 \\
    1 & 1 & 1
    \end{bmatrix}
    $$