# Leftside View

左侧视图

You’ll see a panel running vertically along the left side of the screen. This panel contains a number of useful shortcuts and tools to help understand and manipulate your world.

您会看到一个面板沿屏幕左侧垂直运行。 该面板包含许多有用的快捷方式和工具，可帮助您理解和操纵您的世界。

The leftside view can be shown and hidden by pressing the **F4** key. You can also resize the panel by dragging on the splitter between it and the primary viewport area, or drag the panel and put it on a different screen completely if you wish.

按 **F4** 键可以显示和隐藏左侧视图。 您还可以通过拖动面板和主视口区域之间的分隔线来调整面板大小，或者如果您愿意，也可以拖动面板并将其完全放在不同的屏幕上。

Let’s take a look at each component in turn:

让我们依次看一下每个组件：

## Terrain Preview Window 地形预览窗口

This window allows you to view a small, preview version of the current terrain area before it is built. This window shows whatever device or port is currently selected.

此窗口允许您在构建之前查看当前地形区域的小型预览版本。 此窗口显示当前选择的任何设备或端口。

 ![img](.\Image\image-17.png)

Above the preview window, the name of the current render extent is displayed. Clicking the scroll arrows next to the name allows you to cycle through all of the currently defined render extents. You can create new render extents in the Explorer View or [Project Settings](https://help.world-machine.com/topic/render-extents-and-project-setup/).

在预览窗口上方，显示当前渲染范围的名称。 单击名称旁边的滚动箭头可以循环浏览所有当前定义的渲染范围。 您可以在资源管理器视图或 [项目设置](https://help.world-machine.com/topic/render-extents-and-project-setup/) 中创建新的渲染范围。

If you drag in the preview window, you can manipulate the current lighting direction in all viewports. You can also hold down ALT and navigate within the viewport exactly as if it was a [3D View](https://help.world-machine.com/topic/terrain-views/).

如果在预览窗口中拖动，则可以在所有视口中操纵当前光照方向。 您还可以按住 ALT 并在视口中导航，就好像它是 [3D 视图](https://help.world-machine.com/topic/terrain-views/)。

Immediately below the viewport is a line of buttons. From left to right, they are:

视口正下方是一行按钮。 从左到右，它们是：

#### Configure Viewport 配置视口

Click this button to open a drop-down menu with several options for manipulating the 3D view inside the preview:

单击此按钮可打开一个下拉菜单，其中包含多个用于在预览中操作 3D 视图的选项：

- **Zoom camera to fit** – adjust the camera zoom distance to fit the current scene into the window.

  **Zoom camera to fit** – 调整相机变焦距离以适应窗口中的当前场景。

- **Reset to top view** – Position the camera looking directly down on the terrain

  **重置为俯视图** – 将相机定位在直视地形的位置

- **Reset to perspective view** – Position the camera looking at the terrain from a moderate angle, aligned with the North-South (Y) axis.

  **重置为透视图** – 将相机从一个适度的角度观察地形，与南北 (Y) 轴对齐。

#### Global View Toggles 全局视图切换

The next three buttons are **global toggles.** They enable/disable their particular option across every viewport in the entire program.

接下来的三个按钮是 **全局切换。** 它们在整个程序的每个视口中启用/禁用其特定选项。

- **Show Lighting** – Toggle whether or not to light the terrain. You can define the lighting by right-clicking to bring up the **Viewport Lighting Setup** dialog.

  **Show Lighting** – 切换是否照亮地形。 您可以通过右键单击调出 **Viewport Lighting Setup** 对话框来定义照明。

- **Show Materials** – Toggle the use of any material for the terrain. When enabled, heightfields will have the currently defined color map, and scenes will use their material input. When disabled, the terrain will be shown in a neutral gray only.

  **显示材料** – 切换对地形的任何材料的使用。 启用后，高度场将具有当前定义的颜色贴图，场景将使用其材质输入。 禁用时，地形将仅以中性灰色显示。

- **Show Water** – Toggle the display of scene water, if any. If this is off, no water will be displayed regardless of which device is selected.

  **Show Water** – 切换场景水的显示（如果有）。 如果关闭，则无论选择哪个设备都不会显示水。



## Display Guides 显示指南

Display guides are shown in every view and help you design and construct your world.

显示指南显示在每个视图中，可帮助您设计和构建您的世界。

![img](.\Image\image-20.png)

<div align="center"><i>The currently available display guides <br>当前可用的显示指南</i></div>

Each display guide has a checkbox that can be toggled to turn it on or off globally. Some guides have additional controls to manipulate them.

每个显示指南都有一个复选框，可以切换以全局打开或关闭它。 一些指南有额外的控制来操纵它们。

In order, the guides are are:

按顺序，指南是：

- **Sealevel**: Display a flat plane that can be used to show the water level of the ocean. This is a helpful guide only, and does not actually create water within your scene. Set the water level either directly or by using the slider.

  **海平面**：显示可用于显示海洋水位的平面。 这只是一个有用的指南，实际上不会在您的场景中创建水。 直接或使用滑块设置水位。

- **Tracing**: Drape an external image atop your terrain. This is very helpful when recreating continents and other features from some external source within World Machine (See the Shapes (Layout Generator) for more information on this technique). The folder icon to the right of the slider lets you pick the file to use, while the slider itself controls the opacity of the tracing guide.

  **追踪**：在您的地形上覆盖外部图像。 这在 World Machine 中从某些外部源重新创建大陆和其他特征时非常有用（有关此技术的更多信息，请参阅形状（布局生成器））。 滑块右侧的文件夹图标可让您选择要使用的文件，而滑块本身可控制描摹指南的不透明度。

- **Tile Overlay** (Pro only): Overlay the boundaries of each individual output tile atop the world

  **Tile Overlay**（仅限专业版）：在世界上覆盖每个单独输出图块的边界

- **Contour Lines**: Show contour lines on the terrain, much like a traditional topographic map. Very helpful in understanding the shape of the terrain in areas of low contrast.

  **等高线**：显示地形上的等高线，很像传统的地形图。 非常有助于理解低对比度区域的地形形状。

## Devices 设备

The device list shows you all of the top-level devices that exist in your world. This can be useful in selecting and navigating around between them. There are also some convenience buttons for taking actions upon the currently selected device.

设备列表显示了您的世界中存在的所有顶级设备。 这对于在它们之间进行选择和导航很有用。 还有一些方便的按钮，用于对当前选定的设备执行操作。

![img](.\Image\image-21.png)

The shortcuts above the device list let you:

设备列表上方的快捷方式让您：

- **Edit device properties**: Opens a new window with the selected device’s settings.

  **编辑设备属性**：打开一个包含所选设备设置的新窗口。

- **Set device resolution**: Override the world resolution and spatial type for the selected device.

  **设置设备分辨率**：覆盖所选设备的世界分辨率和空间类型。

- **Set name**: Give the device a unique name; you can also do this from the device settings window.

  **设置名称**：给设备一个唯一的名称； 您也可以从设备设置窗口执行此操作。

- **Lock preview:** Lock all views to show this device, even if you later select a different one. Locking a device that is already locked will unlock the view.

  **锁定预览：**锁定所有视图以显示此设备，即使您稍后选择了不同的视图也是如此。 锁定已经锁定的设备将解锁视图。

Locking the preview is an incredibly important operation! You will often want to continue viewing the final result of your scene while editing various other devices, for example.

锁定预览是一项非常重要的操作！ 例如，您通常希望在编辑各种其他设备时继续查看场景的最终结果。

All of the shortcuts from the workview also work in the device list; you can **double click or control click** to open a device’s properties, or **alt-click** to lock the preview on that device.

工作视图中的所有快捷方式也适用于设备列表； 您可以**双击或控制点击**打开设备的属性，或**alt-click**锁定该设备上的预览。

## History 历史

The history panel shows you all of the edits you have made to your world since the session started. You can jump to any point in time you wish simply by clicking there:

历史面板显示了自会话开始以来您对世界所做的所有编辑。 您只需单击此处即可跳转到您希望的任何时间点：

![img](.\Image\image-23.png)

Unless you maintain a project session file (Pro Edition only), the history of your edits are only preserved in the current editing session, and will be lost when the world is saved and reloaded.

除非您维护一个项目会话文件（仅限专业版），否则您的编辑历史仅保留在当前编辑会话中，并且在保存和重新加载世界时将丢失。



## Project Snapshots 项目快照

You can save several versions of your world as you work. It can be very helpful to create snapshots for major milestones of your project world.

您可以在工作时保存多个版本的世界。 为项目世界的主要里程碑创建快照非常有帮助。

![img](.\Image\image-24.png)

Being able to recreate an exported asset exactly even if you’ve later improved on the project is very useful!

即使您后来改进了项目，也能够准确地重新创建导出的资产，这非常有用！