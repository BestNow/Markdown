# 10  Surface Shading 表面着色

To make objects appear to have more volume, it can help to use shading, i.e., the surface is “painted” with light. This chapter presents the most common heuristic shading methods. The first two, diffuse and Phong shading, were developed in the 1970s and are available in most graphics libraries. The last, artistic shading, uses artistic conventions to assign color to objects. This creates images reminiscent of technical drawings, which is desirable in many applications. 
为了使物体看起来有更大的体积，可以使用阴影，即用光“绘制”表面。 本章介绍最常见的启发式着色方法。 前两种，漫反射和 Phong 着色，是在 20 世纪 70 年代开发的，并且在大多数图形库中都可用。 最后一种是艺术着色，使用艺术惯例为对象分配颜色。 这创建的图像让人想起技术图纸，这在许多应用中都是理想的。

## 10.1 Diffuse Shading 漫反射着色

Many objects in the world have a surface appearance loosely described as “matte,” indicating that the object is not at all shiny. Examples include paper, unfinished wood, and dry, unpolished stones. To a large degree, such objects do not have a color change with a change in viewpoint. For example, if you stare at a particular point on a piece of paper and move while keeping your gaze fixed on that point, the color at that point will stay relatively constant. Such matte objects can be considered as behaving as Lambertian objects. This section discusses how to implement the shading of such objects. A key point is that all formulas in this chapter should be evaluated in world coordinates and not in the warped coordinates after the perspective transform is applied. Otherwise, the angles between normals are changed and the shading will be inaccurate.
世界上许多物体的表面外观被粗略地描述为“无光泽”，表明该物体根本没有光泽。 例如纸张、未加工的木材以及干燥、未抛光的石头。 在很大程度上，此类物体的颜色不会随着视点的变化而变化。 例如，如果您盯着一张纸上的特定点，并在目光固定在该点上的同时移动，则该点的颜色将保持相对恒定。 此类无光泽对象可以被视为具有朗伯对象的行为。 本节讨论如何实现此类对象的着色。 关键点是本章中的所有公式都应在世界坐标中计算，而不是在应用透视变换后在扭曲坐标中计算。 否则，法线之间的角度会发生变化，并且着色将不准确。

### 10.1.1 Lambertian Shading Model  朗伯着色模型

A Lambertian object obeys Lambert’s cosine law, which states that the color c of a surface is proportional to the cosine of the angle between the surface normal and the direction to the light source (Gouraud, 1971):
朗伯物体遵循朗伯余弦定律，该定律规定表面的颜色 c 与表面法线和光源方向之间的角度的余弦成正比（Gouraud，1971）：
$c ∝ \cos θ  $
or in vector form,
或以向量形式，
$c ∝ \bold{n} · \bold{l},  $
where $\bold{n}$ and $\bold{l}$ are shown in Figure 10.1. Thus, the color on the surface will vary according to the cosine of the angle between the surface normal and the light direction. Note that the vector $\bold{l}$ is typically assumed not to depend on the location of the object. That assumption is equivalent to assuming the light is “distant” relative to object size. Such a “distant” light is often called a directional light, because its position is specified only by a direction.
其中 $\bold{n}$ 和 $\bold{l}$ 如图 10.1 所示。 因此，表面上的颜色将根据表面法线与光线方向之间的角度的余弦而变化。 请注意，通常假设向量 $\bold{l}$ 不依赖于对象的位置。 该假设相当于假设光相对于物体大小是“远”的。 这种“远”光通常称为定向光，因为它的位置仅由方向指定。
![Figure 10.1](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.1.png)
Figure 10.1. The geometry for Lambert’s law. Both $\bold{n}$ and $\bold{l}$ are unit vectors.
图 10.1。 兰伯特定律的几何形状。 $\bold{n}$ 和 $\bold{l}$ 都是单位向量。

A surface can be made lighter or darker by changing the intensity of the light source or the reflectance of the surface. The diffuse reflectance $c_r$ is the fraction of light reflected by the surface. This fraction will be different for different color components. For example, a surface is red if it reflects a higher fraction of red incident light than blue incident light. If we assume surface color is proportional to the light reflected from a surface, then the diffuse reflectance $c_r$—an RGB color—must also be included:
通过改变光源的强度或表面的反射率可以使表面变亮或变暗。 漫反射率 $c_r$ 是表面反射的光的比例。 对于不同的颜色分量，该分数会有所不同。 例如，如果表面反射的红色入射光比例高于蓝色入射光，则该表面为红色。 如果我们假设表面颜色与表面反射的光成正比，则还必须包括漫反射率 $c_r$（RGB 颜色）：
$$
c ∝ c_r\bold{n} · \bold{l}. \ \ \ \ \ \ (10.1)
$$
The right-hand side of Equation (10.1) is an RGB color with all RGB components in the range [0, 1]. We would like to add the effects of light intensity while keeping the RGB components in the range [0, 1]. This suggests adding an RGB intensity term $c_l$ which itself has components in the range [0, 1]:
等式（10.1）的右侧是 RGB 颜色，所有 RGB 分量都在 [0, 1] 范围内。 我们希望添加光强度的影响，同时将 RGB 分量保持在 [0, 1] 范围内。 这建议添加一个 RGB 强度项 $c_l$，它本身具有 [0, 1] 范围内的分量：
$$
c = c_rc_l\bold{n} · \bold{l}. (10.2)
$$
This is a very convenient form, but it can produce RGB components for $c$ that are outside the range $[0, 1]$, because the dot product can be negative. The dot product is negative when the surface is pointing away from the light as shown in Figure 10.2. 
这是一种非常方便的形式，但它可以为 $c$ 生成超出范围 $[0, 1]$ 的 RGB 分量，因为点积可能为负。 当表面背向光源时，点积为负，如图 10.2 所示。
![Figure 10.2](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.2.png)
Figure 10.2. When a surface points away from the light, it should receive no light. This case can be verified by checking whether the dot product of $\bold{l}$ and $\bold{n}$ is negative.
图 10.2。 当表面远离光线时，它不应接收到光线。 这种情况可以通过检查 $\bold{l}$ 和 $\bold{n}$ 的点积是否为负来验证。

The “max” function can be added to Equation (10.2) to test for that case:
可以将“max”函数添加到方程（10.2）中来测试这种情况：
$$
c = c_rc_lmax(0, \bold{n} · \bold{l}). \ \ \ \ \ \  (10.3)
$$
Another way to deal with the “negative” light is to use an absolute value:
处理“负”光的另一种方法是使用绝对值：
$$
c = c_rc_l|\bold{n} · \bold{l}|.\ \ \ \ \  (10.4)
$$
While Equation (10.4) may seem physically implausible, it actually corresponds to Equation (10.3) with two lights in opposite directions. For this reason it is often called two-sided lighting (Figure 10.3).
虽然方程（10.4）在物理上看起来不可信，但它实际上对应于方程（10.3），其中两个光方向相反。 因此，它通常被称为两侧照明（图 10.3）。
![Figure 10.3](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.3.png)
Figure 10.3. Using Equation (10.4), the two-sided lighting formula, is equivalent to assuming two opposing light sources of the same color.
图 10.3。 使用方程（10.4)，即两侧照明公式，相当于假设两个相对的相同颜色的光源。

### 10.1.2 Ambient Shading 环境阴影

One problem with the diffuse shading of Equation (10.3) is that any point whose normal faces away from the light will be black. In real life, light is reflected all over, and some light is incident from every direction. In addition, there is often skylight giving “ambient” lighting. One way to handle this is to use several light sources. A common trick is to always put a dim source at the eye so that all visible points will receive some light. Another way is to use two-sided lighting as described by Equation (10.4). A more common approach is to add an ambient term (Gouraud, 1971). This is just a constant color term added to Equation (10.3):
方程 (10.3) 的漫反射着色的一个问题是法线背离光线的任何点都将是黑色的。 在现实生活中，光会到处反射，有些光会从各个方向入射。 此外，通常还有天窗提供“环境”照明。 解决这个问题的一种方法是使用多个光源。 一个常见的技巧是始终将昏暗的光源放在眼睛上，以便所有可见点都会接收到一些光线。 另一种方法是使用两侧照明，如公式 (10.4) 所示。 更常见的方法是添加环境术语（Gouraud，1971）。 这只是添加到方程 (10.3) 中的常数颜色项：
$c = c_r (c_a + c_lmax (0, \bold{n} · \bold{l})) .  $

Intuitively, you can think of the ambient color $c_a$ as the average color of all surfaces in the scene. If you want to ensure that the computed RGB color stays in the range $[0, 1]^3$, then $c_a + c_l ≤ (1, 1, 1)$. Otherwise your code should “clamp” RGB values above one to have the value one.
直观上，您可以将环境颜色 $c_a$ 视为场景中所有表面的平均颜色。 如果要确保计算出的 RGB 颜色保持在 $[0, 1]^3$ 范围内，则 $c_a + c_l ≤ (1, 1, 1)$。 否则，您的代码应将 RGB 值“限制”在 1 以上，以使其值为 1。

### 10.1.3 Vertex-Based Diffuse Shading 基于顶点的漫反射着色

If we apply Equation (10.1) to an object made up of triangles, it will typically have a faceted appearance. Often, the triangles are an approximation to a smooth surface. To avoid the faceted appearance, we can place surface normal vectors at the vertices of the triangles (Phong, 1975), and apply Equation (10.3) at each of the vertices using the normal vectors at the vertices (see Figure 10.4). This will give a color at each triangle vertex, and this color can be interpolated using the barycentric interpolation described in Section 8.1.2. 
如果我们将方程（10.1）应用于由三角形组成的对象，它通常会具有多面外观。 通常，三角形是光滑表面的近似值。 为了避免多面外观，我们可以将表面法线向量放置在三角形的顶点处（Phong，1975），并使用顶点处的法线向量在每个顶点应用方程（10.3）（见图10.4）。 这将在每个三角形顶点给出颜色，并且可以使用第 8.1.2 节中描述的重心插值来插值该颜色。
![Figure 10.4](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.4.png)
Figure 10.4. A circle (left) is approximated by an octagon (right). Vertex normals record the surface normal of the original curve. 
图 10.4。 圆形（左）近似为八边形（右)。 顶点法线记录原始曲线的表面法线。

One problem with shading at triangle vertices is that we need to get the normals from somewhere. Many models will come with normals supplied. If you tessellate your own smooth model, you can create normals when you create the triangles. If you are presented with a polygonal model that does not have normals at vertices and you want to shade it smoothly, you can compute normals by a variety of heuristic methods. The simplest is to just average the normals of the triangles that share each vertex and use this average normal at the vertex. This average normal will not automatically be of unit length, so you should convert it to a unit vector before using it for shading.
三角形顶点着色的一个问题是我们需要从某处获取法线。 许多型号都会提供法线。 如果您对自己的平滑模型进行细分，则可以在创建三角形时创建法线。 如果您看到的多边形模型在顶点处没有法线，并且您希望对其进行平滑着色，则可以通过各种启发式方法计算法线。 最简单的方法是对共享每个顶点的三角形的法线进行平均，并在顶点处使用该平均法线。 该平均法线不会自动具有单位长度，因此您应该在将其用于着色之前将其转换为单位向量。

## 10.2 Phong Shading Phong 阴影

Some surfaces are essentially like matte surfaces, but they have highlights. Examples of such surfaces include polished tile floors, gloss paint, and whiteboards. Highlights move across a surface as the viewpoint moves. This means that we must add a unit vector e toward the eye into our equations. If you look carefully at highlights, you will see that they are really reflections of the light; sometimes these reflections are blurred. The color of these highlights is the color of the light—the surface color seems to have little effect. This is because the reflection occurs at the object’s surface, and the light that penetrates the surface and picks up the object’s color is scattered diffusely.
有些表面本质上类似于无光泽表面，但它们具有高光。 此类表面的示例包括抛光瓷砖地板、光泽涂料和白板。 随着视点的移动，高光也会在表面上移动。 这意味着我们必须在方程中添加一个朝向眼睛的单位向量 e。 如果你仔细观察高光，你会发现它们实际上是光的反射； 有时这些反射是模糊的。 这些高光的颜色就是光的颜色——表面颜色似乎影响不大。 这是因为反射发生在物体表面，穿透表面并拾取物体颜色的光被漫散射。

### 10.2.1 Phong Lighting Model  Phong 光照模型

We want to add a fuzzy “spot” the same color as the light source in the right place. The center of the dot should be drawn where the direction $\bold{e}$ to the eye “lines” up with the natural direction of reflection $\bold{r}$ as shown in Figure 10.5. Here “lines up” is mathematically equivalent to “where $σ$ is zero.” We would like to have the highlight have some nonzero area, so that the eye sees some highlight wherever $σ$ is small. 
我们想在正确的位置添加一个与光源颜色相同的模糊“点”。 点的中心应该绘制在眼睛的方向 $\bold{e}$ 与反射的自然方向 $\bold{r}$ 对齐的位置，如图 10.5 所示。 这里的“排队”在数学上相当于“$σ$ 为零”。 我们希望高光具有一些非零区域，以便眼睛在 $σ$ 较小的地方看到一些高光。
![Figure 10.5](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.5.png)
Figure 10.5. The geometry for the Phong illumination model. The eye should see a highlight if σ is small.
图 10.5。 Phong 照明模型的几何形状。 如果 σ 很小，眼睛应该看到亮点。

Given $\bold{r}$, we’d like a heuristic function that is bright when $\bold{e} = \bold{r}$ and falls off gradually when $\bold{e}$ moves away from $\bold{r}$. An obvious candidate is the cosine of the angle between them:
给定 $\bold{r}$，我们想要一个启发式函数，当 $\bold{e} = \bold{r}$ 时明亮，而当 $\bold{e}$ 远离 $\ 粗体{r}$。 一个明显的候选者是它们之间角度的余弦：
$c = c_l(\bold{e} · \bold{r}).  $

There are two problems with using this equation. The first is that the dot product can be negative. This can be solved computationally with an “if” statement that sets the color to zero when the dot product is negative. The more serious problem is that the highlight produced by this equation is much wider than that seen in real life. The maximum is in the right place and it is the right color, but it is just too big. We can narrow it without reducing its maximum color by raising to a power:
使用这个方程有两个问题。 首先是点积可能为负。 这可以通过“if”语句通过计算来解决，当点积为负时，该语句将颜色设置为零。 更严重的问题是，这个方程产生的亮点比现实生活中看到的要宽得多。 最大值位于正确的位置，颜色也正确，但它太大了。 我们可以通过求幂来缩小它而不减少其最大颜色：
$$
c = c_lmax(0, \bold{e} · \bold{r})^p. \ \ \ \  \ \  \ (10.5)
$$
Here p is called the Phong exponent; it is a positive real number (Phong, 1975). The effect that changing the Phong exponent has on the highlight can be seen in Figure 10.6. 
这里 p 称为 Phong 指数； 它是一个正实数（Phong，1975）。 改变 Phong 指数对高光的影响如图 10.6 所示。
![Figure 10.6](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.6.png)
Figure 10.6. The effect of the Phong exponent on highlight characteristics. This uses Equation (10.5) for the highlight. There is also a diffuse component, giving the objects a shiny but nonmetallic appearance. Image courtesy Nate Robins.
图 10.6。 Phong 指数对高光特征的影响。 这使用方程（10.5)来突出显示。 还有一个漫反射组件，使物体具有闪亮但非金属的外观。 图片由内特·罗宾斯提供。

To implement Equation (10.5), we first need to compute the unit vector r. Given unit vectors l and n, r is the vector l reflected about n. Figure 10.7 shows that this vector can be computed as 
为了实现方程（10.5），我们首先需要计算单位向量r。 给定单位向量 l 和 n，r 是关于 n 反射的向量 l。 图 10.7 显示该向量可以计算为
![Figure 10.7](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.7.png)
Figure 10.7. The geometry for calculating the vector $\bold{r}$. 
图 10.7。 用于计算向量 $\bold{r}$ 的几何图形。
$$
\bold{r} = −\bold{l} + 2(\bold{l} · \bold{n})\bold{n},\ \ \ \ \ \ \ \ (10.6)
$$
where the dot product is used to compute $\cos θ$. 
其中点积用于计算 $\cos θ$。

An alternative heuristic model based on Equation (10.5) eliminates the need to check for negative values of the number used as a base for exponentiation (Warn, 1983). Instead of $\bold{r}$, we compute $\bold{h}$, the unit vector halfway between $\bold{l}$ and $\bold{e}$ (Figure 10.8):
基于方程（10.5）的替代启发式模型无需检查用作求幂基数的数字是否为负值（Warn，1983）。 我们计算 $\bold{h}$，而不是 $\bold{r}$，它是 $\bold{l}$ 和 $\bold{e}$ 之间的单位向量（图 10.8）：
$\bold{h} = \frac{\bold{e} + \bold{l}}{\| \bold{e} + \bold{l} \|} \\$

![Figure 10.8](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.8.png)
Figure 10.8. The unit vector $\bold{h}$ is halfway between $\bold{l}$ and $\bold{e}$.
图 10.8。 单位向量 $\bold{h}$ 位于 $\bold{l}$ 和 $\bold{e}$ 之间。

The highlight occurs when $\bold{h}$ is near $\bold{n}$, i.e., when $\cos ω = \bold{h} · \bold{n}$ is near 1. This suggests the rule:
当 $\bold{h}$ 接近 $\bold{n}$ 时，即当 $\cos ω = \bold{h} · \bold{n}$ 接近 1 时，突出显示。这表明了以下规则： 
$$
c = c_l(\bold{h} · \bold{n})^p. (10.7)
$$
The exponent $p$ here will have analogous control behavior to the exponent in Equation (10.5), but the angle between $\bold{h}$ and $\bold{n}$ is half the size of the angle between $\bold{e}$ and $\bold{r}$, so the details will be slightly different. The advantage of using the cosine between $\bold{n}$ and $\bold{h}$ is that it is always positive for eye and light above the plane. The disadvantage is that a square root and divide is needed to compute $\bold{h}$.
这里的指数$p$将具有与式(10.5)中的指数类似的控制行为，但是$\bold{h}$和$\bold{n}$之间的角度是$\bold{e}$和$\bold{r}$之间角度的一半，因此细节将略有不同。使用$\bold{n}$和$\bold{h}$之间的余弦值的优点是，它对于平面上方的眼睛和光线总是正的。缺点是需要平方根和除法来计算$\bold{h}$。

In practice, we want most materials to have a diffuse appearance in addition to a highlight. We can combine Equations (10.3) and (10.7) to get
在实践中，我们希望大多数材质除了高光之外还具有漫反射外观。 我们可以结合方程（10.3）和（10.7）得到
$$
c = c_r (c_a + c_lmax (0, \bold{n} · \bold{l})) + c_l(\bold{h} · \bold{n})^p. \ \ \ \ \ \ (10.8)
$$
If we want to allow the user to dim the highlight, we can add a control term $c_p$: 
如果我们想允许用户调暗突出显示，我们可以添加一个控制项$c_p$：
$$
c = c_r (c_a + c_lmax (0, \bold{n} · \bold{l})) + c_lc_p(\bold{h} · \bold{n})^p. (10.9)
$$
The term $c_p$ is a RGB color, which allows us to change highlight colors. This is useful for metals where $c_p = c_r$, because highlights on metal take on a metallic color. In addition, it is often useful to make $c_p$ a neutral value less than one, so that colors stay below one. For example, setting $c_p = 1 − M$ where $M$ is the maximum component of $c_r$ will keep colors below one for one light source and no ambient term. 
术语 $c_p$ 是 RGB 颜色，它允许我们更改突出显示颜色。 这对于 $c_p = c_r$ 的金属很有用，因为金属上的高光呈现金属颜色。 此外，将 $c_p$ 设置为小于 1 的中性值通常很有用，这样颜色就会保持在 1 以下。 例如，设置 $c_p = 1 − M$（其中 $M$ 是 $c_r$ 的最大分量）将使一个光源的颜色保持在 1 以下，并且没有环境项。

### 10.2.2 Surface Normal Vector Interpolation 表面法向量插值

Smooth surfaces with highlights tend to change color quickly compared to Lambertian surfaces with the same geometry. Thus, shading at the normal vectors can generate disturbing artifacts.
与具有相同几何形状的朗伯表面相比，具有高光的光滑表面往往会快速改变颜色。 因此，法向量处的阴影可能会产生令人不安的伪影。

These problems can be reduced by interpolating the normal vectors across the polygon and then applying Phong shading at each pixel. This allows you to get good images without making the size of the triangles extremely small. Recall from Chapter 3, that when rasterizing a triangle, we compute barycentric coordinates $(α, β, γ)$ to interpolate the vertex colors $c_0, c_1, c_2$:
通过在多边形上插入法向量，然后在每个像素上应用 Phong 着色，可以减少这些问题。 这样您就可以获得良好的图像，而无需使三角形的尺寸变得非常小。 回想一下第 3 章，当光栅化三角形时，我们计算重心坐标 $(α, β, γ)$ 来插值顶点颜色 $c_0, c_1, c_2$：
$$
c = αc_0 + βc_1 + γc_2. (10.10)
$$
We can use the same equation to interpolate surface normals $n_0$, $n_1$, and $n_2$:
我们可以使用相同的方程来插值表面法线 $n_0$、$n_1$ 和 $n_2$：
$$
\bold{n} = α\bold{n}_0 + β\bold{n}_1 + γ\bold{n}_2. (10.11)
$$
And Equation (10.9) can then be evaluated for the $\bold{n}$ computed at each pixel. Note that the $\bold{n}$ resulting from Equation (10.11) is usually not a unit normal. Better visual results will be achieved if it is converted to a unit vector before it is used in shading computations. This type of normal interpolation is often called Phong normal interpolation (Phong, 1975).
然后可以针对每个像素处计算的 $\bold{n}$ 评估方程（10.9）。 请注意，由方程 (10.11) 得出的 $\bold{n}$ 通常不是单位法线。 如果在用于着色计算之前将其转换为单位向量，将获得更好的视觉效果。 这种类型的法线插值通常称为 Phong 法线插值（Phong，1975）。

## 10.3 Artistic Shading  艺术着色

The Lambertian and Phong shading methods are based on heuristics designed to imitate the appearance of objects in the real world. Artistic shading is designed to mimic drawings made by human artists (Yessios, 1979; Dooley & Cohen, 1990; Saito & Takahashi, 1990; L. Williams, 1991). Such shading seems to have advantages in many applications. For example, auto manufacturers hire artists to draw diagrams for car owners’ manuals. This is more expensive than using much more “realistic” photographs, so there is probably some intrinsic advantage to the techniques of artists when certain types of communication are needed. In this section, we show how to make subtly shaded line drawings reminiscent of human-drawn images. Creating such images is often called non-photorealistic rendering, but we will avoid that term because many non-photorealistic techniques are used for efficiency that are not related to any artistic practice.
Lambertian 和 Phong 着色方法基于启发式算法，旨在模仿现实世界中对象的外观。 艺术着色旨在模仿人类艺术家的绘画（Yessios，1979；Dooley & Cohen，1990；Saito & Takahashi，1990；L. Williams，1991）。 这种阴影似乎在许多应用中都有优势。 例如，汽车制造商聘请艺术家为车主手册绘制图表。 这比使用更“现实”的照片更昂贵，因此当需要某些类型的交流时，艺术家的技术可能有一些内在的优势。 在本节中，我们将展示如何制作微妙的阴影线条图，让人想起人类绘制的图像。 创建此类图像通常称为非真实感渲染，但我们将避免使用该术语，因为许多非真实感技术用于提高与任何艺术实践无关的效率。

### 10.3.1 Line Drawing 画线

The most obvious thing we see in human drawings that we don’t see in real life is silhouettes. When we have a set of triangles with shared edges, we should draw an edge as a silhouette when one of the two triangles sharing an edge faces toward the viewer, and the other triangle faces away from the viewer. This condition can be tested for two normals $\bold{n}_0$ and $\bold{n}_1$ by
我们在人类绘画中看到但在现实生活中看不到的最明显的东西是剪影。 当我们有一组具有共享边的三角形时，当共享边的两个三角形中的一个面向观察者，而另一个三角形背向观察者时，我们应该绘制一条边作为轮廓。 可以通过以下方式对两个法线 $\bold{n}_0$ 和 $\bold{n}1$ 测试此条件
$draw\ silhouette\ if (\bold{e} · \bold{n}_0)(\bold{e} · \bold{n}_1) ≤ 0.  $

Here $\bold{e}$ is a vector from the edge to the eye. This can be any point on the edge or either of the triangles. Alternatively, if $f_i(\bold{p}) = 0$ are the implicit plane equations for the two triangles, the test can be written
这里$\bold{e}$是从边缘到眼睛的向量。 这可以是边缘或任一三角形上的任何点。 或者，如果 $f_i(\bold{p}) = 0$ 是两个三角形的隐式平面方程，则可以编写测试
$draw\ silhouette\ if\ f_0(\bold{e})f_1(\bold{e}) ≤ 0.  $

We would also like to draw visible edges of a polygonal model. To do this, we can use either of the hidden surface methods of Chapter 12 for drawing in the background color and then draw the outlines of each triangle in black. This, in fact, will also capture the silhouettes. Unfortunately, if the polygons represent a smooth surface, we really don’t want to draw most of those edges. However, we might want to draw all creases where there really is a corner in the geometry. We can test for creases by using a heuristic threshold:
我们还想绘制多边形模型的可见边缘。 为此，我们可以使用第 12 章中的任何一种隐藏表面方法来绘制背景色，然后用黑色绘制每个三角形的轮廓。 事实上，这也将捕捉剪影。 不幸的是，如果多边形代表光滑的表面，我们真的不想绘制大部分边缘。 然而，我们可能想要在几何体中确实有角的地方绘制所有折痕。 我们可以使用启发式阈值来测试折痕：
$draw\ crease\ if\ (n_0 · n_1) ≤ threshold.  $

This combined with the silhouette test will give nice-looking line drawings. 
与轮廓测试相结合将得到漂亮的线条图。

### 10.3.2 Cool-to-Warm Shading 冷色到暖色着色

When artists shade line drawings, they often use low intensity shading to give some impression of curve to the surface and to give colors to objects (Gooch, Gooch, Shirley, & Cohen, 1998). Surfaces facing in one direction are shaded with a cool color, such as a blue, and surfaces facing in the opposite direction are shaded with a warm color, such as orange. Typically these colors are not very saturated and are also not dark. That way, black silhouettes show up nicely. Overall this gives a cartoon-like effect. This can be achieved by setting up a direction to a “warm” light l and using the cosine to modulate color, where the warmth constant $k_w$ is defined on $[0, 1]$:
当艺术家对线条图进行着色时，他们经常使用低强度着色来给表面带来一些曲线印象，并为物体赋予颜色（Gooch、Gooch、Shirley 和 Cohen，1998）。 面向一个方向的表面用冷色（例如蓝色）着色，面向相反方向的表面用暖色（例如橙色）着色。 通常这些颜色不是很饱和，也不是很暗。 这样，黑色轮廓就会很好地显现出来。 总体而言，这给出了类似卡通的效果。 这可以通过设置“暖”光 l 的方向并使用余弦来调制颜色来实现，其中暖度常数 $k_w$ 在 $[0, 1]$ 上定义：
$k_w = \frac{1 + \bold{n} \cdot \bold{l}}{2} \\$

The color $c$ is then just a linear blend of the cool color $c_c$ and the warm color $c_w$: 
那么颜色 $c$ 只是冷色 $c_c$ 和暖色 $c_w$ 的线性混合：
$c = k_wc_w + (1 - k_w)c_c.  $

There are many possible $c_w$ and $c_b$ that will produce reasonable looking results. A good starting place for a guess is
有许多可能的 $c_w$ 和 $c_b$ 会产生合理的结果。 猜测的一个很好的起点是
$$
c_c = (0.4, 0.4, 0.7), \\
c_c = (0.8, 0.6, 0.6).
$$
Figure 10.9 shows a comparison between traditional Phong lighting and this type of artistic shading.
图 10.9 显示了传统 Phong 照明与此类艺术着色之间的比较。
![Figure 10.9](E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 10.9.png)
Figure 10.9. Left: a Phong-illuminated image. Middle: cool-to-warm shading is not useful without silhouettes. Right: cool-to-warm shading plus silhouettes. Image courtesy Amy Gooch. 
图 10.9。 左：Phong 照明图像。 中：如果没有轮廓，从冷到暖的阴影是没有用的。 右：从冷色到暖色的阴影加上轮廓。 图片由艾米·古奇提供。

## Frequently Asked Questions 经常问的问题

### All of the shading in this chapter seems like enormous hacks. Is that true? 本章中的所有阴影看起来都是巨大的黑客攻击。 真的吗？

Yes. However, they are carefully designed hacks that have proven useful in practice. In the long run, we will probably have better-motivated algorithms that include physics, psychology, and tone-mapping. However, the improvements in image quality will probably be incremental. 
是的。 然而，它们是精心设计的技巧，在实践中证明是有用的。 从长远来看，我们可能会拥有更积极的算法，包括物理学、心理学和色调映射。 然而，图像质量的改进可能是渐进的。

### I hate calling pow(). Is there a way to avoid it when doing Phong lighting? 我讨厌调用 pow()。 在进行 Phong 照明时有没有办法避免这种情况？

A simple way is to only have exponents that are themselves a power of two, i.e., 2, 4, 8, 16, . . . . In practice, this is not a problematic restriction for most applications. A look-up table is also possible, but will often not give a large speed-up.
一种简单的方法是只使用本身是 2 的幂的指数，即 2, 4, 8, 16, . . . .。 实际上，对于大多数应用程序来说这并不是一个有问题的限制。 查找表也是可能的，但通常不会提供很大的加速。

## Exercises 练习

1. The moon is poorly approximated by diffuse or Phong shading. What observations tell you that this is true? 
   漫反射或 Phong 阴影对月亮的近似效果很差。 什么观察告诉你这是真的？
2. Velvet is poorly approximated by diffuse or Phong shading. What observations tell you that this is true?
   漫反射或 Phong 阴影对天鹅绒的近似效果很差。 什么观察告诉你这是真的？
3. Why do most highlights on plastic objects look white, while those on gold metal look gold?
   为什么塑料物体上的大多数高光看起来是白色的，而金色金属上的高光看起来是金色的？