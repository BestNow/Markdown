# 8  The Graphics Pipeline  图形管道

The previous several chapters have established the mathematical scaffolding we need to look at the second major approach to rendering: drawing objects one by one onto the screen, or object-order rendering. Unlike in ray tracing, where we consider each pixel in turn and find the objects that influence its color, we’ll now instead consider each geometric object in turn and find the pixels that it could have an effect on. The process of finding all the pixels in an image that are occupied by  a geometric primitive is called rasterization, so object-order rendering can also  be called rendering by rasterization. The sequence of operations that is required,  starting with objects and ending by updating pixels in the image, is known as the graphics pipeline.
前面几章已经建立了我们需要查看第二种主要渲染方法的数学支架：将对象一个接一个地绘制到屏幕上，或对象顺序渲染。 与光线追踪中我们依次考虑每个像素并找到影响其颜色的对象不同，我们现在将依次考虑每个几何对象并找到它可能产生影响的像素。 找到图像中某个几何图元所占据的所有像素的过程称为光栅化，因此对象顺序渲染也可以称为光栅化渲染。 所需的操作序列（从对象开始到更新图像中的像素结束）称为图形管道。

> Any graphics system has one or more types of “primitive object” that it can handle directly, and more complex objects are converted into these “primitives.” Triangles are the most often used primitive.
> 任何图形系统都有一种或多种可以直接处理的“原始对象”，更复杂的对象被转换为这些“原始对象”。 三角形是最常用的图元。

> Rasterization-based systems are also called scanline renderers. 
> 基于光栅化的系统也称为扫描线渲染器。

Object-order rendering has enjoyed great success because of its efficiency. For large scenes, management of data access patterns is crucial to performance, and making a single pass over the scene visiting each bit of geometry once has significant advantages over repeatedly searching the scene to retrieve the objects required to shade each pixel.
对象顺序渲染因其效率而获得了巨大的成功。 对于大型场景，数据访问模式的管理对于性能至关重要，与重复搜索场景以检索对每个像素进行着色所需的对象相比，对场景进行单次访问访问几何图形的每一位具有显着的优势。

The title of this chapter suggests that there is only one way to do objectorder rendering. Of course this isn’t true—two quite different examples of graphics pipelines with very different goals are the hardware pipelines used to support interactive rendering via APIs like OpenGL and Direct3D and the software pipelines used in film production, supporting APIs like RenderMan. Hardware pipelines must run fast enough to react in real time for games, visualizations, and user interfaces. Production pipelines must render the highest quality animation and visual effects possible and scale to enormous scenes, but may take much  more time to do so. Despite the different design decisions resulting from these divergent goals, a remarkable amount is shared among most, if not all, pipelines, and this chapter attempts to focus on these common fundamentals, erring on the side of following the hardware pipelines more closely.
本章的标题表明只有一种方法可以进行对象顺序渲染。 当然，这不是真的——两个截然不同的图形管道示例，目标截然不同，一个是用于通过 OpenGL 和 Direct3D 等 API 支持交互式渲染的硬件管道，另一个是电影制作中使用的支持 RenderMan 等 API 的软件管道。 硬件管道必须运行得足够快，才能对游戏、可视化和用户界面做出实时反应。 制作流程必须尽可能渲染最高质量的动画和视觉效果，并扩展到巨大的场景，但可能需要更多时间才能完成。 尽管这些不同的目标导致了不同的设计决策，但大多数（如果不是全部）管道之间共享了大量的数据，本章试图重点关注这些共同的基础知识，而不是更紧密地遵循硬件管道。

The work that needs to be done in object-order rendering can be organized into the task of rasterization itself, the operations that are done to geometry before rasterization, and the operations that are done to pixels after rasterization. The most common geometric operation is applying matrix transformations, as discussed in the previous two chapters, to map the points that define the geometry from object space to screen space, so that the input to the rasterizer is expressed in pixel coordinates, or screen space. The most common pixelwise operation is hidden surface removal which arranges for surfaces closer to the viewer to appear in front of surfaces farther from the viewer. Many other operations also can be included at each stage, thereby achieving a wide range of different rendering effects using the same general process.
对象顺序渲染中需要完成的工作可以组织为光栅化本身的任务、光栅化之前对几何图形执行的操作以及光栅化之后对像素执行的操作。 最常见的几何操作是应用矩阵变换，如前两章所述，将定义几何的点从对象空间映射到屏幕空间，以便光栅化器的输入以像素坐标或屏幕空间表示。 最常见的像素级操作是隐藏表面去除，它将靠近观察者的表面安排在距观察者较远的表面前面。 每个阶段还可以包括许多其他操作，从而使用相同的通用过程实现各种不同的渲染效果。

For the purposes of this chapter, we’ll discuss the graphics pipeline in terms of four stages (Figure 8.1). Geometric objects are fed into the pipeline from an interactive application or from a scene description file, and they are always described by sets of vertices. The vertices are operated on in the vertex-processing stage, then the primitives using those vertices are sent to the rasterization stage. The rasterizer breaks each primitive into a number of fragments, one for each pixel covered by the primitive. The fragments are processed in the fragment processing stage, and then the various fragments corresponding to each pixel are combined in the fragment blending stage.
为了本章的目的，我们将分四个阶段讨论图形管道（图 8.1）。 几何对象从交互式应用程序或场景描述文件输入到管道中，并且它们始终由顶点集描述。 顶点在顶点处理阶段进行操作，然后使用这些顶点的图元被发送到光栅化阶段。 光栅化器将每个基元分解为多个片段，一个片段对应于基元覆盖的每个像素。 在片段处理阶段对片段进行处理，然后在片段混合阶段将每个像素对应的各个片段进行组合。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.1.png" alt="Figure 8.1" style="zoom:67%;" />

Figure 8.1. The stages of a graphics pipeline.
图 8.1. 图形管道的阶段。

We’ll begin by discussing rasterization, then illustrate the purpose of the geometric and pixel-wise stages by a series of examples.
我们将从讨论光栅化开始，然后通过一系列示例说明几何和像素级阶段的目的。

## 8.1 Rasterization 光栅化

Rasterization is the central operation in object-order graphics, and the rasterizer is central to any graphics pipeline. For each primitive that comes in, the rasterizer has two jobs: it enumerates the pixels that are covered by the primitive and it interpolates values, called attributes, across the primitive—the purpose for these attributes will be clear with later examples. The output of the rasterizer is a set of fragments, one for each pixel covered by the primitive. Each fragment “lives” at a particular pixel and carries its own set of attribute values. 
光栅化是对象顺序图形中的核心操作，光栅化器是任何图形管道的核心。 对于每个进来的基元，光栅化器有两个工作：它枚举基元覆盖的像素，并在基元上插入值（称为属性） - 这些属性的用途将在后面的示例中清楚地显示出来。 光栅化器的输出是一组片段，每个片段对应图元覆盖的每个像素。 每个片段“存在”于特定的像素处并携带其自己的一组属性值。

In this chapter, we will present rasterization with a view toward using it to render three-dimensional scenes. The same rasterization methods are used to draw  lines and shapes in 2D as well—although it is becoming more and more common to use the 3D graphics system “under the covers” to do all 2D drawing.
在本章中，我们将介绍光栅化，以期使用它来渲染三维场景。 相同的光栅化方法也用于在 2D 中绘制线条和形状 - 尽管“在幕后”使用 3D 图形系统来完成所有 2D 绘图变得越来越普遍。

### 8.1.1 Line Drawing 画线

Most graphics packages contain a line drawing command that takes two endpoints in screen coodinates (see Figure 3.10) and draws a line between them. For example, the call for endpoints (1,1) and (3,2) would turn on pixels (1,1) and (3,2) and fill in one pixel between them. For general screen coordinate endpoints $(x_0, y_0)$ and $(x_1, y_1)$, the routine should draw some “reasonable” set of pixels that approximates a line between them. Drawing such lines is based on line equations, and we have two types of equations to choose from: implicit and parametric. This section describes the approach using implicit lines.
大多数图形包都包含一个线条绘制命令，该命令获取屏幕坐标中的两个端点（参见图 3.10）并在它们之间绘制一条线。 例如，对端点 (1,1) 和 (3,2) 的调用将打开像素 (1,1) 和 (3,2)，并在它们之间填充一个像素。 对于一般屏幕坐标端点 $(x_0, y_0)$ 和 $(x_1, y_1)$，例程应该绘制一些“合理”的像素集，近似它们之间的一条线。 绘制这样的线是基于线方程，我们有两种类型的方程可供选择：隐式方程和参数方程。 本节介绍使用隐式线的方法。  

> Even though we often use integer-valued endpoints for examples, it’s important to properly support arbitrary endpoints.
> 尽管我们经常使用整数值端点作为示例，但正确支持任意端点也很重要。

#### Line Drawing Using Implicit Line Equations 使用隐式直线方程绘制线条

The most common way to draw lines using implicit equations is the midpoint algorithm (Pitteway (1967); van Aken and Novak (1985)). The midpoint algorithm ends up drawing the same lines as the Bresenham algorithm (Bresenham, 1965) but it is somewhat more straightforward.
使用隐式方程绘制直线的最常见方法是中点算法（Pitteway (1967)；van Aken 和 Novak (1985)）。 中点算法最终绘制与 Bresenham 算法相同的线（Bresenham，1965），但它更简单一些。

The first thing to do is find the implicit equation for the line as discussed in Section 2.5.2:
首先要做的是找到直线的隐式方程，如第 2.5.2 节中所述：
$$
f(x, y) ≡ (y_0 − y_1)x + (x_1 − x_0)y + x_0y_1 − x_1y_0 = 0. (8.1)
$$
We assume that $x_0 ≤ x_1$. If that is not true, we swap the points so that it is true. The slope m of the line is given by
我们假设 $x_0 ≤ x_1$。 如果这不是真的，我们交换点以使其为真。 直线的斜率 m 由下式给出
$m = \frac{y_1 - y_0}{x_1 - x_0}\\$

The following discussion assumes $m ∈ (0, 1]$. Analogous discussions can be derived for $m ∈ (-∞, -1]$, $m ∈ (-1, 0]$, and $m ∈ (1, ∞)$. The four cases cover all possibilities. 
以下讨论假设 $m ∈ (0, 1]$。类似的讨论可以推导出 $m ∈ (-∞, -1]$、$m ∈ (-1, 0]$ 和 $m ∈ (1, ∞)$.这四种情况涵盖了所有的可能性。

For the case m ∈ (0, 1], there is more “run” than “rise,” i.e., the line is moving faster in x than in y. If we have an API where the y-axis points downward, we might have a concern about whether this makes the process harder, but, in fact, we can ignore that detail. We can ignore the geometric notions of “up” and “down,” because the algebra is exactly the same for the two cases. Cautious readers can confirm that the resulting algorithm works for the y-axis downward case. The key assumption of the midpoint algorithm is that we draw the thinnest line possible  that has no gaps. A diagonal connection between two pixels is not considered a gap.
对于 m ∈ (0, 1] 的情况，“运行”多于“上升”，即，线在 x 方向上移动比在 y 方向上移动得更快。如果我们有一个 y 轴指向下方的 API，我们可能会 担心这是否会使过程变得更加困难，但事实上，我们可以忽略这个细节。我们可以忽略“向上”和“向下”的几何概念，因为这两种情况的代数完全相同。 读者可以确认所得算法适用于 y 轴向下的情况。中点算法的关键假设是我们绘制尽可能没有间隙的最细线。两个像素之间的对角线连接不被视为间隙。

As the line progresses from the left endpoint to the right, there are only two possibilities: draw a pixel at the same height as the pixel drawn to its left, or draw a pixel one higher. There will always be exactly one pixel in each column of pixels between the endpoints. Zero would imply a gap, and two would be too thick a line. There may be two pixels in the same row for the case we are considering; the line is more horizontal than vertical so sometimes it will go right, and sometimes up. This concept is shown in Figure 8.2, where three “reasonable” lines are shown, each advancing more in the horizontal direction than in the vertical direction.
当线从左端点向右延伸时，只有两种可能性：在与左侧绘制的像素相同的高度上绘制一个像素，或者在更高的高度绘制一个像素。 端点之间的每一列像素中始终只有一个像素。 零意味着有一个间隙，而两个则意味着线条太粗。 对于我们正在考虑的情况，同一行中可能有两个像素； 该线的水平方向多于垂直方向，因此有时会向右移动，有时会向上移动。 这个概念如图 8.2 所示，其中显示了 3 条“合理”线，每条线在水平方向上比在垂直方向上前进得更多。
![Figure 8.2](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.2.png)
Figure 8.2. Three “reasonable” lines that go seven pixels horizontally and three pixels vertically. 
图 8.2. 三个“合理”的线，水平方向有七个像素，垂直方向有三个像素。

The midpoint algorithm for $m ∈ (0, 1]$ first establishes the leftmost pixel and the column number (x-value) of the rightmost pixel and then loops horizontally establishing the row (y-value) of each pixel. The basic form of the algorithm is:
$m ∈ (0, 1]$ 的中点算法首先建立最左边的像素和最右边像素的列号（x 值），然后水平循环建立每个像素的行（y 值）。基本形式 算法的内容是：

> $y = y_0$
> for $x = x_0$ to $x_1$ do
> 	draw(x, y)
> 	if (some condition) then
> 		y = y + 1  

Note that x and y are integers. In words this says, “keep drawing pixels from left to right and sometimes move upward in the y-direction while doing so.” The key is to establish efficient ways to make the decision in the if statement.
请注意，x 和 y 是整数。 换句话说，“不断从左向右绘制像素，有时在 y 方向上向上移动”。 关键是建立有效的方法来在 if 语句中做出决定。

An effective way to make the choice is to look at the midpoint of the line between the two potential pixel centers. More specifically, the pixel just drawn is pixel (x, y) whose center in real screen coordinates is at (x, y). The candidate pixels to be drawn to the right are pixels (x + 1, y) and (x + 1, y + 1). The midpoint between the centers of the two candidate pixels is (x + 1, y + 0.5). If the line passes below this midpoint we draw the bottom pixel, and otherwise we draw the top pixel (Figure 8.3).  
做出选择的有效方法是查看两个潜在像素中心之间的线的中点。 更具体地说，刚刚绘制的像素是实际屏幕坐标中的中心位于（x，y）的像素（x，y）。 向右绘制的候选像素是像素(x+1，y)和(x+1，y+1)。 两个候选像素中心之间的中点是(x + 1, y + 0.5)。 如果该线穿过该中点下方，我们将绘制底部像素，否则我们将绘制顶部像素（图 8.3）。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.3.png" alt="Figure 8.3" style="zoom:50%;" />
Figure 8.3. Top: the line goes above the midpoint so the top pixel is drawn. Bottom: the line goes below the midpoint so the bottom pixel is drawn. 
图 8.3. 顶部：线位于中点上方，因此绘制顶部像素。 底部：线位于中点下方，因此绘制底部像素。 

To decide whether the line passes above or below $(x+1, y +0.5)$, we evaluate $f(x, y + 0.5)$ in Equation (8.1). Recall from Section 2.5.1 that $f(x, y) = 0$ for points $(x, y)$ on the line, $f(x, y) > 0$ for points on one side of the line, and $f(x, y) < 0$ for points on the other side of the line. Because $-f(x, y) = 0$ and $f(x, y) = 0$ are both perfectly good equations for the line, it is not immediately clear whether $f(x, y)$ being positive indicates that $(x, y)$ is above the line, or whether it is below. However, we can figure it out; the key term in Equation (8.1) is the $y$ term $(x_1 - x_0)y$. Note that $(x_1 - x_0)$ is definitely positive because $x_1 > x_0$. This means that as $y$ increases, the term $(x_1-x_0)y$ gets larger (i.e., more positive or less negative). Thus, the case $f(x, +∞)$ is definitely positive, and definitely above the line, implying points above the line are all positive. Another way to look at it is that the $y$ component of the gradient vector is positive. So above the line, where $y$ can increase arbitrarily, $f(x, y)$ must be positive. Thism eans we can make our code more specific by filling in the if statement:
为了确定直线是否高于或低于 $(x+1, y +0.5)$，我们评估方程 (8.1) 中的 $f(x, y + 0.5)$。 回想一下第 2.5.1 节，对于直线上的点 $(x, y)$，$f(x, y) = 0$，对于直线一侧的点，$f(x, y) > 0$，并且 $f(x, y) < 0$ 对于线另一侧的点。 由于 $-f(x, y) = 0$ 和 $f(x, y) = 0$ 都是该直线的完美方程，因此尚不清楚 $f(x, y)$ 为正是否表明 $(x, y)$ 在线上方，或者在线下方。 然而，我们可以弄清楚； 方程 (8.1) 中的关键项是 $y$ 项 $(x_1 - x_0)y$。 请注意，$(x_1 - x_0)$ 肯定是正数，因为 $x_1 > x_0$。 这意味着随着 $y$ 的增加，$(x_1-x_0)y$ 项变得更大（即，更多的正值或更少的负值）。 因此，$f(x, +∞)$ 的情况肯定是正的，并且肯定在线上方，这意味着线上方的点都是正的。 另一种看待它的方式是梯度向量的 $y$ 分量为正。 因此，在线上方，$y$ 可以任意增加，$f(x, y)$ 必须为正数。 这意味着我们可以通过填写 if 语句来使我们的代码更加具体：

> if $f(x + 1, y + 0.5) < 0$ then
> 	$y = y + 1$

The above code will work nicely for lines of the appropriate slope (i.e., between zero and one). The reader can work out the other three cases which differ only in small details. 
上面的代码对于具有适当斜率（即介于 0 和 1 之间）的线可以很好地工作。 读者可以找出其他三种仅在小细节上有所不同的情况。

If greater efficiency is desired, using an incremental method can help. An incremental method tries to make a loop more efficient by reusing computation from the previous step. In the midpoint algorithm as presented, the main computation is the evaluation of $f(x + 1, y + 0.5)$. Note that inside the loop, after the first iteration, either we already evaluated $f(x - 1, y + 0.5)$ or $f(x - 1, y - 0.5)$ (Figure 8.4). Note also this relationship:
如果需要更高的效率，使用增量方法会有所帮助。 增量方法尝试通过重用上一步的计算来提高循环效率。 在所提出的中点算法中，主要计算是$f(x + 1, y + 0.5)$的评估。 请注意，在循环内部，第一次迭代之后，我们要么已经计算了 $f(x - 1, y + 0.5)$ 或 $f(x - 1, y - 0.5)$（图 8.4）。 还要注意这种关系：
$f(x + 1, y) = f(x, y) + (y_0 - y_1)\\
f(x + 1, y + 1) = f(x, y) + (y_0 - y_1) + (x_1 - x_0).  $

<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.4.png" alt="Figure 8.4" style="zoom:67%;" />
Figure 8.4. When using the decision point shown between the two orange pixels, we just drew the blue pixel, so we evaluated f at one of the two left points shown. 
图 8.4. 当使用两个橙色像素之间显示的决策点时，我们只绘制了蓝色像素，因此我们在显示的两个左侧点之一评估 f。

This allows us to write an incremental version of the code: 
这允许我们编写代码的增量版本：

> $y = y_0$
> $d = f(x_0 + 1, y_0 + 0.5)$
> for $x = x_0$ to $x_1$ do
> 	draw(x, y)
> 	if d < 0 then
> 		y = y + 1
> 		$d = d + (x_1 - x_0) + (y_0 - y_1)$
> 	else
> 		$d = d + (y_0 - y_1)$

This code should run faster since it has little extra setup cost compared to the non-incremental version (that is not always true for incremental algorithms), but it may accumulate more numeric error because the evaluation of $f(x, y + 0.5)$ may be composed of many adds for long lines. However, given that lines are rarely longer than a few thousand pixels, such an error is unlikely to be critical. Slightly longer setup cost, but faster loop execution, can be achieved by storing $(x_1 - x_0) + (y_0 - y_1)$ and $(y_0 - y_1)$ as variables. We might hope a good compiler would do that for us, but if the code is critical, it would be wise to examine the results of compilation to make sure.
该代码应该运行得更快，因为与非增量版本相比，它几乎没有额外的设置成本（增量算法并不总是如此），但它可能会积累更多的数字错误，因为 $f(x, y + 0.5)$的评估可能由许多添加组成，以表示长行。 然而，考虑到线条很少超过几千像素，这样的错误不太可能是严重的。 通过将 $(x_1 - x_0) + (y_0 - y_1)$ 和 $(y_0 - y_1)$ 存储为变量，可以实现稍长的设置成本，但更快的循环执行。 我们可能希望一个好的编译器能为我们做到这一点，但如果代码很关键，那么明智的做法是检查编译结果以确保这一点。

### 8.1.2 Triangle Rasterization 三角形光栅化

We often want to draw a 2D triangle with 2D points $\bold{p}_0 = (x_0, y_0)$, $\bold{p}_1 = (x_1, y_1)$, and $\bold{p}_2 = (x_2, y_2)$ in screen coordinates. This is similar to the line drawing problem, but it has some of its own subtleties. As with line drawing, we may wish to interpolate color or other properties from values at the vertices. This is straightforward if we have the barycentric coordinates (Section 2.7). For example, if the vertices have colors $\bold{c}_0$, $\bold{c}_1$, and $\bold{c}_2$, the color at a point in the triangle with barycentric coordinates $(α, β, γ)$ is
我们经常想画一个2D三角形，在屏幕坐标中有两个点$\bold{p}_0 = (x_0, y_0)$， $\bold{p}_1 = (x_1, y_1)$和$\bold{p}_2 = (x_2, y_2)$。这类似于线条绘制问题，但它有一些自己的微妙之处。与线条绘制一样，我们可能希望从顶点处的值插入颜色或其他属性。如果我们有以质量为中心的坐标(第2.7节)，这是很简单的。例如，如果顶点的颜色为$\bold{c}_0$， $\bold{c}_1$和$\bold{c}_2$，则三角形中具有质心坐标$(α， β， γ)$的点的颜色为
$\bold{c} = α\bold{c}_0 + β\bold{c}_1 + γ\bold{c}_2  $

This type of interpolation of color is known in graphics as Gouraud interpolation after its inventor (Gouraud, 1971). 
这种类型的颜色插值在图形学中被称为 Gouraud 插值，以其发明者命名（Gouraud，1971）。

Another subtlety of rasterizing triangles is that we are usually rasterizing triangles that share vertices and edges. This means we would like to rasterize adjacent triangles so there are no holes. We could do this by using the midpoint algorithm to draw the outline of each triangle and then fill in the interior pixels. This would mean adjacent triangles both draw the same pixels along each edge. If the adjacent triangles have different colors, the image will depend on the order in which the two triangles are drawn. The most common way to rasterize triangles that avoids the order problem and eliminates holes is to use the convention that pixels are drawn if and only if their centers are inside the triangle, i.e., the barycentric coordinates of the pixel center are all in the interval (0, 1). This raises the issue of what to do if the center is exactly on the edge of the triangle. There are several ways to handle this as will be discussed later in this section. The key observation is that barycentric coordinates allow us to decide whether to draw a pixel and what color that pixel should be if we are interpolating colors from the vertices. So our problem of rasterizing the triangle boils down to efficiently finding the barycentric coordinates of pixel centers (Pineda, 1988). The brute-force rasterization algorithm is:
栅格化三角形的另一个微妙之处是我们通常栅格化共享顶点和边的三角形。 这意味着我们想要栅格化相邻的三角形，这样就不会有洞。 我们可以通过使用中点算法绘制每个三角形的轮廓，然后填充内部像素来做到这一点。 这意味着相邻的三角形都沿着每条边绘制相同的像素。 如果相邻三角形具有不同的颜色，则图像将取决于两个三角形的绘制顺序。 栅格化三角形以避免顺序问题并消除空洞的最常见方法是使用以下约定：当且仅当像素中心位于三角形内部时，即像素中心的重心坐标都在区间 ( 0, 1)。 这就提出了一个问题：如果中心恰好位于三角形的边缘上该怎么办。 有多种方法可以处理此问题，本节稍后将对此进行讨论。 关键的观察是，重心坐标允许我们决定是否绘制像素，以及如果我们从顶点插值颜色，该像素应该是什么颜色。 因此，我们对三角形进行光栅化的问题归结为有效地找到像素中心的重心坐标（Pineda，1988）。 暴力光栅化算法是：

> for all x do
> 	for all y do
> 		compute $(α, β, γ)$ for $(x, y)$
> 		if $(α ∈ [0, 1] and β ∈ [0, 1] and γ ∈ [0, 1])$ then
> 			$\bold{c} = α\bold{c}_0 + β\bold{c}_1 + γ\bold{c}_2$
> 			drawpixel (x, y) with color $\bold{c}$

The rest of the algorithm limits the outer loops to a smaller set of candidate pixels and makes the barycentric computation efficient.
该算法的其余部分将外部循环限制为较小的候选像素集，并使重心计算变得高效。

We can add a simple efficiency by finding the bounding rectangle of the three vertices and only looping over this rectangle for candidate pixels to draw. We can compute barycentric coordinates using Equation (2.32). This yields the algorithm:
我们可以通过找到三个顶点的边界矩形并仅循环该矩形来绘制候选像素来增加简单的效率。 我们可以使用方程（2.32）计算重心坐标。 这产生了算法：

> $x_{min}$ = floor($x_i$)
> $x_{max}$ = ceiling($x_i$)
> $y_{min}$ = floor($y_i$)
> $y_{max}$ = ceiling($y_i$)
> for $y = y_{min}$ to $y_{max}$ do
> 	for $x = x_{min}$ to $x_{max}$ do
> 		$α = f_{12}(x, y)/f_{12}(x_0, y_0)$
> 		$β = f_{20}(x, y)/f_{20}(x_1, y_1)$
> 		$γ = f_{01}(x, y)/f_{01}(x_2, y_2)$
> 		if ($α > 0$ and $β > 0$ and $γ > 0$) then
> 			$\bold{c} = α\bold{c}_0 + β\bold{c}_1 + γ\bold{c}_2$
> 			drawpixel (x, y) with color $\bold{c}$

Here $f_{ij}$ is the line given by Equation (8.1) with the appropriate vertices:
这里$f_{ij}$是由式(8.1)给出的具有相应顶点的直线:
$$
f_{01}(x, y) = (y_0 − y_1)x + (x_1 − x_0)y + x_0y_1 − x_1y_0, \\
f_{12}(x, y) = (y_1 − y_2)x + (x_2 − x_1)y + x_1y_2 − x_2y_1, \\
f_{20}(x, y) = (y_2 − y_0)x + (x_0 − x_2)y + x_2y_0 − x_0y_2.
$$
Note that we have exchanged the test $α ∈ (0, 1)$ with $α > 0$ etc., because if all of $α, β, γ$ are positive, then we know they are all less than one because $α + β + γ = 1$. We could also compute only two of the three barycentric variables and get the third from that relation, but it is not clear that this saves computation once the algorithm is made incremental, which is possible as in the line drawing algorithms; each of the computations of $α$, $β$, and $γ$ does an evaluation of the form $f(x, y) = Ax + By + C$. In the inner loop, only $x$ changes, and it changes by one. Note that $f(x + 1, y) = f(x, y) + A$. This is the basis of the incremental algorithm. In the outer loop, the evaluation changes for $f(x, y)$ to $f(x, y + 1)$, so a similar efficiency can be achieved. Because $α$, $β$, and $γ$ change by constant increments in the loop, so does the color $\bold{c}$. So this can be made incremental as well. For example, the red value for pixel $(x + 1, y)$ differs from the red value for pixel $(x, y)$ by a constant amount that can be precomputed. An example of a triangle with color interpolation is shown in Figure 8.5.
请注意，我们已经将测试 $α ∈ (0, 1)$ 与 $α > 0$ 等交换，因为如果所有 $α, β, γ$ 都是正数，那么我们知道它们都小于 1，因为 $ α + β + γ = 1$。 我们也可以只计算三个重心变量中的两个，并从该关系中得到第三个，但尚不清楚一旦算法增量，这是否可以节省计算量，这在画线算法中是可能的； $α$、$β$ 和 $γ$ 的每个计算都会进行 $f(x, y) = Ax + By + C$ 形式的评估。 在内层循环中，只有$x$改变，并且改变了1。 请注意 $f(x + 1, y) = f(x, y) + A$。 这是增量算法的基础。 在外循环中，$f(x, y)$ 的评估更改为$f(x, y + 1)$，因此可以实现类似的效率。 由于 $α$、$β$ 和 $γ$ 在循环中按恒定增量变化，因此颜色 $\bold{c}$ 也会变化。 所以这也可以是增量的。 例如，像素 $(x + 1, y)$ 的红色值与像素 $(x, y)$ 的红色值相差可预先计算的恒定量。 图 8.5 显示了带有颜色插值的三角形示例。
![Figure 8.5](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.5.png)
Figure 8.5. A colored triangle with barycentric interpolation. Note that the changes in color components are linear in each row and column as well as along each edge. In fact it is constant along every line, such as the diagonals, as well. 
图 8.5. 具有重心插值的彩色三角形。 请注意，颜色分量的变化在每行和每列以及沿每条边缘都是线性的。 事实上，它沿着每条线（例如对角线)都是恒定的。

#### Dealing with Pixels on Triangle Edges 处理三角形边缘上的像素

We have still not discussed what to do for pixels whose centers are exactly on the edge of a triangle. If a pixel is exactly on the edge of a triangle, then it is also on the edge of the adjacent triangle if there is one. There is no obvious way to award the pixel to one triangle or the other. The worst decision would be to not draw the pixel because a hole would result between the two triangles. Better, but still not good, would be to have both triangles draw the pixel. If the triangles are transparent, this will result in a double-coloring. We would really like to award the pixel to exactly one of the triangles, and we would like this process to be simple; which triangle is chosen does not matter as long as the choice is well defined.
我们还没有讨论如何处理中心正好位于三角形边缘的像素。 如果一个像素正好位于三角形的边缘上，那么它也位于相邻三角形的边缘上（如果有的话）。 没有明显的方法将像素分配给一个三角形或另一个三角形。 最糟糕的决定是不绘制像素，因为两个三角形之间会产生一个洞。 更好但仍然不好的是让两个三角形都绘制像素。 如果三角形是透明的，这将导致双色。 我们真的很想将像素奖励给其中一个三角形，并且我们希望这个过程很简单； 只要选择明确，选择哪个三角形并不重要。

One approach is to note that any off-screen point is definitely on exactly one side of the shared edge and that is the edge we will draw. For two non-overlapping triangles, the vertices not on the edge are on opposite sides of the edge from each other. Exactly one of these vertices will be on the same side of the edge as the off-screen point (Figure 8.6). This is the basis of the test. The test if numbers $p$ and $q$ have the same sign can be implemented as the test $pq > 0$, which is very efficient in most environments.
一种方法是注意任何屏幕外点绝对位于共享边缘的一侧，这就是我们将绘制的边缘。 对于两个不重叠的三角形，不在边上的顶点位于边的相对两侧。 这些顶点中的一个恰好与屏幕外点位于边缘的同一侧（图 8.6）。 这是测试的基础。 数字 $p$ 和 $q$ 是否具有相同符号的测试可以实现为测试 $pq > 0$，这在大多数环境中非常有效。
![Figure 8.6](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.6.png)
Figure 8.6. The off-screen point will be on one side of the triangle edge or the other. Exactly one of the non-shared vertices $\bold{a}$ and $\bold{b}$ will be on the same side. 
图 8.6. 屏幕外点将位于三角形边缘的一侧或另一侧。 非共享顶点 $\bold{a}$ 和 $\bold{b}$ 中的一个恰好位于同一侧。

Note that the test is not perfect because the line through the edge may also go through the off-screen point, but we have at least greatly reduced the number of problematic cases. Which off-screen point is used is arbitrary, and $(x, y) = (−1, −1)$ is as good a choice as any. We will need to add a check for the case of a point exactly on an edge. We would like this check not to be reached for common cases, which are the completely inside or outside tests. This suggests:
请注意，测试并不完美，因为穿过边缘的线也可能穿过屏幕外的点，但我们至少大大减少了有问题的情况。 使用哪个屏幕外点是任意的，$(x, y) = (−1, −1)$ 是一个不错的选择。 我们需要添加一个检查，检查点是否恰好位于边缘上。 我们希望在常见情况下不要进行此检查，这些情况是完全内部或外部测试。 这表明：

> $x_{min} = floor(x_i)$
> $x_{max} = ceiling(x_i)$
> $y_{min} = floor(y_i) $
> $y_{max} = ceiling(y_i)$
> $f_α = f_{12}(x_0, y_0)$
> $f_β = f_{20}(x_1, y_1)$
> $f_γ = f_{01}(x_2, y_2)$
> for $y = y_{min}$ to $y_{max}$ do
> 	for $x = x_{min}$ to $x_{max}$ do
> 		$α = f_{12}(x, y)/f_α$
> 		$β = f_{20}(x, y)/f_β$
> 		$γ = f_{01}(x, y)/f_γ$
> 		if ($α ≥ 0$ and $β ≥ 0$ and $γ ≥ 0$) then
> 			if ($α > 0$ or $f_αf_{12}(-1, -1) > 0)$ and
> 				($β > 0$ or $f_βf_{20}(-1, -1) > 0$) and
> 				($γ > 0$ or $f_γf_{01}(-1, -1) > 0$) then
> 				$\bold{c} = α\bold{c}_0 + β\bold{c}_1 + γ\bold{c}_2$
> 				drawpixel $(x, y)$ with color $\bold{c}$  

We might expect that the above code would work to eliminate holes and doubledraws only if we use exactly the same line equation for both triangles. In fact, the line equation is the same only if the two shared vertices have the same order in the draw call for each triangle. Otherwise the equation might flip in sign. This could be a problem depending on whether the compiler changes the order of operations. So if a robust implementation is needed, the details of the compiler and arithmetic unit may need to be examined. The first four lines in the pseudocode above must be coded carefully to handle cases where the edge exactly hits the pixel center. 
我们可能期望，只有当我们对两个三角形使用完全相同的直线方程时，上述代码才能消除孔和双重绘制。 事实上，仅当两个共享顶点在每个三角形的绘制调用中具有相同的顺序时，线方程才是相同的。 否则方程的符号可能会翻转。 这可能会成为一个问题，具体取决于编译器是否更改操作顺序。 因此，如果需要健壮的实现，则可能需要检查编译器和算术单元的细节。 上面伪代码中的前四行必须仔细编码，以处理边缘恰好击中像素中心的情况。

In addition to being amenable to an incremental implementation, there are several potential early exit points. For example, if $α$ is negative, there is no need to compute $β$ or $γ$. While this may well result in a speed improvement, profiling is always a good idea; the extra branches could reduce pipelining or concurrency and might slow down the code. So as always, test any attractive-looking optimizations if the code is a critical section. 
除了适合增量实施之外，还有几个潜在的早期退出点。 例如，如果$α$为负，则无需计算$β$或$γ$。 虽然这很可能会提高速度，但分析始终是一个好主意。 额外的分支可能会减少管道或并发性，并可能减慢代码速度。 因此，与往常一样，如果代码是关键部分，请测试任何看起来有吸引力的优化。

Another detail of the above code is that the divisions could be divisions by zero for degenerate triangles, i.e., if $f_γ = 0$. Either the floating point error conditions should be accounted for properly, or another test will be needed.
上述代码的另一个细节是，对于简并三角形，除法可以被零除，即，如果 $f_γ = 0$。 要么应正确考虑浮点错误条件，要么需要进行另一次测试。

### 8.1.3 Clipping 剪辑

Simply transforming primitives into screen space and rasterizing them does not quite work by itself. This is because primitives that are outside the view volume— particularly, primitives that are behind the eye—can end up being rasterized, leading to incorrect results. For instance, consider the triangle shown in Figure 8.7.
简单地将图元转换为屏幕空间并对它们进行光栅化本身并不能完全起作用。 这是因为视图体积之外的图元（特别是眼睛后面的图元）最终可能会被光栅化，从而导致不正确的结果。 例如，考虑图 8.7 中所示的三角形。
![Figure 8.7](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.7.png)
Figure 8.7. The depth $z$ is transformed to the depth $z'$ by the perspective transform. Note that when $z$ moves from positive to negative, $z'$ switches from negative to positive. Thus vertices behind the eye are moved in front of the eye beyond $z' = n + f$. This will lead to wrong results, which is why the triangle is first clipped to ensure all vertices are in front of the eye.
图 8.7. 深度$z$通过透视变换变换为深度$z'$。 请注意，当 $z$ 从正值变为负值时，$z'$ 从负值变为正值。 因此，眼睛后面的顶点会移动到眼睛前面，超出 $z' = n + f$。 这将导致错误的结果，这就是为什么首先对三角形进行裁剪以确保所有顶点都在眼睛前面的原因。

Two vertices are in the view volume, but the third is behind the eye. The projection transformation maps this vertex to a nonsensical location behind the far plane, and if this is allowed to happen the triangle will be rasterized incorrectly. For this reason, rasterization has to be preceded by a clipping operation that removes parts of primitives that could extend behind the eye.
两个顶点在视图体中，但第三个在眼睛后面。投影变换将这个顶点映射到远平面后面的一个无意义的位置，如果允许这种情况发生，三角形将被错误地栅格化。由于这个原因，光栅化之前必须进行裁剪操作，该操作删除可能延伸到眼睛后面的原语部分。

Clipping is a common operation in graphics, needed whenever one geometric entity “cuts” another. For example, if you clip a triangle against the plane x = 0, the plane cuts the triangle into two parts if the signs of the x-coordinates of the vertices are not all the same. In most applications of clipping, the portion of the triangle on the “wrong” side of the plane is discarded. This operation for a single plane is shown in Figure 8.8.
剪切是图形中的一种常见操作，每当一个几何实体“剪切”另一个几何实体时就需要剪切。 例如，如果您相对于平面 x = 0 裁剪三角形，并且顶点的 x 坐标的符号不相同，则平面会将三角形切割成两部分。 在大多数裁剪应用中，平面“错误”一侧的三角形部分会被丢弃。 单平面的操作如图 8.8 所示。
![Figure 8.8](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.8.png)

Figure 8.8. A polygon is clipped against a clipping plane. The portion “inside” the plane is retained.
图 8.8. 多边形相对于剪裁平面进行剪裁。 保留平面“内部”的部分。

In clipping to prepare for rasterization, the “wrong” side is the side outside the view volume. It is always safe to clip away all geometry outside the view volume—that is, clipping against all six faces of the volume—but many systems manage to get away with only clipping against the near plane. 
在为光栅化做准备的剪裁中，“错误”的一侧是视图体积之外的一侧。 剪掉视图体积之外的所有几何体始终是安全的，即剪裁体积的所有六个面，但许多系统设法仅剪裁近平面。

This section discusses the basic implementation of a clipping module. Those interested in implementing an industrial-speed clipper should see the book by Blinn mentioned in the notes at the end of this chapter. 
本节讨论裁剪模块的基本实现。 那些对实现工业速度剪裁机感兴趣的人应该看看本章末尾的注释中提到的 Blinn 的书。

The two most common approaches for implementing clipping are
实现裁剪的两种最常见的方法是

1. in world coordinates using the six planes that bound the truncated viewing pyramid, 
   在世界坐标中，使用限制截断观察金字塔的六个平面，
2. in the 4D transformed space before the homogeneous divide.
   在齐次划分之前的4D变换空间中。

Either possibility can be effectively implemented (J. Blinn, 1996) using the following approach for each triangle:
对于每个三角形，使用以下方法都可以有效地实现任何一种可能性（J. Blinn，1996）：

> for each of six planes do
> 	if (triangle entirely outside of plane) then
> 		break (triangle is not visible)
> 	else if triangle spans plane then
> 		clip triangle
> 		if (quadrilateral is left) then
> 			break into two triangles

### 8.1.4 Clipping Before the Transform (Option 1)  变换前裁剪（选项 1）

Option 1 has a straightforward implementation. The only question is, “What are the six plane equations?” Because these equations are the same for all triangles rendered in the single image, we do not need to compute them very efficiently. For this reason, we can just invert the transform shown in Figure 5.11 and apply it to the eight vertices of the transformed view volume:
选项 1 的实现很简单。 唯一的问题是，“六个平面方程是什么？” 因为这些方程对于单个图像中渲染的所有三角形都是相同的，所以我们不需要非常有效地计算它们。 因此，我们可以反转图 5.11 所示的变换并将其应用到变换后的视图体积的八个顶点：
$$
(x, y, z) =(l, b, n) \\
(r, b, n) \\
(l, t, n) \\
(r, t, n) \\
(l, b, f) \\
(r, b, f) \\
(l, t, f) \\
(r, t, f).
$$
The plane equations can be inferred from here. Alternatively, we can use vector geometry to get the planes directly from the viewing parameters.
平面方程可以从这里推断出来。或者，我们可以使用矢量几何直接从查看参数中获取平面。

### 8.1.5 Clipping in Homogeneous Coordinates (Option 2) 在齐次坐标中裁剪（选项 2）

Surprisingly, the option usually implemented is that of clipping in homogeneous coordinates before the divide. Here the view volume is 4D, and it is bounded by 3D volumes (hyperplanes). These are
令人惊讶的是，通常实现的选项是在划分之前在齐次坐标中进行裁剪。 这里的视图体积是 4D 的，并且它受到 3D 体积（超平面）的限制。 这些都是
$$
−x + lw = 0, \\
x − rw = 0, \\
−y + bw = 0, \\
y − tw = 0, \\
−z + nw = 0, \\
z − fw = 0.
$$
These planes are quite simple, so the efficiency is better than for Option 1. They still can be improved by transforming the view volume $[l, r] × [b, t] × [f, n]$ to $[0, 1]^3$. It turns out that the clipping of the triangles is not much more complicated than in 3D.
这些平面非常简单，所以效率比选项1要好。它们仍然可以通过将视图体积$[1,r] × [b, t] × [f, n]$转换为$[0,1]^3$来改进。事实证明，三角形的裁剪并不比在3D中复杂多少。

### 8.1.6 Clipping against a Plane 对平面进行裁剪

No matter which option we choose, we must clip against a plane. Recall from Section 2.5.5 that the implicit equation for a plane through point $\bold{q}$ with normal $\bold{n}$ is
无论我们选择哪一个选项，我们都必须夹在一个平面上。回想2.5.5节，通过点$\bold{q}$的平面与法线$\bold{n}$的隐式方程为
$f(\bold{p}) = \bold{n} · (\bold{p} - \bold{q}) = 0.  $

This is often written
经常这样写
$f(\bold{p}) = \bold{n} · \bold{p} + D = 0. (8.2)  $

Interestingly, this equation not only describes a 3D plane, but it also describes a line in 2D and the volume analog of a plane in 4D. All of these entities are usually called planes in their appropriate dimension.
有趣的是，这个方程不仅描述了 3D 平面，还描述了 2D 中的直线和 4D 中平面的体积模拟。 所有这些实体通常在其适当的尺寸下被称为平面。

If we have a line segment between points $\bold{a}$ and $\bold{b}$, we can “clip” it against a plane using the techniques for cutting the edges of 3D triangles in BSP tree programs described in Section 12.4.3. Here, the points a and b are tested to determine whether they are on opposite sides of the plane $f(\bold{p}) = 0$ by checking whether $f(\bold{a})$ and $f(\bold{b})$ have different signs. Typically $f(\bold{p}) < 0$ is defined to be “inside” the plane, and $f(\bold{p}) > 0$ is “outside” the plane. If the plane does split the line, then we can solve for the intersection point by substituting the equation for the parametric line,
如果我们在点 $\bold{a}$ 和 $\bold{b}$ 之间有一条线段，我们可以使用第 2 节中描述的 BSP 树程序中切割 3D 三角形边缘的技术将其“剪辑”到平面上 12.4.3。 这里，通过检查 $f(\bold{a})$ 和 $f(\ 粗体{b})$有不同的符号。 通常，$f(\bold{p}) < 0$ 被定义为平面“内部”，$f(\bold{p}) > 0$ 被定义为平面“外部”。 如果平面确实分割了线，那么我们可以通过将方程代入参数线来求解交点，
$\bold{p} = \bold{a} + t(\bold{b} - \bold{a}),  $

into the $f(\bold{p}) = 0$ plane of Equation (8.2). This yields
进入方程（8.2）的 $f(\bold{p}) = 0$ 平面。 这产生
$\bold{n} · (\bold{a} + t(\bold{b} - \bold{a})) + D = 0.  $

Solving for t gives
求解t得到
$$
t = \frac{\bold{n}· \bold{a} + D }{\bold{n}· (\bold{a} − \bold{b})}
$$
We can then find the intersection point and “shorten” the line.
然后我们可以找到交点并“缩短”这条线。

To clip a triangle, we again can follow Section 12.4.3 to produce one or two triangles. 
要裁剪一个三角形，我们同样可以按照第12.4.3节来生成一个或两个三角形。

## 8.2 Operations Before and After Rasterization 光栅化前后的操作

Before a primitive can be rasterized, the vertices that define it must be in screen coordinates, and the colors or other attributes that are supposed to be interpolated across the primitive must be known. Preparing this data is the job of the vertex-processing stage of the pipeline. In this stage, incoming vertices are transformed by the modeling, viewing, and projection transformations, mapping them from their original coordinates into screen space (where, recall, position is measured in terms of pixels). At the same time, other information, such as colors, surface normals, or texture coordinates, is transformed as needed; we’ll discuss these additional attributes in the examples below. 
在对图元进行光栅化之前，定义它的顶点必须位于屏幕坐标中，并且必须知道应该在图元上插值的颜色或其他属性。 准备这些数据是管道的顶点处理阶段的工作。 在此阶段，传入的顶点通过建模、查看和投影变换进行变换，将它们从原始坐标映射到屏幕空间（其中，位置以像素为单位进行测量）。 同时，其他信息，例如颜色、表面法线或纹理坐标，也会根据需要进行转换； 我们将在下面的示例中讨论这些附加属性。

After rasterization, further processing is done to compute a color and depth for each fragment. This processing can be as simple as just passing through an interpolated color and using the depth computed by the rasterizer; or it can involve complex shading operations. Finally, the blending phase combines the fragments generated by the (possibly several) primitives that overlapped each pixel to compute the final color. The most common blending approach is to choose the color of the fragment with the smallest depth (closest to the eye). 
光栅化后，进行进一步处理以计算每个片段的颜色和深度。 这种处理可以非常简单，只需通过插值颜色并使用光栅化器计算的深度即可； 或者它可能涉及复杂的着色操作。 最后，混合阶段组合由重叠每个像素的（可能是多个）图元生成的片段来计算最终颜色。 最常见的混合方法是选择深度最小（最接近眼睛）的片段的颜色。

The purposes of the different stages are best illustrated by examples.
不同阶段的目的可以通过示例得到最好的说明。

### 8.2.1 Simple 2D Drawing 简单的 2D 绘图

The simplest possible pipeline does nothing in the vertex or fragment stages, and in the blending stage the color of each fragment simply overwrites the value of the previous one. The application supplies primitives directly in pixel coordinates, and the rasterizer does all the work. This basic arrangement is the essence of many simple, older APIs for drawing user interfaces, plots, graphs, and other 2D content. Solid color shapes can be drawn by specifying the same color for all vertices of each primitive, and our model pipeline also supports smoothly varying color using interpolation. 
最简单的管道在顶点或片段阶段不执行任何操作，并且在混合阶段，每个片段的颜色只是覆盖前一个片段的值。 应用程序直接以像素坐标提供图元，光栅化器完成所有工作。 这种基本安排是许多简单、较旧的 API 的本质，用于绘制用户界面、绘图、图表和其他 2D 内容。 可以通过为每个图元的所有顶点指定相同的颜色来绘制纯色形状，并且我们的模型管道还支持使用插值平滑地改变颜色。

### 8.2.2 A Minimal 3D Pipeline

To draw objects in 3D, the only change needed to the 2D drawing pipeline is a single matrix transformation: the vertex-processing stage multiplies the incoming vertex positions by the product of the modeling, camera, projection, and viewport matrices, resulting in screen-space triangles that are then drawn in the same way as if they’d been specified directly in 2D. 
要以 3D 方式绘制对象，2D 绘图管道所需的唯一更改是单个矩阵转换：顶点处理阶段将传入的顶点位置乘以建模、相机、投影和视口矩阵的乘积，从而得到屏幕矩阵 然后以与直接在 2D 中指定的方式相同的方式绘制空间三角形。

One problem with the minimal 3D pipeline is that in order to get occlusion relationships correct—to get nearer objects in front of farther away objects— primitives must be drawn in back-to-front order. This is known as the painter’s algorithm for hidden surface removal, by analogy to painting the background of a painting first, then painting the foreground over it. The painter’s algorithm is a perfectly valid way to remove hidden surfaces, but it has several drawbacks. It cannot handle triangles that intersect one another, because there is no correct order in which to draw them. Similarly, several triangles, even if they don’t intersect, can still be arranged in an occlusion cycle, as shown in Figure 8.9, another case in which the back-to-front order does not exist. And most importantly, sorting the primitives by depth is slow, especially for large scenes, and disturbs the efficient flow of data that makes object-order rendering so fast. Figure 8.10 shows the result of this process when the objects are not sorted by depth.
最小3D管道的一个问题是，为了获得正确的遮挡关系——使较近的物体在较远的物体前面——原语必须按前后顺序绘制。这被称为去除隐藏表面的画家算法，类似于先绘制一幅画的背景，然后在其上绘制前景。画家的算法是去除隐藏表面的一种非常有效的方法，但它有几个缺点。它不能处理彼此相交的三角形，因为没有正确的顺序来绘制它们。同样，即使几个三角形不相交，也可以排列成一个遮挡循环，如图8.9所示，这是另一种不存在前后顺序的情况。最重要的是，按深度排序原语很慢，特别是对于大型场景，并且会干扰有效的数据流，从而使对象顺序渲染如此快速。图8.10显示了对象不按深度排序时的处理结果。

![Figure 8.9](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.9.png)
Figure 8.9. Two occlusion cycles, which cannot be drawn in back-to-front order. 
图 8.9. 两个遮挡循环，不能按从后到前的顺序绘制。

 ![Figure 8.10](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.10.png)
Figure 8.10. The result of drawing two spheres of identical size using the minimal pipeline. The sphere that appears smaller is farther away but is drawn last, so it incorrectly overwrites the nearer one.
图 8.10. 使用最小管道绘制两个相同尺寸的球体的结果。 看起来较小的球体距离较远，但最后绘制，因此它错误地覆盖了较近的球体。

### 8.2.3 Using a z-Buffer for Hidden Surfaces对隐藏表面使用 z 缓冲区

In practice, the painter’s algorithm is rarely used; instead a simple and effective hidden surface removal algorithm known as the z-buffer algorithm is used. The method is very simple: at each pixel we keep track of the distance to the closest surface that has been drawn so far, and we throw away fragments that are farther away than that distance. The closest distance is stored by allocating an extra value for each pixel, in addition to the red, green, and blue color values, which is known as the depth, or z-value. The depth buffer, or z-buffer, is the name for the grid of depth values.
在实际应用中，画家算法很少被使用； 相反，使用一种简单有效的隐藏表面去除算法，称为 z 缓冲区算法。 该方法非常简单：在每个像素处，我们跟踪迄今为止绘制的最近表面的距离，并丢弃比该距离更远的片段。 除了红色、绿色和蓝色值之外，还通过为每个像素分配一个额外值（称为深度或 z 值）来存储最近距离。 深度缓冲区或 z 缓冲区是深度值网格的名称。

The z-buffer algorithm is implemented in the fragment blending phase, by comparing the depth of each fragment with the current value stored in the z-buffer. If the fragment’s depth is closer, both its color and its depth value overwrite the values currently in the color and depth buffers. If the fragment’s depth is farther away, it is discarded. To ensure that the first fragment will pass the depth test, the z buffer is initialized to the maximum depth (the depth of the far plane). Irrespective of the order in which surfaces are drawn, the same fragment will win the depth test, and the image will be the same.
z 缓冲区算法是在片段混合阶段实现的，通过将每个片段的深度与 z 缓冲区中存储的当前值进行比较。 如果片段的深度更接近，则其颜色和深度值都会覆盖颜色和深度缓冲区中当前的值。 如果片段的深度较远，则将其丢弃。 为了确保第一个片段能够通过深度测试，z 缓冲区被初始化为最大深度（远平面的深度）。 无论表面绘制的顺序如何，相同的片段将赢得深度测试，并且图像将是相同的。

> Of course there can be ties in the depth test, in which case the order may well matter.
> 当然，深度测试中可能存在平局，在这种情况下，顺序可能很重要。

The z-buffer algorithm requires each fragment to carry a depth. This is done simply by interpolating the z-coordinate as a vertex attribute, in the same way that color or other attributes are interpolated. 
z-buffer算法要求每个片段携带一个深度。 只需将 z 坐标插值作为顶点属性即可完成此操作，与插值颜色或其他属性的方式相同。

The z-buffer is such a simple and practical way to deal with hidden surfaces in object-order rendering that it is by far the dominant approach. It is much simpler than geometric methods that cut surfaces into pieces that can be sorted by depth, because it avoids solving any problems that don’t need to be solved. The depth order only needs to be determined at the locations of the pixels, and that is all that the z-buffer does. It is universally supported by hardware graphics pipelines and is also the most commonly used method for software pipelines. Figure 8.11 shows an example result.
z 缓冲区是一种处理对象顺序渲染中隐藏表面的简单而实用的方法，因此它是迄今为止占主导地位的方法。 它比将曲面切割成可以按深度排序的块的几何方法要简单得多，因为它避免了解决任何不需要解决的问题。 只需要在像素位置确定深度顺序，这就是 z 缓冲区所做的全部工作。 它得到硬件图形管线的普遍支持，也是软件管线最常用的方法。 图 8.11 显示了示例结果。
![Figure 8.11](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.11.png)
Figure 8.11. The result of drawing the same two spheres using the z-buffer.
图 8.11.  使用 z 缓冲区绘制相同的两个球体的结果。

#### Precision Issues 精度问题

In practice, the z-values stored in the buffer are nonnegative integers. This is preferable to true floats because the fast memory needed for the z-buffer is somewhat expensive and is worth keeping to a minimum. 
实际上，存储在缓冲区中的 z 值是非负整数。 这比真正的浮点数更可取，因为 z 缓冲区所需的快速内存有点昂贵，并且值得保持在最低限度。

The use of integers can cause some precision problems. If we use an integer range having $B$ values ${0, 1, . . . , B - 1}$, we can map 0 to the near clipping plane $z = n$ and $B -1$ to the far clipping plane $z = f$. Note, that for this discussion, we assume $z$, $n$, and $f$ are positive. This will result in the same results as the negative case, but the details of the argument are easier to follow. We send each z-value to  a “bucket” with depth $Δz = (f - n)/B$. We would not use the integer z-buffer if memory were not a premium, so it is useful to make $B$ as small as possible.  
使用整数可能会导致一些精度问题。 如果我们使用具有 $B$ 值 ${0, 1, . . ., B - 1}$，我们可以将 0 映射到近裁剪平面 $z = n$，将 $B -1$ 映射到远裁剪平面 $z = f$。 请注意，对于本次讨论，我们假设 $z$、$n$ 和 $f$ 为正。 这将产生与反面情况相同的结果，但论证的细节更容易理解。 我们将每个 z 值发送到深度 $Δz = (f - n)/B$ 的“桶”。 如果内存不是溢价，我们不会使用整数 z 缓冲区，因此使 $B$ 尽可能小是有用的。

If we allocate b bits to store the z-value, then $B = 2^b$. We need enough bits to make sure any triangle in front of another triangle will have its depth mapped to distinct depth bins. 
如果我们分配 b 位来存储 z 值，则 $B = 2^b$。 我们需要足够的位来确保另一个三角形前面的任何三角形都将其深度映射到不同的深度箱。

For example, if you are rendering a scene where triangles have a separation of at least one meter, then $Δz < 1$ should yield images without artifacts. There are two ways to make $Δz$ smaller: move $n$ and $f$ closer together or increase $b$. If $b$ is fixed, as it may be in APIs or on particular hardware platforms, adjusting $n$ and $f$ is the only option. 
例如，如果您渲染的场景中三角形间隔至少一米，则 $Δz < 1$ 应生成没有伪影的图像。 有两种方法可以使 $Δz$ 变小：将 $n$ 和 $f$ 移近或增加 $b$。 如果 $b$ 是固定的，因为它可能在 API 或特定硬件平台上，则调整 $n$ 和 $f$ 是唯一的选择。

The precision of z-buffers must be handled with great care when perspective images are created. The value $Δz$ above is used after the perspective divide. Recall from Section 7.3 that the result of the perspective divide is
创建透视图像时必须非常小心地处理 z 缓冲区的精度。 上面的值 $Δz$ 在透视除法之后使用。 回想一下 7.3 节，透视除法的结果是
$z = n + f - \frac{fn}{z_w}\\$

The actual bin depth is related to $z_w$, the world depth, rather than $z$, the post-perspective divide depth. We can approximate the bin size by differentiating both sides:
实际的 bin 深度与 $z_w$（世界深度）相关，而不是与 $z$（后透视划分深度）相关。 我们可以通过区分两侧来估算 bin 大小：
$Δz ≈  \frac{fnΔz_w}{z^2_w}\\$

Bin sizes vary in depth. The bin size in world space is
垃圾箱的大小因深度而异。 世界空间中的 bin 大小为
$Δzw ≈  \frac{z_w^2 Δz}{fn}\\$

Note that the quantity $Δz$ is as previously discussed. The biggest bin will be for $z' = f$, where
注意，数量$Δz$与前面讨论的一样。最大的箱子将是$z' = f$，其中
$Δz^{max}_w ≈ \frac{fΔz}{n} $

Note that choosing $n = 0$, a natural choice if we don’t want to lose objects right in front of the eye, will result in an infinitely large bin—a very bad condition. To make $Δz_{max}^w$ as small as possible, we want to minimize $f$ and maximize $n$. Thus, it is always important to choose $n$ and $f$ carefully.
请注意，选择$n = 0$，如果我们不想失去眼前的物体，这是一个自然的选择，将导致一个无限大的箱子，这是一个非常糟糕的情况。为了使$Δz_{max}^w$尽可能小，我们希望最小化$f$和最大化$n$。因此，仔细选择$n$和$f$总是很重要的。
<img src="E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.12.png" alt="Figure 8.12" style="zoom:80%;" />
Figure 8.12. A z-buffer rasterizing two triangles in each of two possible orders. The first triangle is fully rasterized. The second triangle has every pixel computed, but for three of the pixels the depth-contest is lost, and those pixels are not drawn. The final image is the same regardless.
图 8.12。 z 缓冲区以两种可能的顺序光栅化两个三角形。 第一个三角形已完全光栅化。 第二个三角形计算了每个像素，但对于其中三个像素，深度竞争丢失，并且不绘制这些像素。 无论如何，最终图像都是相同的。

### 8.2.4 Per-vertex Shading 每顶点着色

So far the application sending triangles into the pipeline is responsible for setting the color; the rasterizer just interpolates the colors and they are written directly into the output image. For some applications this is sufficient, but in many cases we want 3D objects to be drawn with shading, using the same illumination equations that we used for image-order rendering in Chapter 4. Recall that these equations require a light direction, an eye direction, and a surface normal to compute the color of a surface.
到目前为止，将三角形发送到管道的应用程序负责设置颜色； 光栅化器只是插入颜色并将它们直接写入输出图像中。 对于某些应用程序来说，这已经足够了，但在许多情况下，我们希望使用与第 4 章中用于图像顺序渲染的照明方程相同的照明方程，使用着色来绘制 3D 对象。回想一下，这些方程需要光线方向、眼睛方向 ，以及用于计算表面颜色的表面法线。

One way to handle shading computations is to perform them in the vertex stage. The application provides normal vectors at the vertices, and the positions and colors of the lights are provided separately (they don’t vary across the surface, so they don’t need to be specified for each vertex). For each vertex, the direction to the viewer and the direction to each light are computed based on the positions of the camera, the lights, and the vertex. The desired shading equation is evaluated to compute a color, which is then passed to the rasterizer as the vertex color. Per-vertex shading is sometimes called Gouraud shading.
处理着色计算的一种方法是在顶点阶段执行它们。 该应用程序在顶点处提供法线向量，并且单独提供灯光的位置和颜色（它们在整个表面上不会变化，因此不需要为每个顶点指定它们）。 对于每个顶点，根据相机、灯光和顶点的位置计算到观察者的方向和到每个灯光的方向。 评估所需的着色方程以计算颜色，然后将其作为顶点颜色传递到光栅器。 每顶点着色有时称为 Gouraud 着色。

One decision to be made is the coordinate system in which shading computations are done. World space or eye space are good choices. It is important to choose a coordinate system that is orthonormal when viewed in world space, because shading equations depend on angles between vectors, which are not preserved by operations like nonuniform scale that are often used in the modeling transformation, or perspective projection, often used in the projection to the canonical view volume. Shading in eye space has the advantage that we don’t need to keep track of the camera position, because the camera is always at the origin in eye space, in perspective projection, or the view direction is always +z in orthographic projection.
需要做出的一项决定是进行着色计算的坐标系。 世界空间或眼睛空间是不错的选择。 选择在世界空间中查看时正交的坐标系非常重要，因为着色方程取决于向量之间的角度，而这些角度不能通过建模变换中经常使用的非均匀缩放或经常使用的透视投影等操作来保留。 在到规范视图体积的投影中。 眼睛空间中的阴影的优点是我们不需要跟踪相机位置，因为在透视投影中相机始终位于眼睛空间的原点，或者在正交投影中视图方向始终为 +z。

Per-vertex shading has the disadvantage that it cannot produce any details in the shading that are smaller than the primitives used to draw the surface, because it only computes shading once for each vertex and never in between vertices. For instance, in a room with a floor that is drawn using two large triangles and illuminated by a light source in the middle of the room, shading will be evaluated only at the corners of the room, and the interpolated value will likely be much too dark in the center. Also, curved surfaces that are shaded with specular highlights must be drawn using primitives small enough that the highlights can be resolved.
每顶点着色的缺点是它无法在着色中产生任何小于用于绘制表面的图元的细节，因为它只为每个顶点计算一次着色，而从不在顶点之间计算着色。 例如，在一个使用两个大三角形绘制地板并由房间中间的光源照明的房间中，将仅在房间的角落评估阴影，并且插值可能会太大 中心黑暗。 此外，必须使用足够小的图元来绘制用镜面高光着色的曲面，以便可以解析高光。

Figure 8.13 shows our two spheres drawn with per-vertex shading.
图 8.13 显示了我们用逐顶点着色绘制的两个球体。

![Figure 8.13](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.13.png)
Figure 8.13. Two spheres drawn using per-vertex (Gouraud) shading. Because the triangles are large, interpolation artifacts are visible.
图8.13. 使用逐顶点(Gouraud)着色绘制的两个球体。因为三角形很大，所以可以看到插值伪影。

### 8.2.5 Per-fragment Shading  每片段着色

To avoid the interpolation artifacts associated with per-vertex shading, we can avoid interpolating colors by performing the shading computations after the interpolation, in the fragment stage. In per-fragment shading, the same shading equations are evaluated, but they are evaluated for each fragment using interpolated vectors, rather than for each vertex using the vectors from the application. 
为了避免与每顶点着色相关的插值伪像，我们可以通过在片段阶段插值后执行着色计算来避免插值颜色。 在逐片段着色中，计算相同的着色方程，但使用插值向量对每个片段进行计算，而不是使用应用程序中的向量对每个顶点进行计算。

> Per-fragment shading is sometimes called Phong shading, which is confusing because the same name is attached to the Phong illumination model.
> 每片段着色有时称为 Phong 着色，这很容易混淆，因为 Phong 照明模型也有相同的名称。

In per-fragment shading, the geometric information needed for shading is passed through the rasterizer as attributes, so the vertex stage must coordinate with the fragment stage to prepare the data appropriately. One approach is to interpolate the eye-space surface normal and the eye-space vertex position, which then can be used just as they would in per-vertex shading. 
在逐片段着色中，着色所需的几何信息作为属性通过光栅化器传递，因此顶点阶段必须与片段阶段协调以适当地准备数据。 一种方法是对眼睛空间表面法线和眼睛空间顶点位置进行插值，然后可以像在逐顶点着色中一样使用它们。

Figure 8.14 shows our two spheres drawn with per-fragment shading.
图 8.14 显示了我们用每个片段着色绘制的两个球体。

![Figure 8.14](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 8.14.png)
Figure 8.14. Two spheres drawn using per-fragment shading. Because the triangles are large, interpolation artifacts are visible.
图8.14. 使用每个片段着色绘制的两个球体。因为三角形很大，所以可以看到插值伪影。

### 8.2.6 Texture Mapping  纹理映射

Textures (discussed in Chapter 11) are images that are used to add extra detail to the shading of surfaces that would otherwise look too homogeneous and artificial. The idea is simple: each time shading is computed, we read one of the values used in the shading computation—the diffuse color, for instance—from a texture instead of using the attribute values that are attached to the geometry being rendered. This operation is known as a texture lookup: the shading code specifies a texture coordinate, a point in the domain of the texture, and the texture-mapping system finds the value at that point in the texture image and returns it. The texture value is then used in the shading computation.
纹理（第 11 章中讨论）是用于为表面阴影添加额外细节的图像，否则这些图像看起来过于均匀和人造。 这个想法很简单：每次计算着色时，我们都会从纹理中读取着色计算中使用的值之一（例如漫反射颜色），而不是使用附加到正在渲染的几何体的属性值。 此操作称为纹理查找：着色代码指定纹理坐标、纹理域中的点，纹理映射系统查找纹理图像中该点的值并将其返回。 然后将纹理值用于着色计算。

The most common way to define texture coordinates is simply to make the texture coordinate another vertex attribute. Each primitive then knows where it lives in the texture.
定义纹理坐标最常见的方法就是将纹理坐标作为另一个顶点属性。 然后，每个基元都知道它位于纹理中的位置。

### 8.2.7 Shading Frequency 着色频率

The decision about where to place shading computations depends on how fast the color changes—the scale of the details being computed. Shading with large-scale features, such as diffuse shading on curved surfaces, can be evaluated fairly infrequently and then interpolated: it can be computed with a low shading frequency. Shading that produces small-scale features, such as sharp highlights or detailed textures, needs to be evaluated at a high shading frequency. For details that need to look sharp and crisp in the image, the shading frequency needs to be at least one shading sample per pixel. 
关于在何处进行着色计算的决定取决于颜色变化的速度 - 正在计算的细节的规模。 具有大规模特征的着色（例如曲面上的漫反射着色）可以相当不频繁地进行评估，然后进行插值：可以使用低着色频率进行计算。 产生小尺度特征（例如锐利高光或详细纹理）的着色需要以高着色频率进行评估。 对于需要在图像中看起来清晰锐利的细节，着色频率需要至少为每个像素一个着色样本。

So large-scale effects can safely be computed in the vertex stage, even when the vertices defining the primitives are many pixels apart. Effects that require a high shading frequency can also be computed at the vertex stage, as long as the vertices are close together in the image; alternatively, they can be computed at the fragment stage when primitives are larger than a pixel. 
因此，即使定义图元的顶点相距许多像素，也可以在顶点阶段安全地计算大规模效果。 需要高着色频率的效果也可以在顶点阶段计算，只要图像中的顶点靠近即可； 或者，当基元大于像素时，可以在片段阶段计算它们。

For example, a hardware pipeline as used in a computer game, generally using primitives that cover several pixels to ensure high efficiency, normally does most shading computations per fragment. On the other hand, the PhotoRealistic RenderMan system does all shading computations per vertex, after first subdividing, or dicing, all surfaces into small quadrilaterals called micropolygons that are about the size of pixels. Since the primitives are small, per-vertex shading in this system achieves a high shading frequency that is suitable for detailed shading.
例如，计算机游戏中使用的硬件管道通常使用覆盖多个像素的图元来确保高效率，通常对每个片段进行大部分着色计算。 另一方面，PhotoRealistic RenderMan 系统在首先将所有表面细分或切割成大约像素大小的称为微多边形的小四边形之后，对每个顶点进行所有着色计算。 由于图元很小，因此该系统中的逐顶点着色实现了适合详细着色的高着色频率。

## 8.3 Simple Antialiasing  简单的抗锯齿

Just as with ray tracing, rasterization will produce jagged lines and triangle edgesif we make an all-or-nothing determination of whether each pixel is inside theprimitive or not. In fact, the set of fragments generated by the simple trianglerasterization algorithms described in this chapter, sometimes called standard oraliased rasterization, is exactly the same as the set of pixels that would be mappedto that triangle by a ray tracer that sends one ray through the center of each pixel.Also as in ray tracing, the solution is to allow pixels to be partly covered by aprimitive (Crow, 1978). In practice, this form of blurring helps visual quality,especially in animations. This is shown as the top line of Figure 8.15.
就像光线追踪一样，如果我们对每个像素是否位于基元内部进行全有或全无的确定，则光栅化将产生锯齿状线条和三角形边缘。 事实上，本章中描述的简单三角形光栅化算法（有时称为标准口腔锯齿光栅化）生成的一组片段与通过中心发送一条光线的光线追踪器映射到该三角形的像素组完全相同。 与光线追踪一样，解决方案是允许像素部分被基元覆盖（Crow，1978）。 在实践中，这种形式的模糊有助于提高视觉质量，尤其是在动画中。 这如图 8.15 的顶行所示。
![Figure 8.15](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 8.15.png)
Figure 8.15. An antialiased and a jaggy line viewed at close range so individual pixels are visible. 
图 8.15. 在近距离观察时会出现抗锯齿和锯齿线，因此各个像素都可见。

There are a number of different approaches to antialiasing in rasterizationapplications. Just as with a ray tracer, we can produce an antialiased image bysetting each pixel value to the average color of the image over the square areabelonging to the pixel, an approach known as box filtering. This means we have to think of all drawable entities as having well-defined areas. For example, the linein Figure 8.15 can be thought of as approximating a one-pixel-wide rectangle.
光栅化应用程序中有多种不同的抗锯齿方法。 就像光线追踪器一样，我们可以通过将每个像素值设置为属于该像素的方形区域上图像的平均颜色来生成抗锯齿图像，这种方法称为盒过滤。 这意味着我们必须将所有可绘制实体视为具有明确定义的区域。 例如，图 8.15 中的线条可以被认为近似于一个像素宽的矩形。

> There are better filters thanthe box, but a box filter willsuffice for all but the mostdemanding applications.
> 有比箱式过滤器更好的过滤器，但箱式过滤器足以满足除最苛刻应用之外的所有应用。

The easiest way to implement box-filter antialiasing is by supersampling: create images at very high resolutions and then downsample. For example, if ourgoal is a 256 × 256 pixel image of a line with width 1.2 pixels, we could rasterizea rectangle version of the line with width 4.8 pixels on a 1024 × 1024 screen,and then average 4 × 4 groups of pixels to get the colors for each of the 256 ×256 pixels in the “shrunken” image. This is an approximation of the actual boxfiltered image, but works well when objects are not extremely small relative to thedistance between pixels.
实现盒式滤波器抗锯齿的最简单方法是超级采样：以非常高的分辨率创建图像，然后进行下采样。 例如，如果我们的目标是宽度为 1.2 像素的线条的 256 × 256 像素图像，我们可以在 1024 × 1024 屏幕上光栅化宽度为 4.8 像素的线条的矩形版本，然后平均 4 × 4 组像素以获得 “缩小”图像中每个 256 × 256 像素的颜色。 这是实际盒式过滤图像的近似值，但当对象相对于像素之间的距离不是极小时，效果很好。

Supersampling is quite expensive, however. Because the very sharp edgesthat cause aliasing are normally caused by the edges of primitives, rather thansudden variations in shading within a primitive, a widely used optimization isto sample visibility at a higher rate than shading. If information about coverageand depth is stored for several points within each pixel, very good antialiasingcan be achieved even if only one color is computed. In systems like RenderManthat use per-vertex shading, this is achieved by rasterizing at high resolution: it isinexpensive to do so because shading is simply interpolated to produce colors forthe many fragments, or visibility samples. In systems with per-fragment shading,such as hardware pipelines, multisample antialiasing is achieved by storing foreach fragment a single color plus a coverage mask and a set of depth values.
然而，超级采样非常昂贵。 由于导致锯齿的非常尖锐的边缘通常是由基元的边缘引起的，而不是由基元内着色的突然变化引起的，因此广泛使用的优化是以比着色更高的速率对可见性进行采样。 如果为每个像素内的多个点存储有关覆盖范围和深度的信息，即使只计算一种颜色，也可以实现非常好的抗锯齿效果。 在像 RenderMan 这样使用逐顶点着色的系统中，这是通过以高分辨率进行光栅化来实现的：这样做的成本并不高，因为着色只需插值即可为许多片段或可见性样本生成颜色。 在具有逐片段着色的系统中，例如硬件管道，多重采样抗锯齿是通过为每个片段存储单一颜色加上覆盖遮罩和一组深度值来实现的。

## 8.4 Culling Primitives for Efficiency  剔除基元以提高效率

The strength of object-order rendering, that it requires a single pass over all thegeometry in the scene, is also a weakness for complex scenes. For instance, in amodel of an entire city, only a few buildings are likely to be visible at any giventime. A correct image can be obtained by drawing all the primitives in the scene,but a great deal of effort will be wasted processing geometry that is behind thevisible buildings, or behind the viewer, and therefore doesn’t contribute to thefinal image.
对象顺序渲染的优点是它需要一次遍历场景中的所有几何图形，这也是复杂场景的弱点。 例如，在整个城市的模型中，在任何给定时间可能只有少数建筑物可见。 通过绘制场景中的所有图元可以获得正确的图像，但是大量的精力将浪费在处理可见建筑物后面或观看者后面的几何体上，因此对最终图像没有贡献。

Identifying and throwing away invisible geometry to save the time that wouldbe spent processing it is known as culling. Three commonly implemented cullingstrategies (often used in tandem) are
识别并丢弃不可见的几何体以节省处理它所花费的时间称为剔除。 三种常用的剔除策略（通常串联使用）是

- view volume culling—the removal of geometry that is outside the viewvolume;
  视图体积剔除——移除视体积之外的几何体；
- occlusion culling—the removal of geometry that may be within the viewvolume but is obscured, or occluded, by other geometry closer to thecamera;
  遮挡剔除——移除可能位于视体积内但被更靠近相机的其他几何体遮挡或遮挡的几何体；
- backface culling—the removal of primitives facing away from the camera.
  背面剔除——去除远离相机的图元。

We will briefly discuss view volume culling and backface culling, but cullingin high performance systems is a complex topic; see (Akenine-M¨ oller et al., 2008)for a complete discussion and for information about occlusion culling.
我们将简要讨论视图体积剔除和背面剔除，但高性能系统中的剔除是一个复杂的话题； 有关遮挡剔除的完整讨论和信息，请参阅（Akenine-Měller 等人，2008）。

### 8.4.1 View Volume Culling 视图卷剔除

When an entire primitive lies outside the view volume, it can be culled, since itwill produce no fragments when rasterized. If we can cull many primitives with aquick test, we may be able to speed up drawing significantly. On the other hand,testing primitives individually to decide exactly which ones need to be drawn maycost more than just letting the rasterizer eliminate them.
当整个图元位于视图体积之外时，它可以被剔除，因为它在光栅化时不会产生片段。 如果我们可以通过快速测试剔除许多图元，我们也许能够显着加快绘制速度。 另一方面，单独测试图元以准确决定需要绘制哪些图元可能比仅仅让光栅化器消除它们花费更多。

View volume culling, also known as view frustum culling, is especially helpful when many triangles are grouped into an object with an associated boundingvolume. If the bounding volume lies outside the view volume, then so do all thetriangles that make up the object. For example, if we have 1000 triangles boundedby a single sphere with center $\bold{c}$ and radius $r$, we can check whether the spherelies outside the clipping plane,
当许多三角形被分组为具有关联边界体积的对象时，视图体积剔除（也称为视图视锥体剔除）特别有用。 如果边界体积位于视图体积之外，则构成该对象的所有三角形也是如此。 例如，如果我们有 1000 个由中心 $\bold{c}$ 和半径 $r$ 的单个球体包围的三角形，我们可以检查球体是否位于剪切平面之外，
$(\bold{p} - \bold{a}) · \bold{n} = 0,  $

where $\bold{a}$ is a point on the plane, and $\bold{p}$ is a variable. This is equivalent to checkingwhether the signed distance from the center of the sphere $\bold{c}$ to the plane is greaterthan $+r$. This amounts to the check that
其中$\bold{a}$是平面上的点，$\bold{p}$是变量。 这相当于检查球心 $\bold{c}$ 到平面的有符号距离是否大于 $+r$。 这相当于支票
$\frac{(\bold{c} - \bold{a}) \cdot \bold{n}}{|\|n\|} > r \\$

Note that the sphere may overlap the plane even in a case where all the trianglesdo lie outside the plane. Thus, this is a conservative test. How conservative thetest is depends on how well the sphere bounds the object.
请注意，即使所有三角形都位于平面之外，球体也可能与平面重叠。 因此，这是一个保守的测试。 测试的保守程度取决于球体对物体的限制程度。

The same idea can be applied hierarchically if the scene is organized in oneof the spatial data structures described in Chapter 12.
如果场景以第 12 章中描述的空间数据结构之一进行组织，则可以分层应用相同的想法。

### 8.4.2 Backface Culling 背面剔除

When polygonal models are closed, i.e., they bound a closed space with no holes,then they are often assumed to have outward facing normal vectors as discussedin Chapter 10. For such models, the polygons that face away from the eye arecertain to be overdrawn by polygons that face the eye. Thus, those polygons canbe culled before the pipeline even starts. The test for this condition is the sameone used for silhouette drawing given in Section 10.3.1.
当多边形模型是封闭的时，即它们限定了一个没有孔的封闭空间，那么它们通常被假设为具有朝外的法向量，如第 10 章所述。对于此类模型，背离眼睛的多边形肯定会被透支 面向眼睛的多边形。 因此，可以在管道启动之前剔除这些多边形。 此条件的测试与第 10.3.1 节中给出的轮廓绘制所用的测试相同。

## Frequently Asked Questions 经常问的问题

### I’ve often seen clipping discussed at length, and it is a much more involved process than that described in this chapter. What is going on here? 我经常看到对裁剪进行详细讨论，这是一个比本章中描述的过程复杂得多的过程。 这里发生了什么？

The clipping described in this chapter works, but lacks optimizations that anindustrial-strength clipper would have. These optimizations are discussed in detail in Blinn’s definitive work listed in the chapter notes.
本章中描述的剪裁可以工作，但缺乏工业级剪裁器所具有的优化。 这些优化在章节注释中列出的 Blinn 权威著作中进行了详细讨论。

### How are polygons that are not triangles rasterized? 非三角形的多边形是如何光栅化的？

These can either be done directly scan-line by scan-line, or they can be brokendown into triangles. The latter appears to be the more popular technique.
这些可以直接逐行扫描完成，也可以分解为三角形。 后者似乎是更流行的技术。

### Is it always better to antialias? 抗锯齿总是更好吗？

No. Some images look crisper without antialiasing. Many programs use unantialiased “screen fonts” because they are easier to read. 
不会。有些图像在没有抗锯齿的情况下看起来更清晰。 许多程序使用未抗锯齿的“屏幕字体”，因为它们更易于阅读。

### The documentation for my API talks about “scene graphs” and “matrixstacks.” Are these part of the graphics pipeline?我的 API 文档讨论了“场景图”和“矩阵堆栈”。 这些是图形管道的一部分吗？

The graphics pipeline is certainly designed with these in mind, and whether wedefine them as part of the pipeline is a matter of taste. This book delays theirdiscussion until Chapter 12.
图形管道在设计时肯定考虑到了这些，我们是否将它们定义为管道的一部分是一个品味问题。 本书将他们的讨论推迟到第 12 章。

### Is a uniform distance z-buffer better than the standard one that includesperspective matrix nonlinearities?均匀距离 z 缓冲区是否比包含透视矩阵非线性的标准缓冲区更好？

It depends. One “feature” of the nonlinearities is that the z-buffer has more resolution near the eye and less in the distance. If a level-of-detail system is used,then geometry in the distance is coarser and the “unfairness” of the z-buffer canbe a good thing.
这取决于。 非线性的一个“特征”是 z 缓冲区在眼睛附近的分辨率较高，而在远处的分辨率较低。 如果使用细节层次系统，那么远处的几何图形会更粗糙，并且 z 缓冲区的“不公平”可能是一件好事。

### Is a software z-buffer ever useful?软件 z 缓冲区有用吗？

Yes. Most of the movies that use 3D computer graphics have used a variant of thesoftware z-buffer developed by Pixar (Cook, Carpenter, & Catmull, 1987).
是的。 大多数使用 3D 计算机图形的电影都使用了 Pixar 开发的软件 z 缓冲区的变体（Cook、Carpenter 和 Catmull，1987）。

## Notes 注释

A wonderful book about designing a graphics pipeline is Jim Blinn’s Corner:A Trip Down the Graphics Pipeline (J. Blinn, 1996). Many nice details of thepipeline and culling are in 3D Game Engine Design (Eberly, 2000) and Real-TimeRendering (Akenine-M¨ oller et al., 2008).
Jim Blinn 的《Corner:A Trip Down the Graphics Pipeline》（J. Blinn，1996 年）是一本关于设计图形管道的精彩书籍。 3D 游戏引擎设计（Eberly，2000）和实时渲染（Akenine-Měller 等人，2008）中有许多关于管道和剔除的精彩细节。

## Exercises 练习

1. Suppose that in the perspective transform we have $n = 1$ and $f = 2$. Underwhat circumstances will we have a “reversal” where a vertex before andafter the perspective transform flips from in front of to behind the eye orvice versa?
   假设在透视变换中我们有 $n = 1$ 和 $f = 2$。 在什么情况下我们会出现“反转”，即透视变换前后的顶点从眼睛前面翻转到眼睛后面，反之亦然？
2. Is there any reason not to clip in $x$ and $y$ after the perspective divide (seeFigure 11.2, stage 3)?
   在透视分割之后，是否有任何理由不剪辑 $x$ 和 $y$（参见图 11.2，阶段 3）？
3. Derive the incremental form of the midpoint line-drawing algorithm withcolors at endpoints for $0 < m ≤ 1$.
   推导出端点颜色为 $0 < m ≤ 1$ 的中点画线算法的增量形式。
4. Modify the triangle-drawing algorithm so that it will draw exactly one pixelfor points on a triangle edge which goes through $(x, y) = (-1, -1)$.
   修改三角形绘制算法，使其为经过 $(x, y) = (-1, -1)$ 的三角形边缘上的点精确绘制一个像素。
5. Suppose you are designing an integer z-buffer for flight simulation whereall of the objects are at least one meter thick, are never closer to the viewerthan 4 meters, and may be as far away as 100 km. How many bits areneeded in the z-buffer to ensure there are no visibility errors? Suppose thatvisibility errors only matter near the viewer, i.e., for distances less than 100meters. How many bits are needed in that case?
   假设您正在设计一个用于飞行模拟的整数 z 缓冲区，其中所有对象的厚度至少为 1 米，距离观察者的距离绝不会超过 4 米，并且可能远至 100 公里。 z 缓冲区中需要多少位才能确保不存在可见性错误？ 假设可见度误差仅在观察者附近（即距离小于 100 米）产生影响。 在这种情况下需要多少位？