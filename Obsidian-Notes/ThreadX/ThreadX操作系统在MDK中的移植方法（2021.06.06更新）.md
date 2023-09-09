1. 前言
微软于最近开源了 ThreadX 操作系统，关于这个RTOS有多牛逼，请看硬汉哥的这篇文章：

ThreadX全家桶初探，一旦推广起来，对其它RTOS和中间件几乎是毁灭性打击
本文中使用的开发板为小熊派IoT开发板，主控为STM32L431RCT6：



在移植之前，请确保你的MDK版本至少是5.30，否则会失败，可以在硬汉哥的不限速镜像下载：

MDK5.29，5.30和各种软件包镜像下载（2020-06-07）
请准备一份可以正常使用printf串口输出的裸机工程，本文中我使用cubemx生成。

2. 复制ThreadX源码
ThreadX源码请访问开源仓库获取：https://github.com/azure-rtos/threadx


3. 添加源码到MDK工程
新建threadX/common分组，添加threadX/common/src下的所有c文件：

新建threadX/ports分组，此时需要根据编译环境来选择。

此处我们使用的是AC5编译器，则添加 threadX\ports\cortex_m4\ac5\src 下的所有 .s 文件：

设置使用AC5编译器：

添加头文件路径：

设置ASM汇编头文件路径：


4. 添加并修改适配底层文件
4.1. tx_initialize_low_level.s
threadX官方提供了一个底层适配文件tx_initialize_low_level.s，所在位置如图：

这里我就不得不吐槽一下了！

本来这个文件中实现了_tx_initialize_low_level()函数，该函数用于完成处理器的底层初始化，包括：

设置中断向量表
设置用于产生时钟节拍的定位器（Systick）
保存系统栈顶指针给中断程序使用
寻找RAM中首块可用地址传入tx_application_define函数供使用，也就是first_unused_memory指针的值
但是threadx在v6版本及以后，竟然想在这个文件中接管原有的处理器启动文件，证据如下。

设置堆栈环境的证据：

重新定义向量表的证据：

接管复位程序的证据：

作为一个用来提供调度能力的RTOS，仅仅接管pendSV中断和Systick中断就够了，甚至Systick中断还需要给HAL库用，不能直接接管走，竟然想把系统所有中断都接管了……

是该说野心勃勃呢？还是该说画蛇添足呢？

退一步海阔天空，把系统所有中断直接都接管了总得干点正事吧~

接管中断了就写个这？？？

吐槽归吐槽，接着干活！移植threadx之后玩起来还是很舒服的！

4.2. 添加适配文件
将 tx_initialize_low_level_sample.S 文件复制出来一份，改名为 tx_initialize_low_level_bearpi.S，作为本项目的适配文件：

将该文件添加到工程中：


4.3. 修改适配文件
① 将没有用到的标号注释，手动添加_Vectors和__initial_sp标号，分别是STM32启动文件中导出的中断向量表和栈顶指针初始值：

② 设置时钟频率（80Mhz）和时钟节拍（1ms），该值用来初始化Systick定时器：

③ 将设置堆栈的代码全部注释（堆栈环境已经在STM32启动文件中设置了）

④ 将 threadx 定义的中断向量表全部注释（使用STM32启动文件中定义的向量表）：

⑤ 注释threadx定义的复位处理程序（使用STM32启动文件中的复位程序）：

⑥ 修改threadx底层初始化函数：


⑦ 注释用不到的函数：

⑧ 处理Systick中断函数：


4.4. 注释HAL库中提供的中断函数
去除原有stm32l4xx_it.c中的 PendSV 和 Systick 中断服务函数：

至此，移植完成，编译会提示有一个错误：

这个函数是留给用户自己来定义应用程序入口的，接下来会创建。

5. 编写应用代码
新建一个application_entry.c文件并加入到工程中，在其中编写两个任务，然后在tx_application_define中创建这两个任务。

5.1. 编写示例代码
#include <stdio.h>
#include "tx_api.h"
#include "main.h"

#define THREAD1_PRIO         3
#define THREAD1_STACK_SIZE   1024
static  TX_THREAD thread1;
uint8_t thread1_stack[THREAD1_STACK_SIZE];

#define THREAD2_PRIO         2
#define THREAD2_STACK_SIZE   1024
static  TX_THREAD thread2;
uint8_t thread2_stack[THREAD2_STACK_SIZE];

void my_thread1_entry(ULONG thread_input)
{
  /* Enter into a forever loop. */
  while(1)
  {
    printf("threadx 1 application running...\r\n");
    /* Sleep for 1000 tick. */
    tx_thread_sleep(1000);
  }
}

void my_thread2_entry(ULONG thread_input)
{
  /* Enter into a forever loop. */
  while(1)
  {
    printf("threadx 2 application running...\r\n");
    /* Sleep for 1000 tick. */
    tx_thread_sleep(1000);
  }
}

void tx_application_define(void *first_unused_memory)
{
  /* Create thread */
  tx_thread_create(&thread1, "thread 1", my_thread1_entry, 0, &thread1_stack[0], THREAD1_STACK_SIZE, THREAD1_PRIO, THREAD1_PRIO, TX_NO_TIME_SLICE, TX_AUTO_START);
    
  tx_thread_create(&thread2, "thread 2", my_thread2_entry, 0, &thread2_stack[0], THREAD2_STACK_SIZE, THREAD2_PRIO, THREAD2_PRIO, TX_NO_TIME_SLICE, TX_AUTO_START);
}


1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
5.2. 启动内核
在main.c中包含threadx头文件：

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include <stdio.h>
#include "tx_api.h"
/* USER CODE END Includes */
1
2
3
4
5
然后在main函数中初始化部分之后启动内核：

/* USER CODE BEGIN 2 */

printf("threadX RTOS on BearPi IoT Board\r\n");

/* Enter the ThreadX kernel. */
tx_kernel_enter( );

/* USER CODE END 2 */
1
2
3
4
5
6
7
8
编译，下载，在串口终端查看结果：

赶快玩起来吧~

6. 内核配置文件
6.1. 开启宏定义
threadX内核中很多功能都是可以用宏定义去配置的，如果用户定义了TX_INCLUDE_USER_DEFINE_FILE宏定义，则threadx会首先包含用户配置文件tx_user.h作为内核配置文件，代码如下。

所以，我们需要在 MDK 工程中定义该宏：


6.2. 添加tx_user.h文件
threadx官方默认提供了tx_user_sample.h文件，在common/inc目录中，复制出来一份改名为tx_user.h，作为本工程的配置文件：

为了方便随时修改配置文件，在MDK中创建 threadX/config 分组，添加tx_user.h文件：


6.3. 配置项检查
threadx提供的配置项检查分为两个方面：

① 在用户不使用自定义配置文件tx_user.h时，在tx_port.h中提供默认配置，使系统依然可以正常运行；



② 在用户使用自定义配置文件tx_user.h时，在tx_api.h文件的最后对关键配置项进行安全检查，使用TX_SAFETY_CRITICAL宏定义开启，如下。


有了编译项检查的支持，我们可以放心大胆的修改自己的内核配置文件，本文中我在用户配置文件中开启关键参数安全检查和一些系统基本参数（参考port.h）：

#define TX_MAX_PRIORITIES                       32
#define TX_MINIMUM_STACK                        200
#define TX_THREAD_USER_EXTENSION
#define TX_TIMER_THREAD_STACK_SIZE              1024
#define TX_TIMER_THREAD_PRIORITY                0

/* Enable safety critical configuration and exception handling. */
#define TX_SAFETY_CRITICAL
1
2
3
4
5
6
7
8


接收更多精彩文章及资源推送，欢迎订阅我的微信公众号：『mculover666』。
————————————————
版权声明：本文为CSDN博主「Mculover666」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Mculover666/article/details/106607238