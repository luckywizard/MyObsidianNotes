# Azure RTOS ThreadX 概述

Azure RTOS ThreadX 是 Microsoft 提供的高级工业级实时操作系统 (RTOS)。 它是专门为深度嵌入式实时 IoT 应用程序设计的。 Azure RTOS ThreadX 提供高级计划、通信、同步、计时器、内存管理和中断管理功能。 此外，Azure RTOS ThreadX 具有许多高级功能，包括 picokernel™ 体系结构、preemption-threshold™ 计划、event-chaining™、执行分析、性能指标和系统事件跟踪。 Azure RTOS ThreadX 非常易于使用，适用于要求极其苛刻的嵌入式应用程序。 Azure RTOS ThreadX 在各种产品（包括消费者设备、医疗电子设备和工业控制设备）上的部署次数已达数十亿次。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#threadx-footprint)ThreadX 占用情况

Azure RTOS ThreadX 的占用空间非常小，最少只需要一个 2KB 的指令区域和 1 KB 的 RAM。 这种大小在很大程度上归功于其非分层 picokernel 体系结构和自动缩放。 自动缩放是指在链接时仅将应用程序使用的服务（和支持基础结构）包括到最终映像中。

下面是 Azure RTOS ThreadX 的一些典型大小特征。

Azure RTOS ThreadX 服务

典型大小（以字节为单位）

核心服务（必需）

2,000

队列服务

900

事件标志服务

900

信号灯服务

450

互斥锁服务

1,200

块内存服务

550

字节内存服务

900

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#threadx-execution-speed)ThreadX 执行速度

Azure RTOS ThreadX 可在大多数主流处理器上实现亚毫秒级上下文切换，并且总体速度比其他商业 RTOS 都快。 除了快速，Azure RTOS ThreadX 还具有高度确定性。 无论准备就绪的线程有 200 个还是只有一个，它都能实现同样的高性能。

下面是 Azure RTOS ThreadX 的一些典型性能特征：

-   快速启动：Azure RTOS ThreadX 可在 120 个周期内启动。
    
-   禁用基本错误检查（可选）：编译时可以跳过基本的 Azure RTOS ThreadX 错误检查。 当应用程序代码已通过验证，且不再需要对每个参数进行错误检查时，这很有用。 可在编译单元上（而不是在系统范围内）跳过错误检查。
    
-   Picokernel 设计：服务不彼此叠加，从而消除了不必要的函数调用开销。
    
-   优化中断处理：除非需要抢占，否则只有在进入/退出 ISR 时才会保存/还原暂存寄存器。
    
-   优化 API 处理：
    
    Azure RTOS ThreadX 服务
    
    服务时间以微秒为单位*
    
    暂停线程
    
    0.6
    
    继续线程
    
    0.6
    
    发送队列
    
    0.3
    
    接收队列
    
    0.3
    
    获取信号灯
    
    0.2
    
    放置信号灯
    
    0.2
    
    上下文切换
    
    0.4
    
    中断响应
    
    0.0-0.6
    
    *性能指标基于运行频率为 200MHz 的典型处理器。
    

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#advanced-technology)高级技术

Azure RTO ThreadX 最突出之处是它的 Preemption-Threshold 计划。 此功能是 Azure RTOS ThreadX 独有的，并已成为广泛的学术研究课题。 如需深入了解，请参阅由康考迪亚大学的 Yun Wang 与匹兹堡大学的 Manas Saksena 联合发表的《[Scheduling Fixed-Priority Tasks with Preemption Threshold](https://ieeexplore.ieee.org/document/811269)》。

Azure RTOS ThreadX 的主要功能：

-   完整全面的多任务处理功能
    -   线程、应用程序计时器、消息队列、计数信号灯、互斥锁、事件标志、块内存池和字节内存池
-   基于优先级的抢占式计划
-   优先级灵活性 - 最多可定义 1024 个优先级
-   协作式计划
-   Preemption-Threshold - Azure RTOS ThreadX 的独有功能，有助于减少上下文切换并帮助确保可计划性（根据学术研究）
-   通过 Azure RTOS ThreadX MODULES 进行内存保护
-   完全确定性
-   事件跟踪 - 捕获最后 n 个系统事件/应用程序事件
-   Event Chaining - 为每个 Azure RTOS ThreadX 通信或同步对象注册特定于应用程序的“通知”回调函数
-   具有可选内存保护的 Azure RTOS ThreadX MODULES
-   运行时性能指标
    -   线程恢复数
    -   线程暂停数
    -   请求的线程抢占数
    -   异步线程中断抢占数
    -   线程优先级反转数
    -   线程放弃次数
-   Execution Profile Kit (EPK)
-   单独中断堆栈
-   运行时堆栈分析
-   优化计时器中断处理

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#multicore-support-amp--smp)多核支持（AMP 和 SMP）

标准 Azure RTOS ThreadX 通常以非对称多重处理 (AMP) 方式使用，在这种情况下，Azure RTOS ThreadX 的单独副本和应用程序（或 Linux）在每个核心上执行，并通过共享内存或处理器间通信机制（例如 Azure RTOS ThreadX 所支持的 OpenAMP）相互通信。

在高度动态加载处理器的环境中，Azure RTOS ThreadX 对称多重处理 (SMP) 可用于以下处理器系列：

-   ARM Cortex-Ax
-   ARM Cortex-Rx
-   ARM Cortex-A5x（64 位）
-   MIPS 34 K、1004 K 和 interAptiv
-   PowerPC
-   Synopsys ARC HS
-   x86

Azure RTOS ThreadX SMP 跨 n 个处理器执行动态负载均衡。 它允许任何核心上的任何线程访问所有 Azure RTOS ThreadX 资源（队列、信号灯、事件标志和内存池等）。 Azure RTOS ThreadX SMP 在所有核心上启用全部 Azure RTOS ThreadX API，并引入了以下适用于 SMP 操作的新 API：

-   `UINT tx_thread_smp_core_exclude(TX_THREAD *thread_ptr, ULONG exclusion_map);`
-   `UINT tx_thread_smp_core_exclude_get(TX_THREAD *thread_ptr, ULONG *exclusion_map_ptr);`
-   `UINT tx_thread_smp_core_get(void);`
-   `UINT tx_timer_smp_core_exclude(TX_TIMER *timer_ptr, ULONG exclusion_map);`
-   `UINT tx_timer_smp_core_exclude_get(TX_TIMER *timer_ptr, ULONG *exclusion_map_ptr);`

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#memory-protection-via-azure-rtos-threadx-modules)通过 Azure RTOS ThreadX MODULES 进行内存保护

使用称为 Azure RTOS ThreadX Modules 的附加产品可将一个或多个应用程序线程捆绑成一个“模块”，该模块可动态加载并在目标上运行（或就地执行）。

使用这些模块可进行现场升级、缺陷修复和程序分区，从而使大型应用程序仅占用活动线程所需的内存。

这些模块还具有独立于 Azure RTOS ThreadX 的地址空间。 这样，Azure RTOS ThreadX 就可以通过 MPU 或 MMU 对模块进行内存保护，从而阻止模块外部的意外访问损坏任何其他软件组件。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#misra-compliant)符合 MISRA

Azure RTOS ThreadX 和 Azure RTOS ThreadX SMP 的源代码符合 MISRA-C:2004 以及 MISRA C:2012。 MISRA C 是一组编程准则，面向使用 C 编程语言的关键系统。 最初的 MISRA C 准则主要面向汽车业应用；但是，现在人们广泛认可 MISRA C 适用于任何安全关键应用。 Azure RTOS ThreadX 符合 MISRA-C:2004 和 MISRA C:2012 的所有必需规则和强制性规则。

![Misra certification](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/media/overview-threadx/misra-logo-certification.png)

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#supports-most-popular-tools)支持大部分常用工具

Azure RTOS ThreadX 支持大部分常用的嵌入式开发工具，包括 IAR 的 Embedded Workbenc，该工具还提供最全面的 Azure RTOS ThreadX 内核感知功能。 其他工具集成包括 GNU (GCC)、ARM DS-5/uVision®、Green Hills MULTI®、Wind River Workbench、Imagination Codescape、Renesas e2studio、Metaware SeeCode、NXP CodeWarrior、Lauterbach TRACE32®、TI Code-Composer Studio、CrossCore 和所有模拟设备。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/overview-threadx#adaptation-layer-for-threadx)ThreadX 的适配层

可通过使用各种旧版 RTOS API（FreeRTOS、POSIX、OSEK 等）的 ThreadX [适配层](https://github.com/azure-rtos/threadx/tree/master/utility/rtos_compatibility_layers)来缓解到 Azure RTOS 的迁移问题。