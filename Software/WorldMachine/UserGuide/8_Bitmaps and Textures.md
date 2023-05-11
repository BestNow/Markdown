# Bitmaps and Textures

位图和纹理

World Machine has the ability to work with bitmaps and textures. Conceptually, a bitmap consists of 3 color channels (Red, Green, Blue). These color channels can be manipulated together, or split apart and processed on a per-channel basis as if they were heightfields.

World Machine 能够处理位图和纹理。 从概念上讲，位图由 3 个颜色通道（红色、绿色、蓝色）组成。 这些颜色通道可以一起操作，或者分开并在每个通道的基础上进行处理，就好像它们是高度场一样。

![img](.\Image\Bitmap.png)

Most devices in World Machine only operate on heightfields. However, some will work on both heightfields and bitmaps, and a few are designed for bitmaps alone. You can see Bitmap-only devices by using the Filter by Type option on the Tools tab of the toolbar.

World Machine 中的大多数设备仅在高度场上运行。 然而，有些可以同时用于高度场和位图，还有一些是专为位图设计的。 您可以使用工具栏“工具”选项卡上的“按类型过滤”选项查看仅位图设备。

![img](.\Image\Filter-by-data-type.png)

The RGB tab on the toolbar then displays all compatible devices:

然后工具栏上的 RGB 选项卡显示所有兼容设备：

![img](.\Image\bitmap-toolbar-768x36.png)

## *Creating Color* *创造颜色*

The simplest way to produce color is using the Color Generator device:

产生颜色的最简单方法是使用颜色生成器设备：

![img](.\Image\Color-Generator.png)

It produces a single color of your choice. By combining several colors via a Chooser or Combiner device and Chooser masks, you can achieve many different blending possibilities for texturing.

它会产生您选择的单一颜色。 通过选择器或组合器设备和选择器蒙版组合多种颜色，您可以实现许多不同的纹理混合可能性。

![img](.\Image\Example-Selector-Devices.png)

In the example network above, several Selector devices (purple) are being used to pick out various regions of the terrain (such as high slopes, low elevation, and so on), and then merge together various colors based upon that.

在上面的示例网络中，几个 Selector 设备（紫色）被用来挑选地形的各个区域（例如高坡度、低海拔等），然后根据这些区域将各种颜色合并在一起。

There are additional methods you can use to create colors. For example, you can import a tiled texture by using a File Input device and setting an appropriate scale and tiling behavior, as shown below:

您可以使用其他方法来创建颜色。 例如，您可以通过使用文件输入设备并设置适当的比例和平铺行为来导入平铺纹理，如下所示：

![img](.\Image\Color-File-upload-example.png)

Which overlayed atop the terrain would look like the below:

覆盖在地形之上的将如下所示：

![img](.\Image\Color-File-Result-example.png)

Of course, once the texture is imported into the world, it can be combined with other textures and colors as much as you want, to produce very rich and complex texture maps.

当然，一旦纹理导入到世界中，它就可以根据需要与其他纹理和颜色组合，产生非常丰富和复杂的纹理贴图。

## *Working with Color Channels* *使用颜色通道*

You can combine several heightfields together with a channel combiner to create a single bitmap data packet.

您可以将多个高度场与通道组合器组合在一起以创建单个位图数据包。

![img](.\Image\Working-with-Color-Channels.png)

If you want to use a heightfield operator that doesn’t support bitmaps (such as the Expander device), you can break apart the bitmap into either RGB or HSL channels, operate on one or all of the channels, and then recombine them using a Channel Combiner.

如果您想使用不支持位图的高度场运算符（例如 Expander 设备），您可以将位图分解为 RGB 或 HSL 通道，对一个或所有通道进行操作，然后使用 通道组合器。

## *Overlaying Bitmaps atop a Terrain* *在地形上叠加位图*

If you want to view a bitmap or texture atop a terrain, you can use the Overlay View device to combine the two for display.

如果要查看地形上的位图或纹理，可以使用叠加视图设备将两者结合起来进行显示。

![img](.\Image\Overlay-View-Properties.png)

By creating your texture from mask data derived from the terrain, you can create realistic (or completely stylized) texturing for further export.

通过从源自地形的蒙版数据创建纹理，您可以创建逼真的（或完全程式化的）纹理以供进一步导出。

![img](.\Image\Bitmaps-on-top-of-Terrain-Example.png)

The example above uses some simple elevation and slope-based texturing, along with the flow map output from the Erosion device to create the “snail-trail” watercourse effect.

上面的示例使用了一些简单的基于高程和坡度的纹理，以及从侵蚀设备输出的流量图来创建“蜗牛径”水道效果。

## *Specialty Devices* *特殊设备*

There are two special purpose devices available that produce RGB output as well: A Light-map Maker and a Normal-map Maker.

有两种专用设备也可以产生 RGB 输出：Light-map Maker 和 Normal-map Maker。

### **Light-map Maker**  **光照贴图制作工具**

 ![img](.\Image\Light-Map-Maker.png)

The Light-map Maker is found under the Converters devices and creates a greyscale or colored lighting map from a source terrain.

Light-map Maker 位于 Converters 设备下，可从源地形创建灰度或彩色光照贴图。

### **Normal-map Maker** **法线贴图制作器**

![img](.\Image\Normal-Map-Generator.png)

The normal-map maker is found under Converters devices and encodes the terrain normal into an RGB texture; each direction component of the normal is mapped to a color; (R=X, G=Y, B=Z) is the default encoding. This information can be then used over a low-resolution mesh, giving much of the feel of a high resolution terrain with a fraction of the geometry data

法线贴图制作器位于 Converters devices 下，可将地形法线编码为 RGB 纹理； 法线的每个方向分量都映射到一种颜色； (R=X, G=Y, B=Z) 是默认编码。 然后可以在低分辨率网格上使用此信息，用一小部分几何数据给出高分辨率地形的大部分感觉