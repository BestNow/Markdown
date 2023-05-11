# Render Extents and Project Setup

渲染范围和项目设置

Although the devices you connect determine the look and feel of your world, it is the render extents that define the area of the world that you are working in. In this way, the render extents control what you’re looking at. You can zoom down to a very small area of a few meters, or cover a vast thousand- kilometer region of terrain.

虽然您连接的设备决定了您的世界的外观和感觉，但渲染范围定义了您正在工作的世界区域。通过这种方式，渲染范围控制了您正在查看的内容。 您可以缩小到几米的非常小的区域，或覆盖广阔的数千公里地形区域。

**Render Extent**: A rectangular area that exists in 3D world space, used to set the area of terrain being exported or viewed. The Render Extent stores the location, resolution, and other information for this view into your world.

**Render Extent**：存在于3D世界空间中的一个矩形区域，用于设置导出或查看的地形区域。 渲染范围将此视图的位置、分辨率和其他信息存储到您的世界中。

World Machine allows you to have multiple Render Extents defined. This ability is useful to be able to see, work on, or export multiple different areas of the world. Render Extents can be created and manipulated in the Project Setup dialog, described below. In addition, Render Extents can be graphically manipulated in the Explorer View.

World Machine 允许您定义多个渲染范围。 这种能力对于能够查看、处理或导出世界的多个不同区域很有用。 渲染范围可以在“项目设置”对话框中创建和操作，如下所述。 此外，可以在资源管理器视图中以图形方式操作渲染范围。

## Project Setup 项目设置

To setup your project options, select **Project Settings** from the *Project* menu, or click the appropriate icon in the toolbar.

要设置项目选项，请从 *Project* 菜单中选择 **Project Settings**，或单击工具栏中的相应图标。

The project settings dialog will begin at the Scene Setup tab:

项目设置对话框将从“场景设置”选项卡开始：

 ![img](.\Image\image-50.png)

Let’s take a look through the section you’ll want to edit.

让我们看一下您要编辑的部分。

### Scene Selection 情景选择

Every world contains at least one render extent. You can add additional if you wish using the “New Extent…” button. You can select or cycle through the available render extents.

每个世界至少包含一个渲染范围。 如果您愿意，可以使用“新范围...”按钮添加其他内容。 您可以选择或循环浏览可用的渲染范围。

It is also possible to *lock* a render extent. This makes sure that its settings are not accidently changed in the future. To change a locked render extent requires you to first unlock it.

也可以*锁定*渲染范围。 这可确保其设置不会在未来意外更改。 要更改锁定的渲染范围，您需要先将其解锁。

### Resolution 解决

*Please note that the Basic Edition of World Machine is limited to 1025×1025 or lower resolution*

*请注意World Machine基础版限制为1025×1025或更低分辨率*

The Resolution slider controls the size in pixels of the world to be built. Higher settings are more detailed but consume more memory and are slower to build. The exact maximum resolution at which you can build a given world at depends upon the devices present, and the amount of system memory you have.

分辨率滑块控制要构建的世界的大小（以像素为单位）。 更高的设置更详细，但会消耗更多内存并且构建速度更慢。 您可以构建给定世界的确切最大分辨率取决于存在的设备以及您拥有的系统内存量。

- **“Power of Two plus one”**: This dropdown controls the resolution strategy to employ when adjusting the slider. It allows you to easily control the final resolution of your extent according to a variety of methods. If you want to set a completely custom resolution, just choose “Custom” from this strategy and enter the value in the resolution box.

  **“二加一的幂”**：此下拉列表控制调整滑块时采用的分辨率策略。 它允许您根据多种方法轻松控制您的范围的最终分辨率。 如果要设置完全自定义的分辨率，只需从此策略中选择“自定义”，然后在分辨率框中输入值即可。

### Memory Conservation 内存守恒

Normally, World Machine keeps the results for every device in memory at once. This works well when you’re editing the world, but it requires a large amount of memory for high resolution builds.

通常，World Machine 会同时将每个设备的结果保存在内存中。 这在您编辑世界时效果很好，但它需要大量内存才能构建高分辨率。

When Memory Conservation is turned on, increasing amounts of build results are not kept and the network will likely have to be regenerated after any change. Previews are always retained.

当启用内存保护时，不会保留越来越多的构建结果，并且在任何更改后可能必须重新生成网络。 始终保留预览。

The strategies available are:

可用的策略是：

- **No Conservation**: All results are always kept. This requires the most memory!

  **No Conservation**：始终保留所有结果。 这需要最多的内存！

- **Discard unconnected ports**: Any ports that are not connected to another device have their results discarded.

  **丢弃未连接的端口**：任何未连接到其他设备的端口都会丢弃其结果。

- **Keep only outputs and checkpoints**: All devices have their results discarded after building, unless they are either a final output or a checkpoint. Checkpoints serve as a “cache”, letting you save intermediate results so that only a portion of the world will need to be rebuild after a change.

  **仅保留输出和检查点**：所有设备在构建后都会丢弃其结果，除非它们是最终输出或检查点。检查点充当“缓存”，让您保存中间结果，以便在更改后只需要重建世界的一部分。

- **Keep only outputs:** All devices have their results discarded. Changing anything after a final build will require another full final build.

  **只保留输出：**所有设备的结果都被丢弃。 在最终构建之后更改任何内容都需要另一个完整的最终构建。



### World Dimensions 世界维度

This very important section allows you to specify the size and shape of your render extents. These are all presented as specific numerical values; if you want to set the render extent graphically, use the Explorer View.

这个非常重要的部分允许您指定渲染范围的大小和形状。 这些都以具体的数值呈现； 如果要以图形方式设置渲染范围，请使用资源管理器视图。

- **Origin**: The center of the render extent in worldspace.

  **原点**：世界空间中渲染范围的中心。

- **Width & Breadth**: The size of the extent on the X and Y axis, centered around the origin.

  **宽度和宽度**：X 和 Y 轴上范围的大小，以原点为中心。

- **Square/Nonsquare**: This toggle allows you to constrain the width and breadth to be equal to each other.

  **方形/非方形**：此切换允许您将宽度和宽度限制为彼此相等。

As mentioned in the dialog, the maximum vertical elevation is global to all of your render extents, and is set in the Project Setup tab.

如对话框中所述，最大垂直高度对于所有渲染范围都是全局的，并在“项目设置”选项卡中设置。

### Project Setup 项目设置

This tab contains general options for your project.

此选项卡包含项目的常规选项。

 ![img](.\Image\image-51.png)

- **Author and Description:** You can record your name and add any description to the project that you wish that will help yourself or others in the future.

  **作者和描述：**您可以记录您的姓名并向项目添加您希望将来对自己或他人有帮助的任何描述。

- **Override relative project path**: When checked, you can set the base folder that all relative paths in this project will resolve from. If unchecked, the default is always the location of your worldfile.

  **Override relative project path**：选中后，您可以设置该项目中所有相对路径将从中解析的基础文件夹。 如果未选中，则默认始终是您的世界文件的位置。

#### Colors 颜色

Heightfields have automatic color-by-elevation applied to them as a visual aid. You can choose the color scheme you wish to apply here. This color scheme is only intended as a visual aid; you’ll typically create a custom texture for your terrain within the world itself.

Heightfields 具有自动按高度应用颜色作为视觉辅助。 您可以在此处选择要应用的配色方案。 此配色方案仅用作视觉辅助； 您通常会为世界本身的地形创建自定义纹理。

#### Dimension Preference 维度偏好

You can choose to present distances in either kilometer or unitless (World Machine Units). For most purposes, you should work with metric units.

您可以选择以公里或无单位（世界机器单位）显示距离。 对于大多数用途，您应该使用公制单位。

You can also set the maximum elevation possible in your project. Internally, World Machine keeps all height information as a number between 0 and 1. The scaling value set here allows you to set the elevation in meters that a maximum height value refers to. The greater this number, the taller the maximum mountain height.

您还可以设置项目中可能的最大高度。 在内部，World Machine 将所有高度信息保存为 0 到 1 之间的数字。此处设置的缩放值允许您设置最大高度值所指的以米为单位的海拔高度。 这个数字越大，最大山峰高度就越高。

Note that this scaling value is applied worldwide; increasing the value here will instantly increase the apparent vertical relief of every terrain in the world. If the terrain you’re creating is sensitive to having exact elevations, it’s advisable to **set this only once at the start of your project** to the greatest range of elevations you foresee using and then not change the value.

请注意，此缩放值适用于全球； 增加此处的值将立即增加世界上每个地形的明显垂直起伏。 如果您正在创建的地形对具有精确的高程很敏感，建议在您的项目开始时**仅将此设置一次**到您预见使用的最大高程范围，然后不要更改该值。

### Tiled Export Options (Professional Edition Only) 平铺导出选项（仅限专业版）



![img](.\Image\Tiled-export-options.png)

**Please see the Professional Edition Appendix for information on Tiled Builds!**

有关 Tiled Builds 的信息，请参阅专业版附录！