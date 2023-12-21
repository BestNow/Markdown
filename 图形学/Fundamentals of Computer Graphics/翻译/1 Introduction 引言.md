# 1 Introduction 引言

The term computer graphics describes any use of computers to create and manipulate images. This book introduces the algorithmic and mathematical tools that can be used to create all kinds of images—realistic visual effects, informative technical illustrations, or beautiful computer animations. Graphics can be two- or three-dimensional; images can be completely synthetic or can be produced by manipulating photographs. This book is about the fundamental algorithms and mathematics, especially those used to produce synthetic images of three-dimensional objects and scenes.
计算机图形学一词描述了计算机用于创建和操作图像的任何用途。本书介绍了可用于创建各种图像（逼真的视觉效果、信息丰富的技术插图或美丽的计算机动画）的算法和数学工具。图形可以是二维或三维的；图像可以是完全合成的，也可以是通过操作照片生成的。本书介绍了基本算法和数学，特别是用于生成三维物体和场景的合成图像的算法和数学。

Actually doing computer graphics inevitably requires knowing about specific hardware, file formats, and usually a graphics API(API: application program interface.) (see Section 1.3) or two. Computer graphics is a rapidly evolving field, so the specifics of that knowledge are a moving target. Therefore, in this book we do our best to avoid depending on any specific hardware or API. Readers are encouraged to supplement the text with relevant documentation for their software and hardware environment. Fortunately, the culture of computer graphics has enough standard terminology and concepts that the discussion in this book should map nicely to most environments.
实际进行计算机图形学不可避免地需要了解特定的硬件、文件格式以及通常是一个或两个图形API（参见第1.3节）。计算机图形学是一个快速发展的领域，因此这些知识的具体内容是一个不断变化的目标。因此，在本书中，我们尽力避免依赖于任何特定的硬件或API。鼓励读者使用与其软件和硬件环境相关的文档来补充本文。幸运的是，计算机图形学的文化具有足够的标准术语和概念，使得本书中的讨论应该能够很好地映射到大多数环境中。

This chapter defines some basic terminology and provides some historical background, as well as information sources related to computer graphics.
本章定义了一些基本术语，并提供了一些历史背景以及与计算机图形学相关的信息来源。

## 1.1 Graphics Areas 图形学领域

Imposing categories on any field is dangerous, but most graphics practitioners would agree on the following major areas of computer graphics:
对任何领域进行分类都是危险的，但大多数图形学从业者都会同意计算机图形学的以下主要领域：

- **Modeling** deals with the mathematical specification of shape and appearance properties in a way that can be stored on the computer. For example a coffee mug might be described as a set of ordered 3D points along with some interpolation rule to connect the points and a reflection model that describes how light interacts with the mug.
  **建模**处理以数学方式规定形状和外观属性，以便可以存储在计算机上。例如，咖啡杯可以描述为一组有序的3D点，以及一些插值规则来连接这些点和描述光如何与杯子交互的反射模型。
- **Rendering** is a term inherited from art and deals with the creation of shaded images from 3D computer models.
  **渲染**是从艺术中继承的术语，用于从3D计算机模型创建阴影图像。
- **Animation** is a technique to create an illusion of motion through sequences of images. Animation uses modeling and rendering but adds the key issue of movement over time, which is not usually dealt with in basic modeling and rendering.
  **动画**是一种通过图像序列创建运动幻觉的技术。动画使用建模和渲染，但增加了关键的随时间移动问题，这通常不在基本建模和渲染中处理。

There are many other areas that involve computer graphics, and whether they are core graphics areas is a matter of opinion. These will all be at least touched on in the text. Such related areas include the following:
计算机图形学涉及许多其他领域，它们是否是核心图形学领域是一个有争议的问题。这些领域都至少会在本文中提到。这些相关领域包括：

- **User interaction** deals with the interface between input devices such as mice and tablets, the application, feedback to the user in imagery, and other sensory feedback. Historically, this area is associated with graphics largely because graphics researchers had some of the earliest access to the input/out-put devices that are now ubiquitous.
  **用户交互**处理输入设备（如鼠标和平板电脑）、应用程序、反馈给用户的图像以及其他感官反馈之间的接口。从历史上看，这个领域与图形学有很大的关联，因为图形学研究人员最早可以使用现在无处不在的输入/输出设备。
- **Virtual reality** attempts to immerse the user into a 3D virtual world. This typically requires at least stereo graphics and response to head motion. For true virtual reality, sound and force feedback should be provided as well. Because this area requires advanced 3D graphics and advanced display technology, it is often closely associated with graphics.
  **虚拟现实**试图将用户沉浸在3D虚拟世界中。这通常需要至少立体声图形和对头部运动的响应。对于真正的虚拟现实，还应该提供声音和力反馈。因为这个领域需要先进的3D图形和先进的显示技术，所以它经常与图形学密切相关。
- **Visualization** attempts to give users insight into complex information via visual display. Often there are graphic issues to be addressed in a visualization problem.
  **可视化**试图通过视觉显示向用户提供复杂信息的洞察力。通常在可视化问题中需要解决图形问题。
- **Image processing** deals with the manipulation of 2D images and is used in both the fields of graphics and vision.
  **图像处理**处理2D图像的操作，用于图形学和视觉领域。
- **3D scanning** uses range-finding technology to create measured 3D models. Such models are useful for creating rich visual imagery, and the processing of such models often requires graphics algorithms.
  **3D扫描**使用测距技术创建测量的3D模型。这样的模型对于创建丰富的视觉图像非常有用，处理这样的模型通常需要图形算法。
- **Computational photography** is the use of computer graphics, computer vision, and image processing methods to enable new ways of photographically capturing objects, scenes, and environments.
  **计算摄影**是使用计算机图形学、计算机视觉和图像处理方法，以实现以新的方式摄影捕捉对象、场景和环境。



## 1.2 Major Applications 主要应用

Almost any endeavor can make some use of computer graphics, but the major consumers of computer graphics technology include the following industries:
几乎任何事业都可以利用计算机图形学，但计算机图形学技术的主要消费者包括以下行业：

- **Video games** increasingly use sophisticated 3D models and rendering algorithms.
  **视频游戏**越来越多地使用复杂的3D模型和渲染算法。
- **Cartoons** are often rendered directly from 3D models. Many traditional2D cartoons use backgrounds rendered from 3D models, which allow a continuously moving viewpoint without huge amounts of artist time.
  **卡通**通常直接从3D模型渲染。许多传统的2D卡通使用从3D模型渲染的背景，这允许连续移动视点而不需要大量的艺术家时间。
- **Visual effects** use almost all types of computer graphics technology. Almost every modern film uses digital compositing to superimpose backgrounds with separately filmed foregrounds. Many films also use 3D modeling and animation to create synthetic environments, objects, and even characters that most viewers will never suspect are not real.
  **视觉效果**使用几乎所有类型的计算机图形学技术。几乎每一部现代电影都使用数字合成将背景与单独拍摄的前景叠加在一起。许多电影还使用3D建模和动画来创建合成环境、物体，甚至是大多数观众永远不会怀疑的角色。
- **Animated films** use many of the same techniques that are used for visual effects, but without necessarily aiming for images that look real.
  **动画电影**使用许多与视觉效果相同的技术，但不一定旨在制作看起来真实的图像。
- **CAD/CAM** stands for computer-aided design and computer-aided manufacturing. These fields use computer technology to design parts and products on the computer and then, using these virtual designs, to guide the manufacturing process. For example, many mechanical parts are designed in a 3D computer modeling package and then automatically produced on a computer-controlled milling device.
  **CAD/CAM**是计算机辅助设计和计算机辅助制造的缩写。这些领域使用计算机技术在计算机上设计零件和产品，然后使用这些虚拟设计来指导制造过程。例如，许多机械零件是在3D计算机建模软件中设计的，然后在计算机控制的铣床上自动生产。
- **Simulation** can be thought of as accurate video gaming. For example, a flight simulator uses sophisticated 3D graphics to simulate the experience of flying an airplane. Such simulations can be extremely useful for initial training in safety-critical domains such as driving, and for scenario training for experienced users such as specific fire-fighting situations that are too costly or dangerous to create physically.
  **模拟**可以被认为是准确的视频游戏。例如，飞行模拟器使用复杂的3D图形来模拟飞行飞机的体验。这样的模拟对于安全关键领域（如驾驶）的初步培训以及对于经验丰富的用户（如特定的消防情况）的情景培训非常有用，这些情况在物理上过于昂贵或危险。
- **Medical imaging** creates meaningful images of scanned patient data. For example, a computed tomography (CT) dataset is composed of a large 3D rectangular array of density values. Computer graphics is used to create shaded images that help doctors extract the most salient information from such data.
  **医学成像**创建有意义的扫描患者数据的图像。例如，计算机断层扫描（CT）数据集由大量的3D矩形密度值数组组成。计算机图形学用于创建着色图像，以帮助医生从这些数据中提取最重要的信息。
- **Information visualization** creates images of data that do not necessarily have a “natural’ visual depiction. For example, the temporal trend of the price of ten different stocks does not have an obvious visual depiction, but clever graphing techniques can help humans see the patterns in such data.
  **信息可视化**创建数据的图像，这些数据不一定具有“自然”的视觉描述。例如，十种不同股票价格的时间趋势没有明显的视觉描述，但巧妙的绘图技术可以帮助人们看到这些数据中的模式。

## 1.3 Graphics APIs 图形API

A key part of using graphics libraries is dealing with a graphics API. An application program interface (API) is a standard collection of functions to perform a set of related operations, and a graphics API is a set of functions that perform basic operations such as drawing images and 3D surfaces into windows on the screen. 
使用图形库的关键部分是处理图形API。应用程序编程接口（API）是一组标准函数，用于执行一组相关操作，图形API是一组函数，用于在屏幕上的窗口中绘制图像和3D表面等基本操作。

Every graphics program needs to be able to use two related APIs: a graphics API for visual output and a user-interface API to get input from the user. There are currently two dominant paradigms for graphics and user-interface APIs. The first is the integrated approach, exemplified by Java, where the graphics and user interface toolkits are integrated and portable packages that are fully standardized and supported as part of the language. The second is represented by Direct3Dand OpenGL, where the drawing commands are part of a software library tied toa language such as C++, and the user-interface software is an independent entity that might vary from system to system. In this latter approach, it is problematic to write portable code, although for simple programs it may be possible to use a portable library layer to encapsulate the system specific user-interface code. 
每个图形程序都需要能够使用两个相关的API：用于视觉输出的图形API和用于从用户获取输入的用户界面API。目前有两种主要的图形和用户界面API范例。第一种是**集成方法**，例如Java，其中图形和用户界面工具包是集成和可移植的包，完全标准化并作为语言的一部分得到支持。第二种是由Direct3D和OpenGL代表的方法，其中绘图命令是与诸如C++之类的语言**绑定的软件库的一部分**，用户界面软件是一个独立的实体，可能因系统而异。在后一种方法中，编写可移植代码存在问题，尽管对于简单的程序，可能可以使用可移植库层来封装特定于系统的用户界面代码。

Whatever your choice of API, the basic graphics calls will be largely the same, and the concepts of this book will apply.
无论您选择哪种API，基本的图形调用将基本相同，并且本书的概念将适用。

## 1.4 Graphics Pipeline 图形管道

Every desktop computer today has a powerful 3D graphics pipeline. This is a special software/hardware subsystem that efficiently draws 3D primitives in perspective. Usually these systems are optimized for processing 3D triangles with shared vertices. The basic operations in the pipeline map the 3D vertex locations to 2D screen positions and shade the triangles so that they both look realistic and appear in proper back-to-front order.
今天的每台台式计算机都有一个强大的3D图形管道。这是一个特殊的软件/硬件子系统，可以有效地以透视方式绘制3D基元。通常，这些系统<u>被优化为处理具有共享顶点的3D三角形</u>。管道中的基本操作将3D顶点位置映射到2D屏幕位置，并对三角形进行着色，使其既看起来逼真又按正确的前后顺序出现。

Although drawing the triangles in valid back-to-front order was once the most important research issue in computer graphics, it is now almost always solved using the z-buffer, which uses a special memory buffer to solve the problem in a brute-force manner.
虽然以有效的前后顺序绘制三角形曾经是计算机图形学中最重要的研究问题，但现在几乎总是使用**z缓冲区**来解决这个问题，z缓冲区使用特殊的内存缓冲区以蛮力方式解决问题。

It turns out that the geometric manipulation used in the graphics pipeline can be accomplished almost entirely in a 4D coordinate space composed of three traditional geometric coordinates and a fourth homogeneous coordinate that helps with perspective viewing. These 4D coordinates are manipulated using 4 x 4matrices and 4-vectors. The graphics pipeline, therefore, contains much machinery for efficiently processing and composing such matrices and vectors. This4D coordinate system is one of the most subtle and beautiful constructs used in computer science, and it is certainly the biggest intellectual hurdle to jump when learning computer graphics. A big chunk of the first part of every graphics book deals with these coordinates.
事实证明，图形管道中使用的几何操作几乎可以完全在由三个传统几何坐标和第四个用于透视视图的齐次坐标组成的4D坐标空间中完成。这些4D坐标使用4 x 4矩阵和4向量进行操作。因此，图形管道包含了大量的机制，用于高效地处理和组合这些矩阵和向量。这个4D坐标系统是计算机科学中使用的最微妙和最美丽的构造之一，也是学习计算机图形学时最大的知识难点。每本图形书的第一部分都涉及这些坐标。

The speed at which images can be generated depends strongly on the number of triangles being drawn. Because interactivity is more important in many applications than visual quality, it is worthwhile to minimize the number of triangles used to represent a model. In addition, if the model is viewed in the distance, fewer triangles are needed than when the model is viewed from a closer distance. This suggests that it is useful to represent a model with a varying level of detail(LOD).
图形生成速度取决于绘制的三角形数量。因为在许多应用程序中，交互性比视觉质量更重要，所以值得将用于表示模型的三角形数量最小化。此外，如果从远处查看模型，则需要的三角形数量比从较近距离查看模型时少。这表明，使用不同的细节级别（LOD）表示模型是有用的。

## 1.5 Numerical Issues 数值问题

Many graphics programs are really just 3D numerical codes. Numerical issues are often crucial in such programs. In the "old days", it was very difficult to handle such issues in a robust and portable manner because machines had different internal representations for numbers, and even worse, handled exceptions in different and incompatible ways. Fortunately, almost all modern computers conform to the IEEE floating-point standard (IEEE Standards Association, 1985). This al-lows the programmer to make many convenient assumptions about how certain numeric conditions will be handled.
许多图形程序实际上只是3D数值代码。在这些程序中，数值问题通常至关重要。在过去，由于计算机具有不同的数字内部表示方式，而且更糟糕的是，处理异常的方式也不同且不兼容，因此很难以强大和可移植的方式处理这些问题。幸运的是，几乎所有现代计算机都符合IEEE浮点标准（IEEE Standards Association，1985年）。这使得程序员可以对某些数字条件的处理方式做出许多方便的假设。

Although IEEE floating-point has many features that are valuable when coding numeric algorithms, there are only a few that are crucial to know for most situations encountered in graphics. First, and most important, is to understand that there are three "special" values for real numbers in IEEE floating-point:
虽然IEEE浮点具有许多编写数字算法时有价值的功能，但在图形学中遇到的大多数情况下，只有少数功能是至关重要的。首先，也是最重要的是要了解IEEE浮点中有三个实数的"特殊"值：

1. Infinity ($\infty$). This is a valid number that is larger than all other valid numbers.
   无穷大($\infty$)。这是一个大于所有其他有效数字的有效数字
2. Minus infinity ($-\infty$). This is a valid number that is smaller than all other valid numbers.
   负无穷大($-\infty$)。这是一个小于所有其他有效数字的有效数字。
3. Not a number (NaN). This is an invalid number that arises from an operation with undefined consequences, such as zero divided by zero.
   非数字(NaN)。这是一个无效数字，由于具有未定义后果的操作（例如零除以零）而产生。

The designers of IEEE floating-point made some decisions that are extremely convenient for programmers. Many of these relate to the three special values above in handling exceptions such as division by zero. In these cases an exception is logged, but in many cases the programmer can ignore that. Specifically, for any positive real number a, the following rules involving division by infinite values hold:
IEEE浮点数的设计者们做出了一些对程序员非常方便的决策。其中许多与处理诸如除以零等异常情况时上述三个特殊值有关。在这些情况下，会记录异常，但在许多情况下，程序员可以忽略它。具体而言，对于任何正实数a，涉及除以无穷大值的规则如下：
$$
+a / (+\infin) = +0 \\
-a / (+\infin) = -0 \\
+a / (-\infin) = -0 \\
-a / (-\infin) = +0 \\
$$

> IEEE floating-point has two representations for zero, one that is treated as positive and one that is treated as negative. The distinction between –0 and +0 only occasionally matters, but it is worth keeping in mind for those occasions when it does. 
> IEEE浮点数有两种表示0的方式，一种是正的，一种是负的。-0和+0之间的区别只是偶尔重要，但在这种情况下值得记住。

Other operations involving infinite values behave the way one would expect. Again for positive a, the behavior is as follows:
“涉及无穷大值的其他操作”表现出人们所期望的行为。同样，对于正实数a，其行为如下：
$$
\infin + \infin = + \infin \\
\infin - \infin = NaN \\
\infin \cross \infin = \infin \\ 
\infin / \infin = NaN \\
\infin / a = \infin \\
\infin / 0 = \infin \\
0 / 0 = NaN \\
$$
The rules in a Boolean expression involving infinite values are as expected:
包含无限值的布尔表达式中的规则如预期的那样:

1. All finite valid numbers are less than $+\infin$.
   所有有限有效数都小于$+\infin$。
2. All finite valid numbers are greater than $-\infin$.
   所有有限有效数字都大于$-\infin$。
3. $-\infin$ is less than $+\infin$.
   $-\infin$小于$+\infin$。

The rules involving expressions that have NaN values are simple:
包含NaN值的表达式的规则很简单:

1. Any arithmetic expression that includes NaN results in NaN
   任何包含NaN的算术表达式的结果都是NaN
2. Any Boolean expression involving NaN is false.
   任何涉及NaN的布尔表达式都为假

Perhaps the most useful aspect of IEEE floating-point is how divide-by-zero is handled; for any positive real number a, the following rules involving division by zero values hold:
也许IEEE浮点最有用的方面是如何处理除零；对于任意正实数a，除0的规则如下:
$$
+a / +0 = +\infin \\
-a / +0 = -\infin \\
$$

> Some care must be taken if negative zero (-0) might arise.
> 如果可能出现负零(-0)，必须小心。

There are many numeric computations that become much simpler if the programmer takes advantage of the IEEE rules. For example, consider the expression:
如果程序员利用IEEE规则，许多数值计算将变得简单得多。例如，考虑这个表达式:
$$
a = \frac{1}{\frac{1}{b} + \frac{1}{c}}
$$
Such expressions arise with resistors and lenses. If divide-by-zero resulted in a program crash (as was true in many systems before IEEE floating-point), then two if statements would be required to check for small or zero values of b or c. Instead, with IEEE floating-point, if b or c is zero, we will get a zero value for a as desired. Another common technique to avoid special checks is to take advantage of the Boolean properties of NaN. Consider the following code segment:
这样的表达式出现在电阻器和透镜中。如果除以零导致程序崩溃（在IEEE浮点数之前的许多系统中是真实的），那么需要两个if语句来检查b或c的小值或零值。相反，使用IEEE浮点数，如果b或c为零，则我们将获得所需的零值a。另一种避免特殊检查的常见技术是利用NaN的布尔属性。请考虑以下代码段：

```lua
a = f(x)
if (a > 0) then
	do_something
```

Here, the function f may return “ugly" values such as $\infin$ or NaN, but the if condition is still well-defined: it is false for a = NaN or a = $-\infin$ and true for a = $+\infin$. With care in deciding which values are returned, often the if can make the right choice, with no special checks needed. This makes programs smaller, more robust. and more efficient.
这里，函数f可能会返回“丑陋”的值，例如$\infin$或NaN，但if条件仍然是明确定义的：当a = NaN或a = $-\infin$时，它为false，当a = $+\infin$时，它为true。通过仔细决定返回哪些值，if通常可以做出正确的选择，而无需进行特殊检查。这使得程序更小、更健壮、更高效。

## 1.6 Efficiency 效率

There are no magic rules for making code more efficient. Efficiency is achieved through careful tradeoffs, and these tradeoffs are different for different architectures. However, for the foreseeable future, a good heuristic is that programmers should pay more attention to memory access patterns than to operation counts. This is the opposite of the best heuristic of two decades ago. This switch has occurred because the speed of memory has not kept pace with the speed of processors. Since that trend continues, the importance of limited and coherent memory access for optimization should only increase. 
没有什么神奇的规则可以使代码更加高效。通过仔细的权衡，可以实现效率，而这些权衡对于不同的架构是不同的。然而，可预见的未来，一个好的启发式是程序员应该更加关注内存访问模式而不是操作计数。这与二十年前的最佳启发式相反。这种转变是因为内存的速度没有跟上处理器的速度而发生的。由于这种趋势的持续，**有限和连贯的内存访问对于优化的重要性只会增加**。

A reasonable approach to making code fast is to proceed in the following order, taking only those steps which are needed:
提高代码运行速度的一个合理方法是按照以下顺序进行，仅采取必要的步骤：

1. Write the code in the most straightforward way possible. Compute inter-mediate results as needed on the fly rather than storing them. 
   尽可能以最直接的方式编写代码。根据需要动态地计算中间结果，而不是存储它们。
2. Compile in optimized mode.
   以优化模式编译。
3. Use whatever profiling tools exist to find critical bottlenecks
   使用现有的任何分析工具来发现关键瓶颈
4. Examine data structures to look for ways to improve locality. If possible.
   检查数据结构以寻找改进局部性的方法。如果可能的话，使数据单元大小与目标体系结构上的缓存/页面大小匹配。
5. If profiling reveals bottlenecks in numeric computations, examine the as sembly code generated by the compiler for missed efficiencies. Rewrite source code to solve any problems you find.
   如果分析揭示了数值计算中的瓶颈，请检查编译器生成的汇编代码，以查找遗漏的效率。重写源代码以解决您发现的任何问题。

The most important of these steps is the first one. Most “optimizations’ make the code harder to read without speeding things up. In addition, time spent upfront optimizing code is usually better spent correcting bugs or adding features. Also, beware of suggestions from old texts; some classic tricks such as using integers instead of reals may no longer yield speed because modern CPUs can usually perform floating-point operations just as fast as they perform integer operations. In all situations, profiling is needed to be sure of the merit of any optimization fora specific machine and compiler.
其中最重要的一步是第一步。大多数“优化”措施使代码难以阅读，而并未提高执行速度。此外，花费时间在优化代码上通常比纠正错误或添加功能更为明智。同时，要小心古老文本中的建议；一些经典技巧，比如使用整数而非实数，可能因为现代 CPU 通常能够像执行整数操作一样快速执行浮点运算，而不再带来性能提升。在任何情况下，都需要进行性能分析，以确保针对特定的机器和编译器进行的任何优化是有效的。

## 1.7 Designing and Coding Graphics Programs 设计和编码图形程序

Certain common strategies are often useful in graphics programming. In this section we provide some advice that you may find helpful as you implement the methods you learn about in this book.
某些常见的策略在图形编程中通常很有用。在本节中，我们提供了一些建议，在您实现本书中学习的方法时可能会对您有所帮助。

### 1.7.1 Class Design 类设计

A key part of any graphics program is to have good classes or routines for geometric entities such as vectors and matrices, as well as graphics entities such as RGB colors and images. These routines should be made as clean and efficient as possible. A universal design question is whether locations and displacements should be separate classes because they have different operations, e.g. , a location multiplied by one-half makes no geometric sense while one-half of a displacement does (Goldman, 1985: DeRose, 1989). There is little agreement on this question， which can spur hours of heated debate among graphics practitioners, but for the sake of example let's assume we will not make the distinction.
任何图形程序的关键部分是具备良好的类或例程，用于处理几何实体，如向量和矩阵，以及图形实体，如RGB颜色和图像。这些例程应该尽可能地简洁而高效。一个普遍的设计问题是，位置和位移是否应该是独立的类，因为它们具有不同的操作，例如，将位置乘以一半在几何上没有意义，而位移的一半却有（Goldman, 1985; DeRose, 1989）。关于这个问题，图形从业者之间意见分歧较大，可能引发数小时的激烈辩论，但为了举例，让我们假设我们不会进行这种区分。

> I believe strongly in the KISS(“keep it simple, stupid’) principle, and in that light the argument fortwo classes is not compelling enough to justify the added complexity. -PS
> 我坚信“保持简单，愚蠢”（KISS）的原则，基于这一观点，支持使用两个类的论点并不足以证明其复杂性的增加是合理的。 -PS

> I like keeping points and vectors separate because it makes code more readable and can let the compiler catch some bugs.-S.M
> 我喜欢将点和向量分开，因为这可以使代码更易读，并且可以让编译器捕捉一些错误。-S.M

This implies that some basic classes to be written include:
这意味着需要编写的一些基本类包括:

- **vector2.** A 2D vector class that stores an x- and y-component. It should store these components in a length-2 array so that an indexing operator can be well supported. You should also include operations for vector addition, vector subtraction, dot product, cross product, scalar multiplication, and scalar division.
  **vector2.** 一个2D向量类，存储x和y分量。它应该将这些分量存储在长度为2的数组中，以便支持索引运算符。您还应该包括向量加法、向量减法、点积、叉积、标量乘法和标量除法的操作。
- **vector3.** A 3D vector class analogous to vector2.
  **vector3.** 与vector2类似的3D向量类。
- **hvector.** A homogeneous vector with four components (see Chapter 7).
  **hvector.** 具有四个分量的齐次向量（请参见第7章）。
- **rgb.** An RGB color that stores three components. You should also include operations for RGB addition, RGB subtraction, RGB multiplication, scalar multiplication,and scalar division.
  **rgb.** 存储三个分量的RGB颜色。您还应该包括RGB加法、RGB减法、RGB乘法、标量乘法和标量除法的操作。
- **transform.** A 4 x 4 matrix for transformations. You should include a matrix multiply and member functions to apply to locations, directions, and surface normal vectors. As shown in Chapter 6, these are all different.
  **transform.** 用于变换的4 x 4矩阵。您应该包括矩阵乘法和成员函数，以应用于位置、方向和表面法向量。如第6章所示，这些都是不同的。
- **image.** A 2D array of RGB pixels with an output operation.
  **image.** 具有输出操作的RGB像素的2D数组。

In addition, you might or might not want to add classes for intervals, orthonormal bases, and coordinate frames.
此外，您可能会选择或不选择为区间、正交规范基和坐标框架添加类。

> You might also consider a special class for unit-length  vectors, although I have found them more pain than they are worth.-PS.
> 您可能还需要考虑为单位长度向量设计一个特殊的类，尽管我发现它们比它们的价值更痛苦。-PS。



### 1.7.2 Float vs. Double

Modern architecture suggests that keeping memory use down and maintaining coherent memory access are the keys to efficiency. This suggests using single-precision data. However, avoiding numerical problems suggests using double precision arithmetic. The tradeoffs depend on the program, but it is nice to have a default in your class definitions.
现代架构表明，保持内存使用量的控制和维护内存访问的一致性是提高效率的关键。这暗示着使用单精度数据。然而，避免数值问题则建议使用双精度算法。权衡取决于程序的特性，但在类定义中设置一个默认值是个不错的选择。

> I suggest using doubles for geometric computation and floats for color computation. For data that occupies a lot of memory, such as triangle meshes,I suggest storing float data, but con-verting to double when data is accessed through member functions.-PS.
> 我建议在几何计算中使用双精度，而在颜色计算中使用单精度。对于占用大量内存的数据，例如三角形网格，我建议存储单精度数据，但在通过成员函数访问数据时将其转换为双精度。-PS。

> I advocate doing all computations with floats until you find evidence that double precision is needed in a particular part of the code.-S.M.
> 我主张使用单精度浮点数进行所有计算，直到在代码的特定部分发现需要双精度精度的证据。-S.M。

### 1.7.3 Debugging Graphics Programs 调试图形程序

If you ask around, you may find that as programmers become more experienced,they use traditional debuggers less and less. One reason for this is that using such debuggers is more awkward for complex programs than for simple programs. Another reason is that the most difficult errors are conceptual ones where the wrong thing is being implemented, and it is easy to waste large amounts of time stepping through variable values without detecting such cases. We have found several debugging strategies to be particularly useful in graphics.
如果你询问一下，你会发现随着程序员经验的增长，他们使用传统的调试器的次数越来越少。其中一个原因是，对于复杂的程序而言，使用这样的调试器比简单的程序更加棘手。另一个原因是，最困难的错误是概念性的错误，即正在实现错误的事情，而且很容易浪费大量时间在变量值上，而没有检测到这些情况。我们发现在图形中有几种调试策略特别有用。

**The Scientific Method 科学方法**
In graphics programs there is an alternative to traditional debugging that is often very useful. The downside to it is that it is very similar to what computer programmers are taught not to do early in their careers, so you may feel “naughty”if you do it: we create an image and observe what is wrong with it. Then, we develop a hypothesis about what is causing the problem and test it. For example,in a ray-tracing program we might have many somewhat random looking dark pixels. This is the classic “shadow acne” problem that most people run into when they write a ray tracer. Traditional debugging is not helpful here; instead, we must realize that the shadow rays are hitting the surface being shaded. We might notice that the color of the dark spots is the ambient color, so the direct lighting is what is missing. Direct lighting can be turned off in shadow, so you might hypothesize that these points are incorrectly being tagged as in shadow when they are not. To test this hypothesis, we could turn off the shadowing check and recompile. This would indicate that these are false shadow tests, and we could continue our detective work. The key reason that this method can sometimes be good practice is that we never had to spot a false value or really determine our conceptual error. Instead, we just narrowed in on our conceptual error experimentally. Typically only a few trials are needed to track things down, and this type of debugging is enjoyable.
在图形程序中，有一种传统调试的替代方法通常非常有用。它的缺点在于，它与计算机程序员在职业生涯早期所学的内容非常相似，因此你可能会感到“调皮”：我们创建一幅图像并观察其中的问题。然后，我们提出关于问题原因的假设并加以测试。例如，在光线追踪程序中，我们可能会看到许多看起来有些随机的黑色像素。这是大多数人在编写光线追踪器时遇到的经典“阴影痘”问题。传统的调试在这里没有帮助；相反，我们必须意识到阴影光线击中了被着色的表面。我们可能会注意到这些暗点的颜色是环境颜色，因此缺少的是直接照明。在阴影中可以关闭直接照明，因此你可能会假设这些点被错误地标记为在阴影中。为了测试这一假设，我们可以关闭阴影检查并重新编译。这将表明这些是虚假的阴影测试，我们可以继续我们的侦探工作。这种方法有时可以成为良好的实践的关键原因在于，我们从未必须找出错误的值或真正确定我们的概念错误。相反，我们只是通过实验逐渐缩小了我们的概念错误。通常只需要几次尝试就能找到问题，而这种类型的调试是令人愉悦的。

**Images as Coded Debugging Output 图像作为编码调试输出**
In many cases, the easiest channel by which to get debugging information out of a graphics program is the output image itself. If you want to know the value of some variable for part of a computation that runs for every pixel, you can just modify your program temporarily to copy that value directly to the output image and skip the rest of the calculations that would normally be done. For instance, if you suspect a problem with surface normals is causing a problem with shading, you can copy the normal vectors directly to the image (x goes to red, y goes to green,z goes to blue), resulting in a color-coded illustration of the vectors actually being used in your computation. Or, if you suspect a particular value is sometimes out of its valid range, make your program write bright red pixels where that happens. Other common tricks include drawing the back sides of surfaces with an obvious color (when they are not supposed to be visible), coloring the image by the ID numbers of the objects, or coloring pixels by the amount of work they took to compute.
在许多情况下，从图形程序中获取调试信息的最简单渠道是输出图像本身。如果您想要了解某个变量的值，以便对每个像素运行的计算的一部分，您可以暂时修改程序，将该值直接复制到输出图像中，并跳过通常要执行的其余计算。例如，如果您怀疑表面法线存在问题导致着色出现问题，您可以直接将法线向量复制到图像中（x 轴变为红色，y 轴变为绿色，z 轴变为蓝色），从而得到一个彩色编码的向量实际上在您的计算中使用。或者，如果您怀疑某个值有时超出其有效范围，请让您的程序在发生这种情况时写入明亮的红色像素。其他常见的技巧包括用明显的颜色绘制表面的背面（当它们不应该可见时），通过对象的 ID 号对图像进行着色，或者通过像素的计算工作量对像素进行着色。

**Using a Debugger 使用调试器**
There are still cases, particularly when the scientific method seems to have led to a contradiction, when there's no substitute for observing exactly what is going on. The trouble is that graphics programs often involve many, many executions of the same code (once per pixel, for instance, or once per triangle), making it completely impractical to step through in the debugger from the start. And the most difficult bugs usually only occur for complicated inputs.
仍然有一些情况，特别是当科学方法似乎导致矛盾时，没有替代方法来准确观察正在发生的事情。问题在于，图形程序通常涉及许多相同代码的执行（例如，每个像素一次，或每个三角形一次），因此从开始就在调试器中逐步执行是完全不切实际的。而且，最困难的错误通常只会发生在复杂的输入中。

A useful approach is to “set a trap’ for the bug. First, make sure your program is deterministic--run it in a single thread and make sure that all random numbers are computed from fixed seeds. Then, find out which pixel or triangle is exhibiting the bug and add a statement before the code you suspect is incorrect that will be executed only for the suspect case. For instance, if you find that pixel (126, 247)exhibits the bug, then add:
一种有用的方法是为错误“设置陷阱”。首先，确保您的程序是确定性的——在单个线程中运行它，并确保所有随机数都是从固定种子计算的。然后，找出哪个像素或三角形出现了错误，并在您怀疑不正确的代码之前添加一个语句，该语句仅在怀疑的情况下执行。例如，如果您发现像素（126，247）出现了错误，则添加：

```lua
if x = 126 and y = 247 then
	print "blarg!"
```

> A special debugging mode that uses fixed random-number seeds is useful.
> 使用固定随机数种子的特殊调试模式是有用的。

If you set a breakpoint on the print statement, you can drop into the debugger just before the pixel you're interested in is computed. Some debuggers have a “conditional breakpoint feature that can achieve the same thing without modifying the code.
如果在print语句上设置了一个断点，可以在计算感兴趣的像素之前进入调试器。一些调试器具有“条件断点”特性，可以在不修改代码的情况下实现相同的功能。

In the cases where the program crashes, a traditional debugger is useful for pinpointing the site of the crash. You should then start backtracking in the pro-gram, using asserts and recompiles, to find where the program went wrong. These asserts should be left in the program for potential future bugs you will add. This again means the traditional step-through process is avoided, because that would not be adding the valuable asserts to your program.
在程序崩溃的情况下，传统的调试器对于精确定位崩溃的位置很有用。然后，您应该开始在程序中回溯，使用断言和重新编译，以找到程序出错的地方。这些断言应该留在程序中，以备将来可能添加的错误使用。这再次意味着避免了传统的分步执行过程，因为这不会将有价值的断言添加到程序中。

**Data Visualization for Debugging 数据可视化调试**
Often it is hard to understand what your program is doing, because it computes a lot of intermediate results before it finally goes wrong. The situation is similar to a scientific experiment that measures a lot of data, and one solution is the same: make good plots and illustrations for yourself to understand what the data means. For instance, in a ray tracer you might write code to visualize ray trees so you can see what paths contributed to a pixel, or in an image resampling routine you might make plots that show all the points where samples are being taken from the input. Time spent writing code to visualize your program's internal state is also repaid in a better understanding of its behavior when it comes time to optimize it.
通常很难理解程序在做什么，因为它在最终出错之前计算了很多中间结果。这种情况类似于测量大量数据的科学实验，解决方案是相同的:为自己制作好的图表和插图，以了解数据的含义。例如，在光线追踪器中，你可能会编写代码来可视化光线树，这样你就可以看到什么路径促成了一个像素，或者在图像重采样例程中，你可能会制作图表来显示从输入中获取样本的所有点。为了可视化程序的内部状态而编写代码所花费的时间也会在优化程序时更好地理解它的行为。

> I like to format debugging print statements so that the output happens to be a Mat-lab or Gnuplot script that makes a helpful plot.-S.M.
> 我喜欢将调试打印语句格式化，以便输出成Matlab或Gnuplot脚本，从而生成有用的图表。-S.M.

**Notes 注**
The discussion of software engineering is influenced by the Effective C++ series (Meyers, 1995, 1997), the Extreme Programming movement (Beck & Andres, 2004), and The Practice of Programming (Kernighan & Pike, 1999). The discussion of experimental debugging is based on discussions with Steve Parker. There are a number of annual conferences related to computer graphics, including ACM SIGGRAPH and SIGGRAPH Asia, Graphics Interface, the Game Developers Conference (GDC), Eurographics, Pacific Graphics, High Performance Graphics, the Eurographics Symposium on Rendering, and IEEE VisWeek. These can be readily found by web searches on their names.
对软件工程的讨论受到《Effective C++》系列（Meyers，1995，1997）、极限编程运动（Beck＆Andres，2004）和《编程实践》（Kernighan＆Pike，1999）的影响。对实验性调试的讨论基于与Steve Parker的交流。与计算机图形相关的许多年度会议包括ACM SIGGRAPH和SIGGRAPH Asia、Graphics Interface、游戏开发者大会（GDC）、Eurographics、Pacific Graphics、High Performance Graphics、Eurographics渲染学术研讨会和IEEE VisWeek。这些会议可通过网络搜索其名称轻松找到。