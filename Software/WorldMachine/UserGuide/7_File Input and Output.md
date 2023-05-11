# File Input and Output

文件输入输出

World Machine worlds only describe a set of operations to create the terrain rather than the terrain itself. The action of importing or exporting a terrain is described by adding device nodes to the world

World Machine 世界只描述了一组创建地形的操作，而不是地形本身。 通过向世界添加设备节点来描述导入或导出地形的动作

## *File Output* *文件输出*

Saving a file to disk is a simple but important part of building your world. Exporting a file is done by using an Output Node to save terrain (or other data) to disk. There are several types of output possible, including terrain heightfields, meshes, and bitmaps. You can output many files from an individual world. For example, from a single project file you could save a terrain heightfield, a texture map to apply to the heightfield, and several additional masks for further use (perhaps in placing vegetation or other purposes).

将文件保存到磁盘是构建您的世界的一个简单但重要的部分。 导出文件是通过使用输出节点将地形（或其他数据）保存到磁盘来完成的。 有几种可能的输出类型，包括地形高度场、网格和位图。 您可以从一个单独的世界输出许多文件。 例如，从一个项目文件中，您可以保存一个地形高度场、一个应用于高度场的纹理贴图，以及几个额外的遮罩以供进一步使用（可能用于放置植被或其他目的）。

To export data from World Machine, you must place an appropriate Output node from the toolbar into the world and wire your final terrain data into that node.

要从 World Machine 导出数据，您必须将工具栏中的适当输出节点放置到世界中，并将最终地形数据连接到该节点。

![img](.\Image\Output-toolbar.png)

Note: the area exported will always be the currently selected Render Extents!

注意：导出的区域将始终是当前选择的渲染范围！

### **Heightfields** **高度场**

To export a terrain heightfield, use the default File Output node that the starting world includes, or place a new File Output node into the world from the toolbar.

要导出地形高度场，请使用起始世界包含的默认文件输出节点，或从工具栏将新的文件输出节点放置到世界中。

![img](.\Image\Heightfield-File-Output.png)

You can export in many different formats, as seen above. Your choice of what format to use will be governed by the needs of your rendering software, terrain engine, or other further terrain application.

如上所示，您可以导出多种不同的格式。 您选择使用哪种格式将取决于您的渲染软件、地形引擎或其他进一步的地形应用程序的需求。

The basic sequence of steps are:

基本的步骤顺序是：

1. Select the file format you wish to export

   选择您要导出的文件格式

2. Set the filename by pushing the “Set” button and providing a filename 3. Push the “Write output to disk!” button to export the file.

   通过按下“设置”按钮并提供文件名来设置文件名 3. 按下“将输出写入磁盘！” 按钮导出文件。

For more details on the various other options available in the File Output dialog, see the Device Reference.

有关“文件输出”对话框中可用的各种其他选项的更多详细信息，请参阅设备参考。

### **Terrain Meshes** **地形网格**

The Mesh Output creates a triangulated mesh from the input heightfield. This is intended for general purpose rendering software or other applications that cannot use a Heightfield; The heightfield should be the preferred output method as it is a much more compact and efficient way of storing terrain data.

网格输出从输入高度场创建一个三角网格。 这适用于通用渲染软件或其他不能使用 Heightfield 的应用程序； 高度场应该是首选的输出方法，因为它是一种更紧凑、更有效的存储地形数据的方法。

![img](.\Image\Mesh-output.png)

The same three steps described in 6.1.1 are used to export a mesh, and indeed any of the file output devices.

6.1.1 中描述的相同三个步骤用于导出网格，实际上是任何文件输出设备。

### **Bitmaps** **位图**

To export a bitmap, use the Bitmap Output device. This device accepts a bitmap datatype and an optional heightfield you can use to specify a 4th channel for alpha info.

要导出位图，请使用位图输出设备。 该设备接受一个位图数据类型和一个可选的高度域，您可以使用它来为 alpha 信息指定第 4 个通道。

![img](.\Image\Bitmap-Output-properties.png)

Export Formats: 导出格式：

● **8bit Windows BMP** ● **16bit TIFF, PNG** The same three steps apply: Set a file format, set a filename, and click “Write output to disk”.

**8bit Windows BMP** ● **16bit TIFF, PNG** 同样三步：设置文件格式，设置文件名，点击“Write output to disk”。

## *File Input* *文件输入*

![img](.\Image\File-input.png)

To import an existing file, use the File Input device. It can import a variety of file formats and brings them into the device world as either terrain heightfields or color bitmaps. The File Input is found under Generator Devices.

要导入现有文件，请使用文件输入设备。 它可以导入各种文件格式，并将它们作为地形高度场或彩色位图带入设备世界。 文件输入位于生成器设备下。

For more information on the various options available in the File Input dialog, see the Device Reference. The most important ones will be described below.

有关“文件输入”对话框中可用的各种选项的更多信息，请参阅设备参考。 最重要的将在下面描述。

**Loading your file from disk** Click on the “Load” button to browse to and select your input file. Once you’ve done so, WM will load it from disk; check to ensure that the “Original Size” readout matches what you expect. If you want to import a file as a Bitmap rather than a Heightfield, make sure that “Interpret as RGB” is checked.

**从磁盘加载文件** 单击“加载”按钮浏览并选择您的输入文件。 完成后，WM 将从磁盘加载它； 检查以确保“原始尺寸”读数符合您的预期。 如果您想将文件导入为位图而不是高度场，请确保选中“解释为 RGB”。

**Locating your file in the world** It’s very important to understand the relationship between your imported file, the world, and the area being viewed or exported. You can use file inputs for a great many things, from importing very large, rough guide maps that will be refined further in World Machine, to importing specific small features.

**在世界中定位您的文件** 了解您导入的文件、世界以及正在查看或导出的区域之间的关系非常重要。 您可以将文件输入用于很多事情，从导入将在 World Machine 中进一步完善的非常大的粗略指南地图，到导入特定的小功能。

When you import a file, you also specify its location in world space via the options in the “World Placement” section.

导入文件时，您还可以通过“World Placement”部分中的选项指定其在世界空间中的位置。

![img](.\Image\File-input-example.png)

The above view shows how this file input imports to a particular area of the world, which only partially overlaps with the current render extents (the white box). You can either set the worldspace location numerically, or use one of the provided quick placement buttons to place the location of the file into the current render extents. You may also set the extents graphically by clicking the “Set in Layout…” button.

上面的视图显示了此文件输入如何导入到世界的特定区域，该区域仅与当前渲染范围（白框）部分重叠。 您可以以数字方式设置世界空间位置，或使用提供的快速放置按钮之一将文件位置放置到当前渲染范围内。 您还可以通过单击“在布局中设置...”按钮以图形方式设置范围。

**Setting your file’s elevations** There are several ways you can map the file’s elevations into the world:

**设置文件的海拔高度** 您可以通过多种方式将文件的海拔高度映射到世界中：

● **Natural Elevations**: Ensure that the height values in the input file are translated correctly into the same elevation in World Machine

**自然高程**：确保输入文件中的高度值正确转换为 World Machine 中的相同高程

● **Full Range**: Map the elevations present in the file so that the highest and lowest elevation completely span the possible elevation range inside of World Machine

**全范围**：映射文件中存在的高程，使最高和最低高程完全跨越 World Machine 内部可能的高程范围

● **Specify**: Specify an altitude range in meters that the input data should fall between.

**指定**：以米为单位指定输入数据应位于的高度范围。

After the mapping of height values, any heights out of range will be clipped to the minimum and maximum altitudes allowed.

高度值映射后，任何超出范围的高度都将被裁剪为允许的最小和最大高度。

You should now have all of the knowledge you need to be able to bring existing terrains into World Machine, operate on them, and export to a file. There is one more file input device, called the Tiled Input Device. It is designed to work on sets of individual tiles that collectively define a terrain region. As a professional-edition only feature, it is described in the Pro Addendum of Chapter 10.

您现在应该拥有将现有地形导入 World Machine、对其进行操作并导出到文件所需的所有知识。 还有一种文件输入设备，称为平铺输入设备。 它旨在处理共同定义地形区域的一组单独的图块。 作为专业版独有的功能，它在第 10 章的专业版附录中进行了描述。