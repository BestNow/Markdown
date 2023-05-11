# Layout Generator

布局生成器

The Layout Generator is a graphical design tool that allows you to bridge the gap between fully procedural and fully artist-created terrains. With a Layout Generator, you have a suite of vector drawing tools that let you craft terrain areas, insert roads and rivers, draw regions of influence as effect masks, and much more.

布局生成器是一种图形设计工具，可让您弥合完全程序化和完全艺术家创建的地形之间的差距。 借助 Layout Generator，您拥有一套矢量绘图工具，可让您制作地形区域、插入道路和河流、绘制影响区域作为效果蒙版等等。

## *Layout Generator Basics* *布局生成器基础知识*

To create a Layout Generator, go to the Layout View:

要创建布局生成器，请转到布局视图：

![img](.\Image\Layout-View (1).png)

Click the **New Layout** button in the upper-left corner of the above photo. As you create layout generators, they will appear as tabs across the top of the view.

单击上图左上角的 **New Layout** 按钮。 当您创建布局生成器时，它们将显示为横跨视图顶部的选项卡。

When a layout is selected in the view, the screen will change to the Layout Editing mode, as you can see below:

当在视图中选择布局时，屏幕将更改为布局编辑模式，如下所示：

![img](.\Image\Layout-Editing-Mode.png)

A Layout Generator acts as a container for shapes. You can have many different layout generators. each one you create will show up as an associated device in the Device Workview. The output of the layout generator can then be used just like any other component in the workflow.

布局生成器充当形状的容器。 您可以有许多不同的布局生成器。 您创建的每个设备都将在设备工作视图中显示为关联设备。 然后可以像工作流中的任何其他组件一样使用布局生成器的输出。

Also, note that you can change the currently viewed output while editing a layout generator and its shapes. This ability lets you view the final output from farther down the device flow while working on a layout generator.

另请注意，您可以在编辑布局生成器及其形状时更改当前查看的输出。 此功能使您可以在布局生成器上工作时从设备流的更下方查看最终输出。

![img](.\Image\Mode-Buttons (1).png)

**Layout Generator Options** **布局生成器选项**

● **Rendering Mode:** This allows you to choose whether to create full detail or reduced-detail shapes. In most cases you will want to leave this set to “Accurate”, unless you are working with a layout containing a great number of shapes that is building extremely slowly.

**渲染模式：** 这允许您选择是创建完整细节还是减少细节的形状。 在大多数情况下，您希望将此设置保留为“准确”，除非您正在使用包含大量构建速度极慢的形状的布局。

● **Display as Mask:** Causes the output of the layout generator to be flagged as a mask rather than a terrain, and display as such. Useful when creating a layout that is intended to be used as a mask.

**显示为遮罩：** 将布局生成器的输出标记为遮罩而不是地形，并照此显示。 在创建打算用作遮罩的布局时很有用。

● **Use Breakup:** Enables fractal breakup on the shapes in the layout. This allows you to add more natural-looking profiles to your basic geometric shapes. See section 5.4 for details.

**使用分解：** 对布局中的形状启用分形分解。 这使您可以为基本几何形状添加外观更自然的轮廓。 详见第 5.4 节。

● **Invert Values:** inverts all height values of the layout. Useful when creating masks, as well as things like canyons and other terrain where you’ll be removing rather than adding things.

**反转值：**反转布局的所有高度值。 在创建蒙版以及峡谷和其他您将要移除而不是添加内容的地形时很有用。

● **Shape List Button:** brings up a dialog that lists all shapes contained within the current layout generator. Clicking on a shape in the list will select it, allowing you to locate and manage many shapes.

**形状列表按钮：** 弹出一个对话框，其中列出了当前布局生成器中包含的所有形状。 单击列表中的一个形状会将其选中，这样您就可以定位和管理多个形状。

● **File Button:** Imports or exports shapes. See the Shape I/O section below for more information.

**文件按钮：**导入或导出形状。 有关详细信息，请参阅下面的形状 I/O 部分。

## *Creating and using Layout Shapes* *创建和使用布局形状*

On the left is the Shape Library, where you can access the various shapes available for you to draw. To create a new shape, simply select the variety you desire from the libray, and click-drag in the terrain area. All shapes are created in a similar way, although some allow you more flexibility during shape creation. For example, polygon and path shapes can be either sketched or plotted more precisely by clicking individual vertices rather than dragging.

左侧是形状库，您可以在其中访问可供您绘制的各种形状。 要创建新形状，只需从库中选择所需的种类，然后在地形区域中单击并拖动即可。 所有形状都以类似的方式创建，尽管有些形状在创建过程中允许您更加灵活。 例如，可以通过单击各个顶点而不是拖动来更精确地绘制或绘制多边形和路径形状。

![img](.\Image\Creating-Shapes-768x569.png)

Note that around each created shape there is a “transition zone”, where the shape’s influence fades away to the background. When multiple shapes overlap, the one with the greatest height governs. You can also choose to set a shape to Subtractive mode, in which case it will be subtracted from all of the positive shapes at that same point.

请注意，在每个创建的形状周围都有一个“过渡区”，形状的影响会逐渐消失到背景中。 当多个形状重叠时，以高度最大的那个为准。 您还可以选择将形状设置为减法模式，在这种情况下，将从同一点的所有正形状中减去该形状。

![img](.\Image\Moving-Shapes-768x569.png)

Shapes can be selected by left-clicking on them. Multiple shapes can be either drag-selected using the selection marquee, or added to the selection individually by holding down shift while clicking on new shapes.

可以通过左键单击来选择形状。 可以使用选择框拖动选择多个形状，也可以通过在单击新形状的同时按住 Shift 键将其单独添加到选择中。

**Shape Properties** Once a shape has been created, you can bring up a shape’s properties by double-clicking on it: All shapes have several properties in common that can be edited.

**形状属性** 创建形状后，您可以通过双击它来调出形状的属性：所有形状都有几个可以编辑的共同属性。

![img](.\Image\Shape-Properties.png)

● **Default Value:** Controls the height value of the shape

**默认值：** 控制形状的高度值

● **Opacity:** The power of this shape versus the background. Low opacity values allow background heights to show through.

**不透明度：**此形状相对于背景的强度。 低不透明度值允许显示背景高度。

● **Falloff distance:** the distance between the border of the shape and the region in which the shape has no influence on the terrain.

**衰减距离：**形状边界与形状对地形没有影响的区域之间的距离。

● **Falloff type:** Many shapes allow you to how you wish the falloff zone to be defined:

**衰减类型：** 许多形状允许您定义衰减区域：

○ **Exterior falloff** means that the shape is full strength to the border, and then falls away on the outside of the shape.

**Exterior falloff** 表示形状对边界充满力量，然后在形状的外侧消失。

○ **Interior falloff** means the shape’s falloff occurs inside of the shape, reaching no influence at the border of the shape.

**Interior falloff** 表示形状的衰减发生在形状的内部，在形状的边界处没有影响。

● **Operation:** Shapes may be positive or negative. A negative shape is subtracted away from other existing shapes.

**操作：** 形状可正可负。 从其他现有形状中减去负形状。

● **Shape Falloff function:** you can select from a variety of preset falloff functions.

**形状衰减功能：**您可以从多种预设衰减功能中进行选择。

○ **Linear falloff** provides an even gradient to the falloff.

​	**线性衰减** 为衰减提供均匀的梯度。

○ **Squared falloff** provides gentle lower regions and a sharp ridge on top.

​	**方形衰减** 提供平缓的较低区域和顶部的尖锐脊线。

○ **Square root falloff** provides a gentle top transition and steep lower areas

​	**平方根衰减**提供平缓的顶部过渡和陡峭的较低区域

○ **S-falloff** provides smooth falloff on both the top and bottom of the shape.

​	**S-falloff** 在形状的顶部和底部提供平滑的衰减。

○ **Custom falloff** allows you to define a custom falloff function, which can be very useful for among other things, defining road and river profiles.

​	**自定义衰减** 允许您定义自定义衰减函数，这对于定义道路和河流剖面等非常有用。

● **Falloff Fader:** Llets you control how much influence the falloff function chosen above has on the falloff curve. A value of 0% will always give you a linear falloff gradient, while 100% means that you are using the chosen function.

​	**Falloff Fader：** 让您控制上面选择的衰减函数对衰减曲线的影响程度。 0% 的值将始终为您提供线性衰减梯度，而 100% 表示您正在使用所选函数。

● **Shape Breakup Participation:** Controls the extent to which this shape is effected by the Layout Generator’s fractal breakup setting.

​	**Shape Breakup Partication：**控制此形状受布局生成器的分形分解设置影响的程度。

### **Transforming Shapes** **变换形状**

Dragging a selected shape will move the shape in the direction you drag. Right-clicking brings up the a context menu for the selected shapes:

拖动选定的形状会沿您拖动的方向移动该形状。 右键单击会弹出所选形状的上下文菜单：

![img](.\Image\Transforming-Shapes.png)

All shapes support at least some transformation options. These allow you to translate, rotate, or scale the selected shapes. Simply select the transformation option you want (or use the Hotkey for it from the the Layout View) and drag in the viewport to perform the action. Clicking without dragging will end the transformation mode.

所有形状至少支持一些转换选项。 这些允许您平移、旋转或缩放选定的形状。 只需选择您想要的变换选项（或使用布局视图中的热键）并在视口中拖动即可执行操作。 单击而不拖动将结束转换模式。

**Transformation Center** Holding down shift or ctrl while rotating or scaling will perform each action around the shape’s own origin rather than the center-point of the group. The graphic below illustrates the difference:

**变换中心** 在旋转或缩放时按住 shift 或 ctrl 将围绕形状自身的原点而不是组的中心点执行每个动作。 下图说明了差异：

![img](.\Image\Transformation-Center.png)

Shapes can also be copied or pasted by selecting the appropriate option from the edit menu, or using the standard CTRL-X, CTRL-C, CTRL-V shortcut keys.

也可以通过从编辑菜单中选择适当的选项，或使用标准的 CTRL-X、CTRL-C、CTRL-V 快捷键来复制或粘贴形状。

### **Other shape options** **其他形状选项**

![img](.\Image\Other-Shape-Options.png)

● **Enable/Disable Shape:** if a shape is disabled, it no longer effects the world in any way.

**启用/禁用形状：**如果形状被禁用，它不再以任何方式影响世界。

● **Lock Shape:** make the shape unchangable until this is selected again. Use this to prevent accident modification of important shapes.

**锁定形状：**使形状不可改变，直到再次选择。 使用它来防止重要形状的意外修改。

● **Delete Shape:** As you might expect, this deletes the currently selected shape(s)!

**删除形状：**如您所料，这将删除当前选定的形状！

● **Bring to Front/Send to Back:** Moves the selected shapes forward or backward in the Z order. This has no effect on output, but allows you to change which shape is selected first between overlapping shapes.

**置于顶层/置于底层：** 在 Z 顺序中向前或向后移动选定的形状。 这对输出没有影响，但允许您更改重叠形状之间首先选择的形状。

## *Vertex-based shape options* *基于顶点的形状选项*

The polygon and path tools are defined by a sequence of vertices. There are some additional editing options available for vertex based shapes.

多边形和路径工具由一系列顶点定义。 有一些额外的编辑选项可用于基于顶点的形状。

![img](.\Image\Vertex-based-Shape-Options.png)

### **Bezier Shapes** **贝塞尔曲线形状**

Vertex-based shapes support bezier splines for smoothly interpolating between each vertex. This is slower to process but is often highly desireable to create smooth and complex geometry. You can convert between linear and bezier curve segments by checking or unchecking the “Use Bezier Path” option in the right-click context menu for that shape.

基于顶点的形状支持贝塞尔样条曲线，以便在每个顶点之间进行平滑插值。 这处理起来较慢，但通常非常需要创建平滑和复杂的几何体。 您可以通过选中或取消选中该形状的右键单击上下文菜单中的“使用贝塞尔路径”选项，在线性和贝塞尔曲线段之间进行转换。

If a shape has bezier curves enabled, the shape will have additional handles available representing the bezier control points for the curve.

如果形状启用了贝塞尔曲线，则该形状将有额外的手柄可用，代表曲线的贝塞尔控制点。

![img](.\Image\Bezier-Shapes.png)

By default, the handles on either side of a vertex are linked together to provide a smooth transition through that vertex, but you can override this behavior by holding down **shift** wile dragging a bezier handle. In addition, you can set all of the bezier handles in a shape at once to provide a smooth shape by selecting the “Perform Curve Smoothing” option from the context menu.

默认情况下，顶点两侧的手柄链接在一起以提供通过该顶点的平滑过渡，但您可以通过按住 **shift** 并拖动贝塞尔手柄来覆盖此行为。 此外，您可以通过从上下文菜单中选择“执行曲线平滑”选项，一次设置一个形状中的所有贝塞尔曲线图柄以提供平滑的形状。

### **Vertex Editing** **顶点编辑**

Vertices have their own context menu that you access by right-clicking on a specific vertex. This allows you to set some of their properties directly.

顶点有自己的上下文菜单，您可以通过右键单击特定顶点来访问该菜单。 这允许您直接设置它们的一些属性。

![img](.\Image\Vertix-Editing.png)

![img](.\Image\Precise-Value.png)

● **Enter Precise Value:** This option allows you to enter specific numbers for the (X,Y) coordinate of the vertex and its elevation value.

**输入精确值：**此选项允许您为顶点的(X,Y) 坐标及其高程值输入特定数字。

● **Value Key-Point:** Toggle whether the selected vertex is interpolated or whether it is a “keyframe” that has its value set manually.

**Value Key-Point：** 切换所选顶点是插值还是手动设置值的“关键帧”。

● **Delete Vertex:** Removes the vertex from the shape, connecting the two vertices on either side together.

**删除顶点：**从形状中删除顶点，将任一侧的两个顶点连接在一起。

● **Subdivide Vertex:** Inserts two new vertices adjacent to the selected vertex.

**细分顶点：**插入两个与选定顶点相邻的新顶点。

● **Break Vertex Welds**: Break any welds that involve the selected vertex.

**打断顶点焊缝**：打断任何涉及选定顶点的焊缝。

In addition, there is a quick shortcut for setting shape heights on a per-vertex basis. Right-click on a vertex and without releasing the mouse button, drag up or down to quickly set the height value of that point.

此外，还有一个快速快捷方式可以在每个顶点的基础上设置形状高度。 右击一个顶点，在不松开鼠标键的情况下，向上或向下拖动以快速设置该点的高度值。

![img](.\Image\Setting-shape-heights.png)

### **Vertex Welding** **顶点焊接**

You can weld together vertices that occur on different shapes. Welded vertices will always occupy the same position in space, allowing you to link several shapes together in, for example, a road or river. To weld together vertices, simply drag one vertex over another. The cursor will highlight to show the potential welding action.

您可以将出现在不同形状上的顶点焊接在一起。 焊接顶点将始终占据空间中的相同位置，允许您将多个形状连接在一起，例如，道路或河流。 要将顶点焊接在一起，只需将一个顶点拖到另一个顶点上即可。 光标将突出显示潜在的焊接操作。

![img](.\Image\Vertex-Welding.png)

After welding, any transformations performed on one shape that effect that vertex will also move the linked vertex in the other shape(s).

焊接后，对影响该顶点的一个形状执行的任何变换也将移动其他形状中的链接顶点。

If you decide later that you wish to break the weld, simply select the vertex or shape in question and right-click to bring up the context menu, and select “Break Weld”

如果您稍后决定要打断焊缝，只需选择有问题的顶点或形状，然后右键单击以调出上下文菜单，然后选择“打断焊缝”

## *Fractal Breakup* *分形分解*

Fractal Breakup allows you to distort the unnaturally straight edges often produced by the geometric primitives. This is often desirable when creating natural shapes.

Fractal Breakup 允许您扭曲通常由几何图元产生的不自然的直边。 这在创建自然形状时通常是可取的。

![img](.\Image\Fractal-Breakup.png)

Fractal Breakup must be enabled on a per-layout basis when you want to use it. However, you can decide on a per-shape basis which shapes are distorted by changing that Shape’s “Fractal Breakup Participation” value.

当您想要使用分形分解时，必须在每个布局的基础上启用它。 但是，您可以在每个形状的基础上通过更改该形状的“Fractal Breakup Participation”值来决定哪些形状被扭曲。

You can change the scale and intensity of the breakup effect by editing the Fractal Breakup properties:

您可以通过编辑 Fractal Breakup 属性来更改分解效果的比例和强度：

![img](.\Image\Fractal-Breakup-Properties.png)

● Fractal Breakup: The intensity of the effect. Lower values provide a more subtle distortion.

Fractal Breakup：效果的强度。 较低的值提供更细微的失真。

● Breakup Scale: The distance that the distortion effect is applied for. Large values will produce slowly varying but large amplitude variations, while low values produce more of a ripple effect. ● Roughness: The complexity of the edge. This number corresponds to the number of octaves of fractal noise to be applied.

Breakup Scale：应用失真效果的距离。 大值会产生缓慢变化但幅度很大的变化，而低值会产生更多的连锁反应。 ● 粗糙度：边缘的复杂程度。 该数字对应于要应用的分形噪声的倍频程数。

## *Sourcing vs. Modifying terrain with a Layout Generator* *采购与使用布局生成器修改地形*



You can use the Layout Generator in your world in two different ways.

您可以通过两种不同的方式在您的世界中使用布局生成器。

![img](.\Image\Sourcing-vs.-Modifying.png)

1. Use the Layout Generator as a Generator, creating terrain or mask information to be wired to a different device in the world.

   将布局生成器用作生成器，创建地形或遮罩信息以连接到世界上的不同设备。

2. Use the Layout Generator to modify an existing terrain by connecting that terrain into the Primary input port on the LG.

   通过将地形连接到 LG 上的主输入端口，使用布局生成器修改现有地形。

**Deciding on the type of connection to use** You should use the Layout Generator as a source of terrain when you want to generate guide shapes for a fractal generator or a mask for a particular effect. The image below shows the result of connecting the output of a Layout Generator to a Perlin Noise device:

**决定要使用的连接类型** 当您想要为分形生成器生成引导形状或为特定效果生成遮罩时，您应该使用布局生成器作为地形来源。 下图显示了将 Layout Generator 的输出连接到 Perlin Noise 设备的结果：

![img](.\Image\Deciding-on-the-type-of-connection-to-use.png)

On the other hand, you should use the Layout Generator to modify the terrain when you want to **embed** shapes into the terrain.

另一方面，当您想要将形状**嵌入**地形时，您应该使用布局生成器来修改地形。

![img](.\Image\Modifying-Terrain-with-Layout-Generator.png)

For example, leveling areas to a certain height, creating a road that cuts/fills through an existing terrain, or inserting waterways.

例如，将区域平整到一定高度，创建一条切割/填充现有地形的道路，或插入水道。

## *Importing and Exporting Shapes* *导入和导出形状*

You can import or export shapes with one of several vector-graphics art formats. In particular, the SVG and AI formats are supported.

您可以导入或导出具有多种矢量图形艺术格式之一的形状。 特别是支持 SVG 和 AI 格式。

![img](.\Image\Importing-Shapes.png)

**Import Scaling** How to scale the raw coordinates is the most important decision when moving shapes to and from World Machine. You can have WM treat the file coordinates as meters, kilometers, a custom scale factor. A display shows you the current region to be exported to a file.

**导入缩放** 在将形状移入和移出 World Machine 时，如何缩放原始坐标是最重要的决定。 您可以让 WM 将文件坐标视为米、千米、自定义比例因子。 显示屏会向您显示要导出到文件的当前区域。

You can also choose to flip the Y-axis of all of the imported shapes; this is useful when interacting with a program that measures from an origin in the top-left corner instead of the bottom-left system that World Machine uses.

您还可以选择翻转所有导入形状的 Y 轴； 这在与从左上角的原点而不是 World Machine 使用的左下角系统进行测量的程序交互时很有用。

Note that there are some serious limitations in what information can be imported or exported; any per-vertex data you have set will be lost, and World-Machine specific shape information also will not transfer. Nonetheless it can be very useful to be able to re-use vector data from other sources or export the exact paths of splines to the next stage in your production pipeline.

请注意，可以导入或导出的信息有一些严重的限制； 您设置的任何逐顶点数据都将丢失，并且 World-Machine 特定的形状信息也不会传输。 尽管如此，能够重新使用来自其他来源的矢量数据或将样条曲线的确切路径导出到生产管道的下一阶段可能非常有用。

## *Curve Editor* *曲线编辑器*

Layout View contains a curve editor to allow you to define custom falloff profiles for shapes as well as view the elevation profile of a vertex based shape.

布局视图包含一个曲线编辑器，允许您为形状定义自定义衰减配置文件以及查看基于顶点的形状的高程配置文件。

![img](.\Image\Curve-editor.png)

The horizontal axis shows the distance along the curve, while the vertical axis shows elevation. The curve editor works in one of several modes depending on what you’re editing; when modifying a falloff curve, you can freely add new knots to the curve. When editing a lofting curve (heights along a path), the knots are fixed in position and can only be changed in height. These two modes of operating are reflected in the **Editing Method**:

横轴表示沿曲线的距离，而纵轴表示海拔。 曲线编辑器根据您正在编辑的内容以多种模式之一工作； 修改衰减曲线时，您可以在曲线上自由添加新的节点。 编辑放样曲线（沿路径的高度）时，节点的位置是固定的，只能改变高度。 这两种操作方式体现在**编辑方法**中：

● Vertex mode allows you to add or delete vertices, and move them horizontally

顶点模式允许您添加或删除顶点，并水平移动它们

● Modify mode allows you to change the height of existing points only

修改模式允许您仅更改现有点的高度

Lastly, you can load and save preset falloff curves so that you can re-use particular profiles among layouts or projects.

最后，您可以加载和保存预设衰减曲线，以便您可以在布局或项目中重复使用特定的配置文件。