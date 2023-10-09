一、内容简介：  
本教程介绍了一个强大的电路设计和仿真工具TINA-TI。TINA-TI可用于对各种电路进行设计、测试和故障诊断。这些电路可以是简单的或者高级的具有复杂结构的电路，TINA-TI对它们没有任何节点或器件数量的限制。本教程主要介绍TINA-TI软件的基本特征和电路仿真方法。首先介绍了TINA-TI的特点及功能、软件的下载与安装，然后通过一个电路实例介绍了电路原理图编辑，通过另外一个TINA-TI提供的电路示例介绍了电路分析方法以及用虚拟仪器测量电路的方法，最后介绍了TINA-TI的其它辅助功能。  
目录：  
1 概述 (3)  
2 电路示例 (3)  
2.1 放大器和线性电路： (3)  
2.2 SMPS（开关式电源）： (4)  
2.3 其它 (4)  
3 TINA-TI的使用 (4)  
3.1 下载与安装TINA-TI (4)  
3.2 启动TINA-TI (5)  
3.3 搭建电路 (6)  
3.3.1 电路原理 (6)  
3.3.2 在原理图中添加元件 (7)  
3.3.3 添加无源元件 (8)  
3.3.4 布置元件和连线 (10)  
3.4 分析电路 (11)  
3.4.1 直流分析 (13)  
3.4.2 瞬态分析 (15)  
3.4.3 交流分析 (16)  
3.5 测量电路 (18)  
3.5.1 万用表 (18)  
3.5.2 示波器 (19)  
3.5.3 信号分析仪 (19)  
3.5.4 函数发生器 (21)  
3.6 TINA-TI的其它辅助功能 (22)

1、概述  
德州仪器公司（TI）与DesignSoft公司联合为客户提供了一个强大的电路仿真工具TINA-TI。TINA-TI适用于对模拟电路和开关式电源（SMPS）电路的仿真，是进行电路开发与测试的理想选择。TINA基于SPICE引擎，是一款功能强大而易于使用的电路仿真工具；而TINA-TI 则是完整功能版本的TINA，并加载了TI公司的宏模型以及无源和有源器件模型。  
TI之所以选择TINA仿真软件而不是其它的基于SPICE技术的仿真器，是因为它同时具有强大的分析能力和简单直观的图形界面，并且易于使用。  
TINA-TI 提供了多种分析功能，包括SPICE的所有传统直流、交流、瞬态、频域、噪声分析等功能。虚拟仪器非常直观且功能丰富，允许用户选择输入波形、探针电路节点电压和波形。TINA的原理图捕捉非常直观，使用户真正能够“快速入门”。另外TINA具有广泛的后处理功能，允许用户设置输出结果的格式。  
2、电路示例  
TINA-TI中包括了许多应用电路示例，给用户提供最快捷、最容易的电路仿真方式。这些电路示例可在TINA的全部版本上运行，可配置为运行示例中所示的分析类型。用户可以修改它们并用“另存为”保存更改。  
可以从安装TINA-TI软件目录的"Examples"文件夹下获得这些文件，可在软件菜单栏中点击“文件”，然后选择菜单选项“打开示例…”来打开。应用电路示例包括以下几种。  
2.1、放大器和线性电路：  
-音频（音频运算放大器滤波器、麦克风前置放大器）  
-负载电容补偿（C-oad 补偿、线驱动器）  
-比较器（比较器电路）  
-控制环路（PI温度控制）  
-电流环路（4-20mA、0-10mA）  
-电流测量（电流发送、并联测量）  
-差分放大器（差分输入至单端输出、单端输入至差分输出等）  
-用FilterPro设计的滤波器（包括多反馈和Sallen-Key拓扑，由FilterPro软件设计生成）  
-其它滤波器（全通、低通、高通、可调、双T形）  
-振荡器（维恩电桥）  
-功率放大器（激光驱动器、TEC驱动器、并行电源、LED驱动器、光电二极管驱动器）  
-精密放大器（低漂移、低噪声、低偏移、分压器）  
-传感器调节（热敏、电阻电桥、电容电桥、Inst放大器滤波器）  
-信号处理（峰值检测器、削波放大器）  
-单电源（单电源运算放大器电路）  
-测试（电容乘法器、调节电压基准、通用集成器、负载消除、x1000 缩放放大器、准耦合AC放大器）  
-互阻抗放大器（光电二极管、光探测器）  
-电压电流转换器（电压至电流、电流至电流）  
-宽带（宽带运算放大器电路）  
2.2、SMPS（开关式电源）：  
-针对SMPS器件的器件评估模块(EVM)参考设计  
2.3、其它  
以下示例文件目前尚未包括在TINA-TI 的“示例”文件夹下，但可从以下链接下载：  
-噪声分析：  
噪声源http://www.ti.com.cn/en/download/aap/zip/sbfc030.zip  
-传感器仿真器：  
RTD 仿真器http://www.ti.com.cn/en/download/aap/zip/sbfc031.zip  
3、TINA-TI的使用  
3.1、下载与安装TINA-TI  
从TI的TINA-TI网页www.ti.com/tool/tina-ti上下载TINA-TI，如图1所示，或者在TI主页www.ti.com通过输入关键词TINA搜索获得下载信息。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323105931619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图1 TINA-TI下载网页  
目前所发布的TINA-TI版本的最低硬件和软件要求是：  
-兼容IBM PC的计算机，运行微软Windows 98/ME/NT/2000/XP操作系统  
-奔腾系列或同等级处理器  
-64MB的内存  
-至少100MB的硬盘空余空间  
-VGA适配器和显示器  
-鼠标  
3.2、启动TINA-TI  
TINA-TI软件启动后，首先出现在屏幕上的界面为原理图编辑器，如图2所示。图中空白的工作区是设计窗口，用于搭建测试电路。原理图编辑器标题栏的下面包括四行工具。  
第一行是一个可操作的菜单行选项，如文件操作、分析操作、测试及测量设备的选择等等。  
第二行位于菜单行下方，是一行与文件操作或TINA任务相关联的快捷图标。  
第三行图标是可供选择的特定的元件符号，这些元件包括基本的无源元件、  
半导体器件以及精密器件的宏模型，可以利用这些元件来搭建电路原理图。  
第四行是元件库选项卡，用于选择不同的元件分组，包括基本元件、开关元件、仪表、发生源、半导体、制造商模型等。当选定某个选项卡之后，相应的元件库中的元件符号将显示于第三行。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323105947814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图2 TINA-TI原理图编辑器界面  
3.3、搭建电路  
3.3.1、电路原理  
本节以一个实际模拟电路为例，说明TINA-TI如何能快速简便地搭建和编辑电路。选择的模拟电路为一个高输出阻抗、1 kHz的正弦波振荡电路，该电路采用具有稳定振幅的文氏桥振荡器，如图3所示。电路中的运放选用德州仪器的CMOS运算放大器OPA743，该放大器适用于该设计，并能提供良好的直流和交流性能。OPA743正常工作的供电电压范围为+3.5V至+12V，该例中所需要的电压为+5V。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323105956311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图3 文氏桥振荡电路  
3.3.2、在原理图中添加元件  
搭建文氏桥振荡器电路的第一步是选择运算放大器OPA743，具体操作如下：  
步骤1：在原理图编辑器界面的第四行选择‘制造商模型’选项卡，如图4所示；  
步骤2：在第三行元件组中点击最左边的运算放大器符号，出现运算放大器模型列表。  
步骤3：向下滚动列表并单击OPA743，然后点击‘确定’按钮完成选择。运算放大器的标识符将出现在电路工作区。  
步骤4：用鼠标将该运算放大器的标识符拖动到相应位置，点击鼠标左键，它将被锁定到电路工作区的当前位置处。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110005753.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图4 在TINA-TI中放置元件  
也可以通过Insert->Macro…菜单来选择其它的运算放大器模型。此外，宏和多种模拟及SMPS电路示例也可以通过Insert菜单获得，具体操作为  
Insert->Macro…TinaTI_7.0->Examples，选择合适的电路文件夹打开电路。  
3.3.3、添加无源元件  
搭建文氏桥振荡器的第二步是选择电阻和电容等无源元件。添加元件时，首先点击原理图编辑器界面第四行的选项卡来选择所需的元件分组，然后从第三行元件符号中选中相应的元件，并将其拖动到电路工作区的相应位置，通过点击鼠标左键将其锁定到位，然后修改其参数。具体操作如图5所示。  
步骤1：从第四行选项卡中选择‘基本’分组；  
步骤2：从第三行中选中电阻符号并将其拖放到运算放大器标识符的旁边。TINA-TI将该电阻命名为R1。R1的初始值是1k，该值可以根据需要进行修改。  
步骤3：用鼠标左键双击R1标识符，弹出元件参数列表窗口，可以修改参数值。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032311001951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图5 放置无源元件  
步骤4：修改元件参数。电阻的阻值和其它元件的特性可以通过在参数列表窗中选择特定的参数框并改变数值来进行修改。在图5中R1的参数列表中选中某个参数框，例如‘电阻’，然后输入一个新的数值来替换原来的数值，例如4.7k，电路中R1的电阻值就从1k变为了4.7k。完成参数设置以后，点击‘确定’按钮关闭参数列表。其它无源器件、电源等也具有相似的参数列表。  
按照以上步骤依次将其余电阻、电容放置到运放周围，并修改参数列表使其具有合适的值，结果如图6所示。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110033832.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图6 元件布局图  
3.3.4、布置元件和连线  
选定并将所有元件放置到适当的位置以后，就可以用走线将它们连接起来组成电路。每个元件都有若干用于进行电路连接的节点。TINA将这些节点显示为一个小的红色的‘x’，用走线可将元件节点与其它元件节点连接起来。只要将鼠标指针放置在一个节点连接处然后保持左键被按下，移动鼠标就可绘制一条走线，当走线到达预定的终端连接点时，释放鼠标左键，即可完成元件的连接。连线功能还可以通过点击‘插入’菜单项选择‘连接线’，或选择图标栏中的像一个小铅笔的图标来实现。图7说明了TINA-TI软件的布线功能。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110046431.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图7 用走线将元件连在一起  
另外，在‘基本’元件组中有一个便于使用的元件‘跳线’，它看上去像一个倒下的字母‘T’，如图6、7中下方电路所示。跳线可以用来连接相似或相关的电路功能，如图6中的电源V+、V–，或任何其它具有多连接的电路点。使用跳线能减少布线，使电路结构更加清晰。值得注意的是，共用的跳线必须被标记为相同的标签名称，才表示它们连在一起，例如图6中的电源V+、V–。3.4 分析电路  
当电路原理图的编辑完成后，就可以做电路仿真和分析了。通过选择‘分析’菜单进入分析进程，随后出现多个选项，包括错误规则检查(ERC)、模式、选择控制对象、设定分析参数、分析列表。分析列表包括直流、交流、瞬态、稳态、傅里叶或噪声等分析方法，选中其中之一进行分析。  
分析菜单项的第一个选项是错误规则检查ERC。选择此项功能，TINA软件对电路自动进行检查，然后弹出一个窗口列出所有电路错误。点击窗口中的错误项，原理图中的错误指针将被选中。错误窗口还能列出在分析过程中所遇到的其  
它类型的电路错误。即使ERC没被选中，TINA也将在仿真开始时自动执行错误检查。  
模式、选择控制对象、设定分析参数三个选项一般采用默认设置即可，需要时可进行修改设置。  
分析列表中常用的分析方式包括直流、交流、瞬态分析，直流分析能够对正常的直流工作状态进行验证，交流分析能显示交流的输出波形，瞬态分析能显示频率响应特性。  
本节中以Tina-TI自带的例子Low Noise Amplifier 300kHz 80dB Gain来说明Tina-TI的分析功能。点击文件->打开例子，出现如图8所示对话框。选择Precision 文件夹下的Low Noise Amplifier 300kHz 80dB Gain.TSC文件，点击打开，结果如图9所示。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110100813.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图8 打开示例对话框  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110116718.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图9 示例原理图  
该电路为两级同相放大电路，每一级的放大倍数为1+(1000/10.1)=100倍，即每一级的增益为20×log10100=40dB，两级的增益和为80dB。  
3.4.1、直流分析  
如图10所示，选中直流分析后显示四项分析选项：计算节点电压、直流结果表、直流传输特性、温度分析。其中‘直流结果表’将显示节点电压和支路的计算结果列表，直流传输特性将生成电路的输入输出的直流扫描。温度分析需要结合选择菜单分析->模式->温度分级选项才能实现。常用的分析选项是‘直流结果表’和‘直流传输特性’。  
为了更好地看到直流分析的结果，将信号源的信号由振幅为1mV、直流偏置为0的交流正弦波，改为直流偏置为1mV的阶跃输入，阶跃输入的幅度为0的信号，即输入为1mV的直流电压。  
‘直流结果表’分析选项，按照图10所示步骤进行：  
1)点击‘分析’菜单项。  
2)选择‘直流分析’。  
3)点击‘直流结果表’。将会出现电压/电流列表。  
4)用鼠标指针作为探针，测试电路节点。  
被探测的节点和测量值将以红颜色显示在电压/电流列表中，使用非常方便，如图10所示。图中显示的红色电压为两级放大后的输出电压，为10V，而输入电压为1mV，放大倍数为10V/1mV=10000，即增益为80dB，与理论计算的相符。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110147674.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图10 显示电压/电流列表的直流分析  
‘直流传输特性’分析选项，按照如下步骤进行：  
1)点击‘分析’菜单项。  
2)选择‘直流分析’。  
3)点击‘直流传输特性’，弹出直流传输特性对话框，如图11所示，填写输入电压的起始值、终点值以及采样数，点击确定，便可看到直流传输特性曲线，如图12所示。可以点击按键来查看点的坐标值，可以看到，当输入电压为1.44mV时，输出接近达到饱和值13.74V。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110159238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图11 直流传输特性对话框  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110207967.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图12 直流传输特性曲线  
3.4.2、瞬态分析  
本节仍以上面的两级放大为例，来分析电路的瞬态响应，为了更好地看到瞬态分析的结果，将信号源的信号改为直流偏置为0的阶跃输入，阶跃输入的幅度为1mV。按照如下步骤进行瞬态分析。  
1)点击‘分析’菜单。  
2)选择‘瞬时现象’。  
3)将会出现图13所示的瞬态分析对话框。输入开始和结束时间，以及其它需要设置的其它参数。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110219235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图13 瞬态分析对话框  
4)点击确定按钮，运行分析，结果如图14所示，可以看到在输入端输入幅度为1mV的阶跃信号之后，输出端的电压变化曲线。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110229810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图14 瞬时分析结果  
3.4.3、交流分析  
也可以进行复杂的交流频域及时域仿真，查看交流传输特性图，包括增益及相位与频率的关系图。按照以下步骤进行交流分析。  
1)点击‘分析’菜单。  
2)选择‘交流分析’。  
3)选择交流传输特性，将会出现图15所示的交流传输特性对话框。输入起始和终止频率，以及其它需要设置的参数，并选择需要的图表，比如振幅和相位曲线、奈奎斯特曲线、群延迟曲线等等。此例中先后选择振幅和相位、奈奎斯特曲线。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110250424.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图15 交流传输特性对话框  
4)点击确定按钮，运行分析，振幅和相位与频率的关系如图16所示，奈奎斯特图如图17所示。在实际的窗口中所显示的坐标轴、刻度、背景网格颜色等等都可以被编辑，所有这些都可由用户根据需要进行设置。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110302619.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图16 振幅和相位与频率的关系  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110309725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图17 奈奎斯特图  
3.5、测量电路  
TINA-TI软件还提供了虚拟仪器，可以对电路节点进行测量和观察。通过点击菜单T&M可以选择万用表、函数发生器、示波器、信号分析仪等常用仪器。  
3.5.1、万用表  
将电路的输入改为直流1mV，然后点击菜单T&M选择万用表，弹出虚拟万用表，如图18所示。在万用表面板中，首先在Function栏里选择测量类型为直流电压测量。由于V out处放置了一个电压指针，并且只有V ou t处放置了电压指针，所以选择直流测量后，Input栏显示被测点为V out，读数框自动显示V out的电压值为10V。如果需要测量其它节点处的电压，可以点击万用表面板中右边的探针符号，然后在相应的节点处点击，显示区域会显示对应节点的电压值。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110320674.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图18 虚拟万用表  
3.5.2、示波器  
如图19所示，将输入改为正弦波输入，然后点击菜单T&M选择示波器，弹出虚拟示波器。在示波器面板中，首先在X Source栏里选择要测量的信号V out，然后点击Run按键来启动示波器，屏幕显示V out的波形，可以通过Time/Div和V olts/Div来调整横轴和纵轴的标度。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110340929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图19 虚拟示波器  
3.5.3、信号分析仪  
虽然示波器可以查看信号是如何随着时间而变化的，但是无法获得电路在频  
域的特性。TINA-TI的信号分析仪可以分析电路的频域特性。  
有两种基本方法来对频域进行测量：傅立叶变换和扫描调谐（swept-tuned）。最常用的[频谱](https://so.csdn.net/so/search?q=%E9%A2%91%E8%B0%B1&spm=1001.2101.3001.7020)分析仪是扫描分析仪，其分析方法是对信号相关频率范围进行扫描，显示出所有频率分量。  
TINA的信号分析仪是基于快速傅立叶变换的频域测量方法，其使用步骤如下：  
1)打开信号分析仪：  
点击菜单T&M，选择信号分析仪，打开的信号分析仪界面如图20所示。  
2)选择输入信号：  
在Channel栏里选择通道采集的信号为V out，然后点击右边的On按键打开通道，并在Coupling栏里选择输入耦合方式为AC即交流耦合。  
3)选择测量模式：  
在Mode栏里选择测量模式，有正弦波扫描、振幅频谱、振幅频谱密度、功率频谱、功率频谱密度，此处选择正弦波扫描。在正弦波扫描模式中，函数发生器可以根据所选扫描的起始频率、终止频率和分辨率产生线性或对数扫描。  
4)显示设置：  
在Display栏里选择显示的分析类型。可选类型有线性级数、对数级数、dB 级数、相位图、波特图（增益和相位）、奈奎斯特图和群时延图，此处选择波特图。调整其高低数值可以指定垂直轴的刻度。  
5)设置频率范围：  
信号分析仪的横轴总是代表频率，可以在Frequency栏里调整其起点和终点来设置开始和终止频率。另一种方式是通过设置中心频率以及围绕中心频率对称展开频宽的频率范围来设置显示频率。如果Resolution选择了对数(Log)，将按照对数单位进行横轴刻度缩放；如果线性(Lin)被选中，横轴将使用线性刻度。  
6)上述选择完成以后点击Mode下面的Start来开始分析，界面中将出现分析的结果波形。  
7)幅度范围控制：  
在Amplitude栏的Range框调整输入幅度范围，按下dB或  
V(电压)来修改幅度单位。自动按钮会将该仪表切换至自动量程模式。在这种模  
式下，仪表自动选择最佳量程来测量输入信号。也可以通过调整Display栏下的  
High和low后面的选择框中的值选择纵坐标的起始和终止值。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200323110356718.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图20 信号分析仪  
3.5.4、函数发生器  
TINA的函数发生器是一个多功能发生器，可用于以下用途之一：  
-参考源：可按指定频率、幅度、DC偏移量和相位产生正弦波。  
-函数发生器：可按指定频率、幅度、DC偏移量和相位产生各种各样的波形。  
-扫描发生器：可产生对数或线性的频率扫描。  
函数发生器使用步骤如下：  
1）点击菜单T&M，选择函数发生器来打开，界面如图21所示。  
2）在Output栏里选择输出信号接入到电路的哪个节点，此处选择Vin。  
3）在Waveform栏里选择输出信号的类型，包括正弦波、方波、三角波、直流或其它波形。  
4）在面板右侧输入输出信号的幅值、偏置、频率、相位等参数。  
5）点击Start按钮开始输出。  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020032311040683.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3h1ZXd1MHpoaWppbmc=,size_16,color_FFFFFF,t_70)  
图21 函数发生器  
3.6、TINA-TI的其它辅助功能  
TINA-TI还有许多待发掘的功能。例如，该软件还提供屏幕上的语境帮助，当鼠标悬停在工作区中的许多图标和区域时将会显示相关表述，如图22所示。如果对于某一特定的分析，用户还需要其它的辅助功能，或是在设置有源元件的参数时需要获得相关帮助，可以在详细帮助文档中进行查找。点击Help菜单，获得关于电路分析或有源器件等的相关信息。