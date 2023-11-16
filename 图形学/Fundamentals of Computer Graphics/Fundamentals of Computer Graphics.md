[TOC]

------





# Preface 前言

This edition of Fundamentals of Computer Graphics includes substantial rewrites of the chapters on textures and graphics hardware, as well as many corrections throughout. The figures are now in color throughout the book.
本版的《计算机图形学基础》一书对纹理和图形硬件的章节进行了大量重写，并进行了许多修正。本书中的所有图形都是彩色的。

The organization of the book remains substantially similar to the third edition. In our thinking, Chapters 2 through 8 constitute the “core core,” taking the straight and narrow path through what is absolutely required for understanding how images get onto the screen using the complementary approaches of ray tracing and rasterization. Ray tracing is covered first, since it is the simplest way to generate images of 3D scenes, followed by the mathematical machinery required for the graphics pipeline, then the pipeline itself. After that, the “outer core” covers other topics that would commonly be included in an introductory class, such as sampling theory, texture mapping, spatial data structures, and splines. Starting with Chapter 15 is a number of contributed chapters, authored by contributors we have chosen both for their expertise and for their clear way of expressing ideas.
本书的组织结构与第三版基本相似。在我们的思考中，第2章到第8章构成了“核心中的核心”，通过光线跟踪和光栅化的互补方法，沿着直线和狭窄的道路，了解将图像放到屏幕上所需的绝对要求。由于光线跟踪是生成3D场景图像的最简单方法，因此首先介绍光线跟踪，然后介绍图形管道所需的数学机制，然后介绍管道本身。之后，“核心之外”涵盖了其他通常包括在入门课程中的主题，例如采样理论、纹理映射、空间数据结构和样条。从第15章开始，是一些贡献章节，由我们选择的专业人士和表达思想清晰的贡献者编写。

As we have revised this book over the years, we have endeavored to retain the informal, intuitive style of presentation that characterizes the earlier editions, while at the same time improving consistency, precision, and completeness. We hope the reader will find the result is an appealing platform for a variety of courses in computer graphics.  
多年来，我们在修订本书时，一直努力保留早期版本所具有的非正式、直观的演示风格，同时提高了一致性、精度和完整性。我们希望读者能发现，这个结果是一个吸引人的平台，适用于各种计算机图形学课程。

## About the Cover 封面

The cover image is from Tiger in the Water by J. W. Baker (brushed and airbrushed acrylic on canvas, 16” by 20”, www.jwbart.com).
封面图片来自J.W.贝克（J. W. Baker）的《水中老虎》（Tiger in the Water）（16英寸×20英寸，刷涂和喷涂丙烯酸画布，www.jwbart.com）。

The subject of a tiger is a reference to a wonderful talk given by Alain Fournier(1943–2000) at a workshop at Cornell University in 1998. His talk was an evocative verbal description of the movements of a tiger. He summarized his point:
老虎的主题是对Alain Fournier（1943-2000）在1998年康奈尔大学的研讨会上发表的精彩演讲的参考。他的演讲是对老虎运动的生动口头描述。他总结了他的观点：

Even though modelling and rendering in computer graphics have been improved tremendously in the past 35 years, we are still not at the point where we can model automatically a tiger swimming in the river in all its glorious details. By automatically I mean in a way that does not need careful manual tweaking by an artist/expert. The bad news is that we have still a long way to go. The good news is that we have still a long way to go.
尽管在过去的35年中，计算机图形学中的建模和渲染得到了极大的改进，但我们仍然没有达到自动建模老虎在河中游泳的所有辉煌细节的地步。自动化是指以不需要艺术家/专家进行仔细手动调整的方式。坏消息是我们还有很长的路要走。好消息是我们还有很长的路要走。

## Online Resources 在线资源

The website for this book is http://www.cs.cornell.edu/∼srm/fcg4/. We will continue to maintain a list of errata and links to courses that use the book, as well as teaching materials that match the book’s style. Most of the figures in this book are in Adobe Illustrator format, and we would be happy to convert specific figures into portable formats on request. Please feel free to contact us at shirley@cs.utah.edu or srm@cs.cornell.edu.  
本书的网站是 http://www.cs.cornell.edu/∼srm/fcg4/。我们将继续维护勘误表和使用本书的课程链接，以及与本书风格相匹配的教学材料。本书中的大多数图形都是Adobe Illustrator格式的，如果需要，我们可以将特定图形转换为便携式格式。如有任何问题，请随时通过shirley@cs.utah.edu或srm@cs.cornell.edu与我们联系。

## Acknowledgments 鸣谢

The following people have provided helpful information, comments, or feedback about the various editions of this book: Ahmet Oguz Aky¨ ˘ uz, Josh Andersen, Zeferino Andrade, Kavita Bala, Adam Berger, Adeel Bhutta, Solomon Boulos, Stephen Chenney, Michael Coblenz, Greg Coombe, Frederic Cremer, Brian Curtin, Dave Edwards, Jonathon Evans, Karen Feinauer, Amy Gooch, Eungyoung Han, Chuck Hansen, Andy Hanson, Razen Al Harbi, Dave Hart, John Hart, John “Spike” Hughes, Helen Hu, Vicki Interrante, Wenzel Jakob, Doug James, Henrik Wann Jensen, Shi Jin, Mark Johnson, Ray Jones, Revant Kapoor, Kristin Kerr, Erum Arif Khan, Mark Kilgard, Dylan Lacewell, Mathias Lang, Philippe Laval, Marc Levoy, Howard Lo, Joann Luu, Ron Metoyer, Keith Morley, Eric Mortensen, Koji Nakamaru, Micah Neilson, Blake Nelson, Michael Nikelsky, James O’Brien, Steve Parker, Sumanta Pattanaik, Matt Pharr, Peter Poulos, Shaun Ramsey, Rich Riesenfeld, Nate Robins, Nan Schaller, Chris Schryvers, Tom Sederberg, Richard Sharp, Sarah Shirley, Peter-Pike Sloan, Hannah Story, Tony Tahbaz, Jan-Phillip Tiesel, Bruce Walter, Alex Williams, Amy Williams, Chris Wyman, and Kate Zebrose. 
以下人员为本书的各个版本提供了有用的信息、评论或反馈：Ahmet Oguz Aky¨ ˘ uz、Josh Andersen、Zeferino Andrade、Kavita Bala、Adam Berger、Adeel Bhutta、Solomon Boulos、Stephen Chenney、Michael Coblenz、Greg Coombe、Frederic Cremer、Brian Curtin、Dave Edwards、Jonathon Evans、Karen Feinauer、Amy Gooch、Eungyoung Han、Chuck Hansen、Andy Hanson、Razen Al Harbi、Dave Hart、John Hart、John “Spike” Hughes、Helen Hu、Vicki Interrante、Wenzel Jakob、Doug James、Henrik Wann Jensen、Shi Jin、Mark Johnson、Ray Jones、Revant Kapoor、Kristin Kerr、Erum Arif Khan、Mark Kilgard、Dylan Lacewell、Mathias Lang、Philippe Laval、Marc Levoy、Howard Lo、Joann Luu、Ron Metoyer、Keith Morley、Eric Mortensen、Koji Nakamaru、Micah Neilson、Blake Nelson、Michael Nikelsky、James O’Brien、Steve Parker、Sumanta Pattanaik、Matt Pharr、Peter Poulos、Shaun Ramsey、Rich Riesenfeld、Nate Robins、Nan Schaller、Chris Schryvers、Tom Sederberg、Richard Sharp、Sarah Shirley、Peter-Pike Sloan、Hannah Story、Tony Tahbaz、Jan-Phillip Tiesel、Bruce Walter、Alex Williams、Amy Williams、Chris Wyman和Kate Zebrose。

Ching-Kuang Shene and David Solomon allowed us to borrow their examples. Henrik Wann Jensen, Eric Levin, Matt Pharr, and Jason Waltman generously provided images. Brandon Mansfield helped improve the discussion of hierarchical bounding volumes for ray tracing. Philip Greenspun (philip.greenspun.com)  kindly allowed us to use his photographs. John “Spike” Hughes helped improve the discussion of sampling theory. Wenzel Jakob’s Mitsuba renderer was invaluable in creating many figures. We are extremely thankful to J. W. Baker for helping create the cover Pete envisioned. In addition to being a talented artist, he was a great pleasure to work with personally. 
Ching-Kuang Shene和David Solomon允许我们借用他们的例子。Henrik Wann Jensen、Eric Levin、Matt Pharr和Jason Waltman慷慨地提供了图像。Brandon Mansfield帮助改进了光线跟踪中分层边界体的讨论。Philip Greenspun（philip.greenspun.com）慷慨地允许我们使用他的照片。John “Spike” Hughes帮助改进了采样理论的讨论。Wenzel Jakob的Mitsuba渲染器在创建许多图形中非常有价值。我们非常感谢J.W.贝克（J. W. Baker）帮助创作Pete设想的封面。除了是一位才华横溢的艺术家外，他还是一位非常愉快的合作伙伴。

Many works that were helpful in preparing this book are cited in the chapter notes. However, a few key texts that influenced the content and presentation deserve special recognition here. These include the two classic computer graphics texts from which we both learned the basics: Computer Graphics: Principles & Practice (Foley, Van Dam, Feiner, & Hughes, 1990) and Computer Graphics (Hearn & Baker, 1986). Other texts include both of Alan Watt’s influential books (Watt, 1993, 1991), Hill’s Computer Graphics Using OpenGL (Francis S. Hill, 2000), Angel’s Interactive Computer Graphics: A Top-Down Approach Using OpenGL (Angel, 2002), Hugues Hoppe’s University of Washington dissertation (Hoppe, 1994), and Rogers’ two excellent graphics texts (D. F. Rogers, 1985, 1989). 
本书的章节注释中引用了许多有用的作品。然而，一些影响内容和呈现方式的关键文本值得特别认可。这些包括我们两人学习基础的两本经典计算机图形学教材：《计算机图形学原理与实践》（Foley、Van Dam、Feiner和Hughes，1990）和《计算机图形学》（Hearn和Baker，1986）。其他文本包括Alan Watt的两本有影响力的书（Watt，1993年，1991年），Hill的《使用OpenGL的计算机图形学》（Francis S. Hill，2000年），Angel的《交互式计算机图形学：使用OpenGL的自上而下方法》（Angel，2002年），Hugues Hoppe的华盛顿大学论文（Hoppe，1994年）以及Rogers的两本优秀的图形学教材（D. F. Rogers，1985年，1989年）。

We would like to especially thank Alice and Klaus Peters for encouraging Pete to write the first edition of this book and for their great skill in bringing a book to fruition. Their patience with the authors and their dedication to making their books the best they can be has been instrumental in making this book what it is. This book certainly would not exist without their extraordinary efforts.
我们要特别感谢Alice和Klaus Peters，他们鼓励Pete写第一版本书，并以其出色的技能将书籍付诸实践。他们对作者的耐心和对使他们的书籍尽善尽美的奉献精神对于使本书成为现在这个样子起到了关键作用。如果没有他们的非凡努力，这本书肯定不会存在。



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
  **医学成像**创建有意义的扫描患者数据的图像。例如，计算机断层扫描（CT）数据集由大量的3D矩形密度值数组组成。计算机图形学用于创建阴影图像，以帮助医生从这些数据中提取最重要的信息。
- **Information visualization** creates images of data that do not necessarily have a “natural’ visual depiction. For example, the temporal trend of the price of ten different stocks does not have an obvious visual depiction, but clever graphing techniques can help humans see the patterns in such data.
  **信息可视化**创建数据的图像，这些数据不一定具有“自然”的视觉描述。例如，十种不同股票价格的时间趋势没有明显的视觉描述，但巧妙的绘图技术可以帮助人们看到这些数据中的模式。

## 1.3 Graphics APIs 图形API

A key part of using graphics libraries is dealing with a graphics API. An application program interface (API) is a standard collection of functions to perform a set of related operations, and a graphics API is a set of functions that perform basic operations such as drawing images and 3D surfaces into windows on the screen. 
使用图形库的关键部分是处理图形API。应用程序编程接口（API）是一组标准函数，用于执行一组相关操作，图形API是一组函数，用于在屏幕上的窗口中绘制图像和3D表面等基本操作。

Every graphics program needs to be able to use two related APIs: a graphics API for visual output and a user-interface API to get input from the user. There are currently two dominant paradigms for graphics and user-interface APIs. The first is the integrated approach, exemplified by Java, where the graphics and user interface toolkits are integrated and portable packages that are fully standardized and supported as part of the language. The second is represented by Direct3Dand OpenGL, where the drawing commands are part of a software library tied toa language such as C++, and the user-interface software is an independent entity that might vary from system to system. In this latter approach, it is problematic to write portable code, although for simple programs it may be possible to use a portable library layer to encapsulate the system specific user-interface code. 
每个图形程序都需要能够使用两个相关的API：用于视觉输出的图形API和用于从用户获取输入的用户界面API。目前有两种主要的图形和用户界面API范例。第一种是集成方法，例如Java，其中图形和用户界面工具包是集成和可移植的包，完全标准化并作为语言的一部分得到支持。第二种是由Direct3D和OpenGL代表的方法，其中绘图命令是与诸如C++之类的语言绑定的软件库的一部分，用户界面软件是一个独立的实体，可能因系统而异。在后一种方法中，编写可移植代码存在问题，尽管对于简单的程序，可能可以使用可移植库层来封装特定于系统的用户界面代码。

Whatever your choice of API, the basic graphics calls will be largely the same, and the concepts of this book will apply.
无论您选择哪种API，基本的图形调用将基本相同，并且本书的概念将适用。

## 1.4 Graphics Pipeline 图形管道

Every desktop computer today has a powerful 3D graphics pipeline. This is a special software/hardware subsystem that efficiently draws 3D primitives in perspective. Usually these systems are optimized for processing 3D triangles with shared vertices. The basic operations in the pipeline map the 3D vertex locations to 2D screen positions and shade the triangles so that they both look realistic and appear in proper back-to-front order.
今天的每台台式计算机都有一个强大的3D图形管道。这是一个特殊的软件/硬件子系统，可以有效地以透视方式绘制3D基元。通常，这些系统被优化为处理具有共享顶点的3D三角形。管道中的基本操作将3D顶点位置映射到2D屏幕位置，并对三角形进行着色，使其既看起来逼真又按正确的前后顺序出现。

Although drawing the triangles in valid back-to-front order was once the most important research issue in computer graphics, it is now almost always solved using the z-buffer, which uses a special memory buffer to solve the problem in a brute-force manner.
虽然以有效的前后顺序绘制三角形曾经是计算机图形学中最重要的研究问题，但现在几乎总是使用z缓冲区来解决这个问题，z缓冲区使用特殊的内存缓冲区以蛮力方式解决问题。

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
使代码快速的一个合理方法是按照以下顺序进行，只采取必要的步骤：

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
这些步骤中最重要的是第一步。大多数“优化”使代码难以阅读，但却没有加快速度。此外，花在优化代码上的时间通常最好花在纠正错误或添加功能上。此外，要小心旧文本中的建议;一些经典的技巧，比如使用整数代替实数，可能不再提高速度，因为现代CPU执行浮点运算的速度通常和执行整数运算一样快。在所有情况下，都需要进行分析，以确保针对特定机器和编译器的任何优化的优点。

## 1.7 Designing and Coding Graphics Programs 设计和编码图形程序

Certain common strategies are often useful in graphics programming. In this section we provide some advice that you may find helpful as you implement the methods you learn about in this book.
某些常见的策略在图形编程中通常很有用。在本节中，我们提供了一些建议，在您实现本书中学习的方法时可能会对您有所帮助。

### 1.7.1 Class Design 类设计

A key part of any graphics program is to have good classes or routines for geometric entities such as vectors and matrices, as well as graphics entities such as RGB colors and images. These routines should be made as clean and efficient as possible. A universal design question is whether locations and displacements should be separate classes because they have different operations, e.g. , a location multiplied by one-half makes no geometric sense while one-half of a displacement does (Goldman, 1985: DeRose, 1989). There is little agreement on this question， which can spur hours of heated debate among graphics practitioners, but for the sake of example let's assume we will not make the distinction.
任何图形程序的关键部分是拥有良好的类或例程，用于几何实体（如向量和矩阵）以及图形实体（如RGB颜色和图像）。这些例程应尽可能地简洁和高效。一个通用的设计问题是位置和位移是否应该是单独的类，因为它们具有不同的操作，例如，将位置乘以一半没有几何意义，而将位移的一半则有（Goldman, 1985: DeRose, 1989）。对于这个问题，人们的意见不一，这可能会引发图形从业者数小时的激烈辩论，但为了举例，我们假设我们不会做出区分。

> I believe strongly in the KISS(“keep it simple, stupid’) principle, and in that light the argument fortwo classes is not compelling enough to justify the added complexity. -PS
> 我强烈相信KISS（“保持简单，愚蠢”）原则，在这种情况下，两个类的论点不足以证明增加的复杂性是合理的。-PS 

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
此外，您可能或可能不想添加间隔、正交基和坐标框的类。

> You might also consider a special class for unit-length  vectors, although I have found them more pain than they are worth.-PS.
> 您可能还需要考虑为单位长度向量设计一个特殊的类，尽管我发现它们比它们的价值更痛苦。-PS。



### 1.7.2 Float vs. Double

Modern architecture suggests that keeping memory use down and maintaining coherent memory access are the keys to efficiency. This suggests using single-precision data. However, avoiding numerical problems suggests using double precision arithmetic. The tradeoffs depend on the program, but it is nice to have a default in your class definitions.
现代架构建议将内存使用量降至最低并保持连贯的内存访问是提高效率的关键。这表明应使用单精度数据。然而，避免数值问题则建议使用双精度算术。权衡取决于程序，但在类定义中设置默认值是很好的选择。

> I suggest using doubles for geometric computation and floats for color computation. For data that occupies a lot of memory, such as triangle meshes,I suggest storing float data, but con-verting to double when data is accessed through member functions.-PS.
> 我建议在几何计算中使用双精度，而在颜色计算中使用单精度。对于占用大量内存的数据，例如三角形网格，我建议存储单精度数据，但在通过成员函数访问数据时将其转换为双精度。-PS。

> I advocate doing all computations with floats until you find evidence that double precision is needed in a particular part of the code.-S.M.
> 我主张使用单精度浮点数进行所有计算，直到在代码的特定部分发现需要双精度精度的证据。-S.M。

### 1.7.3 Debugging Graphics Programs 调试图形程序

If you ask around, you may find that as programmers become more experienced,they use traditional debuggers less and less. One reason for this is that using such debuggers is more awkward for complex programs than for simple programs. Another reason is that the most difficult errors are conceptual ones where the wrong thing is being implemented, and it is easy to waste large amounts of time stepping through variable values without detecting such cases. We have found several debugging strategies to be particularly useful in graphics.
如果你询问一下，你会发现随着程序员经验的增长，他们使用传统的调试器的次数越来越少。其中一个原因是，对于复杂的程序而言，使用这样的调试器比简单的程序更加棘手。另一个原因是，最困难的错误是概念性的错误，即正在实现错误的事情，而且很容易浪费大量时间在变量值上，而没有检测到这些情况。我们发现在图形中有几种调试策略特别有用。

**The Scientific Method 科学方法**
In graphics programs there is an alternative to traditional debugging that is often very useful. The downside to it is that it is very similar to what computer programmers are taught not to do early in their careers, so you may feel “naughty”if you do it: we create an image and observe what is wrong with it. Then, we develop a hypothesis about what is causing the problem and test it. For example,in a ray-tracing program we might have many somewhat random looking dark pixels. This is the classic “shadow acne” problem that most people run into when they write a ray tracer. Traditional debugging is not helpful here; instead, we must realize that the shadow rays are hitting the surface being shaded. We might notice that the color of the dark spots is the ambient color, so the direct lighting is what is missing. Direct lighting can be turned off in shadow, so you might hypothesize that these points are incorrectly being tagged as in shadow when they are not. To test this hypothesis, we could turn off the shadowing check and recompile. This would indicate that these are false shadow tests, and we could continue our detective work. The key reason that this method can sometimes be good practice is that we never had to spot a false value or really determine our conceptual error. Instead, we just narrowed in on our conceptual error experimentally. Typically only a few trials are needed to track things down, and this type of debugging is enjoyable.
在图形程序中，有一种传统调试的替代方法，通常非常有用。它的缺点是它与计算机程序员在职业生涯早期所学的内容非常相似，因此您可能会感到“naughty”（不安分）：我们创建一个图像并观察其中的问题。然后，我们提出一个关于问题原因的假设并进行测试。例如，在光线追踪程序中，我们可能会有许多看起来有些随机的黑色像素。这是大多数人编写光线追踪器时遇到的经典“阴影痤疮”问题。传统的调试在这里没有帮助；相反，我们必须意识到阴影光线正在击中被遮蔽的表面。我们可能会注意到暗斑点的颜色是环境颜色，因此缺少直接照明。直接照明可以在阴影中关闭，因此您可能会假设这些点被错误地标记为在阴影中，而实际上并不是。为了测试这个假设，我们可以关闭阴影检查并重新编译。这将表明这些是虚假的阴影测试，我们可以继续进行侦探工作。这种方法有时可以成为良好的实践的关键原因是我们从未发现过虚假值或真正确定我们的概念错误。相反，我们只是通过实验缩小了我们的概念错误。通常只需要几次尝试就可以追踪事物，这种调试方式是令人愉快的。

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
软件工程的讨论受到了Effective C++系列（Meyers，1995, 1997），极限编程运动（Beck＆Andres，2004）和编程实践（Kernighan＆Pike，1999）的影响。实验调试的讨论基于与Steve Parker的讨论。有许多与计算机图形相关的年度会议，包括ACM SIGGRAPH和SIGGRAPH Asia，Graphics Interface，游戏开发者大会（GDC），Eurographics，Pacific Graphics，High Performance Graphics，Eurographics渲染研讨会和IEEE VisWeek。这些会议可以通过网络搜索它们的名称轻松找到。



# 2 Miscellaneous Math 各种各样的数学

Much of graphics is just translating math directly into code. The cleaner the math,the cleaner the resulting code; so much of this book concentrates on using just theright math for the job. This chapter reviews various tools from high school andcollege mathematics and is designed to be used more as a reference than as a tu-torial. It may appear to be a hodge-podge of topics and indeed it is; each topicis chosen because it is a bit unusual in “standard’ math curricula, because it isof central importance in graphics, or because it is not typically treated from a ge-ometric standpoint. In addition to establishing a review of the notation used inthe book, the chapter also emphasizes a few points that are sometimes skippedin the standard undergraduate curricula, such as barycentric coordinates on tri-angles. This chapter is not intended to be a rigorous treatment of the material;instead intuition and geometric interpretation are emphasized. A discussion oflinear algebra is deferred until Chapter 5 just before transformation matrices arediscussed. Readers are encouraged to skim this chapter to familiarize themselveswith the topics covered and to refer back to it as needed. The exercises at the endof the chapter may be useful in determining which topics need a refresher.
图形学中的很多内容只是将数学直接转换为代码。 数学越干净，生成的代码就越干净；因此，本书的很多内容都集中在使用正确的数学来完成工作。 本章回顾了高中和大学数学中的各种工具，并旨在作为参考而非教程使用。 它可能看起来像一堆杂乱无章的主题，而事实上确实如此；每个主题都是因为它在“标准”数学课程中有些不寻常，因为它在图形学中具有核心重要性，或者因为它通常不从几何角度处理。 除了建立本书中使用的符号的审查外，本章还强调了一些标准本科课程中有时会跳过的要点，例如三角形的重心坐标。 本章不旨在对材料进行严格的处理；相反，强调直觉和几何解释。 线性代数的讨论推迟到第5章之前，就在讨论变换矩阵之前。 鼓励读者浏览本章以熟悉所涵盖的主题，并根据需要参考它。 章末的练习可能有助于确定哪些主题需要复习。

## 2.1 Sets and Mappings 集合和映射

Mappings, also called functions, are basic to mathematics and programming. Likea function in a program, a mapping in math takes an argument of one type and maps it to (returns) an object of a particular type. In a program we say “type; inmath we would identify the set. When we have an object that is a member of aset, we use the $\in$ symbol. For example, $a \in \bold{S} $,
映射，也称为函数，是数学和编程的基础。就像程序中的函数一样，数学中的映射接受一个类型的参数并将其映射到（返回）特定类型的对象。在程序中，我们说“类型”；在数学中，我们会确定集合。当我们有一个属于集合的对象时，我们使用 $\in$ 符号。例如，$a \in \bold{S} $。

can be read "a is a member of set $\bold{S}$." Given any two sets **A** and **B**, we can createa third set by taking the Cartesian product of the two sets, denoted $\bold{A} \cross \bold{B}$. This set $\bold{A} \cross \bold{B}$ is composed of all possible ordered pairs (a, b) where $a \in \bold{A} $ and $b \in \bold{B} $. As a shorthand, we use the notation $\bold{A}^2$to denote $\bold{A} \cross \bold{A} $. We can extendthe Cartesian product to create a set of all possible ordered triples from three sets and so on for arbitrarily long ordered tuples from arbitrarily many sets.
可以读作“a是集合$\bold{S}$的成员”。给定任意两个集合**A**和**B**，我们可以通过取这两个集合的笛卡尔积来创建第三个集合，表示为$\bold{A} \cross \bold{B}$。这个集合$\bold{A} \cross \bold{B}$由所有可能的有序对(A, B)组成，其中$ a \in \bold{A} $和$ b \in \bold{B}$。作为速记，我们使用符号$\bold{A}^2$来表示$\bold{A} \cross \bold{A} $。我们可以将笛卡尔积扩展到从三个集合中创建所有可能的有序三元组，以及从任意多个集合中创建任意长的有序元组。

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
请注意，虽然$S^2$是由嵌入在三维空间中的点组成的，但它们位于一个可以用两个变量参数化的表面上，因此它可以被认为是一个二维集合。映射的表示法使用箭头和冒号，例如:
$f:\R \mapsto \Z$

which you can read as “There is a function called f that takes a real number as input and maps it to an integer. Here, the set that comes before the arrow is called the domain of the function, and the set on the right-hand side is called the target. Computer programmers might be more comfortable with the following equivalent language: “There is a function called f which has one real argument and returns an integer. In other words, the set notation above is equivalent to the common programming notation:
你可以这样读：“有一个名为f的函数，它以实数作为输入并将其映射到整数。” 这里，箭头前面的集合称为函数的定义域，右侧的集合称为目标。计算机程序员可能更喜欢以下等效语言：“有一个名为f的函数，它有一个实数参数并返回一个整数。“ 换句话说，上面的集合符号等价于常见的编程符号：
$integer\ f(real) \leftarrow equivalent \rightarrow f:\R \mapsto \Z.$

So the colon-arrow notation can be thought of as a programming syntax. It’s that simple.
所以冒号箭头符号可以被看作是一种编程语法。就是这么简单。

The point f(a) is called the image of a, and the image of a set A (a subset of the domain) is the subset of the target that contains the images of all points in A. The image of the whole domain is called the range of the function. 
点f(a)称为a的像，集合A（定义域的子集）的像是包含A中所有点的像的目标的子集。整个定义域的像称为函数的值域。

### 2.1.1 Inverse Mappings 逆映射

If we have a function $f:\bold{A} \mapsto \bold{B}$, there may exist an inverse function $f^{-1}:\bold{B} \mapsto \bold{A}$, which is defined by the rule $f^{-1}(b) = a$ where $b = f(a)$. This definition only works if every $b \in \bold{B}$ is an image of some point under $f$ (that is, the range equals the target) and if there is only one such point (that is, there is only one $a$ for which $f(a) = b$). Such mappings or functions are called bijections. A bijection maps every $a \in A$ to a unique $b \in \bold{B}$, and for every $b \in \bold{B}$, there is exactly one $a \in \bold{A}$ such that $f(a) = b$ (Figure 2.1). A bijection between a group of riders and horses indicates that everybody rides a single horse, and every horse is ridden. The two functions would be rider(horse) and horse(rider). These are inverse functions of each other. Functions that are not bijections have no inverse (Figure 2.2).
如果我们有一个函数$f:\bold{A} \mapsto \bold{B}$，则可能存在一个逆函数 $f^{-1}:\bold{B} \mapsto \bold{A}$，其由规则$f^{-1}(b) = a$定义，其中$b = f(a)$。此定义仅在每个$b \in \bold{B}$都是$f$下某个点的图像（即，范围等于目标）且只有一个这样的点（即，只有一个$a$满足$f(a) = b$）时才有效。这样的映射或函数称为双射。双射将每个$a \in A$映射到唯一的$b \in \bold{B}$，并且对于每个$b \in \bold{B}$，都有一个$a \in \bold{A}$满足$f(a) = b$（图2.1）。骑手和马之间的双射表明每个人都骑一匹马，每匹马都被骑。两个函数将是$rider(horse)$和$horse(rider)$。它们是彼此的逆函数。不是双射的函数没有逆（图2.2）。

<img src=".\Images\Figure 2.1.png" alt="Figure 2.1" style="zoom: 67%;" />
Figure 2.1. A bijection $f$ and the inverse function $f^{-1}$. Note that $f^{–1}$ is also a bijection. 
图2.1. 一个双射$f$和反函数$f^{-1}$。注意$f^{-1}$也是一个双射。
![Figure 2.1](.\Images\Figure 2.2.png)
Figure 2.2.The function $g$ does not have an inverse be-cause two elements of $\bold{d}$ map to the same element of $\bold{E}$. The function h has no inverse be-cause element $T$ of $\bold{F}$ has no element of $\bold{d}$ mapped to it.
图2.2. 函数$g$没有逆，因为$\bold{d}$的两个元素映射到$\bold{E}$的同一个元素。函数h没有逆，因为$\bold{F}$的$T$没有$\bold{d}$的元素映射到它。

An example of a bijection is $f : \R \mapsto \R$, with $f(x) = x^3$. The inverse function is $f^{-1}(x) = \sqrt[3]{x}$. This example shows that the standard notation can be somewhat awkward because $x$ is used as a dummy variable in both $f$ and $f^{-1}$. It is sometimes more intuitive to use different dummy variables, with $y = f(x)$ and $x = f^{-1}(y)$. This yields the more intuitive $y = x^3$ and $x = \sqrt[3]{y}$. An example of a function that does not have an inverse is $sqr : \R \mapsto \R$, where $sqr(x) = x^2$. This is true for two reasons: first $x^2 = (-x)^2$, and second no members of the domain map to the negative portions of the target. Note that we can define an inverse if we restrict the domain and range to $\R ^+$. Then  $\sqrt{x}$ is a valid inverse.
双射的一个例子是$f: \R \mapsto \R$，其中$f(x) = x^3$。逆函数是$f^{-1}(x) = \sqrt[3]{x}$。这个例子表明，标准表示法可能有些笨拙，因为$x$在$f$和$f^{-1}$中都被用作哑变量。有时使用不同的虚拟变量更直观，例如$y = f(x)$和$x = f^{-1}(y)$。这产生了更直观的$y = x^3$和$x = \sqrt[3]{y}$。一个没有逆函数的例子是$sqr: \R \mapsto \R$，其中$sqr(x) = x^2$。这有两个原因:首先$x^2 = (-x)^2$，其次，没有域的成员映射到目标的负部分。注意，如果我们将定义域和值域限制为$\R ^+$，我们可以定义逆。那么$\sqrt{x}$是一个有效的逆。

### 2.1.2 Intervals 区间

Often we would like to specify that a function deals with real numbers that are restricted in value. One such constraint is to specify an interval. An example of an interval is the real numbers between zero and one, not including zero or one We denote this $(0, 1)$. Because it does not include its endpoints, this is referred to as an open interval. The corresponding closed interval, which does contain its endpoints,is denoted with square brackets: $[0, 1]$ . This notation can be mixed, i.e. $[0, 1)$ includes zero but not one. When writing an interval $[a, b]$, we assume that $a \le b$. The three common ways to represent an interval are shown in Figure 2.3.The Cartesian products of intervals are often used. For example, to indicate that a point x is in the unit cube in 3D, we say $x \in [0, 1]^3$.
通常，我们希望指定函数处理受限制的实数。其中一种约束是指定区间。区间的一个例子是介于零和一之间的实数，不包括零或一，我们用$(0, 1)$表示。因为它不包括其端点，所以称为开区间。相应的闭区间，它包含其端点，用方括号表示：$[0, 1]$ 。这个符号可以混合使用，即$[0, 1)$包括零但不包括一。在写区间$[a, b]$时，我们假设$a \le b$。表示区间的三种常见方法如图2.3所示。区间的笛卡尔积经常被使用。例如，要表示点x在三维单位立方体中，我们说$x \in [0, 1]^3$。
![Figure 2.3](.\Images\Figure 2.3.png)
Figure 2.3. Three equivalent ways to denote the interval from a to b that includes b but not a.
图2.3. 表示包括b但不包括a的区间a到b的三种等效方法。

Intervals are particularly useful in conjunction with set operations: intersection, union, and difference. For example, the intersection of two intervals is the set of points they have in common. The symbol $\cap$ is used for intersection. For ex-ample, $[3, 5) \cap [4, 6] = [4, 5)$. For unions, the symbol $\cup$ is used to denote points in either interval. For example, $[3, 5) \cup [4, 6] = [3, 6]$. Unlike the first two operators, the difference operator produces different results depending on argument order. The minus sign is used for the difference operator, which returns the points in the left interval that are not also in the right. For example, $[3, 5) - [4, 6] = [3, 4)$ and $[4, 6] - [3, 5) = [5, 6]$. These operations are particularly easy to visualize using interval diagrams (Figure 2.4).
区间在与集合操作(交集、并并和差)结合时特别有用。例如，两个区间的交集是它们共有的点的集合。符号$\cap$表示交集。例如:$[3, 5) \cap [4, 6] = [4, 5)$。对于联合，符号$\cup$用于表示任一区间中的点。例如:$[3, 5) \cup [4, 6] = [3, 6]$。与前两个操作符不同，差操作符根据参数顺序产生不同的结果。负号用于差分运算符，它返回左边区间中不在右边区间中的点。例如:$[3, 5) - [4, 6] = [3, 4)$、$[4, 6] - [3, 5) = [5, 6]$。使用间隔图(图2.4)，这些操作特别容易可视化。
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

## 2.2 Solving Quadratic Equations

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
这里的"$\pm$"符号表示有两个解，一个带正号，一个带负号。因此，$3\pm1$ 等于“二或四”。请注意，决定实数解数量的术语是
$D \equiv B^2 -4AC$

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
图2.6中，两个半线将单位圆分为两个弧。任何一个弧的长度都是两个半线之间的有效角度。我们可以使用较小的长度作为角度的度量，或者按照某种顺序指定两个半线，并且从第一个半线逆时针扫过的弧确定角度$\varphi$

Each of these angles is the length of the arc of the unit circle that is “cut” by the two directions. Because the perimeter of the unit circle is $2\pi$, the two possible angles sum to $2\pi$. The unit of these arc lengths is radians. Another common unit is degrees, where the perimeter of the circle is 360 degrees. Thus, an angle that is $\pi$ radians is 180 degrees, usually denoted 180◦. The conversion between degrees and radians is  
每个角度都是由两个方向“切割”的单位圆的弧的长度。由于单位圆的周长为$2\pi$，因此两个可能的角度之和为$2\pi$。这些弧长的单位是弧度。另一个常见的单位是度，其中圆的周长为360度。因此，一个$\pi$弧度的角度是180度，通常表示为180◦。度和弧度之间的转换公式为
$$
degrees = \frac{180}{\pi} radians; \\
radians = \frac{\pi}{180} degrees.\\
$$

### 2.3.2 Trigonometric Functions 三角函数

Given a right triangle with sides of length a, o, and h, where h is the length of the longest side (which is always opposite the right angle), or hypotenuse, an important relation is described by the Pythagorean theorem:
给定一个边长为a、o和h的直角三角形，其中h是最长的边(总是直角的对边)或斜边的长度，毕达哥拉斯定理描述了一个重要的关系:
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
这些定义允许我们建立极坐标系，其中一个点被编码为相对于正x轴的距离和带符号的角度（图2.8）。请注意，角度在$\varphi \in (-\pi, \pi] $范围内，并且正角度是从正x轴逆时针旋转的。这种逆时针映射到正数的约定是任意的，但在许多图形上下文中使用，因此值得记忆。
![Figure 2.8](.\Images\Figure 2.8.png)
Figure 2.8. Polar coordinates for the point $(x_a, y_a) = (1, \sqrt{3})$ is $(r_a, \varphi_a) = (2, \pi/3)$.
图2.8.  点$(x_a, y_a) = (1, \sqrt{3})$ 的极坐标为$(r_a, \varphi_a) = (2, \pi/3)$。

Trigonometric functions are periodic and can take any angle as an argument. For example, $\sin(A) = \sin(A + 2)$. This means the functions are not invertible when considered with the domain $\R$. This problem is avoided by restricting the range of standard inverse functions, and this is done in a standard way in almost all modern math libraries (e.g., (Plauger, 1991)). The domains and ranges are:
三角函数是周期性的，可以将任何角度作为参数。例如，$\sin(A) = \sin(A + 2)$。这意味着在定义域$\R$上，这些函数不可逆。这个问题可以通过限制标准反函数的范围来避免，这在几乎所有现代数学库中都是以标准方式完成的（例如，（Plauger，1991））。定义域和值域如下：
$$
\asin: [-1, 1] \mapsto [-\pi/2, \pi/2] \\
\acos: [-1, 1] \mapsto [0, \pi] \\
\atan: \R \mapsto [-\pi/2, \pi/2] \\
\atan2: \R^2 \mapsto [-\pi, \pi] \\
$$
The last function, $atan2(s, c)$ is often very useful. It takes an $s$ value proportional to $\sin A$ and a $c$ value that scales $\cos A$ by the same factor and returns $A$. The factor is assumed to be positive. One way to think of this is that it returns the angle of a 2D Cartesian point $(s, c)$ in polar coordinates (Figure 2.9).
最后一个函数$atan2(s, c)$通常非常有用。它接受与$\sin A$成比例的$s$值和将$\cos A$按相同因子缩放的$c$值，并返回$A$。假定该因子为正。一种思考方式是，它返回二维笛卡尔坐标系中点$(s, c)$的极坐标角度（图2.9）。
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
Pythagorean\ identities: \\
\sin^2 A + \cos^2 A = 1 \\
\sec^2 A − \tan^2 A = 1 \\
\csc^2 A − \cot^2 A = 1 \\
$$

$$
Addition\ and\ subtraction\ identities: \\
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
矢量表示长度和方向。它可以用箭头来表示。如果两个向量的长度和方向相同，即使我们认为它们位于不同的地方，它们也是相等的(图2.11)。尽可能地，你应该把矢量想象成一个箭头，而不是坐标或数字。在某些情况下，我们必须在程序中将向量表示为数字，但即使在代码中，它们也应该作为对象进行操作，并且只有低级向量操作才应该知道它们的数字表示(DeRose, 1989)。向量将被表示为粗体字符，例如，$\bold{a}$。向量的长度表示为$\|\bold{a}\|$。单位向量是任何长度为1的向量。零向量是长度为0的向量。零向量的方向没有定义。![Figure 2.11](.\Images\Figure 2.11.png)
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
二维向量可以写成任意两个不平行的非零向量的组合。这两个向量的性质叫做线性无关。两个线性无关的向量构成一个二维基，因此这两个向量被称为基向量。例如，向量$\bold{c}$ 可以表示为两个基向量$\bold{a}$和$\bold{b}$的组合(图2.15):
$\bold{c} = a_c\bold{a} + b_c\bold{b} \ \ \ \ \ \ (2.3)$.
<img src=".\Images\Figure 2.15.png" alt="Figure 2.15" style="zoom:80%;" />
Figure 2.15. Any 2D vector $\bold{c}$ is a weighted sum of any two nonparallel 2D vectors $\bold{a}$ and $\bold{b}$.
图2.15 任意二维向量$\bold{c}$是任意两个非平行二维向量$\bold{a}$和$\bold{b}$的加权和。

Note that the weights $a_c$ and $b_c$ are unique. Bases are especially useful if the two vectors are orthogonal, i.e., they are at right angles to each other. It is even more useful if they are also unit vectors in which case they are orthonormal. If we assume two such “special" vectors $\bold{x}$ and $\bold{y}$ are known to us, then we can use them to represent all other vectors in a Cartesian coordinate system, where each vector is represented as two real numbers. For example, a vector $\bold{a}$ might be represented as
注意，权重$a_c$和$b_c$是唯一的。如果两个向量是正交的，即它们彼此成直角，基就特别有用。如果它们也是单位向量的话就更有用了在这种情况下它们是标准正交的。如果我们假设两个这样的“特殊向量”$\bold{x}$和$\bold{y}$是已知的，那么我们可以用它们来表示笛卡尔坐标系中的所有其他向量，其中每个向量都用两个实数表示。例如，向量$\bold{a}$可以表示为
$\bold{a} = x_a\bold{x} + y_a\bold{y}$,

where $x_a$ and $y_a$ are the real Cartesian coordinates of the 2D vector a (Figure 2.16). Note that this is not really any different conceptually from Equation (2.3), where the basis vectors were not orthonormal. But there are several advantages to a Cartesian coordinate system. For instance, by the Pythagorean theorem, the length of $\bold{a}$ is
其中，$x_a$和$y_a$为二维向量a的实笛卡尔坐标(图2.16)。请注意，这在概念上与公式(2.3)没有任何不同，其中基向量不是标准正交的。但是笛卡尔坐标系有几个优点。例如，根据勾股定理，$\bold{a}$的长度为
$\|\bold{a}\| = \sqrt{x_a^2 + y_a^2}$
<img src=".\Images\Figure 2.16.png" alt="Figure 2.16" style="zoom:80%;" />
Figure 2.16. A 2D Cartesian basis for vectors.
图2.16 向量的二维笛卡尔基

It is also simple to compute dot products, cross products, and coordinates of vectors in Cartesian systems, as we'll see in the following sections.
在笛卡尔坐标系中计算点积、叉积和向量坐标也很简单，我们将在接下来的章节中看到。

By convention we write the coordinates of a either as an ordered pair $(x_a, y_a)$or a column matrix:
按照惯例，我们将a的坐标写成有序对$(x_a, y_a)$或列矩阵:
$\bold{a} = \begin{bmatrix} x_a \\ y_a \end{bmatrix}$

The form we use will depend on typographic convenience. We will also occasionally write the vector as a row matrix, which we will indicate as $\bold{a}^T$.
我们使用的形式将取决于排版的便利性。我们偶尔也会将向量写成行矩阵，我们将其表示为$\bold{a}^T$。
$\bold{a}^T = \begin{bmatrix} x_a & y_a \end{bmatrix}$

We can also represent 3D, 4D, etc., vectors in Cartesian coordinates. For the 3D case, we use a basis vector z that is orthogonal to both x and y.
我们也可以用笛卡尔坐标表示3D, 4D等向量。对于三维情况，我们使用一个基向量z，它与x和y都正交。



### 2.4.3 Dot Product 点积

The simplest way to multiply two vectors is the dot product. The dot product of $\bold{a}$ and $\bold{b}$ is denoted $\bold{a} \cdot \bold{b}$ and is often called the scalar product because it returns a scalar. The dot product returns a value related to its arguments' lengths and the angle $\varphi$ between them (Figure 2.17):
两个向量相乘最简单的方法是点积。$\bold{a}$和$\bold{b}$的点积表示为$\bold{a} \cdot \bold{b}$，通常称为标量积，因为它返回一个标量。点积返回的值与参数的长度和它们之间的夹角$\varphi$有关(图2.17):
$\bold{a} \cdot \bold{b} = \|\bold{a}\| \|\bold{b}\|\cos\varphi$          (2.4)
![Figure 2.17](.\Images\Figure 2.17.png)
Figure 2.17. The dot product is related to length and angle and is one of the most important formulas in graphics.
图2.17 点积与长度和角度有关，是图形学中最重要的公式之一

The most common use of the dot product in graphics programs is to compute the cosine of the angle between two vectors.
点积在图形程序中最常用的用法是计算两个向量夹角的余弦值。

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
叉乘$\bold{a} \cross \bold{b}$通常只用于三维向量；在本章附注的参考文献中讨论了广义叉积。叉乘返回一个垂直于叉乘的两个参数的三维向量。结果向量的长度与$\sin\varphi$有关:
$\|\bold{a} \cross \bold{b}\| = \|\bold{a}\|\|\bold{b}\|\sin\varphi$

The magnitude $\|\bold{a} \cross \bold{b}\|$ is equal to the area of the parallelogram formed by vectors $\bold{a}$ and $\bold{b}$. In addition, $\bold{a} \cross \bold{b}$ is perpendicular to both $\bold{a}$ and $\bold{b}$ (Figure 2.19). Note that there are only two possible directions for such a vector. By definition, the vectors in the direction of the x-, y- and z-axes are given by
$\|\bold{a} \cross \bold{b}\|$ 的大小 等于由向量 $\bold{a}$ 和 $\bold{b}$ 形成的平行四边形的面积。 此外，$\bold{a} \cross \bold{b}$ 垂直于$\bold{a}$ 和$\bold{b}$（图2.19）。 请注意，这样的向量只有两个可能的方向。 根据定义，x、y 和 z 轴方向上的向量由下式给出
$$
\bold{x} = (1, 0, 0) \\
\bold{y} = (0, 1, 0) \\
\bold{z} = (0, 0, 1) \\
$$
<img src=".\Images\Figure 2.19.png" alt="Figure 2.19" style="zoom:80%;" />
Figure 2.19.The cross product $\bold{a} \cross \bold{b}$ is a 3D vector perpendicular to both 3D vectors $\bold{a}$ and $\bold{b}$, and its length is equal to the area of the parallelogram shown.
图2.19 叉积是一个$\bold{a} \cross \bold{b}$垂直于3D向量$\bold{a}$和$\bold{b}$的三维向量，它的长度等于所示平行四边形的面积

and we set as a convention that $\|\bold{x} \cross \bold{y}\|$must be in the plus or minus z direction. The choice is somewhat arbitrary, but it is standard to assume that
我们设定$\|\bold{x} \cross \bold{y}\|$必须在正负z方向上。这个选择有些武断，但这是标准的假设
$\bold{z} = \bold{x} \cross \bold{y}$

All possible permutations of the three Cartesian unit vectors are
三个笛卡尔单位向量的所有可能的排列是
$$
\bold{x} × \bold{y} = +\bold{z} \\
\bold{y} × \bold{z} = -\bold{z} \\
\bold{y} × \bold{z} = +\bold{x} \\
\bold{z} × \bold{y} = -\bold{x} \\
\bold{z} × \bold{x} = +\bold{y} \\
\bold{x} × \bold{z} = -\bold{y} \\
$$
Because of the $\sin\varphi$ property, we also know that a vector cross itself is the zero-vector, so $\bold{x} \cross \bold{x} = \bold{0}$ and so on. Note that the cross product is not commutative, i.e., $\bold{x} \cross \bold{y} \ne \bold{y} \cross \bold{x}$. The careful observer will note that the above discussion does not allow us to draw an unambiguous picture of how the Cartesian axes relate. More specifically, if we put $\bold{x}$ and $\bold{y}$ on a sidewalk, with $\bold{x}$ pointing east and $\bold{y}$ pointing north, then does $\bold{z}$ point up to the sky or into the ground? The usual convention is to have $\bold{z}$ point to the sky. This is known as a right-handed coordinate system. This name comes from the memory scheme of “grabbing” $\bold{x}$ with your right palm and fingers and rotating it toward $\bold{y}$. The vector $\bold{z}$ should align with your thumb. This is illustrated in Figure 2.20.
由于$\sin\varphi$的性质，我们也知道一个向量与自身相交是零向量，所以$\bold{x} \cross \bold{x} = \bold{0}$等等。注意叉乘是不可交换的，也就是$\bold{x} \cross \bold{y} \ne \bold{y} \cross \bold{x}$。细心的观察者会注意到，上面的讨论并不能让我们明确地描绘出笛卡尔轴之间的关系。更具体地说，如果我们把$\bold{x}$和$\bold{y}$放在水平面上，$\bold{x}$指向东，$\bold{y}$指向北，那么$\bold{z}$是指向天空还是指向地面?通常的惯例是$\bold{z}$指向天空。这被称为右手坐标系。这个名字来自于用右手手掌和手指“抓住”$\bold{x}$，并将其旋转到$\bold{y}$的记忆方案。向量$\bold{z}$应该与你的拇指对齐。如图2.20所示。
<img src=".\Images\Figure 2.20.png" alt="Figure 2.20" style="zoom:67%;" />
Figure 2.20. The “right-hand rule" for cross products. Imagine placing the base your right palm where $\bold{a}$ and $\bold{b}$ join at their tails, and pushing the arrow of $\bold{a}$ toward $\bold{b}$. Your extended right thumb should point toward $\bold{a} \cross \bold{b}$.
图2.20 叉乘的右手定则。想象一下，把你的右手掌底部放在$\bold{a}$和$\bold{b}$尾部连接的地方，然后把$\bold{a}$的箭头推向$\bold{b}$。你伸出的右手拇指应该指向。$\bold{a} \cross \bold{b}$

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
在三维空间中，三个向量$\bold{u}$， $\bold{v}$和$\bold{w}$构成一个标准正交基if
$\|\bold{u}\| = \|\bold{v}\| = \|\bold{w}\| = 1$
$\bold{u} \cdot \bold{v} = \bold{v} \cdot \bold{w} = \bold{w} \cdot \bold{u} = 0$

This orthonormal basis is right-handed provided 
这个标准正交基是右手性的
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
在指定摄像机位置的例子中(第4.3节)，我们想要构造一个帧，其中$\bold{w}$平行于摄像机所看的方向，$\bold{v}$应该指向摄像机的顶部。为了使摄像机垂直定向，我们围绕视角方向建立基，以垂直方向作为参考向量，围绕视角方向建立摄像机的方向。将$\bold{v}$设置为尽可能接近垂直，正好符合“保持相机垂直”的直观概念。

> If you want me to set $\bold{w}$ and $\bold{v}$ to two nonperpendicular directions, something has to give-with this scheme I'll set everything the way you want, except I'll make the smallest change to $\bold{v}$ so that it is in fact perpendicular to $\bold{w}$.
> 如果你想让我把$\bold{w}$和$\bold{v}$设置为两个不垂直的方向，就必须做出一些让步——在这个方案中，我将按照你想要的方式设置所有内容，除了我将对$\bold{v}$做最小的改变，使它实际上垂直于$\bold{w}$。
>
> What will go wrong with the computation if $\bold{a}$ and $\bold{b}$ are parallel?
> 如果$\bold{a}$和$\bold{b}$是平行的，计算会出现什么问题?

### 2.4.8 Squaring Up a Basis 建立基坐标

Occasionally you may find problems caused in your computations by a basis that is supposed to be orthonormal but where error has crept in-due to rounding error in computation, or to the basis having been stored in a file with low precision, for instance.
有时，您可能会发现计算中出现的问题是由本应正交的基导致的，但由于计算中的舍入误差，或者基被存储在低精度文件中，错误已经悄然出现。

The procedure of the previous section can be used; simply constructing the basis anew using the existing $\bold{w}$ and $\bold{v}$ vectors will produce a new basis that is orthonormal and is close to the old one.
可以使用上一节的过程； 只需使用现有的 $\bold{w}$ 和 $\bold{v}$ 向量重新构建基础，就会产生一个正交且接近旧基础的新基础。

This approach is good for many applications, but it is not the best available. It does produce accurately orthogonal vectors, and for nearly orthogonal starting bases the result will not stray far from the starting point. However, it is asymmetric: it “favors” $\bold{w}$ over $\bold{v}$ and $\bold{v}$ over $\bold{u}$ (whose starting value is thrown away).It chooses a basis close to the starting basis but has no guarantee of choosing the closest orthonormal basis. When this is not good enough, the SVD (Section 5.4.1)can be used to compute an orthonormal basis that is guaranteed to be closest to the original basis.
这种方法适用于许多应用程序，但并不是最好的方法。 它确实产生准确的正交向量，并且对于几乎正交的起始基，结果不会偏离起始点太远。 然而，它是不对称的：它“青睐”$\bold{w}$ 而不是 $\bold{v}$，并且“青睐”$\bold{v}$ 而不是 $\bold{u}$（其起始值被丢弃）。 它选择接近起始基础的基础，但不能保证选择最接近的正交基础。 当这还不够好时，SVD（第 5.4.1 节）可用于计算保证最接近原始基的正交基。

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

It is interesting to note that $f$ does have values for all $(x, y)$. We can think of $f$ as a terrain, with sea level at $f = 0$ (Figure 2.22). The shore is the implicit curve. The value of $f$ is the altitude. Another thing to note is that the curve partitions space into regions where $f > 0$, $f < 0$, and $f = 0$. So you evaluate $f$ to decide whether a point is “inside" a curve. Note that $f(x,y) = c$ is a curve for any constant $c$, and $c = 0$ is just used as a convention. For example, if $f(x, y) = x^2 +y^2 - 1$, varying $c$ just gives a variety of circles centered at the origin (Figure 2.23)
有趣的是，$f$ 确实具有所有 $(x, y)$ 的值。 我们可以将 $f$ 视为一个地形，海平面为 $f = 0$（图 2.22）。 海岸是隐式曲线。 $f$ 的值是海拔高度。 另一件需要注意的事情是，曲线将空间划分为 $f > 0$、$f < 0$ 和 $f = 0$ 的区域。 因此，您可以评估 $f$ 来确定某个点是否在曲线“内部”。请注意，$f(x,y) = c$ 是任何常数 $c$ 的曲线，而 $c = 0$ 仅用作 例如，如果 $f(x, y) = x^2 +y^2 - 1$，则改变 $c$ 只会给出以原点为中心的各种圆（图 2.23）
<img src=".\Images\Figure 2.22.png" alt="Figure 2.22" style="zoom:67%;" />
Figure 2.22. An implicit function $f(x,y) = 0$ can be thought of as a height field where $f$ is the height (top). A path where the height is zero is the implicit curve (bottom).
图 2.22。 隐式函数 $f(x,y) = 0$ 可以被视为高度字段，其中 $f$ 是高度（顶部）。 高度为零的路径是隐式曲线（底部）。

![Figure 2.23](.\Images\Figure 2.23.png)
Figure 2.23. An implicit function $f(x,y) = 0$ can be thought of as a height field where $f$ is the height (top). A path where the height is zero is the implicit curve (bottom)
图 2.23。 隐式函数 $f(x,y) = 0$ 可以被视为高度字段，其中 $f$ 是高度（顶部）。 高度为零的路径是隐式曲线（下)

We can compress our notation using vectors. If we have $\bold{c} = (x_c, y_c)$ and $\bold{p} = (x, y)$, then our circle with center c and radius r is defined by those position vectors that satisfy
我们可以使用向量来压缩我们的符号。 如果我们有 $\bold{c} = (x_c, y_c)$ 和 $\bold{p} = (x, y)$，那么以 c 为中心、以 r 为半径的圆由满足以下条件的位置向量定义：
$(\bold{p} - \bold{c} )\cdot (\bold{p} - \bold{c}) -r^2 = 0$

This equation, if expanded algebraically, will yield Equation (2.9), but it is easier to see that this is an equation for a circle by “reading” the equation geometrically. It reads, “points $\bold{p}$ on the circle have the following property: the vector from $\bold{c}$ to $\bold{p}$ when dotted with itself has value $r^2$." Because a vector dotted with itself is just its own length squared, we could also read the equation as, “points $\bold{p}$ on the circle have the following property: the vector from $\bold{c}$ to $\bold{p}$ has squared length $r^2$."
这个方程如果用代数展开，将得到方程（2.9），但通过几何“解读”方程，更容易看出这是一个圆方程。 它写道：“圆上的点 $\bold{p}$ 具有以下属性：从 $\bold{c}$ 到 $\bold{p}$ 的向量在点上自身时具有值 $r^2$。 因为用自身点缀的向量只是其自身长度的平方，所以我们也可以将方程读作“圆上的点 $\bold{p}$ 具有以下属性：从 $\bold{c}$ 到 $\bold{c}$ 的向量 $\bold{p}$ 的长度为 $r^2$ 的平方。”

Even better, is to observe that the squared length is just the squared distance from $\bold{c}$ to $\bold{p}$, which suggests the equivalent form
更好的是，观察到平方长度只是从 $\bold{c}$ 到 $\bold{p}$ 的平方距离，这表明了等效形式
$\|\bold{p} - \bold{c}\|^2 - r^2 = 0$

and, of course, this suggests
当然，这表明
$\|\bold{p} - \bold{c}\| - r = 0$

The above could be read “the points $\bold{p}$ on the circle are those a distance $r$ from the center point $\bold{c}$,which is as good a definition of circle as any. This illustrates that the vector form of an equation often suggests more geometry and intuition than the equivalent full-blown Cartesian form with $x$ and $y$. For this reason, itis usually advisable to use vector forms when possible. In addition, you can support a vector class in your code; the code is cleaner when vector forms are used. The vector-oriented equations are also less error prone in implementation: once you implement and debug vector types in your code, the cut-and-paste errors involving $x$, $y$, and $z$ will go away. It takes a little while to get used to vectors in these equations, but once you get the hang of it, the payoff is large.
上面的内容可以理解为“圆上的点 $\bold{p}$ 是距中心点 $\bold{c}$ 距离 $r$ 的点，这是圆的一个很好的定义。 这说明方程的矢量形式通常比带有 $x$ 和 $y$ 的等效完整笛卡尔形式暗示更多的几何形状和直觉。 因此，通常建议尽可能使用载体形式。 此外，您可以在代码中支持向量类； 使用向量形式时代码更清晰。 面向向量的方程在实现中也不易出错：一旦在代码中实现和调试向量类型，涉及 $x$、$y$ 和 $z$ 的剪切和粘贴错误就会消失。 需要一些时间来适应这些方程中的向量，但一旦掌握了它的窍门，回报是巨大的。

### 2.5.2 The 2D Gradient 2D 渐变

If we think of the function $f(x, y)$ as a height field with $height = f(x,y)$, the gradient vector points in the direction of maximum upslope, i.e., straight uphill. The gradient vector $\nabla f(x, y)$ is given by 
如果我们将函数 $f(x, y)$ 视为一个高度场，其中 $height = f(x,y)$，则梯度向量指向最大上坡方向，即笔直上坡。 梯度向量 $\nabla f(x, y)$ 由下式给出
$\nabla f(x, y) = \left(\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}\right) \\$ 

The gradient vector evaluated at a point on the implicit curve $f(x,y) = 0$ is perpendicular to the tangent vector of the curve at that point. This perpendicular vector is usually called the normal vector to the curve. In addition, since the gradient points uphill, it indicates the direction of the $f(x, y) > 0$ region.
在隐式曲线 $f(x,y) = 0$ 上的一点处计算的梯度向量垂直于该点处曲线的切向量。 该垂直矢量通常称为曲线的法向矢量。 另外，由于梯度指向上坡，因此它指示$f(x,y) > 0$区域的方向。

In the context of height fields, the geometric meaning of partial derivatives and gradients is more visible than usual. Suppose that near the point $(a, b)$, $f(x, y)$ is a plane (Figure 2.24). There is a specific uphill and downhill direction. At right angles to this direction s a direction that is level with respect to the plane. Any intersection between the plane and the $f(x,y) = 0$ plane will be in the direction that is level. Thus the uphill/downhill directions will be perpendicular to the line of intersection $f(x, y) = 0$. To see why the partial derivative has something to do with this, we need to visualize its geometric meaning. Recall that the conventional derivative of a 1D function $y = g(x)$ is
在高度场的背景下，偏导数和梯度的几何意义比平常更明显。 假设在点$(a,b)$附近，$f(x,y)$是一个平面（图2.24）。 有特定的上坡和下坡方向。 与该方向成直角的是相对于平面水平的方向。 该平面与 $f(x,y) = 0$ 平面之间的任何交点都将沿水平方向。 因此，上坡/下坡方向将垂直于交线 $f(x, y) = 0$。 为了明白为什么偏导数与此有关，我们需要形象化它的几何意义。 回想一下，一维函数 $y = g(x)$ 的常规导数是
<img src=".\Images\Figure 2.24.png" alt="Figure 2.24" style="zoom:67%;" />
Figure 2.24. A surface $height = f(x, y)$ is locally planar near $(x,y) = (a,b)$. The gradient is a projection of the up-hill direction onto the $height = 0$ plane.
图 2.24.  表面 $height = f(x, y)$ 在 $(x,y) = (a,b)$ 附近局部为平面。 梯度是上山方向在 $height = 0$ 平面上的投影。
$$
\frac{dy}{dx} = \lim\limits_{\Delta x\to 0}\frac{\Delta y}{\Delta x} = 
\lim\limits_{\Delta x\to 0}\frac{g(x + \Delta x) - g(x)}{\Delta x} \ \ \ \ (2.10)
$$
This measures the slope of the tangent line to $g$ (Figure 2.25)
这测量了 $g$ 切线的斜率（图 2.25）
![Figure 2.25](.\Images\Figure 2.25.png)
Figure 2.25. The derivative of a 1D function measures the slope of the line tangent to the curve.
图 2.25  一维函数的导数测量与曲线相切的直线的斜率

The partial derivative is a generalization of the 1D derivative. For a 2D function $f(x,y)$, we can't take the same limit for $x$ as in Equation (2.10), because $f$ can change in many ways for a given change in $x$. However, if we hold $y$ constant, we can define an analog of the derivative, called the partial derivative(Figure 2.26):
偏导数是一维导数的推广。 对于 2D 函数 $f(x,y)$，我们不能对 $x$ 采取与等式 (2.10) 中相同的限制，因为对于 $x$ 的给定变化，$f$ 可以以多种方式变化。 然而，如果我们保持 $y$ 不变，我们可以定义导数的模拟，称为偏导数（图 2.26）：
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

As an example of the gradient, consider the implicit circle $x^2 + y^2 - 1 = 0$ with gradient vector $(2x,2y)$, indicating that the outside of the circle is the positive region for the function $f(x,y) = x^2 + y^2 - 1$. Note that the length of the gradient vector can be different depending on the multiplier in the implicit equation. For example, the unit circle can be described by $Ax^2 + Ay^2 - A = 0$ for any nonzero $A$. The gradient for this curve is $(2Ax, 2Ay)$. This will be normal (perpendicular) to the circle, but will have a length determined by $A$. For $A > 0$, the normal will point outward from the circle, and for $A < 0$, it will point inward. This switch from outward to inward is as it should be, since the positive region switches inside the circle. In terms of the height-field view, $h = Ax^2 + Ay^2 - A$, and the circle is at zero altitude. For $A > 0$, the circle encloses a depression, and for $A < 0$, the circle encloses a bump. As $A$ becomes more negative, the bump increases in height, but the $h = 0$ circle doesn't change. The direction of maximum uphill doesn't change, but the slope increases. The length of the gradient reflects this change in degree of the slope. So intuitively, you can think of the gradient's direction as pointing uphill and its magnitude as measuring how uphill the slope is.
作为梯度的示例，考虑带有梯度向量 $(2x,2y)$ 的隐式圆 $x^2 + y^2 - 1 = 0$，表示圆的外部是函数 $f  (x,y) = x^2 + y^2 - 1$的正区域。 请注意，梯度向量的长度可能会有所不同，具体取决于隐式方程中的乘数。 例如，对于任何非零 $A$，单位圆可以通过 $Ax^2 + Ay^2 - A = 0$ 来描述。 该曲线的梯度为 $(2Ax, 2Ay)$。 这将垂直于圆，但其长度由 $A$ 确定。 对于 $A > 0$，法线将从圆指向外，而对于 $A < 0$，法线将指向圆内。 这种从外向内的切换是理所应当的，因为正区域在圆内切换。 就高度场视图而言，$h = Ax^2 + Ay^2 - A$，圆的高度为零。 对于 $A > 0$，圆圈包围凹陷，对于 $A < 0$，圆圈包围凸起。 随着 $A$ 变得更负，凹凸的高度会增加，但 $h = 0$ 圆圈不会改变。 最大上坡方向不变，但坡度增加。 坡度的长度反映了坡度的变化。 直观上，您可以将梯度的方向视为指向上坡，将其大小视为测量坡度的坡度。

#### Implicit 2D Lines 隐式二维直线

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

One reason the slope-intercept form is sometimes awkward is that it can't represent some lines such as $x = 0$ because $m$ would have to be infinite. For this reason, a more general form is often useful:
斜率截距形式有时很尴尬的原因之一是它无法表示某些线，例如 $x = 0$，因为 $m$ 必须是无限的。 因此，更通用的形式通常很有用：
$$
Ax + By + C = 0 \ \ \ \ \ (2.15)
$$
for real numbers $A$, $B$, $C$
对于实数$A$, $B$, $C$

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
我们可以从任何垂直于 $(x_1 - x_0, y_1 - y_0)$ 的 $(A, B)$ 开始。 这样的向量就是 $(A, B) = (y_0 - y_1, x_1 - x_0)$，其推理与第 2.5.2 节中相同。 这意味着通过 $(x_0, y_0)$ 和 $(x_1, y_1)$ 的直线方程为
$$
(y_0 - y_1)x + (x_1 - x_0) + C = 0 \ \ \ \ \ (2.16)
$$
Now we just need to find $C$. Because $(x_0, y_0)$ and $(x_1, y_1)$ are on the line, they must satisfy Equation (2.16). We can plug either value in and solve for $C$. Doing this for $(x_0, y_0)$ yields $C = x_0y_1 - x_1y_0$, and thus the full equation for the line is
现在我们只需要找到$C$。 由于 $(x_0, y_0)$ 和 $(x_1, y_1)$ 在线，因此它们必须满足方程（2.16）。 我们可以代入任一值并求解 $C$。 对 $(x_0, y_0)$ 执行此操作会产生 $C = x_0y_1 - x_1y_0$，因此该线的完整方程为
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
![Figure 2.30](G:\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 2.30.png)
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

### 2.5.3 3D Implicit Surfaces

Just as implicit equations can be used to define curves in 2D, they can be used to define surfaces in 3D. As in 2D, implicit equations implicitly define a set of points that are on the surface:
正如隐式方程可用于定义 2D 曲线一样，它们也可用于定义 3D 曲面。 与 2D 中一样，隐式方程隐式定义表面上的一组点：
$f(x, y, z) = 0$

Any point $(x, y, z)$ that is on the surface results in zero when given as an argument to $f$. Any point not on the surface results in some number other than zero. You can check whether a point is on the surface by evaluating $f$, or you can check which side of the surface the point lies on by looking at the sign of $f$, but you cannot always explicitly construct points on the surface. Using vector notation,we will write such functions of $\bold{p} = (x,y,z)$ as
当作为 $f$ 的参数给出时，表面上的任何点 $(x, y, z)$ 都会导致零。 不在表面上的任何点都会产生非零的数字。 您可以通过评估 $f$ 来检查点是否在曲面上，也可以通过查看 $f$ 的符号来检查点位于曲面的哪一侧，但您不能总是在曲面上显式构造点。 使用向量表示法，我们将 $\bold{p} = (x,y,z)$ 的函数写为
$f(\bold{p}) = 0$

### 2.5.4 Surface Normal to an Implicit Surface

A surface normal (which is needed for lighting computations, among other things)is a vector perpendicular to the surface. Each point on the surface may have a different normal vector. In the same way that the gradient provides a normal to an implicit curve in 2D, the surface normal at a point $\bold{p}$ on an implicit surface is given by the gradient of the implicit function
表面法线（除其他外，照明计算所需）是垂直于表面的向量。 表面上的每个点可能具有不同的法向量。 与梯度提供 2D 隐式曲线法线的方式相同，隐式曲面上点 $\bold{p}$ 处的曲面法线由隐式函数的梯度给出
$\bold{n} = \nabla f(\bold{p}) = \left(\frac{\partial f(\bold{p})}{\partial x }, \frac{\partial f(\bold{p})}{\partial y }, \frac{\partial f(\bold{p})}{\partial z }\right)\\$

The reasoning is the same as for the 2D case: the gradient points in the direction of fastest increase in $f$, which is perpendicular to all directions tangent to the surface, in which $f$ remains constant. The gradient vector points toward the side of the surface where $f(\bold{p}) > 0$, which we may think of as “into" the surface or “out from” the surface in a given context. If the particular form of $f$ creates inward-facing gradients, and outward-facing gradients are desired, the surface $-f(\bold{p}) = 0$ is the same as surface $f(\bold{p}) = 0$ but has directionally reversed gradients, i.e., $-\nabla f(p) =  \nabla (-f(p))$.
推理与 2D 情况相同：梯度点位于 $f$ 增加最快的方向，该方向垂直于与表面相切的所有方向，其中 $f$ 保持恒定。 梯度向量指向 $f(\bold{p}) > 0$ 的表面一侧，我们可以将其视为在给定上下文中“进入”表面或“离开”表面。 $f$ 的形式创建向内的渐变，并且需要向外的渐变，表面 $-f(\bold{p}) = 0$ 与表面 $f(\bold{p}) = 0 相同 $ 但具有方向相反的梯度，即 $-\nabla f(p) = \nabla (-f(p))$。

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
阅读该方程的几何方法是，平行六面体的体积由 $\bold{p} - \bold{a}$、$\bold{b} - \bold{a}$ 和 $\bold{c 定义 } - \bold{a}$ 为零，即它们共面。 仅当 $\bold{p}$ 与 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 在同一平面时，这才成立。 完整的笛卡尔表示由行列式给出（这将在第 5.3 节中更详细地讨论）：
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
方程（2.22）和（2.23）是等价的，比较它们是有启发性的。 方程（2.22）很容易从几何角度解释，并且会产生高效的代码。 此外，如果利用调试后的叉乘和点乘代码，则相对容易避免编译成不正确代码的印刷错误。 方程 (2.23) 也很容易从几何角度解释，并且只要实现高效的 3 x 3 行列式函数，它就会很有效。 如果函数 $determinant(\bold{a}, \bold{b}, \bold{c})$ 可用，则也很容易实现而不会出现拼写错误。 如果您重命名行列式函数体积，其他人将特别容易阅读您的代码。 因此方程（2.22）和（2.23）都可以很好地映射到代码中。 将任一方程完全展开为 $x-$、$y-$ 和 $z-$ 分量都可能会产生拼写错误。 此类拼写错误很可能会被编译，因此特别令人讨厌。 这是一个很好的例子，干净的数学生成干净的代码，臃肿的数学生成臃肿的代码。

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
这里$(x,y)$是曲线上的点，t是影响曲线的参数。 对于给定的$t$，存在由函数$g$和$h$确定的某个点。 对于连续的 $g$ 和 $h$，$t$ 的微小变化将导致 $x$ 和 $y$ 的微小变化。 因此，随着 $t$ 不断变化，点会以连续曲线的形式被扫出。 这是一个很好的功能，因为我们可以使用参数 $t$ 显式地构造曲线上的点。 通常我们可以写出矢量形式的参数曲线，
$\bold{p} = f(t)$

where $f$ is a vector-valued function. $f :\R \mapsto \R^2$ .Such vector functions can generate very clean code, so they should be used when possible.
其中 $f$ 是向量值函数。 $f :\R \mapsto \R^2$ 。此类向量函数可以生成非常干净的代码，因此应尽可能使用它们。

We can think of the curve with a position as a function of time. The curve can go anywhere and could loop and cross itself. We can also think of the curve as having a velocity at any point. For example, the point $\bold{p}(t)$ is traveling slowly near $t = -2$ and quickly between $t = 2$ and $t = 3$. This type of “moving point“ vocabulary is often used when discussing parametric curves even when the curve is not describing a moving point.
我们可以将位置视为时间的函数的曲线。 曲线可以去任何地方，并且可以循环和交叉。 我们还可以认为曲线在任意点都有速度。 例如，点 $\bold{p}(t)$ 在 $t = -2$ 附近缓慢移动，并在 $t = 2$ 和 $t = 3$ 之间快速移动。 在讨论参数曲线时，即使曲线没有描述移动点，也经常使用这种类型的“移动点”词汇。

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
为了确保曲线上的每个点都有唯一的参数 $\varphi$，我们可以限制其域： $\varphi \in [0, 2\pi)$ 或 $\varphi \in (-\pi, \ pi]$ 或任何其他长度为 $2\pi$ 的半开区间。

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

The derivative of $\bold{p}$, then, gives two tangent vectors at any point on the sur-face. The normal to the surface may be found by taking the cross product of these vectors: since both are tangent to the surface, their cross product, which is perpendicular to both tangents, is normal to the surface. The right-hand rule for cross products provides a way to decide which side is the front, or outside, of the surface; we will use the convention that the vector
然后，$\bold{p}$ 的导数给出了表面上任意点的两个切向量。 可以通过取这些向量的叉积来找到表面的法线：由于两者都与表面相切，因此垂直于两条切线的它们的叉积垂直于表面。 叉积的右手定则提供了一种方法来确定哪一侧是曲面的正面或外侧； 我们将使用向量的约定
$\bold{n} = \bold{p}_u \cross \bold{p}_v$

points toward the outside of the surface.
指向表面的外侧。

### 2.5.9 Summary of Curves and Surfaces 曲线和曲面总结

Implicit curves in 2D or surfaces in 3D are defined by scalar-valued functions of two or three variables, $f : \R^2 \rightarrow \R$ or $f : \R^3 \rightarrow \R$, and the surface consists of all points where the function is zero:
2D 中的隐式曲线或 3D 中的曲面由两个或三个变量的标量值函数 $f : \R^2 \rightarrow \R$ 或 $f : \R^3 \rightarrow \R$ 和曲面定义 由函数为零的所有点组成：
$S = \{\bold{p} | f(\bold{p}) = 0\}$

Parametric curves in 2D or 3D are defined by vector-valued functions of one variable, $\bold{p} : D  \subset \R \rightarrow \R^2$ or $\bold{p} : D \subset \R \rightarrow \R^3$, and the curve is swept out as $t$ varies over all of $D$:
2D 或 3D 参数曲线由一个变量的向量值函数定义， $\bold{p} : D \subset \R \rightarrow \R^2$ 或 $\bold{p} : D \subset \R \rightarrow \R ^3$，并且随着 $t$ 在所有 $D$ 上变化，曲线被扫除：
$S = \{\bold{p}(t)| t\in D\}.$

Parametric surfaces in 3D are defined by vector-valued functions of two variables, $\bold{p} : D \subset \R^2 \rightarrow \R^3$, and the surface consists of the images of all points $(u, v)$ in the domain:
3D 中的参数化曲面由两个变量的向量值函数 $\bold{p} : D \subset \R^2 \rightarrow \R^3$ 定义，并且该曲面由所有点 $(u , v)$ 在域中：
$S = \{\bold{p}(t)| (u,v) \in D\}.$

For implicit curves and surfaces, the normal vector is given by the derivative of $f$ (the gradient), and the tangent vector (for a curve) or vectors (for a surface) can be derived from the normal by constructing a basis.
对于隐式曲线和曲面，法线向量由$f$（梯度）的导数给出，并且可以通过构造基从法线导出切向量（对于曲线）或向量（对于曲面）  

For parametric curves and surfaces, the derivative of $\bold{p}$ gives the tangent vector(for a curve) or vectors (for a surface), and the normal vector can be derived from the tangents by constructing a basis.
对于参数曲线和曲面，$\bold{p}$ 的导数给出切向量（对于曲线）或向量（对于曲面），并且可以通过构造基从切线导出法向量。

## 2.6 Linear Interpolation 线性插值

Perhaps the most common mathematical operation in graphics is linear interpolation. We have already seen an example of linear interpolation of position to form line segments in 2D and 3D, where two points $\bold{a}$ and $\bold{b}$ are associated with a parameter $t$ to form the line $\bold{p} = (1 - t)\bold{a} + t\bold{b}$. This is interpolation because $\bold{p}$ goes through $\bold{a}$ and $\bold{b}$ exactly at $t = 0$ and $t = 1$. It is linear interpolation because the weighting terms $t$ and $1 - t$ are linear polynomials of $t$.
也许图形中最常见的数学运算是线性插值。 我们已经看到了在 2D 和 3D 中通过位置线性插值形成线段的示例，其中两个点 $\bold{a}$ 和 $\bold{b}$ 与参数 $t$ 关联以形成线 $\bold{p} = (1 - t)\bold{a} + t\bold{b}$。 这是插值，因为 $\bold{p}$ 恰好在 $t = 0$ 和 $t = 1$ 处经过 $\bold{a}$ 和 $\bold{b}$。 它是线性插值，因为加权项 $t$ 和 $1 - t$ 是 $t$ 的线性多项式。

Another common linear interpolation is among a set of positions on the x-axis: $x_0, x_1, ..., x_n$, and for each $x_i$ we have an associated height, $y_i$. We want to create a continuous function $y = f(x)$ that interpolates these positions, so that $f$ goes through every data point, i.e., $f(x_i) = y_i$. For linear interpolation, the points$(x_i, y_i)$ are connected by straight line segments. It is natural to use parametric line equations for these segments. The parameter $t$ is just the fractional distance between $x_i$ and $x_{i+1}$:
另一种常见的线性插值是在 x 轴上的一组位置之间进行：$x_0、x_1、...、x_n$，对于每个 $x_i$，我们都有一个关联的高度 $y_i$。 我们想要创建一个连续函数 $y = f(x)$ 来插值这些位置，以便 $f$ 遍历每个数据点，即 $f(x_i) = y_i$。 对于线性插值，点$(x_i, y_i)$ 通过直线段连接。 对这些段使用参数线方程是很自然的。 参数 $t$ 只是 $x_i$ 和 $x_{i+1}$ 之间的小数距离：
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

If we have a 2D triangle defined by 2D points $\bold{a}$, $\bold{b}$. and $\bold{c}$. we can first find its area:
如果我们有一个由 2D 点 $\bold{a}$、$\bold{b}$ 定义的 2D 三角形。 和$\bold{c}$。 我们首先可以求出它的面积：
$$
area = \frac{1}{2}
\begin{vmatrix}x_b - x_a & x_c - x_a \\ y_b - y_a& y_c - y_a\\\end{vmatrix}
 = \frac{1}{2}(x_ay_b + x_by_c + x_cy_a - x_ay_c - x_by_a - x_cy_b) \ \ \ (2.27)
$$
The derivation of this formula can be found in Section 5.3. This area will have a positive sign if the points $\bold{a}$, $\bold{b}$, and $\bold{c}$ are in counterclockwise order and a negative sign,otherwise.
这个公式的推导可以在5.3节中找到。 如果点 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 按逆时针顺序，则该区域的符号为正，否则符号为负。

Often in graphics, we wish to assign a property, such as color, at each triangle vertex and smoothly interpolate the value of that property across the triangle. There are a variety of ways to do this, but the simplest is to use barycentric coordinates. One way to think of barycentric coordinates is as a nonorthogonal coordinate system as was discussed briefly in Section 2.4.2. Such a coordinate system is shown in Figure 2.36, where the coordinate origin is a and the vectors from $\bold{a}$, $\bold{b}$, and $\bold{c}$ are the basis vectors. With that origin and those basis vectors, any point $\bold{p}$ can be written as
通常在图形中，我们希望在每个三角形顶点分配一个属性，例如颜色，并在整个三角形上平滑地插入该属性的值。 有多种方法可以做到这一点，但最简单的是使用重心坐标。 考虑重心坐标的一种方法是将其视为非正交坐标系，如第 2.4.2 节中简要讨论的那样。 这样的坐标系如图2.36所示，其中坐标原点为a，来自$\bold{a}$、$\bold{b}$和$\bold{c}$的向量是基向量。 有了原点和基向量，任何点 $\bold{p}$ 都可以写成
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
重心坐标乍一看似乎是一个抽象且不直观的结构，但事实证明它们非常强大且方便。 您可能会发现，考虑在有两组平行街道但这些街道不成直角的城市中街道地址如何工作很有用。 自然系统本质上是重心坐标，您很快就会习惯它们。 为平面上的所有点定义重心坐标。 重心坐标的一个特别好的特征是，点 $\bold{p}$ 位于由 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$ 形成的三角形内部，如果并且 除非
$0 < α < 1, \\
0 < β < 1,\\
0 < γ < 1  $

If one of the coordinates is zero and the other two are between zero and one, then you are on an edge. If two of the coordinates are zero, then the other is one, and you are at a vertex. Another nice property of barycentric coordinates is that Equation (2.29) in effect mixes the coordinates of the three vertices in a smooth way. The same mixing coefficients $(α, β, γ)$ can be used to mix other properties, such as color, as we will see in the next chapter.
如果其中一个坐标为零，而另外两个坐标介于 0 和 1 之间，那么您就处于边缘。 如果其中两个坐标为零，则另一个坐标为 1，此时您位于顶点。 重心坐标的另一个很好的特性是方程（2.29）实际上以平滑的方式混合了三个顶点的坐标。 相同的混合系数 $(α, β, γ)$ 可用于混合其他属性，例如颜色，我们将在下一章中看到。

Given a point p, how do we compute its barycentric coordinates? One way is to write Equation (2.28) as a linear system with unknowns $β$ and $γ$, solve, and set $α = 1 - β - γ$. That linear system is 
给定一个点 p，我们如何计算它的重心坐标？ 一种方法是将方程 (2.28) 写为具有未知数 $β$ 和 $γ$ 的线性系统，求解并设置 $α = 1 - β - γ$。 该线性系统是
$$
\begin{bmatrix}x_b - x_a & x_c - x_a \\y_b - y_a & y_c - y_a \\\end{bmatrix} \begin{bmatrix}\beta \\ \gamma \end{bmatrix}
= \begin{bmatrix}x_p - x_a \\ y_p - y_a \end{bmatrix} \ \ \ \ \ (2.31)
$$
Although it is straightforward to solve Equation (2.31) algebraically, it is often fruitful to compute a direct geometric solution.
虽然用代数方法求解方程（2.31）很简单，但计算直接的几何解通常是富有成效的。

One geometric property of barycentric coordinates is that they are the signed scaled distance from the lines through the triangle sides, as is shown for $\beta$ in Figure 2.37. Recall from Section 2.5.2 that evaluating the equation $f(x, y)$ for the line $f(x,y) = 0$ returns the scaled signed distance from $(x,y)$ to the line. Also recall that if $f(x,y) = 0$ is the equation for a particular line, so is $kf(x, y) = 0$ for any nonzero $k$. Changing $k$ scales the distance and controls which side of the line has positive signed distance, and which negative. We would like to choose $k$ such that, for example, $kf(x,y) = \beta$. Since $k$ is only one unknown, we can force this with one constraint, namely that at point $\bold{b}$ we know $\beta = 1$. So if the line $f_{ac}(x, y) = 0$ goes through both $\bold{a}$ and $\bold{c}$, then we can compute $\beta$ for a point $(x, y)$ as follows:
重心坐标的一个几何属性是它们是从穿过三角形边的线到带符号的缩放距离，如图 2.37 中的 $\beta$ 所示。 回想一下第 2.5.2 节，对线 $f(x,y) = 0$ 计算方程 $f(x, y)$ 会返回从 $(x,y)$ 到线的缩放符号距离。 另请记住，如果 $f(x,y) = 0$ 是特定直线的方程，那么对于任何非零 $k$，$kf(x, y) = 0$ 也是如此。 更改 $k$ 会缩放距离并控制线的哪一侧具有正符号距离，哪一侧具有负符号距离。 我们希望选择 $k$，例如 $kf(x,y) = \beta$。 由于 $k$ 只是一个未知数，我们可以用一个约束来强制这一点，即在点 $\bold{b}$ 处我们知道 $\beta = 1$。 因此，如果线 $f_{ac}(x, y) = 0$ 同时经过 $\bold{a}$ 和 $\bold{c}$，那么我们可以计算点 $(x , y)$ 如下：
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

No. However, the intersection of two 3D planes defines a 3D line, so a 3D line can be described by two simultaneous implicit 3D equations  
不会。但是，两个 3D 平面的交集定义了一条 3D 线，因此 3D 线可以通过两个联立隐式 3D 方程来描述

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



# 3 Raster Images 光栅图像

Most computer graphics images are presented to the user on some kind of raster display. Raster displays show images as rectangular arrays of pixels. A common example is a flat-panel computer display or television, which has a rectangular array of small light-emitting pixels that can individually be set to different colors to create any desired image. Different colors are achieved by mixing varying intensities of red, green, and blue light. Most printers, such as laser printers and ink-jet printers, are also raster devices. They are based on scanning: there is no physical grid of pixels, but the image is laid down sequentially by depositing ink at selected points on a grid.
大多数计算机图形图像都在某种光栅显示器上呈现给用户。 光栅显示器将图像显示为矩形像素阵列。 一个常见的例子是平板计算机显示器或电视，它具有小型发光像素的矩形阵列，可以单独将其设置为不同的颜色以创建任何所需的图像。 通过混合不同强度的红、绿、蓝光获得不同的颜色。 大多数打印机，例如激光打印机和喷墨打印机，也是光栅设备。 它们基于扫描：没有物理像素网格，但通过在网格上的选定点沉积墨水来顺序绘制图像。

> Pixel is short for “picture element.”  
> 像素是“图像元素”的缩写。

Rasters are also prevalent in input devices for images. A digital camera contains an image sensor comprising a grid of light-sensitive pixels, each of which records the color and intensity of light falling on it. A desktop scanner contains a linear array of pixels that is swept across the page being scanned, making many measurements per second to produce a grid of pixels.  
光栅在图像输入设备中也很普遍。 数码相机包含一个由光敏像素网格组成的图像传感器，每个像素记录落在其上的光线的颜色和强度。 桌面扫描仪包含线性像素阵列，该像素阵列扫过正在扫描的页面，每秒进行多次测量以产生像素网格。

> Color in printers is more complicated, involving mixtures of at least four pigments. 
> 打印机中的颜色更为复杂，涉及至少四种颜料的混合物。 

Because rasters are so prevalent in devices, raster images are the most common way to store and process images. A raster image is simply a 2D array that stores the pixel value for each pixel--usually a color stored as three numbers, for red, green, and blue. A raster image stored in memory can be displayed by using each pixel in the stored image to control the color of one pixel of the display.
由于光栅在设备中非常普遍，因此光栅图像是存储和处理图像的最常见方式。 光栅图像只是一个二维数组，它存储每个像素的像素值——通常是存储为三个数字的颜色，即红色、绿色和蓝色。 可以通过使用存储图像中的每个像素来控制显示器的一个像素的颜色来显示存储在存储器中的光栅图像。

> Or, maybe it’s because raster images are so convenient that raster devices are prevalent.  
> 或者，也许是因为光栅图像非常方便，所以光栅设备很流行。

But we don’t always want to display an image this way. We might want to change the size or orientation of the image, correct the colors, or even show the image pasted on a moving three-dimensional surface. Even in televisions, the display rarely has the same number of pixels as the image being displayed. Considerations like these break the direct link between image pixels and display pixels. It's best to think of a raster image as a device-independent description of the image to be displayed, and the display device as a way of approximating that ideal image.
但我们并不总是希望以这种方式显示图像。 我们可能想要更改图像的大小或方向、校正颜色，甚至显示粘贴在移动的三维表面上的图像。 即使在电视中，显示器也很少具有与所显示图像相同数量的像素。 诸如此类的考虑打破了图像像素和显示像素之间的直接联系。 最好将光栅图像视为要显示的图像的独立于设备的描述，并将显示设备视为近似理想图像的一种方式。

There are other ways of describing images besides using arrays of pixels. A vector image is described by storing descriptions of shapes-areas of color bounded by lines or curves-with no reference to any particular pixel grid. In essence this amounts to storing the instructions for displaying the image rather than the pixels needed to display it. The main advantage of vector images is that they are resolution independent and can be displayed well on very high resolution devices. The corresponding disadvantage is that they must be rasterized before they can be displayed. Vector images are often used for text, diagrams, mechanical drawings, and other applications where crispness and precision are important and photographic images and complex shading aren't needed.
除了使用像素数组之外，还有其他描述图像的方法。 矢量图像是通过存储形状的描述（由直线或曲线界定的颜色区域）来描述的，而不参考任何特定的像素网格。 本质上，这相当于存储显示图像的指令，而不是存储显示图像所需的像素。 矢量图像的主要优点是它们与分辨率无关，并且可以在非常高分辨率的设备上很好地显示。 相应的缺点是它们必须经过光栅化才能显示。 矢量图像通常用于文本、图表、机械制图和其他需要清晰和精确且不需要摄影图像和复杂阴影的应用。

In this chapter, we discuss the basics of raster images and displays, paying particular attention to the nonlinearities of standard displays. The details of how pixel values relate to light intensities are important to have in mind when we discuss computing images in later chapters.
在本章中，我们讨论光栅图像和显示的基础知识，特别关注标准显示的非线性。 当我们在后面的章节中讨论计算图像时，必须牢记像素值与光强度之间的关系的详细信息。

> Or: you have to know what those numbers in your image actually mean.
> 或者：您必须知道图像中的这些数字的实际含义。

## 3.1 Raster Devices  光栅设备

Before discussing raster images in the abstract, it is instructive to look at the basic operation of some specific devices that use these images. A few familiar raster devices can be categorized into a simple hierarchy: 
在摘要讨论栅格图像之前，要查看使用这些图像的某些特定设备的基本操作是有帮助的。 一些熟悉的栅格设备可以分为一个简单的层次结构：

- Output
  输出
  - Display
    展示
    - Transmissive: liquid crystal display (LCD)
      传播：液晶显示（LCD）
    - Emissive: light-emitting diode (LED) display
      发射：发光二极管（LED）显示
  - Hardcopy
    硬拷贝
    - Binary: ink-jet printer
      二进制：喷墨打印机
    - Continuous tone: dye sublimation printer
      连续音：染料升华打印机
- Input
  输入
  - 2D array sensor: digital camera
    2D阵列传感器：数码相机
  - 1D array sensor: flatbed scanner 
    1D阵列传感器：平板扫描仪

### 3.1.1 Displays 显示

Current displays,including televisions and digital cinematic projectors as well as displays and projectors for computers, are nearly universally based on fixed arrays of pixels. They can be separated into emissive displays, which use pixels that directly emit controllable amounts of light, and transmissive displays, in which the pixels themselves don't emit light but instead vary the amount of light that they allow to pass through them. Transmissive displays require a light source to illuminate them: in a direct-viewed display this is a backlight behind the array; in a projector it is a lamp that emits light that is projected onto the screen after passing through the array. An emissive display is its own light source.
当前的显示器，包括电视和数字电影投影仪以及计算机的显示器和投影仪，几乎是基于固定的像素阵列的。 它们可以分为发射的显示器，它们使用直接发出可控制量的光线和透射显示器的像素，其中像素本身不会发光，而是改变了它们允许通过它们的光量。 透射显示需要一个光源来照亮它们：在直接查看的显示器中，这是阵列背后的背光； 在投影仪中，这是一盏灯，它在通过阵列后发出的光线会发出的光。 发射显示是其自己的光源。

Light-emitting diode (LED) displays are an example of the emissive type. Each pixel is composed of one or more LEDs, which are semiconductor devices(based on inorganic or organic semiconductors) that emit light with intensity de-pending on the electrical current passing through them (see Figure 3.1).
发光二极管（LED）显示是发射类型的示例。 每个像素由一个或多个LED组成，这些LED是半导体设备（基于无机或有机半导体），它们在通过它们的电流上发出强度的光线发光（见图3.1）。
![Figure 3.1](G:\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 3.1.png)
Figure 3.1. The operation of a light-emitting diode(LED) display.
图3.1  发光二极管（LED)显示的操作

The pixels in a color display are divided into three independently controlled subpixels-one red,one green, and one blue-each with its own LED made using different materials so that they emit light of different colors (Figure 3.2). When the display is viewed from a distance, the eye can't separate the individual subpixels, and the perceived color is a mixture of red, green, and blue.
颜色显示器中的像素分为三个独立控制的子像素 - 一个红色，一个绿色和一个蓝色的蓝色，其LED使用不同的材料制成，因此它们会发出不同的颜色（图3.2）。 当从远处查看显示器时，眼睛无法将单个子像素分开，并且感知到的颜色是红色，绿色和蓝色的混合物。
![Figure 3.2](.\Images\Figure 3.2.png)
Figure 3.2. The red, green, and blue subpixels within a pixel of a flat-panel display
图3.2  平板显示器的像素中的红色，绿色和蓝色子像素

Liquid crystal displays (LCDs) are an example of the transmissive type. A liquid crystal is a material whose molecular structure enables it to rotate the polarization of light that passes through it, and the degree of rotation can be adjusted by an applied voltage. An LCD pixel (Figure 3.3) has a layer of polarizing film behind it, so that it is illuminated by polarized light--let's assume it is polarized horizontally.
液晶显示（LCD）是传播类型的一个例子。 液晶是一种材料，其分子结构使其能够旋转通过它的光的极化，并且旋转程度可以通过施加的电压调节。 LCD像素（图3.3）在其后面有一层偏振膜，因此它被极化光照亮 -  LET假设它是水平偏振的。
![Figure 3.3](.\Images\Figure 3.3.png)

Figure 3.3. One pixel of an LCD display in the off state (bottom), in which the front polarizer blocks all the light that passes the back polarizer, and the on state (top), in which the liquid crystal cell rotates the polarization of the light so that it can pass through the front polarizer. Figure courtesy Erik Reinhard (Reinhard, Khan, Aky¨ uz, & Johnson, 2008).  
图3.3。 一个LCD显示在OFF状态（底部）的像素的像素，前偏振器会阻止所有通过后偏振器的光，以及在状态（顶部），其中液晶细胞旋转光线的偏振 它可以通过前偏振器。 人物埃里克·莱因哈德（Erik Reinhard）（Reinhard，Khan，Aky'uz和Johnson，2008年）

A second layer of polarizing film in front of the pixel is oriented to transmit only vertically polarized light. If the applied voltage is set so that the liquid crystal layer in between does not change the polarization, all light is blocked and the pixel is in the “off” (minimum intensity) state. If the voltage is set so that the liquid crystal rotates the polarization by 90 degrees, then all the light that entered through the back of the pixel will escape through the front, and the pixel is fully “on-it has its maximum intensity. Intermediate voltages will partly rotate the polarization so that the front polarizer partly blocks the light, resulting in intensities between the minimum and maximum (Figure 3.4). Like color LED displays, color LCDs have red, green, and blue subpixels within each pixel, which are three independent pixels with red, green, and blue color filters over them.
在像素前面的第二层偏振膜定向仅传输垂直极化的光。 如果设置了施加的电压，以使之间的液晶层不会改变极化，则所有光被阻塞，并且像素在“ OFF”（最小强度）状态中。 如果设置了电压，以使液晶旋转极化90度，则通过像素背面输入的所有光将通过前部逸出，并且Pixel完全“ On-On-in-IT具有最大强度”。 中间电压将部分旋转偏振，以使前偏振器部分阻断光，从而导致最小值和最大值之间的强度（图3.4）。 像颜色LED显示器一样，颜色LCD在每个像素内都具有红色，绿色和蓝色子像素，它们是三个独立的像素，上面有红色，绿色和蓝色的过滤器。
![Figure 3.4](.\Images\Figure 3.4.png)
Figure 3.4.The operation of a liquid crystal display (LCD)
图3.4.液晶显示器(LCD)的操作

Any type of display with a fixed pixel grid, including these and other technologies, has a fundamentally fixed resolution determined by the size of the grid. For displays and images, resolution simply means the dimensions of the pixel grid: if a desktop monitor has a resolution of 1920  1200 pixels, this means that it has 2,304,000 pixels arranged in 1920 columns and 1200 rows.
具有固定像素网格的任何类型的显示器，包括这些技术和其他技术，都具有基本固定的分辨率，该分辨率由网格的大小确定。 对于显示和图像，分辨率仅表示像素网格的尺寸：如果桌面显示器的分辨率为1920 1200像素，这意味着它在1920列和1200行中具有2,304,000像素。

> The resolution of a display is sometimes called its “native resolution” since most displays can handle images of other resolutions, via built-in conversion.  
> 显示屏的分辨率有时称为其“本地分辨率”，因为大多数显示器都可以通过内置转换来处理其他分辨率的图像。

An image of a different resolution, to fill the screen, must be converted into a 1920 x 1200 image using the methods of Chapter 9.
要填充屏幕的不同分辨率的图像必须使用第9章的方法将其转换为1920 x 1200图像。

### 3.1.2 Hardcopy Devices 硬拷贝设备

The process of recording images permanently on paper has very different constraints from showing images transiently on a display. In printing, pigments are distributed on paper or another medium so that when light reflects from the paper it forms the desired image. Printers are raster devices like displays, but many printers can only print binary images-pigment is either deposited or not at each grid position, with no intermediate amounts possible.
在纸上永久录制图像的过程与在显示屏上的瞬时显示图像的约束非常不同。 在印刷中，颜料分布在纸张或其他介质上，因此当光从纸张反射时，它会形成所需的图像。 打印机是像显示器这样的栅格设备，但是许多打印机只能打印二进制图像色调，要么在每个网格位置放置，要么不存放，而无需中间量。

An ink-jet printer (Figure 3.5) is an example of a device that forms a raster image by scanning. An ink-jet print head contains liquid ink carrying pigment, which can be sprayed in very small drops under electronic control. The head moves across the paper, and drops are emitted as it passes grid positions that should receive ink; no ink is emitted in areas intended to remain blank. After each sweep the paper is advanced slightly, and then the next row of the grid is laid down. Color prints are made by using several print heads, each spraying ink with a different pigment, so that each grid position can receive any combination of different colored drops. Because all drops are the same, an ink-jet printer prints binary images: at each grid point there is a drop or no drop; there are no intermediate shades.
喷墨打印机（图3.5）是通过扫描形成光栅图像的设备的一个示例。 喷墨打印头包含液态墨水含有颜料，可以在电子控制下用很小的滴剂喷涂。 头部在纸上移动，并在通过网格位置接收墨水时发出滴头； 旨在保持空白的区域没有发出墨水。 每次扫描后，纸略微提取，然后将下一行放置。 彩色印刷是通过使用几个印刷头制成的，每个印刷头都用不同的颜料喷涂墨水，以便每个网格位置可以接收不同彩色滴剂的任何组合。 由于所有滴剂都是相同的，所以墨水打印机都会打印二进制图像：在每个网格点上都有一个滴剂或没有滴； 没有中间阴影。
![Figure 3.5](.\Images\Figure 3.5.png)
Figure 3.5.The operation of an ink-jet printer.
图3.5.墨水打印机的操作。

> There are also continuous ink-jet printers that print in a continuous helical path on paper wrapped around a spinning drum, rather than moving the head back and forth 
> 还有连续的喷墨打印机，它们在包裹在旋转鼓周围的纸上连续的螺旋路径上打印，而不是来回移动头部

An ink-jet printer has no physical array of pixels; the resolution is determined by how small the drops can be made and how far the paper is advanced after each sweep. Many ink-jet printers have multiple nozzles in the print head, enabling several sweeps to be made in one pass, but it is the paper advance, not the nozzle spacing, that ultimately determines the spacing of the rows.
喷墨打印机没有像素的物理数组。 该分辨率取决于每次扫描后可以将滴剂小的小滴以及纸张进去的距离确定。 许多墨水打印机在打印头上有多个喷嘴，可以在一次通行证中进行几次扫描，但这是纸张的前进，而不是喷嘴间距，最终决定了行的间距。

The thermal dye transfer process is an example of a continuous tone printing process, meaning that varying amounts of dye can be deposited at each pixel——it is not all-or-nothing like an ink-jet printer (Figure 3.6). A donor ribbon containing colored dye is pressed between the paper, or dye receiver, and a print head containing a linear array of heating elements, one for each column of pixels in the image. As the paper and ribbon move past the head, the heating elements switch on and off to heat the ribbon in areas where dye is desired, causing the dye to diffuse from the ribbon to the paper. This process is repeated for each of several dye colors. Since higher temperatures cause more dye to be transferred, the amount of each dye deposited at each grid position can be controlled, allowing a continuous range of colors to be produced. The number of heating elements in the print head establishes a fixed resolution in the direction across the page, but the resolution along the page is determined by the rate of heating and cooling compared to the speed of the paper.
热染料转移过程是连续音调打印过程的一个示例，这意味着可以在每个像素上沉积不同量的染料 - 它并不像墨水喷射打印机那样全或整个（图3.6）。 将含有彩色染料的供体色带压在纸之间，或染料接收器之间，以及一个包含线性加热元件的打印头，图像中的每一列像素一列。 随着纸张和色带移动到头部，加热元件打开和关闭以在需要染料的区域加热色带，从而导致染料从色带扩散到纸。 为几种染料颜色中的每一种都重复此过程。 由于较高的温度会导致更大的染料转移，因此可以控制每个网格位置沉积的每个染料的量，从而产生连续的颜色范围。 打印头中的加热元素数量在整个页面上的方向上建立了固定的分辨率，但是沿页面的分辨率与纸张速度相比取决于加热和冷却速率。
![Figure 3.6](.\Images\Figure 3.6.png)
Figure 3.6.The operation of a thermal dye transfer printer.
图3.6. 热染料转移打印机的操作

Unlike displays, the resolution of printers is described in terms of the pixel density instead of the total count of pixels. So a thermal dye transfer printer that has elements spaced 300 per inch across its print head has a resolution of 300 pixels per inch (ppi) across the page. If the resolution along the page is chosen to be the same, we can simply say the printer's resolution is 300 ppi. An ink-jet printer that places dots on a grid with 1200 grid points per inch is described as having a resolution of 1200 dots per inch (dpi). Because the ink-jet printer is a binary device, it requires a much finer grid for at least two reasons. Because edges are abrupt black/white boundaries, very high resolution is required to avoid stair-stepping, or aliasing, from appearing (see Section 8.3). When continuous-tone images are printed,the high resolution is required to simulate intermediate colors by printing varying-density dot patterns called halftones.
与显示不同，打印机的分辨率是用像素密度而不是像素的总数来描述的。 因此，在整个页面上，其打印头的元素每英寸的分辨率为300像素（PPI）。 如果选择页面的分辨率是相同的，我们可以简单地说打印机的分辨率为300 ppi。 将点放在每英寸1200个网格上的点上，将点放在每英寸的分辨率为1200点（DPI）上。 由于喷墨打印机是二进制设备，因此至少有两个原因需要更细网格。 由于边缘是突然的黑色/白色边界，因此需要非常高的分辨率来避免出现楼梯式或混叠（请参见第8.3节）。 当打印连续色调图像时，需要高分辨率来模拟中间颜色，通过打印称为半径的变化密度点图案。

> The term “dpi” is all too often used to mean “pixels per inch,” but dpi should be used in reference to binary devices and ppi in reference to continuous-tone devices 
> “ DPI”一词通常用来表示“每英寸像素”，但是DPI应参考二进制设备和PPI，参考连续音调设备

### 3.1.3 Input Devices 输入设备

Raster images have to come from somewhere, and any image that wasn't computed by some algorithm has to have been measured by some raster input device, most often a camera or scanner. Even in rendering images of 3D scenes, photographs are used constantly as texture maps (see Chapter 11). A raster input device has to make a light measurement for each pixel, and (like output devices)they are usually based on arrays of sensors.
栅格图像必须来自某个地方，并且某些算法未计算的任何图像都必须由某些栅格输入设备（通常是相机或扫描仪）测量。 即使在渲染3D场景的图像中，照片也会不断用作纹理图（请参阅第11章）。 栅格输入设备必须对每个像素进行轻度测量，并且（就像输出设备一样）它们通常基于传感器阵列。

A digital camera is an example of a 2D array input device. The image sensor in a camera is a semiconductor device with a grid of light-sensitive pixels. Two common types of arrays are known as CCDs (charge-coupled devices) and CMOS (complimentary metal-oxide-semiconductor) image sensors. The camera's lens projects an image of the scene to be photographed onto the sensor, and then each pixel measures the light energy falling on it, ultimately resulting in a number that goes into the output image (Figure 3.7). In much the same way as color displays use red, green, and blue subpixels, most color cameras work by using a color-filter array or mosaic to allow each pixel to see only red, green, or blue light, leaving the image processing software to fill in the missing values in a process known as demosaicking (Figure 3.8).
数码相机是2D阵列输入设备的示例。 相机中的图像传感器是具有光敏像素网格的半导体设备。 两种常见类型的阵列称为CCD（电荷耦合设备）和CMOS（免费金属 - 氧化物 - 氧化型）图像传感器。 相机的镜头投射了要在传感器上拍摄的场景的图像，然后每个像素都测量了落在其上的光能，最终导致了输出图像中的数字（图3.7）。 与颜色显示的方式几乎相同，使用红色，绿色和蓝色子像素，大多数颜色相机通过使用颜色滤波器阵列或马赛克来工作，以允许每个像素仅看到红色，绿色或蓝光，从而留下图像处理软件 在演示的过程中填充缺失值（图3.8）。
![Figure 3.7](.\Images\Figure 3.7.png)
Figure 3.7. The operation of a digital camera.
图3.7 数码相机的操作。
![Figure 3.8](.\Images\Figure 3.8.png)
Figure 3.8. Most color digital cameras use a color-filter array similar to the Bayer mosaic shown here. Each pixel measures either red, green, or blue light.  
图3.8  大多数彩色数码相机都使用类似于此处显示的拜耳马赛克的颜色过滤器阵列。 每个像素测量红色，绿色或蓝光。

Other cameras use three separate arrays, or three separate layers in the array, to measure independent red, green, and blue values at each pixel, producing a usable color image without further processing. The resolution of a camera is determined by the fixed number of pixels in the array and is usually quoted using the total count of pixels: a camera with an array of 3000 columns and 2000 rows produces an image of resolution 3000 x 2000, which has 6 million pixels, and is called a 6 megapixel (MP) camera. It's important to remember that a mosaic sensor does not measure a complete color image, so a camera that measures the same number of pixels but with independent red, green, and blue measurements records more information about the image than one with a mosaic sensor.
其他摄像机使用数组中的三个单独的阵列或三个单独的层来测量每个像素的独立红色，绿色和蓝色值，从而产生一个可用的颜色图像而无需进一步处理。 相机的分辨率由数组中的固定像素数确定，通常使用像素的总数：一个3000列和2000行的摄像机产生分辨率3000 x 2000的图像，该图像具有6个，该图像具有6个。 百万像素，被称为6百万像素（MP）相机。 重要的是要记住，马赛克传感器不能测量完整的颜色图像，因此，可以测量相同数量的像素但具有独立的红色，绿色和蓝色测量值的相机记录了有关图像的信息，而不是带有镶嵌传感器的信息。

> People who are selling cameras use “mega” to mean $10^6$, not $2^{20}$ as with megabytes 
> 出售相机的人使用“ Mega”的意思是$ 10^6 $，而不是$ 2^{20} $，就像Megabytes一样

A flatbed scanner also measures red, green, and blue values for each of a grid of pixels, but like a thermal dye transfer printer it uses a 1D array that sweeps across the page being scanned, making many measurements per second. There solution across the page is fixed by the size of the array, and the resolution along the page is determined by the frequency of measurements compared to the speed at which the scan head moves. A color scanner has a $3 \cross n_x$ array, where $n_x$ is the number of pixels across the page, with the three rows covered by red, green, and blue filters. With an appropriate delay between the times at which the three colors are measured, this allows three independent color measurements at each grid point. As with continuous-tone printers, the resolution of scanners is reported in pixels per inch (ppi).
平板扫描仪还测量了每个像素网格的红色，绿色和蓝色值，但是就像热染料传输打印机一样，它使用的是1D阵列，该阵列在扫描的页面上扫过整个页面，每秒进行了许多测量。 整个页面上的解决方案是由数组的大小固定的，并且沿页面的分辨率与扫描头移动的速度相比，由测量频率确定。 颜色扫描仪具有$ 3 \cross n_x $阵列，其中$ n_x $是整个页面上的像素的数量，其中三行被红色，绿色和蓝色过滤器覆盖。 在测量三种颜色的时间之间有适当的延迟，这允许在每个网格点进行三个独立的颜色测量。 与连续的色调打印机一样，扫描仪的分辨率以每英寸像素（PPI）为单位。

> The resolution of a scanner is sometimes called its “optical resolution” since most scanners can produce images of other resolutions, via built-in conversion
> 扫描仪的分辨率有时被称为“光学分辨率”，因为大多数扫描仪都可以通过内置转换产生其他分辨率的图像

With this concrete information about where our images come from and where they will go, we'll now discuss images more abstractly, in the way we'll use them in graphics algorithms.
借助有关图像来自何处以及它们将去向的具体信息，我们现在将更加抽象地讨论图像，就像我们在图形算法中使用它们一样。
![Figure 3.9](.\Images\Figure 3.9.png)
Figure 3.9. The operation of a flatbed scanner.  
图3.9  平板扫描仪的操作

## 3.2 Images, Pixels, and Geometry 图像，像素和几何形状

We know that a raster image is a big array of pixels, each of which stores information about the color of the image at its grid point. We've seen what various output devices do with images we send to them and how input devices derive them from images formed by light in the physical world. But for computations in the computer, we need a convenient abstraction that is independent of the specifics of any device, that we can use to reason about how to produce or interpret the values stored in images.
我们知道，栅格图像是很大的像素，每个像素都在其网格点存储有关图像颜色的信息。 我们已经看到了各种输出设备对发送给它们的图像以及输入设备如何从物理世界中的光形成的图像中得出的方式。 但是，对于计算机中的计算，我们需要一个方便的抽象，该抽象与任何设备的细节无关，我们可以用来推理如何生成或解释图像中存储的值。

When we measure or reproduce images, they take the form of two-dimensional distributions of light energy: the light emitted from the monitor as a function of position on the face of the display; the light falling on a camera's image sensor as a function of position across the sensor's plane; the reflectance, or fraction of light reflected (as opposed to absorbed) as a function of position on a piece of pa-per. So in the physical world, images are functions defined over two-dimensional areas-almost always rectangles. So we can abstract an image as a function
当我们测量或重现图像时，它们采用光能的二维分布的形式：从监视器发出的光作为显示面上的位置的函数； 光线落在相机的图像传感器上是传感器平面上位置的函数； 反射的反射率或部分反射（而不是吸收）是一块pa-per上的位置的函数。 因此，在物理世界中，图像是在二维区域上定义的函数 - 几乎总是矩形。 因此我们可以将图像作为函数抽象
$I(x, y): R\rightarrow V$

> “A pixel is not a little square!”  — Alvy Ray Smith (A. R. Smith, 1995)
> “像素不是一个小正方形！”  -  Alvy Ray Smith（A. R. Smith，1995）

where $R \subset \R^2$ is a rectangular area and V is the set of possible pixel values. The  simplest case is an idealized grayscale image where each point in the rectangle has just a brightness (no color), and we can say $V = \R^+$ (the nonnegative reals). An idealized color image, with red, green, and blue values at each pixel, has $V = (\R^+)^3$. We’ll discuss other possibilities for $V$ in the next section.
其中$ R \subset \R^2 $是矩形区域，$V$是可能的像素值。 最简单的情况是理想化的灰度图像，其中矩形中的每个点都具有亮度（无颜色），我们可以说$ V = \R^+$（非负元素）。 理想化的颜色图像，每个像素处有红色，绿色和蓝色值，具有$ V =(\R^+)^3 $。 我们将在下一节中讨论$ V $的其他可能性。

> Are there any raster devices that are not rectangular?
> 有没有矩形的栅格设备？

How does a raster image relate to this abstract notion of a continuous image? Looking to the concrete examples, a pixel from a camera or scanner is a measurement of the average color of the image over some small area around the pixel. A display pixel, with its red, green, and blue subpixels, is designed so that the average color of the image over the face of the pixel is controlled by the corresponding pixel value in the raster image. In both cases, the pixel value is a local average of the color of the image, and it is called a point sample of the image. In other words, when we find the value x in a pixel, it means “the value of the image in the vicinity of this grid point is x.” The idea of images as sampled representations of functions is explored further in Chapter 9.  
栅格图像与连续图像的这个抽象概念有何关系？ 展望混凝土示例，来自相机或扫描仪的像素是对像素周围某些小区域上图像的平均颜色的测量。 设计像素的显示像素，其红色，绿色和蓝色子像素的设计，以使像素上图像的平均颜色由光栅图像中的相应像素值控制。 在这两种情况下，像素值都是图像颜色的局部平均值，它称为图像的点样本。 换句话说，当我们在像素中找到值x时，它的意思是“该网格点附近图像的值为x”。 在第9章中，进一步探讨了图像作为函数的采样表示的想法。

A mundane but important question is where the pixels are located in 2D space. This is only a matter of convention, but establishing a consistent convention is important! In this book, a raster image is indexed by the pair $(i, j)$ indicating the column $(i)$ and row $(j)$ of the pixel, counting from the bottom left. If an image has $n_x$ columns and $n_y$ rows of pixels, the bottom-left pixel is $(0, 0)$ and the top-right is pixel $(n_x - 1, n_y - 1)$. We need 2D real screen coordinates to specify pixel positions. We will place the pixels’ sample points at integer coordinates, as shown by the 4 x 3 screen in Figure 3.10.
一个平凡但重要的问题是像素在二维空间中的位置。这只是一个惯例的问题，但是建立一个一致的惯例是很重要的!在本书中，栅格图像由一对$(i, j)$索引，表示像素的列$(i)$和行$(j)$，从左下角开始计数。如果图像有$n_x$列和$n_y$行像素，则左下像素为$(0,0)$，右上像素为$(n_x - 1, n_y - 1)$。我们需要2D真实屏幕坐标来指定像素位置。我们将像素的采样点放置在整数坐标上，如图3.10中的4 x 3屏幕所示。
![Figure 3.10](.\Images\Figure 3.10.png)
Figure 3.10. Coordinates of a four pixel × three pixel screen. Note that in some APIs the y-axis will point downward.  
图3.10 4像素× 3像素屏幕的坐标。请注意，在某些api中，y轴将向下指向

> In some APIs, and many file formats, the rows of an image are organized top-to-bottom, so that (0, 0) is at the top left. This is for historical reasons: the rows in analog television transmission started from the top.
> 在某些API和许多文件格式中，图像的行是从上到下组织的，因此（0，0）位于左上方。 这是出于历史原因：模拟电视传输中的行从顶部开始。

> Some systems shift the coordinates by half a pixel to place the sample points halfway between the integers but place the edges of the image at integers.
> 有些系统将坐标移动半个像素，将样本点置于整数的中间，但将图像的边缘置于整数上。

The rectangular domain of the image has width $n_x$ and height $n_y$ and is centered on this grid, meaning that it extends half a pixel beyond the last sample point on each side. So the rectangular domain of a $n_x \cross n_y$ image is
图像的矩形域具有宽度$ n_x $和高度$ n_y $，并以此网格为中心，这意味着它将一半像素延伸到每一侧的最后一个样品点之外。 因此，$ n_x \cross n_y $图像是
$R = [-0.5, n_x - 0.5] \cross [-0.5, n_y - 0.5]$

Again, these coordinates are simply conventions, but they will be important to remember later when implementing cameras and viewing transformations.
同样，这些坐标只是简单的约定，但稍后在实现摄像机和查看转换时记住它们将非常重要。

### 3.2.1 Pixel Values 像素值

So far we have described the values of pixels in terms of real numbers, representing intensity (possibly separately for red, green, and blue) at a point in the image. This suggests that images should be arrays of floating-point numbers, with either one (for grayscale, or black and white, images) or three (for RGB color images) 32-bit floating point numbers stored per pixel. This format is sometimes used, when its precision and range of values are needed, but images have a lot of pixels and memory and bandwidth for storing and transmitting images are invariably scarce. Just one ten-megapixel photograph would consume about 115 MB of RAM in this format.
到目前为止，我们已经描述了图像点的强度（可能是红色，绿色和蓝色）的强度（可能分别为红色，绿色和蓝色）。 这表明图像应该是浮点数的阵列，其中一个（用于灰度或黑白，图像）或三个（对于RGB颜色图像）32位浮点数存储的每个像素的32位浮点数。 有时会使用这种格式，当需要其精度和值范围，但是图像具有大量的像素，内存和带宽以存储和传输图像的情况总是稀缺的。 只有一张十百万像素的照片将以这种格式消耗约115 MB的RAM。

> Why 115 MB and not 120 MB?  
> 为什么115 MB而不是120 MB？

Less range is required for images that are meant to be displayed directly. While the range of possible light intensities is unbounded in principle, any given device has a decidedly finite maximum intensity, so in many contexts it is perfectly sufficient for pixels to have a bounded range, usually taken to be [0, 1] for simplicity. For instance, the possible values in an 8-bit image are 0, 1/255, 2/255, . . . , 254/255, 1. Images stored with floating-point numbers, allowing a wide range of values, are often called high dynamic range (HDR) images to distinguish them from fixed-range, or low dynamic range (LDR) images that are stored with integers. See Chapter 21 for an in-depth discussion of techniques and applications for high dynamic range images.
对于要直接显示的图像所需的范围更少。 虽然原则上可能没有可能的光强度范围，但任何给定的设备都具有绝对有限的最大强度，因此在许多情况下，像素完全足以具有界限范围，通常认为[0，1]为了简单性。 例如，8位图像中的可能值为 0, 1/255, 2/255, . . . , 254/255, 1。用浮点数存储的图像，允许广泛的值，通常称为高动态范围（HDR）图像，以区分它们与固定范围或低动态范围（LDR）图像 与整数一起存储。 有关高动态范围图像的技术和应用的深入讨论，请参见第21章。

> The denominator of 255, rather than 256, is awkward, but being able to represent 0 and 1 exactly is important.  
> 255的分母，而不是256，这很尴尬，但是能够确切地表示0和1很重要。

Here are some pixel formats with typical applications:
以下是一些具有典型应用的像素格式：

- 1-bit grayscale—text and other images where intermediate grays are not desired (high resolution required);
  1位灰度 - 不需要中间灰色的文本和其他图像（需要高分辨率）；
- 8-bit RGB fixed-range color (24 bits total per pixel)—web and email applications, consumer photographs;
  8位RGB固定范围颜色（每个像素总计24位） -  Web和电子邮件应用程序，消费者照片；
- 8- or 10-bit fixed-range RGB (24–30 bits/pixel)—digital interfaces to computer displays;
  8-或10位固定范围RGB（24–30位/像素） - 计算机显示的数字接口；
- 12- to 14-bit fixed-range RGB (36–42 bits/pixel)—raw camera images for professional photography;
  12至14位固定范围RGB（36-42位/像素） - 专业摄影的RAW相机图像；
- 16-bit fixed-range RGB (48 bits/pixel)—professional photography and printing; intermediate format for image processing of fixed-range images;
  16位固定范围RGB（48位/像素） - 专业摄影和印刷； 用于固定范围图像的图像处理的中间格式；
- 16-bit fixed-range grayscale (16 bits/pixel)—radiology and medical imaging;
  16位固定范围灰度（16位/像素） - 放射学和医学成像；
- 16-bit “half-precision” floating-point RGB—HDR images; intermediate format for real-time rendering;
  16位“半精确”浮点RGB  -  HDR图像； 实时渲染的中间格式；
- 32-bit floating-point RGB—general-purpose intermediate format for software rendering and processing of HDR images.
  32位浮点RGB  - 用于HDR图像的软件渲染和处理的一般用途中间格式。

Reducing the number of bits used to store each pixel leads to two distinctive types of artifacts, or artificially introduced flaws, in images. First, encoding images with fixed-range values produces clipping when pixels that would otherwise be brighter than the maximum value are set, or clipped, to the maximum representable value. For instance, a photograph of a sunny scene may include reflections that are much brighter than white surfaces; these will be clipped (even if they were measured by the camera) when the image is converted to a fixed range to be displayed. Second, encoding images with limited precision leads to quantization artifacts, or banding, when the need to round pixel values to the nearest representable value introduces visible jumps in intensity or color. Banding can be particularly insidious in animation and video, where the bands may not be objectionable in still images, but become very visible when they move back and forth.
减少用于存储每个像素的位数的数量，导致图像中两种独特类型的人工制品或人为地引入缺陷。 首先，用固定范围值编码图像会产生剪辑，而当像素更明亮的像素将最大值设置或剪裁到最大代表值时。 例如，阳光明媚的场景的照片可能包括反射比白色表面更明亮。 当图像转换为要显示的固定范围时，这些将被剪辑（即使它们是由相机测量的）。 其次，当需要将像素值圆形到最近的代表值时，编码有限的精度编码图像会导致量化伪像或频段，这引入了强度或颜色的可见跳跃。 乐队在动画和视频中可能尤其阴险，在动画和视频中，乐队在静止图像中可能并不令人反感，但是当他们来回移动时变得非常明显。

### 3.2.2 Monitor Intensities and Gamma 监视强度和伽玛

All modern monitors take digital input for the “value” of a pixel and convert this to an intensity level. Real monitors have some nonzero intensity when they are off because the screen reflects some light. For our purposes we can consider this “black” and the monitor fully on as “white.” We assume a numeric description of pixel color that ranges from zero to one. Black is zero, white is one, and a gray halfway between black and white is 0.5. Note that here “halfway” refers to the physical amount of light coming from the pixel, rather than the appearance. The human perception of intensity is nonlinear and will not be part of the present discussion; see Chapter 20 for more.
所有现代监视器都以像素的“价值”为数字输入，并将其转换为强度水平。 真正的监视器在关闭时具有某些非零强度，因为屏幕会反射一些光。 出于我们的目的，我们可以将这种“黑色”和监视器完全视为“白色”。 我们假设对像素颜色的数字描述范围从零到一个。 黑色为零，白色是一个，黑白之间的灰色中间为0.5。 请注意，这里的“中途”是指来自像素的物理量，而不是外观。 人类对强度的看法是非线性的，不会成为当前讨论的一部分； 有关更多信息，请参见第20章。

There are two key issues that must be understood to produce correct images on monitors. The first is that monitors are nonlinear with respect to input. For example, if you give a monitor 0, 0.5, and 1.0 as inputs for three pixels, the intensities displayed might be 0, 0.25, and 1.0 (off, one-quarter fully on, and fully on). As an approximate characterization of this nonlinearity, monitors are commonly characterized by a $γ$ (“gamma”) value. This value is the degree of freedom in the formula
必须理解两个关键问题，以便在监视器上产生正确的图像。 首先是监视器相对于输入是非线性的。 例如，如果将监视器0、0.5和1.0作为三个像素的输入，则显示的强度可能是0、0.25和1.0（off，打开四分之一，完全打开）。 作为这种非线性的近似表征，监视器通常以$γ$（“伽马”）值为特征。 这个价值是公式的自由程度
$$
displayed\ intensity = (maximum\ intensity)a^γ, \ \ \ \ (3.1)
$$
where $a$ is the input pixel value between zero and one. For example, if a monitor has a gamma of 2.0, and we input a value of $a = 0.5$, the displayed intensity will be one fourth the maximum possible intensity because $0.5^2 = 0.25$. Note that $a = 0$ maps to zero intensity and $a = 1$ maps to the maximum intensity regardless of the value of $γ$. Describing a display’s nonlinearity using $γ$ is only an approximation; we do not need a great deal of accuracy in estimating the $γ$ of  a device. A nice visual way to gauge the nonlinearity is to find what value of $a$ gives an intensity halfway between black and white. This a will be
其中$a$为0到1之间的输入像素值。例如，如果显示器的gamma值为2.0，我们输入值$a = 0.5$，则显示的强度将是最大可能强度的四分之一，因为$0.5^2 = 0.25$。注意，$a = 0$映射到零强度，而$a = 1$映射到最大强度，而与$γ$的值无关。使用$γ$描述显示器的非线性只是一个近似值;在估计一个装置的γ值时，我们不需要很高的精度。衡量非线性的一种很好的视觉方法是找出$ A $的值在黑色和白色之间给出的强度。这个a等于
$0.5 = a^γ  $

If we can find that $a$, we can deduce $γ$ by taking logarithms on both sides:  
如果我们能找到$a$，我们可以通过对两边取对数来推导$γ$:
$γ = \frac{\ln 0.5}{\ln a}\\$

We can find this a by a standard technique where we display a checkerboard pattern of black and white pixels next to a square of gray pixels with input a (Figure 3.11), then ask the user to adjust a (with a slider, for instance) until the two sides match in average brightness. When you look at this image from a distance (or without glasses if you are nearsighted), the two sides of the image will look about the same when a is producing an intensity halfway between black and white. This is because the blurred checkerboard is mixing even numbers of white and black pixels so the overall effect is a uniform color halfway between white and black.  
我们可以通过一种标准技术来找到这个a，我们在输入a的情况下显示一个黑白像素的棋盘图案，旁边是一个灰色像素的正方形(图3.11)，然后要求用户调整a(例如使用滑块)，直到两边的平均亮度匹配。当你从远处看这幅图像时(如果你是近视眼，可以不戴眼镜)，当a产生的亮度介于黑白之间时，图像的两边看起来是一样的。这是因为模糊的棋盘混合了偶数的白色和黑色像素，所以整体效果是一种均匀的白色和黑色之间的颜色。我们可以通过一种标准技术来找到这个a，我们在输入a的情况下显示一个黑白像素的棋盘图案，旁边是一个灰色像素的正方形(图3.11)，然后要求用户调整a(例如使用滑块)，直到两边的平均亮度匹配。当你从远处看这幅图像时(如果你是近视眼，可以不戴眼镜)，当a产生的亮度介于黑白之间时，图像的两边看起来是一样的。这是因为模糊的棋盘混合了偶数的白色和黑色像素，所以整体效果是一种均匀的白色和黑色之间的颜色。
![Figure 3.11](.\Images\Figure 3.11.png)
Figure 3.11. Alternating black and white pixels viewed from a distance are halfway between black and white. The gamma of a monitor can be inferred by finding a gray value that appears to have the same intensity as the black and white pattern.
图3.11  从远处查看的黑白像素交替在黑色和白色之间的一半。 可以通过找到似乎具有与黑白模式相同强度的灰色值来推断监视器的伽玛。

Once we know $γ$, we can gamma correct our input so that a value of $a = 0.5$ is displayed with intensity halfway between black and white. This is done with the transformation
一旦我们知道了$γ$，我们就可以对输入进行gamma校正，使值$a = 0.5$的显示强度介于黑色和白色之间。这是通过变换完成的
$a' = a^{\frac{1}{γ}}$

When this formula is plugged into Equation (3.1) we get
将此公式代入式(3.1)，得到
$displayed\ intensity = (a')^γ = (a^\frac{1}{γ})^γ (maximum\ intensity) = a(maximum\ intensity)   $

> For monitors with analog interfaces, which have difficulty changing intensity rapidly along the horizontal direction, horizontal black and white stripes work better than a checkerboard.  
> 对于具有模拟界面的监视器，难以沿水平方向迅速改变强度，水平黑色和白色条纹比棋盘板更好。

Another important characteristic of real displays is that they take quantized input values. So while we can manipulate intensities in the floating point range $[0, 1]$, the detailed input to a monitor is a fixed-size integer. The most common range for this integer is $0–255$ which can be held in 8 bits of storage. This means that the possible values for a are not any number in $[0, 1]$ but instead
真实显示器的另一个重要特征是它们采用量化的输入值。因此，虽然我们可以在浮点范围内操作强度$[0,1]$，但监视器的详细输入是一个固定大小的整数。这个整数最常见的范围是$ 0-255 $，它可以保存在8位的存储器中。这意味着a的可能值不是$[0,1]$中的任何数字，而是
$possible\ values\ for\ a = \{ \frac{0}{255}, \frac{1}{255}, \frac{2}{255}, \cdots , \frac{254}{255}, \frac{255}{255}\} $

This means the possible displayed intensity values are approximately 
这意味着可能显示的强度值近似
$\{ M(\frac{0}{255})^γ, M(\frac{1}{255})^γ, M(\frac{2}{255})^γ, \cdots, M(\frac{254}{255})^γ, M(\frac{255}{255})^γ \}\\$

where $M$ is the maximum intensity. In applications where the exact intensities need to be controlled, we would have to actually measure the 256 possible intensities, and these intensities might be different at different points on the screen, especially for CRTs. They might also vary with viewing angle. Fortunately, few applications require such accurate calibration.
其中$M$为最大强度。在需要精确控制强度的应用中，我们必须实际测量256种可能的强度，这些强度在屏幕上的不同点可能是不同的，特别是对于CRTs。它们也可能随着视角的不同而变化。幸运的是，很少有应用需要如此精确的校准。

## 3.3 RGB Color RGB颜色

Most computer graphics images are defined in terms of red-green-blue (RGB) color. RGB color is a simple space that allows straightforward conversion to the controls for most computer screens. In this section, RGB color is discussed from a user’s perspective, and operational facility is the goal. A more thorough discussion of color is given in Chapter 19, but the mechanics of RGB color space will allow us to write most graphics programs. The basic idea of RGB color space is that the color is displayed by mixing three primary lights: one red, one green, and one blue. The lights mix in an additive manner.  
大多数计算机图形图像是根据红绿色蓝色（RGB）颜色定义的。 RGB颜色是一个简单的空间，可以直接转换到大多数计算机屏幕的控件。 在本节中，从用户的角度讨论了RGB颜色，而操作设施是目标。 第19章对颜色进行了更全面的讨论，但是RGB色彩空间的机制将使我们能够编写大多数图形程序。 RGB颜色空间的基本思想是，通过混合三个主灯来显示颜色：一个红色，一个绿色和一个蓝色。 灯以添加的方式混合。

> In grade school you probably learned that the primaries are red, yellow, and blue, and that, e.g., yellow + blue = green. This is subtractive color mixing, which is fundamentally different from the more familiar additive mixing that happens in displays.  
> 在小学里，你可能学过原色是红、黄、蓝，例如，黄+蓝=绿。这是减色混合，它与显示器中更熟悉的加色混合有着根本的不同。

In RGB additive color mixing we have (Figure 3.12)  
在RGB加色混合中，我们有(图3.12)

![Figure 3.12](.\Images\Figure 3.12.png)
Figure 3.12. The additive mixing rules for colors red/green/blue  
图3.12 红色/绿色/蓝色的添加混合规则

red + green = yellow,
green + blue = cyan,
blue + red = magenta,
red + green + blue = white.  
红+绿=黄;
绿色+蓝色=青色;
蓝色+红色=品红，
红+绿+蓝=白。

The color “cyan” is a blue-green, and the color “magenta” is a purple.
“青色”是一种蓝绿色，“品红”是一种紫色。

If we are allowed to dim the primary lights from fully off (indicated by pixel value 0) to fully on (indicated by 1), we can create all the colors that can be displayed on an RGB monitor. The red, green, and blue pixel values create a three-dimensional RGB color cube that has a red, a green, and a blue axis. Allowable coordinates for the axes range from zero to one. The color cube is shown graphically in Figure 3.13.  
如果允许我们从完全关闭（由像素值0指示）的主灯光调暗到完全打开（由1表示），则可以创建可以在RGB显示器上显示的所有颜色。 红色，绿色和蓝色像素值创建了一个三维RGB颜色立方体，具有红色，绿色和蓝色轴。 轴的允许坐标范围从零到一个。 颜色立方图在图3.13中以图形方式显示。
![Figure 3.13](.\Images\Figure 3.13.png)
Figure 3.13. The RGB color cube in 3D and its faces unfolded. Any RGB color is a point in the cube.  
图3.13  RGB颜色立方体为3D，其脸部展开。 任何RGB颜色都是立方体中的一个点。

The colors at the corners of the cube are
立方体角的颜色是
$black = (0, 0, 0), \\
red = (1, 0, 0), \\
green = (0, 1, 0),\\
blue = (0, 0, 1), \\
yellow = (1, 1, 0), \\
magenta = (1, 0, 1),  \\
cyan = (0, 1, 1), \\
white = (1, 1, 1).  \\
$

Actual RGB levels are often given in quantized form, just like the grayscales discussed in Section 3.2.2. Each component is specified with an integer. The most common size for these integers is one byte each, so each of the three RGB components is an integer between 0 and 255. The three integers together take up three bytes, which is 24 bits. Thus a system that has “24-bit color” has 256 possible levels for each of the three primary colors. Issues of gamma correction discussed in Section 3.2.2 also apply to each RGB component separately.  
实际的RGB级别通常以量化形式给出，就像第3.2.2节中讨论的灰度一样。 每个组件都用整数指定。 这些整数最常见的大小是每个字节，因此三个RGB组件中的每个组件都是0到255之间的整数。三个整数一起占用三个字节，即24位。 因此，具有“ 24位颜色”的系统对于三种原色中的每一个都有256个可能的水平。 第3.2.2节中讨论的伽马校正问题也分别适用于每个RGB组件。

## 3.4 Alpha Compositing Alpha合成

Often we would like to only partially overwrite the contents of a pixel. A common example of this occurs in compositing, where we have a background and want to insert a foreground image over it. For opaque pixels in the foreground, we just replace the background pixel. For entirely transparent foreground pixels, we do not change the background pixel. For partially transparent pixels, some care must be taken. Partially transparent pixels can occur when the foreground object has partially transparent regions, such as glass. But, the most frequent case where foreground and background must be blended is when the foreground object only partly covers the pixel, either at the edge of the foreground object, or when there are sub-pixel holes such as between the leaves of a distant tree.  
通常，我们只想部分覆盖像素的内容。 一个常见的例子发生在合成中，我们有背景，并希望在其上插入前景图像。 对于前景中的不透明像素，我们只需更换背景像素即可。 对于完全透明的前景像素，我们不会更改背景像素。 对于部分透明的像素，必须小心。 当前景对象具有部分透明区域（例如玻璃）时，可能会发生部分透明的像素。 但是，必须混合前景和背景的最常见情况是，当前景对象仅部分覆盖像素，即在前景对象的边缘，或者当有子像素孔（例如远处树的叶子之间） 。

The most important piece of information needed to blend a foreground object over a background object is the pixel coverage, which tells the fraction of the pixel covered by the foreground layer. We can call this fraction $α$. If we want  to composite a foreground color $\bold{c}_f$ over background color $\bold{c}_b$, and the fraction of the pixel covered by the foreground is α, then we can use the formula
将前景对象与背景对象混合所需的最重要的信息是像素覆盖率，它告诉我们前景层覆盖的像素的比例。我们称这个分数为α。如果我们想要合成前景色$\bold{c}_f$和背景色$\bold{c}_b$，并且前景覆盖的像素的分数是α，那么我们可以使用公式
$$
\bold{c} = α\bold{c}_f + (1 - α)\bold{c}_b.   \ \ \  \ (3.2)
$$
For an opaque foreground layer, the interpretation is that the foreground object covers area $α$ within the pixel’s rectangle and the background object covers the remaining area, which is $(1 - α)$. For a transparent layer (think of an image  painted on glass or on tracing paper, using translucent paint), the interpretation is that the foreground layer blocks the fraction $(1 - α)$ of the light coming through from the background and contributes a fraction $α$ of its own color to replace what was removed. An example of using Equation (3.2) is shown in Figure 3.14.  
对于不透明的前景层，解释是前景对象覆盖像素矩形内的区域$α$，背景对象覆盖剩余区域$(1 - α)$。对于透明层(想象一幅画在玻璃或描图纸上的图像，使用半透明的颜料)，解释是前景层阻挡了来自背景的部分$(1 - α)$，并贡献了自己颜色的部分$α$来取代被移除的部分。使用公式(3.2)的示例如图3.14所示。
![Figure 3.14](.\Images\Figure 3.14.png)
Figure 3.14. An example of compositing using Equation (3.2). The foreground image is in effect cropped by the $α$ channel before being put on top of the background image. The resulting composite is shown on the bottom. 
图3.14  使用等式(3.2)合成的示例。 前景图像实际上是由$α$通道裁剪到背景图像之上之前裁剪的。所得的复合材料显示在底部。

> Since the weights of the foreground and background layers add up to 1, the color won’t change if the foreground and background layers have the same color.  
> 由于前景和背景层的权重相加为1，如果前景和背景层具有相同的颜色，则颜色不会改变。

The $α$ values for all the pixels in an image might be stored in a separate grayscale image, which is then known as an alpha mask or transparency mask. Or the information can be stored as a fourth channel in an RGB image, in which case it is called the alpha channel, and the image can be called an RGBA image. With 8-bit images, each pixel then takes up 32 bits, which is a conveniently sized chunk in many computer architectures.
图像中所有像素的$α$值可能存储在单独的灰度图像中，然后称为alpha蒙版或透明蒙版。或者信息可以存储为RGB图像中的第四个通道，在这种情况下，它被称为alpha通道，而图像可以称为RGBA图像。对于8位的图像，每个像素占用32位，这在许多计算机体系结构中是一个方便的大小块。

Although Equation (3.2) is what is usually used, there are a variety of situations where $α$ is used differently (Porter & Duff, 1984).  
虽然公式(3.2)是通常使用的，但在各种情况下，$α$的使用方式不同(Porter & Duff, 1984)。

### 3.4.1 Image Storage 图像存储

Most RGB image formats use eight bits for each of the red, green, and blue channels. This results in approximately three megabytes of raw information for a single million-pixel image. To reduce the storage requirement, most image formats allow for some kind of compression. At a high level, such compression is either lossless or lossy. No information is discarded in lossless compression, while some information is lost unrecoverably in a lossy system. Popular image storage formats include:  
大多数RGB图像格式使用八个位为红色，绿色和蓝色通道使用。 这将为一个百万像素图像提供大约三个兆字节的原始信息。 为了减少存储要求，大多数图像格式都允许某种压缩。 在高水平上，这种压缩要么是无损或有损的。 没有任何信息在无损压缩中被丢弃，而在有损系统中，某些信息却无法丢失。 流行的图像存储格式包括：

- **jpeg.** This lossy format compresses image blocks based on thresholds in the human visual system. This format works well for natural images.
  **jpeg.**这种有损格式根据人类视觉系统中的阈值压缩图像块。 这种格式适用于自然图像。
- **tiff**. This format is most commonly used to hold binary images or losslessly compressed 8- or 16-bit RGB although many other options exist.
  这种格式最常用于容纳二进制图像或无损压缩的8或16位RGB，尽管存在许多其他选项。
- **ppm**. This very simple lossless, uncompressed format is most often used for 8-bit RGB images although many options exist.
  这种非常简单的无损，未压缩格式最常用于8位RGB图像，尽管存在许多选项。
- **png**. This is a set of lossless formats with a good set of open source management tools. 
  这是一套具有大量开源管理工具的无损格式。

Because of compression and variants, writing input/output routines for images can be involved. Fortunately one can usually rely on library routines to read and write standard file formats. For quick-and-dirty applications, where simplicity is valued above efficiency, a simple choice is to use raw ppm files, which can often be written simply by dumping the array that stores the image in memory to a file, prepending the appropriate header. 
由于压缩和变体，可以涉及图像的输入/输出例程。 幸运的是，通常可以依靠库例程来读取和编写标准文件格式。 对于快速和划线的应用程序，在效率高于效率之上的简单性的情况下，一个简单的选择是使用原始的PPM文件，通常可以通过将将图像存储在存储器中的数组中简单地写入文件，并准备适当的标头。

## Frequently Asked Questions

### Why don’t they just make monitors linear and avoid all this gamma business?

Ideally the 256 possible intensities of a monitor should look evenly spaced as opposed to being linearly spaced in energy. Because human perception of intensity is itself nonlinear, a gamma between 1.5 and 3 (depending on viewing conditions) will make the intensities approximately uniform in a subjective sense. In this way, gamma is a feature. Otherwise the manufacturers would make the monitors linear.  

## Exercise 练习

Simulate an image acquired from the Bayer mosaic by taking a natural image (preferably a scanned photo rather than a digital photo where the Bayer mosaic may already have been applied) and creating a grayscale image composed of interleaved red/green/blue channels. This simulates the raw output of a digital camera. Now create a true RGB image from that output and compare with the original. 
通过拍摄自然图像（最好是扫描的照片，而不是已经应用了拜耳马赛克的数字照片），并创建一个由交织的红色/绿色/蓝色通道组成的灰度图像。 这模拟了数码相机的原始输出。 现在，从该输出创建一个真正的RGB图像，并与原件进行比较。

# 4 Ray Tracing  射线跟踪

One of the basic tasks of computer graphics is rendering three-dimensional objects: taking a scene, or model, composed of many geometric objects arranged in 3D space and producing a 2D image that shows the objects as viewed from a particular viewpoint. It is the same operation that has been done for centuries by architects and engineers creating drawings to communicate their designs to others.  
计算机图形学的基本任务之一是渲染三维对象：采用一个场景或模型，由在3D空间中排列的许多几何对象组成，并产生一个2D图像，该对象从特定的角度显示为视图所示的对象。 这是建筑师和工程师创建图纸以将其设计传达给他人的几个世纪相同的操作。

Fundamentally, rendering is a process that takes as its input a set of objects and produces as its output an array of pixels. One way or another, rendering involves  considering how each object contributes to each pixel; it can be organized in two general ways. In object-order rendering, each object is considered in turn, and for each object all the pixels that it influences are found and updated. In image-order rendering, each pixel is considered in turn, and for each pixel all the objects that influence it are found and the pixel value is computed. You can think of the difference in terms of the nesting of loops: in image-order rendering the “for each pixel” loop is on the outside, whereas in object-order rendering the “for each object” loop is on the outside. 
从根本上讲，渲染是一个将其输入一组对象的过程，并作为其输出作为一个像素数组。 一种或另一种方式，渲染涉及考虑每个对象如何对每个像素贡献； 它可以通过两种一般的方式组织。 在对象订单渲染中，依次考虑每个对象，对于每个对象，都发现并更新了其影响的所有像素。 在图像订单渲染中，依次考虑每个像素，对于每个像素，所有影响它的对象都被发现并计算出像素值。 您可以想到循环嵌套的差异：在图像顺序中，呈现“每个像素”循环在外部，而在对象顺序中，呈现“每个对象”循环在外部。

> If the output is a vector image rather than a raster image, rendering doesn’t have to involve pixels, but we’ll assume raster images in this book. 
> 如果输出是矢量图像而不是光栅图像，则渲染不必涉及像素，但我们将在本书中假设光栅图像。

Image-order and object-order rendering approaches can compute exactly the same images, but they lend themselves to computing different kinds of effects and have quite different performance characteristics. We’ll explore the comparative strengths of the approaches in Chapter 8 after we have discussed them both, but, broadly speaking, image-order rendering is simpler to get working and more flexible in the effects that can be produced, and usually (though not always) takes much more execution time to produce a comparable image. 
图像顺序和对象订购渲染方法可以计算完全相同的图像，但它们可以计算不同种类的效果并具有完全不同的性能特征。 我们将在讨论两者之间的第8章中探讨方法的比较优势，但是从广义上讲，图像订单渲染更为简单，可以在可以产生的效果上更加灵活，通常不是（尽管不是） 总是）需要更多的执行时间来产生可比的图像。

> In a ray tracer, it is easy to compute accurate shadows and reflections, which are awkward in the object-order framework. 
> 在射线示踪剂中，很容易计算准确的阴影和反射，这在对象订购框架中很尴尬。

Ray tracing is an image-order algorithm for making renderings of 3D scenes, and we’ll consider it first because it’s possible to get a ray tracer working without developing any of the mathematical machinery that’s used for object-order rendering.  
光线追踪是一种用于渲染 3D 场景的图像顺序算法，我们将首先考虑它，因为无需开发任何用于对象顺序渲染的数学机制即可让光线追踪器工作。

## 4.1 The Basic Ray-Tracing Algorithm 基本光线追踪算法

A ray tracer works by computing one pixel at a time, and for each pixel the basic task is to find the object that is seen at that pixel’s position in the image. Each pixel “looks” in a different direction, and any object that is seen by a pixel must intersect the viewing ray, a line that emanates from the viewpoint in the direction that pixel is looking. The particular object we want is the one that intersects the viewing ray nearest the camera, since it blocks the view of any other objects behind it. Once that object is found, a shading computation uses the intersection point, surface normal, and other information (depending on the desired type of rendering) to determine the color of the pixel. This is shown in Figure 4.1, where the ray intersects two triangles, but only the first triangle hit, $T_2$, is shaded. A basic ray tracer therefore has three parts: 
光线追踪器的工作原理是一次计算一个像素，对于每个像素，基本任务是找到在图像中该像素位置看到的物体。 每个像素“看”的方向不同，并且像素所看到的任何对象都必须与视线相交，视线是从视点沿像素所看的方向发出的线。 我们想要的特定对象是与最接近相机的视线相交的对象，因为它阻挡了其后面的任何其他对象的视图。 一旦找到该对象，着色计算就会使用交点、表面法线和其他信息（取决于所需的渲染类型）来确定像素的颜色。 如图 4.1 所示，其中光线与两个三角形相交，但只有第一个三角形 $T_2$ 被着色。 因此，基本的光线追踪器由三个部分组成：
<img src=".\Images\Figure 4.1.png" alt="Figure 4.1" style="zoom:50%;" />
Figure 4.1. The ray is “traced” into the scene and the first object hit is the one seen through the pixel. In this case, the triangle $T_2$ is returned.  
图 4.1  光线被“追踪”到场景中，第一个击中的物体是通过像素看到的物体。 在本例中，返回三角形 $T_2$。

A basic ray tracer therefore has three parts: ·
因此，基本的光线追踪器由三个部分组成：

1. ray generation, which computes the origin and direction of each pixel’s viewing ray based on the camera geometry;
   光线生成，根据相机几何图形计算每个像素观看光线的原点和方向;
2. ray intersection, which finds the closest object intersecting the viewing ray;
   光线相交，寻找与观察光线相交的最近的物体;
3. shading, which computes the pixel color based on the results of ray intersection.  
   着色，基于光线相交的结果计算像素颜色。

The structure of the basic ray tracing program is:  
基本光线追踪程序的结构是:

```lua
for each pixel do
	compute viewing ray
	find first object hit by ray and its surface normal n
	set pixel color to value computed from hit point, light, and n
对于每个像素
    计算观察射线
    求第一个被射线击中的物体及其表面法向n
    将像素颜色设置为根据命中点、光线和n计算的值
```

This chapter covers basic methods for ray generation, ray intersection, and shading, that are sufficient for implementing a simple demonstration ray tracer. For a really useful system, more efficient ray intersection techniques from Chapter 12 need to be added, and the real potential of a ray tracer will be seen with the more advanced shading methods from Chapter 10 and the additional rendering techniques from Chapter 13. 
这一章涵盖了光线生成、光线交叉和阴影的基本方法，这足以实现一个简单的演示光线追踪器。对于一个真正有用的系统，需要在第12章中添加更有效的光线交叉技术，而光线追踪器的真正潜力将在第10章中更高级的阴影方法和第13章中额外的渲染技术中看到。

 

## 4.2 Perspective 看法

The problem of representing a 3D object or scene with a 2D drawing or painting was studied by artists hundreds of years before computers. Photographs also represent 3D scenes with 2D images. While there are many unconventional ways to make images, from cubist painting to fisheye lenses (Figure 4.2) to peripheral cameras, the standard approach for both art and photography, as well as computer graphics, is linear perspective, in which 3D objects are projected onto an image plane in such a way that straight lines in the scene become straight lines in the image. 
在计算机出现之前数百年，艺术家们就已经研究了用 2D 绘图或绘画来表示 3D 对象或场景的问题。 照片还用 2D 图像表示 3D 场景。 虽然有许多非常规的图像制作方法，从立体派绘画到鱼眼镜头（图 4.2）再到外围相机，但艺术和摄影以及计算机图形学的标准方法是线性透视，其中 3D 对象被投影到 图像平面，使场景中的直线变成图像中的直线。
<img src=".\Images\Figure 4.2.png" alt="Figure 4.2" style="zoom:67%;" />
Figure 4.2. An image taken with a fisheye lens is not a linear perspective image. Photo courtesy Philip Greenspun. 
图4.2 用鱼眼镜头拍摄的图像不是线性透视图像。图片由Philip Greenspun提供。

The simplest type of projection is parallel projection, in which 3D points are mapped to 2D by moving them along a projection direction until they hit the image plane (Figures 4.3–4.4). The view that is produced is determined by the choice of projection direction and image plane. If the image plane is perpendicular  to the view direction, the projection is called orthographic; otherwise it is called oblique.  
最简单的投影类型是平行投影，其中 3D 点通过沿投影方向移动直至到达图像平面来映射到 2D（图 4.3-4.4）。 所产生的视图由投影方向和图像平面的选择决定。 如果像平面垂直于视线方向，则该投影称为正交投影； 否则称为斜的。
<img src="G:\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 4.3.png" alt="Figure 4.3" style="zoom:80%;" />
Figure 4.3. When projection lines are parallel and perpendicular to the image plane, the resulting views are called orthographic. 
图 4.3  当投影线平行和垂直于图像平面时，所得视图称为正交视图。
<img src="G:\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 4.4.png" alt="Figure 4.4" style="zoom:80%;" />
Figure 4.4. A parallel projection that has the image plane at an angle to the projection direction is called oblique (right). In perspective projection, the projection lines all pass through the viewpoint, rather than being parallel (left). The illustrated perspective view is non-oblique because a projection line drawn through the center of the image would be perpendicular to the image plane.
图 4.4  像平面与投影方向成一定角度的平行投影称为斜投影（右投影）。 在透视投影中，投影线全部穿过视点，而不是平行（左）。 所示透视图是非倾斜的，因为穿过图像中心绘制的投影线将垂直于图像平面。

Parallel projections are often used for mechanical and architectural drawings because they keep parallel lines parallel and they preserve the size and shape of planar objects that are parallel to the image plane. 
平行投影通常用于机械和建筑绘图，因为它们使平行线保持平行，并保持与图像平面平行的平面物体的大小和形状。

> Some books reserve “orthographic” for projection directions that are parallel to the coordinate axes. 
> 有些书保留“正射影”的投影方向平行于坐标轴。 

The advantages of parallel projection are also its limitations. In our everyday experience (and even more so in photographs) objects look smaller as they get farther away, and as a result parallel lines receding into the distance do not appear parallel. This is because eyes and cameras don’t collect light from a single viewing direction; they collect light that passes through a particular viewpoint. As has been recognized by artists since the Renaissance, we can produce natural-looking views using perspective projection: we simply project along lines that pass through a single point, the viewpoint, rather than along parallel lines (Figure 4.4). In this way, objects farther from the viewpoint naturally become smaller when they are projected. A perspective view is determined by the choice of viewpoint (rather than projection direction) and image plane. As with parallel views, there are oblique and non-oblique perspective views; the distinction is made based on the projection direction at the center of the image.
平行投影的优点也是它的局限性。 在我们的日常经验中（在照片中更是如此），物体随着距离越来越远而看起来越来越小，因此，后退到远处的平行线看起来并不平行。 这是因为眼睛和相机不会收集来自单一观察方向的光线；而是收集光线。 它们收集通过特定视点的光线。 正如文艺复兴以来的艺术家所认识到的那样，我们可以使用透视投影产生自然的视图：我们只需沿着穿过单个点（即视点）的线进行投影，而不是沿着平行线进行投影（图 4.4）。 这样，距离视点较远的物体在投影时自然会变小。 透视图是由视点（而不是投影方向）和图像平面的选择决定的。 与平行视图一样，也有倾斜透视图和非倾斜透视图； 区分是根据图像中心的投影方向进行的。

You may have learned about the artistic conventions of three-point perspective, a system for manually constructing perspective views (Figure 4.5). A surprising fact about perspective is that all the rules of perspective drawing will be followed automatically if we follow the simple mathematical rule underlying perspective: objects are projected directly toward the eye, and they are drawn where they meet a view plane in front of the eye.
您可能已经了解了三点透视的艺术惯例，这是一种手动构建透视图的系统（图 4.5）。 关于透视的一个令人惊讶的事实是，如果我们遵循透视背后的简单数学规则，则将自动遵循透视绘制的所有规则：对象直接投影到眼睛，并在与眼睛前面的视图平面相交的位置绘制它们 。
<img src=".\Images\Figure 4.5.png" alt="Figure 4.5" style="zoom:67%;" />
Figure 4.5. In three-point perspective, an artist picks “vanishing points” where parallel lines meet. Parallel horizontal lines will meet at a point on the horizon. Every set of parallel lines has its own vanishing points. These rules are followed automatically if we implement perspective based on the correct geometric principles. 
图4.5 在三点透视法中，艺术家选择平行线相交的“消失点”。平行的水平线会在地平线上的一点相交。每一组平行线都有自己的消失点。如果我们基于正确的几何原理实现透视图，就会自动遵循这些规则。

## 4.3 Computing Viewing Rays  计算观察光线

From the previous section, the basic tools of ray generation are the viewpoint (or view direction, for parallel views) and the image plane. There are many ways to work out the details of camera geometry; in this section we explain one based on orthonormal bases that supports normal and oblique parallel and orthographic views. 
从上一节可知，光线生成的基本工具是视点（或视图方向，对于平行视图）和图像平面。 有很多方法可以计算出相机几何的细节； 在本节中，我们将解释一种基于正交基的方法，该基支持法线视图、倾斜平行视图和正交视图。

In order to generate rays, we first need a mathematical representation for a ray. A ray is really just an origin point and a propagation direction; a 3D parametric line is ideal for this. As discussed in Section 2.5.7, the 3D parametric line from the eye e to a point s on the image plane (Figure 4.6) is given by 
为了生成射线，我们首先需要射线的数学表示。 射线实际上只是一个原点和一个传播方向； 3D 参数线非常适合此目的。 如第 2.5.7 节所述，从眼睛 e 到图像平面上的点 s（图 4.6）的 3D 参数线由下式给出
$\bold{p}(t) = \bold{e} + t(s - \bold{e})  $
![Figure 4.6](.\Images\Figure 4.6.png)
Figure 4.6. The ray from the eye to a point on the image plane. 
图 4.6 从眼睛到图像平面上的一点的光线

This should be interpreted as, “we advance from e along the vector $(\bold{s} - \bold{e})$ a fractional distance $t$ to find the point $\bold{p}$.” So given $t$, we can determine a point $\bold{p}$. The point $\bold{e}$ is the ray’s origin, and $\bold{s} - \bold{e}$ is the ray’s direction. 
这应该被解释为，“我们从 e 沿着向量 $(\bold{s} - \bold{e})$ 前进一小部分距离 t 来找到点 $\bold{p}$。” 因此给定$t$，我们可以确定一个点$\bold{p}$。 点 $\bold{e}$ 是射线的原点，$\bold{s} - \bold{e}$ 是射线的方向。

Note that $\bold{p}(0) = \bold{e}$, and $\bold{p}(1) = \bold{s}$, and more generally, if $0 < t_1 < t_2$, then $\bold{p}(t_1)$ is closer to the eye than $\bold{p}(t_2)$. Also, if $t < 0$, then $\bold{p}(t)$ is “behind” the eye. These facts will be useful when we search for the closest object hit by the ray that is not behind the eye. 
请注意 $\bold{p}(0) = \bold{e}$ 和 $\bold{p}(1) = \bold{s}$，更一般地说，如果 $0 < t_1 < t_2$，则 $\bold{p}(t_1)$ 比 $\bold{p}(t_2)$ 更接近眼睛。 另外，如果 $t < 0$，则 $\bold{p}(t)$ 位于眼睛“后面”。 当我们搜索光线击中的、不在眼睛后面的最近物体时，这些事实将很有用。

> Caution: we are overloading the variable $t$, which is the ray parameter and also the v-coordinate of the top edge of the image. 
> 注意：我们正在重载变量 $t$，它是光线参数，也是图像上边缘的 v 坐标。

To compute a viewing ray, we need to know $\bold{e}$ (which is given) and $\bold{s}$. Finding $\bold{s}$ may seem difficult, but it is actually straightforward if we look at the problem in the right coordinate system. 
为了计算视线，我们需要知道 $\bold{e}$ （已给出）和 $\bold{s}$。 找到$\bold{s}$可能看起来很困难，但如果我们在正确的坐标系中看问题，实际上很简单。

All of our ray-generation methods start from an orthonormal coordinate frame known as the camera frame, which we’ll denote by $\bold{e}$, for the eye point, or viewpoint, and $\bold{u}$, $\bold{v}$, and $\bold{w}$ for the three basis vectors, organized with $\bold{u}$ pointing rightward (from the camera’s view), $\bold{v}$ pointing upward, and $\bold{w}$ pointing backward, so that {$\bold{u}$, $\bold{v}$, $\bold{w}$} forms a right-handed coordinate system. The most common way  to construct the camera frame is from the viewpoint, which becomes $\bold{e}$, the view  direction, which is $-\bold{w}$, and the up vector, which is used to construct a basis that has $\bold{v}$ and $\bold{w}$ in the plane defined by the view direction and the up direction, using  the process for constructing an orthonormal basis from two vectors described in Section 2.4.7. 
我们所有的光线生成方法都从称为相机坐标系的正交坐标系开始，我们用 $\bold{e}$ 表示眼点或视点，用 $\bold{u}$ 表示， $\bold{v}$ 和 $\bold{w}$ 表示三个基向量，组织为 $\bold{u}$ 指向右侧（从相机的角度），$\bold{v}$ 指向上方， $\bold{w}$ 向后指向，使得 {$\bold{u}$、$\bold{v}$、$\bold{w}$} 构成右手坐标系。 构造相机框架最常见的方法是从视点开始，它变成 $\bold{e}$，视图方向，它是 $-\bold{w}$，以及向上向量，它用于构造一个 在由视图方向和向上方向定义的平面中具有 $\bold{v}$ 和 $\bold{w}$ 的基，使用第 2.4.7 节中描述的从两个向量构造正交基的过程。
<img src=".\Images\Figure 4.7.png" alt="Figure 4.7" style="zoom:67%;" />
Figure 4.7. The sample points on the screen are mapped to a similar array on the 3D window. A viewing ray is sent to each of these locations.  
图 4.7  屏幕上的采样点被映射到 3D 窗口上的类似阵列。 观察光线被发送到这些位置中的每一个。

![Figure 4.8](.\Images\Figure 4.8.png)
Figure 4.8. The vectors of the camera frame, together with the view direction and up direction. The $\bold{w}$ vector is opposite the view direction, and the $\bold{v}$ vector is coplanar with $\bold{w}$ and the up vector. 
图 4.8  相机框架的向量，以及视图方向和向上方向。 $\bold{w}$ 向量与视图方向相反，$\bold{v}$ 向量与 $\bold{w}$ 和向上向量共面。

> Since $\bold{v}$ and $\bold{w}$ have to be perpendicular, the up vector and $\bold{v}$ are not generally the same. But setting the up vector to point straight upward in the scene will orient the camera in the way we would think of as “upright.”  
> 由于 $\bold{v}$ 和 $\bold{w}$ 必须垂直，因此向上向量和 $\bold{v}$ 通常不相同。 但是，将向上向量设置为在场景中笔直向上，将使相机以我们认为的“直立”方式定向。

### 4.3.1 Orthographic Views 正交视图

For an orthographic view, all the rays will have the direction $-\bold{w}$. Even though a parallel view doesn’t have a viewpoint per se, we can still use the origin of the  camera frame to define the plane where the rays start, so that it’s possible for objects to be behind the camera.  
对于正交视图，所有光线的方向都是 $-\bold{w}$。 即使平行视图本身没有视点，我们仍然可以使用相机框架的原点来定义光线开始的平面，这样物体就有可能位于相机后面。

The viewing rays should start on the plane defined by the point $\bold{e}$ and the vectors $\bold{u}$ and $\bold{v}$; the only remaining information required is where on the plane the image is supposed to be. We’ll define the image dimensions with four numbers, for the four sides of the image: $l$ and $r$ are the positions of the left and right edges of the image, as measured from $\bold{e}$ along the $\bold{u}$ direction; and $b$ and $t$ are the positions of the bottom and top edges of the image, as measured from $\bold{e}$ along the $\bold{v}$ direction. Usually $l < 0 < r$ and $b < 0 < t$. (See Figure 4.9.)  
视线应从点 $\bold{e}$ 和向量 $\bold{u}$ 和 $\bold{v}$ 定义的平面开始； 唯一需要的剩余信息是图像在平面上的位置。 我们将用四个数字定义图像的四个边的图像尺寸：$l$ 和 $r$ 是图像左边缘和右边缘的位置，从 $\bold{e}$ 沿 $\bold{u}$ 方向； $b$ 和 $t$ 是图像底部和顶部边缘的位置，从 $\bold{e}$ 沿 $\bold{v}$ 方向测量。 通常 $l < 0 < r$ 且 $b < 0 < t$。 （见图 4.9。）
![Figure 4.9](.\Images\Figure 4.9.png)
Figure 4.9. Ray generation using the camera frame. Left: In an orthographic view, the rays start at the pixels’ locations on the image plane, and all share the same direction, which is equal to the view direction. Right: In a perspective view, the rays start at the viewpoint, and each ray’s direction is defined by the line through the viewpoint, $\bold{e}$, and the pixel’s location on the image plane.  
图 4.9  使用相机框架生成光线。 左：在正交视图中，光线从图像平面上的像素位置开始，并且全部共享相同的方向，该方向等于视图方向。 右：在透视图中，光线从视点开始，每条光线的方向由通过视点的线 $\bold{e}$ 和图像平面上的像素位置定义。

> It might seem logical that orthographic viewing rays should start from infinitely far away, but then it would not be possible to make orthographic views of an object inside a room, for instance  
> 正交观察光线应该从无限远的地方开始，这似乎是合乎逻辑的，但是，例如，就不可能对房间内的物体进行正交视图

> Many systems assume that $l = – r$ and $b = – t$ so that a width and a height suffice.
> 许多系统假设 $l = – r$ 和 $b = – t$ 这样宽度和高度就足够了

In Section 3.2 we discussed pixel coordinates in an image. To fit an image with $n_x × n_y$ pixels into a rectangle of size $(r - l) \cross (t - b)$, the pixels are spaced a distance $(r - l)/n_x$ apart horizontally and $(t - b)/n_y$ apart vertically, with a half-pixel space around the edge to center the pixel grid within the image rectangle. This means that the pixel at position $(i, j)$ in the raster image has the position
在 3.2 节中，我们讨论了图像中的像素坐标。 要将具有 $n_x × n_y$ 像素的图像放入大小为 $(r - l) \cross (t - b)$ 的矩形中，像素的水平间隔距离为 $(r - l)/n_x$，并且 $ (t - b)/n_y$ 垂直分开，边缘周围有半像素空间，使像素网格在图像矩形内居中。 这意味着光栅图像中位置 $(i, j)$ 处的像素的位置为
$$
u = l + (r − l)(i + 0.5)/n_x, \\
v = b + (t − b)(j + 0.5)/n_y, \\
(4.1)
$$
where $(u, v)$ are the coordinates of the pixel’s position on the image plane, measured with respect to the origin $\bold{e}$ and the basis $\{\bold{u}, \bold{v}\}$. 
其中 $(u, v)$ 是像素在图像平面上的位置坐标，相对于原点 $\bold{e}$ 和基准  进行$\{\bold{u}, \bold{v}\}$测量。

In an orthographic view, we can simply use the pixel’s image-plane position as the ray’s starting point, and we already know the ray’s direction is the view direction. The procedure for generating orthographic viewing rays is then: 
在正交视图中，我们可以简单地使用像素的图像平面位置作为射线的起点，并且我们已经知道射线的方向就是视图方向。 生成正交观察光线的过程是：

$compute\ u\ and\ v\ using\ (4.1) \\
ray.direction ← -\bold{w} \\
ray.origin ← \bold{e} + u\bold{u} + v\bold{v} \\ $

> With $l$ and $r$ both specified, there is redundancy: moving the viewpoint a bit to the right and correspondingly decreasing $l$ and $r$ will not change the view (and similarly on the $\bold{v}$-axis) 
> 如果同时指定了$l$和$r$，就存在冗余:将视点向右移动一点并相应减少$l$和$r$不会改变视图(在$\bold{v}$-轴上也是如此)

It’s very simple to make an oblique parallel view: just allow the image plane normal w to be specified separately from the view direction $\bold{d}$. The procedure is then exactly the same, but with $\bold{d}$ substituted for $-\bold{w}$. Of course $\bold{w}$ is still used to construct $\bold{u}$ and $\bold{v}$.  
制作倾斜平行视图非常简单：只需将图像平面法线 w 与视图方向 $\bold{d}$ 分开指定即可。 过程完全相同，但用 $\bold{d}$ 替换 $-\bold{w}$。 当然$\bold{w}$仍然用来构造$\bold{u}$和$\bold{v}$。

### 4.3.2 Perspective Views

For a perspective view, all the rays have the same origin, at the viewpoint; it is the directions that are different for each pixel. The image plane is no longer positioned at $\bold{e}$, but rather some distance $d$ in front of $\bold{e}$; this distance is the image plane distance, often loosely called the focal length, because choosing $d$ plays the same role as choosing focal length in a real camera. The direction of each ray is defined by the viewpoint and the position of the pixel on the image plane. This situation is illustrated in Figure 4.9, and the resulting procedure is similar to the  orthographic one:
对于透视图，所有光线在视点处具有相同的原点； 这是每个像素的不同方向。 图像平面不再位于$\bold{e}$处，而是位于$\bold{e}$前面一段距离$d$处； 这个距离是像平面距离，通常被宽松地称为焦距，因为选择 $d$ 与在真实相机中选择焦距起着相同的作用。 每条光线的方向由视点和图像平面上像素的位置定义。 这种情况如图 4.9 所示，生成的过程与拼字法类似：
$compute\ u\ and\ v\ using\ (4.1) \\
ray.direction ← -d \bold{w} + u \bold{u} + v \bold{v} \\
ray.origin ← \bold{e}$

As with parallel projection, oblique perspective views can be achieved by specifying the image plane normal separately from the projection direction, then replacing $-d\bold{w}$ with $d\bold{d}$ in the expression for the ray direction. 
与平行投影一样，可以通过指定与投影方向分开的图像平面法线，然后将光线方向表达式中的 $-d\bold{w}$ 替换为 $d\bold{d}$ 来获得倾斜透视图 。

## 4.4 Ray-Object Intersection 射线-物体相交

Once we’ve generated a ray $\bold{e}+ t\bold{d}$, we next need to find the first intersection with any object where $t > 0$. In practice, it turns out to be useful to solve a slightly more general problem: find the first intersection between the ray and a surface that occurs at a $t$ in the interval $[t_0, t_1]$. The basic ray intersection is the case where $t_0 = 0$ and $t_1 = +∞$. We solve this problem for both spheres and triangles. In the next section, multiple objects are discussed.  
一旦我们生成了一条射线 $\bold{e}+ t\bold{d}$，接下来我们需要找到与 $t > 0$ 的任何对象的第一个交点。 在实践中，事实证明，它对于解决一个稍微更普遍的问题很有用：找到光线和表面之间的第一个交点，该交点出现在区间 $[t_0, t_1]$ 中的 $t$ 处。 基本射线相交是 $t_0 = 0$ 且 $t_1 = +∞$ 的情况。 我们针对球体和三角形解决了这个问题。 在下一节中，将讨论多个对象。

### 4.4.1 Ray-Sphere Intersection   射线-球体相交

Given a ray $\bold{p}(t) = \bold{e} + t\bold{d}$ and an implicit surface $f(\bold{p}) = 0$ (see Section 2.5.3), we’d like to know where they intersect. Intersection points occur when points on the ray satisfy the implicit equation, so the values of $t$ we seek are those that solve the equation
给定一条射线 $\bold{p}(t) = \bold{e} + t\bold{d}$ 和一个隐式曲面 $f(\bold{p}) = 0$ （参见第 2.5.3 节）， 我们想知道它们相交的地方。 当射线上的点满足隐式方程时，就会出现交点，因此我们寻求的 $t$ 值就是解方程的值
$f(\bold{p}(t)) = 0\ or\ f(\bold{e} + t\bold{d}) = 0  $

A sphere with center $\bold{c} = (x_c, y_c, z_c)$ and radius R can be represented by the implicit equation
中心为 $\bold{c} = (x_c, y_c, z_c)$ 且半径为 R 的球体可以用隐式方程表示
$(x - x_c)^2 + (y - y_c)^2 + (z - z_c)^2 - R^2 = 0.  $

We can write this same equation in vector form:  
我们可以将同样的方程写成向量形式：
$(\bold{p} - \bold{c}) · (\bold{p} - \bold{c}) - R^2 = 0.  $

Any point $\bold{p}$ that satisfies this equation is on the sphere. If we plug points on the ray $\bold{p}(t) = \bold{e} + t\bold{d}$ into this equation, we get an equation in terms of t that is satisfied by the values of $t$ that yield points on the sphere:
满足该方程的任何点 $\bold{p}$ 都在球体上。 如果我们将射线 $\bold{p}(t) = \bold{e} + t\bold{d}$ 上的点代入这个方程，我们就得到一个以 t 表示的方程，它满足$t$的值在球体上产生点：
$(\bold{e} + t\bold{d}- \bold{c}) · (\bold{e} + t\bold{d} - \bold{c}) - R^2 = 0.  $

Rearranging terms yields
重新排列
$(\bold{d} · \bold{d})t^2 + 2\bold{d} · (\bold{e} - \bold{c})t + (\bold{e} - \bold{c}) · (\bold{e} - \bold{c}) - R^2 = 0.  $

Here, everything is known except the parameter $t$, so this is a classic quadratic equation in $t$, meaning it has the form
这里，除了参数$t$，其他都是已知的，所以这是$t$的经典二次方程，也就是说它有这样的形式
$At^2 + Bt + C = 0  $

The solution to this equation is discussed in Section 2.2. The term under the square root sign in the quadratic solution, $B^2 - 4AC$, is called the discriminant and tells us how many real solutions there are. If the discriminant is negative, its square root is imaginary and the line and sphere do not intersect. If the discriminant is positive, there are two solutions: one solution where the ray enters the sphere and one where it leaves. If the discriminant is zero, the ray grazes the sphere, touching it at exactly one point. Plugging in the actual terms for the sphere and canceling a factor of two, we get 
该方程的解在 2.2 节中讨论。 二次解中平方根符号下的项 $B^2 - 4AC$ 称为判别式，它告诉我们有多少个实数解。 如果判别式为负，则其平方根为虚数，并且直线和球面不相交。 如果判别式为正，则有两种解决方案：一种是光线进入球体的解决方案，另一种是光线离开球体的解决方案。 如果判别式为零，则光线擦过球体，恰好接触到一个点。 代入球体的实际项并取消两倍，我们得到
$t = \frac{-\bold{d} · (\bold{e} - \bold{c}) ±  \sqrt{(\bold{d} · (\bold{e} - \bold{c}))^2 - (\bold{d} · \bold{d}) ((\bold{e} - \bold{c}) · (\bold{e} - \bold{c}) - R^2)  }}{(\bold{d} · \bold{d})}\\$

In an actual implementation, you should first check the value of the discriminant before computing other terms. If the sphere is used only as a bounding object for more complex objects, then we need only determine whether we hit it; checking the discriminant suffices. 
在实际实现中，您应该在计算其他项之前首先检查判别式的值。 如果球体仅用作更复杂物体的边界物体，那么我们只需要确定是否击中它即可； 检查判别式就足够了。

As discussed in Section 2.5.4, the normal vector at point $\bold{p}$ is given by the gradient $\bold{n} = 2(\bold{p} - \bold{c})$. The unit normal is $(\bold{p} - \bold{c})/R$. 
正如第 2.5.4 节中所讨论的，点 $\bold{p}$ 处的法向量由梯度 $\bold{n} = 2(\bold{p} - \bold{c})$ 给出。 单位法线为$(\bold{p} - \bold{c})/R$。

### 4.4.2 Ray-Triangle Intersection 射线-三角形相交

There are many algorithms for computing ray-triangle intersections. We will present the form that uses barycentric coordinates for the parametric plane containing the triangle, because it requires no long-term storage other than the vertices of the triangle (Snyder & Barr, 1987).  
有许多计算射线与三角形相交的算法。 我们将提出使用重心坐标作为包含三角形的参数平面的形式，因为它除了三角形的顶点之外不需要长期存储（Snyder & Barr，1987）。

To intersect a ray with a parametric surface, we set up a system of equations where the Cartesian coordinates all match: 
为了使射线与参数曲面相交，我们建立了一个方程组，其中笛卡尔坐标都是匹配的:
$$
\begin{rcases}
x_e + tx_d = f(u, v) \\
y_e + ty_d = g(u, v) \\
z_e + tz_d = h(u, v)
\end{rcases}
or, \bold{e} + t\bold{d} = \bold{f}(u, v).
$$
Here, we have three equations and three unknowns ($t$, $u$, and $v$), so we can solve numerically for the unknowns. If we are lucky, we can solve for them analytically.
在这里，我们有三个方程和三个未知数（$t$、$u$ 和 $v$），因此我们可以对未知数进行数值求解。 如果幸运的话，我们可以通过分析来解决它们。

In the case where the parametric surface is a parametric plane, the parametric equation can be written in vector form as discussed in Section 2.7.2. If the vertices of the triangle are $\bold{a}$, $\bold{b}$, and $\bold{c}$, then the intersection will occur when
在参数曲面是参数平面的情况下，参数方程可以写成矢量形式，如第 2.7.2 节所述。 如果三角形的顶点是 $\bold{a}$、$\bold{b}$ 和 $\bold{c}$，则交集将发生在
$$
\bold{e} + t\bold{d} = \bold{a} + β(\bold{b} − \bold{a}) + γ(\bold{c} − \bold{a}), (4.2)
$$
for some $t$, $β$, and $γ$. The intersection $\bold{p}$ will be at $\bold{e} + t\bold{d}$ as shown in Figure 4.10. Again, from Section 2.7.2, we know the intersection is inside the triangle if and only if $β > 0$, $γ > 0$, and $β + γ < 1$. Otherwise, the ray has hit the plane outside the triangle, so it misses the triangle. If there are no solutions, either the triangle is degenerate or the ray is parallel to the plane containing the triangle. 
对于一些 $t$、$β$ 和 $γ$。 交集 $\bold{p}$ 将位于 $\bold{e} + t\bold{d}$，如图 4.10 所示。 同样，根据第 2.7.2 节，我们知道当且仅当 $β > 0$、$γ > 0$ 且 $β + γ < 1$ 时，交点位于三角形内部。 否则，光线击中了三角形外部的平面，因此它错过了三角形。 如果没有解，则三角形是退化的，或者射线平行于包含三角形的平面。
![Figure 4.10](.\Images\Figure 4.10.png)
Figure 4.10. The ray hits the plane containing the triangle at point $\bold{p}$
图4.10 射线在点$\bold{p}$处击中包含三角形的平面

To solve for $t$, $β$, and $γ$ in Equation (4.2), we expand it from its vector form into the three equations for the three coordinates: 
为了求解方程 (4.2) 中的 $t$、$β$ 和 $γ$，我们将其从向量形式展开为三个坐标的三个方程：
$x_e + tx_d = x_a + β(x_b - x_a) + γ(x_c - x_a), \\
y_e + ty_d = y_a + β(y_b - y_a) + γ(y_c - y_a), \\
z_e + tz_d = z_a + β(z_b - z_a) + γ(z_c - z_a).  $

This can be rewritten as a standard linear system:  
这可以重写为一个标准的线性系统:
$$
\begin{bmatrix}
x_a − x_b & x_a − x_c & x_d \\
y_a − y_b & y_a − y_c & y_d \\
z_a − z_b & z_a − z_c & z_d
\end{bmatrix}
\begin{bmatrix}
β \\
γ \\
t
\end{bmatrix}
 = \begin{bmatrix}
x_a − x_e \\
y_a − y_e \\
z_a − z_e
\end{bmatrix}
$$
The fastest classic method to solve this 3 × 3 linear system is Cramer’s rule. This gives us the solutions  
解决这个 3 × 3 线性系统最快的经典方法是 Cramer 法则。 这给了我们解决方案
$$
β = \frac{\begin{vmatrix}
x_a − x_e & x_a − x_c & x_d \\
y_a − y_e & y_a − y_c & y_d \\
z_a − z_e & z_a − z_c & z_d
\end{vmatrix}} {|\bold{A}|} \\

γ = \frac{\begin{vmatrix}
x_a − x_b & x_a − x_e & x_d \\
y_a − y_b & y_a − y_e & y_d \\
z_a − z_b & z_a − z_e & z_d
\end{vmatrix}} {|\bold{A}|} \\

t = \frac{\begin{vmatrix}
x_a − x_b & x_a − x_c & x_a − x_e \\
y_a − y_b & y_a − y_c & y_a − y_e \\ 
z_a − z_b & z_a − z_c & z_a − z_e
\end{vmatrix}} {|\bold{A}|} \\
$$
where the matrix $\bold{A}$ is
其中矩阵 $\bold{A}$ 是
$$
\bold{A} = \begin{bmatrix}
x_a - x_b & x_a - x_c & x_d \\
y_a - y_b & y_a - y_c & y_d \\
z_a - z_b & z_a - z_c & z_d
\end{bmatrix}
$$
and $|\bold{A}|$ denotes the determinant of $\bold{A}$. The 3×3 determinants have common sub-terms that can be exploited. Looking at the linear systems with dummy variables 
$|\bold{A}|$ 表示 $\bold{A}$ 的行列式。 3×3 行列式有可以利用的共同子项。 查看具有虚拟变量的线性系统
$$
\begin{bmatrix}
a & d & g \\
b & e & h \\
c & f & i
\end{bmatrix}
\begin{bmatrix}
β \\
γ \\
t
\end{bmatrix}
= \begin{bmatrix}
j \\
k \\
l
\end{bmatrix}
$$
Cramer’s rule gives us 
克莱默法则给了我们
$$
β = \frac{j(ei − hf) + k(gf − di) + l(dh − eg)}{M} \\
γ = \frac{i(ak − jb) + h(jc − al) + g(bl − kc)}{M} \\
β = \frac{f(ak − jb) + e(jc − al) + d(bl − kc)}{M} \\ 
\\
M = a(ei − hf) + b(gf − di) + c(dh − eg)
$$
We can reduce the number of operations by reusing numbers such as “ei-minus-hf.”
我们可以通过重复使用“ei-minus-hf”等数字来减少运算次数。

The algorithm for the ray-triangle intersection for which we need the linear solution can have some conditions for early termination. Thus, the function should look something like:  
我们需要线性解的射线与三角形相交的算法可以有一些提前终止的条件。 因此，该函数应该类似于：

```python
boolean raytri (ray r, vector3 a, vector3 b, vector3 c, interval [t0, t1])
    compute t
    if (t < t0) or (t > t1) then
    	return false
    
    compute γ
    if (γ < 0) or (γ > 1) then
    	return false
    
    compute β
    if (β < 0) or (β > 1 − γ) then
    	return false
    
    return true
```

### 4.4.3 Ray-Polygon Intersection 射线与多边形相交

Given a planar polygon with m vertices $\bold{p}_1$ through $\bold{p}_m$ and surface normal $\bold{n}$, we first compute the intersection points between the ray $\bold{e} + t\bold{d}$ and the plane containing the polygon with implicit equation
给定一个具有 m 个顶点 $\bold{p}_1$ 到 $\bold{p}_m$ 和表面法线 $\bold{n}$ 的平面多边形，我们首先计算光线 $\bold{e}  + t\bold{d}$ 之间的交点和包含具有隐式方程的多边形的平面
$(\bold{p} - \bold{p}_1) · \bold{n} = 0.  $

We do this by setting $\bold{p} = \bold{e} + t\bold{d}$ and solving for $t$ to get
我们通过设置 $\bold{p} = \bold{e} + t\bold{d}$ 并求解 $t$ 得到
$t = \frac{(\bold{p}_1 - \bold{e}) · \bold{n}  } {\bold{d} · \bold{n}  } \\$

This allows us to compute $\bold{p}$. If $\bold{p}$ is inside the polygon, then the ray hits it; otherwise, it does not.
这使我们能够计算$\bold{p}$。 如果 $\bold{p}$ 在多边形内部，则光线击中它； 否则，它不会。

We can answer the question of whether $\bold{p}$ is inside the polygon by projecting the point and polygon vertices to the $xy$ plane and answering it there. The easiest way to do this is to send any 2D ray out from $\bold{p}$ and to count the number of intersections between that ray and the boundary of the polygon (Sutherland, Sproull, & Schumacker, 1974; Glassner, 1989). If the number of intersections is odd, then the point is inside the polygon; otherwise it is not. This is true because a ray that goes in must go out, thus creating a pair of intersections. Only a ray that starts inside will not create such a pair. To make computation simple, the 2D ray may as well propagate along the x-axis:  
我们可以通过将点和多边形顶点投影到 $xy$ 平面并在那里回答来回答 $\bold{p}$ 是否在多边形内部的问题。 最简单的方法是从 $\bold{p}$ 发出任何 2D 射线，并计算该射线与多边形边界之间的交点数量 (Sutherland, Sproull, & Schumacker, 1974; Glassner, 1989 ）。 如果交点的数量是奇数，则该点在多边形内部； 否则就不是。 这是正确的，因为进入的光线必须出去，从而创建一对交叉点。 只有从内部开始的射线不会创建这样的射线对。 为了使计算简单，2D 射线也可以沿 x 轴传播：
$$
\begin{bmatrix}
x \\
y
\end{bmatrix}
 = \begin{bmatrix}
x_p \\
y_p
\end{bmatrix}
+ s\begin{bmatrix}
1 \\
0
\end{bmatrix}
$$
It is straightforward to compute the intersection of that ray with the edges such as $(x_1, y_1, x_2, y_2)$ for $s ∈ (0, ∞)$. 
计算该射线与边的交集很简单，例如 $(x_1, y_1, x_2, y_2)$ 对于 $s ∈ (0, ∞)$。

A problem arises, however, for polygons whose projection into the $xy$ plane is a line. To get around this, we can choose among the $xy$, $yz$, or $zx$ planes for whichever is best. If we implement our points to allow an indexing operation, e.g., $\bold{p}(0) = x_p$ then this can be accomplished as follows:  
然而，对于在 $xy$ 平面上的投影是一条线的多边形，就会出现问题。 为了解决这个问题，我们可以在 $xy$、$yz$ 或 $zx$ 平面中选择最好的一个。 如果我们实现我们的点以允许索引操作，例如 $\bold{p}(0) = x_p$ 则可以按如下方式完成：

```python
if (abs(zn) > abs(xn)) and (abs(zn) > abs(yn)) then
	index0 = 0
	index1 = 1
else if (abs(yn) > abs (xn)) then
	index0 = 0
	index1 = 2
else
	index0 = 1
	index1 = 2
```

Now, all computations can use $\bold{p}$(index0) rather than $x_p$, and so on. 
现在，所有的计算都可以使用$\bold{p}$(index0)而不是$x_p$，以此类推。

Another approach to polygons, one that is often used in practice, is to replace them by several triangles.
另一种在实践中经常使用的多边形方法是将它们替换为多个三角形。

### 4.4.4 Intersecting a Group of Objects 一组对象相交

Of course, most interesting scenes consist of more than one object, and when we intersect a ray with the scene we must find only the closest intersection to the camera along the ray. A simple way to implement this is to think of a group of objects as itself being another type of object. To intersect a ray with a group, you simply intersect the ray with the objects in the group and return the intersection with the smallest $t$ value. The following code tests for hits in the interval $t ∈ [t_0, t_1]$:  
当然，最有趣的场景由多个对象组成，当我们将一条光线与场景相交时，我们必须只找到沿光线与相机最近的交点。 实现这一点的一个简单方法是将一组对象本身视为另一种类型的对象。 要将射线与组相交，只需将射线与组中的对象相交并返回具有最小 $t$ 值的交集。 以下代码测试区间 $t ∈ [t_0, t_1]$ 中的命中：

```python
hit = false
for each object o in the group do
	if (o is hit at ray parameter t and t ∈ [t0, t1]) then
		hit = true
		hitobject = o
		t1 = t
return hit
```

![Figure 4.11](.\Images\Figure 4.11.png)
Figure 4.11. A simple scene rendered with only ray generation and surface intersection, but no shading; each pixel is just set to a fixed color depending on which object it hit. 
图 4.11  一个简单的场景，仅使用光线生成和表面相交进行渲染，但没有着色； 每个像素只是根据它击中的对象设置为固定颜色。

## 4.5 Shading  着色

Once the visible surface for a pixel is known, the pixel value is computed by evaluating a shading model. How this is done depends entirely on the application—methods range from very simple heuristics to elaborate numerical computations. In this chapter we describe the two most basic shading models; more advanced models are discussed in Chapter 10.
一旦知道像素的可见表面，就可以通过评估着色模型来计算像素值。 如何做到这一点完全取决于应用程序，方法范围从非常简单的启发式到复杂的数值计算。 在本章中，我们描述了两种最基本的着色模型； 第 10 章讨论了更高级的模型。

Most shading models, one way or another, are designed to capture the process of light reflection, whereby surfaces are illuminated by light sources and reflect part of the light to the camera. Simple shading models are defined in terms of illumination from a point light source. The important variables in light reflection are the light direction $\bold{l}$, which is a unit vector pointing toward the light source; the view direction $\bold{v}$, which is a unit vector pointing toward the eye or camera; the surface normal $\bold{n}$, which is a unit vector perpendicular to the surface at the point where reflection is taking place; and the characteristics of the surface—color, shininess, or other properties depending on the particular model. 
大多数着色模型都以某种方式设计为捕捉光反射的过程，即表面被光源照亮并将部分光反射到相机。 简单的着色模型是根据点光源的照明来定义的。 光反射中重要的变量是光方向$\bold{l}$，它是指向光源的单位向量； 视图方向$\bold{v}$，它是指向眼睛或相机的单位向量； 表面法线$\bold{n}$，它是发生反射的点处垂直于表面的单位向量； 以及表面特征——颜色、光泽度或其他属性，具体取决于特定模型。

### 4.5.1 Lambertian Shading 朗伯着色

The simplest shading model is based on an observation made by Lambert in the 18th century: the amount of energy from a light source that falls on an area of surface depends on the angle of the surface to the light. A surface facing directly toward the light receives maximum illumination; a surface tangent to the light direction (or facing away from the light) receives no illumination; and in between the illumination is proportional to the cosine of the angle $θ$ between the surface normal and the light source (Figure 4.12). This leads to the Lambertian shading model: 
最简单的着色模型基于 Lambert 在 18 世纪的观察：光源落在表面区域上的能量取决于表面与光线的角度。 直接面向光的表面接收最大照度； 与光方向相切（或背向光）的表面不受照明； 其间的照明度与表面法线和光源之间的角度 $θ$ 的余弦成正比（图 4.12）。 这导致了朗伯着色模型：
$L = k_d I max(0, \bold{n} · \bold{l})  $

where $L$ is the pixel color; $k_d$ is the diffuse coefficient, or the surface color; and $I$ is the intensity of the light source. Because $\bold{n}$ and $\bold{l}$ are unit vectors, we can  use $\bold{n} · \bold{l}$ as a convenient shorthand (both on paper and in code) for $\cos θ$. This equation (as with the other shading equations in this section) applies separately to the three color channels, so the red component of the pixel value is the product of the red diffuse component, the red light source intensity, and the dot product; the same holds for green and blue.  
其中$L$为像素颜色;$k_d$为漫射系数，即表面颜色;$I$为光源的强度。因为$\bold{n}$和$\bold{l}$是单位向量，我们可以使用$\bold{n}·\bold{l}$作为$\cos θ$的方便速记(无论是在纸上还是在代码中)。该方程(与本节中的其他阴影方程一样)分别适用于三个颜色通道，因此像素值的红色分量是红色漫射分量、红色光源强度和点积的乘积;绿色和蓝色也是如此。
![Figure 4.12](.\Images\Figure 4.12.png)
Figure 4.12. Geometry for Lambertian shading.
图 4.12  朗伯着色的几何形状。

> Illumination from real point sources falls off as distance squared, but that is often more trouble than it’s worth in a simple renderer.  
> 来自真实点光源的照明随着距离的平方而下降，但在简单的渲染器中，这通常比它的价值更麻烦。

The vector $\bold{l}$ is computed by subtracting the intersection point of the ray and surface from the light source position. Don’t forget that $\bold{v}$, $\bold{l}$, and $\bold{n}$ all must be unit vectors; failing to normalize these vectors is a very common error in shading computations.  
向量$\bold{l}$是通过从光源位置减去光线和表面的交点来计算的。 不要忘记 $\bold{v}$、$\bold{l}$ 和 $\bold{n}$ 都必须是单位向量； 未能对这些向量进行归一化是着色计算中非常常见的错误。

> When in doubt, make light sources neutral in color, with equal red, green, and blue intensities.  
> 如有疑问，请使光源颜色为中性，具有相同的红色、绿色和蓝色强度。

### 4.5.2 Blinn-Phong Shading Blinn-Phong 着色

Lambertian shading is view independent: the color of a surface does not depend on the direction from which you look. Many real surfaces show some degree of shininess, producing highlights, or specular reflections, that appear to move around as the viewpoint changes. Lambertian shading doesn’t produce any highlights and leads to a very matte, chalky appearance, and many shading models add a specular component to Lambertian shading; the Lambertian part is then the diffuse component.  
朗伯着色与视图无关：表面的颜色不取决于您观察的方向。 许多真实的表面显示出一定程度的光泽，产生高光或镜面反射，随着视点的变化而看起来会移动。 朗伯着色不会产生任何高光，并会导致非常哑光、白垩色的外观，并且许多着色模型向朗伯着色添加镜面反射组件； 那么朗伯部分就是漫反射分量。

A very simple and widely used model for specular highlights was proposed by Phong (Phong, 1975) and later updated by Blinn (J. F. Blinn, 1976) to the form most commonly used today. The idea is to produce reflection that is at its brightest when $\bold{v}$ and $\bold{l}$ are symmetrically positioned across the surface normal, which is when mirror reflection would occur; the reflection then decreases smoothly as the vectors move away from a mirror configuration. 
Phong (Phong, 1975)提出了一个非常简单和广泛使用的镜面高光模型，后来由Blinn (J. F. Blinn, 1976)更新为今天最常用的形式。这个想法是产生最亮的反射，当$\bold{v}$和$\bold{l}$对称地放置在表面法线上，这是镜子反射发生的时候；然后，随着矢量远离镜像配置，反射平滑地减小。

![Figure 4.15](.\Images\Figure 4.15.png)
Figure 4.13. A simple scene rendered with diffuse shading from a single light source.  
图4.13 一个简单的场景渲染漫射阴影从一个单一的光源。

![Figure 4.14](.\Images\Figure 4.14.png)
Figure 4.14. A simple scene rendered with diffuse shading and shadows (Section 4.7) from three light sources. 
图4.14 一个简单的场景渲染漫射阴影和阴影(第4.7节)从三个光源。

![Figure 4.13](.\Images\Figure 4.13.png)
Figure 4.15. A simple scene rendered with diffuse shading (blue sphere), Blinn-Phong shading (green sphere), and shadows from three light sources.  
图4.15 一个简单的场景渲染漫射阴影(蓝色球)，Blinn-Phong阴影(绿色球)，并从三个光源的阴影。

We can tell how close we are to a mirror configuration by comparing the half vector $\bold{h}$ (the bisector of the angle between $\bold{v}$ and $\bold{l}$) to the surface normal (Figure 4.16). If the half vector is near the surface normal, the specular component  should be bright; if it is far away it should be dim. This result is achieved by computing the dot product between $\bold{h}$ and $\bold{n}$ (remember they are unit vectors, so  $\bold{n} · \bold{h}$ reaches its maximum of 1 when the vectors are equal), then taking the result to a power $p > 1$ to make it decrease faster. The power, or Phong exponent, controls the apparent shininess of the surface. The half vector itself is easy to compute: since $\bold{v}$ and $\bold{l}$ are the same length, their sum is a vector that bisects the angle between them, which only needs to be normalized to produce $\bold{h}$. 
我们可以通过比较半向量 $\bold{h}$ （$\bold{v}$ 和 $\bold{l}$ 之间的角度平分线）与表面法线来判断我们与镜像配置的接近程度 （图 4.16）。 如果半向量接近表面法线，则镜面反射分量应该是明亮的； 如果距离较远，则应该是昏暗的。 这个结果是通过计算 $\bold{h}$ 和 $\bold{n}$ 之间的点积来实现的（记住它们是单位向量，因此 $\bold{n} · \bold{h}$ 达到其最大值 1（当向量相等时），然后对结果进行 $p > 1$ 次方，使其减少得更快。 功率或 Phong 指数控制表面的表观光泽度。 半向量本身很容易计算：由于 $\bold{v}$ 和 $\bold{l}$ 长度相同，因此它们的和是平分它们之间角度的向量，只需对其进行归一化即可产生 $\bold{h}$。
![Figure 4.16](.\Images\Figure 4.16.png)
Figure 4.16. Geometry for Blinn-Phong shading. 
图 4.16  Blinn-Phong 着色的几何形状。

Putting this all together, the Blinn-Phong shading model is as follows: 
将所有这些放在一起，Blinn-Phong 着色模型如下：
$$
\bold{h} = \frac{\bold{v} + \bold{l}}{\|\bold{v} + \bold{l}\|} \\
L = k_d I max(0, \bold{n} · \bold{l}) + k_s I max(0, \bold{n} · \bold{h})^p
$$
where $k_s$ is the specular coefficient, or the specular color, of the surface. 
其中 $k_s$ 是表面的镜面反射系数或镜面反射颜色。

> Typical values of p:
> 10—“eggshell”;
> 100—mildly shiny;
> 1000—really glossy;
> 10,000—nearly mirror-like.  
> p 的典型值： 10——“蛋壳”； 100——轻微光泽； 1000——非常有光泽； 10,000——几乎像镜子一样。

> When in doubt, make the specular color gray, with equal red, green, and blue values.  
> 如有疑问，请将镜面反射颜色设置为灰色，并具有相同的红色、绿色和蓝色值。

### 4.5.3 Ambient Shading 环境着色

Surfaces that receive no illumination at all will be rendered as completely black, which is often not desirable. A crude but useful heuristic to avoid black shadows  is to add a constant component to the shading model, one whose contribution to the pixel color depends only on the object hit, with no dependence on the surface geometry at all. This is known as ambient shading—it is as if surfaces were illuminated by “ambient” light that comes equally from everywhere. For  convenience in tuning the parameters, ambient shading is usually expressed as the product of a surface color with an ambient light color, so that ambient shading can be tuned for surfaces individually or for all surfaces together. Together with the rest of the Blinn-Phong model, ambient shading completes the full version of a simple and useful shading model:
完全没有受到照明的表面将被渲染为全黑，这通常是不可取的。 避免黑色着色的一种粗略但有用的启发式方法是向着色模型添加一个常量组件，该组件对像素颜色的贡献仅取决于物体击中，而完全不依赖于表面几何形状。 这被称为环境着色——就好像表面被来自各处的“环境”光照亮一样。 为了方便调整参数，环境明暗通常表示为表面颜色与环境光颜色的乘积，以便可以针对单独的表面或针对所有表面一起调整环境明暗。 与 Blinn-Phong 模型的其余部分一起，环境着色完成了简单且有用的着色模型的完整版本：
$$
L = k_aI_a + k_d I max(0, \bold{n} · \bold{l}) + k_s I max(0, \bold{n} · \bold{h})^n, (4.3)
$$
where $k_a$ is the surface’s ambient coefficient, or “ambient color,” and $I_a$ is the  ambient light intensity.
其中 $k_a$ 是表面的环境系数或“环境颜色”，$I_a$ 是环境光强度。

> In the real world, surfaces that are not illuminated by light sources are illuminated by indirect reflections from other surfaces.  
> 在现实世界中，未被光源照亮的表面会被其他表面的间接反射照亮。

> When in doubt set the ambient color to be the same as the diffuse color.  
> 如果有疑问，请将环境颜色设置为与漫反射颜色相同。

### 4.5.4 Multiple Point Lights  

A very useful property of light is superposition—the effect caused by more than one light source is simply the sum of the effects of the light sources individually. For this reason, our simple shading model can easily be extended to handle $N$ light sources:  
$$
L = k_a I_a + \sum^N_{i = 1}[k_d I_i max(0, \bold{n} · \bold{l}_i) + k_s I_i max(0, \bold{n} · \bold{h}_i)^p] \ \ \  \ \ (4.4)
$$
where $I_i$, $l_i$, and $h_i$ are the intensity, direction, and half vector of the $i^{th}$ light source.  
其中$I_i$、$l_i$和$h_i$是$i^{th}$光源的强度、方向和半矢量。



## 4.6 A Ray-Tracing Program 光线追踪程序

We now know how to generate a viewing ray for a given pixel, how to find the closest intersection with an object, and how to shade the resulting intersection. These are all the parts required for a program that produces shaded images with hidden surfaces removed.  
我们现在知道如何为给定像素生成视线，如何找到与对象最近的交点，以及如何对所得交点进行着色。 这些是生成删除了隐藏表面的着色图像的程序所需的所有部分。

```lua
for each pixel do
	compute viewing ray
	if (ray hits an object with t ∈ [0, ∞)) then
		Compute n
		Evaluate shading model and set pixel to that color
	else
		set pixel color to background color
```

Here the statement “if ray hits an object . . . ” can be implemented using the algorithm of Section 4.4.4.
这里的陈述“如果光线击中一个物体 . . . ”可以使用4.4.4节的算法来实现。

In an actual implementation, the surface intersection routine needs to somehow return either a reference to the object that is hit, or at least its normal vector and shading-relevant material properties. This is often done by passing a record/structure with such information. In an object-oriented implementation, it is a good idea to have a class called something like surface with derived classes triangle, sphere, group, etc. Anything that a ray can intersect would be under that class. The ray-tracing program would then have one reference to a “surface” for the whole model, and new types of objects and efficiency structures can be added transparently.
在实际实现中，表面相交例程需要以某种方式返回对被击中的对象的引用，或者至少返回其法线向量和与着色相关的材质属性。 这通常是通过传递包含此类信息的记录/结构来完成的。 在面向对象的实现中，最好有一个名为 Surface 的类，其派生类为三角形、球体、组等。任何光线可以相交的东西都将位于该类下。 然后，光线追踪程序将对整个模型的“表面”进行一次引用，并且可以透明地添加新类型的对象和效率结构。

### 4.6.1 Object-Oriented Design for a Ray-Tracing Program 光线追踪程序的面向对象设计

As mentioned earlier, the key class hierarchy in a ray tracer are the geometric objects that make up the model. These should be subclasses of some geometric object class, and they should support a hit function (Kirk & Arvo, 1988). To avoid confusion from use of the word “object,” surface is the class name often used. With such a class, you can create a ray tracer that has a general interface that assumes little about modeling primitives and debug it using only spheres. An important point is that anything that can be “hit” by a ray should be part of this class hierarchy, e.g., even a collection of surfaces should be considered a subclass of the surface class. This includes efficiency structures, such as bounding volume hierarchies; they can be hit by a ray, so they are in the class. 
如前所述，光线追踪器中的关键类层次结构是构成模型的几何对象。 这些应该是某些几何对象类的子类，并且它们应该支持命中函数（Kirk & Arvo，1988）。 为了避免使用“对象”一词造成混淆，表面是经常使用的类名称。 使用这样的类，您可以创建一个具有通用接口的光线追踪器，该接口对建模基元几乎不做任何假设，并且仅使用球体对其进行调试。 重要的一点是，任何可以被光线“击中”的东西都应该是这个类层次结构的一部分，例如，即使是表面的集合也应该被视为表面类的子类。 这包括效率结构，例如包围体层次结构； 他们可以被射线击中，所以他们在班级里。

For example, the “abstract” or “base” class would specify the hit function as well as a bounding box function that will prove useful later: 
例如，“抽象”或“基”类将指定命中函数以及稍后将证明有用的边界框函数：

```python
class surface
	virtual bool hit(ray e + td, real t0, real t1, hit-record rec)
	virtual box bounding-box()
```

Here $(t_0, t_1)$ is the interval on the ray where hits will be returned, and rec is are cord that is passed by reference; it contains data such as the t at the intersection when hit returns true. The type box is a 3D “bounding box,” that is two points that define an axis-aligned box that encloses the surface. For example, for a sphere,t he function would be implemented by  
这里$(t_0, t_1)$是射线上将返回命中的间隔，而rec是通过引用传递的绳索； 它包含诸如当 hit 返回 true 时交点处的 t 之类的数据。 类型框是一个 3D“边界框”，即定义包围曲面的轴对齐框的两个点。 例如，对于一个球体，该函数将通过以下方式实现

```python
box sphere::bounding-box()
	vector3 min = center − vector3(radius,radius,radius)
	vector3 max = center + vector3(radius,radius,radius)
	return box(min, max)
```

Another class that is useful is material. This allows you to abstract the material behavior and later add materials transparently. A simple way to link objects and materials is to add a pointer to a material in the surface class, although more programmable behavior might be desirable. A big question is what to do with textures; are they part of the material class or do they live outside of the material class? This will be discussed more in Chapter 11.
另一个有用的类别是材料。 这使您可以抽象材质行为，然后透明地添加材质。 链接对象和材质的一种简单方法是在表面类中添加指向材质的指针，尽管可能需要更多的可编程行为。 一个大问题是如何处理纹理； 他们是物质阶层的一部分还是生活在物质阶层之外？ 这将在第 11 章中详细讨论。

## 4.7 Shadows 阴影

Once you have a basic ray tracing program, shadows can be added very easily. Recall from Section 4.5 that light comes from some direction $\bold{l}$. If we imagine ourselves at a point $\bold{p}$ on a surface being shaded, the point is in shadow if we “look” in direction $\bold{l}$ and see an object. If there are no objects, then the light is not blocked.  
一旦有了基本的光线追踪程序，就可以非常轻松地添加阴影。 回想一下 4.5 节，光来自某个方向 $\bold{l}$。 如果我们想象自己位于被阴影表面上的一个点 $\bold{p}$ 处，那么如果我们向 $\bold{l}$ 方向“看”并看到一个物体，则该点处于阴影中。 如果没有物体，那么光线就不会被阻挡。

This is shown in Figure 4.17, where the ray $\bold{p} + t\bold{l}$ does not hit any objects and is thus not in shadow. The point $\bold{q}$ is in shadow because the ray $\bold{q} + t\bold{l}$ does hit an object. The vector $\bold{l}$ is the same for both points because the light is “far” away. This assumption will later be relaxed. The rays that determine in or out of shadow are called shadow rays to distinguish them from viewing rays.  
如图 4.17 所示，其中光线 $\bold{p} + t\bold{l}$ 没有击中任何物体，因此不在阴影中。 点 $\bold{q}$ 位于阴影中，因为光线 $\bold{q} + t\bold{l}$ 确实击中了物体。 两个点的向量 $\bold{l}$ 是相同的，因为光距离“很远”。 这个假设稍后会被放宽。 确定阴影内或阴影外的光线称为阴影光线，以区别于观察光线。
![Figure 4.17](.\Images\Figure 4.17.png)
Figure 4.17. The point $\bold{p}$ is not in shadow, while the point $\bold{q}$  is in shadow.  
图 4.17  点 $\bold{p}$ 不在阴影中，而点 $\bold{q}$ 在阴影中

To get the algorithm for shading, we add an if statement to determine whether the point is in shadow. In a naive implementation, the shadow ray will check for $t ∈ [0, ∞)$, but because of numerical imprecision, this can result in an intersection with the surface on which $\bold{p}$ lies. Instead, the usual adjustment to avoid that problem is to test for $t ∈ [\epsilon, ∞)$ where $\epsilon$ is some small positive constant (Figure 4.18).  
为了获得阴影算法，我们添加一个 if 语句来确定该点是否处于阴影中。 在简单的实现中，阴影光线将检查 $t ∈ [0, ∞)$，但由于数值不精确，这可能会导致与 $\bold{p}$ 所在的表面相交。 相反，避免该问题的通常调整是测试 $t ∈ [\epsilon, ∞)$，其中 $\epsilon$ 是一些小的正常数（图 4.18）。
![Figure 4.18](.\Images\Figure 4.18.png)
Figure 4.18. By testing in the interval starting at $\epsilon$, we avoid numerical imprecision causing the ray to hit the surface $\bold{p}$ is on. 
图 4.18  通过在从 $\epsilon$ 开始的间隔中进行测试，我们可以避免数值不精确导致光线撞击 $\bold{p}$ 所在的表面

If we implement shadow rays for Phong lighting with Equation 4.3 then we have the following:  
如果我们使用公式 4.3 实现 Phong 照明的阴影光线，则我们有以下结果：
<img src=".\Images\Figure 4.18_1.png" alt="Figure 4.18" style="zoom:80%;" />

Note that the ambient color is added whether $\bold{p}$ is in shadow or not. If there are multiple light sources, we can send a shadow ray before evaluating the shading model for each light. The code above assumes that $\bold{d}$ and $\bold{l}$ are not necessarily unit vectors. This is crucial for $\bold{d}$, in particular, if we wish to cleanly add instancing later (see Section 13.2).
请注意，无论 $\bold{p}$ 是否处于阴影中，都会添加环境颜色。 如果有多个光源，我们可以在评估每个光源的着色模型之前发送阴影光线。 上面的代码假设 $\bold{d}$ 和 $\bold{l}$ 不一定是单位向量。 这对于 $\bold{d}$ 至关重要，特别是如果我们希望稍后干净地添加实例（参见第 13.2 节）。

## 4.8 Ideal Specular Reflection 理想的镜面反射

It is straightforward to add ideal specular reflection, or mirror reflection, to a raytracing program. The key observation is shown in Figure 4.19 where a viewer looking from direction $\bold{e}$ sees what is in direction $\bold{r}$ as seen from the surface. The vector $\bold{r}$ is found using a variant of the Phong lighting reflection Equation (10.6). There are sign changes because the vector $\bold{d}$ points toward the surface in this case, so,  
将理想的镜面反射或镜面反射添加到光线跟踪程序中非常简单。 关键观察结果如图 4.19 所示，其中从 $\bold{e}$ 方向观看的观看者看到的是从表面看到的 $\bold{r}$ 方向的内容。 向量 $\bold{r}$ 是使用 Phong 光照反射方程 (10.6) 的变体找到的。 符号发生变化，因为在这种情况下向量 $\bold{d}$ 指向表面，因此，
$$
\bold{r} = \bold{d} − 2(\bold{d} · \bold{n})\bold{n}. \ \ \ \ (4.5)
$$
![Figure 4.19](.\Images\Figure 4.19.png)
Figure 4.19. When looking into a perfect mirror, the viewer looking in direction $\bold{d}$ will see whatever the viewer “below” the surface would see in direction $\bold{r}$. 
图 4.19  当观察完美的镜子时，朝 $\bold{d}$ 方向看的观看者将看到表面“下方”的观看者在 $\bold{r}$ 方向上看到的任何内容。

In the real world, some energy is lost when the light reflects from the surface, and this loss can be different for different colors. For example, gold reflects yellow more efficiently than blue, so it shifts the colors of the objects it reflects. This can be implemented by adding a recursive call in raycolor: 
在现实世界中，当光从表面反射时，会损失一些能量，并且对于不同的颜色，这种损失可能不同。 例如，金色比蓝色更有效地反射黄色，因此它会改变所反射物体的颜色。 这可以通过在raycolor中添加递归调用来实现：
$color\ c = c + k_m raycolor(\bold{p} + s\bold{r}, \epsilon, ∞)  $

where $k_m$ (for “mirror reflection”) is the specular RGB color. We need to make sure we test for $s ∈ [	\epsilon, ∞)$ for the same reason as we did with shadow rays; we don’t want the reflection ray to hit the object that generates it. 
其中 $k_m$（“镜面反射”）是镜面 RGB 颜色。 我们需要确保测试 $s ∈ [ \epsilon, ∞)$ 的原因与我们测试阴影光线的原因相同； 我们不希望反射光线击中产生它的物体。

The problem with the recursive call above is that it may never terminate. For example, if a ray starts inside a room, it will bounce forever. This can be fixed by adding a maximum recursion depth. The code will be more efficient if a reflection ray is generated only if $k_m$ is not zero (black). 
上面的递归调用的问题是它可能永远不会终止。 例如，如果光线从房间内开始，它将永远反弹。 这可以通过添加最大递归深度来解决。 如果仅当 $k_m$ 不为零（黑色）时才生成反射光线，则代码将会更有效。
![Figure 4.20](.\Images\Figure 4.20.png)
Figure 4.20. A simple scene rendered with diffuse and Blinn-Phong shading, shadows from three light sources, and specular reflection from the floor.
图 4.20  使用漫反射和 Blinn-Phong 着色、来自三个光源的阴影以及来自地板的镜面反射渲染的简单场景。

## 4.9 Historical Notes 历史笔记

Ray tracing was developed early in the history of computer graphics (Appel, \1968) but was not used much until sufficient compute power was available (Kay & Greenberg, 1979; Whitted, 1980).
光线追踪是在计算机图形学历史的早期开发的（Appel，\1968），但直到有足够的计算能力才得到广泛使用（Kay & Greenberg，1979；Whitted，1980）。

Ray tracing has a lower asymptotic time complexity than basic object-order rendering (Snyder & Barr, 1987; Muuss, 1995; S. Parker et al., 1999; Wald, Slusallek, Benthin, & Wagner, 2001). Although it was traditionally thought of  as an offline method, real-time ray tracing implementations are becoming more and more common.
光线追踪的渐近时间复杂度低于基本的对象顺序渲染（Snyder & Barr，1987；Muuss，1995；S. Parker 等，1999；Wald、Slusallek、Benthin 和 Wagner，2001）。 尽管传统上它被认为是一种离线方法，但实时光线追踪实现正变得越来越普遍。

## Frequently Asked Questions  经常问的问题

### Why is there no perspective matrix in ray tracing? 为什么光线追踪中没有透视矩阵？

The perspective matrix in a z-buffer exists so that we can turn the perspective projection into a parallel projection. This is not needed in ray tracing, because it is easy to do the perspective projection implicitly by fanning the rays out from the eye.
z 缓冲区中存在透视矩阵，以便我们可以将透视投影转换为平行投影。 这在光线追踪中是不需要的，因为通过将光线从眼睛扇形散开来隐式地进行透视投影很容易。

### Can ray tracing be made interactive? 光线追踪可以交互吗？

For sufficiently small models and images, any modern PC is sufficiently powerful for ray tracing to be interactive. In practice, multiple CPUs with a shared frame buffer are required for a full-screen implementation. Computer power is increasing much faster than screen resolution, and it is just a matter of time before conventional PCs can ray trace complex scenes at screen resolution.
对于足够小的模型和图像，任何现代 PC 都足够强大，可以进行交互式光线追踪。 实际上，全屏实现需要多个具有共享帧缓冲区的 CPU。 计算机能力的增长速度远远快于屏幕分辨率的增长速度，传统 PC 以屏幕分辨率对复杂场景进行光线追踪只是时间问题。

### Is ray tracing useful in a hardware graphics program? 光线追踪在硬件图形程序中有用吗？

Ray tracing is frequently used for picking. When the user clicks the mouse on a pixel in a 3D graphics program, the program needs to determine which object is visible within that pixel. Ray tracing is an ideal way to determine that. 
光线追踪经常用于拾取。 当用户在 3D 图形程序中的像素上单击鼠标时，程序需要确定该像素内哪个对象是可见的。 光线追踪是确定这一点的理想方法。

## Exercises

1. What are the ray parameters of the intersection points between ray $(1, 1, 1)+ t(-1, -1, -1)$ and the sphere centered at the origin with radius 1? Note: this is a good debugging case. 
   射线 $(1, 1, 1)+ t(-1, -1, -1)$ 与以原点为中心、半径为 1 的球体之间的交点的射线参数是多少？ 注意：这是一个很好的调试案例。
2. What are the barycentric coordinates and ray parameter where the ray $(1, 1, 1) + t(-1, -1, -1)$ hits the triangle with vertices $(1, 0, 0)$, $(0, 1, 0)$, and $(0, 0, 1)$? Note: this is a good debugging case. 
   当射线$(1,1,1)+ t(-1， -1， -1)$碰到顶点$(1,0,0)$，$(0,1,0)$和$(0,0,1)$的三角形时，质心坐标和射线参数是什么?注意:这是一个很好的调试案例。
3. Do a back of the envelope computation of the approximate time complexity of ray tracing on “nice” (non-adversarial) models. Split your analysis into the cases of preprocessing and computing the image, so that you can predict the behavior of ray tracing multiple frames for a static model. 
   对“好的”（非对抗性）模型上的光线追踪的近似时间复杂度进行回溯计算。 将您的分析分为预处理和计算图像的情况，以便您可以预测静态模型的光线追踪多帧的行为。



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

# 6  Transformation Matrices 变换矩阵

The machinery of linear algebra can be used to express many of the operations required to arrange objects in a 3D scene, view them with cameras, and get them onto the screen. Geometric transformations like rotation, translation, scaling, and projection can be accomplished with matrix multiplication, and the transformation matrices used to do this are the subject of this chapter.
线性代数机制可用于表达在 3D 场景中排列对象、使用相机查看它们并将它们显示到屏幕上所需的许多操作。 旋转、平移、缩放和投影等几何变换可以通过矩阵乘法来完成，用于执行此操作的变换矩阵是本章的主题。

We will show how a set of points transforms if the points are represented as offset vectors from the origin, and we will use the clock shown in Figure 6.1 as an example of a point set. So think of the clock as a bunch of points that are the ends of vectors whose tails are at the origin. We also discuss how these transforms operate differently on locations (points), displacement vectors, and surface normal vectors.  
我们将展示如果将点表示为距原点的偏移向量，则一组点将如何变换，并且我们将使用图 6.1 中所示的时钟作为点集的示例。 因此，可以将时钟视为一堆点，这些点是尾部位于原点的向量的末端。 我们还讨论了这些变换如何对位置（点）、位移向量和表面法线向量进行不同的操作。我们将展示如果将点表示为距原点的偏移向量，则一组点将如何变换，并且我们将使用图 6.1 中所示的时钟作为点集的示例。 因此，可以将时钟视为一堆点，这些点是尾部位于原点的向量的末端。 我们还讨论了这些变换如何对位置（点）、位移向量和表面法线向量进行不同的操作。

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
这种采用一个 2 向量并通过简单的矩阵乘法产生另一个 2 向量的运算是线性变换。

By this simple formula we can achieve a variety of useful transformations, depending on what we put in the entries of the matrix, as will be discussed in the following sections. For our purposes, consider moving along the x-axis a horizontal move and along the y-axis, a vertical move.
通过这个简单的公式，我们可以实现各种有用的变换，具体取决于我们在矩阵条目中放入的内容，这将在以下各节中讨论。 出于我们的目的，考虑沿 x 轴移动为水平移动，沿 y 轴移动为垂直移动。

### 6.1.1 Scaling 缩放

The most basic transform is a scale along the coordinate axes. This transform can change length and possibly direction: 
最基本的变换是沿坐标轴的缩放。 这种变换可以改变长度和可能的方向：
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
因此，只需查看轴对齐比例的矩阵，我们就可以读出两个比例因子。

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
图 6.1 每个轴统一缩放一半：轴对齐的缩放矩阵具有每个对角线元素的变化比例以及非对角线元素的零。

A matrix which halves in the horizontal and increases by three-halves in the vertical is (see Figure 6.2) 
水平方向减半、垂直方向增加三半的矩阵是（见图 6.2）
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
剪刀是将物体向侧面推的东西，产生类似于一副纸牌的东西，你可以用手推过它； 底部的牌保持原状，并且离牌堆顶部越近的牌移动得越多。 水平和垂直剪切矩阵是
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

Suppose we want to rotate a vector $\bold{a}$ by an angle $φ$ counterclockwise to get vector $\bold{b}$ (Figure 6.5). If a makes an angle $α$ with the x-axis, and its length is $r = \sqrt{x^2_a + y^2_a}$, then we know that
假设我们想将向量 $\bold{a}$ 逆时针旋转角度 $φ$ 得到向量 $\bold{b}$ （图 6.5）。 如果 a 与 x 轴形成角度 $α$，且其长度为 $r = \sqrt{x^2_a + y^2_a}$，那么我们知道
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
因为旋转矩阵每行的范数为 1 $(sin^2 φ+cos^2 φ = 1)$，并且各行是正交的 $(cos φ(- sin φ) + sin φ cos φ = 0) $，我们看到旋转矩阵是正交矩阵（第 5.2.4 节）。 通过查看矩阵，我们可以读出两对正交向量：两列，它们是变换将规范基向量 $(1, 0)$ 和 $(0, 1)$ 发送到的向量； 和行，它们是变换发送到规范基向量的向量。

> Said briefly, $\bold{R}\bold{e}_i = \bold{u}_i$ and $\bold{R}\bold{v}_i = \bold{u}i$, for a rotation with columns $\bold{u}_i$ and rows $\bold{v}_i$. 
> 简单地说，$\bold{R}\bold{e}_i = \bold{u}_i$ 和 $\bold{R}\bold{v}_i = \bold{u}i$，用于列旋转 $\bold{u}_i$ 和行 $\bold{v}_i$。

### 6.1.4 Reflection 反射

We can reflect a vector across either of the coordinate axes by using a scale with one negative scale factor (see Figures 6.8 and 6.9): 
我们可以通过使用具有一个负比例因子的比例来反映跨任一坐标轴的矢量（见图 6.8 和 6.9）：
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
$first,\bold{v}_2 = \bold{S}\bold{v}_1, then,\bold{v}_3 = \bold{R}\bold{v}2.  $

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
图 6.10  按顺序应用两个变换矩阵与应用一次这些矩阵的乘积相同。 这是大多数图形硬件和软件的关键概念。

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
重要的是要始终记住矩阵乘法是不可交换的。 所以转换的顺序很重要。 在此示例中，先旋转，然后缩放，会产生不同的矩阵（参见图 6.11）：
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

Example. Using the scale matrices we have presented, nonuniform scaling can only be done along the coordinate axes. If we wanted to stretch our clock by 50% along one of its diagonals, so that 8:00 through 1:00 move to the northwest and 2:00 through 7:00 move to the southeast, we can use rotation matrices in
combination with an axis-aligned scaling matrix to get the result we want. The idea is to use a rotation to align the scaling axis with a coordinate axis, then scale along that axis, then rotate back. In our example, the scaling axis is the “backslash” diagonal of the square, and we can make it parallel to the x-axis with  a rotation by $+45◦$. Putting these operations together, the full transformation is
例子。 使用我们提出的尺度矩阵，非均匀缩放只能沿着坐标轴完成。 如果我们想沿着其中一条对角线拉伸时钟 50%，以便 8:00 到 1:00 向西北方向移动，2:00 到 7:00 向东南方向移动，我们可以使用旋转矩阵
与轴对齐缩放矩阵组合以获得我们想要的结果。 这个想法是使用旋转将缩放轴与坐标轴对齐，然后沿该轴缩放，然后向后旋转。 在我们的示例中，缩放轴是正方形的“反斜杠”对角线，我们可以使其与 x 轴平行，旋转 $+45°$。 将这些操作放在一起，完整的转换是
$rotate(-45◦) scale(1.5, 1) rotate(45◦)  $

> Remember to read the transformations from right to left. 
> 请记住从右到左阅读转换。

In mathematical notation, this can be written $\bold{R}\bold{S}\bold{R}^T$. The result of multiplying the three matrices together is
用数学符号来说，这可以写成RSRT。 三个矩阵相乘的结果是
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
有时有必要“撤消”变换的组合，将变换分解成更简单的部分。 例如，向用户呈现一个变换以便根据单独的旋转和缩放因子进行操作通常很有用，但变换可能在内部简单地表示为矩阵，其中旋转和缩放已经混合在一起。 如果可以通过计算将矩阵分解为所需的部分，调整这些部分，然后通过将这些部分再次相乘来重新组合矩阵，则可以实现这种操作。

It turns out that this decomposition, or factorization, is possible, regardless of the entries in the matrix—and this fact provides a fruitful way of thinking about transformations and what they do to geometry that is transformed by them.
事实证明，无论矩阵中的条目如何，这种分解或因式分解都是可能的，这一事实提供了一种富有成效的方式来思考变换以及它们对变换后的几何图形的作用。

#### Symmetric Eigenvalue Decomposition 对称特征值分解

Let’s start with symmetric matrices. Recall from Section 5.4 that a symmetric matrix can always be taken apart using the eigenvalue decomposition into a product of the form 
让我们从对称矩阵开始。 回想一下 5.4 节，对称矩阵总是可以使用特征值分解分解为以下形式的乘积
$\bold{A} = \bold{R}\bold{S}\bold{R}^T  $

where $\bold{R}$ is an orthogonal matrix and $\bold{S}$ is a diagonal matrix; we will call the columns of $\bold{R}$ (the eigenvectors) by the names $\bold{v}_1$ and $\bold{v}_2$, and we’ll call the diagonal entries of $\bold{S}$ (the eigenvalues) by the names $λ_1$ and $λ_2$. 
其中$\bold{R}$是正交矩阵，$\bold{S}$是对角矩阵； 我们将通过名称 $\bold{v}_1$ 和 $\bold{v}_2$ 来调用 $\bold{R}$ 的列（特征向量），我们将 $\bold{S}$ （特征值）的对角线条目命名为 $λ_1$ 和 $λ_2$。

In geometric terms we can now recognize $\bold{R}$ as a rotation and $\bold{S}$ as a scale, sot his is just a multi-step geometric transformation (Figure 6.13): 
用几何术语来说，我们现在可以将 $\bold{R}$ 识别为旋转，将 $\bold{S}$ 识别为缩放，因此他只是一个多步几何变换（图 6.13）：

1. Rotate $\bold{v}_1$ and $\bold{v}_2$ to the x- and y-axes (the transform by $R^T$).
   将 $\bold{v}_1$ 和 $\bold{v}_2$ 旋转到 x 轴和 y 轴（通过 $R^T$ 进行变换）。
2. Scale in $x$ and $y$ by $(λ1, λ2)$ (the transform by $\bold{S}$).
   按 $(λ1, λ2)$ 缩放 $x$ 和 $y$（通过 $\bold{S}$ 进行变换）。
3. Rotate the x- and y-axes back to $\bold{v}_1$ and $\bold{v}2$ (the transform by $\bold{R}$). 
   将 x 轴和 y 轴旋转回 $\bold{v}_1$ 和 $\bold{v}2$（通过 $\bold{R}$ 进行变换）。

> If you like to count dimensions: a symmetric 2 × 2 matrix has 3 degrees of freedom, and the eigenvalue decomposition rewrites them as a rotation angle and two scale factors. 
> 如果你喜欢计算维度：对称的 2 × 2 矩阵有 3 个自由度，特征值分解将它们重写为旋转角度和两个比例因子。

<img src=".\Images\Figure 6.13.png" alt="Figure 6.13" style="zoom:67%;" />
Figure 6.13. What happens when the unit circle is transformed by an arbitrary symmetric matrix $\bold{A}$, also known as a non–axis-aligned, nonuniform scale. The two perpendicular vectors $\bold{v}_1$ and $\bold{v}_2$, which are the eigenvectors of $\bold{A}$, remain fixed in direction but get scaled. In terms of elementary transformations, this can be seen as first rotating the eigenvectors to the canonical basis, doing an axis-aligned scale, and then rotating the canonical basis back to the eigenvectors. 
图 6.13。 当单位圆被任意对称矩阵 $\bold{A}$（也称为非轴对齐、非均匀尺度）变换时会发生什么。 两个垂直向量 $\bold{v}_1$ 和 $\bold{v}_2$ 是 $\bold{A}$ 的特征向量，其方向保持固定，但会进行缩放。 就初等变换而言，这可以看作是首先将特征向量旋转到规范基，进行轴对齐缩放，然后将规范基旋转回特征向量。

Looking at the effect of these three transforms together, we can see that they have the effect of a nonuniform scale along a pair of axes. As with an axis-aligned scale, the axes are perpendicular, but they aren’t the coordinate axes; instead they  are the eigenvectors of $\bold{A}$. This tells us something about what it means to be a symmetric matrix: symmetric matrices are just scaling operations—albeit potentially nonuniform and non–axis-aligned ones. 
一起查看这三个变换的效果，我们可以看到它们具有沿一对轴的非均匀缩放效果。 与轴对齐比例一样，轴是垂直的，但它们不是坐标轴； 相反，它们是 $\bold{A}$ 的特征向量。 这告诉我们对称矩阵的含义：对称矩阵只是缩放操作——尽管可能是不均匀和非轴对齐的。

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
然后，根据其特征值分解，上面的矩阵从三点钟（x 轴）开始沿逆时针方向 $31.7°$ 缩放。 这是下午 2 点之前的触摸。 如图 6.14 所示。
<img src=".\Images\Figure 6.14.png" alt="Figure 6.14" style="zoom:80%;" />
Figure 6.14. A symmetric matrix is always a scale along some axis. In this case it is along the $φ = 31.7◦$ direction which means the real eigenvector for this matrix is in that direction.  
图 6.14  对称矩阵始终是沿某个轴的尺度。 在这种情况下，它沿着 $φ = 31.7°$ 方向，这意味着该矩阵的真实特征向量在该方向上。

We can also reverse the diagonalization process; to scale by $(λ_1, λ_2)$ with the first scaling direction an angle $φ$ clockwise from the x-axis, we have
我们还可以反转对角化过程； 要按 $(λ_1, λ_2)$ 缩放，并且第一个缩放方向与 x 轴顺时针旋转 $φ$ 角度，我们有
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
我们应该放心，这是一个对称矩阵，因为我们知道它一定是真的，因为我们是通过对称特征值分解构造它的。

#### Singular Value Decomposition 奇异值分解

A very similar kind of decomposition can be done with nonsymmetric matrices as well: it’s the Singular Value Decomposition (SVD), also discussed in Section 5.4.1. The difference is that the matrices on either side of the diagonal matrix are no longer the same: 
非对称矩阵也可以进行一种非常相似的分解：它是奇异值分解（SVD），也在第 5.4.1 节中讨论。 不同之处在于对角矩阵两侧的矩阵不再相同：
$\bold{A} = \bold{U}\bold{S}\bold{V}^T  $

The two orthogonal matrices that replace the single rotation $\bold{R}$ are called $\bold{U}$ and $\bold{V}$, and their columns are called $\bold{u}_i$ (the left singular vectors) and $\bold{v}_i$ (the right singular vectors), respectively. In this context, the diagonal entries of $\bold{S}$ are called singular values rather than eigenvalues. The geometric interpretation is very similar to that of the symmetric eigenvalue decomposition (Figure 6.15): 
代替单个旋转$\bold{R}$的两个正交矩阵称为$\bold{U}$和$\bold{V}$，它们的列称为$\bold{u}_i$（左边 分别是奇异向量）和 $\bold{v}_i$ （右奇异向量）。 在这种情况下，$\bold{S}$ 的对角线条目称为奇异值而不是特征值。 几何解释与对称特征值分解非常相似（图 6.15）：

1. Rotate $\bold{v}_1$ and $\bold{v}_2$ to the x- and y-axes (the transform by $\bold{V}^T$).
   将 $\bold{v}_1$ 和 $\bold{v}_2$ 旋转到 x 轴和 y 轴（通过 $\bold{V}^T$ 进行变换）。
2. Scale in $x$ and $y$ by $(σ_1, σ_2)$ (the transform by $\bold{S}$).
   按 $(σ_1, σ_2)$ 缩放 $x$ 和 $y$（通过 $\bold{S}$ 进行变换）。
3. Rotate the x- and y-axes to $\bold{u}_1$ and $\bold{u}_2$ (the transform by $\bold{U}$). 
   将 x 轴和 y 轴旋转到 $\bold{u}_1$ 和 $\bold{u}_2$（通过 $\bold{U}$ 进行变换）。

> For dimension counters: a general 2 × 2 matrix has 4 degrees of freedom, and the SVD rewrites them as two rotation angles and two scale factors. One more bit is needed to keep track of reflections, but that doesn’t add a dimension. 
> 对于维度计数器：一般的 2 × 2 矩阵有 4 个自由度，SVD 将它们重写为两个旋转角度和两个比例因子。 还需要一位来跟踪反射，但这并不会增加维度。

![Figure 6.15](.\Images\Figure 6.15.png)
Figure 6.15. What happens when the unit circle is transformed by an arbitrary matrix $\bold{A}$. The two perpendicular vectors $\bold{v}_1$ and $\bold{v}_2$, which are the right singular vectors of $\bold{A}$, get scaled and changed in direction to match the left singular vectors, $\bold{u}_1$ and $\bold{u}_2$. In terms of elementary transformations, this can be seen as first rotating the right singular vectors to the canonical basis, doing an axis-aligned scale, and then rotating the canonical basis to the left singular vectors. 
图 6.15  当单位圆被任意矩阵 $\bold{A}$ 变换时会发生什么。 两个垂直向量 $\bold{v}_1$ 和 $\bold{v}_2$ 是 $\bold{A}$ 的右奇异向量，它们被缩放并改变方向以匹配左奇异向量， $\bold{u}_1$ 和 $\bold{u}_2$。 就初等变换而言，这可以看作是首先将右奇异向量旋转到规范基，进行轴对齐缩放，然后将规范基旋转到左奇异向量。

The principal difference is between a single rotation and two different orthogonal matrices. This difference causes another, less important, difference. Because the SVD has different singular vectors on the two sides, there is no need for negative singular values: we can always flip the sign of a singular value, reverse the direction of one of the associated singular vectors, and end up with the same transformation again. For this reason, the SVD always produces a diagonal matrix with all positive entries, but the matrices $\bold{U}$ and $\bold{V}$ are not guaranteed to be rotations—they could include reflection as well. In geometric applications like graphics this is an inconvenience, but a minor one: it is easy to differentiate rotations from reflections by checking the determinant, which is +1 for rotations and −1 for reflections, and if rotations are desired, one of the singular values can be negated, resulting in a rotation–scale–rotation sequence where the reflection is rolled in with the scale, rather than with one of the rotations.
主要区别在于单个旋转和两个不同的正交矩阵之间。 这种差异导致了另一个不太重要的差异。 由于 SVD 两侧具有不同的奇异向量，因此不需要负奇异值：我们始终可以翻转奇异值的符号，反转相关奇异向量之一的方向，并最终得到相同的变换 再次。 因此，SVD 总是生成一个所有正项的对角矩阵，但矩阵 $\bold{U}$ 和 $\bold{V}$ 不保证是旋转，它们也可能包含反射。 在图形等几何应用中，这是一个不便，但只是一个小问题：通过检查行列式很容易区分旋转和反射，行列式对于旋转为+1，对于反射为-1，如果需要旋转，则奇异值之一 值可以取反，从而产生旋转-缩放-旋转序列，其中反射随缩放滚动，而不是随旋转之一滚动。

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
图 6.12。 剪切矩阵的奇异值分解 (SVD)。 任何二维矩阵都可以分解为旋转、缩放、旋转的乘积。 请注意，时钟的圆形面必须变成椭圆形，因为它只是一个旋转和缩放的圆。

An immediate consequence of the existence of SVD is that all the 2D transformation matrices we have seen can be made from rotation matrices and scale matrices. Shear matrices are a convenience, but they are not required for expressing transformations. 
SVD 存在的直接后果是我们所看到的所有 2D 变换矩阵都可以由旋转矩阵和缩放矩阵组成。 剪切矩阵很方便，但它们不是表达变换所必需的。

In summary, every matrix can be decomposed via SVD into a rotation times a scale times another rotation. Only symmetric matrices can be decomposed via eigenvalue diagonalization into a rotation times a scale times the inverse-rotation, and such matrices are a simple scale in an arbitrary direction. The SVD of a symmetric matrix will yield the same triple product as eigenvalue decomposition via a slightly more complex algebraic manipulation. 
总之，每个矩阵都可以通过 SVD 分解为一个旋转乘以一个尺度乘以另一个旋转。 只有对称矩阵可以通过特征值对角化分解为旋转乘以尺度乘以逆旋转，并且这样的矩阵是任意方向上的简单尺度。 对称矩阵的 SVD 将通过稍微复杂的代数运算产生与特征值分解相同的三重积。

#### Paeth Decomposition of Rotations 旋转的 Paeth 分解

Another decomposition uses shears to represent nonzero rotations (Paeth, 1990). The following identity allows this: 
另一种分解使用剪切来表示非零旋转（Paeth，1990）。 以下身份允许这样做：
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
这种特殊的变换对于光栅旋转很有用，因为剪切对于图像来说是一种非常有效的光栅操作； 它会引入一些锯齿，但不会留下任何洞。 关键的观察是，如果我们采用栅格位置 $(i, j)$ 并对它应用水平剪切，我们会得到
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
> 要理解为什么负号位于 y 轴旋转的左下角，请考虑按循环顺序排列的三个轴：y 在 x 之后； z 在 y 之后； z 之后的 x。

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
与 2D 变换一样，任何 3D 变换矩阵都可以使用 SVD 分解为旋转、缩放和另一个旋转。 任何对称 3D 矩阵都可以将特征值分解为旋转、缩放和逆旋转。 最后，3D 旋转可以分解为 3D 剪切矩阵的乘积。

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
如果 $\bold{R}_{uvw}$ 是一个具有正交行的旋转矩阵，则 $R^T_{uvw}$也是一个具有正交列的旋转矩阵，并且实际上是 $\bold{R}_{uvw}$的逆（正交矩阵的逆始终是其转置）。一个重要的观点是，对于变换矩阵，代数逆矩阵也是几何逆矩阵。因此，如果 $\bold{R}_{uvw}$将 $\bold{u}$ 映射到 $\bold{x}$，则 $\bold{R}^T_{uvw}$将 $\bold{x}$ 映射到$\bold{u}$。我们可以确认，对于 $\bold{v}$ 和 $\bold{y}$，情况也应该是如此：
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

#### 6.2.2 Transforming Normal Vectors 变换法线向量

While most 3D vectors we use represent positions (offset vectors from the origin) or directions, such as where light comes from, some vectors represent surface normals. Surface normal vectors are perpendicular to the tangent plane of a surface. These normals do not transform the way we would like when the underlying surface is transformed. For example, if the points of a surface are transformed by a matrix $\bold{M}$, a vector $\bold{t}$ that is tangent to the surface and is multiplied by $\bold{M}$ will be tangent to the transformed surface. However, a surface normal vector $\bold{v}$ that is transformed by $\bold{M}$ may not be normal to the transformed surface (Figure 6.17). 
虽然我们使用的大多数 3D 矢量表示位置（距原点的偏移矢量）或方向，例如光线的来源，但某些矢量表示表面法线。 表面法向量垂直于表面的切平面。 当底层表面变换时，这些法线不会按照我们想要的方式变换。 例如，如果曲面上的点通过矩阵 $\bold{M}$ 进行变换，则与曲面相切并乘以 $\bold{M}$ 的向量 $\bold{t}$ 将与变换后的曲面相切。 然而，由 $\bold{M}$ 变换的表面法线向量 $\bold{v}$ 可能不垂直于变换后的表面（图 6.17）。
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
单个矩阵实现了一个线性变换，然后是一个平移!这种变换被称为仿射变换，这种通过增加一个额外维度来实现仿射变换的方式被称为齐次坐标(Roberts, 1965; Riesenfeld, 1981;Penna & Patterson, 1986)。齐次坐标不仅清理了转换的代码，而且该方案还使如何组合两个仿射转换变得很明显:只需将矩阵相乘。

A problem with this new formalism arises when we need to transform vectors that are not supposed to be positions—they represent directions, or offsets between positions. Vectors that represent directions or offsets should not change when we translate an object. Fortunately, we can arrange for this by setting the third coordinate to zero:
当我们需要变换不应该是位置的向量时，这种新形式主义就会出现问题——它们代表方向或位置之间的偏移。 当我们平移对象时，表示方向或偏移的向量不应改变。 幸运的是，我们可以通过将第三个坐标设置为零来做到这一点：
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
图6.19 点(2,1)有一个变换“translate by(-1,0)”应用于它。右上方是我们的心理图像，如果我们把这个变换看作是一个物理运动，右下方是我们的心理图像，如果我们把它看作是坐标的变化(在这种情况下是原点的运动)。人工边界只是一种技巧，在任何一种情况下，轴和点的相对位置都是相同的。

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



# 7  Viewing 视图

In the previous chapter, we saw how to use matrix transformations as a tool for arranging geometric objects in 2D or 3D space. A second important use of geometric transformations is in moving objects between their 3D locations and their positions in a 2D view of the 3D world. This 3D to 2D mapping is called a viewing transformation, and it plays an important role in object-order rendering, in which we need to rapidly find the image-space location of each object in the scene. 
在上一章中，我们了解了如何使用矩阵变换作为在 2D 或 3D 空间中排列几何对象的工具。 几何变换的第二个重要用途是在 3D 位置和 3D 世界的 2D 视图中的位置之间移动对象。 这种 3D 到 2D 的映射称为视图变换，它在对象顺序渲染中发挥着重要作用，其中我们需要快速找到场景中每个对象的图像空间位置。

When we studied ray tracing in Chapter 4, we covered the different types of perspective and orthographic views and how to generate viewing rays according to any given view. This chapter is about the inverse of that process. Here we explain how to use matrix transformations to express any parallel or perspective view. The transformations in this chapter project 3D points in the scene (world space) to 2D points in the image (image space), and they will project any point on a given pixel’s viewing ray back to that pixel’s position in image space. 
当我们在第 4 章中学习光线追踪时，我们介绍了不同类型的透视和正交视图以及如何根据任何给定视图生成观察光线。 本章讨论的是该过程的逆过程。 在这里，我们解释如何使用矩阵变换来表达任何平行视图或透视图。 本章中的变换将场景（世界空间）中的 3D 点投影到图像（图像空间）中的 2D 点，并且它们会将给定像素的视线上的任何点投影回该像素在图像空间中的位置。

If you have not looked at it recently, it is advisable to review the discussion of perspective and ray generation in Chapter 4 before reading this chapter. 
如果你最近没有看过它，建议在阅读本章之前回顾一下第 4 章中关于透视和光线生成的讨论。

By itself, the ability to project points from the world to the image is only good for producing wireframe renderings—renderings in which only the edges of objects are drawn, and closer surfaces do not occlude more distant surfaces (Figure 7.1). Just as a ray tracer needs to find the closest surface intersection along each viewing ray, an object-order renderer displaying solid-looking objects has to work out which of the (possibly many) surfaces drawn at any given point on the screen is closest and display only that one. In this chapter, we assume we are drawing a model consisting only of 3D line segments that are specified by the $(x, y, z)$ coordinates of their two endpoints. Later chapters will discuss the machinery needed to produce renderings of solid surfaces. 
就其本身而言，将点从世界投影到图像的能力仅适用于生成线框渲染，即仅绘制对象边缘的渲染，并且较近的表面不会遮挡较远的表面（图 7.1）。 正如光线追踪器需要沿着每条观察光线找到最近的表面交点一样，显示实体外观对象的对象顺序渲染器也必须计算出在屏幕上的任何给定点绘制的哪个（可能是多个）表面最接近，并且 只显示那个。 在本章中，我们假设我们正在绘制一个仅由 3D 线段组成的模型，这些线段由其两个端点的 $(x, y, z)$ 坐标指定。 后面的章节将讨论生成实体表面渲染所需的机械。
<img src=".\Images\Figure 7.1.png" alt="Figure 7.1" style="zoom:67%;" />
Figure 7.1. Left: wireframe cube in orthographic projection. Middle: wireframe cube in perspective projection. Right: perspective projection with hidden lines removed. 
图 7.1.  左：正交投影中的线框立方体。 中：透视投影中的线框立方体。 右：删除隐藏线的透视投影。



## 7.1 Viewing Transformations 视图变换

The viewing transformation has the job of mapping 3D locations, represented as $(x, y, z)$ coordinates in the canonical coordinate system, to coordinates in the image, expressed in units of pixels. It is a complicated beast that depends on  many different things, including the camera position and orientation, the type of projection, the field of view, and the resolution of the image. As with all complicated transformations it is best approached by breaking it up into a product of several simpler transformations. Most graphics systems do this by using a sequence of three transformations: 
视图变换的任务是将 3D 位置（在规范坐标系中表示为 $(x, y, z)$ 坐标）映射到图像中的坐标（以像素为单位表示）。 它是一个复杂的野兽，取决于许多不同的因素，包括相机的位置和方向、投影类型、视野和图像的分辨率。 与所有复杂的转换一样，最好的方法是将其分解为几个更简单的转换的产物。 大多数图形系统通过使用三个转换序列来实现此目的：

> Some APIs use “viewing transformation” for just the piece of our viewing transformation that we call the camera transformation. 
> 一些 API 将“视图变换”仅用于我们称为相机变换的视图变换部分。

- A camera transformation or eye transformation, which is a rigid body transformation that places the camera at the origin in a convenient orientation. It depends only on the position and orientation, or pose, of the camera.
  相机变换或眼睛变换，这是一种刚体变换，它将相机以方便的方向放置在原点。 它仅取决于相机的位置和方向或姿势。
- A projection transformation, which projects points from camera space so that all visible points fall in the range -1 to 1 in x and y. It depends only on the type of projection desired.
  投影变换，从相机空间投影点，以便所有可见点都落在 x 和 y 的 -1 到 1 范围内。 这仅取决于所需的投影类型。
- A viewport transformation or windowing transformation, which maps this unit image rectangle to the desired rectangle in pixel coordinates. It depends only on the size and position of the output image. 
  视口变换或窗口变换，将单位图像矩形映射到像素坐标中所需的矩形。 它仅取决于输出图像的大小和位置。

To make it easy to describe the stages of the process (Figure 7.2), we give names to the coordinate systems that are the inputs and output of these transformations.  The camera transformation converts points in canonical coordinates (or world space) to camera coordinates or places them in camera space. The projection transformation moves points from camera space to the canonical view volume.  Finally, the viewport transformation maps the canonical view volume to screen space. 
为了便于描述该过程的各个阶段（图 7.2），我们为作为这些变换的输入和输出的坐标系命名。 相机变换将规范坐标（或世界空间）中的点转换为相机坐标或将它们放置在相机空间中。 投影变换将点从相机空间移动到规范视图体积。 最后，视口变换将规范视图体积映射到屏幕空间。
<img src=".\Images\Figure 7.2.png" alt="Figure 7.2" style="zoom:67%;" />

Figure 7.2. The sequence of spaces and transformations that gets objects from their original coordinates into screen space. 
图 7.2. 将对象从原始坐标转换到屏幕空间的空间和变换序列。

> Other names: camera space is also “eye space” and the camera transformation is sometimes the “viewing transformation;” the canonical view volume is also “clip space” or “normalized device coordinates;” screen space is also “pixel coordinates.” 
> 其他名称：相机空间也是“眼睛空间”，相机变换有时是“观看变换”； 规范视图体积也是“剪辑空间”或“标准化设备坐标”； 屏幕空间也是“像素坐标”。

Each of these transformations is individually quite simple. We’ll discuss them in detail for the orthographic case beginning with the viewport transformation, then cover the changes required to support perspective projection.
这些转换中的每一个都非常简单。 我们将从视口转换开始详细讨论正交案例，然后介绍支持透视投影所需的更改。

### 7.1.1 The Viewport Transformation 视口变换

We begin with a problem whose solution will be reused for any viewing condition. We assume that the geometry we want to view is in the canonical view volume,  and we wish to view it with an orthographic camera looking in the $-z$ direction. The canonical view volume is the cube containing all 3D points whose Cartesian coordinates are between $-1$ and $+1$—that is, $(x, y, z) ∈ [-1, 1]^3$ (Figure 7.3) We project $x = -1$ to the left side of the screen, $x = +1$ to the right side of the screen, $y = -1$ to the bottom of the screen, and $y = +1$ to the top of the screen. 
我们从一个问题开始，其解决方案将在任何观看条件下重复使用。 我们假设我们想要查看的几何图形位于规范视图体积中，并且我们希望使用正交相机在 $-z$ 方向上查看它。 规范视图体积是包含笛卡尔坐标在 $-1$ 和 $+1$ 之间的所有 3D 点的立方体，即 $(x, y, z) ∈ [-1, 1]^3$（图 7.3 ）我们将 $x = -1$ 投影到屏幕左侧，$x = +1$ 投影到屏幕右侧，$y = -1$ 投影到屏幕底部，$y = +1 $ 到屏幕顶部。
![Figure 7.3](.\Images\Figure 7.3.png)
Figure 7.3. The canonical view volume is a cube with side of length two centered at the origin. 
图 7.3. 规范视图体积是一个边长为 2、以原点为中心的立方体。

> The word “canonical” crops up again—it means something arbitrarily chosen for convenience. For instance, the unit circle could be called the “canonical circle.”
> “规范”这个词再次出现——它的意思是为了方便而任意选择的东西。 例如，单位圆可以称为“规范圆”。

Recall the conventionsfor pixel coordinates from Chapter 3: each pixel “owns” a unit square centered at integer coordinates; the image boundaries have a half-unit overshoot from the pixel centers; and the smallest pixel center coordinates are $(0, 0)$. If we are drawing into an image (or window on the screen) that has $n_x$ by $n_y$ pixels, we need to map the square $[−1, 1]^2$ to the rectangle $[−0.5, n_x − 0.5] × [−0.5, n_y − 0.5]$.
回想一下第 3 章中像素坐标的约定：每个像素“拥有”一个以整数坐标为中心的单位正方形； 图像边界与像素中心有半个单位的超调； 最小像素中心坐标为$(0, 0)$。 如果我们要绘制具有 $n_x$ x $n_y$ 像素的图像（或屏幕上的窗口），我们需要将正方形 $[−1, 1]^2$ 映射到矩形 $[−0.5, n_x − 0.5] × [−0.5, n_y − 0.5]$。

> Mapping a square to a potentially non-square rectangle is not a problem; x and y just end up with different scale factors going from canonical to pixel coordinates.
> 将正方形映射到潜在的非正方形矩形不是问题； x 和 y 最终会得到从规范坐标到像素坐标的不同比例因子。

For now, we will assume that all line segments to be drawn are completely inside the canonical view volume. Later we will relax that assumption when we discuss clipping.
现在，我们假设所有要绘制的线段都完全位于规范视图体积内。 稍后，当我们讨论裁剪时，我们将放宽这一假设。

Since the viewport transformation maps one axis-aligned rectangle to another, it is a case of the windowing transform given by Equation (6.6):
由于视口变换将一个轴对齐的矩形映射到另一个轴对齐的矩形，因此它是等式（6.6）给出的窗口变换的一种情况：
$$
\begin{bmatrix}
x_{screen} \\
y_{screen} \\
1
\end{bmatrix} 
= \begin{bmatrix}
\frac{n_x}{2} & 0 & \frac{n_x - 1}{2} \\
0 & \frac{n_y}{2} & \frac{n_y - 1}{2} \\
0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
x_{canonical} \\
y_{canonical} \\
1
\end{bmatrix} \ \ \ \ \ (7.1)
$$
Note that this matrix ignores the z-coordinate of the points in the canonical view volume, because a point’s distance along the projection direction doesn’t affect where that point projects in the image. But before we officially call this the viewport matrix, we add a row and column to carry along the z-coordinate without changing it. We don’t need it in this chapter, but eventually we will need the z values because they can be used to make closer surfaces hide more distant surfaces (see Section 8.2.3).
请注意，该矩阵忽略了规范视图体积中点的 z 坐标，因为点沿投影方向的距离不会影响该点在图像中的投影位置。 但在我们正式将其称为视口矩阵之前，我们添加一行和一列来携带 z 坐标而不更改它。 在本章中我们不需要它，但最终我们将需要 z 值，因为它们可以用来使更近的曲面隐藏更远的曲面（参见第 8.2.3 节）。
$$
M_{vp} = \begin{bmatrix}
\frac{n_x}{2} & 0 & 0 & \frac{n_x - 1}{2} \\
0 & \frac{n_y}{2} & 0 & \frac{n_y - 1}{2} \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ \ \ (7.2)
$$

### 7.1.2 The Orthographic Projection Transformation正交投影变换

Of course, we usually want to render geometry in some region of space other than the canonical view volume. Our first step in generalizing the view will keep the view direction and orientation fixed looking along -z with +y up, but will allow arbitrary rectangles to be viewed. Rather than replacing the viewport matrix, we’ll augment it by multiplying it with another matrix on the right. 
当然，我们通常希望在规范视图体积之外的某些空间区域中渲染几何图形。 我们概括视图的第一步将保持视图方向和方向固定，沿着 -z 和 +y 向上看，但允许查看任意矩形。 我们不是替换视口矩阵，而是通过将其与右侧的另一个矩阵相乘来增强它。

Under these constraints, the view volume is an axis-aligned box, and we’ll name the coordinates of its sides so that the view volume is $[l, r] × [b, t] × [f, n]$ shown in Figure 7.4. We call this box the orthographic view volume and refer to the bounding planes as follows:
在这些约束下，视图体积是一个轴对齐的盒子，我们将命名其边的坐标，以便视图体积为 $[l, r] × [b, t] × [f, n]$ 所示 如图 7.4 所示。 我们将此框称为正交视图体积，并按如下方式引用边界平面： 
![Figure 7.4](.\Images\Figure 7.4.png)
Figure 7.4. The orthographic view volume.
图 7.4. 正交视图体积。
$$
x = l ≡ left\ plane, \\
x = r ≡ right\ plane, \\
y = b ≡ bottom\ plane, \\
y = t ≡ top\ plane, \\
z = n ≡ near\ plane, \\
z = f ≡ far\ plane. \\
$$
That vocabulary assumes a viewer who is looking along the minus z-axis with  his head pointing in the y-direction(Most programmers find it intuitive to have the x-axis pointing right and the y-axis pointing up. In
a right-handed coordinate system, this implies that we are looking in the -z direction. Some systems use a left-handed coordinate system for viewing so that the gaze direction is along +z. Which is best is a matter of taste, and this text assumes a right-handed coordinate system. A reference that argues for the left-handed system instead is given in the notes at the end of the chapter.  ). This implies that $n > f$, which may be unintuitive, but if you assume the entire orthographic view volume has negative $z$ values then the $z = n$ “near” plane is closer to the viewer if and only if $n > f$; here $f$ is a smaller number than $n$, i.e., a negative number of larger absolute value than $n$. 
该词汇假设观看者沿着负 z 轴观看，头指向 y 方向（大多数程序员认为 x 轴指向右侧，y 轴指向上方是直观的。右手坐标系，这意味着我们正在朝 -z 方向看。 一些系统使用左手坐标系进行观察，以便注视方向沿着+z。 哪个最好取决于个人喜好，本文假设使用右手坐标系。 本章末尾的注释中给出了支持左手系统的参考文献。 ）。 这意味着 $n > f$，这可能不直观，但如果假设整个正交视图体积具有负 $z$ 值，则 $z = n$ “近”平面更接近观察者当且仅当 $ n > f$; 这里$f$是比$n$小的数，即绝对值比$n$大的负数。

This concept is shown in Figure 7.5. The transform from orthographic view volume to the canonical view volume is another windowing transform, so we can simply substitute the bounds of the orthographic and canonical view volumes into Equation (6.7) to obtain the matrix for this transformation:
这个概念如图 7.5 所示。 从正交视图体积到规范视图体积的变换是另一种加窗变换，因此我们可以简单地将正交视图体积和规范视图体积的边界代入方程（6.7）以获得该变换的矩阵：
$$
\bold{M}_{orth} = \begin{bmatrix}
\frac{2}{r - l} & 0 & 0 & -\frac{r + l}{r - l} \\
0 & \frac{2}{t - b} & 0 & -\frac{t+b}{t-b} \\
0 & 0 & \frac{2}{n-f} & -\frac{n+f}{n-f} \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ (7.3)
$$

> This matrix is very close to the one used traditionally in OpenGL, except that $n$, $f$, and $z_{canonical}$ all have the opposite sign.
> 该矩阵与 OpenGL 中传统使用的矩阵非常接近，只是 $n$、$f$ 和 $z_{canonical}$ 都具有相反的符号。

![Figure 7.5](.\Images\Figure 7.5.png)
Figure 7.5. The orthographic view volume is along the negative z-axis, so $f$ is a more negative number than $n$, thus $n > f$. 
图 7.5. 正交视图体积沿着负 z 轴，因此 $f$ 是比 $n$ 更负的数，因此 $n > f$。

To draw 3D line segments in the orthographic view volume, we project them into screen x- and y-coordinates and ignore z-coordinates. We do this by combining Equations (7.2) and (7.3). Note that in a program we multiply the matrices together to form one matrix and then manipulate points as follows:
为了在正交视图体积中绘制 3D 线段，我们将它们投影到屏幕 x 和 y 坐标并忽略 z 坐标。 我们通过结合方程（7.2）和（7.3）来做到这一点。 请注意，在程序中，我们将矩阵相乘以形成一个矩阵，然后按如下方式操作点：
$$
\begin{bmatrix}
x_{pixel} \\
y_{pixel} \\
z_{canonical} \\
1
\end{bmatrix}
=(\bold{M}_{vp}\bold{M}_{orth})\begin{bmatrix}
x \\
y \\
z \\
1
\end{bmatrix}
$$
The z-coordinate will now be in [-1, 1]. We don’t take advantage of this now, but it will be useful when we examine z-buffer algorithms. 
z 坐标现在位于 [-1, 1] 中。 我们现在不利用这一点，但当我们检查 z 缓冲区算法时它会很有用。

The code to draw many 3D lines with endpoints $\bold{a}_i$ and $\bold{b}_i$ thus becomes both simple and efficient: 
因此，绘制许多带有端点 $\bold{a}_i$ 和 $\bold{b}_i$ 的 3D 线的代码变得既简单又高效：
<img src=".\Images\Figure 7.5_1.png" alt="Figure 7.5_1" style="zoom:67%;" />

> This is a first example of how matrix transformation machinery makes graphics programs clean and efficient.
> 这是矩阵变换机制如何使图形程序变得干净和高效的第一个例子。

### 7.1.3 The Camera Transformation  相机转换

We’d like to be able to change the viewpoint in 3D and look in any direction. There are a multitude of conventions for specifying viewer position and orientation. We will use the following one (see Figure 7.6):
我们希望能够改变 3D 视角并朝任意方向观看。 有多种用于指定观看者位置和方向的约定。 我们将使用以下一个（见图 7.6）：
<img src=".\Images\Figure 7.6.png" alt="Figure 7.6" style="zoom:80%;" />
Figure 7.6. The user specifies viewing as an eye position $\bold{e}$, a gaze direction $\bold{g}$, and an up vector $\bold{t}$. We construct a right-handed basis with $\bold{w}$ pointing opposite to the gaze and $\bold{v}$ being in the same plane as $\bold{g}$ and $\bold{t}$.
图 7.6. 用户将观看指定为眼睛位置 $\bold{e}$、注视方向 $\bold{g}$ 和向上向量 $\bold{t}$。 我们构造一个右手基础，其中 $\bold{w}$ 指向凝视方向，并且 $\bold{v}$ 与 $\bold{g}$ 和 $\bold{t}$ 在同一平面上。

- the eye position $\bold{e}$,
  眼睛位置$\bold{e}$,
- the gaze direction $\bold{g}$,
  凝视方向$\bold{g}$,
- the view-up vector $\bold{t}$. 
  视图向上向量$\bold{t}$。

The eye position is a location that the eye “sees from.” If you think of graphics as a photographic process, it is the center of the lens. The gaze direction is any vector in the direction that the viewer is looking. The view-up vector is any vector in the plane that both bisects the viewer’s head into right and left halves and points “to the sky” for a person standing on the ground. These vectors provide us with enough information to set up a coordinate system with origin $\bold{e}$ and a $\bold{uvw}$ basis, using the construction of Section 2.4.7:
眼睛位置是眼睛“观看”的位置。 如果您将图形视为摄影过程，那么它就是镜头的中心。 注视方向是观察者注视方向上的任意向量。 视图向上向量是平面中的任何向量，它将观看者的头部平分为左右两半，并且对于站在地面上的人来说指向“天空”。 这些向量为我们提供了足够的信息来建立一个以原点 $\bold{e}$ 和 $\bold{uvw}$ 为基础的坐标系，使用第 2.4.7 节的构造：
$$
\bold{w} = -\frac{\bold{g}}{\|\bold{g}\|}, \\
\bold{u} = \frac{\bold{t}\cross \bold{w}}{\|\bold{t}\cross \bold{w}\|} \\
\bold{v} = \bold{w} \cross \bold{u}
$$
Our job would be done if all points we wished to transform were stored in coordinates with origin $\bold{e}$ and basis vectors $\bold{u}$, $\bold{v}$, and $\bold{w}$. But as shown in Figure 7.7, the coordinates of the model are stored in terms of the canonical (or world) origin o and the x-, y-, and z-axes. To use the machinery we have already developed, we just need to convert the coordinates of the line segment endpoints we wish to draw from xyz-coordinates into uvw-coordinates. This kind of transformation was discussed in Section 6.5, and the matrix that enacts this transformation is the canonical-to-basis matrix of the camera’s coordinate frame:
如果我们希望变换的所有点都存储在具有原点 $\bold{e}$ 和基向量 $\bold{u}$、$\bold{v}$ 和 $\bold{w}$ 的坐标中，我们的工作就完成了。 但如图 7.7 所示，模型的坐标是根据规范（或世界）原点 o 以及 x、y 和 z 轴存储的。 要使用我们已经开发的机制，我们只需要将要绘制的线段端点的坐标从 xyz 坐标转换为 uvw 坐标。 这种变换在 6.5 节中讨论过，执行这种变换的矩阵是相机坐标系的规范基矩阵：
$$
\bold{M}_{cam} = \begin{bmatrix}
\bold{u} & \bold{v} & \bold{w} & \bold{e} \\
0 & 0 & 0 & 1
\end{bmatrix}^{-1}
= \begin{bmatrix}
x_u & y_u & z_u & 0 \\
x_v & y_v & z_v & 0 \\
x_w & y_w & z_w & 0 \\
0 & 0 & 0 & 1
\end{bmatrix}
\begin{bmatrix}
1 & 0 & 0 & −x_e \\
0 & 1 & 0 & −y_e \\
0 & 0 & 1 & −z_e \\
0 & 0 & 0 & 1
\end{bmatrix} \ \ \ \ \ (7.4)
$$
<img src=".\Images\Figure 7.7.png" alt="Figure 7.7" style="zoom:67%;" />
Figure 7.7. For arbitrary viewing, we need to change the points to be stored in the “appropriate” coordinate system. In this case it has origin e and offset coordinates in terms of $\bold{u}\bold{v}\bold{w}$.
图 7.7. 为了任意查看，我们需要更改要存储在“适当”坐标系中的点。 在这种情况下，它具有原点 e 和以 $\bold{u}\bold{v}\bold{w}$ 表示的偏移坐标。

Alternatively, we can think of this same transformation as first moving $\bold{e}$ to the origin, then aligning $\bold{u}$, $\bold{v}$, $\bold{w}$ to $\bold{x}$, $\bold{y}$, $\bold{z}$.
或者，我们可以将相同的转换视为首先将 $\bold{e}$ 移动到原点，然后将 $\bold{u}$、$\bold{v}$、$\bold{w}$ 与 $  \bold{x}$、$\bold{y}$、$\bold{z}$对齐。

To make our previously z-axis-only viewing algorithm work for cameras with any location and orientation, we just need to add this camera transformation to  the product of the viewport and projection transformations, so that it converts the incoming points from world to camera coordinates before they are projected:
为1了使我们之前的仅 z 轴查看算法适用于任何位置和方向的相机，我们只需将此相机变换添加到视口和投影变换的乘积中，以便它将输入点从世界坐标转换为相机坐标 在预测之前：
<img src=".\Images\Figure 7.6_1.png" alt="Figure 7.6_1" style="zoom:67%;" />

Again, almost no code is needed once the matrix infrastructure is in place. 
同样，一旦矩阵基础设施就位，几乎不需要任何代码。

## 7.2 Projective Transformations 投影变换

We have left perspective for last because it takes a little bit of cleverness to make it fit into the system of vectors and matrix transformations that has served us so well up to now. To see what we need to do, let’s look at what the perspective projection transformation needs to do with points in camera space. Recall that the  viewpoint is positioned at the origin and the camera is looking along the z-axis.
我们把透视图留到最后，因为它需要一点点聪明才智才能使其适应迄今为止为我们提供良好服务的向量和矩阵变换系统。 为了了解我们需要做什么，让我们看看透视投影变换需要对相机空间中的点做什么。 回想一下，视点位于原点，相机沿着 z 轴观察。

> For the moment we will ignore the sign of z to keep the equations simpler, but it will return on page 150. 
> 目前我们将忽略 z 的符号以使方程更简单，但它将在第 150 页返回。

The key property of perspective is that the size of an object on the screen is proportional to $1/z$ for an eye at the origin looking up the negative z-axis. This can be expressed more precisely in an equation for the geometry in Figure 7.8: 
透视的关键属性是，对于在原点处向上看负 z 轴的眼睛，屏幕上对象的大小与 $1/z$ 成正比。 这可以用图 7.8 中的几何方程更精确地表达：
$$
y_s = \frac{d}{z}y,\ \ \ \ (7.5)
$$
<img src=".\Images\Figure 7.8.png" alt="Figure 7.8" style="zoom:67%;" />
Figure 7.8. The geometry for Equation (7.5). The viewer’s eye is at $\bold{e}$ and the gaze direction is $\bold{g}$ (the minus z-axis). The view plane is a distance $d$ from the eye. A point is projected toward $\bold{e}$ and where it intersects the view plane is where it is drawn. 
图 7.8. 方程（7.5）的几何形状。 观看者的眼睛位于$\bold{e}$，注视方向为$\bold{g}$（负z轴）。 视平面距眼睛的距离为$d$。 一个点向 $\bold{e}$ 投影，它与视图平面相交的地方就是它被绘制的地方。

where $y$ is the distance of the point along the $y$-axis, and $y_s$ is where the point should be drawn on the screen. 
其中 $y$ 是点沿 $y$ 轴的距离，$y_s$ 是应在屏幕上绘制点的位置。

We would really like to use the matrix machinery we developed for orthographic projection to draw perspective images; we could then just multiply another matrix into our composite matrix and use the algorithm we already have. However, this type of transformation, in which one of the coordinates of the input vector appears in the denominator, can’t be achieved using affine transformations. 
我们真的很想使用我们为正交投影开发的矩阵机制来绘制透视图像； 然后我们可以将另一个矩阵乘以我们的复合矩阵并使用我们已有的算法。 然而，这种类型的变换（其中输入向量的坐标之一出现在分母中）无法使用仿射变换来实现。

We can allow for division with a simple generalization of the mechanism of homogeneous coordinates that we have been using for affine transformations. We have agreed to represent the point $(x, y, z)$ using the homogeneous vector $[x\ y\ z\ 1]^T$; the extra coordinate, $w$, is always equal to 1, and this is ensured by always using $[0\ 0\ 0\ 1]^T$ as the fourth row of an affine transformation matrix. 
我们可以通过对我们一直用于仿射变换的齐次坐标机制的简单概括来允许除法。 我们同意使用齐次向量 $[x\ y\ z\ 1]^T$ 来表示点 $(x, y, z)$； 额外的坐标 $w$ 始终等于 1，这是通过始终使用 $[0\ 0\ 0\ 1]^T$ 作为仿射变换矩阵的第四行来确保的。

Rather than just thinking of the 1 as an extra piece bolted on to coerce matrix multiplication to implement translation, we now define it to be the denominator of the $x-$, $y-$, and $z-$coordinates: the homogeneous vector $[x\ y\ z\ w]^T$ represents the point $(x/w, y/w, z/w)$. This makes no difference when $w = 1$, but it allows a broader range of transformations to be implemented if we allow any values in the bottom row of a transformation matrix, causing $w$ to take on values other than 1. 
我们现在将其定义为 $x-$、$y-$ 和 $z-$ 坐标的分母，而不是仅仅将 1 视为附加在强制矩阵乘法上以实现平移的额外部分：齐次 向量$[x\ y\ z\ w]^T$表示点$(x/w, y/w, z/w)$。 当 $w = 1$ 时，这没有什么区别，但如果我们允许变换矩阵底行中的任何值，导致 $w$ 取 1 以外的值，则可以实现更广泛的变换。

Concretely, linear transformations allow us to compute expressions like
具体来说，线性变换允许我们计算如下表达式
$x' = ax + by + cz  $

and affine transformations extend this to
仿射变换将其扩展到
$x' = ax + by + cz + d  $

Treating $w$ as the denominator further expands the possibilities, allowing us to compute functions like
将 $w$ 视为分母进一步扩展了可能性，使我们能够计算如下函数
$x' = \frac{ax + by + cz + d  }{ex + fy + gz + h  } \\$ 

this could be called a “linear rational function” of x, y, and z. But there is an extra constraint—the denominators are the same for all coordinates of the transformed point: 
这可以称为 x、y 和 z 的“线性有理函数”。 但有一个额外的约束 - 变换点的所有坐标的分母都相同：
$$
x' = \frac{a_1x + b_1y + c_1z + d_1}{ex + fy + gz + h} \\
y' = \frac{a_2x + b_2y + c_2z + d_2}{ex + fy + gz + h} \\
z' = \frac{a_3x + b_3y + c_3z + d_3}{ex + fy + gz + h} \\
$$
Expressed as a matrix transformation, 
表示为矩阵变换，
$$
\ \begin{bmatrix}
\tilde{x} \\
\tilde{y} \\
\tilde{z} \\
\tilde{w}
\end{bmatrix} = 
\begin{bmatrix}
a_1 & b_1 & c_1 & d_1 \\
a_2 & b_2 & c_2 & d_2 \\
a_3 & b_3 & c_3 & d_3 \\
e & f & g & h
\end{bmatrix}
\begin{bmatrix}
x \\
y\\
z \\
1
\end{bmatrix} \\
(x', y', z') = (\tilde{x}/\tilde{w}, \tilde{y}/ \tilde{w}, \tilde{z}/ \tilde{w})
$$
A transformation like this is known as a projective transformation or a homography. 
像这样的变换称为投影变换或单应性。

Example. The matrix
例子。 矩阵
$$
\bold{M} = \begin{bmatrix}
 2 & 0 & -1 \\
 0 & 3 & 0  \\
 0 & \frac{2}{3} & \frac{1}{3}
\end{bmatrix}
$$
represents a 2D projective transformation that transforms the unit square $([0, 1] × [0, 1])$ to the quadrilateral shown in Figure 7.9. 
表示一个 2D 投影变换，将单位正方形 $([0, 1] × [0, 1])$ 变换为图 7.9 所示的四边形。

![Figure 7.9](.\Images\Figure 7.9.png)
Figure 7.9. A projective transformation maps a square to a quadrilateral, preserving straight lines but not parallel lines. 
图 7.9. 射影变换将正方形映射为四边形，保留直线但不保留平行线。

For instance, the lower-right corner of the square at (1, 0) is represented by the homogeneous vector $[1\ 0\ 1]^T$ and transforms as follows: 
例如，(1, 0) 处的正方形右下角由齐次向量 $[1\ 0\ 1]^T$ 表示，并变换如下：
