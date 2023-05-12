# Device Workspace 设备工作空间



## Device Workview 设备工作视图

The Workview is the most important view in World Machine. You can select the workview from the toolbar, or by pressing **F5**. It also is the default view when World machine starts.

Workview是World Machine中最重要的视图。您可以从工具栏中选择工作视图，或者按**F5**。它也是World machine启动时的默认视图。

![img](.\Image\image-26.png)

Your World Machine world is defined by the devices that exist and their connections, and the workview is your view of them.

您的世界机器世界是由存在的设备及其连接定义的，而工作视图是您对它们的视图。

What are devices?

什么是设备?

## Devices 设备

**Devices** are everything in World Machine. They represent an *action* or *effect*. Much like a flowchart, you create a world by connecting together the boxes with lines (wires).

在《World Machine》中，设备就是一切。它们代表一个“动作”或“效果”。就像流程图一样，你通过用线(线)将盒子连接在一起来创建一个世界。

![img](.\Image\image-25.png)

A device has **Ports**. A port allows data to enter or leave a device. In the device networks, data generally flows from left to right.

设备有**端口**。端口允许数据进入或离开设备。在设备网络中，数据通常从左向右流动。

**Inputs** are on the left side of the device, and bring data into a device to be acted on. After the action of the device takes place, the data is then taken out of the device via an **output**, on the right side. Some devices have a **mask input port** on the bottom, which controls the area of effect of that device.

**输入**在设备的左侧，并将数据带入要操作的设备。在设备的动作发生后，数据随后通过右侧的输出**从设备中取出。有些设备在底部有一个掩码输入端口，用来控制该设备的作用区域。

There is one other type of port in World Machine, called a parameter port. These are located along the top edge of the device, and allow advanced users to adjust the settings of a device from a different one. Use of Parameter Ports is covered later in the manual.

在World Machine中还有另一种类型的端口，称为参数端口。这些位于设备的顶部边缘，允许高级用户从不同的设备调整设备的设置。参数端口的使用将在手册的后面介绍。

It is helpful to think in terms of creating, modifying or exporting data. Data is:

从创建、修改或导出数据的角度进行思考是有帮助的。数据是:

- **Created** by *Generator* devices
- **Modified** by *Filters and Combiner* devices
- **Exported** by *Output* devices.

### Add a new device 添加新设备

You will constantly be adding new devices to your world, so there are multiple ways to accomplish this. Choose the one that makes the most sense to you. The “Add from Search” option by pressing **TAB** is the most powerful.

你将不断向你的世界添加新设备，所以有多种方法可以实现这一目标。选择一个对你来说最有意义的。按**TAB**从搜索中添加”选项是最强大的。

1. Select the device you want from the Devices menu:

   从“设备”菜单中选择所需的设备:

![img](.\Image\image-29.png)

2. Select the device from the toolbar: 

   在工具栏中选择设备:

![img](.\Image\image-30.png)

3. Right click in the workview to access the context menu

   在工作视图中右键单击以访问上下文菜单

![img](.\Image\image-31.png)

4. Most powerfully, press **tab** to bring up the Add from Search dialog:

   最强大的是，按**tab**弹出“从搜索中添加”对话框:

![img](.\Image\image-32.png)

Depending on the method you’ve chosen, it will either immediately place a new device at the spot the mouse cursor was at, or show you a small ghost outline of the device. Click the mouse to place the device where the ghost is shown.

根据您选择的方法，它会立即在鼠标光标所在的位置放置一个新设备，或者向您显示设备的小幽灵轮廓。点击鼠标将设备放置在显示幽灵的地方。

By default, you will add a single device of that type to the world. If you’d like, you can hold down SHIFT to continue adding multiple devices of the same type.

默认情况下，您将向世界添加该类型的单个设备。如果您愿意，可以按住SHIFT键继续添加多个相同类型的设备。

If you click on a device or port, World Machine will automatically connect your new device to that port.

如果你点击一个设备或端口，World Machine会自动将你的新设备连接到该端口。

### Selecting & Moving Devices 选择和移动设备

![img](.\Image\image-38.png)

- You may select a single device by simply clicking it.
- 你可以选择一个单一的设备，只需点击它。
- You may add another device to the selection by holding **SHIFT** and clicking on that device. Clicking a selected device with shift held will toggle it out of the selection.
- 您可以通过按住**SHIFT**并点击该设备来添加另一个设备。按住shift键单击选定的设备将使其退出选定。
- You may select multiple devices at once with drag-selection: Click in an empty part of the workview and drag a box around your chosen devices.
- 您可以通过拖拽选择一次选择多个设备:单击工作视图的空白部分，并在所选设备周围拖动一个框。
- Holding down shift while drag-selecting will add the drag-selected group to the currently selected devices.
- 在拖拽选择时按住shift键会将拖拽选择的组添加到当前选择的设备中。

You may move any selected device(s) by simply clicking and dragging on the device.

您可以移动任何选定的设备(s)，只需点击和拖动设备。

### Device Status 设备状态

Next to the name of a device, there is a small colored box that shows you its **status**. The status tells you if the device has been built or not, or if it has encountered an error.

在设备名称旁边，有一个小的彩色方框，显示设备的状态。状态告诉您设备是否已经构建，或者它是否遇到了错误。

![img](.\Image\image-27.png)

Pictured above are three devices in various build states.

上图是三个处于不同构建状态的设备。

• **Green Status**: The Advanced Perlin shown above is fully built and properly connected. The status indicator is a deep green. If you click on the device, you can see the highest resolution build results.

**绿色状态**:上面显示的先进柏林已完全建成并正确连接。状态指示灯呈深绿色。如果你点击设备，你可以看到最高分辨率的构建结果。

• **Pale Green Status**: The device is properly connected. However, it has not yet been fully built; it is only showing you a preview. The devices are built in the background up to certain resolution, and the color will change from yellow to green as it builds at higher and higher resolution.

**淡绿色状态**:设备连接正常。然而，它还没有完全建成;它只是向你展示一个预览。这些设备是在一定分辨率的背景下构建的，当分辨率越来越高时，颜色会从黄色变为绿色。

• **Red Status**: The device is unconnected, or there’s a problem. In the image above, the Height Output is not connected to anything, so it cannot function.

**红色状态**:设备未连接，或有问题。在上图中，高度输出没有连接到任何东西，所以它不能工作。

How do you connect together two devices?

如何将两个设备连接在一起?

### Wiring Devices 连接设备

To wire two devices together, you must connect an output port on one device to an input port on another, or vice versa. To do this, begin dragging on one of the ports. A wire will become attached to that port on one end, and the mouse cursor on the other. All ports will disappear except those that are potential connections.

要将两个设备连接在一起，必须将一个设备的输出端口连接到另一个设备的输入端口，反之亦然。为此，开始拖动其中一个端口。一根电线将被连接到端口的一端，鼠标光标在另一端。所有的端口将消失，除了那些潜在的连接。

![img](.\Image\image-33.png)

When you release the mouse button over the other port it will create a wire connecting the two devices, assuming that such a connection is allowed.

当您在另一个端口上释放鼠标按钮时，它将创建一条连接两个设备的线，假设允许这样的连接。

If you release the mouse button over empty space, World Machine will bring up the add-from-search dialog to let you quickly create a new device and wire it to the port you started dragging from.

如果你在空白区域释放鼠标按钮，World Machine将弹出add-from-search对话框，让你快速创建一个新设备，并将其连接到你开始拖动的端口。



**Connecting an output multiple times **

**多次连接输出**

You can connect a single output port to many different devices, eliminating the need for a Splitter device. An input can only have a single connection, however.

您可以将单个输出端口连接到许多不同的设备，从而消除了对Splitter设备的需求。但是，一个输入只能有一个连接。

### Wire Routing 布线

World Machine has a *wire routing* feature. By clicking and dragging on a wire, you can add a route point, which is a simple organizational aid.

World Machine有一个“电线布线”功能。通过在导线上单击和拖动，您可以添加路由点，这是一种简单的组织帮助。

![img](.\Image\image-34.png)

The wire will run through wherever you place the route point. You can add multiple route points to a single wire. You can move route points by dragging them.

无论你把线路点放在哪里，电线都会穿过。您可以在单线上添加多个路由点。您可以通过拖动路由点来移动它们。

Adjacent routing points can be merged together into a single point by dragging one atop the other. In addition, you may start a new wire by left-clicking on a routing point, or attach a wire by ending a wire drag operation on one.

相邻的路由点可以通过拖动一个点到另一个点上合并成一个点。此外，您可以通过左键单击路由点来启动新的导线，或者通过结束对导线拖动操作来附加导线。

Right-clicking on a wire will bring up the wire context menu:

右键单击导线将调出导线上下文菜单:

![img](.\Image\image-35.png)

● **Remove all route points:** This wire is removed from any routing points it runs through. Routing points are deleted unless they are shared.

**移除所有路由点:**这条线从它穿过的任何路由点移除。除非路由点被共享，否则它们将被删除。

● **Delete wire:** The wire is removed from the device world, disconnecting the associated devices.

**删除电线:**将电线从设备世界中移除，断开相关设备的连接。

## Groups 组

Groups are a way to logically organize your device network. Groups are named, and you can add a description to help you remember what a particular group does.

组是一种逻辑地组织设备网络的方法。组被命名，您可以添加描述来帮助您记住特定组的功能。

 ![img](.\Image\image-36.png)

### **Group Creation** 创建组

To create a group, you have two options:

要创建一个组，您有两个选项:

● Select one or more devices, then right click on them and choose “Group selected devices” from the context menu.

选择一个或多个设备，然后右键单击它们，并在上下文菜单中选择“分组选定设备”。

● Use the Grouping Tool to draw a group in the workview (described below)

使用分组工具在工作视图中绘制组(如下所述)

### **Group Manipulation **组操作

When you move a group, all the devices and sub-groups inside of it are moved as well. When a group runs into another group, it will push that group and any others out of the way.

当您移动一个组时，其中的所有设备和子组也会随之移动。当一个群体遇到另一个群体时，它会把那个群体和其他群体推开。

 ![img](.\Image\Group-Manipulation.png)

If you don’t want this bumping behavior, you can turn the group into a floating group, by editing the group (below). It will then not interact with other groups in any way. A solid group has a solid border. A floating group has a dashed border.

如果您不想要这种碰撞行为，您可以通过编辑组(如下所示)将组转换为浮动组。然后它将不会以任何方式与其他组交互。实线群有实线边界。浮动组有虚线边框。

### **Editing a Group**编辑组

To edit a group’s properties, double click on the group to open the Group Settings dialog:

要编辑一个组的属性，双击该组打开组设置对话框:

 ![img](.\Image\Image-37.png)

This dialog allows you to set a group’s name, text, RGBA color, and floating status.

这个对话框允许您设置组的名称、文本、RGBA颜色和浮动状态。

**Editing a Device’s Properties:** **编辑设备属性:**

To change the properties of a device, simply double click it in the workview. A dialog will appear that allows you to change the parameters and settings of the device. The Leftside preview will show you the results of any adjustments you make.

要更改设备的属性，只需在工作视图中双击它。将出现一个对话框，允许您更改设备的参数和设置。左侧预览将显示您所做的任何调整的结果。

**Deleting Devices:删除设备:**

To delete a device, simply select it and then choose Delete Device from the Edit menu, or simply hit the Delete key. By default, you will be prompted to confirm the decision to delete the device – if you wish to avoid this prompt, hold the shift key while you hit Delete.

要删除设备，只需选择它，然后从“编辑”菜单中选择“删除设备”，或者只需按“删除”键。默认情况下，您将被提示确认是否删除设备-如果您希望避免此提示，按住shift键，同时点击删除。

## Workview Commands Workview命令

The Edit menu contains a number of standard commands that are valid within the device workview, including undo/redo and copy/paste:

编辑菜单包含许多在设备工作视图中有效的标准命令，包括撤消/重做和复制/粘贴:

 ![img](.\Image\Image-40.png)

These are fairly typical editing commands that are also valid in other viewports.

这些是相当典型的编辑命令，在其他视图中也有效。

## **Device Commands 设备命令**

You can access a list of device commands by right clicking on any device, or from the top menubar ‘Commands’ entry:

您可以通过右键单击任何设备或从顶部菜单栏“命令”条目访问设备命令列表:

 ![img](.\Image\Image-39.png)

- **About this device:** A short description of what the device does.

  **关于本设备:**设备功能的简短描述。

- **Set Name:** Renames the device.

  **设置名称:**重命名设备名称。

- **Set Properties**: Sets the properties of the device (same as double-clicking).

  **设置属性**:设置设备属性(与双击相同)。

- **Set Resolution**: Override the project resolution, or make this device [localspace](https://help.world-machine.com/topic/localspace/).

  **设置分辨率**:覆盖项目分辨率，或将此设备设置为[localspace](https://help.world-machine.com/topic/localspace/)。

- **Set output display hint:** Control how WM displays interprets the elevation data. See the **Display Hint** section below for more details.

  **设置输出显示提示:**控制WM显示如何解释高程数据。请参阅下面的**显示提示**部分了解更多细节。

- **Lock Preview on Device: Freezes the preview** on the currently selected device.

  **锁定预览设备:冻结预览**在当前选定的设备。

- **Bypass Device:** Bypassing a device temporarily makes the device perform no action. This can be very useful for judging the effects of a device on a network by toggling bypass mode on and off for that device.

  **旁路设备:**暂时旁路设备使设备不做任何动作。这对于通过为该设备打开和关闭旁路模式来判断该设备对网络的影响非常有用。

- **Disable Device:** Disables the device. A disabled device is grayed out, and will not be activated when the world is build. Any devices depending on its output will also fail to build. Selecting this again will re-enable the device.

  **Disable Device:**禁用设备。被禁用的设备将显示为灰色，并且在构建世界时不会被激活。任何依赖其输出的设备也将无法构建。再次选择此选项将重新启用设备。

- **Disconnect Device:** Remove all wires from this device so that it is isolated from the rest of the network.

  **断开设备:**从该设备上拆除所有电线，使其与网络的其余部分隔离。

- **Convert Devices into Macro**: Converts the selected device(s) to a macro. Any links leading into or out of the collection of selected devices are converted to macro ports. See Chapter 8: Macros for more information.

  **将设备转换为宏**:将选定的设备转换为宏。任何进入或退出所选设备集合的链接都转换为宏端口。有关更多信息，请参见第8章:宏。

- **Group selected:** Create a new group around the currently selected device(s). See Chapter 2.3 below for more information on groups.

  **选择的组:**在当前选择的设备周围创建一个新组。有关组的更多信息，请参见下面的第2.3章。

**Display Hints: 显示提示**

World Machine allows you to provide a hint as to how the heightfield should be displayed, since a heightfield is fundamentally simply a rectangular region of data. Your two choices are terrain or mask. Many devices will automatically flag their output appropriately. Terrain means that the output will be shown as an elevation; mask, as a black and white flat image.

World Machine允许您提供关于如何显示高度字段的提示，因为高度字段基本上只是一个矩形数据区域。你的两个选择是地形或面具。许多设备将自动适当地标记它们的输出。地形意味着输出将显示为海拔;蒙版，作为黑白平面图像。

 ![img](.\Image\Terrain-Hints.png)

## *Tools 工具*

The device toolbar also contains a *Tools* section. These are not devices; instead they help you manipulate and visualize your project.

设备工具栏还包含一个*Tools*部分。这些不是装置;相反，它们可以帮助您操作和可视化您的项目。

![img](.\Image\Image-28.png)

From left to right, they are:

从左到右分别是:

- **Create Group** – click this button then drag within the workview to create a new grouping of your devices. See the section on Groups above for more details.
- **创建组** -单击此按钮，然后在工作视图内拖动以创建您的设备的新分组。有关详细信息，请参阅上面的组部分。
- **Create Blueprint** – click this button and drag within the workview to define and save to your library a reusable component, called a blueprint. Blueprints can be later added to any world, allowing you to quickly add sets of devices together that you commonly use.
- **创建蓝图** -单击此按钮并在工作视图中拖动，以定义并保存到库中可重用的组件，称为蓝图。蓝图可以稍后添加到任何世界中，允许您快速将常用的设备组合在一起。

### Overlays 叠加

Overlays let you see at a glance what parts of your world are consuming the most resources. The overlay changes the color of devices and wires according to their resource usage:

叠加让你一眼就能看到世界的哪个部分消耗了最多的资源。叠加会根据设备和电线的资源使用情况改变颜色:

![img](.\Image\Image-41.png)

The options available are:

可用的选项有:

- **Build Time**: Color devices by the amount of time taken to build
- **建造时间**:按建造时间的数量为设备着色
- **Memory**: Color devices by the amount of memory consumed
- **内存**:根据所消耗的内存量为设备着色
- **Tile Blending**: Color devices by their (in)compatibility with tiled builds
- **平铺混合**:颜色设备的(在)兼容性平铺构建