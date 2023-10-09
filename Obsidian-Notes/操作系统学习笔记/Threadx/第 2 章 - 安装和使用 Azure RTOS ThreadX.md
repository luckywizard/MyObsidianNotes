# 第 2 章 - 安装和使用 Azure RTOS ThreadX

-   项目
-   2022/04/02
-   4 个参与者

本章旨在介绍与安装、设置和使用高性能 Azure RTOS ThreadX 内核相关的各种问题。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#host-considerations)主机注意事项

嵌入式软件通常是在 Windows 或 Linux (Unix) 主机计算机上开发的。 在对应用程序进行编译和链接并将其放置在主机上之后，将应用程序下载到目标硬件，以执行它。

通常，从开发工具调试器内完成目标下载。 在下载完成后，调试器负责提供目标执行控制（“执行”、“暂停”、“断点”等） 以及对内存和处理器寄存器的访问。

大多数开发工具调试器通过 JTAG (IEEE 1149.1) 和后台调试模式 (BDM) 等芯片调试 (OCD) 连接与目标硬件进行通信。 调试器还通过线路内仿真 (ICE) 连接与目标硬件进行通信。 OCD 和 ICE 连接提供可靠的解决方案，使对目标常驻软件的入侵最少。

对于主机上使用的资源，ThreadX 的源代码以 ASCII 格式提供，并需要大约 1 MB 的主计算机硬盘空间。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#target-considerations)目标注意事项

ThreadX 要求目标具有 2 KB 和 20 KB 只读内存 (ROM)。 对于 ThreadX 系统堆栈和其他全局数据结构，它还需要 1 到 2KB 的目标的随机访问内存 (RAM)。

对于与计时器相关的函数（如服务调用超时、时间切片和要运行的应用程序计时器），基础目标硬件必须提供定期中断源。 如果处理器具有此功能，则 ThreadX 会使用它。 否则，如果目标处理器无法生成定期中断，则用户的硬件必须提供此功能。 计时器中断的设置和配置通常位于 ThreadX 分发的 tx_initialize_low_level 程序集文件中。

 备注

_即使没有可用的定期计时器中断源，ThreadX 仍可正常运行。 但是，与计时器相关的服务都无法正常运行。_

在函数 _tx_initialize_low_level 中，第一个可用 RAM 地址保存在全局变量 _tx_initialize_unused_memory 中。 此地址稍后会传递到 tx_application_define（请参阅 /chapter3.md#application-definition-function）。 还可以在 _tx_initialize_low_level 中配置异常向量表和中断优先级。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#product-distribution)产品分发

可以从我们的公共源代码存储库获取 Azure RTOS ThreadX，网址为：[https://github.com/azure-rtos/threadx/](https://github.com/azure-rtos/threadx/)。

下面列出了该存储库中的几个重要文件。

文件名

描述

tx_api.h

C 头文件，包含所有系统等式、数据结构和服务原型。

tx_port.h

C 头文件包含所有开发工具及目标特定的数据定义和结构。

demo_threadx.c

C 文件包含小型演示应用程序。

tx.a（或 tx.lib）

随标准包一起分发的 ThreadX C 库的二进制版本。

 备注

_所有文件名均为小写。 通过此命名约定可以更轻松地将命令转换为 Linux (Unix) 开发平台的命令。_

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#threadx-installation)ThreadX 安装

可以通过将 GitHub 存储库克隆到本地计算机来安装 ThreadX。 下面是用于在 PC 上创建 ThreadX 存储库的克隆的典型语法。

shell复制

```
    git clone https://github.com/azure-rtos/threadx
```

或者，也可以使用 GitHub 主页上的“下载”按钮来下载存储库的副本。

你还可以在联机存储库的首页上找到有关生成 ThreadX 库的说明。

 备注

_应用程序软件需要访问 ThreadX 库文件（通常为 tx.a 或 tx.lib）和 C 包含文件 tx_api.h 和 tx_port.h。 为实现此目的，可以设置开发工具的相应路径，或者将这些文件复制到应用程序开发区域。_

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#using-threadx)使用 ThreadX

若要使用 ThreadX，应用程序代码必须在编译期间包含 tx_api.h，并与 ThreadX 运行时库 tx.a（或 tx.lib）链接。

生成 ThreadX 应用程序需要四个步骤。

1.  在所有使用 ThreadX 服务或数据结构的应用程序文件中包含 tx_api.h 文件。
    
2.  创建标准 C main 函数。 此函数必须最终调用 tx_kernel_enter 才能启动 ThreadX。 在输入内核之前，可能会添加不涉及 ThreadX 的应用程序特定的初始化。
    
     重要
    
    _ThreadX entry 函数 tx_kernel_enter 不返回。 因此，请确保在其之后不进行任何处理或函数调用。_
    
3.  创建 tx_application_define 函数。 这是创建初始系统资源的位置。 系统资源的示例包括线程、队列、内存池、事件标志组、互斥体和信号灯。
    
4.  编译应用程序源并与 ThreadX 运行时库 tx.lib 链接。 生成的图像可下载到目标并执行！
    

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#small-example-system)小型示例系统

图 1 中的小型示例系统显示了优先级为 3 的单个线程的创建。 线程执行，递增计数器，然后休眠一个时钟周期。 此过程会永远继续下去。

C复制

```
#include "tx_api.h"
unsigned long my_thread_counter = 0;
TX_THREAD my_thread;
main( )
{
    /* Enter the ThreadX kernel. */
    tx_kernel_enter( );
}
void tx_application_define(void *first_unused_memory)
{
    /* Create my_thread! */
    tx_thread_create(&my_thread, "My Thread",
    my_thread_entry, 0x1234, first_unused_memory, 1024,
    3, 3, TX_NO_TIME_SLICE, TX_AUTO_START);
}
void my_thread_entry(ULONG thread_input)
{
    /* Enter into a forever loop. */
    while(1)
    {
        /* Increment thread counter. */
        my_thread_counter++;
        /* Sleep for 1 tick. */
        tx_thread_sleep(1);
    }
}
```

**图 1. 应用程序开发模板**

尽管这是一个简单的示例，但它为真正的应用程序开发提供了一个很好的模板。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#troubleshooting)疑难解答

每个 ThreadX 端口都随演示应用程序一起提供。 首先运行演示系统，无论是在实际的目标硬件上，还是在模拟环境中，这始终是个不错的主意。

如果演示系统未正确执行，以下是一些故障排除提示。

1.  确定演示的运行量。
2.  增加堆栈大小（这在实际的应用程序代码中比在演示中更为重要）。
3.  重新生成 ThreadX 库，其中定义了 TX_ENABLE_STACK_CHECKING。 这将启用内置的 ThreadX 堆栈检查。
4.  暂时跳过最近所做的任何更改，以查看问题是否消失或发生更改。 此类信息对于支持工程师非常有用。

按照[客户支持中心](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/about-this-guide#customer-support-center)中概述的步骤，发送从故障排除步骤中收集的信息。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#configuration-options)配置选项

使用 ThreadX 生成 ThreadX 库和应用程序时，有几个配置选项。 可以在应用程序源、命令行或 tx_user.h include 文件中定义以下选项。

 重要

只有当应用程序和 ThreadX 库在构建时定义了 TX_INCLUDE_USER_DEFINE_FILE，才会应用在 tx_user.h 中定义的选项。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#smallest-configuration)最小配置

对于最小的代码大小，应考虑以下 ThreadX 配置选项（缺少所有其他选项）。

C复制

```
TX_DISABLE_ERROR_CHECKING
TX_DISABLE_PREEMPTION_THRESHOLD
TX_DISABLE_NOTIFY_CALLBACKS
TX_DISABLE_REDUNDANT_CLEARING
TX_DISABLE_STACK_FILLING
TX_NOT_INTERRUPTABLE
TX_TIMER_PROCESS_IN_ISR
```

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#fastest-configuration)最快配置

为实现最快的执行，在以前的最小配置中使用相同的配置选项，但也将这些选项考虑在内。

C复制

```
TX_REACTIVATE_INLINE
TX_INLINE_THREAD_RESUME_SUSPEND
```

介绍了[详细的配置选项](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#detailed-configuration-options)。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#global-time-source)全局时间源

对于其他 Microsoft Azure RTOS 产品（FileX、NetX、GUIX、USBX 等），ThreadX 定义表示一秒的 ThreadX 计时器时钟周期数。 其他产品基于此常量派生其时间要求。 默认情况下，该值为 100（假设 10ms 定期中断）。 用户可以通过在 tx_port.h 或在 IDE 或命令行中以所需值定义 TX_TIMER_TICKS_PER_SECOND 来覆盖此值。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#detailed-configuration-options)详细的配置选项

TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO

如果定义了此选项，则可以在字节池上收集性能信息。 默认情况下，未定义此选项。

TX_BYTE_POOL_ENABLE_PERFORMANCE_INFO

如果定义了此选项，则可以在字节池上收集性能信息。 默认情况下，未定义此选项。

TX_DISABLE_ERROR_CHECKING

跳过基本服务调用错误检查。 在应用程序源中定义时，将禁用所有基本参数错误检查。 这可能会将性能提高多达 30%，还可能会减小图像大小。

 备注

_仅当应用程序可以绝对保证所有输入参数（包括从外部输入派生的输入参数）在所有情况下都始终有效时，才可以安全地禁用错误检查。 如果在禁用错误检查的情况下向 API 提供无效输入，则因此而发生的行为是未定义的，并且可能会导致内存损坏或系统崩溃。_

 备注

_不受禁用错误检查影响的 ThreadX API 返回值在第 4 章的每个 API 说明的“返回值”部分中以粗体列出。 如果通过使用 TX_DISABLE_ERROR_CHECKING 选项禁用了错误检查，则非加粗返回值失效。_

TX_DISABLE_NOTIFY_CALLBACKS

定义后，将对各种 ThreadX 对象禁用通知回调。 使用此选项可以略微减少代码大小并提高性能。 默认情况下，未定义此选项。

TX_DISABLE_PREEMPTION_THRESHOLD

定义后，将禁用抢占阈值功能，并略微减少代码大小并提高性能。 当然，抢占阈值功能不再可用。 默认情况下，未定义此选项。

TX_DISABLE_REDUNDANT_CLEARING

定义后，删除用于将 ThreadX 全局 C 数据结构初始化为零的逻辑。 仅当编译器的初始化代码将所有未初始化的 C 全局数据设置为零时，才应使用此选项。 在初始化期间，使用此选项可以略微减少代码大小并提高性能。 默认情况下，未定义此选项。

TX_DISABLE_STACK_FILLING

定义后，禁止在创建时将 0xEF 值置于每个线程的堆栈的每个字节中。 默认情况下，未定义此选项。

TX_ENABLE_EVENT_TRACE

定义后，ThreadX 启用事件收集代码，用于创建 TraceX 跟踪缓冲区。

TX_ENABLE_STACK_CHECKING

定义后，将启用 ThreadX 运行时堆栈检查，其中包括分析已使用的堆栈量，以及堆栈区域前后的数据模式“防护”检查。 如果检测到堆栈错误，则会调用已注册应用程序堆栈错误处理程序。 此选项会导致系统开销和代码大小略有增加。 有关详细信息，请查看 tx_thread_stack_error_notify API 函数。 默认情况下，未定义此选项。

TX_EVENT_FLAGS_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关事件标志组的性能信息。 默认情况下，未定义此选项。

TX_INLINE_THREAD_RESUME_SUSPEND

定义后，ThreadX 通过行内代码改进 tx_thread_resume 和 tx_thread_suspend API 调用。 这会增加代码大小，但会增强这两个 API 调用的性能。

TX_MAX_PRIORITIES

定义 ThreadX 的优先级别。 合法值的范围为 32 到 1024（含），且必须能被 32 整除。 增加支持的优先级别数量会使每组 32 个优先级别的 RAM 用量增加 128 字节。 但是，对性能的影响可忽略不计。 默认情况下，此值设置为 32 个优先级别。

TX_MINIMUM_STACK

定义最小堆栈大小（以字节为单位）。 它用于在创建线程时进行错误检查。 默认值是端口特定的，位于 tx_port.h 中。

TX_MISRA_ENABLE

定义后，ThreadX 将使用 MISRA C 兼容约定。 有关详细信息，请参阅 [ThreadX_MISRA_Compliance](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/appendix-e)。

TX_MUTEX_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关互斥体的性能信息。 默认情况下，未定义此选项。

TX_NO_TIMER

定义后，ThreadX 计时器逻辑被完全禁用。 这在无法使用 ThreadX 计时器功能（线程睡眠、API 超时、时间切片和应用程序计时器）的情况下十分有用。 如果指定 TX_NO_TIMER，还必须定义选项 TX_TIMER_PROCESS_IN_ISR。

TX_NOT_INTERRUPTABLE

定义后，ThreadX 不会尝试最大程度地缩短中断锁定时间。 这会提升执行速度，但会略微增加中断锁定时间。

TX_QUEUE_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关队列的性能信息。 默认情况下，未定义此选项。

TX_REACTIVATE_INLINE

定义后，执行 ThreadX 计时器内联的激活，而不是使用函数调用。 这可以提升性能，但会略微增加代码大小。 默认情况下，未定义此选项。

TX_SEMAPHORE_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关信号灯的性能信息。 默认情况下，未定义此选项。

TX_THREAD_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关线程的性能信息。 默认情况下，未定义此选项。

TX_TIMER_ENABLE_PERFORMANCE_INFO

定义后，可以收集有关计时器的性能信息。 默认情况下，未定义此选项。

TX_TIMER_PROCESS_IN_ISR

定义后，将消除 ThreadX 的内部系统计时器线程。 这会提升计时器事件和更小 RAM 要求的性能，因为不再需要计时器堆栈和控制块。 但是，使用此选项会将所有计时器过期处理移动到计时器 ISR 级别。 默认情况下，未定义此选项。

 备注

计时器允许的服务可能得不到 ISR 的允许，因此，在使用此选项时可能不允许这样做。

TX_TIMER_THREAD_PRIORITY

定义内部 ThreadX 系统计时器线程的优先级。 默认值为优先级 0 - ThreadX 中的最高优先级。 默认值在 tx_port.h 中定义。

TX_TIMER_THREAD_STACK_SIZE

定义内部 ThreadX 系统计时器线程的堆栈大小（以字节为单位）。 此线程处理所有线程睡眠请求以及所有服务调用超时。 此外，从该上下文调用所有应用程序计时器回调例程。 默认值是端口特定的，位于 tx_port.h 中。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter2#threadx-version-id)ThreadX 版本 ID

程序员可以通过检查 tx_port.h 文件来获得 ThreadX 版本。 此外，该文件还包含相应端口的版本历史记录。 应用程序软件可以通过检查全局字符串 _tx_version_id 来获取 ThreadX 版本。