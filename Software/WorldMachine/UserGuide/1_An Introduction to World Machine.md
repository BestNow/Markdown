# An Introduction to World Machine

Unlike many other terrain editors that function like paint programs, World Machine operates on a procedural level. A World Machine world file doesn’t define a terrain, but the **steps** to create a terrain. This is the source of both its power and its complexity.

与许多其他像绘图程序一样的地形编辑器不同，World Machine在程序层面上运行。World Machine世界文件并不定义地形，而是定义创建地形的步骤。这是它的能力和复杂性的来源。

When working with World Machine, your mission is to determine the overall appearance and characteristics of the terrain, and then allow our algorithms to create and detail the appearance of your world. This way of working and thinking at a higher level compared to sculpting takes some getting used to, but the rewards are huge: You can create impressive terrains with relatively little work, and once you have created a terrain that you like, you can use the same world file with different random “seeds” to produce a different terrain entirely that retains the same feel.

当使用World Machine时，你的任务是确定地形的整体外观和特征，然后允许我们的算法创建和详细描述你的世界外观。与雕刻相比，这种更高层次的工作和思考方式需要一些时间来适应，但回报是巨大的:你可以用相对较少的工作创造出令人印象深刻的地形，一旦你创造了一个你喜欢的地形，你可以使用带有不同随机“种子”的相同世界文件来产生完全保留相同感觉的不同地形。

![img](.\Image\image-52.png)

<div align='center'><i>Terrain defined by erosion and random fractal noise <br>地形由侵蚀和随机分形噪声定义</i></div>

The tradeoff in computer graphics for this is usually a lack of control over feature placement. However, the Shapes device and other tools let you to work in a more artistic fashion, plotting out the terrain as roughly or precisely as you like. The ability to determine for yourself the level of control you exert is one of the best super-powers that World Machine makes available to you as an artist.

在计算机图形学中，这种权衡通常是缺乏对特征放置的控制。但是，形状设备和其他工具可以让您以更艺术的方式工作，根据您的喜好粗略或精确地绘制地形。自己决定控制水平的能力是《World Machine》提供给艺术家的最好的超能力之一。

## Concepts you should know 你应该知道的概念

World Machine operates on **worlds**. A world is simply the collection of steps used to create the terrain, as well as information about areas to view, detail level, and so on. These steps are referred to as **devices**, and each device will perform some operation on the world. The devices are represented graphically in something like a flowchart. The **workview** is where you can see and change the devices (steps taken). World Machine continuously previews each device in your world. To create the final product, you must **build** the world, which creates a high resolution output that you can then save to disk.

世界机器在**世界**上运行。世界只是用于创建地形的步骤的集合，以及关于要查看的区域、细节级别等的信息。这些步骤被称为**设备**，每个设备将对世界执行一些操作。这些设备用流程图之类的图形表示。**工作视图**是您可以查看和更改设备(采取的步骤)的地方。世界机器不断预览每个设备在你的世界。要创建最终产品，您必须**构建**世界，这将创建一个高分辨率的输出，然后您可以将其保存到磁盘。

In the next chapter, you’ll learn how to use the device workview and interact with devices to create your world.

在下一章中，您将学习如何使用设备工作视图和与设备交互来创建您的世界。

## The Starting World 开始的世界

When you first start World Machine, you’ll see a screen like the below:

当你第一次启动World Machine时，你会看到如下画面:

![img](.\Image\image-49.png)

Each aspect of the screen above will be visited in great detail in later chapters. The most important point is to understand how each of the basic concepts relates to what you can see:

上面屏幕的每个方面将在后面的章节中详细介绍。最重要的一点是理解每个基本概念是如何与你所看到的联系起来的:

● The *world* is the contents of the device workview (the screen visible above) 

*world*是设备工作视图的内容(上面可见的屏幕)

● The *devices* are the small colored blocks; there are four of them in the photo above. The devices reside within larger labelled areas called *groups*, which help you organize your world.

“设备”是小的彩色块;在上面的照片中有四个。这些设备驻留在更大的被称为“组”的标记区域中，帮助你组织你的世界。

● The lines connecting the blocks are *wires*, showing the order that actions are taken in and defining the flow of data.

连接这些块的线是“线”，显示了执行操作的顺序并定义了数据流。

● World Machine is displaying a preview of the currently selected device in the upper-left corner

“世界机器”将在左上角显示当前选定设备的预览

● To *build* the world, you must choose the Build option from the menu or toolbar, which will bring up a progress report dialog while calculations are being performed. Once the world is built, you can then export the terrain as mentioned in Chapter 6.

要*构建*世界，您必须从菜单或工具栏中选择build选项，这将在执行计算时弹出进度报告对话框。一旦世界建成，你就可以像第6章提到的那样导出地形。

You can select any device and see what the terrain looks like at that point by clicking on it. If you like learning by exploration, there is a large collection of various example files sorted by difficulty in concepts in the “/Examples” folder under your World Machine installation. Otherwise, continue reading below about how to use the Device Workview and what it all means.

你可以选择任何设备，并通过点击它来查看地形的样子。如果你喜欢通过探索来学习，在你的World Machine安装下的“/Examples”文件夹中有大量按概念难度排序的示例文件。否则，请继续阅读下面的内容，了解如何使用设备工作视图及其含义。