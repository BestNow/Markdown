# 12  Data Structures for Graphics 图形数据结构

Certain data structures seem to pop up repeatedly in graphics applications, perhaps because they address fundamental underlying ideas like surfaces, space, and scene structure. This chapter talks about several basic and unrelated categories of data structures that are among the most common and useful: mesh structures, spatial data structures, scene graphs, and tiled multidimensional arrays. 
某些数据结构似乎在图形应用程序中反复出现，也许是因为它们解决了表面、空间和场景结构等基本概念。 本章讨论最常见和最有用的数据结构的几个基本且不相关的类别：网格结构、空间数据结构、场景图和平铺多维数组。

For meshes, we discuss the basic storage schemes used for storing static meshes and for transferring meshes to graphics APIs. We also discuss the winged-edge data structure (Baumgart, 1974) and the related half-edge structure, which are useful for managing models where the tessellation changes, such as in subdivision or model simplification. Although these methods generalize to arbitrary polygon meshes, we focus on the simpler case of triangle meshes here. 
对于网格，我们讨论用于存储静态网格和将网格传输到图形 API 的基本存储方案。 我们还讨论了翼边数据结构（Baumgart，1974）和相关的半边结构，它们对于管理细分变化的模型很有用，例如在细分或模型简化中。 尽管这些方法可以推广到任意多边形网格，但我们在这里关注的是三角形网格的简单情况。

Next, the scene-graph data structure is presented. Various forms of this data structure are ubiquitous in graphics applications because they are so useful in managing objects and transformations. All new graphics APIs are designed to support scene graphs well. 
接下来，介绍场景图数据结构。 这种数据结构的各种形式在图形应用程序中无处不在，因为它们在管理对象和转换方面非常有用。 所有新的图形 API 都旨在很好地支持场景图。

For spatial data structures, we discuss three approaches to organizing models in 3D space—bounding volume hierarchies, hierarchical space subdivision, and uniform space subdivision—and the use of hierarchical space subdivision (BSP trees) for hidden surface removal. The same methods are also used for other purposes, including geometry culling and collision detection. 
对于空间数据结构，我们讨论了在 3D 空间中组织模型的三种方法——包围体层次结构、层次空间细分和均匀空间细分——以及使用层次空间细分（BSP 树）去除隐藏表面。 相同的方法也用于其他目的，包括几何剔除和碰撞检测。

Finally, the tiled multidimensional array is presented. Originally developed to help paging performance in applications where graphics data needed to be swapped in from disk, such structures are now crucial for memory locality on machines regardless of whether the array fits in main memory.
最后，给出了平铺的多维数组。 最初开发这种结构是为了帮助需要从磁盘换入图形数据的应用程序的分页性能，现在无论阵列是否适合主内存，这种结构对于机器上的内存局部性都至关重要。

## 12.1 Triangle Meshes 三角形网格

Most real-world models are composed of complexes of triangles with shared vertices. These are usually known as triangular meshes, triangle meshes, or triangular irregular networks (TINs), and handling them efficiently is crucial to the performance of many graphics programs. The kind of efficiency that is important depends on the application. Meshes are stored on disk and in memory, and we’d like to minimize the amount of storage consumed. When meshes are transmitted across networks or from the CPU to the graphics system, they consume bandwidth, which is often even more precious than storage. In applications that perform operations on meshes, besides simply storing and drawing them—such as subdivision, mesh editing, mesh compression, or other operations—efficient access to adjacency information is crucial. 
大多数现实世界的模型都是由具有共享顶点的三角形复合体组成。 这些通常称为三角形网格、三角形网格或不规则三角形网络 (TIN)，有效处理它们对于许多图形程序的性能至关重要。 效率的重要程度取决于应用。 网格存储在磁盘和内存中，我们希望最大限度地减少存储消耗。 当网格通过网络或从 CPU 传输到图形系统时，它们会消耗带宽，而带宽通常比存储更宝贵。 在对网格执行操作的应用程序中，除了简单地存储和绘制网格（例如细分、网格编辑、网格压缩或其他操作）之外，有效访问邻接信息也至关重要。

Triangle meshes are generally used to represent surfaces, so a mesh is not just a collection of unrelated triangles, but rather a network of triangles that connect to one another through shared vertices and edges to form a single continuous surface. This is a key insight about meshes: a mesh can be handled more efficiently than a collection of the same number of unrelated triangles. 
三角形网格通常用于表示曲面，因此网格不仅仅是不相关三角形的集合，而是通过共享顶点和边相互连接以形成单个连续曲面的三角形网络。 这是关于网格的一个关键见解：与相同数量的不相关三角形的集合相比，网格的处理效率更高。

The minimum information required for a triangle mesh is a set of triangles (triples of vertices) and the positions (in 3D space) of their vertices. But many, if not most, programs require the ability to store additional data at the vertices, edges, or faces to support texture mapping, shading, animation, and other operations. Vertex data is the most common: each vertex can have material parameters, texture coordinates, irradiances—any parameters whose values change across the surface. These parameters are then linearly interpolated across each triangle to define a continuous function over the whole surface of the mesh. However, it is also occasionally important to be able to store data per edge or per face.
三角形网格所需的最少信息是一组三角形（三个顶点）及其顶点的位置（在 3D 空间中）。 但许多（如果不是大多数）程序需要能够在顶点、边或面存储附加数据，以支持纹理映射、着色、动画和其他操作。 顶点数据是最常见的：每个顶点可以有材质参数、纹理坐标、辐照度——其值在表面上变化的任何参数。 然后，这些参数在每个三角形上进行线性插值，以在网格的整个表面上定义连续函数。 然而，有时能够存储每个边或每个面的数据也很重要。

### 12.1.1 Mesh Topology 网状拓扑

The idea that meshes are surface-like can be formalized as constraints on the mesh topology—the way the triangles connect together, without regard for the vertex positions. Many algorithms will only work, or are much easier to implement, on a mesh with predictable connectivity. The simplest and most restrictive requirement on the topology of a mesh is for the surface to be a manifold. A manifold mesh is “watertight”—it has no gaps and separates the space on the inside of the surface from the space outside. It also looks like a surface everywhere on the mesh.
网格类似于表面的想法可以形式化为对网格拓扑的约束——三角形连接在一起的方式，而不考虑顶点位置。 许多算法只能在具有可预测连接性的网格上工作，或者更容易实现。 对网格拓扑最简单且最具限制性的要求是表面是流形。 流形网格是“水密的”——它没有间隙，并将表面内部的空间与外部的空间分开。 它看起来也像网格上各处的表面。

> We’ll leave the precise definitions to the mathematicians; see the chapter notes.  
> 我们将把精确的定义留给数学家； 参见章节注释。

The term manifold comes from the mathematical field of topology: roughly speaking, a manifold (specifically a two-dimensional manifold, or 2-manifold) is  a surface in which a small neighborhood around any point could be smoothed out into a bit of flat surface. This idea is most clearly explained by counterexample: if an edge on a mesh has three triangles connected to it, the neighborhood of a point on the edge is different from the neighborhood of one of the points in the interior of one of the triangles, because it has an extra “fin” sticking out of it (Figure 12.1). If the edge has exactly two triangles attached to it, points on the edge have neighborhoods just like points in the interior, only with a crease down the middle. Similarly, if the triangles sharing a vertex are in a configuration like the left one in Figure 12.2, the neighborhood is like two pieces of surface glued together at the center, which can’t be flattened without doubling it up. The vertex with the simpler neighborhood shown at right is just fine.
术语流形来自拓扑学的数学领域：粗略地说，流形（特别是二维流形或 2 流形）是一个表面，其中任何点周围的小邻域都可以平滑为一点平坦的表面 。 这个想法可以通过反例得到最清楚的解释：如果网格上的一条边与三个三角形相连，则该边上的点的邻域与其中一个三角形内部的点的邻域不同，因为 它有一个额外的“鳍”伸出（图12.1）。 如果边缘恰好连接有两个三角形，则边缘上的点具有与内部点一样的邻域，只是中间有一条折痕。 类似地，如果共享一个顶点的三角形处于如图 12.2 中左侧所示的配置，则邻域就像在中心粘合在一起的两块表面，如果不将其折叠起来就无法展平。 右侧显示的具有更简单邻域的顶点就很好。
![Figure 12.1](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.1.png)
Figure 12.1. Non-manifold (left) and manifold (right) interior edges.
图 12.1。 非歧管（左）和歧管（右）内边缘。
![Figure 12.2](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.2.png)
Figure 12.2. Non-manifold (left) and manifold (right) interior vertices.
图 12.2。 非流形（左）和流形（右)内部顶点。

Many algorithms assume that meshes are manifold, and it’s always a good idea to verify this property to prevent crashes or infinite loops if you are handed a malformed mesh as input. This verification boils down to checking that all edges are manifold and checking that all vertices are manifold by verifying the following conditions:
许多算法都假设网格是流形的，如果您收到一个格式错误的网格作为输入，那么验证此属性始终是一个好主意，以防止崩溃或无限循环。 此验证归结为检查所有边是否是流形的，并通过验证以下条件来检查所有顶点是否是流形的：

- Every edge is shared by exactly two triangles. 
  每条边都由两个三角形共享。
- Every vertex has a single, complete loop of triangles around it.
  每个顶点周围都有一个完整的三角形环。

Figure 12.1 illustrates how an edge can fail the first test by having too many triangles, and Figure 12.2 illustrates how a vertex can fail the second test by having two separate loops of triangles attached to it. 
图 12.1 说明了一条边如何因具有太多三角形而无法通过第一个测试，图 12.2 说明了一个顶点如何通过附加两个单独的三角形环而无法通过第二个测试。

Manifold meshes are convenient, but sometimes it’s necessary to allow meshes to have edges, or boundaries. Such meshes are not manifolds—a point on the boundary has a neighborhood that is cut off on one side. They are not necessarily watertight. However, we can relax the requirements of a manifold mesh to those for a manifold with boundary without causing problems for most mesh processing algorithms. The relaxed conditions are:
流形网格很方便，但有时需要允许网格具有边缘或边界。 这样的网格不是流形——边界上的点有一个在一侧被切断的邻域。 它们不一定是防水的。 然而，我们可以将流形网格的要求放宽到具有边界的流形的要求，而不会导致大多数网格处理算法出现问题。 放宽的条件是：

- Every edge is used by either one or two triangles. 
  每条边都由一个或两个三角形使用。
- Every vertex connects to a single edge-connected set of triangles.
  每个顶点都连接到一组单条边连接的三角形。

Figure 12.3 illustrates these conditions: from left to right, there is an edge with one triangle, a vertex whose neighboring triangles are in a single edge-connected set, and a vertex with two disconnected sets of triangles attached to it.
图 12.3 说明了这些情况：从左到右，有一条带有一个三角形的边，一个其相邻三角形位于单个边连接集合中的顶点，以及一个带有两个不相连的三角形集合的顶点。
![Figure 12.3](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.3.png)
Figure 12.3. Conditions at the edge of a manifold with boundary.
图 12.3。 具有边界的流形边缘的条件。

Finally, in many applications it’s important to be able to distinguish the “front” or “outside” of a surface from the “back” or “inside”—this is known as the orientation of the surface. For a single triangle, we define orientation based on the order in which the vertices are listed: the front is the side from which the triangle’s three vertices are arranged in counterclockwise order. A connected mesh is consistently oriented if its triangles all agree on which side is the front—and this is true if and only if every pair of adjacent triangles is consistently oriented.
最后，在许多应用中，能够区分表面的“正面”或“外部”与“背面”或“内部”非常重要，这称为表面的方向。 对于单个三角形，我们根据顶点列出的顺序定义方向：前面是三角形的三个顶点按逆时针顺序排列的边。 如果连接的网格的三角形都一致以哪一侧为前，则该网格的方向一致 - 当且仅当每对相邻三角形的方向一致时，这才是正确的。

In a consistently oriented pair of triangles, the two shared vertices appear in opposite orders in the two triangles’ vertex lists (Figure 12.4). What’s important is consistency of orientation—some systems define the front using clockwise rather than counterclockwise order.
在方向一致的三角形对中，两个共享顶点在两个三角形的顶点列表中以相反的顺序出现（图 12.4）。 重要的是方向的一致性——一些系统使用顺时针而不是逆时针顺序定义前端。
![Figure 12.4](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.4.png)
Figure 12.4. Triangles (B,A,C) and (D,C,A) are consistently oriented, whereas (B,A,C) and (A,C,D) are inconsistently oriented.
图 12.4。 三角形 (B,A,C) 和 (D,C,A) 方向一致，而 (B,A,C) 和 (A,C,D) 方向不一致。

Any mesh that has non-manifold edges can’t be oriented consistently. But it’s also possible for a mesh to be a valid manifold with boundary (or even a manifold), and yet have no consistent way to orient the triangles—they are not orientable surfaces. An example is the Möbius band shown in Figure 12.5. This is rarely an issue in practice, however.
任何具有非流形边的网格都无法一致地定向。 但网格也可能是具有边界的有效流形（甚至是流形），但没有一致的方法来定向三角形 - 它们不是可定向的表面。 图 12.5 所示的莫比乌斯带就是一个例子。 然而，这在实践中很少成为问题。
![Figure 12.5](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.5.png)
Figure 12.5. A triangulated Möbius band, which is not orientable.
图 12.5。 不可定向的三角莫比乌斯带。

### 12.1.2 Indexed Mesh Storage 索引网格存储

A simple triangular mesh is shown in Figure 12.6. You could store these three triangles as independent entities, each of this form:
一个简单的三角形网格如图 12.6 所示。 您可以将这三个三角形存储为独立的实体，每个形式如下：
![Figure 12.6](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.6.png)
Figure 12.6. A three-triangle mesh with four vertices, represented with separate triangles (left) and with shared vertices (right). 
图 12.6。 具有四个顶点的三三角形网格，用单独的三角形（左）和共享顶点（右)表示。

```
Triangle {
	vector3 vertexPosition[3]
}
```

This would result in storing vertex $\bold{b}$ three times and the other vertices twice each for a total of nine stored points (three vertices for each of three triangles). Or you could instead arrange to share the common vertices and store only four, resulting in a shared-vertex mesh. Logically, this data structure has triangles which point to vertices which contain the vertex data:
这将导致存储顶点 $\bold{b}$ 三次，其他顶点各存储两次，总共九个存储点（三个三角形各三个顶点）。 或者，您可以安排共享公共顶点并仅存储四个顶点，从而形成共享顶点网格。 从逻辑上讲，该数据结构具有指向包含顶点数据的顶点的三角形：

```
Triangle {
	Vertex v[3]
}
Vertex {
	vector3 position // or other vertex data
}
```

Note that the entries in the v array are references, or pointers, to Vertex objects; the vertices are not contained in the triangle.
请注意，v 数组中的条目是对 Vertex 对象的引用或指针； 顶点不包含在三角形中。
![Figure 12.7](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.7.png)
Figure 12.7. The triangle-to-vertex references in a shared-vertex mesh.
图 12.7。 共享顶点网格中的三角形到顶点的参考。

In implementation, the vertices and triangles are normally stored in arrays, with the triangle-to-vertex references handled by storing array indices:
在实现中，顶点和三角形通常存储在数组中，三角形到顶点的引用通过存储数组索引来处理：

```
IndexedMesh {
	int tInd[nt][3]
	vector3 verts[nv]
}
```

The index of the $k$th vertex of the $i$th triangle is found in $tInd[i][k]$, and the position of that vertex is stored in the corresponding row of the verts array; see Figure 12.8 for an example. This way of storing a shared-vertex mesh is an indexed triangle mesh. 
在$tInd[i][k]$中找到第$i$个三角形的第$k$个顶点的索引，并将该顶点的位置存储在verts数组的相应行中； 示例见图 12.8。 这种存储共享顶点网格的方式是索引三角形网格。
![Figure 12.8](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.8.png)
Figure 12.8. A larger triangle mesh, with part of its representation as an indexed triangle mesh.  
图 12.8。 较大的三角形网格，其部分表示形式为索引三角形网格。

Separate triangles or shared vertices will both work well. Is there a space advantage for sharing vertices? If our mesh has $n_v$ vertices and $n_t$ triangles, and if we assume that the data for floats, pointers, and ints all require the same storage (a dubious assumption), the space requirements are as follows:
单独的三角形或共享的顶点都可以很好地工作。 共享顶点有空间优势吗？ 如果我们的网格有 $n_v$ 个顶点和 $n_t$ 个三角形，并且如果我们假设浮点数、指针和整数的数据都需要相同的存储（一个可疑的假设），则空间要求如下：

- **Triangle**. Three vectors per triangle, for $9n_t$ units of storage; 
  **三角形**。 每个三角形三个向量，用于 $9n_t$ 存储单元；
- **IndexedMesh**. One vector per vertex and three ints per triangle, for $3n_v + 3n_t$ units of storage.
  **索引网格**。 每个顶点一个向量，每个三角形三个整数，存储单元为 $3n_v + 3n_t$。

The relative storage requirements depend on the ratio of $n_t$ to $n_v$.
相对存储要求取决于 $n_t$ 与 $n_v$ 的比率。

As a rule of thumb, a large mesh has each vertex connected to about six triangles (although there can be any number for extreme cases). Since each triangle connects to three vertices, this means that there are generally twice as many triangles as vertices in a large mesh: $nt ≈ 2n_v$. Making this substitution, we can conclude that the storage requirements are $18n_v$ for the Triangle structure and $9n_v$ for IndexedMesh. Using shared vertices reduces storage requirements by about a factor of two; and this seems to hold in practice for most implementations.
根据经验，大网格的每个顶点连接到大约六个三角形（尽管极端情况下可以有任意数量）。 由于每个三角形连接到三个顶点，这意味着大网格中三角形的数量通常是顶点的两倍：$nt ≈ 2n_v$。 通过这种替换，我们可以得出结论，Triangle 结构的存储需求为 $18n_v$，IndexedMesh 的存储需求为 $9n_v$。 使用共享顶点可将存储需求减少大约两倍； 对于大多数实现来说，这似乎在实践中是成立的。

> Is this factor of two worth the complication? I think the answer is yes, and it becomes an even bigger win as soon as you start adding “properties” to the vertices.
> 这个二的因素值得复杂化吗？ 我认为答案是肯定的，一旦你开始向顶点添加“属性”，它就会成为一个更大的胜利。

### 12.1.3 Triangle Strips and Fans 三角条和扇子

Indexed meshes are the most common in-memory representation of triangle meshes, because they achieve a good balance of simplicity, convenience, and compactness. They are also commonly used to transfer meshes over networks and between the application and graphics pipeline. In applications where even more compactness is desirable, the triangle vertex indices (which take up two-thirds of the space in an indexed mesh with only positions at the vertices) can be expressed more efficiently using triangle strips and triangle fans.
索引网格是三角形网格最常见的内存表示形式，因为它们实现了简单性、便利性和紧凑性的良好平衡。 它们还通常用于通过网络以及应用程序和图形管道之间传输网格。 在需要更紧凑的应用中，可以使用三角形条和三角形扇更有效地表达三角形顶点索引（在仅包含顶点位置的索引网格中占据三分之二的空间）。

A triangle fan is shown in Figure 12.9. In an indexed mesh, the triangles array would contain [(0, 1, 2), (0, 2, 3), (0, 3, 4), (0, 4, 5)]. We are storing 12 vertex indices, although there are only six distinct vertices. In a triangle fan, all the triangles share one common vertex, and the other vertices generate a set of triangles like the vanes of a collapsible fan. The fan in the figure could be specified with the sequence [0, 1, 2, 3, 4, 5]: the first vertex establishes the center, and subsequently each pair of adjacent vertices (1-2, 2-3, etc.) 
三角扇如图 12.9 所示。 在索引网格中，三角形数组将包含 [(0, 1, 2), (0, 2, 3), (0, 3, 4), (0, 4, 5)]。 尽管只有 6 个不同的顶点，但我们存储了 12 个顶点索引。 在三角形风扇中，所有三角形共享一个公共顶点，其他顶点生成一组三角形，就像可折叠风扇的叶片一样。 图中的扇形可以用序列 [0, 1, 2, 3, 4, 5] 指定：第一个顶点建立中心，随后每对相邻顶点（1-2、2-3 等）建立中心。 ) 创建一个三角形。creates a triangle.
![Figure 12.9](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.9.png)
Figure 12.9. A triangle fan. 
图 12.9。 一把三角扇。

The triangle strip is a similar concept, but it is useful for a wider range of meshes. Here, vertices are added alternating top and bottom in a linear strip as shown in Figure 12.10. The triangle strip in the figure could be specified by the sequence [0 1 2 3 4 5 6 7], and every subsequence of three adjacent vertices (0- 1-2, 1-2-3, etc.) creates a triangle. For consistent orientation, every other triangle needs to have its order reversed. In the example, this results in the triangles (0, 1, 2), (2, 1, 3), (2, 3, 4), (4, 3, 5), etc. For each new vertex that comes in, the oldest vertex is forgotten and the order of the two remaining vertices is swapped. See Figure 12.11 for a larger example.
三角形带是一个类似的概念，但它适用于更广泛的网格。 在这里，顶点以线性条带的顶部和底部交替添加，如图 12.10 所示。 图中的三角形带可以由序列[0 1 2 3 4 5 6 7]指定，并且三个相邻顶点（0-1-2、1-2-3等）的每个子序列创建一个三角形。 为了保持方向一致，所有其他三角形都需要颠倒顺序。 在本例中，这会产生三角形 (0, 1, 2)、(2, 1, 3)、(2, 3, 4)、(4, 3, 5) 等。对于进入的每个新顶点 ，最旧的顶点被遗忘，剩下的两个顶点的顺序被交换。 更大的例子见图 12.11。
![Figure 12.10](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.10.png)
Figure 12.10. A triangle strip. 
图 12.10。 一条三角带。

![Figure 12.11](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.11.png)
Figure 12.11. Two triangle strips in the context of a larger mesh. Note that neither strip can be extended to include the triangle marked with an asterisk. 
图 12.11。 较大网格中的两个三角形条带。 请注意，这两个条带都不能扩展以包含标有星号的三角形。

In both strips and fans, $n + 2$ vertices suffice to describe $n$ triangles—a substantial savings over the $3n$ vertices required by a standard indexed mesh. Long triangle strips will save approximately a factor of three if the program is vertex-bound. 
在条带和扇形中，$n + 2$ 个顶点足以描述 $n$ 个三角形，这比标准索引网格所需的 $3n$ 个顶点节省了很多。 如果程序是顶点绑定的，长三角形带将节省大约三倍的时间。

It might seem that triangle strips are only useful if the strips are very long, but even relatively short strips already gain most of the benefits. The savings in storage space (for only the vertex indices) are as follows:
看起来三角形条带只有在条带很长的情况下才有用，但即使是相对较短的条带也已经获得了大部分好处。 节省的存储空间（仅针对顶点索引）如下：

| strip length  |  1   |  2   |  3   |  4   |  5   |  6   |  7   |  8   |  16  | 100  | $∞$  |
| :-----------: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| relative size | 1.00 | 0.67 | 0.56 | 0.50 | 0.47 | 0.44 | 0.43 | 0.42 | 0.38 | 0.34 | 0.33 |

So, in fact, there is a rather rapid diminishing return as the strips grow longer. Thus, even for an unstructured mesh, it is worthwhile to use some greedy algorithm to gather them into short strips.
因此，事实上，随着条带变长，回报会迅速递减。 因此，即使对于非结构化网格，也值得使用一些贪心算法将它们聚集成短条。

### 12.1.4 Data Structures for Mesh Connectivity 网格连接的数据结构

Indexed meshes, strips, and fans are all good, compact representations for static meshes. However, they do not readily allow for meshes to be modified. In order to efficiently edit meshes, more complicated data structures are needed to efficiently answer queries such as:
索引网格、条带和扇形都是静态网格的良好、紧凑的表示形式。 然而，它们不容易允许修改网格。 为了有效地编辑网格，需要更复杂的数据结构来有效地回答查询，例如：

- Given a triangle, what are the three adjacent triangles?
  给定一个三角形，三个相邻的三角形是什么？
- Given an edge, which two triangles share it?
  给定一条边，哪两个三角形共享它？
- Given a vertex, which faces share it?
  给定一个顶点，哪些面共享它？
- Given a vertex, which edges share it?
  给定一个顶点，哪些边共享它？

There are many data structures for triangle meshes, polygonal meshes, and polygonal meshes with holes (see the notes at the end of the chapter for references). In many applications the meshes are very large, so an efficient representation can be crucial. 
三角形网格、多边形网格、带孔多边形网格的数据结构有很多种（参考见本章末尾的注释）。 在许多应用中，网格非常大，因此有效的表示至关重要。

The most straightforward, though bloated, implementation would be to have three types, Vertex, Edge, and Triangle, and to just store all the relationships directly:
最直接但臃肿的实现是具有三种类型：顶点、边和三角形，并直接存储所有关系：

```
Triangle {
	Vertex v[3]
	Edge e[3]
}
Edge {
	Vertex v[2]
	Triangle t[2]
}
Vertex {
	Triangle t[]
	Edge e[]
}
```

This lets us directly look up answers to the connectivity questions above, but because this information is all inter-related, it stores more than is really needed. Also, storing connectivity in vertices makes for variable-length data structures (since vertices can have arbitrary numbers of neighbors), which are generally less efficient to implement. Rather than committing to store all these relationships explicitly, it is best to define a class interface to answer these questions, behind which a more efficient data structure can hide. It turns out we can store only some of the connectivity and efficiently recover the other information when needed. 
这使我们可以直接查找上述连接问题的答案，但由于这些信息都是相互关联的，因此它存储的信息超出了实际需要的信息。 此外，在顶点中存储连接性会产生可变长度的数据结构（因为顶点可以具有任意数量的邻居），这通常实现起来效率较低。 与其致力于显式存储所有这些关系，不如定义一个类接口来回答这些问题，在其后面可以隐藏更高效的数据结构。 事实证明，我们可以只存储一些连接性，并在需要时有效地恢复其他信息。

The fixed-size arrays in the Edge and Triangle classes suggest that it will be more efficient to store the connectivity information there. In fact, for polygon meshes, in which polygons have arbitrary numbers of edges and vertices, only edges have fixed-size connectivity information, which leads to many traditional mesh data structures being based on edges. But for triangle-only meshes, storing connectivity in the (less numerous) faces is appealing. 
Edge 和 Triangle 类中的固定大小数组表明在那里存储连接信息会更有效。 事实上，对于多边形网格来说，多边形具有任意数量的边和顶点，只有边具有固定大小的连通性信息，这导致许多传统的网格数据结构都是基于边的。 但对于纯三角形网格来说，在（数量较少的）面中存储连接性很有吸引力。

A good mesh data structure should be reasonably compact and allow efficient answers to all adjacency queries. Efficient means constant-time: the time to find neighbors should not depend on the size of the mesh. We’ll look at three data structures for meshes, one based on triangles and two based on edges.
一个好的网格数据结构应该相当紧凑，并且能够有效地回答所有邻接查询。 高效意味着恒定时间：寻找邻居的时间不应取决于网格的大小。 我们将研究三种网格数据结构，一种基于三角形，两种基于边缘。

#### The Triangle-Neighbor Structure 三角形相邻结构

We can create a compact mesh data structure based on triangles by augmenting the basic shared-vertex mesh with pointers from the triangles to the three neighboring triangles, and a pointer from each vertex to one of the adjacent triangles (it doesn’t matter which one); see Figure 12.12:
我们可以创建一个基于三角形的紧凑网格数据结构，通过使用从三角形到三个相邻三角形的指针以及从每个顶点到相邻三角形之一的指针（无论是哪一个）来扩充基本共享顶点网格。 ）； 见图12.12：
![Figure 12.12](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.12.png)
Figure 12.12. The references between triangles and vertices in the triangle-neighbor structure.
图 12.12。 三角形邻居结构中三角形和顶点之间的引用。

```
Triangle {
	Triangle nbr[3];
	Vertex v[3];
}
Vertex {
	// ... per-vertex data ...
	Triangle t; // any adjacent tri
}
```

In the array Triangle.nbr, the kth entry points to the neighboring triangle that shares vertices k and k + 1. We call this structure the triangle-neighbor structure. Starting from standard indexed mesh arrays, it can be implemented with two additional arrays: one that stores the three neighbors of each triangle, and one that stores a single neighboring triangle for each vertex (see Figure 12.13 for an example):
在数组 Triangle.nbr 中，第 k 个条目指向共享顶点 k 和 k + 1 的相邻三角形。我们将此结构称为三角形相邻结构。 从标准索引网格数组开始，它可以通过两个附加数组来实现：一个存储每个三角形的三个邻居，另一个存储每个顶点的单个相邻三角形（参见图 12.13 的示例）：
![Figure 12.13](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.13.png)

Figure 12.13. The triangle-neighbor structure as encoded in arrays, and the sequence that is followed in traversing the neighboring triangles of vertex 2. 
图 12.13。 数组中编码的三角形相邻结构，以及遍历顶点 2 的相邻三角形时遵循的序列。

```
Mesh {
	// ... per-vertex data ...
	int tInd[nt][3]; // vertex indices
	int tNbr[nt][3]; // indices of neighbor triangles
	int vTri[nv]; // index of any adjacent triangle
}
```

Clearly the neighboring triangles and vertices of a triangle can be found directly in the data structure, but by using this triangle adjacency information carefully it is also possible to answer connectivity queries about vertices in constant time. The idea is to move from triangle to triangle, visiting only the triangles adjacent to the relevant vertex. If triangle t has vertex v as its kth vertex, then the triangle $t.nbr[k]$ is the next triangle around v in the clockwise direction. This observation leads to the following algorithm to traverse all the triangles adjacent to a given vertex:
显然，可以直接在数据结构中找到相邻三角形和三角形的顶点，但是通过仔细使用该三角形邻接信息，也可以在恒定时间内回答有关顶点的连通性查询。 这个想法是从一个三角形移动到另一个三角形，仅访问与相关顶点相邻的三角形。 如果三角形 t 将顶点 v 作为其第 k 个顶点，则三角形 $t.nbr[k]$ 是沿顺时针方向围绕 v 的下一个三角形。 这一观察导致以下算法来遍历与给定顶点相邻的所有三角形：

```
TrianglesOfVertex(v) {
	t = v.t
	do {
		find i such that (t.v[i] == v)
		t = t.nbr[i]
	} while (t != v.t)
}
```

> Of course, a real program would do something with the triangles as it found them.
> 当然，真正的程序会在找到三角形时对其进行处理。

This operation finds each subsequent triangle in constant time—even though a search is required to find the position of the central vertex in each triangle’s vertex list, the vertex lists have constant size so the search takes constant time. However, that search is awkward and requires extra branching. 
此操作在恒定时间内找到每个后续三角形 - 尽管需要搜索来查找每个三角形顶点列表中中心顶点的位置，但顶点列表具有恒定大小，因此搜索需要恒定时间。 然而，这种搜索很尴尬并且需要额外的分支。

A small refinement can avoid these searches. The problem is that once we follow a pointer from one triangle to the next, we don’t know from which way we came: we have to search the triangle’s vertices to find the vertex that connects back to the previous triangle. To solve this, instead of storing pointers to neighboring triangles, we can store pointers to specific edges of those triangles by storing an index with the pointer:
一个小的改进可以避免这些搜索。 问题是，一旦我们沿着指针从一个三角形到下一个三角形，我们就不知道我们是从哪条路来的：我们必须搜索三角形的顶点以找到连接回前一个三角形的顶点。 为了解决这个问题，我们可以通过存储指针的索引来存储指向这些三角形的特定边的指针，而不是存储指向相邻三角形的指针：

```
Triangle {
	Edge nbr[3];
	Vertex v[3];
}
Edge { // the i-th edge of triangle t
	Triangle t;
	int i; // in {0,1,2}
}
Vertex {
	// ... per-vertex data ...
	Edge e; // any edge leaving vertex
}
```

In practice the Edge is stored by borrowing two bits of storage from the triangle index $t$ to store the edge index $i$, so that the total storage requirements remain the same.
实际上，边的存储是通过从三角形索引$t$借用两位存储来存储边索引$i$，使得总存储需求保持不变。

In this structure the neighbor array for a triangle tells which of the neighboring triangles’ edges are shared with the three edges of that triangle. With this extra information, we always know where to find the original triangle, which leads to an invariant of the data structure: for any $j$th edge of any triangle $t$,
在这个结构中，三角形的邻居数组告诉我们相邻三角形的哪条边与该三角形的三个边共享。 有了这些额外的信息，我们总是知道在哪里可以找到原始三角形，这导致了数据结构的不变性：对于任何三角形$t$的任何$j$th边，
$t.nbr[j].t.nbr[t.nbr[j].i].t == t.$

Knowing which edge we came in through lets us know immediately which edge to leave through in order to continue traversing around a vertex, leading to a streamlined algorithm:
知道我们通过哪条边进入可以让我们立即知道要离开哪条边以便继续围绕顶点遍历，从而形成简化的算法：

```
TrianglesOfVertex(v) {
	{t, i} = v.e;
	do {
		{t, i} = t.nbr[i];
		i = (i+1) mod 3;
	} while (t != v.e.t);
}
```

The triangle-neighbor structure is quite compact. For a mesh with only vertex positions, we are storing four numbers (three coordinates and an edge) per vertex and six (three vertex indices and three edges) per face, for a total of $4n_v + 6n_t ≈ 16n_v$ units of storage per vertex, compared with $9n_v$ for the basic indexed mesh. 
三角形邻居结构非常紧凑。 对于仅包含顶点位置的网格，我们为每个顶点存储 4 个数字（三个坐标和一条边），为每个面存储 6 个数字（三个顶点索引和三个边），总共为每个存储 $4n_v + 6n_t ≈ 16n_v$ 单位。 顶点，与基本索引网格的 $9n_v$ 相比。

The triangle neighbor structure as presented here works only for manifold meshes, because it depends on returning to the starting triangle to terminate the traversal of a vertex’s neighbors, which will not happen at a boundary vertex that doesn’t have a full cycle of triangles. However, it is not difficult to generalize it to manifolds with boundary, by introducing a suitable sentinel value (such as −1) for the neighbors of boundary triangles and taking care that the boundary vertices point to the most counterclockwise neighboring triangle, rather than to any arbitrary triangle.
这里介绍的三角形邻居结构仅适用于流形网格，因为它依赖于返回起始三角形来终止顶点邻居的遍历，这不会发生在没有完整三角形循环的边界顶点上。 然而，将其推广到有边界的流形并不困难，通过为边界三角形的邻居引入合适的哨兵值（例如-1），并注意边界顶点指向最逆时针相邻的三角形，而不是指向 任意三角形。

#### The Winged-Edge Structure 翼缘结构

One widely used mesh data structure that stores connectivity information at the edges instead of the faces is the winged-edge data structure. This data structure makes edges the first-class citizen of the data structure, as illustrated in Figures 12.14 and 12.15.
翼边数据结构是一种广泛使用的网格数据结构，它存储边缘而不是面的连接信息。 这种数据结构使边成为数据结构的一等公民，如图 12.14 和 12.15 所示。
![Figure 12.14](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.14.png)
Figure 12.14. An example of a winged-edge mesh structure, stored in arrays. 
图 12.14。 存储在数组中的翼边网格结构的示例。

![Figure 12.15](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.15.png)
Figure 12.15. A tetrahedron and the associated elements for a winged-edge data structure. The two small tables are not unique; each vertex and face stores any one of the edges with which it is associated.
图 12.15。 翼边数据结构的四面体和相关元素。 这两张小桌子并不独特； 每个顶点和面都存储与其关联的任何一条边。

In a winged-edge mesh, each edge stores pointers to the two vertices it connects (the head and tail vertices), the two faces it is part of (the left and right faces), and, most importantly, the next and previous edges in the counterclockwise traversal of its left and right faces (Figure 12.16). Each vertex and face also stores a pointer to a single, arbitrary edge that connects to it:
在翼边网格中，每条边都存储指向它连接的两个顶点（头顶点和尾顶点）、它所属的两个面（左面和右面）的指针，以及最重要的下一条边和上一条边 逆时针遍历其左右面（图12.16）。 每个顶点和面还存储一个指向连接到它的单个任意边的指针：
![Figure 12.16](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.16.png)
Figure 12.16. The references from an edge to the neighboring edges, faces, and vertices in the winged-edge structure.
图 12.16。 翼边结构中从边到相邻边、面和顶点的参考。

```
Edge {
	Edge lprev, lnext, rprev, rnext;
	Vertex head, tail;
	Face left, right;
}
Face {
	// ... per-face data ...
	Edge e; // any adjacent edge
}
Vertex {
	// ... per-vertex data ...
	Edge e; // any incident edge
}
```

The winged-edge data structure supports constant-time access to the edges of a face or of a vertex, and from those edges the adjoining vertices or faces can be found:
翼边数据结构支持对面或顶点的边进行恒定时间访问，并且可以从这些边找到相邻的顶点或面：

```
EdgesOfVertex(v) {
	e = v.e;
	do {
		if (e.tail == v)
			e = e.lprev;
		else
			e = e.rprev;
	} while (e != v.e);
}
EdgesOfFace(f) {
	e = f.e;
	do {
		if (e.left == f)
			e = e.lnext;
		else
			e = e.rnext;
	} while (e != f.e);
}
```

These same algorithms and data structures will work equally well in a polygon mesh that isn’t limited to triangles; this is one important advantage of edge-based structures. 
这些相同的算法和数据结构在多边形网格中同样适用，不仅限于三角形； 这是基于边缘的结构的一个重要优势。

As with any data structure, the winged-edge data structure makes a variety of time/space tradeoffs. For example, we can eliminate the prev references. This makes it more difficult to traverse clockwise around faces or counterclockwise around vertices, but when we need to know the previous edge, we can always follow the successor edges in a circle until we get back to the original edge. This saves space, but it makes some operations slower. (See the chapter notes for more information on these tradeoffs).
与任何数据结构一样，翼缘数据结构会进行各种时间/空间权衡。 例如，我们可以删除以前的引用。 这使得绕面顺时针遍历或绕顶点逆时针遍历变得更加困难，但是当我们需要知道前一条边时，我们总是可以沿着一圈跟随后继边，直到回到原始边。 这可以节省空间，但会使某些操作变慢。 （有关这些权衡的更多信息，请参阅章节注释）。

#### The Half-Edge Structure 半边结构

The winged-edge structure is quite elegant, but it has one remaining awkwardness—the need to constantly check which way the edge is oriented before moving to the next edge. This check is directly analogous to the search we saw in the basic version of the triangle neighbor structure: we are looking to find out whether we entered the present edge from the head or from the tail. The solution is also almost indistinguishable: rather than storing data for each edge, we store data for each half-edge. There is one half-edge for each of the two triangles that share an edge, and the two half-edges are oriented oppositely, each oriented consistently with its own triangle. 
翼缘结构非常优雅，但它还有一个尴尬之处——在移动到下一个边缘之前需要不断检查边缘的方向。 这种检查直接类似于我们在三角形邻居结构的基本版本中看到的搜索：我们正在寻找我们是从头部还是从尾部进入当前边缘。 该解决方案也几乎无法区分：我们不是为每个边存储数据，而是为每个半边存储数据。 共享一条边的两个三角形各有一个半边，并且这两个半边的方向相反，每个半边的方向与其自己的三角形一致。

The data normally stored in an edge is split between the two half-edges. Each half-edge points to the face on its side of the edge and to the vertex at its head, and each contains the edge pointers for its face. It also points to its neighbor on the other side of the edge, from which the other half of the information can be found. Like the winged-edge, a half-edge can contain pointers to both the previous and next half-edges around its face, or only to the next half-edge. We’ll show the example that uses a single pointer.
通常存储在边缘中的数据被分割在两个半边缘之间。 每个半边都指向该边一侧的面和其头部的顶点，并且每个半边都包含其面的边指针。 它还指向边缘另一侧的邻居，从中可以找到另一半信息。 与翼边一样，半边可以包含指向其面周围的前一个半边和下一个半边的指针，或者仅包含指向下一个半边的指针。 我们将展示使用单个指针的示例。

```
HEdge {
	HEdge pair, next;
	Vertex v;
	Face f;
}
Face {
	// ... per-face data ...
	HEdge h; // any h-edge of this face
}
Vertex {
	// ... per-vertex data ...
	HEdge h; // any h-edge pointing toward this vertex
}
```

![Figure 12.17](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.17.png)
Figure 12.17. The references from a half-edge to its neighboring mesh components.
图 12.17。 从半边到其相邻网格组件的引用。

Traversing a half-edge structure is just like traversing a winged-edge structure except that we no longer need to check orientation, and we follow the pair pointer to access the edges in the opposite face.
遍历半边结构就像遍历翼边结构一样，只不过我们不再需要检查方向，并且我们沿着对指针访问相反面的边。

```
EdgesOfVertex(v) {
	h = v.h;
	do {
		h = h.pair.next;
	} while (h != v.h);
}
EdgesOfFace(f) {
	h = f.h;
	do {
		h = h.next;
	} while (h != f.h);
}
```

The vertex traversal here is clockwise, which is necessary because of omitting the prev pointer from the structure.
这里的顶点遍历是顺时针的，这是必要的，因为从结构中省略了 prev 指针。

Because half-edges are generally allocated in pairs (at least in a mesh with no boundaries), many implementations can do away with the pair pointers. For instance, in an implementation based on array indexing (such as shown in Figure 12.18), the array can be arranged so that an even-numbered edge $i$ always pairs with edge $i + 1$ and an odd-numbered edge $j$ always pairs with edge $j − 1$. 
由于半边通常成对分配（至少在没有边界的网格中），因此许多实现可以取消对指针。 例如，在基于数组索引的实现中（如图 12.18 所示），可以对数组进行排列，使得偶数边 $i$ 始终与边 $i + 1$ 和奇数边 $ 配对 j$ 总是与边 $j − 1$ 配对。
![Figure 12.18](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.18.png)
Figure 12.18. An example of a half-edge mesh structure, stored in arrays.
图 12.18。 存储在数组中的半边网格结构的示例。

In addition to the simple traversal algorithms shown in this chapter, all three of these mesh topology structures can support “mesh surgery” operations of various sorts, such as splitting or collapsing vertices, swapping edges, adding or removing triangles, etc.
除了本章所示的简单遍历算法之外，所有这三种网格拓扑结构都可以支持各种类型的“网格手术”操作，例如分裂或折叠顶点、交换边、添加或删除三角形等。

## 12.2 Scene Graphs 场景图

A triangle mesh manages a collection of triangles that constitute an object in a scene, but another universal problem in graphics applications is arranging the objects in the desired positions. As we saw in Chapter 6, this is done using transformations, but complex scenes can contain a great many transformations and organizing them well makes the scene much easier to manipulate. Most scenes admit to a hierarchical organization, and the transformations can be managed according to this hierarchy using a scene graph.
三角形网格管理构成场景中对象的三角形集合，但图形应用程序中的另一个普遍问题是将对象排列在所需的位置。 正如我们在第 6 章中看到的，这是使用变换来完成的，但是复杂的场景可以包含大量变换，并且良好地组织它们使场景更容易操作。 大多数场景都允许分层组织，并且可以使用场景图根据该分层结构来管理转换。

To motivate the scene-graph data structure, we will use the hinged pendulum shown in Figure 12.19. Consider how we would draw the top part of the pendulum:
为了激发场景图数据结构，我们将使用如图 12.19 所示的铰链摆。 考虑一下我们如何绘制钟摆的顶部：
![Figure 12.19](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.19.png)
Figure 12.19. A hinged pendulum. On the left are the two pieces in their “local” coordinate systems. The hinge of the bottom piece is at point $\bold{b}$ and the attachment for the bottom piece is at its local origin. The degrees of freedom for the assembled object are the angles $(θ,φ)$ and the location $\bold{p}$ of the top hinge.
图 12.19。 一个铰接摆。 左边是“局部”坐标系中的两个部分。 底部部件的铰链位于点 $\bold{b}$ 处，底部部件的附件位于其本地原点。 组装物体的自由度是角度 $(θ,φ)$ 和顶部铰链的位置 $\bold{p}$。

> $\bold{M}_1 = rotate(θ)$
> $\bold{M}_2 = translate(\bold{p})$
> $\bold{M}_3 = \bold{M}_2\bold{M}_1$
> Apply $\bold{M}_3$ to all points in upper pendulum  

The bottom is more complicated, but we can take advantage of the fact that it is attached to the bottom of the upper pendulum at point $\bold{b}$ in the local coordinate system. First, we rotate the lower pendulum so that it is at an angle φ relative to its initial position. Then, we move it so that its top hinge is at point b. Now it is at the appropriate position in the local coordinates of the upper pendulum, and it can then be moved along with that coordinate system. The composite transform for the lower pendulum is:
底部更复杂，但我们可以利用它在局部坐标系中的点 $\bold{b}$ 处连接到上摆底部的事实。 首先，我们旋转下摆，使其相对于初始位置成角度 φ。 然后，我们移动它，使其顶部铰链位于 b 点。 现在它位于上摆局部坐标中的适当位置，然后它可以沿着该坐标系移动。 下摆的复合变换为：

> $\bold{M}_a = rotate(φ)$
> $\bold{M}_b = translate(\bold{b})$
> $\bold{M}_c = \bold{M}_b\bold{M}_a$
> $\bold{M}_d = \bold{M}_3\bold{M}_c$
> Apply $\bold{M}_d$ to all points in lower pendulum  

Thus, we see that the lower pendulum not only lives in its own local coordinate system, but also that coordinate system itself is moved along with that of the upper pendulum. 
因此，我们看到下摆不仅存在于自己的局部坐标系中，而且该坐标系本身也随着上摆的坐标系一起移动。

We can encode the pendulum in a data structure that makes management of these coordinate system issues easier, as shown in Figure 12.20. The appropriate matrix to apply to an object is just the product of all the matrices in the chain from the object to the root of the data structure. For example, consider the model of a ferry that has a car that can move freely on the deck of the ferry, and wheels that each move relative to the car as shown in Figure 12.21.
我们可以将摆编码为数据结构，从而使这些坐标系问题的管理变得更加容易，如图 12.20 所示。 应用于对象的适当矩阵只是从对象到数据结构根的链中所有矩阵的乘积。 例如，考虑一个渡轮模型，其中有一辆可以在渡轮甲板上自由移动的汽车，以及每个相对于汽车移动的轮子，如图 12.21 所示。

![Figure 12.20](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.20.png)
Figure 12.20. The scene graph for the hinged pendulum of Figure 12.19.
图 12.20。 图 12.19 的铰接摆场景图。

![Figure 12.21](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.21.png)
Figure 12.21. A ferry, a car on the ferry, and the wheels of the car (only two shown) are stored in a scene-graph.
图 12.21。 渡轮、渡轮上的汽车以及汽车的车轮（仅显示两个)都存储在场景图中。

As with the pendulum, each object should be transformed by the product of the matrices in the path from the root to the object: 
与钟摆一样，每个对象都应该通过从根到对象的路径中的矩阵乘积进行变换：

- ferry transform using $M_0$; 
  使用 $M_0$ 进行轮渡变换；
- car body transform using $M_0M_1$; 
  使用$M_0M_1$进行车身变换；
- left wheel transform using $M_0M_1M_2$; 
  使用 $M_0M_1M_2$ 进行左轮变换；
- left wheel transform using $M_0M_1M_3$.
  使用$M_0M_1M_3$进行左轮变换。

An efficient implementation can be achieved using a matrix stack, a data structure supported by many APIs. A matrix stack is manipulated using push and pop operations that add and delete matrices from the right-hand side of a matrix product. For example, calling:
使用矩阵堆栈（许多 API 支持的数据结构）可以实现高效的实现。 矩阵堆栈是使用压入和弹出操作来操作的，这些操作从矩阵乘积的右侧添加和删除矩阵。 例如，调用：

> push($\bold{M}_0$)
> push($\bold{M}_1$)
> push($\bold{M}_2$)

creates the active matrix $\bold{M} = \bold{M}_0\bold{M}_1\bold{M}_2$. A subsequent call to pop() strips the last matrix added so that the active matrix becomes $\bold{M} = \bold{M}_0\bold{M}_1$. Combining the matrix stack with a recursive traversal of a scene graph gives us:
创建活动矩阵 $\bold{M} = \bold{M}_0\bold{M}_1\bold{M}_2$。 随后调用 pop() 会删除最后添加的矩阵，以便活动矩阵变为 $\bold{M} = \bold{M}_0\bold{M}_1$。 将矩阵堆栈与场景图的递归遍历相结合，我们可以得到：

> function traverse(node)
> 	push($\bold{M}_{local}$)
> 	draw object using composite matrix from stack
> 	traverse(left child)
> 	traverse(right child)
> 	pop()

There are many variations on scene graphs but all follow the basic idea above.
场景图有很多变化，但都遵循上述基本思想。

## 12.3 Spatial Data Structures 空间数据结构

In many, if not all, graphics applications, the ability to quickly locate geometric objects in particular regions of space is important. Ray tracers need to find objects that intersect rays; interactive applications navigating an environment need to find the objects visible from any given viewpoint; games and physical simulations require detecting when and where objects collide. All these needs can be supported by various spatial data structures designed to organize objects in space so they can be looked up efficiently. 
在许多（如果不是全部）图形应用程序中，快速定位特定空间区域中的几何对象的能力非常重要。 光线追踪器需要找到与光线相交的物体； 在环境中导航的交互式应用程序需要找到从任何给定视点可见的对象； 游戏和物理模拟需要检测物体碰撞的时间和地点。 所有这些需求都可以通过各种空间数据结构来支持，这些空间数据结构旨在组织空间中的对象，以便可以有效地查找它们。

In this section we will discuss examples of three general classes of spatial data structures. Structures that group objects together into a hierarchy are object partitioning schemes: objects are divided into disjoint groups, but the groups may end up overlapping in space. Structures that divide space into disjoint regions are space partitioning schemes: space is divided into separate partitions, but one object may have to intersect more than one partition. Space partitioning schemes can be regular, in which space is divided into uniformly shaped pieces, or irregular, in which space is divided adaptively into irregular pieces, with smaller pieces where there are more and smaller objects. 
在本节中，我们将讨论三类通用空间数据结构的示例。 将对象分组到层次结构中的结构是对象分区方案：对象被分为不相交的组，但这些组最终可能在空间上重叠。 将空间划分为不相交区域的结构是空间划分方案：空间被划分为单独的分区，但一个对象可能必须与多个分区相交。 空间划分方案可以是规则的，其中空间被划分为均匀形状的块，或者是不规则的，其中空间被适应性地划分为不规则的块，其中存在更多和更小的对象的块更小。

We will use ray tracing as the primary motivation while discussing these structures, though they can all also be used for view culling or collision detection. In Chapter 4, all objects were looped over while checking for intersections. For N objects, this is an O(N) linear search and is thus slow for large scenes. Like most search problems, the ray-object intersection can be computed in sub-linear time using “divide and conquer” techniques, provided we can create an ordered data structure as a preprocess. There are many techniques to do this. 
在讨论这些结构时，我们将使用光线追踪作为主要动机，尽管它们也可以用于视图剔除或碰撞检测。 在第 4 章中，在检查交叉点时循环遍历所有对象。 对于 N 个对象，这是一个 O(N) 线性搜索，因此对于大场景来说速度很慢。 与大多数搜索问题一样，只要我们可以创建有序数据结构作为预处理，就可以使用“分而治之”技术在亚线性时间内计算光线与对象的交集。 有很多技术可以做到这一点。

This section discusses three of these techniques in detail: bounding volume hierarchies (Rubin & Whitted, 1980; Whitted, 1980; Goldsmith & Salmon, 1987), uniform spatial subdivision (Cleary, Wyvill, Birtwistle, & Vatti, 1983; Fujimoto, Tanaka, & Iwata, 1986; Amanatides & Woo, 1987), and binary space partitioning (Glassner, 1984; Jansen, 1986; Havran, 2000). An example of the first two strategies is shown in Figure 12.22.
本节详细讨论其中三种技术：包围体层次结构（Rubin & Whitted，1980；Whitted，1980；Goldsmith & Salmon，1987）、统一空间细分（Cleary、Wyvill、Birtwistle 和 Vatti，1983；Fujimoto、Tanaka， & Iwata，1986；Amanatides & Woo，1987），以及二进制空间划分（Glassner，1984；Jansen，1986；Havran，2000）。 前两种策略的示例如图 12.22 所示。
![Figure 12.22](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.22.png)

Figure 12.22. Left: a uniform partitioning of space. Right: adaptive bounding-box hierarchy. Image courtesy David DeMarle.  
图 12.22。 左：统一的空间划分。 右：自适应边界框层次结构。 图片由大卫·德马尔提供。

### 12.3.1 Bounding Boxes 边界框

A key operation in most intersection-acceleration schemes is computing the intersection of a ray with a bounding box (Figure 12.23). This differs from conventional intersection tests in that we do not need to know where the ray hits the box; we only need to know whether it hits the box. 
大多数相交加速方案中的一个关键操作是计算射线与边界框的相交（图 12.23）。 这与传统的相交测试不同，我们不需要知道光线击中盒子的位置； 我们只需要知道它是否击中盒子即可。
![Figure 12.23](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.23.png)
Figure 12.23. The ray is only tested for intersection with the surfaces if it hits the bounding box.
图 12.23。 仅当光线击中边界框时才测试光线与表面的相交。

To build an algorithm for ray-box intersection, we begin by considering a 2D ray whose direction vector has positive x and y components. We can generalize this to arbitrary 3D rays later. The 2D bounding box is defined by two horizontal and two vertical lines: 
为了构建射线盒相交的算法，我们首先考虑方向向量具有正 x 和 y 分量的 2D 射线。 稍后我们可以将其推广到任意 3D 射线。 2D 边界框由两条水平线和两条垂直线定义：

> $x = x_{min}$, 
> $x = x_{max}$,
> $y = y_{min}$,
> $y = y_{max}.  $

The points bounded by these lines can be described in interval notation: 
这些线所包围的点可以用区间表示法来描述：
$(x, y) ∈ [x_{min}, x_{max}] × [y_{min}, y_{max}]  $

As shown in Figure 12.24, the intersection test can be phrased in terms of these intervals. First, we compute the ray parameter where the ray hits the line $x = x_{min}$:
如图 12.24 所示，交叉测试可以用这些间隔来表达。 首先，我们计算光线撞击线 $x = x_{min}$ 的光线参数：
$t_{xmin} = \frac{x_{min}-x_e}{x_d}\\$
![Figure 12.24](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.24.png)
Figure 12.24. The ray will be inside the interval $x ∈ [x_{min}, x_{max}]$ for some interval in its parameter space $t ∈ [t_{xmin}, t_{xmax}]$. A similar interval exists for the y interval. The ray intersects the box if it is in both the x interval and y interval at the same time, i.e., the intersection of the two one-dimensional intervals is not empty.
图 12.24。 对于参数空间 $t ∈ [t_{xmin}, t_{xmax}]$ 中的某个区间，射线将位于区间 $x ∈ [x_{min}, x_{max}]$ 内。 y 区间也存在类似的区间。 如果射线同时位于 x 区间和 y 区间，即两个一维区间的交集不为空，则射线与盒子相交。

We then make similar computations for $t_{xmax}$, $t_{ymin}$, and $t_{ymax}$. The ray hits the box if and only if the intervals $[t_{xmin}, t_{xmax}]$ and $[t_{ymin}, t_{ymax}]$ overlap, i.e., their intersection is nonempty. In pseudocode this algorithm is:
然后我们对 $t_{xmax}$、$t_{ymin}$ 和 $t_{ymax}$ 进行类似的计算。 当且仅当区间 $[t_{xmin}, t_{xmax}]$ 和 $[t_{ymin}, t_{ymax}]$ 重叠时，光线才会击中盒子，即它们的交集非空。 该算法的伪代码为：

> $t_{xmin} = (x_{min} - x_e)/x_d$
> $t_{xmax} = (x_{max} - x_e)/x_d$
> $t_{ymin} = (y_{min} - y_e)/y_d$
> $tymax = (ymax - ye)/y_d$
> if $(t_{xmin} > t_{ymax})$ or $(t_{ymin} > t_{xmax})$ then
> 	return false
> else
> 	return true  

The if statement may seem non-obvious. To see the logic of it, note that there is no overlap if the first interval is either entirely to the right or entirely to the left of the second interval.
if 语句可能看起来不明显。 要了解其逻辑，请注意，如果第一个间隔完全位于第二个间隔的右侧或完全左侧，则不存在重叠。

The first thing we must address is the case when $x_d$ or $y_d$ is negative. If $x_d$ is negative, then the ray will hit $x_{max}$ before it hits $x_{min}$. Thus the code for computing $t_{xmin}$ and $t_{xmax}$ expands to:
我们必须解决的第一件事是 $x_d$ 或 $y_d$ 为负数的情况。 如果 $x_d$ 为负数，则光线将在到达 $x_{min}$ 之前先到达 $x_{max}$。 因此，计算 $t_{xmin}$ 和 $t_{xmax}$ 的代码扩展为：

> if ($x_d ≥ 0$) then
> 	$t_{xmin} = (x_{min} - x_e)/x_d$
> 	$t_{xmax} = (x_{max} - x_e)/x_d$
> else
> 	$t_{xmin} = (x_{max} - x_{e})/x_d$
> 	$t_{xmax} = (x_{min} - x_e)/x_d  $

A similar code expansion must be made for the $y$ cases. A major concern is that horizontal and vertical rays have a zero value for $y_d$ and $x_d$, respectively. This will cause divide by zero which may be a problem. However, before addressing this directly, we check whether IEEE floating point computation handles these cases gracefully for us. Recall from Section 1.5 the rules for divide by zero: for any positive real number $a$,
必须对 $y$ 情况进行类似的代码扩展。 主要问题是水平和垂直光线的 $y_d$ 和 $x_d$ 分别为零值。 这将导致除以零，这可能是一个问题。 然而，在直接解决这个问题之前，我们检查 IEEE 浮点计算是否可以很好地为我们处理这些情况。 回想一下 1.5 节除以零的规则：对于任何正实数 $a$，
$+a/0 = +∞;\\
-a/0 = -∞.  $

Consider the case of a vertical ray where $x_d = 0$ and $y_d > 0$. We can then calculate
考虑垂直射线的情况，其中 $x_d = 0$ 且 $y_d > 0$。 然后我们可以计算
$$
t_{xmin} = \frac{x_{min} - x_e}{0}\\
t_{xmax} = \frac{x_{max} - x_e}{0}
$$
There are three possibilities of interest:
感兴趣的有以下三种可能性：

1. $x_e ≤ x_{min}$ (no hit);
2. $x_{min} < x_e < x_{max}$ (hit);
3. $x_{max} ≤ x_e$ (no hit).

For the first case we have
对于第一种情况，我们有
$$
t_{xmin} = \frac{positive\ number}{0} \\
t_{xmax} = \frac{positive\ number}{0} \\
$$
This yields the interval $(t_{xmin}, t_{xmin}) = (∞, ∞)$. That interval will not overlap with any interval, so there will be no hit, as desired. For the second case, we have
由此得出区间 $(t_{xmin}, t_{xmin}) = (∞, ∞)$。 该间隔不会与任何间隔重叠，因此不会出现所需的命中。 对于第二种情况，我们有
$$
t_{xmin} = \frac{negative\ number}{0} \\
t_{xmax} = \frac{positive\ number}{0} \\
$$
This yields the interval $(t_{xmin}, t_{xmin}) = (−∞, ∞)$ which will overlap with all intervals and thus will yield a hit as desired. The third case results in the interval $(−∞, −∞)$ which yields no hit, as desired. Because these cases work as desired, we need no special checks for them. As is often the case, IEEE floating point conventions are our ally. However, there is still a problem with this approach. 
这会产生区间 $(t_{xmin}, t_{xmin}) = (−∞, ∞)$ ，它将与所有区间重叠，从而产生所需的命中。 第三种情况导致区间 $(−∞, −∞)$ 不产生所需的命中。 因为这些情况按预期工作，所以我们不需要对它们进行特殊检查。 通常情况下，IEEE 浮点约定是我们的盟友。 然而，这种方法仍然存在一个问题。

Consider the code segment:
考虑代码段：

> if $(x_d ≥ 0)$ then
> 	$t_{min} = (x_{min} - x_e)/x_d$
> 	$t_{max} = (x_{max} - x_e)/x_d$ 
> else
> 	$t_{min} = (x_{max} − x_e)/x_d$
> 	$t_{max} = (x_{min} − x_e)/x_d$

This code breaks down when $x_d = -0$. This can be overcome by testing on the reciprocal of $x_d$ (A. Williams, Barrus, Morley, & Shirley, 2005): 
当 $x_d = -0$ 时，此代码将崩溃。 这可以通过测试 $x_d$ 的倒数来克服（A. Williams, Barrus, Morley, & Shirley, 2005）：

> $a = 1/x_d$
> if $(a ≥ 0)$ then
> 	$t_{min} = a(x_{min} - x_e)$
> 	$t_{max} = a(x_{max} - x_e)$
> else
> 	$t_{min} = a(x_{max} - x_e)$
> 	$t_{max} = a(x_{min} - x_e)$

### 12.3.2 Hierarchical Bounding Boxes 分层边界框

The basic idea of hierarchical bounding boxes can be seen by the common tactic of placing an axis-aligned 3D bounding box around all the objects as shown in Figure 12.25. Rays that hit the bounding box will actually be more expensive to compute than in a brute force search, because testing for intersection with the box is not free. However, rays that miss the box are cheaper than the brute force search. Such bounding boxes can be made hierarchical by partitioning the set of objects in a box and placing a box around each partition as shown in Figure 12.26. The data structure for the hierarchy shown in Figure 12.27 might be a tree with the large bounding box at the root and the two smaller bounding boxes as left and right subtrees. These would in turn each point to a list of three triangles. The intersection of a ray with this particular hard-coded tree would be: 
分层边界框的基本思想可以通过在所有对象周围放置轴对齐的 3D 边界框的常见策略来看出，如图 12.25 所示。 击中边界框的光线实际上比暴力搜索的计算成本更高，因为与边界框相交的测试并不是免费的。 然而，错过盒子的射线比强力搜索便宜。 这种边界框可以通过划分框中的对象集并在每个分区周围放置一个框来分层，如图 12.26 所示。 图 12.27 所示的层次结构的数据结构可能是一棵树，其中大边界框位于根，两个较小的边界框作为左子树和右子树。 这些将依次指向三个三角形的列表。 射线与这个特定的硬编码树的交集将是：

```
if (ray hits root box) then
	if (ray hits left subtree box) then
		check three triangles for intersection
	if (ray intersects right subtree box) then
		check other three triangles for intersection
	if (an intersections returned from each subtree) then
		return the closest of the two hits
	else if (a intersection is returned from exactly one subtree) then
		return that intersection
	else
		return false
else
	return false
```

![Figure 12.25](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.25.png)
Figure 12.25. A 2D ray $\bold{e} + t\bold{d}$ is tested against a 2D bounding box.
图 12.25。 2D 射线 $\bold{e} + t\bold{d}$ 针对 2D 边界框进行测试。

![Figure 12.26](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.26.png)
Figure 12.26. The bounding boxes can be nested by creating boxes around subsets of the model.
图 12.26。 可以通过在模型子集周围创建框来嵌套边界框。

![Figure 12.27](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.27.png)
Figure 12.27. The gray box is a tree node that points to the three gray spheres, and the thick black box points to the three black spheres. Note that not all spheres enclosed by the box are guaranteed to be pointed to by the corresponding tree node.
图 12.27。 灰色框是一个树节点，指向三个灰色球体，粗黑框指向三个黑色球体。 请注意，并非所有被盒子包围的球体都保证被相应的树节点指向。

Some observations related to this algorithm are that there is no geometric ordering between the two subtrees, and there is no reason a ray might not hit both subtrees. Indeed, there is no reason that the two subtrees might not overlap.
与该算法相关的一些观察结果是，两个子树之间没有几何顺序，并且光线没有理由不击中两个子树。 事实上，两个子树没有理由不重叠。

A key point of such data hierarchies is that a box is guaranteed to bound all objects that are below it in the hierarchy, but they are not guaranteed to contain all objects that overlap it spatially, as shown in Figure 12.27. This makes this geometric search somewhat more complicated than a traditional binary search on strictly ordered one-dimensional data. The reader may note that several possible optimizations present themselves. We defer optimizations until we have a full hierarchical algorithm.
这种数据层次结构的一个关键点是，一个盒子保证绑定层次结构中低于它的所有对象，但不能保证它们包含空间上与其重叠的所有对象，如图 12.27 所示。 这使得这种几何搜索比严格排序的一维数据上的传统二分搜索更加复杂。 读者可能会注意到，存在几种可能的优化。 我们推迟优化，直到我们拥有完整的分层算法。

If we restrict the tree to be binary and require that each node in the tree have a bounding box, then this traversal code extends naturally. Further, assume that all nodes are either leaves in the tree and contain a primitive, or that they contain one or two subtrees.
如果我们将树限制为二叉树，并要求树中的每个节点都有一个边界框，那么这个遍历代码就会自然地扩展。 此外，假设所有节点要么是树中的叶子并包含基元，要么它们包含一两个子树。

The bvh-node class should be of type surface, so it should implement surface::hit. The data it contains should be simple:
bvh-node 类应该是surface 类型，因此它应该实现surface::hit。 它包含的数据应该很简单：

> class bvh-node subclass of surface
> 	virtual bool hit(ray $\bold{e} + t\bold{d}$, real $t_0$, real $t_1$, hit-record rec)
> 	virtual box bounding-box()
> 	surface-pointer left
> 	surface-pointer right
> 	box bbox

The traversal code can then be called recursively in an object-oriented style:
然后可以以面向对象的方式递归调用遍历代码：

> function bool bvh-node::hit(ray $\bold{a} + t\bold{b}$, real $t_0$, real $t_1$, hit-record rec)
> 	if (bbox.hitbox($\bold{a} + t\bold{b}$, $t_0$, $t_1$)) then
> 		hit-record lrec, rrec
> 		left-hit = (left ≠ NULL) and (left → hit($\bold{a} + t\bold{b}$, $t_0$, $t_1$, lrec))
> 		right-hit = (right ≠ NULL) and (right → hit($\bold{a}+t\bold{b}$, $t_0$, $t_1$, rrec))
> 		if (left-hit and right-hit) then
> 			if (lrec.t < rrec.t) then
> 				rec = lrec
> 			else
> 				rec = rrec
> 			return true
> 		else if (left-hit) then
> 			rec = lrec
> 			return true
> 		else if (right-hit) then
> 			rec = rrec
> 			return true
> 		else
> 			return false
> 	else
> 		return false  

Note that because left and right point to surfaces rather than bvh-nodes specifically, we can let the virtual functions take care of distinguishing between internal and leaf nodes; the appropriate hit function will be called. Note that if the tree is built properly, we can eliminate the check for left being NULL. If we want to eliminate the check for right being NULL, we can replace NULL right pointers with a redundant pointer to left. This will end up checking left twice, but will eliminate the check throughout the tree. Whether that is worth it will depend on the details of tree construction.
请注意，因为 left 和 right 专门指向表面而不是 bvh 节点，所以我们可以让虚函数负责区分内部节点和叶节点； 将调用适当的命中函数。 请注意，如果树构建正确，我们可以消除对 left 为 NULL 的检查。 如果我们想消除对右为 NULL 的检查，我们可以用指向左的冗余指针替换 NULL 右指针。 这将最终检查左两次，但会消除整个树的检查。 这是否值得将取决于树木构造的细节。

There are many ways to build a tree for a bounding volume hierarchy. It is convenient to make the tree binary, roughly balanced, and to have the boxes of sibling subtrees not overlap too much. A heuristic to accomplish this is to sort the surfaces along an axis before dividing them into two sublists. If the axes are defined by an integer with $x = 0$, $y = 1$, and $z = 2$ we have:
有多种方法可以构建包围体层次结构的树。 方便使树成为二叉树，大致平衡，并且兄弟子树的框不会重叠太多。 实现此目的的启发式方法是先沿轴对曲面进行排序，然后再将其划分为两个子列表。 如果轴由整数定义，其中 $x = 0$、$y = 1$ 和 $z = 2$，我们有：

> function bvh-node::create(object-array A, int AXIS)
> 	N = A.length
> 	if (N= 1) then
> 		left = A[0]
> 		right = NULL
> 		bbox = bounding-box(A[0])
> 	else if (N= 2) then
> 		left-node = A[0]
> 		right-node = A[1]
> 		bbox = combine(bounding-box(A[0]), bounding-box(A[1]))
> 	else
> 		sort A by the object center along AXIS
> 		left= new bvh-node(A[0..N/2 - 1], (AXIS +1) mod 3)
> 		right = new bvh-node(A[N/2..N-1], (AXIS +1) mod 3)
> 		bbox = combine(left → bbox, right → bbox)  

The quality of the tree can be improved by carefully choosing AXIS each time. One way to do this is to choose the axis such that the sum of the volumes of the bounding boxes of the two subtrees is minimized. This change compared to rotating through the axes will make little difference for scenes composed of isotopically distributed small objects, but it may help significantly in less well-behaved scenes. This code can also be made more efficient by doing just a partition rather than a full sort. 
每次仔细选择 AXIS 都可以提高树的质量。 实现此目的的一种方法是选择轴，以使两个子树的边界框的体积之和最小化。 与通过轴旋转相比，这种变化对于由同位素分布的小物体组成的场景几乎没有什么影响，但对于表现不佳的场景可能会有很大帮助。 通过仅执行分区而不是完整排序，还可以提高此代码的效率。

Another, and probably better, way to build the tree is to have the subtrees contain about the same amount of space rather than the same number of objects. To do this we partition the list based on space:
另一种可能更好的构建树的方法是让子树包含大约相同数量的空间而不是相同数量的对象。 为此，我们根据空间对列表进行分区：

> function bvh-node::create(object-array A, int AXIS)
> 	N = A.length
> 	if (N = 1) then
> 		left = A[0]
> 		right = NULL
> 		bbox = bounding-box(A[0])
> 	else if (N = 2) then
> 		left = A[0]
> 		right = A[1]
> 		bbox = combine(bounding-box(A[0]), bounding-box(A[1]))
> 	else
> 		find the midpoint m of the bounding box of A along AXIS
> 		partition A into lists with lengths k and (N − k) surrounding m
> 		left = new bvh-node(A[0..k], (AXIS +1) mod 3)
> 		right = new bvh-node(A[k + 1..N − 1], (AXIS +1) mod 3)
> 		bbox = combine(left → bbox, right → bbox)

Although this results in an unbalanced tree, it allows for easy traversal of empty space and is cheaper to build because partitioning is cheaper than sorting. 
尽管这会导致树不平衡，但它可以轻松遍历空白空间，并且构建成本更低，因为分区比排序更便宜。

### 12.3.3 Uniform Spatial Subdivision 统一空间细分

Another strategy to reduce intersection tests is to divide space. This is fundamentally different from dividing objects as was done with hierarchical bounding volumes: 
减少交叉测试的另一个策略是划分空间。 这与使用分层包围体划分对象有本质上的不同：

- In hierarchical bounding volumes, each object belongs to one of two sibling nodes, whereas a point in space may be inside both sibling nodes. 
  在分层包围体中，每个对象属于两个兄弟节点之一，而空间中的点可能位于两个兄弟节点内。
- In spatial subdivision, each point in space belongs to exactly one node, whereas objects may belong to many nodes. 
  在空间细分中，空间中的每个点恰好属于一个节点，而对象可能属于多个节点。

In uniform spatial subdivision, the scene is partitioned into axis-aligned boxes. These boxes are all the same size, although they are not necessarily cubes. The ray traverses these boxes as shown in Figure 12.28. When an object is hit, the traversal ends.
在均匀空间细分中，场景被划分为轴对齐的框。 这些盒子大小相同，但不一定是立方体。 光线穿过这些盒子，如图 12.28 所示。 当物体被击中时，遍历结束。
![Figure 12.28](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.28.png)
Figure 12.28. In uniform spatial subdivision, the ray is tracked forward through cells until an object in one of those cells is hit. In this example, only objects in the shaded cells are checked. 
图 12.28。 在均匀空间细分中，光线向前跟踪穿过细胞，直到击中其中一个细胞中的物体。 在此示例中，仅检查阴影单元格中的对象。

The grid itself should be a subclass of surface and should be implemented as a 3D array of pointers to surface. For empty cells these pointers are NULL. For cells with one object, the pointer points to that object. For cells with more than one object, the pointer can point to a list, another grid, or another data structure, such as a bounding volume hierarchy.
网格本身应该是表面的子类，并且应该作为表面指针的 3D 数组来实现。 对于空单元格，这些指针为 NULL。 对于具有一个对象的单元格，指针指向该对象。 对于具有多个对象的单元格，指针可以指向列表、另一个网格或另一个数据结构，例如包围体层次结构。 

This traversal is done in an incremental fashion. The regularity comes from the way that a ray hits each set of parallel planes, as shown in Figure 12.29. To see how this traversal works, first consider the 2D case where the ray direction has positive x and y components and starts outside the grid. Assume the grid is bounded by points $(x_{min}, y_{min})$ and $(x_{max}, y_{max})$. The grid has $n_x × n_y$ cells.
这种遍历是以增量方式完成的。 规律性来自于光线撞击每组平行平面的方式，如图 12.29 所示。 要了解这种遍历的工作原理，首先考虑 2D 情况，其中射线方向具有正 x 和 y 分量并从网格外部开始。 假设网格以点 $(x_{min}, y_{min})$ 和 $(x_{max}, y_{max})$ 为边界。 网格有 $n_x × n_y$ 个单元格。
![Figure 12.29](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.29.png)
Figure 12.29. Although the pattern of cell hits seems irregular (left), the hits on sets of parallel planes are very even.
图 12.29。 尽管细胞命中的模式看起来不规则（左)，但平行平面组上的命中非常均匀。

Our first order of business is to find the index $(i, j)$ of the first cell hit by the ray $\bold{e} + t\bold{d}$. Then, we need to traverse the cells in an appropriate order. The key parts to this algorithm are finding the initial cell $(i, j)$ and deciding whether to increment $i$ or $j$ (Figure 12.30). Note that when we check for an intersection with objects in a cell, we restrict the range of t to be within the cell (Figure 12.31). Most implementations make the 3D array of type “pointer to surface.” To improve the locality of the traversal, the array can be tiled as discussed in Section 12.5.
我们的首要任务是找到光线 $\bold{e} + t\bold{d}$ 击中的第一个单元格的索引 $(i, j)$。 然后，我们需要以适当的顺序遍历单元格。 该算法的关键部分是找到初始单元$(i, j)$并决定是否增加$i$或$j$（图12.30）。 请注意，当我们检查与单元格中的对象的交集时，我们将 t 的范围限制在单元格内（图 12.31）。 大多数实现将 3D 数组设为“指向表面的指针”类型。 为了提高遍历的局部性，可以按照 12.5 节中的讨论对数组进行平铺。
![](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.30.png)
Figure 12.30. To decide whether we advance right or upward, we keep track of the intersections with the next vertical and horizontal boundary of the cell.
图 12.30。 为了决定是向右还是向上前进，我们跟踪与单元格的下一个垂直和水平边界的交点。

![](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.31.png)
Figure 12.31. Only hits within the cell should be reported. Otherwise the case above would cause us to report hitting object $b$ rather than object $a$.
图 12.31。 仅应报告细胞内的命中。 否则，上面的情况会导致我们报告击中对象 $b$ 而不是对象 $a$。

### 12.3.4 Axis-Aligned Binary Space Partitioning  轴对齐的二进制空间分区

We can also partition space in a hierarchical data structure such as a binary space partitioning tree (BSP tree). This is similar to the BSP tree used for visibility sorting in Section 12.4, but it’s most common to use axis-aligned, rather than polygon-aligned, cutting planes for ray intersection. 
我们还可以在分层数据结构中划分空间，例如二元空间划分树（BSP 树）。 这类似于第 12.4 节中用于可见性排序的 BSP 树，但最常见的是使用轴对齐而不是多边形对齐的切割平面来进行射线相交。

A node in this structure contains a single cutting plane and a left and right subtree. Each subtree contains all the objects on one side of the cutting plane. Objects that pass through the plane are stored in in both subtrees. If we assume the cutting plane is parallel to the $yz$ plane at $x = D$, then the node class is:
该结构中的节点包含单个切割平面和左右子树。 每个子树包含切割平面一侧的所有对象。 通过平面的对象存储在两个子树中。 如果我们假设切割平面在 $x = D$ 处平行于 $yz$ 平面，则节点类为：

> class bsp-node subclass of surface
> 	virtual bool hit(ray $\bold{e} + t\bold{d}$, real $t_0$, real $t_1$, hit-record rec)
> 	virtual box bounding-box()
> 	surface-pointer left
> 	surface-pointer right
> 	real D  

We generalize this to y and z cutting planes later. The intersection code can then be called recursively in an object-oriented style. The code considers the four cases shown in Figure 12.32. For our purposes, the origin of these rays is a point at parameter $t_0$:
稍后我们将其推广到 y 和 z 切割平面。 然后可以以面向对象的方式递归调用交集代码。 该代码考虑了图 12.32 中所示的四种情况。 出于我们的目的，这些光线的原点是参数 $t_0$ 处的点：
$\bold{p} = \bold{a} + t_0\bold{b}.  $
![Figure 12.32](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.32.png)
Figure 12.32. The four cases of how a ray relates to the BSP cutting plane $x = D$.
图 12.32。 射线与 BSP 剖切面 $x = D$ 的关系的四种情况。

The four cases are: 
这四种情况是：

1. The ray only interacts with the left subtree, and we need not test it for intersection with the cutting plane. It occurs for $x_p < D$ and $x_b < 0$. 
   射线仅与左子树相互作用，我们不需要测试它与切割平面的相交。 当 $x_p < D$ 且 $x_b < 0$ 时会发生这种情况。
2. The ray is tested against the left subtree, and if there are no hits, it is then tested against the right subtree. We need to find the ray parameter at $x = D$, so we can make sure we only test for intersections within the subtree. This case occurs for $x_p < D$ and $x_b > 0$.
   射线针对左子树进行测试，如果没有命中，则针对右子树进行测试。 我们需要找到 $x = D$ 处的射线参数，这样我们就可以确保只测试子树内的相交。 这种情况发生在 $x_p < D$ 和 $x_b > 0$ 时。
3. This case is analogous to case 1 and occurs for $x_p > D$ and $x_b > 0$. 
   这种情况与情况 1 类似，发生在 $x_p > D$ 且 $x_b > 0$ 的情况下。
4. This case is analogous to case 2 and occurs for $x_p > D$ and $x_b < 0$.
   这种情况与情况 2 类似，发生在 $x_p > D$ 且 $x_b < 0$ 的情况下。

The resulting traversal code handling these cases in order is:
按顺序处理这些情况的最终遍历代码是：

> function bool bsp-node::hit(ray $\bold{a} + t\bold{b}$, real $t_0$, real $t_1$,hit-record rec)
> 	$x_p = x_a + t_0x_b$
> 	if $(x_p < D)$ then
> 		if $(x_b < 0)$ then
> 			return (left ≠ NULL) and (left→hit($\bold{a} + t\bold{b}, t_0, t_1, rec$))
> 		$t = (D - x_a)/x_b$
> 		if $(t > t_1)$ then
> 			return (left ≠ NULL) and (left→hit($\bold{a} + t\bold{b}, t_0, t_1$, rec))
> 		if (left ≠ NULL) and (left→hit($\bold{a} + t\bold{b}, t_0, t$, rec)) then
> 			return true
> 		return (right ≠ NULL) and (right→hit($\bold{a} + t\bold{b}, t, t_1$, rec))
> 	else
> 		analogous code for cases 3 and 4

This is very clean code. However, to get it started, we need to hit some root object that includes a bounding box so we can initialize the traversal, t0 and t1. An issue we have to address is that the cutting plane may be along any axis. We can add an integer index axis to the bsp-node class. If we allow an indexing operator for points, this will result in some simple modifications to the code above, for example,
这是非常干净的代码。 然而，为了开始它，我们需要命中一些包含边界框的根对象，以便我们可以初始化遍历 t0 和 t1。 我们必须解决的一个问题是切割平面可以沿着任何轴。 我们可以向 bsp-node 类添加一个整数索引轴。 如果我们允许点的索引运算符，这将导致对上面的代码进行一些简单的修改，例如，
$x_p = x_a + t_0x_b  $

would become
会成为
$u_p = a[axis] + t_0b[axis]  $

which will result in some additional array indexing, but will not generate more branches. 
这将导致一些额外的数组索引，但不会生成更多分支。

While the processing of a single bsp-node is faster than processing a bvh-node, the fact that a single surface may exist in more than one subtree means there are more nodes and, potentially, a higher memory use. How “well” the trees are built determines which is faster. Building the tree is similar to building the BVH tree. We can pick axes to split in a cycle, and we can split in half each time, or we can try to be more sophisticated in how we divide.
虽然处理单个 bsp 节点比处理 bvh 节点更快，但单个表面可能存在于多个子树中这一事实意味着存在更多节点，并且可能会使用更高的内存。 树木建造的“好”程度决定了哪一个更快。 构建树与构建 BVH 树类似。 我们可以选择一个循环中的轴进行分割，并且每次都可以分割成两半，或者我们可以尝试更复杂的分割方式。

## 12.4 BSP Trees for Visibility BSP 树的可见性

Another geometric problem in which spatial data structures can be used is determining the visibility ordering of objects in a scene with changing viewpoint. 
可以使用空间数据结构的另一个几何问题是确定视点变化的场景中对象的可见性顺序。

If we are making many images of a fixed scene composed of planar polygons, from different viewpoints—as is often the case for applications such as games— we can use a binary space partitioning scheme closely related to the method for ray intersection discussed in the previous section. The difference is that for visibility sorting we use non–axis-aligned splitting planes, so that the planes can be made coincident with the polygons. This leads to an elegant algorithm known as the BSP tree algorithm to order the surfaces from front to back. The key aspect of the BSP tree is that it uses a preprocess to create a data structure that is useful for any viewpoint. So, as the viewpoint changes, the same data structure is used without change.
如果我们从不同的角度制作由平面多边形组成的固定场景的许多图像（游戏等应用程序经常出现这种情况），我们可以使用与前面讨论的光线相交方法密切相关的二元空间划分方案 部分。 不同之处在于，对于可见性排序，我们使用非轴对齐的分割平面，以便平面可以与多边形重合。 这导致了一种称为 BSP 树算法的优雅算法，用于从前到后对表面进行排序。 BSP 树的关键方面是它使用预处理来创建对任何观点都有用的数据结构。 因此，随着观点的变化，使用相同的数据结构而不改变。 

### 12.4.1 Overview of BSP Tree Algorithm BSP树算法概述

The BSP tree algorithm is an example of a painter’s algorithm. A painter’s algorithm draws every object from back-to-front, with each new polygon potentially overdrawing previous polygons, as is shown in Figure 12.33. It can be implemented as follows:
BSP 树算法是画家算法的一个例子。 画家的算法从后到前绘制每个对象，每个新的多边形都可能会过度绘制先前的多边形，如图 12.33 所示。 可以按如下方式实现：

```
sort objects back to front relative to viewpoint
for each object do
	draw object on screen
```

![Figure 12.33](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.33.png)
Figure 12.33. A painter’s algorithm starts with a blank image and then draws the scene one object at a time from back-to-front, overdrawing whatever is already there. This automatically eliminates hidden surfaces.
图 12.33。 画家的算法从一张空白图像开始，然后从后到前一次绘制场景中的一个对象，过度绘制已经存在的任何内容。 这会自动消除隐藏的曲面。

The problem with the first step (the sort) is that the relative order of multiple objects is not always well defined, even if the order of every pair of objects is. This problem is illustrated in Figure 12.34 where the three triangles form a cycle.
第一步（排序）的问题在于，多个对象的相对顺序并不总是明确定义的，即使每对对象的顺序都是如此。 这个问题如图 12.34 所示，其中三个三角形形成一个循环。
![Figure 12.34](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.34.png)
Figure 12.34. A cycle occurs if a global back-to-front ordering is not possible for a particular eye position.
图 12.34。 如果对于特定眼睛位置不可能进行全局从后到前排序，则会发生循环。

The BSP tree algorithm works on any scene composed of polygons where no polygon crosses the plane defined by any other polygon. This restriction is then relaxed by a preprocessing step. For the rest of this discussion, triangles are assumed to be the only primitive, but the ideas extend to arbitrary polygons.
BSP 树算法适用于由多边形组成的任何场景，其中没有多边形与任何其他多边形定义的平面相交。 然后通过预处理步骤放宽此限制。 在本次讨论的其余部分中，假设三角形是唯一的基元，但这些想法可以扩展到任意多边形。

The basic idea of the BSP tree can be illustrated with two triangles, $T_1$ and $T_2$. We first recall (see Section 2.5.3) the implicit plane equation of the plane containing $T_1: f_1(\bold{p}) = 0$. The key property of implicit planes that we wish to take advantage of is that for all points $\bold{p}^+$ on one side of the plane, $f_1(\bold{p}^+) > 0$; and for all points $\bold{p}^−$ on the other side of the plane, $f_1(\bold{p}^−) < 0$. Using this property, we can find out on which side of the plane $T_2$ lies. Again, this assumes all three vertices of T2 are on the same side of the plane. For discussion, assume that $T_2$ is on the $f_1(\bold{p}) < 0$ side of the plane. Then, we can draw $T_1$ and $T_2$ in the right order for any eyepoint $\bold{e}$: 
BSP树的基本思想可以用两个三角形T1和T2来说明。我们首先回顾一下（见第2.5.3节）包含T1的平面的隐式方程：$T_1: f_1(\bold{p}) = 0$。我们希望利用隐式平面的一个关键性质，即对于平面一侧的所有点$\bold{p}^+$，有$f_1(\bold{p}^+) > 0$；对于平面另一侧的所有点$\bold{p}^−$，有$f_1(\bold{p}^−) < 0$。利用这个性质，我们可以找出$T_2$位于平面的哪一侧。这里假设$T_2$的三个顶点都在平面的同一侧。为了讨论，假设$T_2$在$f_1(\bold{p}) < 0$的平面一侧。那么，我们可以按照任意视点$\bold{e}$的正确顺序绘制 $T_1$和 $T_2$：

> if $(f_1(\bold{e}) < 0)$ then
> 	draw $T_1$
> 	draw $T_2$
> else
> 	draw $T_2$
> 	draw $T_1$

The reason this works is that if $T_2$ and e are on the same side of the plane containing $T_1$, there is no way for $T_2$ to be fully or partially blocked by $T_1$ as seen from $\bold{e}$, so it is safe to draw $T_1$ first. If $\bold{e}$ and $T_2$ are on opposite sides of the plane containing $T_1$, then $T_2$ cannot fully or partially block $T_1$, and the opposite drawing order is safe (Figure 12.35).
这样做的原因是，如果$T_2$和e在包含$T_1$的平面的同一侧，则从$\bold{e}$中可以看出，$T_2$不可能被$T_1$完全或部分阻塞，因此先绘制$T_1$是安全的。如果$\bold{e}$和$T_2$在包含$T_1$的平面的对面，则$T_2$不能完全或部分阻塞$T_1$，相反的绘制顺序是安全的(图12.35)。
![Figure 12.35](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.35.png)
Figure 12.35. When $\bold{e}$ and $T_2$ are on opposite sides of the plane containing $T_1$, then it is safe to draw $T_2$ first and $T_1$ second. If $\bold{e}$ and $T_2$ are on the same side of the plane, then $T_1$ should be drawn before $T_2$. This is the core idea of the BSP tree algorithm.
图12.35。当$\bold{e}$和$T_2$位于包含$T_1$的平面的相对两侧时，则可以安全地绘制$T_2$ first和$T_1$ second。如果$\bold{e}$和$T_2$在平面的同一侧，则$T_1$应在$T_2$之前绘制。这是BSP树算法的核心思想。

This observation can be generalized to many objects provided none of them span the plane defined by $T_1$. If we use a binary tree data structure with $T_1$ as root, the negative branch of the tree contains all the triangles whose vertices have $f_i(\bold{p}) < 0$, and the positive branch of the tree contains all the triangles whose vertices have $f_i(\bold{p}) > 0$. We can draw in proper order as follows:
这种观察可以推广到许多对象，只要它们都不跨越 $T_1$ 定义的平面。 如果我们使用以$T_1$为根的二叉树数据结构，树的负分支包含所有顶点$f_i(\bold{p}) < 0$的三角形，树的正分支包含所有顶点为$f_i(\bold{p}) < 0$的三角形。 顶点 $f_i(\bold{p}) > 0$ 的三角形。 我们可以按照正确的顺序绘制如下：

> function draw(bsptree tree, point $\bold{e}$)
> 	if (tree.empty) then
> 		return
> 	if $(f_{tree.root}(\bold{e}) < 0)$ then
> 		draw(tree.plus, $\bold{e}$)
> 		rasterize tree.triangle
> 		draw(tree.minus, $\bold{e}$)
> 	else
> 		draw(tree.minus, $\bold{e}$)
> 		rasterize tree.triangle
> 		draw(tree.plus, $\bold{e}$)  

The nice thing about that code is that it will work for any viewpoint $\bold{e}$, so the tree can be precomputed. Note that, if each subtree is itself a tree, where the root triangle divides the other triangles into two groups relative to the plane containing it, the code will work as is. It can be made slightly more efficient by terminating the recursive calls one level higher, but the code will still be simple. A tree illustrating this code is shown in Figure 12.36. As discussed in Section 2.5.5, the implicit equation for a point $\bold{p}$ on a plane containing three non-colinear points $\bold{a}$, $\bold{b}$, and $\bold{c}$ is
这段代码的好处是，它将适用于任何视点$\bold{e}$，因此树可以预先计算。注意，如果每个子树本身是一个树，其中根三角形将其他三角形相对于包含它的平面分成两组，则代码将按原样工作。通过在更高一级终止递归调用，可以稍微提高效率，但代码仍然很简单。图12.36中显示了一个树来说明这段代码。如第2.5.5节所述，在包含三个非共线点$\bold{a}$、$\bold{b}$和$\bold{c}$的平面上，点$\bold{p}$的隐式方程为
$$
f(\bold{p}) = ((\bold{b} − \bold{a}) × (\bold{c} − \bold{a})) · (\bold{p} − \bold{a}) = 0. (12.1)
$$
![Figure 12.36](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.36.png)
Figure 12.36. Three triangles and a BSP tree that is valid for them. The “positive” and “negative” are encoded by right and left subtree position, respectively. 
图12.36。三个三角形和一个对它们有效的BSP树。“正”和“负”分别由右子树和左子树位置编码。

It can be faster to store the (A, B, C, D) of the implicit equation of the form
它可以更快地存储(A, B, C, D)的隐式方程的形式 
$$
f(x, y, z) = Ax + By + Cz + D = 0. (12.2)
$$
Equations (12.1) and (12.2) are equivalent, as is clear when you recall that the gradient of the implicit equation is the normal to the triangle. The gradient of Equation (12.2) is $\bold{n} = (A, B, C)$ which is just the normal vector
方程 (12.1) 和 (12.2) 是等价的，当您回想隐式方程的梯度是三角形的法线时就清楚了。 方程（12.2）的梯度为$\bold{n} = (A, B, C)$，它只是法向量
$\bold{n} = (\bold{b} - \bold{a}) × (\bold{c} - \bold{a}).  $

We can solve for D by plugging in any point on the plane, e.g., $\bold{a}$:
我们可以通过代入平面上的任意点来求解 D，例如 $\bold{a}$：
$D = -Ax_a - By_a - Cz_a = -\bold{n} · \bold{a}。 $
$D = -Ax_a - By_a - Cz_a = -\bold{n} · \bold{a}.  $  

This suggests the form:
这建议采用以下形式：
$f(\bold{p}) = \bold{n} · \bold{p} - \bold{n} · \bold{a} = \bold{n} · (\bold{p} - \bold{a}) = 0,  $

which is the same as Equation (12.1) once you recall that $\bold{n}$ is computed using the cross product. Which form of the plane equation you use and whether you store only the vertices, $\bold{n}$ and the vertices, or $\bold{n}$, $D$, and the vertices, is probably a matter of taste—a classic time-storage tradeoff that will be settled best by profiling. For debugging, using Equation (12.1) is probably the best.
一旦您回想起 $\bold{n}$ 是使用叉积计算的，它就与方程 (12.1) 相同。 使用哪种形式的平面方程以及是否仅存储顶点、$\bold{n}$ 和顶点，或者 $\bold{n}$、$D$ 和顶点，可能是一个品味问题 ——一个经典的时间存储权衡，最好通过分析来解决。 对于调试，使用方程（12.1）可能是最好的。

The only issue that prevents the code above from working in general is that one cannot guarantee that a triangle can be uniquely classified on one side of a plane or the other. It can have two vertices on one side of the plane and the third on the other. Or it can have vertices on the plane. This is handled by splitting the triangle into smaller triangles using the plane to “cut” them.
阻止上述代码正常工作的唯一问题是，无法保证三角形可以唯一地分类在平面的一侧或另一侧。 它可以在平面的一侧有两个顶点，在另一侧有第三个顶点。 或者它可以在平面上有顶点。 这是通过使用平面“切割”三角形将三角形分割成更小的三角形来处理的。

### 12.4.2 Building the Tree 构建树

If none of the triangles in the dataset cross each other’s planes, so that all triangles are on one side of all other triangles, a BSP tree that can be traversed using the code above can be built using the following algorithm:
如果数据集中没有一个三角形彼此相交，因此所有三角形都位于所有其他三角形的一侧，则可以使用以下算法构建可以使用上述代码遍历的 BSP 树：

> 		tree-root = node($T_1$)
> 		for $i ∈ {2, . . . , N}$ do
> 			tree-root.add($T_i$)
> 	function add ( triangle T )
> 		if (f($\bold{a}$) < 0 and f($\bold{b}$) < 0 and f($\bold{c}$) < 0) then
> 			if (negative subtree is empty) then
> 				negative-subtree = node(T)
> 			else
> 				negative-subtree.add (T)
> 		else if (f($\bold{a}$) > 0 and f($\bold{b}$) > 0 and f($\bold{c}$) > 0) then
> 			if positive subtree is empty then
> 				positive-subtree = node(T)
> 			else
> 				positive-subtree.add (T)
> 		else
> 			we have assumed this case is impossible  

The only thing we need to fix is the case where the triangle crosses the dividing plane, as shown in Figure 12.37. Assume, for simplicity, that the triangle has vertices $\bold{a}$ and $\bold{b}$ on one side of the plane, and vertex $\bold{c}$ is on the other side. In this case, we can find the intersection points $\bold{A}$ and $\bold{B}$ and cut the triangle into three new triangles with vertices
我们唯一需要修复的是三角形与分割面相交的情况，如图 12.37 所示。 为简单起见，假设三角形的顶点 $\bold{a}$ 和 $\bold{b}$ 位于平面的一侧，顶点 $\bold{c}$ 位于平面的另一侧。 在这种情况下，我们可以找到交点 $\bold{A}$ 和 $\bold{B}$ 并将三角形切割成三个带有顶点的新三角形
$$
T_1 = (\bold{a}, \bold{b}, \bold{A}), \\
T_2 = (\bold{b}, \bold{B}, \bold{A}), \\
T_3 = (\bold{A}, \bold{B}, \bold{c}),
$$
![Figure 12.37](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.37.png)
Figure 12.37. When a triangle spans a plane, there will be one vertex on one side and two on the other.
图 12.37。 当三角形跨越一个平面时，一侧有一个顶点，另一侧有两个顶点。

as shown in Figure 12.38. This order of vertices is important so that the direction of the normal remains the same as for the original triangle. If we assume that $f(\bold{c}) < 0$, the following code could add these three triangles to the tree assuming the positive and negative subtrees are not empty:
如图12.38所示。 顶点的这种顺序很重要，这样法线的方向与原始三角形的法线方向保持相同。 如果我们假设 $f(\bold{c}) < 0$，则假设正子树和负子树不为空，以下代码可以将这三个三角形添加到树中：
$$
positive-subtree = node (T_1) \\
positive-subtree = node (T_2) \\
negative-subtree = node (T_3) \\
$$
![Figure 12.38](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.38.png)
Figure 12.38. When a triangle is cut, we break it into three triangles, none of which span the cutting plane.
图 12.38。 当一个三角形被切割时，我们把它分成三个三角形，三个三角形都不跨越切割平面。

A precision problem that will plague a naive implementation occurs when a vertex is very near the splitting plane. For example, if we have two vertices on one side of  the splitting plane and the other vertex is only an extremely small distance on the other side, we will create a new triangle almost the same as the old one, a triangle that is a sliver, and a triangle of almost zero size. It would be better to detect this as a special case and not split into three new triangles. One might expect this case to be rare, but because many models have tessellated planes and triangles with shared vertices, it occurs frequently, and thus must be handled carefully. Some simple manipulations that accomplish this are:
当顶点非常靠近分割平面时，就会出现困扰简单实现的精度问题。 例如，如果我们在分割平面的一侧有两个顶点，而另一个顶点在另一侧只有极小的距离，我们将创建一个与旧三角形几乎相同的新三角形，一个是条子的三角形 ，以及一个大小几乎为零的三角形。 最好将其检测为特殊情况，而不是将其分成三个新三角形。 人们可能认为这种情况很少见，但由于许多模型都具有细分平面和具有共享顶点的三角形，因此这种情况经常发生，因此必须小心处理。 完成此操作的一些简单操作是：

> function add( triangle T )
> 	$fa = f(\bold{a})$
> 	$fb = f(\bold{b})$
> 	$fc = f(\bold{c})$
> 	if $(abs(fa) < \epsilon)$ then
> 		fa = 0
> 	if $(abs(fb) < \epsilon)$ then
> 		fb = 0
> 	if $(abs(fc) < \epsilon)$ then
> 		fc = 0
> 	if ($fa ≤ 0$ and $fb ≤ 0$ and $fc ≤ 0$) then
> 		if (negative subtree is empty) then
> 			negative-subtree = node(T) 
> 		else
> 			negative-subtree.add(T )
> 	else if ($fa ≥ 0$ and $fb ≥ 0$ and $fc ≥ 0$) then
> 		if (positive subtree is empty) then
> 			positive-subtree = node(T)
> 		else
> 			positive-subtree.add(T)
> 	else
> 		cut triangle into three triangles and add to each side  

This takes any vertex whose $f$ value is within $\epsilon$ of the plane and counts it as positive or negative. The constant $\epsilon$ is a small positive real chosen by the user. The technique above is a rare instance where testing for floating-point equality is useful and works because the zero value is set rather than being computed. Comparing for equality with a computed floating-point value is almost never advisable, but we are not doing that.
这采用 $f$ 值在平面 $\epsilon$ 范围内的任何顶点，并将其计为正数或负数。 常数 $\epsilon$ 是用户选择的一个小的正实数。 上面的技术是一个罕见的实例，其中测试浮点相等性非常有用并且有效，因为零值是设置的而不是计算的。 与计算的浮点值进行比较是否相等几乎是不可取的，但我们不会这样做。

### 12.4.3 Cutting Triangles 切割三角形

Filling out the details of the last case “cut triangle into three triangles and add to each side” is straightforward, but tedious. We should take advantage of the BSP tree construction as a preprocess where highest efficiency is not key. Instead, we should attempt to have a clean compact code. A nice trick is to force many of the cases into one by ensuring that c is on one side of the plane and the other two vertices are on the other. This is easily done with swaps. Filling out the details in the final else statement (assuming the subtrees are nonempty for simplicity) gives:
填写最后一个案例“将三角形切成三个三角形并添加到每个边”的详细信息很简单，但很乏味。 我们应该利用 BSP 树构建作为预处理，其中最高效率不是关键。 相反，我们应该尝试拥有干净紧凑的代码。 一个不错的技巧是通过确保 c 位于平面的一侧而其他两个顶点位于另一侧，将许多情况强制合并为一个。 这可以通过交换轻松完成。 在最后的 else 语句中填写详细信息（为简单起见，假设子树非空）给出：

> if $(fa ∗ fc ≥ 0)$ then
> 	swap(fb, fc)
> 	swap$(\bold{b}, \bold{c})$
> 	swap(fa, fb)
> 	swap$(\bold{a}, \bold{b})$
> else if (fb ∗ fc ≥ 0) then
> 	swap(fa, fc)
> 	swap$(\bold{a}, \bold{c})$
> 	swap$(fa, fb)$
> 	swap($\bold{a}$, $\bold{b}$)
> compute $\bold{A}$
> compute $\bold{B}$
> $T_1 = (\bold{a}, \bold{b}, \bold{A})$
> $T_2 = (\bold{b}, \bold{B}, \bold{A})$
> $T_3 = (\bold{A}, \bold{B}, \bold{c})$
> if (fc ≥ 0) then
> 	negative-subtree.add($T_1$)
> 	negative-subtree.add($T_2$)
> 	positive-subtree.add($T_3$)
> else
> 	positive-subtree.add($T_1$)
> 	positive-subtree.add($T_2$)
> 	negative-subtree.add($T_3$)  

This code takes advantage of the fact that the product of a and b are positive if they have the same sign—thus, the first if statement. If vertices are swapped, we must do two swaps to keep the vertices ordered counterclockwise. Note that exactly one of the vertices may lie exactly on the plane, in which case the code above will work, but one of the generated triangles will have zero area. This can be handled by ignoring the possibility, which is not that risky, because the rasterization code must handle zero-area triangles in screen space (i.e., edge-on triangles). You can also add a check that does not add zero-area triangles to the tree. Finally, you can put in a special case for when exactly one of $fa$, $fb$, and $fc$ is zero which cuts the triangle into two triangles. 
此代码利用了这样一个事实：如果 a 和 b 具有相同的符号，则它们的乘积为正，因此是第一个 if 语句。 如果交换顶点，我们必须进行两次交换以保持顶点逆时针排序。 请注意，其中一个顶点可能恰好位于平面上，在这种情况下，上面的代码将起作用，但生成的三角形之一的面积将为零。 这可以通过忽略这种可能性来处理，这并没有那么危险，因为光栅化代码必须处理屏幕空间中的零面积三角形（即边缘三角形）。 您还可以添加一个不将零面积三角形添加到树中的检查。 最后，您可以添加一种特殊情况，即当 $fa$、$fb$ 和 $fc$ 中的一个正好为零时，将三角形切成两个三角形。

To compute $\bold{A}$ and $\bold{B}$, a line segment and implicit plane intersection is needed. For example, the parametric line connecting $\bold{a}$ and $\bold{c}$ is
为了计算 $\bold{A}$ 和 $\bold{B}$，需要线段和隐式平面相交。 例如，连接 $\bold{a}$ 和 $\bold{c}$ 的参数线为
$\bold{p}(t) = \bold{a} + t(\bold{c} - \bold{a}).  $

The point of intersection with the plane $\bold{n} · \bold{p} + D = 0$ is found by plugging $\bold{p}(t)$ into the plane equation:
将 $\bold{p}(t)$ 代入平面方程即可找到与平面 $\bold{n} · \bold{p} + D = 0$ 的交点： 
$\bold{n} · (\bold{a} + t(\bold{c} - \bold{a})) + D = 0,  $

and solving for $t$:
并求解$t$：
$$
t = −\frac{\bold{n} \cdot \bold{a} + D}{\bold{n} \cdot (\bold{c} - \bold{a})}
$$
Calling this solution $t_A$, we can write the expression for $\bold{A}$: 
调用这个解决方案$t_A$，我们可以编写$\bold{A}$的表达式：
$\bold{A} = \bold{a} + t_A(\bold{c} - \bold{a})  $

A similar computation will give $\bold{B}$. 
类似的计算将给出$\bold{B}$。

### 12.4.4 Optimizing the Tree 优化树

The efficiency of tree creation is much less of a concern than tree traversal because it is a preprocess. The traversal of the BSP tree takes time proportional to the number of nodes in the tree. (How well balanced the tree is does not matter.) There will be one node for each triangle, including the triangles that are created as a result of splitting. This number can depend on the order in which triangles are added to the tree. For example, in Figure 12.39, if $T_1$ is the root, there will be two nodes in the tree, but if $T_2$ is the root, there will be more nodes, because $T_1$ will be split.
树创建的效率远不如树遍历那么重要，因为它是一个预处理。 遍历 BSP 树所需的时间与树中节点的数量成正比。 （树的平衡程度如何并不重要。）每个三角形都有一个节点，包括由于分裂而创建的三角形。 该数字取决于三角形添加到树中的顺序。 例如，在图12.39中，如果$T_1$是根，树中将有两个节点，但如果$T_2$是根，则会有更多节点，因为$T_1$将被分裂。
![Figure 12.39](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.39.png)
Figure 12.39. Using $T_1$ as the root of a BSP tree will result in a tree with two nodes. Using $T_2$ as the root will require a cut and thus make a larger tree.
图 12.39。 使用 $T_1$ 作为 BSP 树的根将生成具有两个节点的树。 使用 $T_2$ 作为根需要进行切割，从而形成更大的树。

It is difficult to find the “best” order of triangles to add to the tree. For N triangles, there are N! orderings that are possible. So trying all orderings is not usually feasible. Alternatively, some predetermined number of orderings can be tried from a random collection of permutations, and the best one can be kept for the final tree.
很难找到添加到树中的三角形的“最佳”顺序。 对于 N 个三角形，有 N 个！ 可能的订单。 因此尝试所有订单通常是不可行的。 或者，可以从随机排列集合中尝试一些预定数量的排序，并且可以为最终树保留最好的排序。

The splitting algorithm described above splits one triangle into three triangles. It could be more efficient to split a triangle into a triangle and a convex quadrilateral. This is probably not worth it if all input models have only triangles, but would be easy to support for implementations that accommodate arbitrary polygons.
上述分割算法将一个三角形分割成三个三角形。 将三角形分割成三角形和凸四边形可能会更有效。 如果所有输入模型都只有三角形，这可能不值得，但很容易支持容纳任意多边形的实现。

## 12.5 Tiling Multidimensional Arrays 平铺多维数组

Effectively utilizing the memory hierarchy is a crucial task in designing algorithms for modern architectures. Making sure that multidimensional arrays have data in a “nice” arrangement is accomplished by tiling, sometimes also called bricking. A traditional 2D array is stored as a 1D array together with an indexing mechanism; for example, an $N_x$ by $N_y$ array is stored in a 1D array of length $N_xN_y$ and the 2D index $(x, y)$ (which runs from $(0, 0)$ to $(N_x −1, N_y −1)$) maps to the 1D index (running from 0 to $N_xN_y − 1$) using the formula
有效利用内存层次结构是设计现代架构算法的一项关键任务。 确保多维数组的数据以“良好”的方式排列是通过平铺（有时也称为分砖）来完成的。 传统的二维数组与索引机制一起存储为一维数组； 例如，$N_x$ by $N_y$ 数组存储在长度为 $N_xN_y$ 的一维数组中，二维索引为 $(x, y)$（从 $(0, 0)$ 到 $(N_x - 1, N_y −1)$) 使用以下公式映射到一维索引（从 0 到 $N_xN_y − 1$）
$index = x + N_xy.  $

An example of how that memory lays out is shown in Figure 12.40. A problem with this layout is that although two adjacent array elements that are in the same row are next to each other in memory, two adjacent elements in the same column will be separated by $N_x$ elements in memory. This can cause poor memory locality for large $N_x$. The standard solution to this is to use tiles to make memory locality for rows and columns more equal. An example is shown in Figure 12.41 where 2 × 2 tiles are used. The details of indexing such an array are discussed in the next section. A more complicated example, with two levels of tiling on a 3D array, is covered after that.
图 12.40 显示了该内存布局的示例。 这种布局的一个问题是，虽然同一行中的两个相邻数组元素在内存中彼此相邻，但同一列中的两个相邻元素在内存中将被 $N_x$ 个元素分隔开。 这可能会导致较大的 $N_x$ 的内存局部性较差。 对此的标准解决方案是使用切片来使行和列的内存局部性更加平等。 图 12.41 显示了一个使用 2 × 2 块的示例。 下一节将讨论对此类数组进行索引的详细信息。 之后介绍了一个更复杂的示例，在 3D 阵列上有两层平铺。
![Figure 12.40](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.40.png)
Figure 12.40. The memory layout for an untiled 2D array with $N_x = 4$ and $N_y = 3$.
图 12.40。 $N_x = 4$ 和 $N_y = 3$ 的无齿二维数组的内存布局。

![Figure 12.41](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.41.png)
Figure 12.41. The memory layout for a tiled 2D array with $N_x = 4$ and $N_y = 3$ and 2 × 2 tiles. Note that padding on the top of the array is needed because $N_y$ is not a multiple of the tile size two.
图 12.41。 平铺二维数组的内存布局，其中 $N_x = 4$ 和 $N_y = 3$ 以及 2 × 2 个平铺。 请注意，需要在数组顶部进行填充，因为 $N_y$ 不是图块大小 2 的倍数。

A key question is what size to make the tiles. In practice, they should be similar to the memory-unit size on the machine. For example, if we are using 16-bit (2-byte) data values on a machine with 128-byte cache lines, 8 × 8 tiles fit exactly in a cache line. However, using 32-bit floating-point numbers, which fit 32 elements to a cache line, 5 × 5 tiles are a bit too small and 6 × 6 tiles are a bit too large. Because there are also coarser-sized memory units such as pages, hierarchical tiling with similar logic can be useful.
一个关键问题是制作瓷砖的尺寸。 实际上，它们应该与机器上的内存单元大小相似。 例如，如果我们在具有 128 字节缓存行的机器上使用 16 位（2 字节）数据值，则 8 × 8 块正好适合缓存行。 然而，使用 32 位浮点数（可容纳 32 个元素到一个缓存行），5 × 5 块有点太小，6 × 6 块有点太大。 由于还存在尺寸较粗的内存单元（例如页面），因此具有类似逻辑的分层平铺可能会很有用。

### 12.5.1 One-Level Tiling for 2D Arrays 2D 数组的一级平铺

If we assume an $N_x×N_y$ array decomposed into square n×n tiles (Figure 12.42), then the number of tiles required is
如果我们假设 $N_x×N_y$ 数组分解为方形 n×n 个图块（图 12.42），则所需的图块数量为
$$
B_x = N_x/n, \\
B_y = N_y/n.
$$
![Figure 12.42](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 12.42.png)
Figure 12.42. A tiled 2D array composed of $B_x × B_y$ tiles each of size $n$ by $n$. 
图 12.42。 由 $B_x × B_y$ 组成的平铺二维数组将每个大小为 $n$ 的平铺为 $n$。

Here, we assume that $n$ divides $N_x$ and $N_y$ exactly. When this is not true, the array should be padded. For example, if $N_x = 15$ and $n = 4$, then $N_x$ should be changed to 16. To work out a formula for indexing such an array, we first find the tile indices $(b_x, b_y)$ that give the row/column for the tiles (the tiles themselves form a 2D array):
这里，我们假设 $n$ 正好整除 $N_x$ 和 $N_y$。 当这不成立时，应该填充数组。 例如，如果 $N_x = 15$ 且 $n = 4$，则 $N_x$ 应更改为 16。要计算出索引此类数组的公式，我们首先找到图块索引 $(b_x, b_y)$ 给出图块的行/列（图块本身形成一个 2D 数组）：
$b_x = x ÷ n, \\
b_y = y ÷ n,  $

where ÷ is integer division, e.g., $12 ÷ 5 = 2$. If we order the tiles along rows as shown in Figure 12.40, then the index of the first element of the tile $(b_x, b_y)$ is
其中 ÷ 是整数除法，例如 $12 ÷ 5 = 2$。 如果我们按行对图块进行排序，如图 12.40 所示，则图块 $(b_x, b_y)$ 的第一个元素的索引为
$index = n^2(B_xb_y + b_x).  $

The memory in that tile is arranged like a traditional 2D array as shown in Figure 12.41. The partial offsets $(x', y')$ inside the tile are
该图块中的内存排列方式类似于传统的 2D 数组，如图 12.41 所示。 图块内的部分偏移量 $(x', y')$ 为
$x' = x\ mod\ n, \\
y' = y\ mod\ n,  $

where mod is the remainder operator, e.g., $12 mod 5 = 2$. Therefore, the offset inside the tile is
其中 mod 是余数运算符，例如 $12 mod 5 = 2$。 因此，图块内部的偏移量为
$offset = y'n + x'$

Thus the full formula for finding the 1D index element $(x, y)$ in an $N_x × N_y$ array with $n × n$ tiles is
因此，在具有 $n × n$ 块的 $N_x × N_y$ 数组中查找一维索引元素 $(x, y)$ 的完整公式为
$index = n^2(B_xb_y + b_x) + y'n + x', \\
= n^2((N_x ÷ n)(y ÷ n) + x ÷ n) + (y\ mod\ n)n + (x\ mod\ n).  $  

This expression contains many integer multiplication, divide and modulus operations, which are costly on some processors. When $n$ is a power of two, these operations can be converted to bitshifts and bitwise logical operations. However, as noted above, the ideal size is not always a power of two. Some of the multiplications can be converted to shift/add operations, but the divide and modulus operations are more problematic. The indices could be computed incrementally, but this would require tracking counters, with numerous comparisons and poor branch prediction performance.
该表达式包含许多整数乘法、除法和模运算，这些运算在某些处理器上成本很高。 当$n$是2的幂时，这些运算可以转换为位移位和按位逻辑运算。 然而，如上所述，理想的大小并不总是 2 的幂。 一些乘法可以转换为移位/加法运算，但除法和模运算问题较多。 索引可以增量计算，但这需要跟踪计数器，需要进行大量比较并且分支预测性能较差。

However, there is a simple solution; note that the index expression can be written as
然而，有一个简单的解决方案； 请注意，索引表达式可以写为
$index = F_x(x) + F_y(y),  $

where
其中
$$
F_x(x) = n^2(x ÷ n) + (x\ mod\ n), \\
F_y(y) = n^2(N_x ÷ n)(y ÷ n) + (y\ mod\ n)n.
$$
We tabulate $F_x$ and $F_y$, and use $x$ and $y$ to find the index into the data array. These tables will consist of $N_x$ and $N_y$ elements, respectively. The total size of the tables will fit in the primary data cache of the processor, even for very large data set sizes.
我们将 $F_x$ 和 $F_y$ 制成表格，并使用 $x$ 和 $y$ 查找数据数组的索引。 这些表将分别由 $N_x$ 和 $N_y$ 元素组成。 表的总大小将适合处理器的主数据缓存，即使对于非常大的数据集大小也是如此。

### 12.5.2 Example: Two-Level Tiling for 3D Arrays 示例：3D 数组的两级平铺

Effective TLB utilization is also becoming a crucial factor in algorithm performance. The same technique can be used to improve TLB hit rates in a 3D array by creating m × m × m bricks of n × n × n cells. For example, a 40 × 20 × 19 volume could be decomposed into 4 × 2 × 2 macrobricks of 2 × 2 × 2 bricks of 5 × 5 × 5 cells. This corresponds to $m = 2$ and $n = 5$. Because 19 cannot be factored by $mn = 10$, one level of padding is needed. Empirically useful sizes are $m = 5$ for 16-bit datasets and $m = 6$ for float datasets.
有效的 TLB 利用率也正在成为算法性能的关键因素。 通过创建 n × n × n 单元的 m × m × m 块，可以使用相同的技术来提高 3D 阵列中的 TLB 命中率。 例如，40 × 20 × 19 的体积可以分解为 4 × 2 × 2 的宏块，2 × 2 × 2 的块，5 × 5 × 5 的单元。 这对应于 $m = 2$ 和 $n = 5$。 由于 19 无法被 $mn = 10$ 分解，因此需要一级填充。 根据经验，对于 16 位数据集，有用的大小为 $m = 5$；对于浮点数据集，有用的大小为 $m = 6$。

> TLB: translation lookaside buffer, a cache that is part of the virtual memory system.
> TLB：转换后备缓冲区，是虚拟内存系统一部分的高速缓存。

The resulting index into the data array can be computed for any $(x, y, z)$ triple with the expression
可以使用表达式计算任何 $(x, y, z)$ 三元组的数据数组结果索引
$$
index = ((x ÷ n) ÷ m)n^3m^3((N_z ÷ n) ÷ m)((N_y ÷ n) ÷ m) \\
+((y ÷ n) ÷ m)n^3m^3((N_z ÷ n) ÷ m) \\
+((z ÷ n) ÷ m)n^3m^3 \\
+((x ÷ n)\ mod\ m)n^3m^2 \\
+((y ÷ n)\ mod\ m)n^3m \\ 
+((z ÷ n)\ mod\ m)n^3 \\
+(x\ mod\ (n^2))n^2 \\
+(y\ mod\ n)n \\
+(z\ mod\ n), \\
$$
where $N_x$, $N_y$ and $N_z$ are the respective sizes of the dataset.
其中 $N_x$、$N_y$ 和 $N_z$ 分别是数据集的大小。

Note that, as in the simpler 2D one-level case, this expression can be written as
请注意，与更简单的 2D 单层情况一样，该表达式可以写为
$index = F_x(x) + F_y(y) + F_z(z),  $

where
其中
$$
F_x(x) = ((x ÷ n) ÷ m)n^3m^3((N_z ÷ n) ÷ m)((N_y ÷ n) ÷ m) \\
+((x ÷ n)\ mod\ m)n^3m^2 \\
+(x\ mod\ n)n^2, \\ \\ 

F_y(y) = ((y ÷ n) ÷ m)n^3m^3((N_z ÷ n) ÷ m) \\
+((y ÷ n)\ mod\ m)n^3m \\
+(y\ mod\ n)n, \\ \\ 

F_z(z) = ((z ÷ n) ÷ m)n^3m^3 \\
+((z ÷ n)\ mod\ m)n^3 \\
+(z\ mod\ n). \\
$$

## Frequently Asked Questions 经常问的问题

### Does tiling really make that much difference in performance? 平铺真的会对性能产生如此大的影响吗？

On some volume rendering applications, a two-level tiling strategy made as much as a factor-of-ten performance difference. When the array does not fit in main memory, it can effectively prevent thrashing in some applications such as image editing. 
在某些体渲染应用程序中，两级平铺策略造成的性能差异高达十倍。 当数组无法容纳在主存中时，它可以有效防止某些应用程序（例如图像编辑）中的抖动。

### How do I store the lists in a winged-edge structure? 如何将列表存储在翼缘结构中？

For most applications, it is feasible to use arrays and indices for the references. However, if many delete operations are to be performed, then it is wise to use linked lists and pointers. 
对于大多数应用程序，使用数组和索引作为引用是可行的。 然而，如果要执行很多删除操作，那么使用链表和指针是明智的。

## Notes 注释

The discussion of the winged-edge data structure is based on the course notes of Ching-Kuang Shene (Shene, 2003). There are smaller mesh data structures than winged-edge. The tradeoffs in using such structures is discussed in Directed Edges—A Scalable Representation for Triangle Meshes (Campagna, Kobbelt, & Seidel, 1998). The tiled-array discussion is based on Interactive Ray Tracing for Volume Visualization (S. Parker et al., 1999). A structure similar to the triangle neighbor structure is discussed in a technical report by Charles Loop (Loop, 2000). A discussion of manifolds can be found in an introductory topology text (Munkres, 2000). 
翼边数据结构的讨论基于 Ching-Kuang Shene 的课程笔记 (Shene, 2003)。 有比翼边更小的网格数据结构。 使用此类结构的权衡在《Directed Edges—A Scalable Representation for Triangle Meshes》（Campagna、Kobbelt 和 Seidel，1998）中进行了讨论。 平铺阵列的讨论基于体积可视化的交互式光线追踪（S. Parker 等人，1999）。 Charles Loop（Loop，2000）的技术报告中讨论了类似于三角形邻居结构的结构。 关于流形的讨论可以在介绍性拓扑文本中找到（Munkres，2000）。

## Exercises 练习

1. What is the memory difference for a simple tetrahedron stored as four independent triangles and one stored in a winged-edge data structure? 
   一个简单的四面体存储为四个独立的三角形和一个存储在翼边数据结构中的内存差异是什么？
1. Diagram a scene graph for a bicycle. 
   绘制自行车的场景图。
1. How many look-up tables are needed for a single-level tiling of an n-dimensional array? 
   n 维数组的单层平铺需要多少个查找表？
1. Given N triangles, what is the minimum number of triangles that could be added to a resulting BSP tree? What is the maximum number?
   给定 N 个三角形，可以添加到生成的 BSP 树中的三角形的最小数量是多少？ 最大数量是多少？