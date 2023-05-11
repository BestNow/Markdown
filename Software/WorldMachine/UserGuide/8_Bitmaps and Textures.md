# Bitmaps and Textures

World Machine has the ability to work with bitmaps and textures. Conceptually, a bitmap consists of 3 color channels (Red, Green, Blue). These color channels can be manipulated together, or split apart and processed on a per-channel basis as if they were heightfields.

![img](.\Image\Bitmap.png)

Most devices in World Machine only operate on heightfields. However, some will work on both heightfields and bitmaps, and a few are designed for bitmaps alone. You can see Bitmap-only devices by using the Filter by Type option on the Tools tab of the toolbar.

![img](.\Image\Filter-by-data-type.png)

The RGB tab on the toolbar then displays all compatible devices:

![img](.\Image\bitmap-toolbar-768x36.png)

## *Creating Color*

The simplest way to produce color is using the Color Generator device:

![img](.\Image\Color-Generator.png)

It produces a single color of your choice. By combining several colors via a Chooser or Combiner device and Chooser masks, you can achieve many different blending possibilities for texturing.

![img](.\Image\Example-Selector-Devices.png)

In the example network above, several Selector devices (purple) are being used to pick out various regions of the terrain (such as high slopes, low elevation, and so on), and then merge together various colors based upon that.

There are additional methods you can use to create colors. For example, you can import a tiled texture by using a File Input device and setting an appropriate scale and tiling behavior, as shown below:

![img](.\Image\Color-File-upload-example.png)

Which overlayed atop the terrain would look like the below:

![img](.\Image\Color-File-Result-example.png)

Of course, once the texture is imported into the world, it can be combined with other textures and colors as much as you want, to produce very rich and complex texture maps.

## *Working with Color Channels*

You can combine several heightfields together with a channel combiner to create a single bitmap data packet.

![img](.\Image\Working-with-Color-Channels.png)

If you want to use a heightfield operator that doesn’t support bitmaps (such as the Expander device), you can break apart the bitmap into either RGB or HSL channels, operate on one or all of the channels, and then recombine them using a Channel Combiner.

## *Overlaying Bitmaps atop a Terrain*

If you want to view a bitmap or texture atop a terrain, you can use the Overlay View device to combine the two for display.

![img](.\Image\Overlay-View-Properties.png)

By creating your texture from mask data derived from the terrain, you can create realistic (or completely stylized) texturing for further export.

![img](.\Image\Bitmaps-on-top-of-Terrain-Example.png)

The example above uses some simple elevation and slope-based texturing, along with the flow map output from the Erosion device to create the “snail-trail” watercourse effect.

## *Specialty Devices*

There are two special purpose devices available that produce RGB output as well: A Light-map Maker and a Normal-map Maker.

### **Light-map Maker**

 ![img](.\Image\Light-Map-Maker.png)

The Light-map Maker is found under the Converters devices and creates a greyscale or colored lighting map from a source terrain.

### **Normal-map Maker**

![img](.\Image\Normal-Map-Generator.png)

The normal-map maker is found under Converters devices and encodes the terrain normal into an RGB texture; each direction component of the normal is mapped to a color; (R=X, G=Y, B=Z) is the default encoding. This information can be then used over a low-resolution mesh, giving much of the feel of a high resolution terrain with a fraction of the geometry data