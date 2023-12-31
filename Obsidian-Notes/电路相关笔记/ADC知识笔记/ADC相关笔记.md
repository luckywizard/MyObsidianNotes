
## 1、高速 ADC：
- 流水线型 ADC，趋势是往高速高精度发展，应用在医疗影像采集，通信基础设施，雷达信号处理等领域。16 位 200MSPS 的产品和 12 位 500MSPS 的单片 ADC 产品，这都是产业界最高水平的器件。
> 流水线型 ADC的工作框图：
> ![[电路相关笔记/ADC知识笔记/Pasted image 20221107095717.png]]
ADS5424 由三段 ADC 组成，5 位，5 位和 6 位 ADC，通过转换后的 DAC 还原并相减，  使得 3 段 ADC 各自负责一部分模拟信号的数字转换，转换得到的 16 位数字信号再进行一 次误差校正运算后最终得到 14 位数据完成输出。由于内部有三段 ADC 依次转换，ADS5424的转换延迟为 3 个时钟周期。

## 2、高速 ADC 器件选型
  - 方法是考察 ADC 的**动态指标**或**频域性能**  
 > 测试方法: 就是对 ADC 输入高纯度正弦信号，同步采样后计算其功率谱.
 > ![[电路相关笔记/ADC知识笔记/Pasted image 20221107101432.png]]


> [!note] SNR (Signal to Noise Ratio)
> $SNR = 10 \times \log{  \dfrac{ P_{signal} }{ P_{noise} } }$

> [!note]  **SINAD** **（Signal to Noise and Distortion Ratio）**
>  等于功率谱上基波信号（输入正弦波）的能量比上整个奈奎斯特域内的余下噪声和谐波能量之和。 
>   $$ SINAD = 10 \times \log{ {P_{signal} + P_{noise} + P_{distortion}} \over {P_{noise}} }$$

>[!noet] 有效位数 ENOB **（Effective Number of Bits）**
> $ENOB＝ \dfrac{(SINAD-1.76dB)}{6.02dB}$

> [!note] SFDR **(Spurious Free Dynamic range)**
> 定义为基波能量与余下最大谐波能量之比，或在 dB 为单位时，即为相减.表示在杂散分量干扰基本信号或导致基本信号失真之前可用的动态范围。[[电路相关笔记/ADC知识笔记/dB、dBm、dBc等概念的解释]]
> ![[电路相关笔记/ADC知识笔记/Pasted image 20221107102911.png]]
![[电路相关笔记/ADC知识笔记/Pasted image 20221107135115.png]]

**当要比较两款数据转换器的SFDR时，需要给定基准电平及其工作和信号条件。**我们来对比一下AD9625和AD9680的SFDR，打开它们的官方DataSheet，如下图。其中红色框中给出SFDR时都给出了对应的条件。

![](http://5b0988e595225.cdn.sohucs.com/images/20190921/fb341c39fa2c4aa7a942c544a7788f23.jpeg)

**通常，SFDR是在预先定义的窗口或奈奎斯特频率内观测的。**例如下图，观测窗口选择中间的白色部分，其SFDR将大很多，这是因为整个Fs/2内的最大杂散分量并没有落入定义的观测窗口。

![](http://5b0988e595225.cdn.sohucs.com/images/20190921/6f06ce00a3b040e38dbdf32dcd319975.png)

可以看出，限制SFDR性能的是最恶劣二次谐波或三次谐波，但如果使用正确信道滤波并采用理想采样时钟和良好频率分配，可以轻松地滤除这样的带外谐波。

## 2. 量化误差与分辨率

> [!note] 最小有效位（Least Significant Bit，简称 LSB）
> 将最低位数字量所对应的模拟电平称为称为最小有效位（Least Significant Bit，简称 LSB）
> ![[电路相关笔记/ADC知识笔记/attatchments/Pasted image 20221108095426.png]]
> 我们以横轴最左边一格为例，输入 ≤ 1/2 LSB 时输出为 000b， 1/2 LSB < 输入 ≤ 1 LSB 时输出为 001b，而实际输入范围是 0-1 LSB， ADC 无法分辨在 0 - 1/2 LSB，或是 1/2 LSB - 1 LSB 之间的输入。在最坏情况下，实际输入和量化之后的值之间有 1/2 LSB 的误差。也就是说 ADC 的量化误差为±1/2 LSB。


> [!note] 量化误差
> 量化误差 eq 和 ADC 位数 N 之间有如下关系：
> $e_q = \dfrac12 \times LSB = 0.5 \times \dfrac{FS}{2^N}$
> 量化误差可以看成是一种噪声作用，称为量化噪声，量化噪声将叠加到理想输出上。量化噪声为白噪声，即噪声的随机变量在输出二进制码之间分布的平均值为 0，则其噪声功率计算如下：
> $$
> e^{rms}_{q} = \int_{-\dfrac12 LSB}^{\dfrac12 LSB} (\dfrac{e_q^2}{LSB})de = \dfrac{LSB^2}{12}
> $$
> **均方根(Root mean square, RMS)**

> [!note] 量化噪声信噪比（ SNR）
> ![[电路相关笔记/ADC知识笔记/attatchments/Pasted image 20221108101300.png]]
> 量化噪声均匀的分布在从 0 到 fs/2 的频谱之间。对于 N-bit ADC来说，信号功率和噪声功率之比称为信噪比（ SNR），在只考虑量化噪声的情况下，信噪比的大小为：
> $$SNR = 6.02N + 1.76dB$$


> [!note]混叠-过采样
> ![[电路相关笔记/ADC知识笔记/attatchments/Pasted image 20221108102604.png]]
> 图 1-8 分别给出了 fs及 K 倍 fs采样后得到的频谱。根据 量化噪声的概念, 在采样过程中产生的量化噪声均匀分布在从 0 到 fs/2 的频域范围内，其功率为:
> $$e_q^{rms} = \dfrac{LSB^2}{12}$$
> 由上式可知，==量化噪声功率只与最小分辨率有关，与采样频率无关==，因此若我们将采样频率增大到原来的 K 倍，由于量化噪声总功率仍保持不变而分布区间扩大到了 0 - Kfs/2，所以量化噪声的功率谱密度减小为原来的 1/K，如图 8 中绿框部分所示。因此如果我们对采样后的数据应用一个数字低通滤波器到感兴趣的频带，就可以有效减少感兴趣频带的带内量化噪声总量，从而有效提高带内的信噪比。
> 
$$

$$

> [!note]混叠-欠采样

