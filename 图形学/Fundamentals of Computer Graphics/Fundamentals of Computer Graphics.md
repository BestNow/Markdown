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
-  **rgb.** An RGB color that stores three components. You should also include operations for RGB addition, RGB subtraction, RGB multiplication, scalar multiplication,and scalar division.
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

