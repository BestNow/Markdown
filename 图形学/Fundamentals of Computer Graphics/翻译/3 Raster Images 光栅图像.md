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