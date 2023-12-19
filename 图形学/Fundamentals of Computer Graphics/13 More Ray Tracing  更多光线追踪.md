# 13  More Ray Tracing  更多光线追踪

A ray tracer is a great substrate on which to build all kinds of advanced rendering effects. Many effects that take significant work to fit into the object-order rasterization framework, including basics like the shadows and reflections already presented in Chapter 4, are simple and elegant in a ray tracer. In this chapter, we discuss some fancier techniques that can be used to ray-trace a wider variety of scenes and to include a wider variety of effects. Some extensions allow more general geometry: instancing and constructive solid geometry (CSG) are two ways to make models more complex with minimal complexity added to the program. Other extensions add to the range of materials we can handle: refraction through transparent materials, like glass and water, and glossy reflections on a variety of surfaces are essential for realism in many scenes.
光线追踪器是构建各种高级渲染效果的绝佳基础。 许多需要大量工作才能适应对象顺序光栅化框架的效果，包括第 4 章中已经介绍的阴影和反射等基础知识，在光线追踪器中都是简单而优雅的。 在本章中，我们将讨论一些更高级的技术，这些技术可用于对更广泛的场景进行光线追踪并包含更广泛的效果。 一些扩展允许更通用的几何图形：实例化和构造实体几何图形（CSG）是使模型变得更加复杂的两种方法，同时将添加到程序中的复杂性降至最低。 其他扩展增加了我们可以处理的材质范围：通过玻璃和水等透明材质的折射以及各种表面上的光泽反射对于许多场景中的真实感至关重要。

This chapter also discusses the general framework of distribution ray tracing (Cook, Porter, & Carpenter, 1984), a powerful extension to the basic raytracing idea in which multiple random rays are sent through each pixel in an image to produce images with smooth edges and to simply and elegantly (if slowly) produce a wide range of effects from soft shadows to camera depth-of-field.
本章还讨论了分布光线追踪的一般框架（Cook、Porter 和 Carpenter，1984），它是基本光线追踪思想的强大扩展，其中多条随机光线穿过图像中的每个像素，以生成具有平滑边缘和边缘的图像。 简单而优雅（如果缓慢）产生从柔和阴影到相机景深的各种效果。

> If you start with a brute-force ray intersection loop, you’ll have ample time to implement an acceleration structure while you wait for images to render.
> 如果您从强力射线相交循环开始，那么在等待图像渲染时您将有充足的时间来实现加速结构。

The price of the elegance of ray tracing is exacted in terms of computer time: most of these extensions will trace a very large number of rays for any nontrivial scene. Because of this, it’s crucial to use the methods described in Chapter 12 to accelerate the tracing of rays.
光线追踪的优雅代价是根据计算机时间来计算的：大多数这些扩展都会为任何重要的场景追踪大量光线。 因此，使用第 12 章中描述的方法来加速光线追踪至关重要。

## 13.1 Transparency and Refraction 透明度和折射

In Chapter 4, we discussed the use of recursive ray tracing to compute specular, or mirror, reflection from surfaces. Another type of specular object is a dielectric—a transparent material that refracts light. Diamonds, glass, water, and air are dielectrics. Dielectrics also filter light; some glass filters out more red and blue light than green light, so the glass takes on a green tint. When a ray travels from a medium with refractive index n into one with a refractive index $n_t$, some of the light is transmitted, and it bends. This is shown for $n_t > n$ in Figure 13.1. Snell’s Law tells us that
在第 4 章中，我们讨论了使用递归光线追踪来计算表面的镜面反射或镜面反射。 另一种类型的镜面物体是电介质——一种折射光的透明材料。 钻石、玻璃、水和空气都是电介质。 电介质还可以过滤光； 有些玻璃过滤掉的红光和蓝光多于绿光，因此玻璃呈现出绿色色调。 当光线从折射率为 n 的介质传播到折射率为 $n_t$ 的介质时，部分光会被透射，并且会发生弯曲。 图 13.1 中显示了 $n_t > n$ 的情况。 斯涅尔定律告诉我们
$n \sin θ = n_t \sin φ.  $

> Example values of n:
> air: 1.00;
> water: 1.33–1.34;
> window glass: 1.51;
> optical glass: 1.49–1.92;
> diamond: 2.42.  

![Figure 13.1](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.1.png)
Figure 13.1. Snell’s Law describes how the angle $φ$ depends on the angle $θ$ and the refractive indices of the object and the surrounding medium. 
图 13.1。 斯涅尔定律描述了角度 $φ$ 如何取决于角度 $θ$ 以及物体和周围介质的折射率。

Computing the sine of an angle between two vectors is usually not as convenient as computing the cosine, which is a simple dot product for the unit vectors such as we have here. Using the trigonometric identity $\sin^2 θ + \cos^2 θ = 1$, we can derive a refraction relationship for cosines:
计算两个向量之间角度的正弦通常不如计算余弦那么方便，余弦是单位向量的简单点积，就像我们这里的那样。 利用三角恒等式 $\sin^2 θ + \cos^2 θ = 1$，我们可以推导出余弦的折射关系：
$$
\cos^2 φ = 1 − \frac{n^2 (1 − \cos^2 θ)}{n^2_t}
$$
Note that if $n$ and $n_t$ are reversed, then so are $θ$ and $φ$ as shown on the right of Figure 13.1.
请注意，如果 $n$ 和 $n_t$ 颠倒，那么 $θ$ 和 $φ$ 也颠倒，如图 13.1 右侧所示。 

To convert $\sin φ$ and $\cos φ$ into a 3D vector, we can set up a 2D orthonormal basis in the plane of the surface normal, $\bold{n}$, and the ray direction, $\bold{d}$. 
为了将$\sin φ$和$\cos φ$转换成一个3D向量，我们可以在表面法线$\bold{n}$和射线方向$\bold{d}$的平面上建立一个二维正交基。

From Figure 13.2, we can see that $\bold{n}$ and $\bold{b}$ form an orthonormal basis for the plane of refraction. By definition, we can describe the direction of the transformed ray, $\bold{t}$, in terms of this basis:
从图13.2中，我们可以看到$\bold{n}$和$\bold{b}$构成了折射平面的正交基。 根据定义，我们可以根据这个基础来描述变换后的光线 $\bold{t}$ 的方向：
$\bold{t} = \sin φ\bold{b} - \cos φ\bold{n}.  $
![Figure 13.2](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.2.png)
Figure 13.2. The vectors $\bold{n}$  and $\bold{b}$ form a 2D orthonormal basis that is parallel to the transmission vector $\bold{t}$.
图 13.2。 向量 $\bold{n}$ 和 $\bold{b}$ 形成与传输向量 $\bold{t}$ 平行的 2D 正交基。 

Since we can describe $\bold{d}$ in the same basis, and $\bold{d}$ is known, we can solve for $\bold{b}$:
由于我们可以在相同的基础上描述$\bold{d}$，并且$\bold{d}$已知，因此我们可以求解$\bold{b}$：
$$
\bold{d} = \sin θ\bold{b} − \cos θ\bold{n}, \\
\bold{n} = \frac{\bold{d} + \bold{n} \cos θ}{\sin θ}
$$

This means that we can solve for $\bold{t}$ with known variables: 
这意味着我们可以用已知变量求解 $\bold{t}$：
$$
\bold{t} = \frac{n(\bold{d} + \bold{n}\cosθ )}{n-t} - \bold{n}φ \\
= \frac{\bold{n}-(\bold{d} − \bold{n}(\bold{d} · \bold{n}))}{n_t} - 
\bold{n}\sqrt{1 - \frac{n^2(1 - (\bold{d}\cdot \bold{n}))^2)}{n^2_t}}
$$
Note that this equation works regardless of which of n and $n_t$ is larger. An immediate question is, “What should you do if the number under the square root is negative?” In this case, there is no refracted ray and all of the energy is reflected. This is known as total internal reflection, and it is responsible for much of the rich appearance of glass objects. 
请注意，无论 n 和 $n_t$ 中哪一个更大，该方程都有效。 一个直接的问题是，“如果平方根下的数字是负数，你该怎么办？” 在这种情况下，没有折射光线，所有能量都被反射。 这被称为全内反射，它是玻璃物体丰富外观的主要原因。

The reflectivity of a dielectric varies with the incident angle according to the Fresnel equations. A nice way to implement something close to the Fresnel equations is to use the Schlick approximation (Schlick, 1994a),
根据菲涅尔方程，电介质的反射率随入射角变化。 实现接近菲涅耳方程的一个好方法是使用 Schlick 近似（Schlick，1994a），
$R(θ) = R_0 + (1 - R_0) (1 - \cos θ)^5 ,  $

where $R_0$ is the reflectance at normal incidence:
其中 $R_0$ 是法向入射时的反射率：
$$
R_0 = (\frac{n_t - 1}{n_t + 1})^2
$$
Note that the $\cos θ$ terms above are always for the angle in air (the larger of the internal and external angles relative to the normal). 
请注意，上面的 $\cos θ$ 项始终针对空气中的角度（相对于法线的内角和外角中较大的一个）。

For homogeneous impurities, as is found in typical colored glass, a lightcarrying ray’s intensity will be attenuated according to Beer’s Law. As the ray travels through the medium it loses intensity according to $dI = −CI dx$, where dx is distance. Thus, $dI/dx = −CI$. We can solve this equation and get the exponential $I = k exp(−Cx)$. The degree of attenuation is described by the RGB attenuation constant a, which is the amount of attenuation after one unit of distance. Putting in boundary conditions, we know that $I(0) = I_0$, and $I(1) = aI(0)$. The former implies $I(x) = I_0exp(-Cx)$. The latter implies $I_0a = I_0 exp(-C)$, so $-C = ln(a)$. Thus, the final formula is
对于均匀的杂质，如典型的彩色玻璃中所发现的，携带光线的射线的强度将根据比尔定律衰减。当射线穿过介质时，它的强度会根据$dI = −CI dx$,减小，其中dx是距离。因此，$dI/dx = −CI$。我们可以解这个方程，得到指数$I = k exp(−Cx)$。衰减的程度由RGB衰减常数a描述，它是单位距离后的衰减量。代入边界条件，我们知道$I(0) = I_0$，并且$I(1) = aI(0)$。前者意味着$I(x) = I_0exp(-Cx)$。后者意味着$I_0a = I_0 exp(-C)$，所以$-C = ln(a)$。因此，最终的公式是
$I(s) = I(0)e^{ln(a)s,}  $

where I(s) is the intensity of the beam at distance s from the interface. In practice, we reverse-engineer a by eye, because such data is rarely easy to find. The effect of Beer’s Law can be seen in Figure 13.3, where the glass takes on a green tint. 
其中 I(s) 是距界面距离 s 处的光束强度。 在实践中，我们通过肉眼进行逆向工程，因为此类数据很少容易找到。 比尔定律的影响如图 13.3 所示，其中玻璃呈现绿色。
![Figure 13.3](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.3.png)
Figure 13.3. The color of the glass is affected by total internal reflection and Beer’s Law. The amount of light transmitted and reflected is determined by the Fresnel equations. The complex lighting on the ground plane was computed using particle tracing as described in Chapter 23.
图 13.3。 玻璃的颜色受全内反射和比尔定律的影响。 透射和反射的光量由菲涅尔方程确定。 地平面上的复杂光照是使用第 23 章中所述的粒子追踪来计算的。

To add transparent materials to our code, we need a way to determine when a ray is going “into” an object. The simplest way to do this is to assume that all objects are embedded in air with refractive index very close to 1.0, and that surface normals point “out” (toward the air). The code segment for rays and dielectrics with these assumptions is:
为了将透明材质添加到我们的代码中，我们需要一种方法来确定光线何时“进入”对象。 最简单的方法是假设所有物体都嵌入空气中，折射率非常接近 1.0，并且表面法线指向“外面”（朝向空气）。 具有这些假设的射线和电介质的代码段是：

> if ($\bold{p}$ is on a dielectric) then
> 	$\bold{r}$ = reflect$(\bold{d}, \bold{n} )$
> 	if $(\bold{d} · \bold{n} < 0)$ then
> 		refract$(\bold{d}, \bold{n}, n, \bold{t})$
> 		$c = -\bold{d} · \bold{n}$
> 		$k_r = k_g = k_b = 1$
> 	else
> 		$k_r = exp(-a_rt)$
> 		$kg = exp(-a_gt)$
> 		$k_b = exp(-a_bt)$
> 		if refract$(\bold{d}, -\bold{n}, 1/n, \bold{t})$ then
> 			$c = \bold{t} · \bold{n}$
> 		else
> 			return $k ∗ color(\bold{p} + t\bold{r})$
> 	$R_0 = (n - 1)^2/(n + 1)^2$
> 	$R = R_0 + (1 - R_0)(1 - c)^5$
> 	return $k(R color(\bold{p} + t\bold{r}) + (1 - R)$ color$(\bold{p} + t\bold{t}))$  

The code above assumes that the natural log has been folded into the constants $(a_r, a_g, a_b)$. The refract function returns false if there is total internal reflection, and otherwise it fills in the last argument of the argument list.
上面的代码假设自然对数已折叠为常量 $(a_r, a_g, a_b)$。 如果存在全内反射，则 refract 函数返回 false，否则将填充参数列表的最后一个参数。

## 13.2 Instancing 实例化

An elegant property of ray tracing is that it allows very natural instancing. The basic idea of instancing is to distort all points on an object by a transformation matrix before the object is displayed. For example, if we transform the unit circle (in 2D) by a scale factor (2, 1) in x and y, respectively, then rotate it by 45◦, and move one unit in the x-direction, the result is an ellipse with an eccentricity of 2 and a long axis along the $(x = −y)$-direction centered at (0, 1) (Figure 13.4). The key thing that makes that entity an “instance” is that we store the circle and the composite transform matrix. Thus, the explicit construction of the ellipse is left as a future operation at render time.
光线追踪的一个优雅特性是它允许非常自然的实例化。 实例化的基本思想是在显示对象之前通过变换矩阵扭曲对象上的所有点。 例如，如果我们将单位圆（二维）在 x 和 y 方向上分别按比例因子 (2, 1) 进行变换，然后将其旋转 45°，并在 x 方向上移动一个单位，则结果是 椭圆，偏心率为 2，长轴沿 $(x = −y)$ 方向，中心为 (0, 1)（图 13.4）。 使该实体成为“实例”的关键是我们存储圆和复合变换矩阵。 因此，椭圆的显式构造留作渲染时的未来操作。
![Figure 13.4](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.4.png)
Figure 13.4. An instance of a circle with a series of three transforms is an ellipse.
图 13.4。 具有一系列三个变换的圆的一个实例是椭圆。

The advantage of instancing in ray tracing is that we can choose the space in which to do intersection. If the base object is composed of a set of points, one of which is $\bold{p}$, then the transformed object is composed of that set of points transformed by matrix $\bold{M}$, where the example point is transformed to $\bold{Mp}$. If we have a ray $\bold{a} + t\bold{b}$ that we want to intersect with the transformed object, we can instead intersect an inverse-transformed ray with the untransformed object (Figure 13.5). There are two potential advantages to computing in the untransformed space (i.e., the right-hand side of Figure 13.5):
光线追踪中实例化的优点是我们可以选择进行相交的空间。 如果基础对象由一组点组成，其中一个为 $\bold{p}$，则变换后的对象由矩阵 $\bold{M}$ 变换的该组点组成，其中示例点 转换为$\bold{Mp}$。 如果我们有一条射线 $\bold{a} + t\bold{b}$ 想要与变换后的对象相交，我们可以将逆变换的射线与未变换的对象相交（图 13.5）。 在未变换空间（即图 13.5 的右侧）中进行计算有两个潜在优势：
![Figure 13.5](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.5.png)
Figure 13.5. The ray intersection problem in the two spaces are just simple transforms of each other. The object is specified as a sphere plus matrix $\bold{M}$. The ray is specified in the transformed (world) space by location $\bold{a}$ and direction $\bold{b}$.
图 13.5。 两个空间中的射线相交问题只是彼此的简单变换。 该对象被指定为球体加矩阵 $\bold{M}$。 光线在变换后的（世界)空间中通过位置 $\bold{a}$ 和方向 $\bold{b}$ 指定。

1. The untransformed object may have a simpler intersection routine, e.g., a sphere versus an ellipsoid. 
   未变换的对象可能具有更简单的相交例程，例如球体与椭球体。
2. Many transformed objects can share the same untransformed object thus reducing storage, e.g., a traffic jam of cars, where individual cars are just transforms of a few base (untransformed) models.
   许多转换后的对象可以共享相同的未转换对象，从而减少存储，例如，汽车交通拥堵，其中各个汽车只是一些基本（未转换）模型的转换。

As discussed in Section 6.2.2, surface normal vectors transform differently. With this in mind and using the concepts illustrated in Figure 13.5, we can determine the intersection of a ray and an object transformed by matrix $\bold{M}$. If we create an instance class of type surface, we need to create a hit function:
正如第 6.2.2 节中所讨论的，表面法线向量的变换方式不同。 考虑到这一点并使用图 13.5 中所示的概念，我们可以确定光线与由矩阵 $\bold{M}$ 变换的物体的交集。 如果我们创建一个surface类型的实例类，我们需要创建一个hit函数：

> instance::hit(ray $\bold{a} + t\bold{b}$, real $t_0$, real $t_1$, hit-record rec)
> 	ray $\bold{r}' = \bold{M}^{-1}\bold{a} + t\bold{M}^{-1}\bold{b}$
> 	if (base-object→hit$(\bold{r}', t_0, t_1, rec))$ then
> 		$rec.\bold{n} = (\bold{M}^{-1})^Trec.\bold{n}$
> 		return true
> 	else
> 		return false  

An elegant thing about this function is that the parameter rec.t does not need to be changed, because it is the same in either space. Also note that we need not compute or store the matrix $\bold{M}$. 
该函数的一个优雅之处在于参数 rec.t 不需要更改，因为它在两个空间中都是相同的。 另请注意，我们不需要计算或存储矩阵 $\bold{M}$。

This brings up a very important point: the ray direction $\bold{b}$ must not be restricted to a unit-length vector, or none of the infrastructure above works. For this reason, it is useful not to restrict ray directions to unit vectors.
这提出了一个非常重要的点：光线方向 $\bold{b}$ 不得限制为单位长度向量，否则上述基础设施都不起作用。 因此，不将射线方向限制为单位向量是有用的。

## 13.3 Constructive Solid Geometry  构造立体几何

One nice thing about ray tracing is that any geometric primitive whose intersection with a 3D line can be computed can be seamlessly added to a ray tracer. It turns out to also be straightforward to add constructive solid geometry (CSG) to a ray tracer (Roth, 1982). The basic idea of CSG is to use set operations to combine solid shapes. These basic operations are shown in Figure 13.6. The operations can be viewed as set operations. For example, we can consider $C$ the set of all points in the circle and $S$ the set of all points in the square. The intersection operation $C ∩ S$ is the set of all points that are both members of $C$ and $S$. The other operations are analogous.
光线追踪的一个好处是，任何可以计算与 3D 线相交的几何图元都可以无缝添加到光线追踪器中。 事实证明，将构造实体几何 (CSG) 添加到光线追踪器中也很简单（Roth，1982）。 CSG的基本思想是使用集合运算来组合实体形状。 这些基本操作如图 13.6 所示。 这些操作可以被视为集合操作。 例如，我们可以认为$C$是圆中所有点的集合，$S$是正方形中所有点的集合。 交集运算 $C ∩ S$ 是同时属于 $C$ 和 $S$ 成员的所有点的集合。 其他操作类似。
![Figure 13.6](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.6.png)
Figure 13.6. The basic CSG operations on a 2D circle and square.
图 13.6。 二维圆形和正方形上的基本 CSG 运算。

Although one can do CSG directly on the model, if all that is desired is an image, we do not need to explicitly change the model. Instead, we perform the set operations directly on the rays as they interact with a model. To make this natural, we find all the intersections of a ray with a model rather than just the closest. For example, a ray $\bold{a} + t\bold{b}$ might hit a sphere at $t = 1$ and $t = 2$. In the context of CSG, we think of this as the ray being inside the sphere for $t ∈ [1, 2]$. We can compute these “inside intervals” for all of the surfaces and do set operations on those intervals (recall Section 2.1.2). This is illustrated in Figure 13.7, where the hit intervals are processed to indicate that there are two intervals inside the difference object. The first hit for $t > 0$ is what the ray actually intersects.
虽然可以直接在模型上进行 CSG，但如果需要的只是一张图像，则不需要显式更改模型。 相反，当光线与模型交互时，我们直接对光线执行集合操作。 为了使其自然，我们找到光线与模型的所有交点，而不仅仅是最接近的交点。 例如，光线 $\bold{a} + t\bold{b}$ 可能会在 $t = 1$ 和 $t = 2$ 处撞击球体。 在 CSG 的上下文中，我们将其视为 $t ∈ [1, 2]$ 球体内的射线。 我们可以计算所有曲面的这些“内部区间”，并对这些区间进行集合运算（回想第 2.1.2 节）。 图 13.7 对此进行了说明，其中处理命中间隔以指示差异对象内有两个间隔。 $t > 0$ 的第一次命中是射线实际相交的地方。
![Figure 13.7](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.7.png)
Figure 13.7. Intervals are processed to indicate how the ray hits the composite object.
图 13.7。 处理间隔以指示光线如何撞击复合对象。

In practice, the CSG intersection routine must maintain a list of intervals. When the first hitpoint is determined, the material property and surface normal is that associated with the hitpoint. In addition, you must pay attention to precision issues because there is nothing to prevent the user from taking two objects that abut and taking an intersection. This can be made robust by eliminating any interval whose thickness is below a certain tolerance.
实际上，CSG 交叉例程必须维护一个间隔列表。 当确定第一个命中点时，材质属性和表面法线就是与该命中点相关的属性和表面法线。 此外，您必须注意精度问题，因为没有什么可以阻止用户获取相邻的两个对象并进行相交。 通过消除厚度低于特定公差的任何间隔，可以使这一点变得稳健。

## 13.4 Distribution Ray Tracing 分布光线追踪

For some applications, ray-traced images are just too “clean.” This effect can be mitigated using distribution ray tracing (Cook et al., 1984). The conventionally ray-traced images look clean, because everything is crisp; the shadows are perfectly sharp, the reflections have no fuzziness, and everything is in perfect focus. Sometimes we would like to have the shadows be soft (as they are in real life), the reflections be fuzzy as with brushed metal, and the image have variable degrees of focus as in a photograph with a large aperture. While accomplishing these things from first principles is somewhat involved (as is developed in Chapter 23), we can get most of the visual impact with some fairly simple changes to the basic ray tracing algorithm. In addition, the framework gives us a relatively simple way to antialias (recall Section 8.3) the image.
对于某些应用程序来说，光线追踪图像太“干净”。 使用分布光线追踪可以减轻这种影响（Cook 等人，1984）。 传统的光线追踪图像看起来很干净，因为一切都很清晰； 阴影非常清晰，反射没有模糊，一切都完美聚焦。 有时我们希望阴影是柔和的（就像现实生活中的那样），反射是模糊的，就像拉丝金属一样，并且图像具有可变的焦度，就像大光圈照片中的那样。 虽然从第一原理完成这些事情有些复杂（如第 23 章中所述），但我们可以通过对基本光线追踪算法进行一些相当简单的更改来获得大部分视觉效果。 此外，该框架为我们提供了一种相对简单的方法来对图像进行抗锯齿（回忆第 8.3 节）。

### 13.4.1 Antialiasing 抗锯齿

Recall that a simple way to antialias an image is to compute the average color for the area of the pixel rather than the color at the center point. In ray tracing, our computational primitive is to compute the color at a point on the screen. If we average many of these points across the pixel, we are approximating the true average. If the screen coordinates bounding the pixel are $[i, i + 1] × [j, j + 1]$, then we can replace the loop:
回想一下，对图像进行抗锯齿的一种简单方法是计算像素区域的平均颜色而不是中心点的颜色。 在光线追踪中，我们的计算原语是计算屏幕上某个点的颜色。 如果我们对像素上的许多点进行平均，我们就接近真实的平均值。 如果围绕像素的屏幕坐标是 $[i, i + 1] × [j, j + 1]$，那么我们可以替换循环：

> for each pixel (i, j) do
> 	c_{ij} = ray-color(i + 0.5, j + 0.5)  

with code that samples on a regular n × n grid of samples within each pixel: 
使用在每个像素内的规则 n × n 样本网格上进行采样的代码：

> for each pixel (i, j) do
> 	c = 0
> 	for p = 0 to n - 1 do
> 		for q = 0 to n - 1 do
> 			c = c + ray-color(i + (p + 0.5)/n, j + (q + 0.5)/n)
> 	$c_{ij} = c/n^2$  

![Figure 13.8](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.8.png)
Figure 13.8. A simple scene rendered with one sample per pixel (lower left half) and nine samples per pixel (upper right half).
图 13.8。 一个简单的场景，每个像素一个样本（左下半部分）和每个像素九个样本（右上半部分)渲染。

This is usually called regular sampling. The 16 sample locations in a pixel for $n = 4$ are shown in Figure 13.9. Note that this produces the same answer as rendering a traditional ray-traced image with one sample per pixel at $n_xn$ by $n_yn$ resolution and then averaging blocks of n by n pixels to get a $n_x$ by $n_y$ image.
这通常称为定期抽样。 $n = 4$ 的像素中的 16 个样本位置如图 13.9 所示。 请注意，这与以 $n_xn$ x $n_yn$ 分辨率渲染每个像素一个样本的传统光线追踪图像相同，然后对 n x n 像素块进行平均以获得 $n_x$ x $n_y$ 图像。
![Figure 13.9](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.9.png)
Figure 13.9. Sixteen regular samples for a single pixel. 
图 13.9。 单个像素的十六个常规样本。

One potential problem with taking samples in a regular pattern within a pixel is that regular artifacts such as moiré patterns can arise. These artifacts can be turned into noise by taking samples in a random pattern within each pixel as shown in Figure 13.10. This is usually called random sampling and involves just a small change to the code:
在像素内以规则图案采样的一个潜在问题是可能会出现规则伪像，例如莫尔图案。 通过在每个像素内以随机模式采样，这些伪影可以变成噪声，如图 13.10 所示。 这通常称为随机采样，只需要对代码进行很小的更改：

> for each pixel (i, j) do
> 	c = 0
> 	for p = 1 to $n^2$ do
> 		c = c+ ray-color(i + ξ, j + ξ)
> 	$c_{ij} = c/n^2$ 

![Figure 13.10](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.10.png)
Figure 13.10. Sixteen random samples for a single pixel.
图 13.10。 单个像素的十六个随机样本。

Here ξ is a call that returns a uniform random number in the range $[0, 1)$. Unfortunately, the noise can be quite objectionable unless many samples are taken. A compromise is to make a hybrid strategy that randomly perturbs a regular grid:
这里 Ψ 是一个返回 $[0, 1)$ 范围内的均匀随机数的调用。 不幸的是，除非采集大量样本，否则噪声可能会非常令人讨厌。 一种折衷方案是制定一种随机扰动规则网格的混合策略：

> for each pixel (i, j) do
> 	c = 0
> 	for p = 0 to n - 1 do
> 		for q = 0 to n - 1 do
> 			c = c + ray-color(i + (p + ξ)/n, j + (q + ξ)/n)
> 	$c_{ij} = c/n^2$

That method is usually called jittering or stratified sampling (Figure 13.11). 
该方法通常称为抖动或分层采样（图 13.11）。
![Figure 13.11](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.11.png)
Figure 13.11. Sixteen stratified (jittered) samples for a single pixel shown with and without the bins highlighted. There is exactly one random sample taken within each bin.
图 13.11。 单个像素的十六个分层（抖动)样本显示有和没有突出显示的垃圾箱。 每个箱内仅抽取一个随机样本。

### 13.4.2 Soft Shadows 软阴影

The reason shadows are hard to handle in standard ray tracing is that lights are infinitesimal points or directions and are thus either visible or invisible. In real life, lights have nonzero area and can thus be partially visible. This idea is shown in 2D in Figure 13.12. The region where the light is entirely invisible is called the umbra. The partially visible region is called the penumbra. There is not a commonly used term for the region not in shadow, but it is sometimes called the anti-umbra.
在标准光线追踪中阴影难以处理的原因是灯光是无限小的点或方向，因此要么可见，要么不可见。 在现实生活中，灯光具有非零面积，因此可以部分可见。 这个想法在图 13.12 中以 2D 形式显示。 光完全不可见的区域称为本影。 部分可见的区域称为半影。 对于不在阴影中的区域没有常用的术语，但它有时被称为反本影。
![Figure 13.12](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.12.png)
Figure 13.12. A soft shadow has a gradual transition from the unshadowed to shadowed region. The transition zone is the “penumbra” denoted by $p$ in the figure.
图 13.12。 软阴影从非阴影区域逐渐过渡到阴影区域。 过渡区就是图中用$p$表示的“半影”。

The key to implementing soft shadows is to somehow account for the light being an area rather than a point. An easy way to do this is to approximate the light with a distributed set of N point lights each with one Nth of the intensity of the base light. This concept is illustrated at the left of Figure 13.13 where nine lights are used. You can do this in a standard ray tracer, and it is a common trick to get soft shadows in an off-the-shelf renderer. There are two potential problems with this technique. First, typically dozens of point lights are needed to achieve visually smooth results, which slows down the program a great deal. The second problem is that the shadows have sharp transitions inside the penumbra.
实现软阴影的关键是以某种方式将光视为一个区域而不是一个点。 实现此目的的一种简单方法是使用一组分布的 N 个点光源来近似光源，每个点光源的强度为基础光源的 N 分之一。 这个概念如图 13.13 左侧所示，其中使用了九个灯。 您可以在标准光线追踪器中执行此操作，并且在现成的渲染器中获得柔和阴影是一种常见的技巧。 这种技术有两个潜在的问题。 首先，通常需要数十个点光源才能获得视觉上平滑的结果，这会大大减慢程序速度。 第二个问题是阴影在半影内有急剧的过渡。
![Figure 13.13](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.13.png)
Figure 13.13. Left: an area light can be approximated by some number of point lights; four of the nine points are visible to $\bold{p}$ so it is in the penumbra. Right: a random point on the light is chosen for the shadow ray, and it has some chance of hitting the light or not.
图 13.13。 左：区域光可以用一定数量的点光源来近似； 九个点中的四个对 $\bold{p}$ 可见，因此位于半影中。 右：为阴影光线选择灯光上的随机点，并且它有一定的机会击中或不击中灯光。

Distribution ray tracing introduces a small change in the shadowing code. Instead of representing the area light at a discrete number of point sources, we represent it as an infinite number and choose one at random for each viewing ray. This amounts to choosing a random point on the light for any surface point being lit as is shown at the right of Figure 13.13.
分布光线追踪在阴影代码中引入了一个小变化。 我们不是将区域光表示为离散数量的点光源，而是将其表示为无限数量，并为每条观察光线随机选择一个。 这相当于为任何被照亮的表面点选择灯光上的随机点，如图 13.13 右侧所示。

If the light is a parallelogram specified by a corner point $\bold{c}$ and two edge vectors $\bold{a}$ and $\bold{b}$ (Figure 13.14), then choosing a random point $\bold{r}$ is straightforward:
如果光线是由角点 $\bold{c}$ 和两个边缘向量 $\bold{a}$ 和 $\bold{b}$ 指定的平行四边形（图 13.14），则选择一个随机点 $\bold {r}$ 很简单：
$\bold{r} = \bold{c} + ξ_1\bold{a} + ξ_2\bold{b},  $
where $ξ_1$ and $ξ_2$ are uniform random numbers in the range [0, 1). 
其中$ξ_1$和$ξ_2$是[0, 1)范围内的均匀随机数。
![Figure 13.14](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.14.png)
Figure 13.14. The geometry of a parallelogram light specified by a corner point and two edge vectors.
图 13.14。 由角点和两个边缘向量指定的平行四边形光的几何形状。

We then send a shadow ray to this point as shown at the right in Figure 13.13. Note that the direction of this ray is not unit length, which may require some modification to your basic ray tracer depending upon its assumptions. 
然后我们向该点发送阴影射线，如图 13.13 右侧所示。 请注意，该光线的方向不是单位长度，这可能需要根据其假设对基本光线追踪器进行一些修改。

We would really like to jitter points on the light. However, it can be dangerous to implement this without some thought. We would not want to always have the ray in the upper left-hand corner of the pixel generate a shadow ray to the upper left-hand corner of the light. Instead we would like to scramble the samples, such that the pixel samples and the light samples are each themselves jittered, but so that there is no correlation between pixel samples and light samples. A good way to accomplish this is to generate two distinct sets of $n^2$ jittered samples and pass samples into the light source routine:
我们真的很想在灯光上抖动点。 然而，不经过深思熟虑就实施这一点可能会很危险。 我们不希望像素左上角的光线始终生成到光源左上角的阴影光线。 相反，我们想对样本进行置乱，使得像素样本和光样本本身都抖动，但像素样本和光样本之间不存在相关性。 实现此目的的一个好方法是生成两组不同的 $n^2$ 抖动样本并将样本传递到光源例程中：

> for each pixel (i, j) do
> 	c = 0
> 	generate $N = n^2$ jittered 2D points and store in array r[ ]
> 	generate $N = n^2$ jittered 2D points and store in array s[ ]
> 	shuffle the points in array s[ ]
> 	for p = 0 to N - 1 do
> 		c = c + ray-color(i + r[p].x(), j + r[p].y(), s[p])
> 	$c_{ij} = c/N$

This shuffle routine eliminates any coherence between arrays $r$ and $s$. The shadow routine will just use the 2D random point stored in s[p] rather than calling the random number generator. A shuffle routine for an array indexed from 0 to N − 1 is:
这个随机例程消除了数组 $r$ 和 $s$ 之间的任何一致性。 影子例程将仅使用存储在 s[p] 中的 2D 随机点，而不是调用随机数生成器。 索引从 0 到 N − 1 的数组的洗牌例程是：

> for i = N - 1 downto 1 do
> 	choose random integer j between 0 and i inclusive
> 	swap array elements i and j  

### 13.4.3 Depth of Field 景深

The soft focus effects seen in most photos can be simulated by collecting light at a nonzero size “lens” rather than at a point. This is called depth of field. The lens collects light from a cone of directions that has its apex at a distance where everything is in focus (Figure 13.15). We can place the “window” we are sampling on the plane where everything is in focus (rather than at the $z = n$ plane as we did previously) and the lens at the eye. The distance to the plane where everything is in focus we call the focus plane, and the distance to it is set by the user, just as the distance to the focus plane in a real camera is set by the user or range finder.
大多数照片中看到的柔焦效果可以通过在非零尺寸“镜头”而不是在一个点收集光线来模拟。 这称为景深。 透镜从一个方向锥收集光线，该锥的顶点位于所有物体都聚焦的距离处（图 13.15）。 我们可以将采样的“窗口”放置在一切都聚焦的平面上（而不是像我们之前那样放置在 $z = n$ 平面上）并将晶状体放置在眼睛上。 到一切都聚焦的平面的距离我们称为焦平面，到它的距离由用户设置，就像真实相机中到焦平面的距离由用户或测距仪设置一样。
![Figure 13.15](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.15.png)
Figure 13.15. The lens averages over a cone of directions that hit the pixel location being sampled.
图 13.15。 镜头对撞击正在采样的像素位置的方向锥进行平均。

To be most faithful to a real camera, we should make the lens a disk. However, we will get very similar effects with a square lens (Figure 13.16). So we choose the side-length of the lens and take random samples on it. The origin of the view rays will be these perturbed positions rather than the eye position. Again, a shuffling routine is used to prevent correlation with the pixel sample positions. An example using 25 samples per pixel and a large disk lens is shown in Figure 13.17.
为了最忠实于真实的相机，我们应该将镜头做成圆盘。 然而，使用方形透镜我们会得到非常相似的效果（图 13.16）。 因此，我们选择透镜的边长并对其进行随机采样。 视线的来源将是这些扰动的位置而不是眼睛的位置。 再次，使用改组例程来防止与像素样本位置的相关性。 图 13.17 显示了使用每像素 25 个样本和大圆盘透镜的示例。
![Figure 13.16](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.16.png)
Figure 13.16. To create depth-of-field effects, the eye is randomly selected from a square region.
图 13.16。 为了创建景深效果，眼睛是从方形区域中随机选择的。
![Figure 13.17](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.17.png)
Figure 13.17. An example of depth of field. The caustic in the shadow of the wine glass is computed using particle tracing as described in Chapter 23. 
图 13.17。 景深的示例。 酒杯阴影中的焦散度是使用第 23 章中所述的粒子追踪来计算的。

### 13.4.4 Glossy Reflection 光泽反射

Some surfaces, such as brushed metal, are somewhere between an ideal mirror and a diffuse surface. Some discernible image is visible in the reflection, but it is blurred. We can simulate this by randomly perturbing ideal specular reflection rays as shown in Figure 13.18.
某些表面（例如拉丝金属）介于理想镜面和漫射表面之间。 反射中可以看到一些可辨别的图像，但它是模糊的。 我们可以通过随机扰动理想镜面反射光线来模拟这一点，如图 13.18 所示。
![Figure 13.18](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.18.png)
Figure 13.18. The reflection ray is perturbed to a random vector $\bold{r}'$.
图 13.18。 反射光线受到随机向量 $\bold{r}'$ 的扰动。

Only two details need to be worked out: how to choose the vector $\bold{r}'$ and what to do when the resulting perturbed ray is below the surface from which the ray is reflected. The latter detail is usually settled by returning a zero color when the ray is below the surface.
只需要解决两个细节：如何选择向量 $\bold{r}'$ 以及当产生的扰动光线低于反射光线的表面时该怎么办。 当光线低于表面时，后一个细节通常通过返回零颜色来解决。

To choose $r'$, we again sample a random square. This square is perpendicular to $\bold{r}$ and has width a which controls the degree of blur. We can set up the square’s orientation by creating an orthonormal basis with $\bold{w} = \bold{r}$ using the techniques in Section 2.4.6. Then, we create a random point in the 2D square with side length a centered at the origin. If we have 2D sample points $(ξ, ξ') ∈ [0, 1]^2$, then the analogous point on the desired square is
为了选择 $r'$，我们再次对随机正方形进行采样。 这个正方形垂直于$\bold{r}$，宽度a控制模糊程度。 我们可以使用第 2.4.6 节中的技术通过 $\bold{w} = \bold{r}$ 创建正交基来设置正方形的方向。 然后，我们在 2D 正方形中创建一个边长为 a、以原点为中心的随机点。 如果我们有 2D 样本点 $(ξ, ξ') ∈ [0, 1]^2$，那么所需正方形上的类似点是
$$
u = -\frac{a}{2} + ξa, \\
v = −\frac{a}{2} + ξ'a.
$$
Because the square over which we will perturb is parallel to both the $\bold{u}$ and $\bold{v}$ vectors, the ray $\bold{r}'$ is just
因为我们要扰动的正方形与 $\bold{u}$ 和 $\bold{v}$ 向量平行，所以射线 $\bold{r}'$ 只是
$\bold{r}' = \bold{r }+ u\bold{u} + v\bold{v}.  $

Note that $\bold{r}'$ is not necessarily a unit vector and should be normalized if your code requires that for ray directions.
请注意，$\bold{r}'$ 不一定是单位向量，如果您的代码需要射线方向，则应对其进行归一化。

### 13.4.5 Motion Blur 运动模糊

We can add a blurred appearance to objects as shown in Figure 13.19. This is called motion blur and is the result of the image being formed over a nonzero span of time. In a real camera, the aperture is open for some time interval during which objects move. We can simulate the open aperture by setting a time variable ranging from $T_0$ to $T_1$. For each viewing ray we choose a random time,
我们可以为对象添加模糊外观，如图 13.19 所示。 这称为运动模糊，是在非零时间跨度内形成图像的结果。 在真实相机中，光圈会打开一段时间间隔，在此期间物体会移动。 我们可以通过设置范围从 $T_0$ 到 $T_1$ 的时间变量来模拟开放孔径。 对于每条观察光线，我们选择一个随机时间，
$T = T_0 + ξ(T_1 - T_0).  $

We may also need to create some objects to move with time. For example, we might have a moving sphere whose center travels from $\bold{c}_0$ to $\bold{c}_1$ during the interval. Given $T$ , we could compute the actual center and do a ray–intersection with that sphere. Because each ray is sent at a different time, each will encounter the sphere at a different position, and the final appearance will be blurred. Note that the bounding box for the moving sphere should bound its entire path so an efficiency structure can be built for the whole time interval (Glassner, 1988).
我们可能还需要创建一些随时间移动的对象。 例如，我们可能有一个移动球体，其中心在间隔期间从 $\bold{c}_0$ 移动到 $\bold{c}_1$。 给定 $T$ ，我们可以计算实际中心并与该球体进行射线相交。 由于每条光线在不同的时间发送，每条光线都会在不同的位置遇到球体，最终的外观会变得模糊。 请注意，移动球体的边界框应限制其整个路径，以便可以为整个时间间隔构建效率结构（Glassner，1988）。
![Figure 13.19](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 13.19.png)
Figure 13.19. The bottom right sphere is in motion, and a blurred appearance results. Image courtesy Chad Barb.
图 13.19。 右下角的球体在运动，并产生模糊的外观。 图片由查德·巴布提供。

## Notes 注释

There are many, many other advanced methods that can be implemented in the ray-tracing framework. Some resources for further information are Glassner’s An Introduction to Ray Tracing and Principles of Digital Image Synthesis, Shirley’s Realistic Ray Tracing, and Pharr and Humphreys’s Physically Based Rendering: From Theory to Implementation.
还有很多很多其他高级方法可以在光线追踪框架中实现。 有关更多信息的一些资源包括 Glassner 的《光线追踪和数字图像合成原理简介》、Shirley 的《真实光线追踪》以及 Pharr 和 Humphreys 的《基于物理的渲染：从理论到实现》。

## Frequently Asked Questions 经常问的问题

### What is the best ray-intersection efficiency structure? 最佳光线相交效率结构是什么？

The most popular structures are binary space partitioning trees (BSP trees), uniform subdivision grids, and bounding volume hierarchies. Most people who use BSP trees make the splitting planes axis-aligned, and such trees are usually called k-d trees. There is no clear-cut answer for which is best, but all are much, much better than brute-force search in practice. If I were to implement only one, it would be the bounding volume hierarchy because of its simplicity and robustness.
最流行的结构是二元空间划分树（BSP 树）、均匀细分网格和包围体层次结构。 大多数使用 BSP 树的人都使分裂平面轴对齐，这种树通常称为 k-d 树。 对于哪一个最好没有明确的答案，但在实践中，所有这些都比暴力搜索要好得多。 如果我只实现一个，那就是包围体层次结构，因为它简单且稳健。

### Why do people use bounding boxes rather than spheres or ellipsoids? 为什么人们使用边界框而不是球体或椭球体？

Sometimes spheres or ellipsoids are better. However, many models have polygonal elements that are tightly bounded by boxes, but they would be difficult to tightly bind with an ellipsoid.
有时球体或椭球体更好。 然而，许多模型都具有由盒子紧密包围的多边形元素，但它们很难与椭球体紧密束缚。