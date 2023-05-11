# Terrain Views

地形视图

World Machine has a variety of views which provide a view of the current terrain. Some display the current render extents, while others view the entire infinite procedural world in which the render extents are defined.

World Machine 有多种视图，可以提供当前地形的视图。 一些显示当前渲染范围，而另一些则查看定义渲染范围的整个无限程序世界。

## *Leftside View* *左视图*

The “Leftside View”, as it is called, is the toolbar running vertically along the left side of the screen. The leftview can be shown and hidden by pressing the **F4** key. For clarity, we will examine each section of the toolbar by itself.

所谓的“Leftside View”是沿着屏幕左侧垂直运行的工具栏。 按**F4** 键可以显示和隐藏左视图。 为了清楚起见，我们将单独检查工具栏的每个部分。

**Terrain Preview Window ** **地形预览窗口**

This window allows you to view a small, preview version of the current terrain area before it is built. This window is updated in real-time as you adjust device settings, allowing you to quickly see the effect your modifications have on the terrain.

此窗口允许您在构建之前查看当前地形区域的小型预览版本。 当您调整设备设置时，此窗口会实时更新，使您可以快速查看您的修改对地形的影响。

![img](.\Image\Terrain-Preview-Window.png)

Above the preview window, the name of the current render extent is displayed. Clicking the scroll arrows next to the name allows you to cycle through all of the currently defined render extents.

在预览窗口上方，显示当前渲染范围的名称。 单击名称旁边的滚动箭头可以循环浏览所有当前定义的渲染范围。

The preview window can be set to either 2D or 3D mode. Depending on the mode, you may be able to perform different actions, shown below. To toggle the preview mode, click the “**2D/3D**” button below the preview window.

预览窗口可以设置为 2D 或 3D 模式。 根据模式，您可以执行不同的操作，如下所示。 要切换预览模式，请单击预览窗口下方的“**2D/3D**”按钮。

The exact operation performed when you click and drag in the preview window depends upon your view navigation options. Click dragging will perform the following actions:

在预览窗口中单击并拖动时执行的确切操作取决于您的视图导航选项。 单击拖动将执行以下操作：

**2D Mode**: You may change the direction of the current terrain lighting in the preview area. **3D Mode**: You may rotate and zoom the view to find a new viewing angle of the terrain. In addition, you may change the direction of the current lighting of the terrain.

**2D 模式**：您可以在预览区域更改当前地形照明的方向。 **3D 模式**：您可以旋转和缩放视图以找到地形的新视角。 此外，您可以更改地形当前照明的方向。

**View Option Buttons: ** **查看选项按钮：**

![img](.\Image\View-Option-Buttons.png)

The three buttons right below the preview window allow you to change how terrains are shaded in World Machine:

预览窗口正下方的三个按钮允许您更改地形在 World Machine 中的着色方式：

• **Height**: Do not shade maps; Assign color by height only.

**高度**：不给贴图加阴影； 仅按高度分配颜色。

• **Shade**: Shade by terrain features (diffuse lighting)

**阴影**：地形特征的阴影（漫射照明）

• **H+S**: Assign color by height and also shade the terrain features

**H+S**：按高度分配颜色并对地形特征进行阴影处理

• **Set Terrain Color**: Choose a color scheme for the terrain. This is a cosmetic choice only and will not affect the terrain in any way.

**设置地形颜色**：为地形选择配色方案。 这只是一个装饰性的选择，不会以任何方式影响地形。

• **2D/3D**: This button toggles the preview window between 2D and 3D display modes.

**2D/3D**：此按钮可在 2D 和 3D 显示模式之间切换预览窗口。

• **Reset Preview**: Resets the lighting and camera angle of the preview window to default. Useful if you ever “get lost”.

**重置预览**：将预览窗口的照明和摄像机角度重置为默认值。 如果你曾经“迷路”，这很有用。

• **Fit**: Automatically sets the zoom level of the preview to fit the terrain into the view.

**适合**：自动设置预览的缩放级别以适合地形到视图中。

• **Toggle Main View**: This button will toggle the display in the main window between the Device Workview and the last active Viewing mode. *Right-clicking on any empty region in one of the other views will also accomplish this.*

**切换主视图**：此按钮将在设备工作视图和最后活动的查看模式之间切换主窗口中的显示。 *右键单击其他视图之一中的任何空白区域也可以完成此操作。*

**Water Level** This section controls the optional water plane that WM can display to help you visualize a global water level that your application might use.

**水位** 此部分控制 WM 可以显示的可选水位线，以帮助您可视化您的应用程序可能使用的全局水位线。

![img](.\Image\Water-Level.png)

You can show or hide the waterlevel display by clicking the appropriate button. Either entering a value directly or moving the slider will allow you to change the waterlevel.

您可以通过单击相应的按钮来显示或隐藏水位显示。 直接输入值或移动滑块都可以更改水位。

**Device Navigation Area**  **设备导航区**

![img](.\Image\Device-Navigation.png)

The device navigation list shows every device that exists in the current world. Devices are listed by either the creation order of devices or by groups. You can change the currently selected device by clicking on a new one; double-clicking will change that device’s properties.

设备导航列表显示了当前世界中存在的每一个设备。 设备按设备的创建顺序或按组列出。 您可以通过单击新设备来更改当前选择的设备； 双击将更改该设备的属性。

• **Lock Preview on Device (*****f hotkey\*****)**: This very useful function allows you to ‘freeze’ the preview window onto a device other than the currently selected one. For example, you may wish to freeze the preview onto a terrain filter device, and then go back up the chain and modify the settings of the generator device and see the *filtered* changes in real-time. Toggling the lock button again will disable the preview freeze.

**在设备上锁定预览**（f 热键）：这个非常有用的功能允许您将预览窗口“冻结”到当前所选设备以外的设备上。 例如，您可能希望将预览冻结到地形过滤器设备上，然后返回链并修改生成器设备的设置，并实时查看过滤的变化。 再次切换锁定按钮将禁用预览冻结。

• **Move Backward**: Changes the selected device to the prior device in the chain from the currently selected device.

**向后移动**：将所选设备从当前所选设备更改为链中的前一个设备。

• **Move Forward**: Selects the next device in the chain from the current one.

**向前移动**：从当前设备链中选择下一个设备。

• **Move to End**: Selects the LAST device in the chain from the current one.

**Move to End**：从当前设备链中选择最后一个设备。

• **Sort-By**: Allows you to sort the device listing by either creation order, or grouping.

**排序方式**：允许您按创建顺序或分组对设备列表进行排序。

• **Edit…**: Brings up the properties dialog for the currently selected device.

**编辑…**：打开当前所选设备的属性对话框。

## *3D View* *3D 视图*

The 3D View can be selected from the Command Bar, or by pressing F8

可以从命令栏或按 F8 键选择 3D 视图

![img](.\Image\3D-view.png)

The 3D View will always show the current contents of the active terrain. If the currently selected device has not been built yet (displays a yellow rather than green light in the Workview), the 3D View will show the lower-resolution preview results rather than the full-detail build results.

3D 视图将始终显示活动地形的当前内容。 如果当前选择的设备尚未构建（在工作视图中显示黄色而不是绿色），3D 视图将显示较低分辨率的预览结果而不是完整的细节构建结果。

The 3D View also has its own toolbar:

3D 视图也有自己的工具栏：

![img](.\Image\3d-View-toolbar.png)

• **Orbit**: This button puts the 3D View into Orbit mode. In this mode, moving the mouse will orbit the view around the terrain. This mode makes it easy to inspect the terrain from a variety of angles.

**Orbit**：此按钮将3D 视图置于Orbit 模式。 在此模式下，移动鼠标将使视图围绕地形旋转。 这种模式可以很容易地从各种角度检查地形。

• **Free Look**: The Free Look mode is similar to the traditional camera controls in WM 0.99. You can rotate the camera in any direction you want by left-clicking and dragging with the mouse; right-clicking and dragging up and down will move the camera vertically; and the arrow keys on the keyboard move the view in the direction you are facing. This allows you to freely navigate and inspect the terrain from wherever you wish.

**Free Look**：Free Look 模式类似于 WM 0.99 中的传统相机控制。 您可以通过左键单击并用鼠标拖动向任意方向旋转相机； 右键单击并上下拖动将垂直移动相机； 和键盘上的箭头键将视图朝您所面对的方向移动。 这使您可以从任何地方自由导航和检查地形。

• **Reset View**: This resets the current mode to its default rotation – useful if you’ve navigated somewhere strange and can’t find the terrain anymore!

**重置视图**：这会将当前模式重置为默认旋转——如果您导航到某个陌生的地方并且再也找不到地形，这很有用！

• **Snapshot Mode**: The Snapshot more performs a “render” using Opengl at full terrain resolution. Typically terrains higher than 1024×1024 are rescaled down for display due to the millions of triangles produced. Snapshot mode lets you view the terrain in its fully detailed glory. Note that as soon as you move or adjust the view, it will revert back to the realtime display. • **Detail Toggle**: Turns detail texturing on or off. Using a detail texture can help give the terrain a better sense of scale, but you may wish to disable it in some instances to see the “true” terrain.

**快照模式**：快照更多地使用Opengl 在全地形分辨率下执行“渲染”。 由于产生了数百万个三角形，通常高于 1024×1024 的地形会按比例缩小以进行显示。 快照模式可让您查看地形的全貌。 请注意，一旦您移动或调整视图，它就会恢复为实时显示。 • **细节切换**：打开或关闭细节纹理。 使用细节纹理有助于使地形具有更好的比例感，但在某些情况下您可能希望禁用它以查看“真实”地形。

## *2D View*  *二维视图*

![img](.\Image\2D-view-768x410.png)

The 2D View can be selected from the Command Bar, or by pressing **F9**.

可以从命令栏或按 **F9** 来选择 2D 视图。

The 2D View offers you an overhead view of the terrain with optional shading applied to show the relief of the terrain. The 2D View does not use OpenGL or other 3D systems and so is a good viewing choice for very large maps, systems with slow 3D cards, or other conditions that favor 2D use.

二维视图为您提供了地形的俯视图，并应用了可选的阴影来显示地形的起伏。 2D 视图不使用 OpenGL 或其他 3D 系统，因此对于非常大的地图、具有慢速 3D 卡的系统或其他有利于 2D 使用的条件，这是一个很好的查看选择。

The 2D View offers very little interactivity. The display will update to reflect new sunlight conditions when you use the Leftside view to adjust the lighting. When the map is large enough to extend past the view boundaries, you can use the scrollbars to view different areas of the terrain.

2D View 提供的交互性非常低。 当您使用左侧视图调整照明时，显示屏将更新以反映新的阳光条件。 当地图大到足以超出视图边界时，您可以使用滚动条查看地形的不同区域。

## *Layout View*  *布局视图*

Layout View can be selected from the Command Bar, or by pressing **F6**.

可以从命令栏或按 **F6** 来选择布局视图。

![img](.\Image\Layout-View.png)

Layout View is extremely useful for planning out your world. Much like Explorer View, it displays terrain outside of the currently defined render extents. Layout View allows you to rapidly pan and zoom across the entire world, zooming in to view details at a range of a few meters, then pulling out to view many thousands of kilometers of terrain.

布局视图对于规划您的世界非常有用。 与 Explorer View 非常相似，它显示当前定义的渲染范围之外的地形。 布局视图允许您快速平移和缩放整个世界，放大以查看几米范围内的细节，然后拉出以查看数千公里的地形。

A Note about Terrain Artifacts: Layout and Explorer View can display any part of the entire virtual world, not just the render extents you designate. However, this ability means that some devices, in particular simulation-based devices such as Erosion, may not perform identically in these views as they do within the render extents. World Machine marks these devices with an optional warning symbol in the Device Workview. The warning symbol is a red exclamation point: “!” The severity of the problem depends upon the device and zoom level.

关于 Terrain Artifacts 的注释：Layout 和 Explorer View 可以显示整个虚拟世界的任何部分，而不仅仅是您指定的渲染范围。 然而，这种能力意味着一些设备，特别是基于模拟的设备，如侵蚀，在这些视图中的表现可能与它们在渲染范围内的表现不同。 World Machine 在设备工作视图中用可选的警告符号标记这些设备。 警告符号是一个红色感叹号：“！” 问题的严重性取决于设备和缩放级别。

In addition, Layout View provides a visual way to set and modify render extents, and manipulate certain devices that expose parameters to visual adjustment.

此外，Layout View 提供了一种可视化方式来设置和修改渲染范围，以及操作某些将参数暴露给可视化调整的设备。

The most important use of Layout View, however, is in conjunction with a Layout Generator to edit shapes in the Shape View. **Chapter 5** of this manual is devoted to using this incredibly powerful feature. We’ll only slightly address this functionality here.

然而，布局视图最重要的用途是与布局生成器结合使用以在形状视图中编辑形状。 本手册的**第 5 章**专门介绍如何使用这一极其强大的功能。 我们只会在这里略微解决这个功能。

![img](.\Image\Layout-Generator-commands.png)

**Layout Generator Commands**  **布局生成器命令**

● **New Layout:** Creates a new Layout Generator and selects it into the view.

**New Layout：** 创建一个新的Layout Generator 并将其选中到视图中。

● **Select:** Selects as the current device, the Layout Tab being displayed in the view.

**选择：**选择当前设备，布局选项卡显示在视图中。

● **Attach Layout as Mask:** Creates a new Layout Generator and attaches it to the mask input of the currently selected device. This action is not available if the selected device has no mask input.

**Attach Layout as Mask：** 创建一个新的 Layout Generator 并将其附加到当前所选设备的 mask 输入。 如果所选设备没有屏蔽输入，则此操作不可用。

● **Attach Layout as Height Adjustment:** Attaches a Layout Generator to the output of the currently selected device. This action is not available if you are viewing a device with no output.

**附加布局作为高度调整：**将布局生成器附加到当前选定设备的输出。 如果您正在查看没有输出的设备，则此操作不可用。

**Common State Toggles** Clicking any of the buttons in the common function area will toggle their status on/off. The button state is remembered seperately for the Overview tab and the Layout tabs.

**常用状态切换** 单击常用功能区中的任何按钮将切换其状态开/关。 为概览选项卡和布局选项卡单独记住按钮状态。

![img](.\Image\Common-State-Toggles.png)

● **Grid**: Display of a grid atop the terrain

**Grid**：在地形上显示网格

● **Snap**: Snap the mouse to the grid

**捕捉**：将鼠标捕捉到网格

● **RQ**: Displaying the render extents

**RQ**：显示渲染范围

● **Tiles**: Show the render extent being used for tiled output, and show which areas of the terrain will be in which tile

**Tiles**：显示用于分块输出的渲染范围，并显示地形的哪些区域将位于哪个分块中

● **Show**: Show or hide the display of terrain in the Layout View

**显示**：在布局视图中显示或隐藏地形的显示

**Mode Buttons**  **模式按钮**

![img](.\Image\Mode-Buttons.png)

The three mode buttons control the operating mode while in the Overview.

三个模式按钮控制概览中的操作模式。

### **Overview Mode**  **概览模式**

Overview Mode is the default mode. You can perform no actions, merely pan and zoom around the terrain.

概览模式是默认模式。 您不能执行任何操作，只能在地形周围平移和缩放。

### **Render Extent Mode** **渲染范围模式**

Render Extents Mode allows you to graphically add and manipulate your render extents.

渲染范围模式允许您以图形方式添加和操作渲染范围。

**Render Extent Manipulation** **渲染范围操作**

![img](.\Image\Render-Extent-Manipulation.png)

While in Render Extents mode, all of the currently defined extents are visible at their appropriate locations in worldspace. You can click and drag on either the corners of the extent quadrant, or on the extent itself to change its size or location.

在渲染范围模式下，所有当前定义的范围都在世界空间中的适当位置可见。 您可以单击并拖动范围象限的角或范围本身以更改其大小或位置。

**Render Extent Commands** The following commands are available in Render Extent Mode:

**渲染范围命令** 以下命令在渲染范围模式下可用：

![img](.\Image\Render-Extent-Commands.png)

● **Zoom to Extents:** Brings into view the currently selected Render Extents

**Zoom to Extents：**显示当前选择的渲染范围

● **New Extents:** Adds a new Render Extent to the world, that defaults to the same location as the currently selected one.

**新范围：** 向世界添加一个新的渲染范围，默认为与当前选定的相同位置。

● **Set Current:** Set the currently selected Render Extent by dragging a rectangle in the view. Once you finish the drag, the rectangle you defined is the new borders of the current Render Extent.

**设置当前：**通过在视图中拖动一个矩形来设置当前选择的渲染范围。 完成拖动后，您定义的矩形就是当前 Render Extent 的新边框。

● **Manage…:** Bring up the Project Setup dialog to precisely define the Render Extents.

**管理...：**调出项目设置对话框以精确定义渲染范围。

### **Device Mode** **设备模式**

Device Mode lets you manipulate certain device parameters visually that Devices in your world may expose.

设备模式让您可以直观地操作您世界中的设备可能公开的某些设备参数。

![img](.\Image\Device-Mode.png)

There are two options on the Layout Overview Bar that are applicable to Device Mode:

布局概览栏上有两个选项适用于设备模式：

● **Zoom to Device Origin:** If the currently selected device supports a device origin, this button will zoom to its location. Only certain devices, principally Generators, have an origin.

**缩放到设备原点：**如果当前选择的设备支持设备原点，这个按钮将缩放到它的位置。 只有某些设备，主要是发电机，才有来源。

● **Show only Selected:** When checked, you will only see controls (if any) from the currently selected device.

**Show only Selected：**选中时，您将只看到当前所选设备的控件（如果有）。

## *Explorer View* *资源管理器视图*

Explorer View can be selected from the Command Bar, or by pressing **F7**.

可以从命令栏或按 **F7** 选择资源管理器视图。

![img](.\Image\Explorer-View.png)

Explorer View allows you to easily explore the infinite world defined by the devices you placed into your World Machine world. Unlike the 2D and 3D views, you can see and travel over a representation of what the world looks like everywhere, not just within the render extent square. This is ***extremely\*** useful for locating interesting areas of terrain in the current world defined by your device networks.

Explorer View 允许您轻松探索由您放置在 World Machine 世界中的设备所定义的无限世界。 与 2D 和 3D 视图不同，您可以看到并浏览世界各地的表现，而不仅仅是在渲染范围内。 这对于在您的设备网络定义的当前世界中定位有趣的地形区域非常有用。

#### *Explorer Details* *资源管理器详细信息*

What exactly Explorer mode looks like depends greatly upon the power of your computer system and the settings you selected in the Graphics Options dialog.

Explorer 模式的具体外观在很大程度上取决于您的计算机系统的性能和您在“图形选项”对话框中选择的设置。

![img](.\Image\Explorer-Details.png)

Explorer mode uses a *refining progressive level of detail* system. In non-technical terms, this means that the world starts out in very low detail, as seen on the left, and then is continuously refined so that nearby areas are shown with greater resolution, as on the right. In addition, beware that an old or underpowered system might be only able to run Explorer mode at a detail level equal to the left view above. A high-end computer with a powerful 3D card can look like the right side or better.

资源管理器模式使用*细化渐进式细节*系统。 用非技术术语来说，这意味着世界从非常低的细节开始，如左图所示，然后不断细化，以便以更高的分辨率显示附近区域，如右图所示。 此外，请注意，旧的或动力不足的系统可能只能以与上面左视图相同的详细级别运行资源管理器模式。 具有强大 3D 卡的高端计算机可能看起来像右侧或更好。

You can see that in the upper middle of the screen, there is a compass; the red marker indicates the current view direction. North is in the middle, indicated by N; the extreme sides of the compass both represent south.

你可以看到在屏幕的中上部，有一个指南针； 红色标记表示当前视图方向。 北在中间，用N表示； 指南针的两端都代表南方。

On the left, there are three lines of text. They indicate the **current coordinates** of the view along the x and y axis, the **speed** with which you are moving, and the **build load**. Although the first two are self explanatory, the build load is less obvious.

在左边，有三行文字。 它们指示视图沿 x 和 y 轴的**当前坐标**、移动的**速度**以及**构建负载**。 虽然前两个是不言自明的，但构建负载不太明显。

**Build load**: The percentage of time during the last second that Explorer mode has been actively building tiles. Thus, if this value is greater than 0%, tiles are currently being created that will increase the level of detail of the current scene.

**构建负载**：资源管理器模式在最后一秒内主动构建磁贴的时间百分比。 因此，如果此值大于 0%，则当前正在创建的图块将增加当前场景的细节级别。

#### *Exploring Explorer!* *探索资源管理器！*

To use Explorer mode, you can simply jump in and go! Explorer starts in “God’s Eye” navigation mode. You can use the arrow keys and/or the drag the mouse on the landscape to move.

要使用资源管理器模式，您只需跳进去就可以了！ 资源管理器以“上帝之眼”导航模式启动。 您可以使用箭头键和/或在景观上拖动鼠标进行移动。

If you ever get lost, simply push the “View” button on the Explorer Toolbar. This will reset your current position so that you are looking at the current terrain render quad.

如果您迷路了，只需按下资源管理器工具栏上的“查看”按钮即可。 这将重置您的当前位置，以便您查看当前地形渲染四边形。

#### ***Explorer Toolbar*** ***资源管理器工具栏***

![img](.\Image\Explorer-Toolbar.png)

The Explorer Toolbar is divided into two segments that deal with different aspects of Explorer. They are, from left to right across the toolbar:

Explorer 工具栏分为两个部分，分别处理 Explorer 的不同方面。 它们在工具栏中从左到右依次为：

*View Locations:* *查看地点：*

• **View**: Move the camera to bring the current render quad into view.

**View**：移动相机使当前渲染四边形进入视野。

• **Jump:** Jump to a particular location by specifying X/Y coordinates.

**跳转：** 通过指定X/Y 坐标跳转到特定位置。

*Navigation Mode:* *导航模式：*

Each navigation mode uses the keys in a slightly different way:

每种导航模式使用按键的方式略有不同：

• **God’s Eye:** Pan around the terrain by dragging it.

**上帝之眼：** 通过拖动在地形周围平移。

o Dragging the terrain with the **left mouse button** moves the camera o Dragging up/down with the **right button** changes your elevation o **Left + Right mouse buttons** together change the current viewing angle

o 使用 **鼠标左键** 拖动地形移动相机 o 使用 **右键** 向上/向下拖动更改您的高度 o **鼠标左键 + 右键** 一起更改当前视角

• **Fly:** Fly above the terrain.

**飞行：** 飞越地形。

o **Up/down arrow** controls speed o **Left/right arrow AND/OR mouse** controls heading and elevation o **Right mouse button + mouse up/down** adjusts elevation

**o **上/下箭头**控制速度 o **左/右箭头和/或鼠标**控制航向和高度 o **鼠标右键+鼠标上/下**调整高度

• **Walk:** Walk over the terrain.

**步行：** 在地形上行走。

o Up/down arrow steps forward/back o Left/right arrow sidesteps o Left mouse button + mouse left/right adjusts heading o ***Hold down\*** **the right mouse button** to step forward

o 向上/向下箭头前进/后退 o 左/右箭头退步 o 鼠标左键+鼠标左/右调整航向 o ***按住\*** **鼠标右键** 前进

• **Drive:** Drive around the terrain in a buggy.

**驾驶：** 驾驶越野车绕过地形。

o Up/down arrow accelerates/brakes o Left/right arrow turns o Holding the ctrl key puts the buggy into “hover” mode o Holding the shift key acts as a “turbo boost”

o 向上/向下箭头加速/刹车 o 左/右箭头转动 o 按住 ctrl 键使越野车进入“悬停”模式 o 按住 shift 键作为“涡轮增压”

#### ***Explorer Caveats*** ***探索者注意事项***

Explorer Mode is a very powerful and useful feature. However, because of its demanding nature, it requires a lot from your computer system. Specifically: a fast CPU to generate terrain tiles, and a fast video card to display them. You will likely need to play with the quality presets in the Layout/Explorer Performance Options dialog to find a performance level acceptable for your system.

资源管理器模式是一个非常强大和有用的功能。 但是，由于其苛刻的性质，它对您的计算机系统要求很高。 具体来说：用于生成地形图块的快速 CPU，以及用于显示它们的快速视频卡。 您可能需要使用 Layout/Explorer Performance Options 对话框中的质量预设来找到您的系统可接受的性能级别。

In addition, much like Layout View, some devices will cause visual artifacting within Explorer Mode! See the warning in section 4.4 for more information.

此外，与布局视图非常相似，某些设备会在浏览器模式下导致视觉失真！ 有关详细信息，请参阅第 4.4 节中的警告。