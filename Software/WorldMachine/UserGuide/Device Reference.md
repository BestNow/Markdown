# Advanced Perlin Noise

Advanced Perlin Noise is a highly customizable fractal terrain generator based upon the basic fractal noise techniques pioneered by Ken Perlin.

 
Perlin Noise works by layering multiple sets of blobby-looking noise patterns together. These layers are called octaves. The multiple octaves are combined together in a variety of ways to create the final result. Advanced Perlin Noise gives you total control over the types of noise used in each layer, as well as how they are combined. This allows you to create some very unique terrain shapes. 

## Device Parameters

**Feature Scale**

Controls the density of features of the terrain. 
Feature Size roughly corresponds to the distance between major peaks or valleys. Small values produce quickly changing terrain, suitable for hills or lumps, while middle values are ideal for mountains. Large values allow continents and other shapes that are created on a massive scale.



**Style**

Change the type of fractal noise that is produced.

| **Basic:**              | Classic Perlin Noise. The resulting terrain looks something like very rough, jagged mountain terrain. |
| ----------------------- | ------------------------------------------------------------ |
| **Ridged:**             | Ridged Perlin has a very different character. Sharp discontinuities are laced throughout the terrain at all scales; these can look like ridges and spines in the terrain. |
| **Billowy:**            | The inverse of Ridged Perlin, the Billowy style produces terrain that has a lumpy appearance with sharp depressed creases throughout. |
| **Smooth Ridged:**      | Smooth Ridged style is similar to the Ridged style but has a smooth top to the ridges instead of sharp ridges. |
| **Smooth Billowy:**     | Smooth Billowy has lumpy shapes that have smooth creases throughout. |
| **Sharp Ridged:**       | Sharp Ridged is like the Ridged style but has even steeper walls than the regular Ridged style. |
| **Flat Middle:**        | As the name implies, this style uses a shape that has a flattened middle area, providing a broad band of smooth terrain shapes with steep peaks and valleys. |
| **Terraced:**           | The terraced style has a sharp drop in the middle altitude region. When layered together, it etches these drops all across the terrain. |
| **Stephen’s Choice 1:** | A multifractal variant created by Stephen Schmitt, author of World Machine. It has large-scale ridges much like the ridged variant, but at smaller scales it takes on much of the character of the billowy variant. |



**Persistence**

Controls the degree to which the strength of each layer of noise is reduced as they are layered together. Low persistence values produce very smooth terrains, whereas increasing the persistence produces more detail (and spikiness). Unlike a low octaves value, all layers of noise are still calculated when using a low persistence, so that terrain features are smoothly introduced as the value is increased.



**Steepness**

Adjust the steepness of the grades in the terrain. Low values produce a flatter terrain; High values a steeper one.



**Middle elevation**

中位海拔



**Input**

|                                  |                    |
| -------------------------------- | ------------------ |
| shaping guide (height field)     | 整形导向器(高度场) |
| distortion guide (height field)  |                    |
| persistence guide (height field) |                    |



**Output**

|                             |                       |
| --------------------------- | --------------------- |
| Primary Output(Heightfield) | 主要输出(Heightfield) |



# Coast Erosion 海岸侵蚀

# Erosion 侵蚀

# Reach Character

为河流设备提供河流特征。