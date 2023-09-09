  
本次演示是基于vivado 2018.3版本完成的。硬件是7020 512M DDR 7010与7020的arm a9核是相同的，可以直接参考自己的硬件进行创建自己的工程。  
本次的原始工程文件连接在论坛中已经可以找到。下载并解压，使用其中的xilinx下的文件。当前创建的threadx工程文件除了tx_initialize_low_level.S文件其余都是基于最新的6.1.9.  
  
当前的文件工程见附件  
  
**1、 创建Vivado工程**  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01JZcOJV1gIY7HR05dj_!!299314119.png)  
  
我们创建一个名为Ailurus的工程：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i3/299314119/O1CN01I0XjNO1gIY7GOcwjQ_!!299314119.png)  
  
一路Next  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01IgqQ2U1gIY7FcyI4W_!!299314119.png)  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01zUrb2N1gIY7AV7NOq_!!299314119.png)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i3/299314119/O1CN01p0e6Vf1gIY7Fcv4V5_!!299314119.png)  
  
处理器选择：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01fHuY2P1gIY7GOcXn2_!!299314119.png)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i3/299314119/O1CN01LtRehv1gIY7DybKpn_!!299314119.png)  
  
到这里点击Finish即可.  
  
**2、配置ZYNQ处理器及其相关外设**  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01J7d3p61gIY7CyuHc5_!!299314119.png)  
  
创建新bd文件，使用默认名design_1。  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01h02pDU1gIY77i2PEA_!!299314119.png)  
点击+号，输入zynq, 提示zynq处理器双击：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01AaSTVI1gIY7BmL4RV_!!299314119.png)  
  
我的硬件配置如此，自己可以根据自己的硬件进行配置即可  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01COv7q71gIY7HR1Uvb_!!299314119.png)  
  
DDR 配置  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN012OzKIJ1gIY7AV7ueh_!!299314119.png)  
  
  
点击OK,确认，并如图所示连接：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01uuCq331gIY79t1Ntq_!!299314119.png)  
我们电机下方红线处，验证我们的最小系统设计，如果没有问题进入下一步。file:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image028.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01PMkYvb1gIY7I6taUr_!!299314119.png)  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01Kf93ej1gIY7AV7RYL_!!299314119.png)  
  
生成HDL 文件，再次点击GenerateOutput Products：file:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image032.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01oQTJFS1gIY774iY8C_!!299314119.png)  
  
点击Generate Bitstream:file:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image034.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01lvJwq31gIY7BRVOhA_!!299314119.png)  
  
完成后，到处bit文件到xSDK中  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01SMgojH1gIY79t1NuJ_!!299314119.png)  
  
方便后期的Petalinux等设计使用。一定要勾选Includebitstreamfile:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image037.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01juzBh01gIY7BmLGuU_!!299314119.png)  
  
启动SDK:file:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image039.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01ZrrzQb1gIY75Xc487_!!299314119.png)  
  
  
**3、创建ThreadX 链接库：File->New->Other->Xilinx->LibraryProject点击Next:**  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN011pFHOt1gIY7GOdLfe_!!299314119.png)  
  
修改如红线处：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01ZrrzQb1gIY75Xc487_!!299314119.png)  
  
  
我们把从github上下载好的文件的threadx->common中的inc与src文件夹和Port->cortex_a9->gnu中的inc与src文件夹内容全部拷贝到,当前工程的src文件夹中，  
同时解压文件夹下的src目录下tx_initialize_low_level.S拷贝到当前工程的src文件夹下。同时将下原文件夹中的common_file文件夹拷贝到工程文件夹下面：  
工程文件夹下面文件：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01AtY57N1gIY7EUcQw5_!!299314119.png)  
这个时候我们点击编译，我们可以看到已经成功生成了libtx.a库文件：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i3/299314119/O1CN01Bjk2Ch1gIY7I6plTc_!!299314119.png)  
  
  
**4、 创建ThreadX例程：**  
  
File->New->Application Project,创建一个名为demo_threadx的工程，注意红线部分的选项：第一次创建应用，我们选择基于当前的platform创建一个新的bsp。  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN012NUEts1gIY70lMyN8_!!299314119.png)  
  
选择Hello World:file:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image047.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01WG0R8S1gIY77i5QMo_!!299314119.png)  
  
我们首先编译当前的Hello World 确认无误后继续下一步：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01scNaMS1gIY774hH9L_!!299314119.png)  
  
  
**5、修改编译选项添加common_file文件夹：**  
  
我们右键项目->New->Other->General->Floder->Next->Advance->LinkTo alternate location (Linkerd Floder)->Finishfile:///C:/Users/10322/AppData/Local/Temp/msohtmlclip1/01/clip_image051.png  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01dc92DY1gIY7FczEJz_!!299314119.png)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i3/299314119/O1CN01sV0dEJ1gIY77i4owa_!!299314119.png)  
  
  
这时候我们将HelloWorld.c文件修改为我们下载的demo中的demo_threadx.c文件并且编译：出现error: tx_api.h: No such file or directory错误， 因为该文件在tx库工程中，我们在demo_threadx工程中添加对应的include文件夹以及对应的库的文件夹：  
右键demo_threadx工程，属性->C/C++ Build->Settings->ARM v7Gcc compiler->Inferred Options->SoftWare Platform增减/tx/src文件夹：  
C/C++ Build->Settings->ARM v7 Linker ->Libraries增减之前生成的tx库；  
在C/C++ Build->Settings->ARM v7 Linker-> Inferred Options->SoftWare Platform中增加对应库的文件夹。  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01kpCmuX1gIY75XbnV2_!!299314119.png)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01giBRBr1gIY7HR0DyP_!!299314119.png)  
  
此时我们重新进行编译：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01mpL4eg1gIY79t17G2_!!299314119.png)  
  
  
编译完成，进行一下测试：右键工程，Debug As -> Debug Configurations->XilinxC/C++ application (System Debuger)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01ZCpo4C1gIY7I6s722_!!299314119.png)  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01ivJtDn1gIY7Dyc0Tb_!!299314119.png)  
  
至此，demo_threadx工程创建完毕：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i4/299314119/O1CN01CDwZ3E1gIY7GOa85f_!!299314119.png)  
  
其余的关于FileX、USBX、NetX的工程创建可以按照这个创建，他们都依赖于libtx.a库，比如USBX,NetX等同时还依赖于FileX的库，NetX需要按照自己的phy芯片修改对应驱动，其余的就可以按照此例子在对应位置添加对应文件以及目录即可。  
  
这是早些时候的测试版本：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i1/299314119/O1CN01wesAzP1gIY7HQzcYi_!!299314119.png)  
  
网络测试：  
  
![ZYNQ ThreadX 部分移植与演示](https://img.alicdn.com/imgextra/i2/299314119/O1CN01n1eaaf1gIY75XbOZr_!!299314119.png)



[ZYNQ ThreadX 部分移植与演示 - uCOS & uCGUI & emWin & embOS & TouchGFX & ThreadX - 硬汉嵌入式论坛 - Powered by Discuz! (armbbs.cn)](https://www.armbbs.cn/forum.php?mod=viewthread&tid=109603)

  
Ailurus.7z