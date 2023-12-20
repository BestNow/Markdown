# 9 Signal Processing 信号处理

In graphics, we often deal with functions of a continuous variable: an image is the first example you have seen, but you will encounter many more as you continue your exploration of graphics. By their nature, continuous functions can’t be directly represented in a computer; we have to somehow represent them using a finite number of bits. One of the most useful approaches to representing continuous functions is to use samples of the function: just store the values of the function at many different points and reconstruct the values in between when and if they are needed. 
在图形中，我们经常处理连续变量的函数：图像是您看到的第一个示例，但是当您继续探索图形时，您会遇到更多示例。 就其本质而言，连续函数不能直接在计算机中表示； 我们必须以某种方式使用有限数量的位来表示它们。 表示连续函数的最有用的方法之一是使用函数的样本：只需将函数的值存储在许多不同的点，并在需要时和需要时重建值。

You are by now familiar with the idea of representing an image using a two-dimensional grid of pixels—so you have already seen a sampled representation! Think of an image captured by a digital camera: the actual image of the scene that was formed by the camera’s lens is a continuous function of the position on the image plane, and the camera converted that function into a two-dimensional grid of samples. Mathematically, the camera converted a function of type $\R^2 → \bold{C}$ (where $\bold{C}$ is the set of colors) to a two-dimensional array of color samples, or a function of type $\Z^2 → \bold{C}$. 
您现在已经熟悉了使用二维像素网格表示图像的想法，因此您已经看到了采样表示！ 想象一下数码相机捕获的图像：由相机镜头形成的场景的实际图像是图像平面上位置的连续函数，并且相机将该函数转换为样本的二维网格。 从数学上讲，相机将 $\R^2 → \bold{C}$ 类型的函数（其中 $\bold{C}$ 是颜色集）转换为二维颜色样本数组，或者函数 输入 $\Z^2 → \bold{C}$。

Another example of a sampled representation is a 2D digitizing tablet, such as the screen of a tablet computer or a separate pen tablet used by an artist. In this case, the original function is the motion of the stylus, which is a time-varying 2D position, or a function of type $\R → \R^2$. The digitizer measures the position of the stylus at many points in time, resulting in a sequence of 2D coordinates, or a function of type $\Z → \R^2$. A motion capture system does exactly the same thing for a special marker attached to an actor’s body: it takes the 3D position of the marker over time ($\R → \R^3$) and makes it into a series of instantaneous position measurements ($\Z → \R^3$). 
采样表示的另一个示例是 2D 数字化平板电脑，例如平板电脑的屏幕或艺术家使用的单独的手写板。 在这种情况下，原始函数是触笔的运动，即随时间变化的 2D 位置，或者 $\R → \R^2$ 类型的函数。 数字化仪在多个时间点测量触笔的位置，从而产生一系列 2D 坐标，或 $\Z → \R^2$ 类型的函数。 动作捕捉系统对于附着在演员身体上的特殊标记执行完全相同的操作：它随着时间的推移获取标记的 3D 位置 ($\R → \R^3$) 并将其转换为一系列瞬时位置测量值 ($\Z → \R^3$)。

Going up in dimension, a medical CT scanner, used to non-invasively examine the interior of a person’s body, measures density as a function of position inside the body. The output of the scanner is a 3D grid of density values: it converts the density of the body $(\R^3 → \R)$ to a 3D array of real numbers $(\Z^3 → \R)$. 
在维度上，医用 CT 扫描仪用于非侵入性检查人体内部，测量密度作为体内位置的函数。 扫描仪的输出是密度值的 3D 网格：它将身体的密度 $(\R^3 → \R)$ 转换为实数 $(\Z^3 → \R)$ 的 3D 数组。

These examples seem different, but in fact they can all be handled using exactly the same mathematics. In all cases a function is being sampled at the points of a lattice in one or more dimensions, and in all cases we need to be able to reconstruct that original continuous function from the array of samples. 
这些例子看起来不同，但实际上它们都可以使用完全相同的数学来处理。 在所有情况下，函数都会在一维或多维的点阵点处进行采样，并且在所有情况下，我们都需要能够从样本数组中重建原始连续函数。

From the example of a 2D image, it may seem that the pixels are enough, and we never need to think about continuous functions again once the camera has discretized the image. But what if we want to make the image larger or smaller on the screen, particularly by non-integer scale factors? It turns out that the simplest algorithms to do this perform badly, introducing obvious visual artifacts known as aliasing. Explaining why aliasing happens and understanding how to prevent it require the mathematics of sampling theory. The resulting algorithms are rather simple, but the reasoning behind them, and the details of making them perform well, can be subtle. 
从2D图像的例子来看，似乎像素已经足够了，一旦相机将图像离散化，我们就不再需要考虑连续函数了。 但是，如果我们想要在屏幕上放大或缩小图像，特别是通过非整数比例因子，该怎么办？ 事实证明，最简单的算法执行此操作的效果很差，引入了明显的视觉伪像，称为混叠。 解释混叠发生的原因以及了解如何防止混叠需要采样理论的数学知识。 由此产生的算法相当简单，但其背后的推理以及使它们表现良好的细节可能很微妙。

Representing continuous functions in a computer is, of course, not unique to graphics; nor is the idea of sampling and reconstruction. Sampled representations are used in applications from digital audio to computational physics, and graphics is just one (and by no means the first) user of the related algorithms and mathematics. The fundamental facts about how to do sampling and reconstruction have been known in the field of communications since the 1920s and were stated in exactly the form we use them by the 1940s (Shannon & Weaver, 1964). 
当然，在计算机中表示连续函数并不是图形所独有的。 采样和重建的想法也不是。 采样表示用于从数字音频到计算物理的应用中，而图形只是相关算法和数学的一个（并且绝不是第一个）用户。 自 20 年代以来，有关如何进行采样和重建的基本事实在通信领域已为人所知，并且在 1940 年代以我们使用的形式准确地表述了（Shannon & Weaver，1964）。

This chapter starts by summarizing sampling and reconstruction using the concrete one-dimensional example of digital audio. Then, we go on to present the basic mathematics and algorithms that underlie sampling and reconstruction in one and two dimensions. Finally, we go into the details of the frequency-domain viewpoint, which provides many insights into the behavior of these algorithms.
本章首先使用数字音频的具体一维示例总结采样和重建。 然后，我们继续介绍一维和二维采样和重建的基础数学和算法。 最后，我们详细介绍频域观点，它为这些算法的行为提供了许多见解。

## 9.1 Digital Audio: Sampling in 1D 数字音频：一维采样

Although sampled representations had already been in use for years in telecommunications, the introduction of the compact disc in 1982, following the increased use of digital recording for audio in the previous decade, was the first highly visible consumer application of sampling. 
尽管采样表示法已在电信领域使用多年，但随着过去十年音频数字录音的使用不断增加，1982 年推出的光盘成为第一个高度可见的采样消费者应用。

In audio recording, a microphone converts sound, which exists as pressure waves in the air, into a time-varying voltage that amounts to a measurement of the changing air pressure at the point where the microphone is located. This electrical signal needs to be stored somehow so that it may be played back at a later time and sent to a loudspeaker that converts the voltage back into pressure waves by moving a diaphragm in synchronization with the voltage. 
在音频录制中，麦克风将空气中以压力波形式存在的声音转换为随时间变化的电压，该电压相当于麦克风所在位置变化的气压的测量值。 该电信号需要以某种方式存储，以便稍后回放并发送到扬声器，扬声器通过与电压同步移动隔膜将电压转换回压力波。

The digital approach to recording the audio signal (Figure 9.1) uses sampling: an analog-to-digital converter (A/D converter, or ADC) measures the voltage many thousand times per second, generating a stream of integers that can easily be stored on any number of media, say a disk on a computer in the recording studio, or transmitted to another location, say the memory in a portable audio player. At playback time, the data is read out at the appropriate rate and sent to a digital-to-analog converter (D/A converter, or DAC). The DAC produces a voltage according to the numbers it receives, and, provided we take enough samples to fairly represent the variation in voltage, the resulting electrical signal is, for all practical purposes, identical to the input. 
记录音频信号的数字方法（图 9.1）使用采样：模数转换器（A/D 转换器或 ADC）每秒测量电压数千次，生成易于存储的整数流 在任意数量的媒体上，例如录音室计算机上的磁盘，或传输到另一个位置，例如便携式音频播放器中的内存。 在播放时，数据以适当的速率读出并发送到数模转换器（D/A 转换器或 DAC）。 DAC 根据其接收到的数字产生电压，并且，如果我们采取足够的样本来公平地表示电压的变化，则出于所有实际目的，所得电信号与输入相同。
![Figure 9.1](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.1.png)
Figure 9.1. Sampling and reconstruction in digital audio.  
图 9.1. 数字音频中的采样和重建。

It turns out that the number of samples per second required to end up with a good reproduction depends on how high-pitched the sounds are that we are trying to record. A sample rate that works fine for reproducing a string bass or a kick drum produces bizarre-sounding results if we try to record a piccolo or a cymbal; but those sounds are reproduced just fine with a higher sample rate. To avoid these undersampling artifacts the digital audio recorder filters the input to the ADC to remove high frequencies that can cause problems. 
事实证明，最终获得良好再现效果所需的每秒样本数取决于我们尝试录制的声音的高音调。 如果我们尝试录制短笛或铙钹，那么适合再现低音提琴或底鼓的采样率会产生听起来很奇怪的结果； 但这些声音可以通过更高的采样率很好地再现。 为了避免这些欠采样伪影，数字录音机会对 ADC 的输入进行过滤，以消除可能导致问题的高频。

Another kind of problem arises on the output side. The DAC produces a voltage that changes whenever a new sample comes in, but stays constant until the next sample, producing a stair-step shaped graph. These stair-steps act like noise, adding a high-frequency, signal-dependent buzzing sound. To remove this reconstruction artifact, the digital audio player filters the output from the DAC to smooth out the waveform.
另一种问题出现在输出侧。 DAC 产生的电压在新样本进入时会发生变化，但在下一个样本到来之前保持恒定，从而产生阶梯形图形。 这些楼梯就像噪音一样，增加了高频、与信号相关的嗡嗡声。 为了消除这种重建伪影，数字音频播放器会对 DAC 的输出进行过滤以平滑波形。

### 9.1.1 Sampling Artifacts and Aliasing 采样伪像和混叠

The digital audio recording chain can serve as a concrete model for the sampling and reconstruction processes that happen in graphics. The same kind of undersampling and reconstruction artifacts also happen with images or other sampled signals in graphics, and the solution is the same: filtering before sampling and filtering again during reconstruction. 
数字音频记录链可以作为图形中发生的采样和重建过程的具体模型。 同样的欠采样和重建伪影也会发生在图像或图形中的其他采样信号上，解决方案是相同的：在采样之前进行滤波，并在重建期间再次进行滤波。

A concrete example of the kind of artifacts that can arise from too-low sample frequencies is shown in Figure 9.2. Here we are sampling a simple sine wave using two different sample frequencies: 10.8 samples per cycle on the top and 1.2 samples per cycle on the bottom. The higher rate produces a set of samples that obviously capture the signal well, but the samples resulting from the lower sample rate are indistinguishable from samples of a low-frequency sine wave—in fact, faced with this set of samples the low-frequency sinusoid seems the more likely interpretation.
图 9.2 显示了因采样频率过低而产生的伪像的具体示例。 在这里，我们使用两种不同的采样频率对简单的正弦波进行采样：顶部每个周期 10.8 个样本，底部每个周期 1.2 个样本。 较高的速率产生的一组样本显然可以很好地捕获信号，但较低采样率产生的样本与低频正弦波的样本无法区分 - 事实上，面对这组样本，低频正弦波 似乎更有可能的解释。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.2.png" alt="Figure 9.2" style="zoom:67%;" />
Figure 9.2. A sine wave (blue curve) sampled at two different rates. Top: at a high sample rate, the resulting samples (black dots) represent the signal well. Bottom: a lower sample rate produces an ambiguous result: the samples are exactly the same as would result from sampling a wave of much lower frequency (dashed curve).
图 9.2. 以两种不同速率采样的正弦波（蓝色曲线）。 上图：在高采样率下，生成的样本（黑点）很好地代表了信号。 底部：较低的采样率会产生不明确的结果：样本与对频率低得多的波进行采样所得到的结果完全相同（虚线）。

Once the sampling has been done, it is impossible to know which of the two signals—the fast or the slow sine wave—was the original, and therefore there is no single method that can properly reconstruct the signal in both cases. Because the high-frequency signal is “pretending to be” a low-frequency signal, this phenomenon is known as aliasing.
一旦完成采样，就不可能知道两个信号（快正弦波或慢速正弦波）中哪一个是原始信号，因此没有一种方法可以在这两种情况下正确重建信号。 由于高频信号“假装”为低频信号，因此这种现象称为混叠。

Aliasing shows up whenever flaws in sampling and reconstruction lead to artifacts at surprising frequencies. In audio, aliasing takes the form of odd-sounding extra tones—a bell ringing at 10KHz, after being sampled at 8KHz, turns into a 6KHz tone. In images, aliasing often takes the form of moire patterns ´ that result from the interaction of the sample grid with regular features in an image, for instance the window blinds in Figure 9.34.
每当采样和重建中的缺陷导致令人惊讶的频率的伪影时，就会出现混叠。 在音频中，混叠表现为听起来很奇怪的额外音调——以 10KHz 响起的铃声，在以 8KHz 采样后变成 6KHz 音调。 在图像中，混叠通常采用莫尔图案的形式，这是由样本网格与图像中的常规特征相互作用产生的，例如图 9.34 中的百叶窗。

Another example of aliasing in a synthetic image is the familiar stair-stepping on straight lines that are rendered with only black and white pixels (Figure 9.34). This is an example of small-scale features (the sharp edges of the lines) creating artifacts at a different scale (for shallow-slope lines the stair steps are very long). 
合成图像中锯齿的另一个例子是常见的仅用黑白像素渲染的直线上的阶梯（图 9.34）。 这是小尺度特征（线条的尖锐边缘）在不同尺度上创建伪影的示例（对于浅坡度线条，楼梯台阶非常长）。

The basic issues of sampling and reconstruction can be understood simply based on features being too small or too large, but some more quantitative questions are harder to answer: 
采样和重建的基本问题可以简单地根据特征太小或太大来理解，但一些更定量的问题很难回答：

- What sample rate is high enough to ensure good results? 
  什么样的采样率足够高才能确保良好的结果？
- What kinds of filters are appropriate for sampling and reconstruction? 
  什么样的滤波器适合采样和重建？
- What degree of smoothing is required to avoid aliasing?
  需要什么程度的平滑才能避免混叠？

Solid answers to these questions will have to wait until we have developed the theory fully in Section 9.5
这些问题的可靠答案必须等到我们在第 9.5 节中充分发展理论之后

## 9.2 Convolution 卷积

Before we discuss algorithms for sampling and reconstruction, we’ll first examine the mathematical concept on which they are based—convolution. Convolution is a simple mathematical concept that underlies the algorithms that are used for sampling, filtering, and reconstruction. It also is the basis of how we will analyze these algorithms later in the chapter.
在讨论采样和重建算法之前，我们将首先研究它们所基于的数学概念——卷积。 卷积是一个简单的数学概念，是用于采样、滤波和重建的算法的基础。 这也是我们在本章后面分析这些算法的基础。

Convolution is an operation on functions: it takes two functions and combines them to produce a new function. In this book, the convolution operator is denoted by a star: the result of applying convolution to the functions $f$ and $g$ is $f *g$. We say that $f$ is convolved with $g$, and $f*g$ is the convolution of $f$ and $g$. 
卷积是函数的运算：它采用两个函数并将它们组合起来产生一个新函数。 在本书中，卷积算子用星号表示：将卷积应用于函数$f$和$g$的结果是$f *g$。 我们说$f$与$g$进行卷积，$f*g$是$f$和$g$的卷积。

Convolution can be applied either to continuous functions (functions $f(x)$ that are defined for any real argument $x$) or to discrete sequences (functions $a[i]$ that are defined only for integer arguments $i$). It can also be applied to functions defined on one-dimensional, two-dimensional, or higher-dimensional domains (that is, functions of one, two, or more arguments). We will start with the discrete, one-dimensional case first, then continue to continuous functions and two- and three-dimensional functions.
卷积可以应用于连续函数（为任何实数参数 $x$ 定义的函数 $f(x)$）或离散序列（仅为整数参数 $i$ 定义的函数 $a[i]$） 。 它还可以应用于在一维、二维或更高维域上定义的函数（即一个、两个或多个参数的函数）。 我们将首先从离散的一维情况开始，然后继续讨论连续函数以及二维和三维函数。

For convenience in the definitions, we generally assume that the functions’ domains go on forever, though of course in practice they will have to stop somewhere, and we have to handle the endpoints in a special way.
为了定义方便，我们通常假设函数的域永远持续下去，尽管在实践中它们当然必须在某个地方停止，并且我们必须以特殊的方式处理端点。

### 9.2.1 Moving Averages 移动平均线

To get a basic picture of convolution, consider the example of smoothing a 1D function using a moving average (Figure 9.3). To get a smoothed value at any point, we compute the average of the function over a range extending a distance r in each direction. The distance r, called the radius of the smoothing operation, is a parameter that controls how much smoothing happens.
要了解卷积的基本情况，请考虑使用移动平均值平滑一维函数的示例（图 9.3）。 为了获得任意点的平滑值，我们计算函数在每个方向延伸距离 r 的范围内的平均值。 距离 r，称为平滑操作的半径，是控制平滑程度的参数。
![Figure 9.3](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.3.png)
Figure 9.3. Smoothing using a moving average. 
图 9.3. 使用移动平均线进行平滑。

We can state this idea mathematically for discrete or continuous functions. If we’re smoothing a continuous function $g(x)$, averaging means integrating $g$ over an interval and then dividing by the length of the interval:
我们可以用数学方法对离散或连续函数表达这个想法。 如果我们要平滑连续函数 $g(x)$，平均意味着在一个区间内对 $g$ 进行积分，然后除以区间的长度：
$$
h(x) = \frac{1}{2r}\int^{x+r}_{x-r}g(t)dt
$$
On the other hand, if we’re smoothing a discrete function $a[i]$, averaging means summing a for a range of indices and dividing by the number of values: 
另一方面，如果我们要平滑离散函数 $a[i]$，平均意味着对一系列索引求和 a，然后除以值的数量：
$$
c[i] = \frac{1}{2r + 1}\sum^{i+r}_{j=i-r}a[j] \ \ \ \ (9.1)
$$
In each case, the normalization constant is chosen so that if we smooth a constant function the result will be the same function. 
在每种情况下，都会选择归一化常数，以便如果我们平滑常数函数，结果将是相同的函数。

This idea of a moving average is the essence of convolution; the only difference is that in convolution the moving average is a weighted average.
移动平均的思想是卷积的本质； 唯一的区别是，在卷积中，移动平均值是加权平均值。

### 9.2.2 Discrete Convolution 离散卷积

We will start with the most concrete case of convolution: convolving a discrete sequence $a[i]$ with another discrete sequence $b[i]$. The result is a discrete sequence $(a*b)[i]$. The process is just like smoothing a with a moving average, but this time instead of equally weighting all samples within a distance $r$, we use a second sequence $b$ to give a weight to each sample (Figure 9.4). The value $b[i − j]$ gives the weight for the sample at position $j$, which is at a distance $i − j$ from the index i where we are evaluating the convolution. Here is the definition of $(a*b)$, expressed as a formula:
我们将从最具体的卷积案例开始：将离散序列 $a[i]$ 与另一个离散序列 $b[i]$ 进行卷积。 结果是离散序列$(a*b)[i]$。 这个过程就像用移动平均值平滑 a 一样，但这次我们不是对距离 $r$ 内的所有样本进行平均加权，而是使用第二个序列 $b$ 为每个样本赋予权重（图 9.4）。 值 $b[i − j]$ 给出位置 $j$ 处样本的权重，该位置距我们评估卷积的索引 i 的距离为 $i − j$。 这是 $(a*b)$ 的定义，用公式表示：
$$
(a * b)[i] = \sum_ja[j]b[i − j]. \ \ \ \ \ \ (9.2)
$$
By omitting bounds on $j$, we indicate that this sum runs over all integers (that is, from $−∞$ to $+∞$). Figure 9.4 illustrates how one output sample is computed, using the example of $b = \frac{1}{16}[. . . , 0, 1, 4, 6, 4, 1, 0, . . .]$—that is, $b[0] = \frac{6}{16}$ , $a[±1] = \frac{4}{16}$, etc.
通过省略$j$的界限，我们表示这个求和是对所有整数进行的（也就是说，从$−∞$到$+∞$）。图9.4说明了如何计算一个输出样本，使用的例子是$b = \frac{1}{16}[. . . , 0, 1, 4, 6, 4, 1, 0, . . .]$——也就是说，$b[0] = \frac{6}{16}$ , $a[±1] = \frac{4}{16}$，等等。

In graphics, one of the two functions will usually have finite support (as does the example in Figure 9.4), which means that it is nonzero only over a finite interval of argument values. If we assume that b has finite support, there is some radius r such that $b[k] = 0$ whenever $|k| > r$. In that case, we can write the sum above as 
在图形中，两个函数之一通常具有有限支持（如图 9.4 中的示例所示），这意味着它仅在参数值的有限区间内才非零。 如果我们假设 b 具有有限支持，则存在某个半径 r，使得每当 $|k| 时 $b[k] = 0$ > r$。 在这种情况下，我们可以将上面的总和写为
$(a*b)[i] = \sum^{i+r}_{j=i-r}a[j]b[i-j] \\$
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.4.png" alt="Figure 9.4" style="zoom:67%;" />
Figure 9.4. Computing one value in the discrete convolution of a sequence a with $a$ filter $b$ that has support five samples wide. Each sample in $a*b$ is an average of nearby samples in $a$, weighted by the values of $b$.
图 9.4. 使用支持五个样本宽的 $a$ 过滤器 $b$ 计算序列 a 的离散卷积中的一个值。 $a*b$ 中的每个样本都是 $a$ 中附近样本的平均值，并按 $b$ 的值加权。

and we can express the definition in code as
我们可以把这个定义用代码表示为

> function convolve(sequence a, filter b, int i)
> 	$s = 0$
> 	$r = b.radius$
> 	for $j = i - r$ to $i + r$ do
> 		$s = s + a[j]b[i - j]$
> 	return s  

#### Convolution Filters 卷积滤波器

Convolution is important because we can use it to perform filtering. Looking back at our first example of filtering, the moving average, we can now reinterpret that smoothing operation as convolution with a particular sequence. When we compute an average over some limited range of indices, that is the same as weighting the points in the range all identically and weighting the rest of the points with zeros. This kind of filter, which has a constant value over the interval where it is nonzero, is known as a box filter (because it looks like a rectangle if you draw its graph—see Figure 9.5). For a box filter of radius r the weight is $1/(2r + 1)$: 
卷积很重要，因为我们可以用它来进行过滤。回顾我们滤波的第一个例子，即移动平均线，我们现在可以将平滑操作重新解释为与特定序列的卷积。当我们在一些有限的指标范围内计算平均值时，这就等同于对范围内的点进行相同的加权，并对其余的点进行零加权。这种过滤器在非零区间内具有恒定值，称为框式过滤器(因为如果您绘制它的图形，它看起来像一个矩形，请参见图9.5)。对于半径为r的框过滤器，其权重为$1/(2r + 1)$:
![Figure 9.5](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.5.png)
Figure 9.5. A discrete box filter. 
图9.5. 离散盒滤波器。
$$
b[k] = \begin{cases}
\frac{1}{2r+1} \ \ \ \ \ (-r ≤ k ≤ r)\\
0 \ \ \ \ otherwise
\end{cases}
$$
If you substitute this filter into Equation (9.2), you will find that it reduces to the moving average in Equation (9.1). 
如果将此滤波器代入方程（9.2），您会发现它简化为方程（9.1）中的移动平均值。

As in this example, convolution filters are usually designed so that they sum to 1. That way, they don’t affect the overall level of the signal.
如本例所示，卷积滤波器通常设计为总和为 1。这样，它们就不会影响信号的整体电平。

Example (Convolution of a box and a step). For a simple example of filtering, let the signal be the step function 
示例（框和步骤的卷积）。 对于一个简单的滤波示例，令信号为阶跃函数 
$$
a_{i} = \begin{cases}
1 \ \ \ i ≥ 0 \\
1 \ \ \ i < 0
\end{cases}
$$
and the filter be the five-point box filter centered at zero, 
滤波器是以零为中心的五点箱式滤波器，
$$
b[k] = \frac{1}{5}
\begin{cases}
1 \ \ \ \ -2 ≤ k ≤ 2 \\
0 \ \ \ \ \ \ otherwise
\end{cases}
$$
What is the result of convolving $a$ and $b$? At a particular index $i$, as shown in Figure 9.6, the result is the average of the step function over the range from $i − 2$ to $i + 2$. If $i < −2$, we are averaging all zeros and the result is zero. If $i ≥ 2$, we are averaging all ones and the result is one. In between there are $i + 3$ ones, resulting in the value $\frac{i+3}{5}$ . The output is a linear ramp that goes from 0 to 1 over five samples: $\frac{1}{5}[. . . , 0, 0, 1, 2, 3, 4, 5, 5, . . .]$.
$a$ 和 $b$ 卷积的结果是什么？ 在特定索引 $i$ 处，如图 9.6 所示，结果是从 $i − 2$ 到 $i + 2$ 范围内阶跃函数的平均值。 如果 $i < −2$，我们对所有零进行平均，结果为零。 如果 $i ≥ 2$，我们对所有 1 进行平均，结果为 1。 中间有 $i + 3$ 个，结果为 $\frac{i+3}{5}$ 值。 输出是一个线性斜坡，在五个样本中从 0 到 1：$\frac{1}{5}[. . . , 0, 0, 1, 2, 3, 4, 5, 5, . . .]$.
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.6.png" alt="Figure 9.6" style="zoom:80%;" />
Figure 9.6. Discrete convolution of a box function with a step function. 
图 9.6. 盒函数与阶跃函数的离散卷积。

#### Properties of Convolution 卷积的性质

The way we’ve written it so far, convolution seems like an asymmetric operation: $a$ is the sequence we’re smoothing, and $b$ provides the weights. But one of the nice properties of convolution is that it actually doesn’t make any difference which is which: the filter and the signal are interchangeable. To see this, just rethink the sum in Equation (9.2) with the indices counting from the origin of the filter $b$, rather than from the origin of $a$. That is, we replace $j$ with $i - k$. The result of this change of variable is 
到目前为止我们编写的方式，卷积似乎是一种不对称操作：$a$ 是我们正在平滑的序列，$b$ 提供权重。 但卷积的一个很好的特性是，它实际上没有任何区别：滤波器和信号是可以互换的。 要看到这一点，只需重新考虑等式 (9.2) 中的总和，其中索引从过滤器 $b$ 的原点计数，而不是从 $a$ 的原点计数。 也就是说，我们将 $j$ 替换为 $i - k$。 变量变化的结果是
$$
(a*b)[i] = \sum_ka[i − k]b[i − (i − k)] = \sum_kb[k]a[i − k]
$$
This is exactly the same as Equation (9.2) but with $a$ acting as the filter and $b$ acting as the signal. So for any sequences $a$ and $b$, $(a*b) = (b*a)$, and we say that convolution is a commutative operation.（You may have noticed that one of the functions in the convolution sum seems to be flipped over— that is, $b[k]$ gives the weight for the sample $k$ units earlier in the sequence, while $b[−k]$ gives the weight for the sample $k$ units later in the sequence. The reason for this has to do with ensuring associativity; see Exercise 4. Most of the filters we use are symmetric, so you hardly ever need to worry about this.）
这与方程 (9.2) 完全相同，但 $a$ 充当滤波器，$b$ 充当信号。 所以对于任意序列$a$和$b$，$(a*b) = (b*a)$，我们说卷积是一种交换运算。（你可能已经注意到，卷积和中的函数之一 似乎被翻转了——也就是说，$b[k]$ 给出了序列中较早的样本 $k$ 单位的权重，而 $b[−k]$ 给出了序列中较晚的样本 $k$ 单位的权重 序列。 这样做的原因与确保关联性有关。 请参见练习 4。我们使用的大多数滤波器都是对称的，因此您几乎不需要担心这一点。）

More generally, convolution is a “multiplication-like” operation. Like multiplication or addition of numbers or functions, neither the order of the arguments nor the placement of parentheses affects the result. Also, convolution relates to addition in the same way that multiplication does. To be precise, convolution is commutative and associative, and it is distributive over addition.
更一般地说，卷积是一种“类似乘法”的运算。 与数字或函数的乘法或加法一样，参数的顺序和括号的位置都不影响结果。 此外，卷积与加法的关系与乘法的关系相同。 准确地说，卷积是可交换的和结合的，并且对加法是分配的。
$$
commutative: (a * b)[i] = (b * a)[i] \\
associative: (a * (b * c))[i] = ((a * b) * c)[i] \\
distributive: (a * (b + c))[i] = (a * b + a * c)[i]
$$
These properties are very natural if we think of convolution as being like multiplication, and they are very handy to know about because they can help us save work by simplifying convolutions before we actually compute them. For instance, suppose we want to take a sequence a and convolve it with three filters, $b_1$, $b_2$, and $b_3$—that is, we want $((a*b_1)*b_2)*b_3$. If the sequence is long and the filters are short (that is, they have small radii), it is much faster to first convolve the three filters together (computing $b_1*b_2*b_3$) and finally to convolve the result with the signal, computing $a*(b_1*b_2*b_3)$, which we know from associativity gives the same result.
如果我们将卷积视为乘法，那么这些属性是非常自然的，并且它们非常容易了解，因为它们可以帮助我们在实际计算卷积之前通过简化卷积来节省工作量。 例如，假设我们想要获取一个序列 a 并将其与三个过滤器 $b_1$、$b_2$ 和 $b_3$ 进行卷积，也就是说，我们需要 $((a*b_1)*b_2)*b_3$。 如果序列很长并且滤波器很短（即它们的半径很小），那么首先将三个滤波器卷积在一起（计算 $b_1*b_2*b_3$），最后将结果与信号进行卷积要快得多 ，计算 $a*(b_1*b_2*b_3)$，我们从结合性知道它会给出相同的结果。

A very simple filter serves as an identity for discrete convolution: it is the discrete filter of radius zero, or the sequence $d[i] = . . . , 0, 0, 1, 0, 0, . . .$ (Figure 9.7). If we convolve d with a signal a, there will be only one nonzero term in the sum:
一个非常简单的滤波器作为离散卷积的恒等式:它是半径为零的离散滤波器，或者序列($d[i] = . . . , 0, 0, 1, 0, 0, . . .$图9.7)。如果我们将d与信号a进行卷积，那么和中只有一个非零项:
![Figure 9.7](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.7.png)
Figure 9.7. The discrete identity filter. 
图9.7. 离散身份过滤器。
$$
(a*d)[i] =\sum^{j=i}_{j=i}a[j]d[i − j] = a[i]
$$
So clearly, convolving a with d just gives back a again. The sequence d is known as the discrete impluse. It is occasionally useful in expressing a filter: for instance, the process of smoothing a signal a with a filter b and then subtracting that from the original could be expressed as a single convolution with the filter $d − b$:
很明显，将 a 与 d 进行卷积只会再次返回 a。 序列 d 称为离散脉冲。 它有时在表达滤波器时很有用：例如，用滤波器 b 平滑信号 a，然后从原始信号中减去该信号的过程可以表示为与滤波器 $d − b$ 的单个卷积：
$c = a - a*b = a*d - a*b = a*(d - b).  $

### 9.2.3 Convolution as a Sum of Shifted Filters 卷积作为移位滤波器的总和

There is a second, entirely equivalent, way of interpreting Equation (9.2). Looking at the samples of $a*b$ one at a time leads to the weighted-average interpretation that we have already seen. But if we omit the $[i]$, we can instead think of the sum as adding together entire sequences. One piece of notation is required to make this work: if $b$ is a sequence, then the same sequence shifted to the right by j places is called $b_{→j}$ (Figure 9.8):
还有第二种完全等价的解释方程（9.2）的方法。 一次查看 $a*b$ 的样本会得出我们已经看到的加权平均解释。 但如果我们省略 $[i]$，我们可以将总和视为将整个序列加在一起。 需要一种符号来完成这项工作：如果 $b$ 是一个序列，那么向右移动 j 个位置的同一序列称为 $b_{→j}$ （图 9.8）：
$b_{→j}[i] = b[i - j].  $

![Figure 9.8](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.8.png)
Figure 9.8. Shifting a sequence b to get $b_{→j}$.
图 9.8. 移动序列 b 得到 $b_{→j}$。

Then, we can write Equation (9.2) as a statement about the whole sequence $(a*b)$ rather than element-by-element: 
然后，我们可以将方程（9.2）写为关于整个序列 $(a*b)$ 的陈述，而不是逐个元素：
$(a*b) = \sum_ja[j]b_{→j}.  $

Looking at it this way, the convolution is a sum of shifted copies of $b$, weighted by the entries of $a$ (Figure 9.9). Because of commutativity, we can pick either $a$ or $b$ as the filter; if we choose $b$, then we are adding up one copy of the filter for every sample in the input.
从这个角度来看，卷积是 $b$ 的移位副本的总和，并由 $a$ 的条目加权（图 9.9）。 由于交换律，我们可以选择 $a$ 或 $b$ 作为过滤器； 如果我们选择 $b$，那么我们将为输入中的每个样本添加一份过滤器副本。
![Figure 9.9](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.9.png)
Figure 9.9. Discrete convolution as a sum of shifted copies of the filter. 
图 9.9. 离散卷积作为滤波器的移位副本的总和。

### 9.2.4 Convolution with Continuous Functions 与连续函数的卷积

While it is true that discrete sequences are what we actually work with in a computer program, these sampled sequences are supposed to represent continuous functions, and often we need to reason mathematically about the continuous functions in order to figure out what to do. For this reason, it is useful to define convolution between continuous functions and also between continuous and discrete functions.
虽然离散序列确实是我们在计算机程序中实际使用的，但这些采样序列应该表示连续函数，并且通常我们需要对连续函数进行数学推理，以便弄清楚要做什么。 因此，定义连续函数之间以及连续函数和离散函数之间的卷积很有用。 

The convolution of two continuous functions is the obvious generalization of Equation (9.2), with an integral replacing the sum:
两个连续函数的卷积是方程（9.2）的明显推广，用积分代替和：
$$
(f*g)(x) = 	\int^{+∞}_{-∞}f(t)g(x − t) dt. \ \ \ \ \ \ \ \  (9.3)
$$
One way of interpreting this definition is that the convolution of $f$ and $g$, evaluated at the argument $x$, is the area under the curve of the product of the two functions  after we shift $g$ so that $g(0)$ lines up with $f(t)$. Just like in the discrete case, the convolution is a moving average, with the filter providing the weights for the average (see Figure 9.10).
解释此定义的一种方法是，$f$ 和 $g$ 的卷积（在参数 $x$ 处求值）是我们移动 $g$ 后两个函数的乘积曲线下的面积，使得 $g (0)$ 与 $f(t)$ 对齐。 就像离散情况一样，卷积是移动平均值，滤波器提供平均值的权重（见图 9.10）。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.10.png" alt="Figure 9.10" style="zoom:67%;" />
Figure 9.10. Continuous convolution. 
图 9.10. 连续卷积。

Like discrete convolution, convolution of continuous functions is commutative and associative, and it is distributive over addition. Also as with the discrete case, the continuous convolution can be seen as a sum of copies of the filter rather than the computation of weighted averages. Except, in this case, there are infinitely many copies of the filter $g$:
与离散卷积一样，连续函数的卷积是可交换的和结合的，并且对加法是分配的。 与离散情况一样，连续卷积可以看作是滤波器副本的总和，而不是加权平均值的计算。 除了在这种情况下，过滤器 $g$ 有无限多个副本：
$(f*g) =  \int^{+∞}_{-∞}f(t)g_{→t}dt.  $

Example (Convolution of two box functions). Let $f$ be a box function:
示例（两个框函数的卷积）。 令 $f$ 为盒函数：
$$
f(x) = \begin{cases}
1 \ \ \ \ \ -\frac{1}{2} ≤ x < \frac{1}{2} \\
0 \ \ \ \ \ otherwise
\end{cases}
$$
Then what is $f*f$ ? The definition (Equation 9.3) gives
那么 $f*f$ 是什么？ 定义（公式 9.3）给出
$(f*f)(x) =  \int^{∞}_{-∞}f(t)f(x - t) dt.  $

Figure 9.11 shows the two cases of this integral. The two boxes might have zero overlap, which happens when $x ≤ −1$ or $x ≥ 1$; in this case the result is zero. When $−1 < x < 1$, the overlap depends on the separation between the two boxes, which is $|x|$; the result is $1 − |x|$. So
图 9.11 显示了该积分的两种情况。 当 $x ≤ −1$ 或 $x ≥ 1$ 时，两个框可能有零重叠； 在这种情况下，结果为零。 当$−1 < x < 1$时，重叠取决于两个盒子之间的间隔，即$|x|$； 结果是 $1 − |x|$。 所以
![Figure 9.11](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.11.png)
Figure 9.11. Convolving two boxes yields a tent function. 
图 9.11.  对两个盒子进行卷积会产生一个帐篷函数
$$
(f*f)(x) = \begin{cases}
1 - |x| \ \ \ \ \ -1 < x < 1 \\
0 \ \ \ \ \ \ otherwise
\end{cases}
$$
This function, known as the tent function, is another common filter (see Section 9.3.1).
该函数称为帐篷函数，是另一个常见的过滤器（参见第 9.3.1 节）。

#### The Dirac Delta Function 狄拉克 Delta 函数

In discrete convolution, we saw that the discrete impulse $d$ acted as an identity: $d*a = a$. In the continuous case, there is also an identity function, called the Dirac impulse or Dirac delta function, denoted $δ(x)$.
在离散卷积中，我们看到离散脉冲 $d$ 充当恒等式：$d*a = a$。 在连续情况下，还有一个恒等函数，称为狄拉克脉冲或狄拉克δ函数，表示为$δ(x)$。

Intuitively, the delta function is a very narrow, very tall spike that has infinitesimal width but still has area equal to 1 (Figure 9.12). The key defining property of  the delta function is that multiplying it by a function selects out the value exactly at zero: 
直观上，Delta 函数是一个非常窄、非常高的尖峰，其宽度无穷小，但面积仍等于 1（图 9.12）。 Delta 函数的关键定义属性是，将其乘以一个函数会选择恰好为零的值：
$$
\int^∞_{-∞}δ(x)f(x)dx = f(0).
$$
![Figure 9.12](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.12.png)
Figure 9.12. The Dirac delta function $δ(x)$. 
图 9.12. 狄拉克δ函数$δ(x)$。

The delta function does not have a well-defined value at $0$ (you can think of its value loosely as $+∞$), but it does have the value $δ(x) = 0$ for all $x ≠ 0$. 
Delta 函数在 $0$ 处没有明确定义的值（您可以将其值宽松地视为 $+∞$），但对于所有 $x ≠ 0$，它的值确实为 $δ(x) = 0$ 。

From this property of selecting out single values, it follows that the delta function is the identity for continuous convolution (Figure 9.13), because convolving $δ$ with any function $f$ yields
从选择单个值的这个性质可以看出，delta 函数是连续卷积的恒等式（图 9.13），因为将 $δ$ 与任何函数 $f$ 进行卷积会产生
$(δ*f)(x) = \int^{∞}_{-∞}δ(t)f(x - t)dt = f(x).  $
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.13.png" alt="Figure 9.13" style="zoom:67%;" />
Figure 9.13. Convolving a function with $δ(x)$ returns a copy of the same function.
图 9.13. 将函数与 $δ(x)$ 进行卷积会返回同一函数的副本。

So $δ*f = f$ (and because of commutativity $f*δ = f$ also). 
所以$δ*f = f$（并且由于交换律$f*δ = f$）。

### 9.2.5 Discrete-Continuous Convolution 离散连续卷积

There are two ways to connect the discrete and continuous worlds. One is sampling: we convert a continuous function into a discrete one by writing down the function’s value at all integer arguments and forgetting about the rest. Given a continuous function f(x), we can sample it to convert to a discrete sequence $a[i]$:
有两种方法可以连接离散世界和连续世界。 一种是采样：我们通过记下函数在所有整数参数处的值并忘记其余部分，将连续函数转换为离散函数。 给定一个连续函数 f(x)，我们可以对其进行采样以转换为离散序列 $a[i]$：
$a[i] = f(i).  $

Going the other way, from a discrete function, or sequence, to a continuous function, is called reconstruction. This is accomplished using yet another form of convolution, the discrete-continuous form. In this case, we are filtering a discrete sequence $a[i]$ with a continuous filter $f(x)$:
相反，从离散函数或序列到连续函数，称为重构。 这是通过使用另一种形式的卷积（离散连续形式）来完成的。 在本例中，我们使用连续过滤器 $f(x)$ 过滤离散序列 $a[i]$：
$(a*f)(x) = \sum_ia[i]f(x - i).  $

The value of the reconstructed function $a*f$ at $x$ is a weighted sum of the samples $a[i]$ for values of $i$ near $x$ (Figure 9.14). The weights come from the filter $f$, which is evaluated at a set of points spaced one unit apart. For example, if $x = 5.3$ and $f$ has radius 2, f is evaluated at 1.3, 0.3, -0.7, and -1.7. Note that for discrete-continuous convolution we generally write the sequence first and the filter second, so that the sum is over integers.
$x$ 处的重构函数 $a*f$ 的值是 $x$ 附近 $i$ 值的样本 $a[i]$ 的加权和（图 9.14）。 权重来自过滤器 $f$，它在一组间隔一个单位的点上进行评估。 例如，如果 $x = 5.3$ 并且 $f$ 的半径为 2，则 f 的计算值为 1.3、0.3、-0.7 和 -1.7。 请注意，对于离散连续卷积，我们通常先写序列，然后写滤波器，以便总和超过整数。

<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.14.png" alt="Figure 9.14" style="zoom:67%;" />
Figure 9.14. Discrete-continuous convolution. 
图9.14. 离散连续卷积。

As with discrete convolution, we can put bounds on the sum if we know the filter’s radius, $r$, eliminating all points where the difference between $x$ and $i$ is at least $r$:
与离散卷积一样，如果我们知道滤波器的半径 $r$，我们可以对总和设置界限，从而消除 $x$ 和 $i$ 之间的差异至少为 $r$ 的所有点：
$$
(a*f)(x) = \sum^{\lfloor x + r \rfloor}_{i=\lceil x - r \rceil} a[i]f(x − i).
$$
Note, that if a point falls exactly at distance $r$ from $x$ (i.e., if $x − r$ turns out to be an integer), it will be left out of the sum. This is in contrast to the discrete case, where we included the point at $i − r$.
请注意，如果一个点恰好落在距 $x$ 的距离 $r$ 处（即，如果 $x − r$ 结果是一个整数），则它将被排除在总和之外。 这与离散情况相反，在离散情况下，我们将点包含在 $i − r$ 处。

Expressed in code, this is:
用代码来表达就是：

> function reconstruct(sequence a, filter f, real x)
> 	$s = 0$
> 	$r = f.radius$
> 	for $i = \lceil x - r\rceil$ to $\lfloor x + r\rfloor$ do
> 		$s = s + a[i]f(x - i)$
> 	return s  

As with the other forms of convolution, discrete-continuous convolution may be seen as summing shifted copies of the filter (Figure 9.15): 
与其他形式的卷积一样，离散连续卷积可以被视为对滤波器的移位副本求和（图 9.15）：
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.15.png" alt="Figure 9.15" style="zoom:67%;" />
Figure 9.15. Reconstruction (discrete-continuous convolution) as a sum of shifted copies of the filter.  
图 9.15. 重建（离散连续卷积）作为滤波器的移位副本的总和。
$$
(a*f) = \sum_i a[i]f_{→i}.
$$
Discrete-continuous convolution is closely related to splines. For uniform splines (a uniform B-spline, for instance), the parameterized curve for the spline is exactly the convolution of the spline’s basis function with the control point sequence (see Section 15.6.2).
离散连续卷积与样条密切相关。 对于均匀样条（例如均匀 B 样条），样条的参数化曲线正是样条的基函数与控制点序列的卷积（参见第 15.6.2 节）。

### 9.2.6 Convolution in More Than One Dimension 多维卷积

So far, everything we have said about sampling and reconstruction has been one-dimensional: there has been a single variable x or a single sequence index i. Many of the important applications of sampling and reconstruction in graphics, though, are applied to two-dimensional functions—in particular, to 2D images. Fortunately, the generalization of sampling algorithms and theory from 1D to 2D, 3D, and beyond is conceptually very simple.
到目前为止，我们所说的有关采样和重建的所有内容都是一维的：存在单个变量 x 或单个序列索引 i。 然而，图形中采样和重建的许多重要应用都应用于二维函数，特别是二维图像。 幸运的是，从 1D 到 2D、3D 等的采样算法和理论的推广在概念上非常简单。

Beginning with the definition of discrete convolution, we can generalize it to two dimensions by making the sum into a double sum:
从离散卷积的定义开始，我们可以通过将和变成双和来将其推广到二维：
$(a*b)[i, j] = \sum_{i'}\sum_{j'}a[i', j']b[i - i', j - j'].   \\$

If $b$ is a finitely supported filter of radius r (that is, it has $(2r + 1)^2$ values), then we can write this sum with bounds (Figure 9.16): 
如果 $b$ 是半径为 r 的有限支持滤波器（即，它具有 $(2r + 1)^2$ 值），那么我们可以将这个总和写为有界（图 9.16）：
$(a*b)[i, j] = \sum^{i+r}_{i'=i-r}\sum^{j+r}_{j'=j-r}a[i', j']b[i - i', j - j']   \\ $
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.16.png" alt="Figure 9.16" style="zoom:67%;" />
Figure 9.16. The weights for the nine input samples that contribute to the discrete convolution at point $(i, j)$ with a filter $b$ of radius 1. 
图 9.16. 九个输入样本的权重，有助于在点 $(i, j)$ 处使用半径为 1 的滤波器 $b$ 进行离散卷积。

and express it in code:
并用代码表达：

> function convolve2d(sequence2d a, filter2d b, int i, int j)
> 	$s = 0$
> 	$r = b.radius$
> 	for $i' = i − r$ to $i + r$ do
> 		for $j' = j − r$ to $j + r$ do
> 			$s = s + a[i'][j']b[i − i'][j − j']$
> 	return s

This definition can be interpreted in the same way as in the 1D case: each output sample is a weighted average of an area in the input, using the 2D filter as a “mask” to determine the weight of each sample in the average. 
这个定义可以用与 1D 情况相同的方式解释：每个输出样本是输入中某个区域的加权平均值，使用 2D 滤波器作为“掩模”来确定平均值中每个样本的权重。

Continuing the generalization, we can write continuous-continuous (Figure 9.17) and discrete-continuous (Figure 9.18) convolutions in 2D as well:
继续泛化，我们也可以在 2D 中编写连续-连续（图 9.17）和离散-连续（图 9.18）卷积：
![Figure 9.17](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.17.png)
Figure 9.17. The weight for an infinitesimal area in the input signal resulting from continuous convolution at $(x, y)$.
图 9.17. 输入信号中无穷小区域的权重，由 $(x, y)$ 处的连续卷积产生。

![Figure 9.18](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.18.png)
Figure 9.18. The weights for the 16 input samples that contribute to the discrete-continuous convolution at point $(x, y)$ for a reconstruction filter of radius 2. 
图 9.18. 16 个输入样本的权重，有助于半径为 2 的重建滤波器在点 $(x, y)$ 处的离散连续卷积。
$$
(f*g)(x, y) =\int\int f(x', y')g(x − x', y − y') dx' dy'; \\
(a*f)(x, y) = \sum_i\sum_j a[i, j]f(x − i, y − j). 
$$
In each case, the result at a particular point is a weighted average of the input near that point. For the continuous-continuous case, it is a weighted integral over a region centered at that point, and in the discrete-continuous case it is a weighted average of all the samples that fall near the point.
在每种情况下，特定点的结果是该点附近输入的加权平均值。对于连续连续的情况，它是在该点为中心的区域上的加权积分，而在离散连续的情况下，它是落在该点附近的所有样本的加权平均值。

Once we have gone from 1D to 2D, it should be fairly clear how to generalize further to 3D or even to higher dimensions.
一旦我们从 1D 过渡到 2D，如何进一步推广到 3D 甚至更高的维度就应该相当清楚了。

### 9.3 Convolution Filters 卷积滤波器

Now that we have the machinery of convolution, let’s examine some of the particular filters commonly used in graphics. 
现在我们已经掌握了卷积机制，让我们研究一下图形中常用的一些特定过滤器。

Each of the following filters has a natural radius, which is the default size to be used for sampling or reconstruction when samples are spaced one unit apart. In this section filters are defined at this natural size: for instance, the box filter has a natural radius of $\frac{1}{2}$, and the cubic filters have a natural radius of 2. We also arrange for each filter to integrate to $1: \int^{∞}_{x=0}f(x)dx = 1$, as required for sampling and reconstruction without changing a signal’s average value.
以下每个滤波器都有一个自然半径，这是当样本间隔一个单位时用于采样或重建的默认大小。 在本节中，过滤器定义为自然尺寸：例如，盒式过滤器的自然半径为 $\frac{1}{2}$，立方过滤器的自然半径为 2。我们还为每个过滤器进行了安排 积分到 $1：\int^{∞}_{x=0}f(x)dx = 1$，根据采样和重建的要求，而不改变信号的平均值。

As we will see in Section 9.4.3, some applications require filters of different sizes, which can be obtained by scaling the basic filter. For a filter $f(x)$, we can define a version of scale $s$:
正如我们将在第 9.4.3 节中看到的，某些应用程序需要不同大小的滤波器，这可以通过缩放基本滤波器来获得。 对于过滤器 $f(x)$，我们可以定义尺度 $s$ 的一个版本：
$f_s{x} = \frac{f(x/s)}{s}\\$

The filter is stretched horizontally by a factor of $s$, and then squashed vertically by a factor $\frac{1}{s}$ so that its area is unchanged. A filter that has a natural radius of $r$ and is used at scale s has a radius of support $sr$ (see Figure 9.20 below). 
过滤器在水平方向被拉伸$s$，然后在垂直方向被挤压$\frac{1}{s}$，这样它的面积是不变的。一个具有自然半径$r$并在尺度s上使用的滤波器具有支持半径$sr$(见下面的图9.20)。

![Figure 9.20](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.20.png)
Figure 9.20. The tent filter and two scaled versions. 
图 9.20。 帐篷过滤器和两个缩放版本。

### 9.3.1 A Gallery of Convolution Filters  卷积滤波器图库

#### The Box Filter 箱式过滤器

The box filter (Figure 9.19) is a piecewise constant function whose integral is equal to one. As a discrete filter, it can be written as 
箱式滤波器（图 9.19）是一个分段常数函数，其积分等于 1。 作为离散滤波器，它可以写为
$$
a_{box,r}[i] = \begin{cases}
1/(2r + 1) \ \ \  \ \ \ \ |i| ≤ r, \\
0 \ \ \ \ \ \ \ \ otherwise
\end{cases}
$$
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.19.png" alt="Figure 9.19" style="zoom:80%;" />
Figure 9.19. The discrete and continuous box filters.
图 9.19. 离散和连续箱式过滤器。

Note that for symmetry we include both endpoints.
请注意，为了对称，我们包括两个端点。

As a continuous filter, we write
作为连续过滤器，我们写
$$
f_{box, r}(x) = \begin{cases}
1/(2r) \ \ \ \ \ -r ≤ x < r \\
0 \ \ \ \ \ \ \ otherwise
\end{cases}
$$
In this case, we exclude one endpoint, which makes the box of radius 0.5 usable as a reconstruction filter. It is because the box filter is discontinuous that these boundary cases are important, and so for this particular filter we need to pay attention to them. We write just fbox for the natural radius of $r = \frac{1}{2}$.
在这种情况下，我们排除一个端点，这使得半径为 0.5 的盒子可用作重建滤波器。 正是因为盒式滤波器是不连续的，所以这些边界情况很重要，因此对于这个特定的滤波器我们需要注意它们。 我们只用 fbox 来表示 $r = \frac{1}{2}$ 的自然半径。

#### The Tent Filter 帐篷过滤器

The tent, or linear filter (Figure 9.20), is a continuous, piecewise linear function:
帐篷或线性滤波器（图 9.20）是一个连续的分段线性函数：
<img src="E:\持久化数据\笔记\Markdown\图形学\Fundamentals of Computer Graphics\Images\Figure 9.20.png" alt="Figure 9.20" style="zoom:80%;" />
Figure 9.20. The tent filter and two scaled versions.
图 9.20。 帐篷过滤器和两个缩放版本。
$$
f_{tent}(x) = \begin{cases}
1 - |x| \ \ \ \ |x| < 1 \\
0 \ \ \ \ \ \ \ otherwise
\end{cases}
$$
Its natural radius is 1. For filters, such as this one, that are at least $C^0$ (that is, there are no sudden jumps in the value, as there are with the box), we no longer need to separate the definitions of the discrete and continuous filters: the discrete filter is just the continuous filter sampled at the integers.
它的自然半径是 1。对于像这个这样的至少为 $C^0$ 的过滤器（也就是说，值不会像盒子那样突然跳跃），我们不再需要分离 离散滤波器和连续滤波器的定义：离散滤波器只是以整数采样的连续滤波器。

#### The Gaussian Filter 高斯滤波器 

The Gaussian function (Figure 9.21), also known as the normal distribution, is an important filter theoretically and practically. We’ll see more of its special properties as the chapter goes on:
高斯函数（图 9.21），也称为正态分布，是理论上和实践中重要的滤波器。 随着本章的继续，我们将看到更多它的特殊属性：
$$
f_g,σ(x) = \frac{1}{σ\sqrt{2π}}e^{-x^2/2σ^2}
$$
![Figure 9.21](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.21.png)
Figure 9.21. The Gaussian filter.
图 9.21。 高斯滤波器。

The parameter σ is called the standard deviation. The Gaussian makes a good sampling filter because it is very smooth; we’ll make this statement more precise later in the chapter.
参数 σ 称为标准差。 高斯滤波器是一个很好的采样滤波器，因为它非常平滑； 我们将在本章后面使这一说法更加精确。

The Gaussian filter does not have any particular natural radius; it is a useful sampling filter for a range of σ. The Gaussian also does not have a finite radius of support, although because of the exponential decay, its values rapidly become small enough to ignore. When necessary, then, we can trim the tails from the function by setting it to zero outside some radius r, resulting in a trimmed Gaussian. This means that the filter’s width and natural radius can vary depending on the application, and a trimmed Gaussian scaled by s is the same as an unscaled trimmed Gaussian with standard deviation sσ and radius sr. The best way to handle this in practice is to let σ and r be set as properties of the filter, fixed when the filter is specified, and then scale the filter just like any other when it is applied.
高斯滤波器没有任何特定的自然半径； 它对于 σ 范围来说是一个有用的采样过滤器。 高斯也没有有限的支持半径，尽管由于指数衰减，它的值很快变得小到可以忽略。 必要时，我们可以通过将函数在半径 r 之外设置为零来修剪函数的尾部，从而得到修剪后的高斯分布。 这意味着滤波器的宽度和自然半径可以根据应用而变化，并且按 s 缩放的修剪高斯与标准偏差 sσ 和半径 sr 的未缩放修剪高斯相同。 在实践中处理这个问题的最佳方法是让 σ 和 r 设置为过滤器的属性，在指定过滤器时固定，然后在应用时像任何其他过滤器一样缩放过滤器。

> Good starting points are σ = 1 and r = 3. 
> 好的起点是 σ = 1 和 r = 3。

#### The B-Spline Cubic Filter B 样条三次过滤器

Many filters are defined as piecewise polynomials, and cubic filters with four pieces (natural radius of 2) are often used as reconstruction filters. One such filter  is known as the B-spline filter (Figure 9.22) because of its origins as a blending function for spline curves (see Chapter 15):
许多滤波器被定义为分段多项式，并且四部分三次滤波器（自然半径为2）通常用作重建滤波器。 其中一种滤波器被称为 B 样条滤波器（图 9.22），因为它起源于样条曲线的混合函数（参见第 15 章）：
![Figure 9.22](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.22.png)
Figure 9.22. The B-spline filter.
图 9.22。 B 样条滤波器。
$$
f_B(x) = \frac{1}{6} \begin{cases}
-3(1 − |x|)^3 + 3(1 − |x|)^2 + 3(1 − |x|) + 1 \ \ \ \ \ -1 ≤ x ≤ 1 \\
(2 - |x|)^3 \ \ \ \ \ \ \ 1 ≤ |x| ≤ 2 \\
0 \ \ \ \ \ \ \ \ \ otherwise
\end{cases}
$$
Among piecewise cubics, the B-spline is special because it has continuous first and second derivatives—that is, it is $C^2$. A more concise way of defining this filter is $fB = f_{box} * f_{box} * f_{box} * f_{box}$; proving that the longer form above is equivalent is a nice exercise in convolution (see Exercise 3).
在分段三次中，B 样条比较特殊，因为它具有连续的一阶导数和二阶导数，即 $C^2$。 定义此过滤器的更简洁方法是 $fB = f_{box} * f_{box} * f_{box} * f_{box}$; 证明上面的较长形式是等效的是一个很好的卷积练习（参见练习 3）。

#### The Catmull-Rom Cubic Filter Catmull-Rom 立方滤波器

Another piecewise cubic filter named for a spline, the Catmull-Rom filter (Figure 9.23), has the value zero at $x = −2, −1, 1,$ and $2$, which means it will interpolate the samples when used as a reconstruction filter (Section 9.3.2):
另一个以样条命名的分段三次滤波器 Catmull-Rom 滤波器（图 9.23）在 $x = −2, −1, 1,$ 和 $2$ 处的值为零，这意味着当用作 重建滤波器（第 9.3.2 节）：
$$
f_C(x) = \frac{1}{2} \begin{cases}
-3(1 − |x|)^3 + 4(1 − |x|)^2 + (1 − |x|) \ \ \ \ \ \ -1 ≤ x ≤ 1 \\
(2 − |x|)^3 − (2 − |x|)^2 \ \ \ \ \ \ \ \ \ 1 ≤ |x| ≤ 2 \\ 
0 \ \ \ \ \ \ \ \ \ otherwise.
\end{cases}
$$
![Figure 9.23](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.23.png)
Figure 9.23. The CatmullRom filter. 
图 9.23。 CatmullRom 过滤器。

#### The Mitchell-Netravali Cubic Filter Mitchell-Netravali 立方滤波器

For the all-important application of resampling images, Mitchell and Netravali (Mitchell & Netravali, 1988) made a study of cubic filters and recommended one partway between the previous two filters as the best all-around choice (Figure 9.24). It is simply a weighted combination of the previous two filters:
对于图像重采样这一至关重要的应用，Mitchell 和 Netravali（Mitchell & Netravali，1988）对三次滤波器进行了研究，并推荐前两个滤波器之间的一个作为最佳全面选择（图 9.24）。 它只是前两个过滤器的加权组合：
$$
f_M(x) = \frac{1}{3}f_B(x) + \frac{2}{3}f_C(x) \\
= \frac{1}{18}\begin{cases}
−21(1 − |x|)^3 + 27(1 − |x|)^2 + 9(1 − |x|) + 1 \ \ \ \ \ \ -1 ≤ x ≤ 1 \\
7(2 − |x|)^3 − 6(2 − |x|)^2 \ \ \ \ \ \ \ \ \ 1 ≤ |x| ≤ 2 \\
0 \ \  \ \ \ \ \ \ otherwise
\end{cases}
$$
![Figure 9.24](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.24.png)
Figure 9.24. The MitchellNetravali filter. 
图 9.24。 MitchellNetravali 过滤器。

### 9.3.2 Properties of Filters 过滤器的属性

Filters have some traditional terminology that goes with them, which we use to describe the filters and compare them to one another.
过滤器有一些与之相关的传统术语，我们用它们来描述过滤器并将它们相互比较。

The impulse response of a filter is just another name for the function: it is the response of the filter to a signal that just contains an impluse (and recall that convolving with an impulse just gives back the filter).
滤波器的脉冲响应只是该函数的另一个名称：它是滤波器对仅包含脉冲的信号的响应（回想一下，与脉冲进行卷积只会返回滤波器）。

A continuous filter is interpolating if, when it is used to reconstruct a continuous function from a discrete sequence, the resulting function takes on exactly the values of the samples at the sample points— that is, it “connects the dots” rather than producing a function that only goes near the dots. Interpolating filters are exactly those filters f for which $f(0) = 1$ and $f(i) = 0$ for all nonzero integers i (Figure 9.25).
如果当连续滤波器用于从离散序列重建连续函数时，所得到的函数精确地采用样本点处的样本值，则连续滤波器正在插值 - 也就是说，它“连接点”而不是产生一个 只接近点的函数。 插值滤波器正是那些滤波器 f，对于所有非零整数 i，$f(0) = 1$ 且 $f(i) = 0$（图 9.25）。
![Figure 9.25](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.25.png)
Figure 9.25. An interpolating filter reconstructs the sample points exactly because it has the value zero at all nonzero integer offsets from the center.
图 9.25。 插值滤波器精确地重建样本点，因为它在距中心的所有非零整数偏移处具有零值。

A filter that takes on negative values has ringing or overshoot: it will produce extra oscillations in the value around sharp changes in the value of the function being filtered.
具有负值的滤波器会产生振铃或过冲：它会在被滤波函数值急剧变化时产生额外的振荡。

For instance, the Catmull-Rom filter has negative lobes on either side, and if you filter a step function with it, it will exaggerate the step a bit, resulting in function values that undershoot 0 and overshoot 1 (Figure 9.26).
例如，Catmull-Rom 滤波器的两侧都有负瓣，如果用它过滤阶跃函数，它会稍微夸大阶跃，导致函数值低于 0 且高于 1（图 9.26）。
![Figure 9.26](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.26.png)
Figure 9.26. A filter with negative lobes will always produce some overshoot when filtering or reconstructing a sharp discontinuity.
图 9.26。 当过滤或重建尖锐的不连续性时，具有负瓣的滤波器总是会产生一些过冲。

A continuous filter is ripple free if, when used as a reconstruction filter, it will reconstruct a constant sequence as a constant function (Figure 9.27). This is equivalent to the requirement that the filter sum to one on any integer-spaced grid:
如果连续滤波器用作重构滤波器时，它将重构常数序列作为常数函数，则它是无纹波的（图 9.27）。 这相当于要求滤波器在任何整数间隔网格上总和为 1：
$\sum_if(x + i) = 1\ \ \ for\ all\ x \\$

![Figure 9.27](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.27.png)
Figure 9.27. The tent filter of radius 1 is a ripple-free reconstruction filter; the Gaussian filter with standard deviation 1/2 is not.
图 9.27。 半径为1的帐篷滤波器是无波纹重构滤波器； 标准差为 1/2 的高斯滤波器则不然。

All the filters in Section 9.3.1 are ripple free at their natural radii, except the Gaussian, but none of them are necessarily ripple free when they are used at a noninteger scale. If it is necessary to eliminate ripple in discrete-continuous convolution, it is easy to do so: divide each computed sample by the sum of the weights used to compute it:
除高斯滤波器外，第 9.3.1 节中的所有滤波器在其自然半径上都是无波纹的，但当它们用于非整数尺度时，它们都不一定是无波纹的。 如果需要消除离散连续卷积中的纹波，很容易做到：将每个计算样本除以用于计算它的权重总和：
$$
\overline{(a * f)}(x) = \frac{\sum_ia[i]f(x-i)}{\sum_ia[i]} \ \ \ \ (9.4)
$$
This expression can still be interpreted as convolution between a and a filter $\overline{f}$ (see Exercise 6). 
这个表达式仍然可以解释为 a 和过滤器 $\overline{f}$ 之间的卷积（参见练习 6）。

A continuous filter has a degree of continuity, which is the highest-order derivative that is defined everywhere. A filter, like the box filter, that has sudden jumps in its value is not continuous at all. A filter that is continuous but has sharp corners (discontinuities in the first derivative), such as the tent filter, has order of continuity zero, and we say it is $C^0$. A filter that has a continuous derivative (no sharp corners), such as the piecewise cubic filters in the previous section, is $C^1$; if its second derivative is also continuous, as is true of the B-spline filter, it is $C^2$. The order of continuity of a filter is particularly important for a reconstruction filter because the reconstructed function inherits the continuity of the filter.
连续滤波器具有一定程度的连续性，这是到处都定义的最高阶导数。 过滤器（如箱式过滤器）的值突然跳跃，根本不是连续的。 连续但具有尖角（一阶导数不连续）的滤波器（例如帐篷滤波器）的连续阶数为零，我们称其为 $C^0$。 具有连续导数（无尖角）的滤波器，例如上一节中的分段三次滤波器，为 $C^1$； 如果它的二阶导数也是连续的，就像 B 样条滤波器一样，则它是 $C^2$。 滤波器的连续性阶对于重构滤波器来说特别重要，因为重构函数继承了滤波器的连续性。

#### Separable Filters 可分离过滤器

So far we have only discussed filters for 1D convolution, but for images and other multidimensional signals we need filters too. In general, any 2D function could be a 2D filter, and occasionally it is useful to define them this way. But, in most cases, we can build suitable 2D (or higher-dimensional) filters from the 1D filters we have already seen.
到目前为止，我们只讨论了一维卷积的滤波器，但对于图像和其他多维信号，我们也需要滤波器。 一般来说，任何 2D 函数都可以是 2D 滤波器，有时以这种方式定义它们很有用。 但是，在大多数情况下，我们可以从已经见过的 1D 滤波器构建合适的 2D（或更高维）滤波器。

The most useful way of doing this is by using a separable filter. The value of a separable filter $f_2(x, y)$ at a particular $x$ and $y$ is simply the product of $f_1$ (the 1D filter) evaluated at $x$ and at $y$:
最有用的方法是使用可分离的过滤器。 可分离滤波器 $f_2(x, y)$ 在特定 $x$ 和 $y$ 处的值只是在 $x$ 和 $y$ 处计算的 $f_1$（一维滤波器）的乘积：
$f_2(x, y) = f_1(x)f_1(y)  $

Similarly, for discrete filters, 
类似地，对于离散滤波器，
$b_2[i, j] = b_1[i]b_1[j].  $

Any horizontal or vertical slice through $f_2$ is a scaled copy of $f_1$. The integral of $f_2$ is the square of the integral of $f_1$, so in particular if $f_1$ is normalized, then so is $f_2$.
通过 $f_2$ 的任何水平或垂直切片都是 $f_1$ 的缩放副本。 $f_2$ 的积分是 $f_1$ 积分的平方，因此特别是如果 $f_1$ 被标准化，那么 $f_2$ 也被标准化。

**Example (The separable tent filter)**. If we choose the tent function for $f_1$, the resulting piecewise bilinear function (Figure 9.28) is
**示例（可分离的帐篷过滤器）**。 如果我们为$ f_1 $选择帐篷函数，则得到的分段双线性函数（图 9.28）为
$$
f_{2,tent}(x,y) = \begin{cases}
(1 - |x|)(1 - |y|) \ \ \ \ \ |x| < 1\ and\ |y| < 1 \\
0 \ \ \ \ \ \ \ \ \ otherwise
\end{cases}
$$
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.28.png" alt="Figure 9.28" style="zoom:67%;" />

Figure 9.28. The separable 2D tent filter.
图 9.28。 可分离的 2D 帐篷过滤器。

The profiles along the coordinate axes are tent functions, but the profiles along the diagonals are quadratics (for instance, along the line $x = y$ in the positive quadrant, we see the quadratic function $(1 − x)^2$).
沿坐标轴的轮廓是帐篷函数，但沿对角线的轮廓是二次函数（例如，沿正象限中的 $x = y$ 线，我们看到二次函数 $(1 − x)^2$） 。

**Example (The 2D Gaussian filter)**. If we choose the Gaussian function for f1, the resulting 2D function (Figure 9.29) is 
**示例（2D 高斯滤波器）**。 如果我们为 f1 选择高斯函数，则得到的 2D 函数（图 9.29）为
$f_{2,g}(x,y) = \frac{1}{2\pi}(e^{-x^2/2}e^{-y^2/2}) \\ 
 = \frac{1}{2\pi}(e^{-(x^2+y^2)/2})\\
 = \frac{1}{2\pi}e^{-r^2/2}$

<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.29.png" alt="Figure 9.29" style="zoom:67%;" />

Figure 9.29. The 2D Gaussian filter, which is both separable and radially symmetric.
图 9.29。 二维高斯滤波器，既可分离又径向对称。

Notice that this is (up to a scale factor) the same function we would get if we revolved the 1D Gaussian around the origin to produce a circularly symmetric function. The property of being both circularly symmetric and separable at the same time is unique to the Gaussian function. The profiles along the coordinate axes are Gaussians, but so are the profiles along any direction at any offset from the center.
请注意，如果我们围绕原点旋转一维高斯函数以产生圆对称函数，则这（在比例因子范围内）与我们得到的函数相同。 同时具有圆对称性和可分离性的性质是高斯函数所独有的。 沿坐标轴的轮廓是高斯分布，但沿距中心任意偏移的任意方向的轮廓也是高斯分布。

The key advantage of separable filters over other 2D filters has to do with efficiency in implementation. Let’s substitute the definition of $a_2$ into the definition of discrete convolution:
与其他 2D 滤波器相比，可分离滤波器的主要优势在于实现效率。 我们将$a_2$的定义代入离散卷积的定义：
$(a*b_2)[i, j] = \sum_{i'}\sum_{j'}a[i', j']b_1[i - i']b_1[j - j']    \\$

Note that $b_1[i - i']$ does not depend on $j'$ and can be factored out of the inner sum:
请注意，$b_1[i - i']$ 不依赖于 $j'$，并且可以从内部总和中分解出来：
$= \sum_{i'}b_1[i - i']\sum_{j'}a[i',j']b_1[j-j'] \\ $

Let’s abbreviate the inner sum as $S[i']$: 
让我们将内部总和缩写为 $S[i']$：
$$
S[i'] = \sum_{j'}a[i', j']b_1[j-j'] \\
(a*b_2)[i,j] = \sum_{i'}b_1[i - i']S[i']  \ \ \  \ \ \ (9.5)
$$
With the equation in this form, we can first compute and store $S[i']$ for each value of $i'$, and then compute the outer sum using these stored values. At first glance this does not seem remarkable, since we still had to do work proportional to $(2r + 1)^2$ to compute all the inner sums. However, it’s quite different if we want to compute the value at many points $[i, j]$.
通过这种形式的方程，我们可以首先计算并存储 $i'$ 的每个值的 $S[i']$，然后使用这些存储的值计算外部总和。 乍一看，这似乎并不引人注目，因为我们仍然必须做与 $(2r + 1)^2$ 成比例的工作来计算所有内部总和。 然而，如果我们想要计算多个点 $[i, j]$ 的值，那就完全不同了。

Suppose we need to compute $a*b_2$ at $[2, 2]$ and $[3, 2]$, and $b_1$ has a radius of 2. Examining Equation 9.5, we can see that we will need $S[0], . . . , S[4]$ to compute the result at $[2, 2]$, and we will need $S[1], . . . , S[5]$ to compute the result at $[3, 2]$. So, in the separable formulation, we can just compute all six values of $S$ and share $S[1], . . . , S[4]$ (Figure 9.30).
假设我们需要计算 $[2, 2]$ 和 $[3, 2]$ 处的 $a*b_2$，并且 $b_1$ 的半径为 2。检查公式 9.5，我们可以看到我们需要 $S [0]，..., S[4]$ 来计算 $[2, 2]$ 处的结果，我们将需要 $S[1], ..., S[5]$ 计算 $[3, 2]$ 处的结果。 因此，在可分离公式中，我们可以计算 $S$ 的所有六个值并共享 $S[1], ...，S[4]$（图 9.30）。
![Figure 9.30](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.30.png)
Figure 9.30. Computing two output points using separate 2D arrays of 25 samples (above) vs. filtering once along the columns, then using separate 1D arrays of five samples (below).
图 9.30。 使用包含 25 个样本的单独 2D 数组（上图）计算两个输出点，而不是沿列过滤一次，然后使用包含 5 个样本的单独 1D 数组（下图)。

This savings has great significance for large filters. Filtering an image with a filter of radius r in the general case requires computation of $(2r + 1)^2$ products per pixel, while filtering the image with a separable filter of the same size requires $2(2r + 1)$ products (at the expense of some intermediate storage). This change in asymptotic complexity from $O(r^2)$ to $O(r)$ enables the use of much larger filters.
这种节省对于大型过滤器具有重要意义。 一般情况下，使用半径为 r 的滤波器过滤图像需要计算每个像素 $(2r + 1)^2$ 个乘积，而使用相同大小的可分离滤波器过滤图像需要 $2(2r + 1)$ 个乘积 （以一些中间存储为代价）。 渐近复杂度从 $O(r^2)$ 到 $O(r)$ 的这种变化使得可以使用更大的滤波器。

The algorithm is:
算法是：

> function filterImage(image I, filter b)
> 	$r = b.radius$
> 	$n_x = I.width$
> 	$n_y = I.height$
> 	allocate storage array $S[0 . . . n_x − 1]$
> 	allocate image $I_{out}[r . . . n_x − r − 1, r . . . n_y − r − 1]$
> 	initialize $S$ and $I_{out}$ to all zero
> 	for $j = r$ to $n_y − r − 1$ do
> 		for $i' = 0$ to $n_x − 1$ do
> 			$S[i'] = 0$
> 			for $j' = j − r$ to $j + r$ do
> 				$S[i'] = S[i'] + I[i', j']b[j − j']$
> 		for $i = r$ to $n_x − r − 1$ do
> 			for $i' = i − r$ to $i + r$ do
> 				$I_{out}[i, j] = I_{out}[i, j] + S[i']b[i − i']$
> 	return $I_{out}$

For simplicity, this function avoids all questions of boundaries by trimming $r$ pixels off all four sides of the output image. In practice there are various ways to handle the boundaries; see Section 9.4.3.
为简单起见，此函数通过修剪输出图像所有四个边的 $r$ 像素来避免所有边界问题。 在实践中，有多种方法可以处理边界； 参见第 9.4.3 节。

## 9.4 Signal Processing for Images 图像信号处理

We have discussed sampling, filtering, and reconstruction in the abstract so far, using mostly 1D signals for examples. But as we observed at the beginning of the chapter, the most important and most common application of signal processing in graphics is for sampled images. Let us look carefully at how all this applies to images.
到目前为止，我们已经抽象地讨论了采样、滤波和重构，主要使用一维信号作为示例。 但正如我们在本章开头所观察到的，信号处理在图形中最重要和最常见的应用是采样图像。 让我们仔细看看这一切如何应用于图像。

### 9.4.1 Image Filtering Using Discrete Filters 使用离散滤波器进行图像滤波

Perhaps the simplest application of convolution is processing images using discrete convolution. Some of the most widely used features of image manipulation programs are simple convolution filters. Blurring of images can be achieved by convolving with many common lowpass filters, ranging from the box to the Gaussian (Figure 9.31). A Gaussian filter creates a very smooth-looking blur and is commonly used for this purpose. 
也许卷积最简单的应用是使用离散卷积处理图像。 图像处理程序最广泛使用的一些功能是简单的卷积滤波器。 图像模糊可以通过与许多常见的低通滤波器（从盒子到高斯）进行卷积来实现（图 9.31）。 高斯滤镜可创建看起来非常平滑的模糊效果，通常用于此目的。 
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.31.png" alt="Figure 9.31" style="zoom:67%;" />
Figure 9.31. Blurring an image by convolution with each of three different filters. 
图9.31。通过与三种不同的滤镜中的每一种进行卷积来模糊图像。

The opposite of blurring is sharpening, and one way to do this is by using the “unsharp mask” procedure: subtract a fraction α of a blurred image from the original. With a rescaling to avoid changing the overall brightness, we have
模糊的反面是锐化，实现此目的的一种方法是使用“unsharp mask”过程：从原始图像中减去模糊图像的一小部分 α。 通过重新缩放以避免改变整体亮度，我们有
$$
I_{sharp} = (1 + α)I − α(I * f_{g,σ}) \\
= I * ((1 + α)d − αf_{g,σ}) \\
= I * f_{sharp}(σ, α),
$$
where $f_{g,σ}$ is the Gaussian filter of width $σ$. Using the discrete impluse d and the distributive property of convolution, we were able to write this whole process as a single filter that depends on both the width of the blur and the degree of sharpening (Figure 9.32).
其中 $f_{g,σ}$ 是宽度 $σ$ 的高斯滤波器。 使用离散脉冲 d 和卷积的分布特性，我们能够将整个过程编写为单个滤波器，该滤波器取决于模糊的宽度和锐化的程度（图 9.32）。
![Figure 9.32](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.32.png)
Figure 9.32. Sharpening an image using a convolution filter. 
图 9.32。 使用卷积滤波器锐化图像。

Another example of combining two discrete filters is a drop shadow. It’s common to take a blurred, shifted copy of an object’s outline to create a soft drop shadow (Figure 9.33). We can express the shifting operation as convolution with an off-center impulse:
组合两个离散滤镜的另一个示例是阴影。 通常采用对象轮廓的模糊、移位副本来创建柔和的阴影（图 9.33）。 我们可以将移位操作表示为带有偏心脉冲的卷积：
![Figure 9.33](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.33.png)
Figure 9.33. A soft drop shadow. 
图9.33。柔和的投影。
$$
d_{m,n}(i, j) = \begin{cases}
1 \ \ \ \ \ \ i = m\ and\ j = n \\
0 \ \ \ \ \ \ otherwise.
\end{cases}
$$
Shifting, then blurring, is achieved by convolving with both filters:
通过与两个滤波器进行卷积来实现移动，然后模糊：
$$
I_{shadow} = (I * d_{m,n}) * f_{g,σ} \\
= I * (d_{m,n} * f_{g,σ}) \\
= I * f_{shadow}(m, n, σ) 
$$
Here we have used associativity to group the two operations into a single filter with three parameters. 
这里我们使用结合律将这两个操作组合到一个带有三个参数的过滤器中。

### 9.4.2 Antialiasing in Image Sampling 图像采样中的抗锯齿

In image synthesis, we often have the task of producing a sampled representation of an image for which we have a continuous mathematical formula (or at least a procedure we can use to compute the color at any point, not just at integer pixel positions). Ray tracing is a common example; more about ray tracing and the specific methods for antialiasing is in Chapter 4. In the language of signal processing, we have a continuous 2D signal (the image) that we need to sample on a regular 2D lattice. If we go ahead and sample the image without any special measures, the result will exhibit various aliasing artifacts (Figure 9.34). At sharp edges in the image, we see stair-step artifacts known as “jaggies.” In areas where there are repeating patterns, we see wide bands known as moire patterns .
在图像合成中，我们经常需要生成图像的采样表示，对于该图像，我们有一个连续的数学公式（或者至少是一个可以用来计算任意点的颜色的过程，而不仅仅是整数像素位置的颜色）。 光线追踪是一个常见的例子； 有关光线追踪和抗锯齿具体方法的更多信息请参见第 4 章。用信号处理的语言来说，我们有一个连续的 2D 信号（图像），需要在规则的 2D 晶格上进行采样。 如果我们在不采取任何特殊措施的情况下对图像进行采样，结果将出现各种混叠伪像（图 9.34）。 在图像的锐利边缘，我们看到称为“锯齿”的阶梯伪影。 在有重复图案的区域，我们会看到称为莫尔图案的宽带。
![Figure 9.34](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.34.png)
Figure 9.34. Two artifacts of aliasing in images: moir patterns in periodic textures (left), and “jaggies” on straight lines (right). 
图 9.34。 图像中的两种锯齿现象：周期性纹理中的莫尔图案（左）和直线上的“锯齿”（右)。

The problem here is that the image contains too many small-scale features; we need to smooth it out by filtering it before sampling. Looking back at the definition of continuous convolution in Equation (9.3), we need to average the image over an area around the pixel location, rather than just taking the value at a single point. The specific methods for doing this are discussed in Chapter 4. A simple filter like a box will improve the appearance of sharp edges, but it still produces some moir´ e patterns (Figure 9.35). The Gaussian filter, which is very smooth, is much more effective against the moir´ e patterns, at the expense of overall somewhat more blurring. These two examples illustrate the tradeoff between sharpness and aliasing that is fundamental to choosing antialiasing filters.
这里的问题是图像包含太多小尺度特征； 我们需要在采样之前通过过滤来平滑它。 回顾方程（9.3）中连续卷积的定义，我们需要在像素位置周围的区域上对图像进行平均，而不是仅仅取单个点的值。 具体方法将在第 4 章中讨论。像盒子这样的简单过滤器将改善锐利边缘的外观，但它仍然会产生一些莫尔图案（图 9.35）。 高斯滤镜非常平滑，对莫尔图案的抑制效果要好得多，但总体上会更加模糊。 这两个例子说明了清晰度和混叠之间的权衡，这是选择抗混叠滤波器的基础。
![Figure 9.35](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.35.png)
Figure 9.35. A comparison of three different sampling filters being used to antialias a difficult test image that contains circles that are spaced closer and closer as they get larger. 
图 9.35。 比较三种不同的采样滤波器，用于对困难的测试图像进行抗锯齿处理，其中包含的圆圈随着它们变大而间隔越来越近。

### 9.4.3 Reconstruction and Resampling 重建和重采样

One of the most common image operations where careful filtering is crucial is resampling—changing the sample rate, or changing the image size.
最常见的图像操作之一是重新采样，其中仔细的过滤至关重要，即更改采样率或更改图像大小。

Suppose we have taken an image with a digital camera that is 3000 by 2000 pixels in size, and we want to display it on a monitor that has only 1280 by 1024 pixels. In order to make it fit, while maintaining the 3:2 aspect ratio, we need to resample it to 1278 by 852 pixels. How should we go about this?
假设我们用数码相机拍摄了一张尺寸为 3000 x 2000 像素的图像，并且希望将其显示在只有 1280 x 1024 像素的显示器上。 为了使其适合，同时保持 3:2 的宽高比，我们需要将其重新采样为 1278 x 852 像素。 我们应该怎样做呢？

One way to approach this problem is to think of the process as dropping pixels: the size ratio is between 2 and 3, so we’ll have to drop out one or two pixels between pixels that we keep. It’s possible to shrink an image in this way, but the quality of the result is low—the images in Figure 9.34 were made using pixel dropping. Pixel dropping is very fast, however, and it is a reasonable choice to make a preview of the resized image during an interactive manipulation.
解决这个问题的一种方法是将该过程视为丢弃像素：尺寸比在 2 到 3 之间，因此我们必须在保留的像素之间丢弃一两个像素。 可以通过这种方式缩小图像，但结果的质量较低——图 9.34 中的图像是使用像素丢弃技术制作的。 然而，像素下降非常快，在交互式操作期间预览调整大小的图像是一个合理的选择。

The way to think about resizing images is as a resampling operation: we want a set of samples of the image on a particular grid that is defined by the new image dimensions, and we get them by sampling a continuous function that is reconstructed from the input samples (Figure 9.36). Looking at it this way, it’s just a sequence of standard image processing operations: first we reconstruct a continuous function from the input samples, and then we sample that function just as we would sample any other continuous image. To avoid aliasing artifacts, appropriate filters need to be used at each stage.
调整图像大小的方式被视为重采样操作：我们希望在由新图像尺寸定义的特定网格上获得一组图像样本，并通过对从输入重建的连续函数进行采样来获取它们 样本（图 9.36）。 从这个角度来看，它只是一系列标准图像处理操作：首先，我们从输入样本中重建一个连续函数，然后我们对该函数进行采样，就像对任何其他连续图像进行采样一样。 为了避免混叠伪影，需要在每个阶段使用适当的滤波器。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.36.png" alt="Figure 9.36" style="zoom:67%;" />
Figure 9.36. Resampling an image consists of two logical steps that are combined into a single operation in code. First, we use a reconstruction filter to define a smooth, continuous function from the input samples. Then, we sample that function on a new grid to get the output samples.
图 9.36。 图像重采样由两个逻辑步骤组成，这两个步骤组合成代码中的单个操作。 首先，我们使用重建滤波器根据输入样本定义平滑、连续的函数。 然后，我们在新网格上对该函数进行采样以获得输出样本。

A small example is shown in Figure 9.37: if the original image is 12 × 9 pixels and the new one is 8 × 6 pixels, there are 2/3 as many output pixels as input pixels in each dimension, so their spacing across the image is 3/2 the spacing of the original samples.
图 9.37 显示了一个小例子：如果原始图像是 12 × 9 像素，新图像是 8 × 6 像素，则每个维度上的输出像素数量是输入像素数量的 2/3，因此它们在图像上的间距 是原始样本间距的 3/2。
![Figure 9.37](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.37.png)
Figure 9.37. The sample locations for the input and output grids in resampling a 12 by 9 image to make an 8 by 6 one.
图 9.37。 对 12 x 9 图像重新采样以生成 8 x 6 图像时输入和输出网格的样本位置。

In order to come up with a value for each of the output samples, we need to somehow compute values for the image in between the samples. The pixeldropping algorithm gives us one way to do this: just take the value of the closest sample in the input image and make that the output value. This is exactly equivalent to reconstructing the image with a 1-pixel-wide (radius one-half) box filter and then point sampling.
为了得出每个输出样本的值，我们需要以某种方式计算样本之间图像的值。 像素丢弃算法为我们提供了一种方法：只需获取输入图像中最接近样本的值并将其作为输出值。 这完全相当于用 1 像素宽（半径二分之一）的盒式滤波器重建图像，然后进行点采样。

Of course, if the main reason for choosing pixel dropping or other very simple filtering is performance, one would never implement that method as a special case of the general reconstruction-and-resampling procedure. In fact, because of the discontinuities, it’s difficult to make box filters work in a general framework. But, for high-quality resampling, the reconstruction/sampling framework provides valuable flexibility.
当然，如果选择像素丢弃或其他非常简单的过滤的主要原因是性能，则永远不会将该方法作为一般重建和重采样过程的特殊情况来实现。 事实上，由于不连续性，很难使盒式滤波器在通用框架中工作。 但是，对于高质量重采样，重建/采样框架提供了宝贵的灵活性。

To work out the algorithmic details, it’s simplest to drop down to 1D and discuss resampling a sequence. The simplest way to write an implementation is in terms of the reconstruct function we defined in Section 9.2.5.
要弄清楚算法细节，最简单的方法是下降到一维并讨论对序列进行重采样。 编写实现的最简单方法是使用我们在第 9.2.5 节中定义的重建函数。

> function resample(sequence a, float $x_0$, float $Δx$, int $n$, filter $f$)
> 	create sequence $b$ of length $n$
> 	for $i = 0$ to $n - 1$ do
> 		$b[i]$ = reconstruct$(a, f, x_0 + iΔx)$
> 	return $b$

The parameter $x_0$ gives the position of the first sample of the new sequence in terms of the samples of the old sequence. That is, if the first output sample falls midway between samples 3 and 4 in the input sequence, $x_0$ is 3.5.
参数 $x_0$ 给出了新序列的第一个样本相对于旧序列的样本的位置。 也就是说，如果第一个输出样本位于输入序列中样本 3 和 4 之间，则 $x_0$ 为 3.5。

This procedure reconstructs a continuous image by convolving the input sequence with a continuous filter and then point samples it. That’s not to say that these two operations happen sequentially—the continuous function exists only in principle and its values are computed only at the sample points. But mathematically, this function computes a set of point samples of the function $a*f$.
该过程通过将输入序列与连续滤波器进行卷积来重建连续图像，然后对其进行点采样。 这并不是说这两个操作是顺序发生的——连续函数仅在原则上存在，并且其值仅在样本点处计算。 但从数学上讲，该函数计算函数 $a*f$ 的一组点样本。

This point sampling seems wrong, though, because we just finished saying that a signal should be sampled with an appropriate smoothing filter to avoid aliasing. We should be convolving the reconstructed function with a sampling filter $g$ and point sampling $g*(f*a)$. But since this is the same as $(g*f)*a$, we can roll the sampling filter together with the reconstruction filter; one convolution operation is all we need (Figure 9.38). This combined reconstruction and sampling filter is known as a resampling filter.
不过，这种点采样似乎是错误的，因为我们刚刚说过应该使用适当的平滑滤波器对信号进行采样以避免混叠。 我们应该将重构函数与采样滤波器 $g$ 和点采样 $g*(f*a)$ 进行卷积。 但由于这与 $(g*f)*a$ 相同，因此我们可以将采样滤波器与重建滤波器一起滚动； 我们只需要一次卷积运算（图 9.38）。 这种组合的重建和采样滤波器称为重采样滤波器。
![Figure 9.38](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.38.png)
Figure 9.38. Resampling involves filtering for reconstruction and for sampling. Since two convolution filters applied in sequence can be replaced with a single filter, we only need one resampling filter, which serves the roles of reconstruction and sampling.
图 9.38。 重采样涉及重构和采样的过滤。 由于顺序应用的两个卷积滤波器可以用单个滤波器代替，因此我们只需要一个重采样滤波器，它起到重建和采样的作用。

When resampling images, we usually specify a source rectangle in the units of the old image that specifies the part we want to keep in the new image. For example, using the pixel sample positioning convention from Chapter 3, the rectangle we’d use to resample the entire image is $(−0.5, n^{old}_{x} − 0.5) × (−0.5, n^{old}_y − 0.5)$. Given a source rectangle $(x_l, x_h) × (y_l, y_h)$, the sample spacing for the new image is $Δx = (x_h − x_l)/n^{new}_x$ in $x$ and $Δy = (y_h − y_l)/n^{new}_y$ in $y$. The lower-left sample is positioned at $(x_l + Δx/2, y_l + Δy/2)$.
当我们重新采样图像时，我们通常会在旧图像的单位中指定一个源矩形，该矩形指定了我们希望在新图像中保留的部分。例如，使用第3章中的像素采样定位约定，我们用来重新采样整个图像的矩形是 $(−0.5, n^{old}_{x} − 0.5) × (−0.5, n^{old}_y − 0.5)$。给定源矩形 $(x_l, x_h) × (y_l, y_h)$，新图像的样本间距是 $Δx = (x_h − x_l)/n^{new}_x$ 在 $x$ 方向和 $Δy = (y_h − y_l)/n^{new}_y$ 在 $y$ 方向。左下角的样本位于 $(x_l + Δx/2, y_l + Δy/2)$ 的位置。

Modifying the 1D pseudocode to use this convention, and expanding the call to the reconstruct function into the double loop that is implied, we arrive at:
修改一维伪代码以使用此约定，并将对重建函数的调用扩展为隐含的双循环，我们得到：

> function resample(sequence $a$, float $x_l$, float $x_h$, int $n$, filter $f$)
> 	create sequence $b$ of length $n$
> 	$r = f.radius$
> 	$x_0 = x_l + Δx/2$
> 	for $i = 0$ to $n - 1$ do
> 		$s = 0$
> 		$x = x_0 + iΔx$
> 		for $j = \lceil x - r\rceil$ to $\lfloor x + r\rfloor$ do
> 			$s = s + a[j]f(x - j)$
> 		$b[i] = s$
> 	return $b$

This routine contains all the basics of resampling an image. One last issue that remains to be addressed is what to do at the edges of the image, where the simple version here will access beyond the bounds of the input sequence. There are several things we might do:
该例程包含图像重采样的所有基础知识。 仍有待解决的最后一个问题是在图像边缘做什么，这里的简单版本将超出输入序列的边界。 我们可以做几件事：

- Just stop the loop at the ends of the sequence. This is equivalent to padding the image with zeros on all sides.
  只需在序列末尾停止循环即可。 这相当于用零填充图像的所有边。
- Clip all array accesses to the end of the sequence—that is, return a[0] when we would want to access $a[−1]$. This is equivalent to padding the edges of the image by extending the last row or column.
  将所有数组访问剪辑到序列的末尾，也就是说，当我们想要访问 $a[−1]$ 时，返回 a[0]。 这相当于通过延伸最后一行或最后一列来填充图像的边缘。
- Modify the filter as we approach the edge so that it does not extend beyond the bounds of the sequence.
  当我们接近边缘时修改过滤器，使其不会超出序列的边界。

The first option leads to dim edges when we resample the whole image, which is not really satisfactory. The second option is easy to implement; the third is probably the best performing. The simplest way to modify the filter near the edge of the image is to renormalize it: divide the filter by the sum of the part of the filter that falls within the image. This way, the filter always adds up to 1 over the actual image samples, so it preserves image intensity. For performance, it is desirable to handle the band of pixels within a filter radius of the edge (which require this renormalization) separately from the center (which contains many more pixels and does not require renormalization).
当我们对整个图像重新采样时，第一个选项会导致边缘变暗，这并不令人满意。 第二种方案很容易实现； 第三个可能是表现最好的。 修改图像边缘附近的滤波器的最简单方法是将其重新归一化：将滤波器除以落在图像内的滤波器部分的总和。 这样，滤波器在实际图像样本上的总和总是为 1，因此它保留了图像强度。 为了提高性能，需要将边缘滤波器半径内的像素带（需要重新归一化）与中心（包含更多像素并且不需要重新归一化）分开处理。

The choice of filter for resampling is important. There are two separate issues: the shape of the filter and the size (radius). Because the filter serves both as a reconstruction filter and a sampling filter, the requirements of both roles affect the choice of filter. For reconstruction, we would like a filter smooth enough to avoid aliasing artifacts when we enlarge the image, and the filter should be ripplefree. For sampling, the filter should be large enough to avoid undersampling and smooth enough to avoid moir´ e artifacts. Figure 9.39 illustrates these two different needs.
用于重采样的滤波器的选择很重要。 有两个独立的问题：过滤器的形状和尺寸（半径）。 由于滤波器既充当重建滤波器又充当采样滤波器，因此这两种角色的要求都会影响滤波器的选择。 对于重建，我们希望滤波器足够平滑，以避免放大图像时出现混叠伪影，并且滤波器应该没有波纹。 对于采样，滤波器应该足够大以避免采样不足，并且足够平滑以避免莫尔伪影。 图 9.39 说明了这两种不同的需求。
![Figure 9.39](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.39.png)
Figure 9.39. The effects of using different sizes of a filter for upsampling (enlarging) or downsampling (reducing) an image.
图 9.39。 使用不同尺寸的滤波器对图像进行上采样（放大）或下采样（缩小)的效果。

Generally, we will choose one filter shape and scale it according to the relative resolutions of the input and output. The lower of the two resolutions determines the size of the filter: when the output is more coarsely sampled than the input (downsampling, or shrinking the image), the smoothing required for proper sampling is greater than the smoothing required for reconstruction, so we size the filter according to the output sample spacing (radius 3 in Figure 9.39). On the other hand, when the output is more finely sampled (upsampling, or enlarging the image) then the smoothing required for reconstruction dominates (the reconstructed function is already smooth enough to sample at a higher rate than it started), so the size of the filter is determined by the input sample spacing (radius 1 in Figure 9.39).
通常，我们会选择一种滤波器形状并根据输入和输出的相对分辨率对其进行缩放。 两个分辨率中较低的一个决定了滤波器的大小：当输出的采样比输入更粗略时（下采样或缩小图像），正确采样所需的平滑大于重建所需的平滑，因此我们调整大小 根据输出样本间距（图 9.39 中的半径 3）过滤器。 另一方面，当对输出进行更精细的采样（上采样或放大图像）时，重建所需的平滑占主导地位（重建函数已经足够平滑，可以以比开始时更高的速率进行采样），因此 滤波器由输入样本间距（图 9.39 中的半径 1）决定。

Choosing the filter itself is a tradeoff between speed and quality. Common choices are the box filter (when speed is paramount), the tent filter (moderate quality), or a piecewise cubic (excellent quality). In the piecewise cubic case, the degree of smoothing can be adjusted by interpolating between fB and fC; the Mitchell-Netravali filter is a good choice. 
选择过滤器本身就是速度和质量之间的权衡。 常见的选择是盒式过滤器（当速度至关重要时）、帐篷过滤器（中等质量）或分段立方过滤器（卓越质量）。 在分段三次的情况下，可以通过在fB和fC之间插值来调整平滑程度； Mitchell-Netravali 滤波器是一个不错的选择。

Just as with image filtering, separable filters can provide a significant speedup. The basic idea is to resample all the rows first, producing an image with changed width but not height, then to resample the columns of that image to produce the final result (Figure 9.40). Modifying the pseudocode given earlier so that it takes advantage of this optimization is reasonably straightforward.
正如图像过滤一样，可分离的过滤器可以提供显着的加速。 基本思想是首先对所有行重新采样，生成宽度改变但高度不变的图像，然后对该图像的列重新采样以产生最终结果（图 9.40）。 修改前面给出的伪代码以利用这种优化是相当简单的。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.40.png" alt="Figure 9.40" style="zoom:80%;" />
Figure 9.40. Resampling an image using a separable approach. 
图 9.40。 使用可分离方法对图像进行重新采样。

## 9.5 Sampling Theory 抽样理论

If you are only interested in implementation, you can stop reading here; the algorithms and recommendations in the previous sections will let you implement programs that perform sampling and reconstruction and achieve excellent results. However, there is a deeper mathematical theory of sampling with a history reaching back to the first uses of sampled representations in telecommunications. Sampling theory answers many questions that are difficult to answer with reasoning based strictly on scale arguments.
如果你只对实现感兴趣，你可以停止阅读这里； 前面几节中的算法和建议将让您实现执行采样和重建的程序并获得出色的结果。 然而，还有更深入的采样数学理论，其历史可以追溯到电信中采样表示的首次使用。 抽样理论回答了许多严格基于尺度论证的推理难以回答的问题。

But most important, sampling theory gives valuable insight into the workings of sampling and reconstruction. It gives the student who learns it an extra set of intellectual tools for reasoning about how to achieve the best results with the most efficient code.
但最重要的是，采样理论为采样和重建的工作原理提供了宝贵的见解。 它为学习它的学生提供了一套额外的智力工具，用于推理如何使用最有效的代码实现最佳结果。

### 9.5.1 The Fourier Transform 傅里叶变换

The Fourier transform, along with convolution, is the main mathematical concept that underlies sampling theory. You can read about the Fourier transform in many math books on analysis, as well as in books on signal processing.
傅立叶变换与卷积一起是构成采样理论的主要数学概念。 您可以在许多有关分析的数学书籍以及有关信号处理的书籍中阅读有关傅立叶变换的内容。

The basic idea behind the Fourier transform is to express any function by adding together sine waves (sinusoids) of all frequencies. By using the appropriate weights for the different frequencies, we can arrange for the sinusoids to add up to any (reasonable) function we want.
傅立叶变换背后的基本思想是通过将所有频率的正弦波（正弦波）相加来表达任何函数。 通过对不同频率使用适当的权重，我们可以安排正弦曲线相加得到我们想要的任何（合理的）函数。

As an example, the square wave in Figure 9.41 can be expressed by a sequence of sine waves:
例如，图 9.41 中的方波可以用正弦波序列表示：
$\sum^∞_{n=1,3,5,...}\frac{4}{\pi n}\sin2\pi nx\\$

![Figure 9.41](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.41.png)
Figure 9.41. Approximating a square wave with finite sums of sines.
图 9.41。 用有限正弦和近似方波。

This Fourier series starts with a sine wave ($\sin 2πx$) that has frequency 1.0—same as the square wave—and the remaining terms add smaller and smaller corrections to reduce the ripples and, in the limit, reproduce the square wave exactly. Note that all the terms in the sum have frequencies that are integer multiples of the frequency of the square wave. This is because other frequencies would produce results that don’t have the same period as the square wave.
该傅立叶级数以频率为 1.0 的正弦波 ($\sin 2πx$) 开始（与方波相同），其余项添加越来越小的修正以减少纹波，并在极限情况下精确再现方波 。 请注意，总和中的所有项的频率都是方波频率的整数倍。 这是因为其他频率会产生与方波周期不同的结果。

A surprising fact is that a signal does not have to be periodic in order to be expressed as a sum of sinusoids in this way: a non-periodic signal just requires more sinusoids. Rather than summing over a discrete sequence of sinusoids, we will instead integrate over a continuous family of sinusoids. For instance, a box function can be written as the integral of a family of cosine waves:
一个令人惊讶的事实是，信号不一定必须是周期性的才能以这种方式表示为正弦波之和：非周期性信号只需要更多的正弦波。 我们不会对离散的正弦曲线序列进行求和，而是对连续的正弦曲线族进行积分。 例如，盒函数可以写成余弦波族的积分： 
$$
\int^∞_{−∞}\frac{\sin\pi u}{\pi u}\cos2\pi ux du \ \ \ \ \ (9.6)
$$
This integral in Equation (9.6) is adding up infinitely many cosines, weighting the cosine of frequency $u$ by the weight $(\sin πu)/πu$. The result, as we include higher and higher frequencies, converges to the box function (see Figure 9.42). When a function $f$ is expressed in this way, this weight, which is a function of the frequency $u$, is called the Fourier transform of $f$, denoted $\hat{f}$. The function $\hat{f}$tells us how to build $f$ by integrating over a family of sinusoids:
方程（9.6）中的积分将无穷多个余弦相加，用权重 $(\sin πu)/πu$ 对频率 $u$ 的余弦进行加权。 当我们包含越来越高的频率时，结果会收敛到框函数（见图 9.42）。 当函数$f$以这种方式表达时，这个权重是频率$u$的函数，称为$f$的傅立叶变换，记为$\hat{f}$。 函数 $\hat{f}$ 告诉我们如何通过对一系列正弦曲线进行积分来构建 $f$：
$$
f(x) = \int^∞_{-∞}\hat{f}(u)e^{2\pi iux}du \ \ \ \ \ (9.7)
$$
![Figure 9.42](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.42.png)
Figure 9.42. Approximating a box function with integrals of cosines up to each of four cutoff frequencies.
图 9.42。 使用最多四个截止频率中的每一个的余弦积分来近似箱函数。

Equation (9.7) is known as the inverse Fourier transform (IFT) because it starts with the Fourier transform of f and ends up with $f$.(Note that the term “Fourier transform” is used both for the function $\hat{f}$ and for the operation that computes $\hat{f}$ from $f$. Unfortunately, this rather ambiguous usage is standard.  )
方程 (9.7) 被称为逆傅里叶变换 (IFT)，因为它以 f 的傅里叶变换开始，以 $f$ 结束。（请注意，术语“傅里叶变换”同时用于函数 $\hat{ f}$ 以及从 $f$ 计算 $\hat{f}$ 的操作。不幸的是，这种相当模糊的用法是标准的。）

Note that in Equation (9.7) the complex exponential $e^{2πiux}$ has been substituted for the cosine in the previous equation. Also, $\hat{f}$ is a complex-valued function. The machinery of complex numbers is required to allow the phase, as well as the frequency, of the sinusoids to be controlled; this is necessary to represent any functions that are not symmetric across zero. The magnitude of $\hat{f}$ is known as the Fourier spectrum, and, for our purposes, this is sufficient—we won’t need to worry about phase or use any complex numbers directly.
请注意，在方程 (9.7) 中，复指数 $e^{2πiux}$ 已替换为前面方程中的余弦。 此外，$\hat{f}$ 是一个复值函数。 需要复数机制来控制正弦波的相位和频率； 这对于表示任何不对称于零的函数是必要的。 $\hat{f}$ 的幅度被称为傅里叶谱，对于我们的目的来说，这已经足够了——我们不需要担心相位或直接使用任何复数。

It turns out that computing $\hat{f}$ from $f$ looks very much like computing $f$ from $\hat{f}$: 
事实证明，从 $f$ 计算 $\hat{f}$ 看起来非常像从 $\hat{f}$ 计算 $f$： 
$$
\hat{f}u = \int^∞_{-∞}f(x)e^{2πiux}dx \ \ \ \ \ (9.8)
$$
Equation (9.8) is known as the (forward) Fourier transform (FT). The sign in the exponential is the only difference between the forward and inverse Fourier transforms, and it is really just a technical detail. For our purposes, we can think of the FT and IFT as the same operation.
方程（9.8）被称为（前）傅立叶变换（FT）。 指数中的符号是正向和逆傅里叶变换之间的唯一区别，这实际上只是一个技术细节。 出于我们的目的，我们可以将 FT 和 IFT 视为相同的操作。

Sometimes the $f–\hat{f}$ notation is inconvenient, and then we will denote the Fourier transform of $f$ by $F{f}$ and the inverse Fourier transform of $\hat{f}$by $F^{−1}\{\hat{f}\}$. 
有时$f–\hat{f}$表示法不方便，这时我们将$f$的傅立叶变换表示为$F{f}$，将$\hat{f}$的逆傅立叶变换表示为$F ^{−1}\{\hat{f}\}$。

A function and its Fourier transform are related in many useful ways. A few facts (most of them easy to verify) that we will use later in the chapter are:
函数及其傅里叶变换在许多有用的方面相关。 我们将在本章后面使用的一些事实（其中大多数很容易验证）是：

- A function and its Fourier transform have the same squared integral:
  函数及其傅里叶变换具有相同的平方积分： 
  $\int (f(x))^2dx = \int(\hat{f}(u))^2du$

  The physical interpretation is that the two have the same energy (Figure 9.43).
  物理解释是两者具有相同的能量（图9.43）。
  ![Figure 9.43](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.43.png)
  Figure 9.43. The Fourier transform preserves the squared integral of the signal.
  图 9.43。 傅里叶变换保留了信号的平方积分。
  In particular, scaling a function up by a also scales its Fourier transform by $a$. That is, $F{af} = aF{f}$.
  特别是，将函数放大 a 也会将其傅立叶变换放大 $a$。 即 $F{af} = aF{f}$。

- Stretching a function along the x-axis squashes its Fourier transform along the u-axis by the same factor (Figure 9.44):
  沿 x 轴拉伸函数会沿 u 轴将其傅立叶变换压缩相同的因子（图 9.44）：

  ![Figure 9.44](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.44.png)
  Figure 9.44. Scaling a signal along the x-axis in the space domain causes an inverse scale along the u-axis in the frequency domain.
  图 9.44。 在空间域中沿 x 轴缩放信号会导致在频域中沿 u 轴缩放信号。
  $F\{f(x/b)\} = b\hat{f}(bx)  $
  (The renormalization by b is needed to keep the energy the same.) 
  （需要通过 b 进行重整化以保持能量相同。）
  This means that if we are interested in a family of functions of different width and height (say all box functions centered at zero), then we only need to know the Fourier transform of one canonical function (say the box function with width and height equal to one), and we can easily know the Fourier transforms of all the scaled and dilated versions of that function. For example, we can instantly generalize Equation (9.6) to give the Fourier transform of a box of width $b$ and height $a$:
  这意味着，如果我们对一系列不同宽度和高度的函数感兴趣（假设所有框函数都以零为中心），那么我们只需要知道一个规范函数的傅立叶变换（假设宽度和高度相等的框函数） 到一），我们可以很容易地知道该函数的所有缩放和扩张版本的傅里叶变换。 例如，我们可以立即推广方程（9.6)来给出宽度为 $b$ 和高度为 $a$ 的盒子的傅里叶变换：
  $ab\frac{\sin\pi bu}{\pi bu} \\$

- The average value of f is equal to $\hat{f}(0)$. This makes sense since $\hat{f}(0)$ is supposed to be the zero-frequency component of the signal (the DC component if we are thinking of an electrical voltage).
  f 的平均值等于 $\hat{f}(0)$。 这是有道理的，因为 $\hat{f}(0)$ 应该是信号的零频率分量（如果我们考虑的是电压，则为直流分量）。

- If $f$ is real (which it always is for us), $\hat{f}$ is an even function—that is, $\hat{f}(u) = \hat{f}(−u)$. Likewise, if f is an even function then $\hat{f}$ will be real (this is not usually the case in our domain, but remember that we really are only going to care about the magnitude of $\hat{f}$).
  如果 $f$ 是实数（对我们来说始终如此），则 $\hat{f}$ 是偶函数，即 $\hat{f}(u) = \hat{f}(−u) $。 同样，如果 f 是偶函数，那么 $\hat{f}$ 将是实数（在我们的域中通常不是这种情况，但请记住，我们实际上只关心 $\hat{f} 的大小 $）。

### 9.5.2 Convolution and the Fourier Transform 卷积和傅立叶变换

One final property of the Fourier transform that deserves special mention is its relationship to convolution (Figure 9.45). Briefly,
傅立叶变换值得特别提及的最后一个属性是它与卷积的关系（图 9.45）。 简要地，
$F\{f*g\} = \hat{f}\hat{g}$
![Figure 9.45](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.45.png)
Figure 9.45. A commutative diagram to show visually the relationship between convolution and multiplication. If we multiply $f$ and g in space, then transform to frequency, we end up in the same place as if we transformed $f$ and $g$ to frequency and then convolved them. Likewise, if we convolve $f$ and $g$ in space and then transform into frequency, we end up in the same place as if we transformed $f$ and $g$ to frequency, then multiplied them.
图 9.45。 交换图直观地展示了卷积和乘法之间的关系。 如果我们在空间中将 $f$ 和 g 相乘，然后转换为频率，我们最终会得到相同的结果，就像我们将 $f$ 和 $g$ 转换为频率然后对它们进行卷积一样。 同样，如果我们在空间中对 $f$ 和 $g$ 进行卷积，然后转换为频率，我们最终会得到相同的位置，就像我们将 $f$ 和 $g$ 转换为频率，然后将它们相乘一样。

The Fourier transform of the convolution of two functions is the product of the Fourier transforms. Following the by now familiar symmetry, 
两个函数卷积的傅里叶变换是傅里叶变换的乘积。 遵循现在熟悉的对称性，
$\hat{f}*\hat{g}=F\{fg\}$

The convolution of two Fourier transforms is the Fourier transform of the product of the two functions. These facts are fairly straightforward to derive from the definitions.
两个傅里叶变换的卷积是两个函数乘积的傅里叶变换。 这些事实很容易从定义中推导出来。

This relationship is the main reason Fourier transforms are useful in studying the effects of sampling and reconstruction. We’ve seen how sampling, filtering, and reconstruction can be seen in terms of convolution; now the Fourier transform gives us a new domain—the frequency domain—in which these operations are simply products.
这种关系是傅立叶变换可用于研究采样和重建效果的主要原因。 我们已经了解了如何用卷积来看待采样、滤波和重构； 现在，傅里叶变换为我们提供了一个新的域——频域——其中这些运算只是乘积。

### 9.5.3 A Gallery of Fourier Transforms 傅里叶变换画廊

Now that we have some facts about Fourier transforms, let’s look at some examples of individual functions. In particular, we’ll look at some filters from Section 9.3.1, which are shown with their Fourier transforms in Figure 9.46. We have already seen the box function:
现在我们已经了解了有关傅里叶变换的一些事实，让我们看一下各个函数的一些示例。 特别是，我们将查看第 9.3.1 节中的一些滤波器，它们及其傅里叶变换如图 9.46 所示。 我们已经看到了 box 函数：
$F\{f_{box}\} = \frac{\sinπu}{πu}
= sinc\ πu.  $
![Figure 9.46](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.46.png)
Figure 9.46. The Fourier transforms of the box, tent, B-spline, and Gaussian filters.
图 9.46。 盒子滤波器、帐篷滤波器、B 样条滤波器和高斯滤波器的傅立叶变换。

The function $sin x/x$ is important enough to have its own name, $sinc\ x$.(You may notice that $\sin πu/πu$ is undefined for $u = 0$. It is, however, continuous across zero,a nd we take it as understood that we use the limiting value of this ratio, 1, at $u = 0$.  )
函数 $sin x/x$ 非常重要，有自己的名称 $sinc\ x$。（您可能会注意到，$\sin πu/πu$ 对于 $u = 0$ 是未定义的。然而，它是连续的 跨越零，并且我们认为我们使用该比率的极限值 1，在 $u = 0$ 处。）

The tent function is the convolution of the box with itself, so its Fourier transform is just the square of the Fourier transform of the box function:
帐篷函数是盒子与自身的卷积，因此它的傅里叶变换只是盒子函数傅里叶变换的平方：
$F\{f_{tent}\} = \frac{\sin^2 πu}{π^2u^2} = sinc^2πu. \\$

We can continue this process to get the Fourier transform of the B-spline filter (see Exercise 3):
我们可以继续这个过程来获得 B 样条滤波器的傅立叶变换（参见练习 3）：
$F\{f_B\} = \frac{\sin^4 πu}{π^4u^4} = sinc^4πu \\ $

The Gaussian has a particularly nice Fourier transform:
高斯有一个特别好的傅立叶变换：
$F\{f_G\} = e^{-(2πu)^2/2}  $

It is another Gaussian! The Gaussian with standard deviation 1.0 becomes a Gaussian with standard deviation 1/2π.
这是另一个高斯分布！ 标准差为 1.0 的高斯函数变为标准差为 1/2π 的高斯函数。

### 9.5.4 Dirac Impulses in Sampling Theory 抽样理论中的狄拉克脉冲

The reason impulses are useful in sampling theory is that we can use them to talk about samples in the context of continuous functions and Fourier transforms. We represent a sample, which has a position and a value, by an impulse translated to that position and scaled by that value. A sample at position a with value b is represented by $bδ(x − a)$. This way we can express the operation of sampling the function $f(x)$ at a as multiplying $f$ by $δ(x − a)$. The result is $f(a)δ(x − a)$.
脉冲在采样理论中有用的原因是我们可以使用它们来讨论连续函数和傅里叶变换背景下的样本。 我们通过转换到该位置并按该值缩放的脉冲来表示具有位置和值的样本。 位置 a 且值为 b 的样本由 $bδ(x − a)$ 表示。 这样我们就可以将在 a 处对函数 $f(x)$ 进行采样的操作表示为 $f$ 乘以 $δ(x − a)$。 结果是 $f(a)δ(x − a)$。

Sampling a function at a series of equally spaced points is therefore expressed as multiplying the function by the sum of a series of equally spaced impulses, called an impulse train (Figure 9.47). An impulse train with period T, meaning that the impulses are spaced a distance T apart is
因此，在一系列等距点处对函数进行采样表示为将该函数乘以一系列等距脉冲的总和，称为脉冲串（图 9.47）。 周期为 T 的脉冲串，意味着脉冲之间的距离为 T
$s_T(x) = \sum^{∞}_{i= -∞}δ(x - Ti)  $
![Figure 9.47](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.47.png)
Figure 9.47. Impulse trains. The Fourier transform of an impulse train is another impulse train. Changing the period of the impulse train in space causes an inverse change in the period in frequency.
图 9.47。 脉冲列车。 脉冲串的傅里叶变换是另一种脉冲串。 改变空间脉冲序列的周期会导致频率周期的反向变化。

The Fourier transform of $s_1$ is the same as $s_1$: a sequence of impulses at all integer frequencies. You can see why this should be true by thinking about what happens when we multiply the impulse train by a sinusoid and integrate. We wind up adding up the values of the sinusoid at all the integers. This sum will exactly cancel to zero for non-integer frequencies, and it will diverge to $+∞$ for integer frequencies.
$s_1$ 的傅立叶变换与 $s_1$ 相同：所有整数频率的脉冲序列。 通过思考当我们将脉冲串乘以正弦曲线并积分时会发生什么，您可以明白为什么这是正确的。 我们最终将所有整数处的正弦曲线值相加。 对于非整数频率，这个总和将精确地抵消为零，对于整数频率，它将发散到 $+∞$。

Because of the dilation property of the Fourier transform, we can guess that the Fourier transform of an impulse train with period T (which is like a dilation of $s_1$) is an impulse train with period $1/T$ . Making the sampling finer in the space domain makes the impulses farther apart in the frequency domain.
由于傅里叶变换的膨胀特性，我们可以猜测周期为 T 的脉冲序列（类似于 $s_1$ 的膨胀）的傅里叶变换是周期为 $1/T$ 的脉冲序列。 在空间域中进行更精细的采样会使脉冲在频域中相距更远。 

### 9.5.5 Sampling and Aliasing 采样和混叠

Now that we have built the mathematical machinery, we need to understand the sampling and reconstruction process from the viewpoint of the frequency domain. The key advantage of introducing Fourier transforms is that it makes the effects of convolution filtering on the signal much clearer, and it provides more precise explanations of why we need to filter when sampling and reconstructing.
现在我们已经构建了数学机制，我们需要从频域的角度来理解采样和重构过程。 引入傅里叶变换的主要优点是它使卷积滤波对信号的影响更加清晰，并且更精确地解释了为什么我们在采样和重构时需要滤波。

We start the process with the original, continuous signal. In general its Fourier transform could include components at any frequency, although for most kinds of signals (especially images), we expect the content to decrease as the frequency gets higher. Images also tend to have a large component at zero frequency— remember that the zero-frequency, or DC, component is the integral of the whole image, and since images are all positive values this tends to be a large number.
我们从原始的连续信号开始该过程。 一般来说，它的傅里叶变换可以包括任何频率的分量，尽管对于大多数类型的信号（尤其是图像），我们预计随着频率的升高，内容会减少。 图像在零频率处也往往有一个很大的分量 - 请记住，零频率或 DC 分量是整个图像的积分，并且由于图像都是正值，因此这往往是一个很大的数字。

Let’s see what happens to the Fourier transform if we sample and reconstruct without doing any special filtering (Figure 9.48). When we sample the signal, we model the operation as multiplication with an impulse train; the sampled signal is $fs_T$ . Because of the multiplication-convolution property, the FT of the sampled signal is $\hat{f}* \hat{s_T} = \hat{f} * s_{1/T} $. 
让我们看看如果我们在不进行任何特殊滤波的情况下进行采样和重建，傅里叶变换会发生什么（图 9.48）。 当我们对信号进行采样时，我们将运算建模为与脉冲序列相乘； 采样信号是 $fs_T$ 。 由于乘法卷积特性，采样信号的 FT 为 $\hat{f}* \hat{s_T} = \hat{f} * s_{1/T} $。
<img src="E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.48.png" alt="Figure 9.48" style="zoom:80%;" />
Figure 9.48. Sampling and reconstruction with no filtering. Sampling produces alias spectra that overlap and mix with the base spectrum. Reconstruction with a box filter collects even more information from the alias spectra. The result is a signal that has serious aliasing artifacts.
图 9.48。 无过滤的采样和重建。 采样产生与基础光谱重叠并混合的混叠光谱。 使用盒式滤波器进行重建可以从别名光谱中收集更多信息。 结果是信号具有严重的混叠伪影。

Recall that $δ$ is the identity for convolution. This means that
回想一下，$δ$ 是卷积的恒等式。 这意味着
$(\hat{f}*s_{1/T})(u) = \sum^∞_{i=-∞}\hat{f}(u - i/T);  $

that is, convolving with the impulse train makes a whole series of equally spaced copies of the spectrum of f. A good intuitive interpretation of this seemingly odd result is that all those copies just express the fact (as we saw back in Section 9.1.1) that frequencies that differ by an integer multiple of the sampling frequency are indistinguishable once we have sampled—they will produce exactly the same set of samples. The original spectrum is called the base spectrum and the copies are known as alias spectra.
也就是说，与脉冲序列卷积生成 f 频谱的一系列等距副本。 对这个看似奇怪的结果的一个很好的直观解释是，所有这些副本都只是表达了这样一个事实（正如我们在第 9.1.1 节中看到的那样）：一旦我们采样，相差采样频率整数倍的频率就无法区分——它们将 产生完全相同的一组样本。 原始光谱称为基础光谱，副本称为别名光谱。

The trouble begins if these copies of the signal’s spectrum overlap, which will happen if the signal contains any significant content beyond half the sample frequency. When this happens, the spectra add, and the information about different frequencies is irreversibly mixed up. This is the first place aliasing can occur, and if it happens here, it’s due to undersampling—using too low a sample frequency for the signal.
如果信号频谱的这些副本重叠，那么麻烦就开始了，如果信号包含超过采样频率一半的任何重要内容，就会发生这种情况。 当这种情况发生时，频谱会相加，不同频率的信息就会不可逆地混合在一起。 这是第一个可能发生混叠的地方，如果在这里发生混叠，那是由于采样不足——对信号使用了太低的采样频率。 

Suppose we reconstruct the signal using the nearest-neighbor technique. This is equivalent to convolving with a box of width 1. (The discrete-continuous convolution used to do this is the same as a continuous convolution with the series of impulses that represent the samples.) The convolution-multiplication property means that the spectrum of the reconstructed signal will be the product of the spectrum of the sampled signal and the spectrum of the box. The resulting reconstructed Fourier transform contains the base spectrum (though somewhat attenuated at higher frequencies), plus attenuated copies of all the alias spectra. Because the box has a fairly broad Fourier transform, these attenuated bits of alias spectra are significant, and they are the second form of aliasing, due to an inadequate reconstruction filter. These alias components manifest themselves in the image as the pattern of squares that is characteristic of nearest-neighbor reconstruction.
假设我们使用最近邻技术重建信号。 这相当于与宽度为 1 的框进行卷积。（用于执行此操作的离散连续卷积与与代表样本的一系列脉冲进行连续卷积相同。）卷积乘法属性意味着 重建的信号将是采样信号的频谱和盒子的频谱的乘积。 由此产生的重建傅里叶变换包含基础频谱（尽管在较高频率下有所衰减），以及所有混叠频谱的衰减副本。 由于该盒子具有相当宽的傅里叶变换，因此混叠频谱的这些衰减位非常重要，并且由于重建滤波器不充分，它们是混叠的第二种形式。 这些混叠分量在图像中表现为正方形图案，这是最近邻重建的特征。

#### Preventing Aliasing in Sampling 防止采样中的混叠

To do high quality sampling and reconstruction, we have seen that we need to choose sampling and reconstruction filters appropriately. From the standpoint of the frequency domain, the purpose of lowpass filtering when sampling is to limit the frequency range of the signal so that the alias spectra do not overlap the base spectrum. Figure 9.49 shows the effect of sample rate on the Fourier transform of the sampled signal. Higher sample rates move the alias spectra farther apart, and eventually whatever overlap is left does not matter.
为了进行高质量的采样和重建，我们已经看到我们需要适当地选择采样和重建滤波器。 从频域的角度来看，采样时低通滤波的目的是限制信号的频率范围，使混叠频谱不与基础频谱重叠。 图 9.49 显示了采样率对采样信号傅里叶变换的影响。 较高的采样率会使混叠频谱相距更远，最终留下的任何重叠都无关紧要。
![Figure 9.49](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.49.png)
Figure 9.49. The effect of sample rate on the frequency spectrum of the sampled signal. Higher sample rates push the copies of the spectrum apart, reducing problems caused by overlap.
图 9.49。 采样率对采样信号频谱的影响。 更高的采样率将频谱的副本分开，减少了重叠引起的问题。

The key criterion is that the width of the spectrum must be less than the distance between the copies—that is, the highest frequency present in the signal must be less than half the sample frequency. This is known as the Nyquist criterion, and the highest allowable frequency is known as the Nyquist frequency or Nyquist limit. The Nyquist-Shannon sampling theorem states that a signal whose frequencies do not exceed the Nyquist limit (or, said another way, a signal that is bandlimited to the Nyquist frequency) can, in principle, be reconstructed exactly from samples.
关键标准是频谱的宽度必须小于副本之间的距离，也就是说，信号中存在的最高频率必须小于采样频率的一半。 这称为奈奎斯特准则，最高允许频率称为奈奎斯特频率或奈奎斯特极限。 奈奎斯特-香农采样定理指出，原则上，频率不超过奈奎斯特极限的信号（或者换句话说，带宽限制为奈奎斯特频率的信号）可以从样本中精确重建。

With a high enough sample rate for a particular signal, we don’t need to use a sampling filter. But if we are stuck with a signal that contains a wide range of frequencies (such as an image with sharp edges in it), we must use a sampling filter to bandlimit the signal before we can sample it. Figure 9.50 shows the effects of three lowpass (smoothing) filters in the frequency domain, and Figure 9.51 shows the effect of using these same filters when sampling. Even if the spectra overlap without filtering, convolving the signal with a lowpass filter can narrow the spectrum enough to eliminate overlap and produce a well-sampled representation of the filtered signal. Of course, we have lost the high frequencies, but that’s better than having them get scrambled with the signal and turn into artifacts.
如果特定信号的采样率足够高，我们就不需要使用采样滤波器。 但是，如果我们遇到包含各种频率的信号（例如具有锐利边缘的图像），则必须使用采样滤波器对信号进行带宽限制，然后才能对其进行采样。 图 9.50 显示了频域中三个低通（平滑）滤波器的效果，图 9.51 显示了采样时使用这些相同滤波器的效果。 即使频谱在没有滤波的情况下重叠，用低通滤波器对信号进行卷积也可以使频谱变窄，足以消除重叠并产生滤波后信号的良好采样表示。 当然，我们失去了高频，但这比让它们与信号混杂并变成伪影要好。
![Figure 9.50](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.50.png)
Figure 9.50. Applying lowpass (smoothing) filters narrows the frequency spectrum of a signal.
图 9.50。 应用低通（平滑)滤波器可以缩小信号的频谱。

![Figure 9.51](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.51.png)
Figure 9.51. How the lowpass filters from Figure 9.50 prevent aliasing during sampling. Lowpass filtering narrows the spectrum so that the copies overlap less, and the high frequencies from the alias spectra interfere less with the base spectrum.
图 9.51。 图 9.50 中的低通滤波器如何防止采样期间出现混叠。 低通滤波使频谱变窄，从而使副本重叠更少，并且混叠频谱中的高频对基本频谱的干扰更少。

#### Preventing Aliasing in Reconstruction 防止重建中出现锯齿

From the frequency domain perspective, the job of a reconstruction filter is to remove the alias spectra while preserving the base spectrum. In Figure 9.48, we can see that the crudest reconstruction filter, the box, does attenuate the alias spectra. Most important, it completely blocks the DC spike for all the alias spectra. This is a characteristic of all reasonable reconstruction filters: they have zeroes in frequency space at all multiples of the sample frequency. This turns out to be equivalent to the ripple-free property in the space domain.
从频域的角度来看，重建滤波器的作用是去除混叠频谱，同时保留基础频谱。 在图 9.48 中，我们可以看到最原始的重建滤波器（盒子）确实衰减了混叠频谱。 最重要的是，它完全阻挡了所有混叠频谱的直流尖峰。 这是所有合理的重构滤波器的一个特征：它们在频率空间中在采样频率的所有倍数处都有零点。 事实证明，这相当于空间域中的无波纹特性。

So a good reconstruction filter needs to be a good lowpass filter, with the added requirement of completely blocking all multiples of the sample frequency. The purpose of using a reconstruction filter different from the box filter is to more completely eliminate the alias spectra, reducing the leakage of high-frequency artifacts into the reconstructed signal, while disturbing the base spectrum as little as possible. Figure 9.52 illustrates the effects of different filters when used during reconstruction. As we have seen, the box filter is quite “leaky” and results in plenty of artifacts even if the sample rate is high enough. The tent filter, resulting in linear interpolation, attenuates high frequencies more, resulting in milder artifacts, and the B-spline filter is very smooth, controlling the alias spectra very effectively. It also smooths the base spectrum some—this is the tradeoff between smoothing and aliasing that we saw earlier.
因此，一个好的重构滤波器必须是一个好的低通滤波器，并且还需要完全阻止采样频率的所有倍数。 使用与盒式滤波器不同的重建滤波器的目的是更完全地消除混叠频谱，减少高频伪影泄漏到重建信号中，同时尽可能少地干扰基础频谱。 图 9.52 说明了在重建过程中使用不同滤波器的效果。 正如我们所看到的，盒式滤波器非常“泄漏”，即使采样率足够高，也会产生大量伪影。 帐篷滤波器产生线性插值，更多地衰减高频，从而产生更温和的伪影，而 B 样条滤波器非常平滑，可以非常有效地控制混叠频谱。 它还对基础频谱进行了一些平滑——这是我们之前看到的平滑和混叠之间的权衡。
![Figure 9.52](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.52.png)
Figure 9.52. The effects of different reconstruction filters in the frequency domain. A good  reconstruction filter attenuates the alias spectra effectively while preserving the base spectrum.
图 9.52。 频域中不同重构滤波器的效果。 良好的重建滤波器可以有效地衰减混叠频谱，同时保留基础频谱。

#### Preventing Aliasing in Resampling 防止重采样中的混叠

When the operations of reconstruction and sampling are combined in resampling, the same principles apply, but with one filter doing the work of both reconstruction and sampling. Figure 9.53 illustrates how a resampling filter must remove the alias spectra and leave the spectrum narrow enough to be sampled at the new sample rate.
当在重采样中组合重建和采样操作时，适用相同的原理，但由一个滤波器同时完成重建和采样工作。 图 9.53 说明了重采样滤波器如何必须去除混叠频谱并使频谱足够窄以便以新的采样率进行采样。
![Figure 9.53](E:/持久化数据/笔记/Markdown/图形学/Fundamentals of Computer Graphics/Images/Figure 9.53.png)
Figure 9.53. Resampling viewed in the frequency domain. The resampling filter both reconstructs the signal (removes the alias spectra) and bandlimits it (reduces its width) for sampling at the new rate.
图 9.53。 在频域中查看重采样。 重采样滤波器既重建信号（去除混叠频谱），又对其进行频带限制（减小其宽度)，以便以新的速率进行采样。

### 9.5.6 Ideal Filters vs. Useful Filters 理想过滤器与有用过滤器

Following the frequency domain analysis to its logical conclusion, a filter that is exactly a box in the frequency domain is ideal for both sampling and reconstruction. Such a filter would prevent aliasing at both stages without diminishing the frequencies below the Nyquist frequency at all.
根据频域分析得出的逻辑结论，频域中恰好是一个盒子的滤波器对于采样和重建都是理想的。 这样的滤波器可以防止两个阶段的混叠，而根本不会减少奈奎斯特频率以下的频率。

Recall that the inverse and forward Fourier transforms are essentially identical, so the spatial domain filter that has a box as its Fourier transform is the function $\sin πx/πx = sinc πx$.
回想一下，逆傅立叶变换和正向傅立叶变换本质上是相同的，因此以框作为傅立叶变换的空间域滤波器是函数 $\sin πx/πx = sinc πx$。

However, the sinc filter is not generally used in practice, either for sampling or for reconstruction, because it is impractical and because, even though it is optimal according to the frequency domain criteria, it doesn’t produce the best results for many applications.
然而，sinc 滤波器在实践中通常不用于采样或重建，因为它不切实际，而且即使根据频域标准它是最佳的，它也不会为许多应用产生最佳结果。

For sampling, the infinite extent of the sinc filter, and its relatively slow rate of decrease with distance from the center, is a liability. Also, for some kinds of sampling, the negative lobes are problematic. A Gaussian filter makes an excellent sampling filter even for difficult cases where high-frequency patterns must be removed from the input signal, because its Fourier transform falls off exponentially, with no bumps that tend to let aliases leak through. For less difficult cases, a tent filter generally suffices.
对于采样来说，sinc 滤波器的无限范围及其随着距中心距离的减小而相对缓慢的速率是一个缺点。 此外，对于某些类型的采样，负瓣是有问题的。 即使对于必须从输入信号中去除高频模式的困难情况，高斯滤波器也是一个出色的采样滤波器，因为它的傅里叶变换呈指数下降，并且没有容易让混叠泄漏的凹凸。 对于不太困难的情况，帐篷过滤器通常就足够了。

For reconstruction, the size of the sinc function again creates problems, but even more importantly, the many ripples create “ringing” artifacts in reconstructed signals.
对于重建来说，sinc 函数的大小再次产生了问题，但更重要的是，许多纹波会在重建信号中产生“振铃”伪影。

## Exercises 练习

1. Show that discrete convolution is commutative and associative. Do the same for continuous convolution. 
   证明离散卷积是可交换的和结合的。 对连续卷积做同样的事情。
2. Discrete-continuous convolution can’t be commutative, because its arguments have two different types. Show that it is associative, though.
   离散连续卷积不能交换，因为它的参数有两种不同的类型。 不过，请证明它是关联的。
3. Prove that the B-spline is the convolution of four box functions.
   证明B样条是四个框函数的卷积。
4. Show that the “flipped” definition of convolution is necessary by trying to show that convolution is commutative and associative using this (incorrect) definition (see the footnote on page 192):
   通过尝试使用这个（不正确的）定义来证明卷积是可交换的和结合的，证明卷积的“翻转”定义是必要的（参见第 192 页的脚注）：
   $(a*b)[i] = \sum_ja[j]b[i + j]  \\$
5. Prove that $F\{f*g\} = \hat{f}\hat{g}$  and $\hat{f}*\hat{g} = F\{fg\}$. 
   证明 $F\{f*g\} = \hat{f}\hat{g}$ 且 $\hat{f}*\hat{g} = F\{fg\}$。
6. Equation 9.4 can be interpreted as the convolution of a with a filter $\overline{f}$. Write a mathematical expression for the “de-rippled” filter $\overline{f}$. Plot the filter that results from de-rippling the box, tent, and B-spline filters scaled to $s = 1.25$.
   方程 9.4 可以解释为 a 与滤波器 $\overline{f}$ 的卷积。 为“去波纹”滤波器 $\overline{f}$ 编写一个数学表达式。 绘制通过对盒子、帐篷和 B 样条滤波器去波纹而得到的滤波器，并缩放至 $s = 1.25$。