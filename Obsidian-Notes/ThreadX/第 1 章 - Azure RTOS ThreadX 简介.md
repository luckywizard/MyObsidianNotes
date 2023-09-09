# 第 1 章 - Azure RTOS ThreadX 简介

Azure RTOS ThreadX 是专门为嵌入式应用程序设计的高性能实时内核。 本章提供了该产品的简介，并说明了其应用和优势。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#threadx-unique-features)ThreadX 的独特功能

与其他实时内核不同，ThreadX 功能多样。通过使用强大的 CISC、RISC 和 DSP 处理器的应用程序，可以轻松地在基于小型微控制器的应用程序之间扩展。

ThreadX 可基于其基础体系结构进行扩展。 因为 ThreadX 服务是作为 C 库实现的，所以只有应用程序实际使用的那些服务被引入了运行时映像。 因此，ThreadX 的实际大小完全由应用程序决定。 对于大多数应用程序，ThreadX 的指令映像的大小在 2 KB 至 15 KB 之间。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#picokernel-architecture)picokernel™ 体系结构

ThreadX 服务没有像传统的微内核体系结构那样将内核函数相互层叠，而是直接将其插入核心。 由此产生了最快的上下文切换和服务呼叫性能。 我们将此非分层设计称为 picokernel 体系结构。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#ansi-c-source-code)ANSI C 源代码

ThreadX 主要是在 ANSI C 中编写的。用户需要少量的汇编语言来定制内核，从而满足基础目标处理器的需求。 此设计使用户可以在很短的时间内（通常在几周内）将 ThreadX 移植到新的处理器系列！

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#advanced-technology)高级技术

下面是 ThreadX 高级技术的亮点。

-   简单的 picokernel 体系结构
-   自动扩展（占用空间少）
-   确定性处理
-   快速实时性能
-   抢先式和协作式计划
-   灵活的线程优先级支持
-   动态系统对象创建
-   无限量的系统对象
-   经过优化的中断处理
-   抢占阈值 (Preemption-threshold™)
-   优先级继承
-   事件链接 (Event-chaining™)
-   快速软件计时器
-   运行时内存管理
-   运行时性能监视
-   运行时堆栈分析
-   内置系统跟踪
-   广泛的处理器支持
-   广泛的开发工具支持
-   字节顺序完全中性

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#not-a-black-box)不是黑盒

ThreadX 的大多数发行版都包含完整的 C 源代码以及特定于处理器的汇编语言。 这消除了许多商业内核所出现的“黑盒”问题。 借助 ThreadX，应用程序开发人员可以看到内核正在进行的确切操作。没有任何秘密可言！

源代码还允许进行特定于应用程序的修改。 尽管不建议这么做，但如果真的需要，具备修改内核的能力当然是有益的。

对于习惯使用自己的内部内核的开发人员而言，这些功能尤其令人欣慰。 他们期望拥有源代码和修改内核的能力。 ThreadX 是适用于这类开发人员的终极内核。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#the-rtos-standard)RTOS 标准

由于 ThreadX 的多功能性、高性能的 picokernel 体系结构、先进的技术以及经证实的可移植性，目前已部署 ThreadX 的设备超过了 20 亿。 这实际上使 ThreadX 成为深度嵌入式应用程序的 RTOS 标准。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#safety-certifications)安全认证

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#t%C3%BCv-certification)TÜV 认证

ThreadX 已被 SGS-TÜV Saar 认证可用于安全关键型系统，并且符合 IEC61508 和 IEC-62304 标准。 该认证证明：ThreadX 可用于开发达到国际电工委员会 (IEC) 61508 和 IEC 62304 最高安全完整性等级的安全相关软件，这些安全完整性级别旨在确保“电气设备、电子设备和可编程的安全相关电子系统的功能安全”。SGS-TÜV Saar 由德国的 SGSGroup 和 TÜV Saarland 合并而成，现已成为领先的经过资格验证的独立公司，专门为全球的安全相关系统测试、审核、验证和认证嵌入式软件。 工业安全标准 IEC 61508 以及从其派生的所有标准（包括 IEC 62304）用于确保电气设备、电子设备和可编程的安全相关电子医疗设备、流程控制系统、工业机械和铁路控制系统的功能安全。

SGS-TÜV Saar 已根据 ISO 26262 标准对 ThreadX 进行了认证，确定其可用于安全关键型汽车系统。 此外，ThreadX 还获得了汽车安全完整性等级 (ASIL) D 的认证，该等级代表了 ISO 26262 认证的最高等级。

此外，SGS-TÜV Saar 已对 ThreadX 进行了认证，确定其可用于安全关键型铁路系统，符合 EN 50128 标准并达到 SW-SIL 4 等级。

![TÜV Certification](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/media/overview-threadx/partener-logo-sgs-tuv-saar-2.png)

-   IEC 61508，达到 SIL 4 等级
    
-   IEC 62304，SW 安全类别为 C 类
    
-   ISO 26262 ASIL D
    
-   EN 50128 SW-SIL 4
    

 备注

请联系我们，了解 ThreadX 的哪些版本已通过 TÜV 认证，或者了解如何获取测试报表、证书和相关文档。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#misra-c-compliant)符合 MISRA C

MISRA C 是一组编程准则，面向使用 C 编程语言的关键系统。 最初的 MISRA C 准则主要面向汽车业应用；但是，现在人们广泛认可 MISRA C 适用于任何安全关键应用。 ThreadX 符合 MISRA-C:2004 和 MISRA C:2012 的所有“必需”规则和“强制性”规则。 ThreadX 还符合除三个“公告”规则之外的所有规则。 有关更多详细信息，请参阅 ThreadX_MISRA_Compliance.pdf 文档。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#ul-certification)UL 认证

ThreadX 已通过 UL 的认证，符合面向可编程软件组件的 UL 60730-1 Annex H、CSA E60730-1 Annex H、IEC 60730-1 Annex H、UL 60335-1 Annex R、IEC 60335-1 Annex R 和 UL 1998 安全标准。 连同 IEC/UL 60730-1（其附件 H 中对“使用软件进行控制”的要求）一起，IEC 60335-1 标准在其附件 R 中描述了“可编程电子电路”的要求。IEC 60730 附件 H 和 IEC 60335 -1 附件 R 阐述了在洗衣机、洗碗机、烘干机、冰箱、冰柜和烤箱等电器中使用的 MCU 硬件和软件的安全性。

![UL Certification](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/media/overview-threadx/partener-logo-c-ru-us-2.png)

UL/IEC 60730、UL/IEC 60335、UL 1998

 备注

请联系 Microsoft，了解 ThreadX 的哪些版本已通过 TÜV 认证，或者了解如何获取测试报表、证书和相关文档。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#certification-pack)认证包

ThreadX Certification Pack™ 是100% 完整、统包式、行业特定的独立包，提供所有必要的 ThreadX 证据，以认证或成功申报基于 ThreadX 的产品，致力于达到安全关键型航空、医疗和工业系统所需的最高可靠性和关键性等级。 支持的认证包括 DO-178B、ED-12B、DO-278、FDA510(k)、IEC62304、IEC-60601、ISO-14971、UL-1998、IEC-61508、CENELEC EN50128、BS50128 和 49CFR236。 有关认证包的更多信息，请联系 Microsoft。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#embedded-applications)嵌入式应用程序

嵌入式应用程序在诸如无线通信设备、汽车引擎、激光打印机、医疗器械等产品内置的微处理器上执行。嵌入式应用程序的另一个区别在于它们的软件和硬件有着特定的用途。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#real-time-software)实时软件

当对应用软件施加时间限制时，它被称为实时软件。 由于嵌入式应用程序与外部事件的固有交互，因此几乎总是实时的。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#multitasking)多任务

如前所述，嵌入式应用程序有着特定的用途。 为了实现此目的，软件必须执行各种任务。 任务是执行特定职责的应用程序的半独立部分。 同样，事实上某些任务比其他任务更重要。 嵌入式应用程序的主要难题之一是在各种应用程序任务之间分配处理器。 在竞争任务之间分配处理器是 ThreadX 的主要目的。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#tasks-vs-threads)任务与线程

关于任务的另一个区别在于，“任务”这个术语是以多种方式使用的。 有时它意味着可单独加载的程序。 在其他情况下，它可以指内部程序段。 因此，在现代操作系统中，有两个术语或多或少地替代了“任务”：“进程”和“线程”。 “进程”是具有自己的地址空间的完全独立的程序，而“线程”是在进程内执行的半独立程序段。 线程共享相同的进程地址空间。 与线程管理相关的开销是最小的。

大多数嵌入式应用程序负担不起与面向进程的成熟操作系统相关的开销（内存和性能）。 此外，较小的微处理器并没有支持真正面向进程的操作系统的硬件体系结构。 出于这些原因，ThreadX 实现了一个线程模型，对于大多数实时嵌入式应用程序来说，该模型非常高效实用。

为避免混淆，ThreadX 不使用“任务”这个术语。 取而代之的是，使用更具描述性和现代性的名称“线程”。

## [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#threadx-benefits)ThreadX 的好处

使用 ThreadX 为嵌入式应用程序带来了许多好处。 当然，主要好处在于如何为嵌入式应用程序线程分配处理时间。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#improved-responsiveness)更高的响应能力

在出现像 ThreadX 这样的实时内核之前，大多数嵌入式应用程序都使用简单的控制循环（通常来自 C main 函数内部）来分配处理时间。 在非常小或简单的应用程序中，这种方法仍在使用。 但是，在大型或复杂的应用程序中，这是不切实际的，因为对任何事件的响应时间是一个函数，是一次通过控制循环的传递的最差处理时间的函数。

更糟糕的是，每当对控制循环进行修改时，应用程序的时序特性都会发生变化。 这使应用程序本身就不稳定，难以维护和改进。

ThreadX 提供对重要外部事件的快速确定性响应时间。 ThreadX 通过其基于优先级的抢先式计划算法来实现这一点，该算法允许优先级较高的线程抢先于正在执行的优先级较低的线程。 因此，最差的响应时间接近执行上下文切换所需的时间。 这不仅是确定性的，而且还是非常快速的。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#software-maintenance)软件维护

ThreadX 内核使应用程序开发人员能够专注于其应用程序线程的特定要求，而无需担心更改应用程序其他区域的计时。 此功能还简化了使用 ThreadX 的应用程序的修复或增强。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#increased-throughput)更高的吞吐量

解决控制循环响应时间问题的一种方法可以是添加更多轮询。 这样可以提高响应能力，但仍不能保证最差响应时间保持不变，而且也不利于推动应用程序的未来修改。 而且，由于额外的轮询，处理器现在正在执行更多不必要的处理。 所有这些不必要的处理都会降低系统的总体吞吐量。

关于开销，有趣的一点是，许多开发人员都认为多线程环境（如 ThreadX）会增加开销，并对总系统吞吐量产生负面影响。 但是在某些情况下，多线程实际上通过消除在控制循环环境中发生的所有冗余轮询减少了开销。 与多线程内核相关的开销通常是上下文切换所需时间的函数。 如果上下文切换时间少于轮询过程，则 ThreadX 提供的解决方案可能会减少开销并提高吞吐量。 无论应用程序的复杂性和大小如何，这都使 ThreadX 成为明智之选。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#processor-isolation)处理器隔离

ThreadX 在应用程序与基础处理器之间提供可靠的独立于处理器的接口。 这使开发人员能够专注于应用程序，而不是花费大量时间研究硬件详细信息。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#dividing-the-application)划分应用程序

在基于控件循环的应用程序中，每个开发人员都必须对整个应用程序的运行时行为和要求有着深入的了解。 这是因为处理器分配逻辑分散在整个应用程序中。 随着应用程序的大小或复杂性的增加，所有开发人员都无法记住整个应用程序的精确处理要求。

ThreadX 让每个开发人员摆脱了与处理器分配相关的烦恼，并允许他们专注于嵌入式应用程序的特定部分。 此外，ThreadX 强制将应用程序划分为明确定义的线程。 将应用程序划分为多个线程本身可使开发变得更简单。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#ease-of-use)易用性

ThreadX 在设计时考虑到了应用程序开发人员。 ThreadX 体系结构和服务调用接口被设计为易于理解。 因此，ThreadX 开发人员可以快速使用其高级功能。

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#improve-time-to-market)缩短上市时间

ThreadX 的这一切优点都加速了软件开发过程。 ThreadX 负责处理大多数处理器问题和最常见的安全认证，从而从开发计划中省去了这些工作。 所有这些都使上市时间缩短！

### [](https://docs.microsoft.com/zh-cn/azure/rtos/threadx/chapter1#protecting-the-software-investment)保护软件投资

由于其体系结构，ThreadX 可轻松移植到新的处理器和/或开发工具环境。 基于这一特性，再加上 ThreadX 可以将应用程序与基础处理器的详细信息隔离的事实，从而使 ThreadX 应用程序变得高度可移植。 最终保证了应用程序的迁移路径，并保护了原始开发投资。