# 1.	.NET体系结构



## 1.1	.NET 平台

.NET 是一个通用开发平台，支持多种编程语言。.NET实现**公共语言基础结构（CLI）**，它指定与语言无关的运行时环境和语言互操作性，即它提供了一个跨语言的统一编程环境。目前能在 .NET 平台上使用的开发语言很多，例如 Visual Basic .NET、Python、C#、Visual C++.NET 等，而C# 是一种在 .NET 开发平台上使用最多的编程语言。



### 1.1.1	跨语言互操作

**互操作性**（英文：**Interoperability**；中文又称为：**协同工作能力**，**互用性**）作为一种特性，它指的是不同的系统和组织机构之间相互合作，协同工作（即互操作）的能力。[IEEE](https://zh.wikipedia.org/wiki/IEEE)（Institute of Electrical & Electronic Engineers，电气与电子工程师协会）对互操作性做出了如下定义：

> *两个或多个系统或组成部分之间交换信息以及对所交换的信息加以使用的能力*。

**语言互操作性**是一种代码与使用其他编程语言编写的另一种代码进行交互的能力。语言互操作性可以有助于最大程度地提高代码的重复使用率，从而提高开发过程的效率。

因为开发人员使用多种工具和技术，每一种工具和技术都支持不同的功能和类型，这就形成了确保语言互操作性较为困难的历史根源。CLI定义了一个语言无关的跨体系结构的运行环境（公共语言运行库），这使得开发者可以用**规范内定义**的各种高级语言来开发软件，然后将程序编译成中间语言最后执行，实现多语言的互操作性。

公共语言运行库通过指定和强制公共类型系统以及提供元数据为语言互操作性提供了必要的基础。因为所有面向运行库的语言都遵循[通用类型系统](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/zcx1eb1e(v=vs.90))规则来定义和使用类型，类型的用法在各种语言之间是一致的。[元数据](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/xcd8txaw(v=vs.90))通过定义统一的存储和检索类型信息的机制使语言互操作性成为可能。编译器将类型信息存储为元数据，公共语言运行库使用该信息在执行过程中提供服务；因为所有类型信息都以相同的方式存储和检索，而与编写该代码的语言无关，所以运行库可以**管理多语言应用程序的执行**。



#### CLI

CLI不是某种代码库或者程序，它是一项国际性的标准，全名是公共语言基础结构（Common Language Infrastructure），它是一系列规范的总称。CLI不是特定为C#服务的，它这套标准可以应用于多种语言，开发者可以依据CLI的规范实现各种编译平台并应用于多种语言和多种操作系统中。

CLI包含的规范有：

- 虚拟执行系统（VES）
- 公共中间语言（CIL）
- 公共类型系统（Common Type System，CTS）
- 公共语言规范（Common Language Specification，CLS）
- 元数据（Metadata）
- 框架（Framework）



#### CTS

通用类型系统定义了如何在运行库中声明、使用和管理类型，同时也是运行库支持跨语言集成的一个重要组成部分。通用类型系统执行以下功能：

- 建立一个支持跨语言集成、类型安全和高性能代码执行的框架。
- 提供一个支持完整实现多种编程语言的面向对象的模型。
- 定义各语言必须遵守的规则，有助于确保用不同语言编写的对象能够交互作用。
- 提供包含应用程序开发中使用的基元数据类型（如[Boolean](https://msdn.microsoft.com/zh-cn/library/a28wyd50(v=vs.100))、[Byte](https://msdn.microsoft.com/zh-cn/library/yyb1w04y(v=vs.100))、[Char](https://msdn.microsoft.com/zh-cn/library/k493b04s(v=vs.100))、[Int32](https://msdn.microsoft.com/zh-cn/library/td2s409d(v=vs.100)) 和 [UInt64](https://msdn.microsoft.com/zh-cn/library/06cf7918(v=vs.100))）的库。



#### CLS

要和其他对象完全交互，而不管这些对象是以何种语言实现的，对象必须只向调用方公开那些它们必须与之互用的所有语言的通用功能。 为此定义了公共语言规范 (CLS)，它是许多应用程序所需的一套基本语言功能。 CLS 规则定义了[常规类型系统](https://docs.microsoft.com/zh-cn/previous-versions/dotnet/netframework-4.0/zcx1eb1e(v=vs.100))的子集，即所有适用于常规类型系统的规则都适用于 CLS，除非 CLS 中定义了更严格的规则。 CLS 通过定义一组开发人员可以确信在多种语言中都可用的功能来增强和确保语言互用性。 CLS  还建立了 CLS 遵从性要求，这帮助您确定您的托管代码是否符合 CLS 以及一个给定的工具对托管代码（该代码是使用 CLS  功能的）开发的支持程度。

如果您的组件在对其他代码（包括派生类）公开的 API 中只使用了 CLS 功能，那么可以保证在任何支持 CLS 的编程语言中都可以访问该组件。 遵守 CLS 规则、仅使用 CLS 中所包含功能的组件叫做符合 CLS 的组件。

CLS 在设计上足够大，可以包括开发人员经常需要的语言构造；同时也足够小，大多数语言都可以支持它。 此外，任何不可能快速验证代码类型安全性的语言构造都被排除在 CLS 之外，以便所有符合 CLS 的语言都可以生成可验证的代码（如果它们选择这样做）。



### 1.1.2	公共语言运行时 CLR 

**CLR 是由 Microsoft 执行的公共语言基础结构 (CLI) 的商业实现，CLI 是作为执行和开发环境（语言和库在其中无缝协作）创建依据的国际标准。**

#### 托管

交由运行时管理执行的过程称为托管，在这种情况下，相关的运行时称为公共语言运行时，不管使用的是哪种实现（[Mono](https://www.mono-project.com/)、.NET Framework 或.NET Core）。托管代码就是执行过程交由运行时管理的代码。托管代码具有许多优点，例如：跨语言集成、跨语言异常处理、增强的安全性、版本控制和部署支持、简化的组件交互模型、调试和分析服务等。CLR 负责提取托管代码，将其编译成机器代码，然后执行它。 除此之外，运行时还提供多个重要服务，例如自动内存管理、安全边界、类型安全，等等。相反，如果运行 C/C++ 程序，则运行的代码也称为“非托管代码”。 在非托管环境中，程序员需要亲自负责处理相当多的事情。 实际的程序在本质上是操作系统 (OS) 载入内存，然后启动的二进制代码。

托管执行过程包括下列步骤：

1. [选择编译器](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/cds9hbbb(v=vs.90))。

   为获得公共语言运行库提供的优点，必须使用一个或多个针对运行库的语言编译器。

2. 将代码编译为 [Microsoft 中间语言 (MSIL)](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/c5tkafs1(v=vs.90))。

   编译将源代码翻译为 MSIL 并生成所需的元数据。

3. [将 MSIL 编译为本机代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/ht8ecch6(v=vs.90))。

   在执行时，实时 (JIT) 编译器将 MSIL 翻译为本机代码。在此编译过程中，代码必须通过验证过程，该过程检查 MSIL 和元数据以查看是否可以将代码确定为类型安全。

4. [运行代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/8t3521k6(v=vs.90))。

   公共语言运行库提供使执行能够发生以及可在执行期间使用的各种服务的结构。



**中间语言**





## 1.2	.NET 体系结构

![image.png](https://upload-images.jianshu.io/upload_images/1979022-801fe113610c2aaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





### 1.2.1	.NET 体系结构的组件

> A .NET app is developed for and runs in one or more *implementations of .NET*.  Implementations of .NET include the .NET Framework, .NET Core, and Mono. There is an API specification common to all implementations of .NET that's called the .NET Standard.

.NET应用的开发和运行可以基于一个或者多个.NET的实现。.NET的实现包括 .NET Framework，.NET Core，以及Mono。而.NET的所有实现都是基于.NET Standard这个通用API规范的。

#### 1	.NET Standard

.NET Standard是一组由 .NET实现的基类库实现的API。这样保证了不同 .NET实现间的可移植性。

.NET Standard 也是一个[目标框架](https://docs.microsoft.com/zh-cn/dotnet/standard/glossary#target-framework)。 如果代码面向 .NET Standard 版本，则它可在支持该 .NET Standard 版本的任何 .NET 实现上运行。

#### 2	.NET 实现

Each implementation of .NET includes the following components:

- One or more runtimes. Examples: CLR for .NET Framework, CoreCLR and CoreRT for .NET Core.
- A class library that implements the .NET Standard and may implement additional APIs. Examples: .NET Framework Base Class Library, .NET Core Base Class Library.
- Optionally, one or more application frameworks. Examples: [ASP.NET](https://www.asp.net/), [Windows Forms](https://docs.microsoft.com/zh-cn/dotnet/framework/winforms/windows-forms-overview), and [Windows Presentation Foundation (WPF)](https://docs.microsoft.com/zh-cn/dotnet/framework/wpf/) are included in the .NET Framework and .NET Core.
- Optionally, development tools. Some development tools are shared among multiple implementations.

There are four primary .NET implementations that Microsoft actively develops  and maintains: .NET Core, .NET Framework, Mono.

**.NET Core**

.NET Core 是 .NET 的跨平台实现，专用于处理大规模的服务器和云工作负荷。 可在 Windows、macOS 和 Linux 上运行。 它实现 .NET Standard，因此面向 .NET Standard 的代码都可在 .NET Core 上运行。 [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core)、[Windows 窗体](https://docs.microsoft.com/zh-cn/dotnet/framework/winforms/windows-forms-overview)和 [Windows Presentation Foundation (WPF)](https://docs.microsoft.com/zh-cn/dotnet/framework/wpf/) 都在 .NET Core 上运行。

**.NET Framework**

.Net Framework 是自 2002 年起就已存在的原始 .NET 实现。 4.5 版以及更高版本实现 .NET Standard， 它还包含一些特定于 Windows 的 API，如通过 Windows 窗体和 WPF 进行 Windows 桌面开发的 API。

**Mono**

MONO项目是由Ximian发起、Miguel de lcaza领导、Novell公司主持的项目。它是一个致力于开创.NET在Linux，FreeBSD，Unix，Mac OS  X和Solaris等其他平台使用的开源工程。它包含了一个C#语言的编译器，一个CLR的运行时，和一组类库，并逐渐实现了  ADO.NET、ASP.NET、WinForm、Silverlight（可惜没有实现强大的WPF），能够使得开发人员在其他平台用C#开发程序。

#### 3	.NET 运行时

运行时是用于托管程序的执行环境。 操作系统属于运行时环境，但不属于 .NET 运行时。 下面是 .NET 运行时的一些示例：

- .NET Framework 公共语言运行时 (CLR)
- .NET Core 核心公共语言运行时 (CoreCLR)
- 用于 Xamarin.iOS、Xamarin.Android、Xamarin.Mac 和 Mono 桌面框架的 Mono 运行时

#### 4	.NET 工具和常见基础结构

可访问一整套适用于每种 .NET 实现的工具和基础结构组件。 这些工具和组件包括：

- .NET 语言及其编译器
- .NET 项目系统（基于 .csproj  .vbproj  和 .fsproj  文件）
- [MSBuild](https://docs.microsoft.com/zh-cn/visualstudio/msbuild/msbuild)（用于生成项目的生成引擎）
- [NuGet](https://docs.microsoft.com/zh-cn/nuget/)（适用于.NET 的 Microsoft 程序包管理器）
- 开放源生成业务流程工具，例如 [CAKE](https://cakebuild.net/) 和 [FAKE](https://fake.build/)



### 1.2.2 	.NET Framework

![ .NET Framework的体系结构](http://c.biancheng.net/uploads/allimg/190313/4-1Z3131IF54N.gif)

.NET Framwork是CLR的一种实现，它包括名为“公共语言运行时 (CLR)”的虚执行系统和一组统一的类库。 

用 C# 编写的源代码被编译成符合 CLI 规范的[中间语言 (IL)](https://docs.microsoft.com/zh-cn/dotnet/standard/managed-code)。 IL 代码和资源（如位图和字符串）存储在磁盘上名为“程序集”的可执行文件（扩展名通常为 .exe 或 .dll）中。 程序集包含一个介绍程序集的类型、版本、区域性和安全要求的清单。

当 C# 程序执行时，程序集会加载到 CLR 中，可能根据清单中的信息执行各种操作。 然后，如果满足安全要求，CLR 会直接执行实时 (JIT) 编译，将 IL 代码转换成本机指令。 CLR 还提供其他与自动垃圾回收、异常处理和资源管理相关的服务。 CLR 执行的代码有时称为“托管代码”（而不是“非托管代码”），被编译成面向特定系统的本机语言。 下图展示了 C# 源代码文件、.NET Framework 类库、程序集和 CLR 的编译时和运行时关系。

![](https://docs.microsoft.com/zh-cn/dotnet/csharp/getting-started/media/introduction-to-the-csharp-language-and-the-net-framework/net-architecture-relationships.png)

语言互操作性是 .NET Framework 的一项重要功能。 由于 C# 编译器生成的 IL 代码符合公共类型规范 (CTS)，因此 C# 生成的 IL 代码可以与 .NET 版本 Visual Basic、Visual C++ 或其他任何符合 CTS 的超过 20 种语言生成的代码进行交互。 一个程序集可能包含多个用不同 .NET 语言编写的模块，且类型可以相互引用，就像是用同一种语言编写的一样。

除了运行时服务之外，.NET Framework 还包括一个由 4000 多个已整理到命名空间中的类构成的扩展库，这些类提供各种实用功能，包括文件输入输出、字符串控制、XML 分析和 Windows 窗体控件。

有关 .NET Framework 的详细信息，请参阅 [Microsoft.NET Framework 概述](https://docs.microsoft.com/zh-cn/dotnet/framework/get-started/overview)。





# 2	.NET 指南



## 2.1	内存管理

每个进程都有其自己单独的虚拟地址空间。 同一台计算机上的所有进程共享相同的物理内存和页文件（如果有）。默认情况下，32 位计算机上的每个进程都具有 2 GB 的用户模式[虚拟地址空间]()。

虚拟内存有三种状态：

| 状态   | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| Free   | 该内存块没有引用关系，可用于分配。                           |
| 保留   | 内存块可供你使用，并且不能用于任何其他分配请求。 但是，在该内存块提交之前，你无法将数据存储到其中。 |
| 已提交 | 内存块已指派给物理存储。                                     |

自动内存管理是公共语言运行时在[托管执行](https://docs.microsoft.com/zh-cn/dotnet/standard/managed-execution-process)过程中提供的服务之一。.NET 的垃圾回收器管理应用程序的内存分配和释放。 每当有对象新建时，公共语言运行时都会从托管堆为对象分配内存。 只要托管堆中有地址空间，运行时就会继续为新对象分配空间。 不过，内存并不是无限的。 垃圾回收器最终必须执行垃圾回收来释放一些内存。 垃圾回收器的优化引擎会根据所执行的分配来确定执行回收的最佳时机。 执行回收时，垃圾回收器会在托管堆中检查应用程序不再使用的对象，然后执行必要的操作来回收其内存。



### 2.1.1	垃圾回收

在公共语言运行时 (CLR) 中，垃圾回收器 (GC) 用作自动内存管理器。 对于使用托管代码的开发人员而言，这就意味着不必编写执行内存管理任务的代码。 自动内存管理可解决常见问题，例如，忘记释放对象并导致内存泄漏，或尝试访问已释放对象的内存。

垃圾回收器具有以下优点：

- 开发人员**不必手动释放内存**。
- **有效分配**托管堆上的对象。
- 回收不再使用的对象，清除它们的内存，并保留内存以用于将来分配。 托管对象会自动获取**干净**的内容来开始，因此，它们的构造函数不必对每个数据字段进行初始化。
- 通过确保对象不能使用另一个对象的内容来提供**内存安全**。



#### 内存分配

初始化新进程时，运行时会为进程保留一个连续的地址空间区域。 这个保留的地址空间被称为托管堆。 托管堆维护着一个指针，用它指向将在堆中分配的下一个对象的地址。 最初，该指针设置为指向托管堆的基址。 托管堆上部署了所有引用类型。 应用程序创建第一个引用类型时，将为托管堆的基址中的类型分配内存。 应用程序创建下一个对象时，垃圾回收器在紧接第一个对象后面的地址空间内为它分配内存。 只要地址空间可用，垃圾回收器就会继续以这种方式为新对象分配空间。

从托管堆中分配内存要比非托管内存分配速度快。 由于运行时通过为指针添加值来为对象分配内存，所以这几乎和从堆栈中分配内存一样快。 另外，由于连续分配的新对象在托管堆中是连续存储，所以应用程序可以快速访问这些对象。



#### 内存释放

垃圾回收器的优化引擎根据所执行的分配决定执行回收的最佳时间。 垃圾回收器在执行回收时，会释放应用程序不再使用的对象的内存。 它通过检查应用程序的根来确定不再使用的对象。 每个应用程序都有一组根。每个根引用托管堆里的一个对象或者被设置为null。垃圾回收器可以访问由[实时 (JIT) 编译器](https://docs.microsoft.com/zh-cn/dotnet/standard/managed-execution-process)和运行时维护的活动根的列表。 垃圾回收器对照此列表检查应用程序的根，并在此过程中创建一个图表，在其中包含所有可从这些根中访问的对象。

不在该图表中的对象将无法从应用程序的根中访问。 垃圾回收器会考虑无法访问的对象垃圾，并释放为它们分配的内存。 在回收中，垃圾回收器检查托管堆，查找无法访问对象所占据的地址空间块。 发现无法访问的对象时，它就使用内存复制功能来压缩内存中可以访问的对象，释放分配给不可访问对象的地址空间块。 在压缩了可访问对象的内存后，垃圾回收器就会做出必要的指针更正，以便应用程序的根指向新地址中的对象。 它还将托管堆指针定位至最后一个可访问对象之后。 请注意，只有在回收发现大量的无法访问的对象时，才会压缩内存。 如果托管堆中的所有对象均未被回收，则不需要压缩内存。

为了改进性能，运行时为单独堆中的大型对象分配内存。 垃圾回收器会自动释放大型对象的内存。 但是，为了避免移动内存中的大型对象，不会压缩此内存。



#### 垃圾回收的条件

当满足以下条件之一时将发生垃圾回收：

- 系统具有低的物理内存。 这是通过 OS 的内存不足通知或主机指示的内存不足检测出来。
- 由托管堆上已分配的对象使用的内存超出了可接受的阈值。 随着进程的运行，此阈值会不断地进行调整。
- 调用 [GC.Collect](https://docs.microsoft.com/zh-cn/dotnet/api/system.gc.collect) 方法。 几乎在所有情况下，你都不必调用此方法，因为垃圾回收器会持续运行。 此方法主要用于特殊情况和测试。



#### 托管堆

在垃圾回收器由 CLR 初始化之后，它会分配一段内存用于存储和管理对象。 此内存称为托管堆（与操作系统中的本机堆相对）。

每个托管进程都有一个托管堆。 进程中的所有线程都在同一堆上为对象分配内存。

若要保留内存，垃圾回收器会调用 Windows [VirtualAlloc](https://docs.microsoft.com/zh-cn/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc) 函数，并且每次为托管应用保留一个内存段。 垃圾回收器还会根据需要保留内存段，并调用 Windows [VirtualFree](https://docs.microsoft.com/zh-cn/windows/desktop/api/memoryapi/nf-memoryapi-virtualfree) 函数，将内存段释放回操作系统（在清除所有对象的内存段后）。

当触发垃圾回收时，垃圾回收器将回收由非活动对象占用的内存。 回收进程会对活动对象进行压缩，以便将它们一起移动，并移除死空间，从而使堆更小一些。 这将确保一起分配的对象全都位于托管堆上，从而保留它们的局部性。

垃圾回收的侵入性（频率和持续时间）是由分配的数量和托管堆上保留的内存数量决定的。



#### 级数

垃圾回收方案的原理已在计算机软件业通过实验得到了证实。运行时的垃圾回收算法（GC算法）基于以下几个普遍原理：

- 压缩托管堆的一部分内存要比压缩整个托管堆速度快。
- 较新的对象生存期较短，而较旧的对象生存期则较长。
- 较新的对象趋向于相互关联，并且大致同时由应用程序访问。

垃圾回收主要在回收短生存期对象时发生。 为优化垃圾回收器的性能，将托管堆分为三级：0、1和2，因此它可以单独处理长生存期和短生存期对象。 垃圾回收器将新对象存储在第 0 级中。 在应用程序生存期的早期创建的对象如果未被回收，则被依次升级并存储在第 1 级和第 2 级中。 因为压缩托管堆的一部分要比压缩整个托管堆速度快，所以此方案允许垃圾回收器在每次执行回收时释放特定级别的内存，而不是整个托管堆的内存。

> 实际上，垃圾回收器在第 0 级托管堆已满时执行回收。 如果应用程序在第 0 级托管堆已满时尝试新建对象，垃圾回收器将会发现第 0 级托管堆中没有可分配给该对象的剩余地址空间。 垃圾回收器执行回收，尝试为对象释放第 0 级托管堆中的地址空间。 垃圾回收器从检查第 0 级托管堆中的对象（而不是托管堆中的所有对象）开始执行回收。 这是最有效的途径，因为新对象的生存期往往较短，并且期望在执行回收时，应用程序不再使用第 0 级托管堆中的许多对象。 另外，单独回收第 0 级托管堆通常可以回收足够的内存，这样，应用程序便可以继续创建新对象。
>
> 垃圾回收器执行第 0 级托管堆的回收后，会压缩可访问对象的内存。 然后，垃圾回收器升级这些对象到第 1 级托管堆。 因为未被回收的对象往往具有较长的生存期，所以将它们升级至更高的级别很有意义。 因此，垃圾回收器在每次执行第 0 级托管堆的回收时，不必重新检查第 1 级和第 2 级托管堆中的对象。
>
> 在执行第 0 级托管堆的首次回收并把可访问的对象升级至第 1 级托管堆后，垃圾回收器将考虑第 0 级托管堆的其余部分。 它将继续为第 0 级托管堆中的新对象分配内存，直至第 0 级托管堆已满并需执行另一回收为止。 这时，垃圾回收器的优化引擎会决定是否需要检查较旧的级别中的对象。 例如，如果第 0 级托管堆的回收没有回收足够的内存，不能使应用程序成功完成创建新对象的尝试，垃圾回收器就会先执行第 1 级托管堆的回收，然后再执行第 2 级托管堆的回收。 如果这样仍不能回收足够的内存，垃圾回收器将执行第 2、1 和 0 级托管堆的回收。 每次回收后，垃圾回收器都会压缩第 0 级托管堆中的可访问对象并将它们升级至第 1 级托管堆。 第 1 级托管堆中未被回收的对象将会升级至第 2 级托管堆。 由于垃圾回收器只支持三个级别，因此第 2 级托管堆中未被回收的对象会继续保留在第 2 级托管堆中，直到在将来的回收中确定它们为无法访问为止。

图 1 说明了一种情况，在第一次第 0 代 GC 后 GC 形成了第 1 代，其中 `Obj1` 和 `Obj3` 被清除；在第一次第 1 代 GC 后形成了第 2 代，其中 `Obj2` 和 `Obj5` 被清除。 请注意此图和下图仅用于说明，它们只包含能更好展示堆上的情况的极少几个对象。 实际上，GC 中通常包含更多的对象。

![图 1：第 0 代 GC 和第 1 代 GC](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/media/loh/loh-figure-1.jpg)

图 2 显示了第 2 代 GC 发现 `Obj1` 和 `Obj2` 被清除后，GC 在内存中形成了相邻的可用空间，由 `Obj1` 和 `Obj2` 占用，然后用于满足 `Obj4` 的分配要求。 从最后一个对象 `Obj3` 到此段末尾的空间仍可用于满足分配请求。

![图 2：第 2 代 GC 后](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/media/loh/loh-figure-2.jpg)



当条件得到满足时，垃圾回收将在特定级上发生。 回收某个级意味着回收此级中的对象及其所有更年轻的级。 第 2 级垃圾回收也称为完整垃圾回收，因为它回收所有级中的对象（即，托管堆中的所有对象）。



**幸存和提升**

垃圾回收中未回收的对象也称为幸存者，并会被提升到下一级：

- 第 0 级垃圾回收中未被回收的对象将会升级至第 1 级。
- 第 1 级垃圾回收中未被回收的对象将会升级至第 2 级。
- 第 2 级垃圾回收中未被回收的对象将仍保留在第 2 级。

当垃圾回收器检测到某个级中的幸存率很高时，它会增加该级的分配阈值。 下次回收将回收非常大的内存。 CLR 持续在以下两个优先级之间进行平衡：不允许通过延迟垃圾回收，让应用程序的工作集获取太大内存，以及不允许垃圾回收过于频繁地运行。



**暂时代和暂时段**

因为第 0 代和第 1 代中的对象的生存期较短，因此，这些代被称为“暂时代”。

暂时代在称为“暂时段”的内存段中进行分配。 垃圾回收器获取的每个新段将成为新的暂时段，并包含在第 0 代垃圾回收中幸存的对象。 旧的暂时段将成为新的第 2 代段。

根据系统为 32 位还是 64 位以及它正在哪种类型的垃圾回收器（工作站或服务器 GC）上运行，暂时段的大小发生相应变化。 下表显示了暂时段的默认大小：

| 工作站/服务器 GC                     | 32 位 | 64 位  |
| ------------------------------------ | ----- | ------ |
| 工作站 GC                            | 16 MB | 256 MB |
| 服务器 GC                            | 64 MB | 4 GB   |
| 服务器 GC（具有 4 个以上的逻辑 CPU） | 32 MB | 2 GB   |
| 服务器 GC（具有 8 个以上的逻辑 CPU） | 16 MB | 1 GB   |



#### 垃圾回收过程发生的情况





### 2.1.2	大型对象堆

.NET 垃圾回收器 (GC) 将对象分为小型和大型对象。 如果是大型对象，它的某些特性将比对象较小时显得更为重要。 例如，压缩大型对象（也就是在内存中将其复制到堆上的其他位置）的性能损耗相当高。 因此，垃圾回收器将大型对象放置在大型对象堆 (LOH) 上。

如果对象的大小大于或等于 85,000 字节，将被视为大型对象。 此数字根据性能优化确定。 对象分配请求为 85,000 字节或更大时，运行时会将其分配到大型对象堆。

小型对象始终在第 0 代中进行分配，或者根据它们的生存期，可能会提升为第 1 代或第 2 代。 大型对象始终在第 2 代中进行分配。

大型对象属于第 2 代，因为只有在第 2 代回收期间才能回收它们。 回收一代时，同时也会回收它前面的所有代。 例如，执行第 1 代 GC 时，将同时回收第 1 代和第 0 代。 执行第 2 代 GC 时，将回收整个堆。 因此，第 2 代 GC 还可称为“完整 GC”。 本文引用第 2 代 GC 而不是完整 GC，但这两个术语是可以互换的。

实际上，对象存在于托管堆段中。 托管堆段是 GC 通过调用 [VirtualAlloc 功能](https://docs.microsoft.com/zh-cn/windows/desktop/api/memoryapi/nf-memoryapi-virtualalloc)代表托管代码在操作系统上保留的内存块。 加载 CLR 时，GC 分配两个初始堆段：一个用于小型对象（小型对象堆或 SOH），一个用于大型对象（大型对象堆）。

然后，通过将托管对象置于这些托管堆段上来满足分配请求。 如果该对象小于 85,000 字节，则将它置于 SOH 的段上，否则，将它置于 LOH 段。对于 SOH，GC 未处理的对象将提升为下一代。 第 0 代回收未处理的对象现在视为第 1 代对象，以此类推。 但是，最后一代回收未处理的对象仍会被视为最后一代中的对象。 也就是说，第 2 代垃圾回收未处理的对象仍是第 2 代对象；LOH 未处理的对象仍是 LOH 对象（由第 2 代回收）。

用户代码只能在第 0 代（小型对象）或 LOH（大型对象）中分配。 只有 GC 可以在第 1 代（通过提升第 0 代回收未处理的对象）和第 2 代（通过提升第 1 代和第 2 代回收未处理的对象）中“分配”对象。



#### 何时收集大型对象？

通常情况下，出现以下三种情形中的任一情况，都会执行 GC：

- 分配超出第 0 代或大型对象阈值。

  阈值是某代的属性。 垃圾回收器在其中分配对象时，会为代设置阈值。 超出阈值后，会在该代上触发 GC。 因此，分配小型或大型对象时，需要分别使用第 0 代和 LOH 的阈值。 当垃圾回收器分配到第 1 代和第 2 代中时，将使用它们的阈值。 运行此程序时，会动态调整这些阈值。

  这是典型情况，大部分 GC 执行都因为托管堆上的分配。

- 调用 [GC.Collect](https://docs.microsoft.com/zh-cn/dotnet/api/system.gc.collect) 方法。

  如果调用无参数 [GC.Collect()](https://docs.microsoft.com/zh-cn/dotnet/api/system.gc.collect#System_GC_Collect) 方法，或另一个重载作为参数传递到 [GC.MaxGeneration](https://docs.microsoft.com/zh-cn/dotnet/api/system.gc.maxgeneration#System_GC_MaxGeneration)，将会一起收集 LOH 和剩余的托管堆。

- 系统处于内存不足的状况。

  垃圾回收器收到来自操作系统 的高内存通知时，会发生以上情况。 如果垃圾回收器认为执行第 2 代 GC 会有效率，它将触发第 2 代。



#### LOH 性能意义

大型对象堆上的分配通过以下几种方式影响性能。

- 分配成本。

  CLR 确保清除了它提供的每个新对象的内存。 这意味着大型对象的分配成本完全由清理的内存（除非触发了 GC）决定。 如果需要 2 轮才能清除一个字节，即需要 170,000 轮才能清除最小的大型对象。 清除 2GHz 计算机上 16MB 对象的内存大约需要 16ms。 这些成本相当大。

- 回收成本。

  因为 LOH 和第 2 代一起回收，如果超出了它们之中任何一个的阈值，则触发第 2 代回收。 如果由于 LOH 触发第 2 代回收，第 2 代没有必要在 GC 后变得更小。 如果第 2 代上数据不多，则影响较小。 但是，如果第 2 代很大，则触发多次第 2 代 GC 可能会产生性能问题。 如果很多大型对象都在非常短暂的基础上进行分配，并且拥有大型 SOH，则可能会花费太多时间来执行 GC。 除此之外，如果连续分配并且释放真正的大型对象，那么分配成本可能会增加。

- 具有引用类型的数组元素。

  LOH 上的特大型对象通常是数组（很少会有非常大的实例对象）。 如果数组的元素有丰富的引用，则可能产生成本；如果元素没有丰富的引用，将不会产生此类成本。 如果元素不包含任何引用，则垃圾回收器根本无需处理此数组。 例如，如果使用数组存储二进制树中的节点，一种实现方法是按实际节点引用某个节点的左侧节点和右侧节点：

  ```csharp
  class Node
  {
     Data d;
     Node left;
     Node right;
  };
  
  Node[] binary_tr = new Node [num_nodes];
  ```

  如果 `num_nodes` 非常大，则垃圾回收器需要处理每个元素的至少两个引用。 另一种方法是存储左侧节点和右侧节点的索引：

  ```csharp
  class Node
  {
     Data d;
     uint left_index;
     uint right_index;
  } ;
  ```

  不要将左侧节点的数据引用为 `left.d`，而是将其引用为 `binary_tr[left_index].d`。 而垃圾回收器无需查看左侧节点和右侧节点的任何引用。

在这三种因素中，前两个通常比第三个更重要。 因此，建议分配重复使用的大型对象池，而不是分配临时大型对象。



### 2.1.3	垃圾回收和性能

可使用以下工具来收集垃圾回收性能数据：

- [.NET CLR 内存性能计数器](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/large-object-heap#net-clr-memory-performance-counters)
- [ETW 事件](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/large-object-heap#etw-events)
- [调试器](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/large-object-heap#a-debugger)

可以使用 [Windows 调试器 (WinDbg)](https://docs.microsoft.com/zh-cn/windows-hardware/drivers/debugger/index) 检查托管堆上的对象。

若要安装 WinDbg，请从[下载 Windows 调试工具](https://docs.microsoft.com/zh-cn/windows-hardware/drivers/debugger/debugger-download-tools)页安装 Windows 调试工具。

详情参照：

[垃圾回收和性能](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/performance)

[Windows 系统上的大型对象堆](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/large-object-heap)



## 2.2	[清理非托管资源](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/unmanaged)

对于应用创建的大多数对象，可以依赖 [.NET 垃圾回收器](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/)来进行内存管理。 但是，如果创建包含非托管资源的对象，则当你使用完非托管资源后，必须显式释放这些资源。 最常用的非托管资源类型是包装操作系统资源的对象，如文件、窗口、网络连接或数据库连接。 虽然垃圾回收器可以跟踪封装非托管资源的对象的生存期，但无法了解如何发布并清理这些非托管资源。创建封装非托管资源的对象时，建议在公共 **Dispose** 方法中提供必要的代码以清理非托管资源。 通过提供 **Dispose** 方法，对象的用户可以在使用完对象后显式释放其内存。

如果你的类型使用非托管资源，则应执行以下操作：

- 实现[清理模式](https://docs.microsoft.com/zh-cn/dotnet/standard/garbage-collection/implementing-dispose)。 这要求你提供 [IDisposable.Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 实现以启用非托管资源的确定性释放。 当不再需要此对象（或其使用的资源）时，类型使用者可调用 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose)。 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 方法立即释放非托管资源。

- 在类型使用者忘记调用 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 的情况下，请提供一种方法来释放非托管资源。 有两种方法可以实现此目的：

  - 使用安全句柄包装非托管资源。 这是推荐采用的方法。 安全句柄派生自 [System.Runtime.InteropServices.SafeHandle](https://docs.microsoft.com/zh-cn/dotnet/api/system.runtime.interopservices.safehandle) 抽象类，并包含可靠的 [Finalize](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.finalize) 方法。 在使用安全句柄时，只需实现 [IDisposable](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable) 接口并在 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.runtime.interopservices.safehandle.dispose) 实现中调用安全句柄的 [IDisposable.Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 方法。 如果未调用安全句柄的 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 方法，则垃圾回收器将自动调用安全句柄的终结器。

    —或—

  - 重写 [Object.Finalize](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.finalize) 方法。 当类型使用者无法调用 [IDisposable.Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 以确定性地释放非托管资源时，终止会启用对非托管资源的非确定性释放。 通过重写 [Object.Finalize](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.finalize) 方法来定义[终结器](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/destructors)。

  > 警告
  >
  > 但是，由于对象终止是一项复杂且易出错的操作，建议你使用安全句柄，而不是提供你自己的终结器。

然后，类型使用者可直接调用 [IDisposable.Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 实现以释放非托管资源使用的内存。 在正确实现 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 方法时，安全句柄的 [Finalize](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.finalize) 方法或 [Object.Finalize](https://docs.microsoft.com/zh-cn/dotnet/api/system.object.finalize) 方法的重写会在未调用 [Dispose](https://docs.microsoft.com/zh-cn/dotnet/api/system.idisposable.dispose) 方法的情况下阻止清理资源。



### 2.2.1	实现Dispose方法





### 2.2.2	实现DisposeAsync方法





### 2.2.3	实现IDisposable的对象











# 2.	C#语法

## 2.1	C# 基础语法

## 2.2	C# 高级语法



# 3.	C#高级编程



































































## C# 语言和 .NET Framework 简介



### C#语言

C# 是一种面向对象且类型安全的编程语言。



### .NET Framework 平台体系结构

.NET 框架是一个多语言组件开发和执行环境，它提供了一个跨语言的统一编程环境。而 C# 是一种在 .NET 开发平台上使用的编程语言，目前能在 .NET 平台上使用的开发语言很多，例如 Visual Basic .NET、[Python](http://c.biancheng.net/python/)、J#、Visual C++.NET 等。但在 .NET 平台上使用最多的是 C# 语言。

C# 程序在 .NET Framework 上运行，这是 Windows 不可或缺的一部分，包括名为“公共语言运行时 (CLR)”的虚执行系统和一组统一的类库。 CLR 是由 Microsoft 执行的公共语言基础结构 (CLI) 的商业实现，CLI 是作为执行和开发环境（语言和库在其中无缝协作）创建依据的国际标准。

用 C# 编写的源代码被编译成符合 CLI 规范的[中间语言 (IL)](https://docs.microsoft.com/zh-cn/dotnet/standard/managed-code)。 IL 代码和资源（如位图和字符串）存储在磁盘上名为“程序集”的可执行文件（扩展名通常为 .exe 或 .dll）中。 程序集包含一个介绍程序集的类型、版本、区域性和安全要求的清单。

当 C# 程序执行时，程序集会加载到 CLR 中，可能根据清单中的信息执行各种操作。 然后，如果满足安全要求，CLR 会直接执行实时 (JIT) 编译，将 IL 代码转换成本机指令。 CLR 还提供其他与自动垃圾回收、异常处理和资源管理相关的服务。 CLR 执行的代码有时称为“托管代码”（而不是“非托管代码”），被编译成面向特定系统的本机语言。 下图展示了 C# 源代码文件、.NET Framework 类库、程序集和 CLR 的编译时和运行时关系。

![](https://docs.microsoft.com/zh-cn/dotnet/csharp/getting-started/media/introduction-to-the-csharp-language-and-the-net-framework/net-architecture-relationships.png)

语言互操作性是 .NET Framework 的一项重要功能。 由于 C# 编译器生成的 IL 代码符合公共类型规范 (CTS)，因此 C# 生成的 IL 代码可以与 .NET 版本 Visual Basic、Visual C++ 或其他任何符合 CTS 的超过 20 种语言生成的代码进行交互。 一个程序集可能包含多个用不同 .NET 语言编写的模块，且类型可以相互引用，就像是用同一种语言编写的一样。

除了运行时服务之外，.NET Framework 还包括一个由 4000 多个已整理到命名空间中的类构成的扩展库，这些类提供各种实用功能，包括文件输入输出、字符串控制、XML 分析和 Windows 窗体控件。

有关 .NET Framework 的详细信息，请参阅 [Microsoft.NET Framework 概述](https://docs.microsoft.com/zh-cn/dotnet/framework/get-started/overview)。





## .NET 中的程序集

程序集构成了 .NET 应用程序的部署、版本控制、重用、激活范围和安全权限的基本单元。 程序集是为协同工作而生成的类型和资源的集合，这些类型和资源构成了一个逻辑功能单元。 程序集采用可执行文件 (.exe) 或动态链接库文件 (.dll) 的形式，是 .NET 应用程序的构建基块   。 它们向公共语言运行时提供了注意类型实现代码所需的信息。

**ILMerge**

**Fody**

**Nuget**





## 特性

特性向程序添加元数据。 *元数据*是程序中定义的类型的相关信息。 所有 .NET 程序集都包含一组指定的元数据，用于描述程序集中定义的类型和类型成员。 可以添加自定义特性来指定所需的其他任何信息。

使用特性，可以有效地将元数据或声明性信息与代码（程序集、类型、方法、属性等）相关联。 将特性与程序实体相关联后，可以在运行时使用*反射*这项技术查询特性。

.Net 框架提供了两种类型的特性：*预定义*特性和*自定义*特性。



.Net 框架提供了三种预定义特性：

- AttributeUsage
- Conditional
- Obsolete



创建并使用自定义特性包含四个步骤：

- 声明自定义特性
- 构建自定义特性
- 在目标程序元素上应用自定义特性
- 通过反射访问特性

1、创建一个自定义特性：

```c#
// 描述如何使用一个自定义特性 SomethingAttribute
[AttributeUsage(AttributeTargets.All, AllowMultiple = true, Inherited = true)]    

//********自定义特性SomethingAttribute**************//
public class SomethingAttribute : Attribute    {
    private string name; // 名字
    private string data; // 日期
    public string Name {
        get { return name; }
        set { name = value; }
    }
    public string Data    {
        get { return data; }
        set { data = value; }
    }
    public SomethingAttribute(string name)    {
        this.name = name;
        this.name = name;
    }
}
```

2、实例化自定义

```c#
[Something("Amy", Data = "2018-06-18")]
[Something("Jack", Data = "2018-06-18")]
class Test{}
```

3、获取自定义特性的中的变量

```c#
Type t = typeof(Test);
var something = t.GetCustomAttributes(typeof(SomethingAttribute),true);
foreach(SomethingAttribute each in something)
{
    Console.WriteLine("Name:{0}", each.Name);
    Console.WriteLine("Data:{0}",each.Data);
}
```





## 动态编程

### 1.	反射

反射提供描述程序集、模块和类型的对象（[Type](https://docs.microsoft.com/zh-cn/dotnet/api/system.type) 类型）。 可以使用反射动态地创建类型的实例，将类型绑定到现有对象，或从现有对象中获取类型，然后调用其方法或访问器字段和属性。 如果代码中使用了特性，可以利用反射来访问它们。



#### 1.1	Assembly 类

使用 [Assembly](https://docs.microsoft.com/zh-cn/dotnet/api/system.reflection.assembly?view=netframework-4.8) 类加载程序集、浏览程序集的元数据和构成部分、发现程序集中包含的类型以及创建这些类型的实例。

* 查看类型信息
* 动态加载和动态创建对象
* 访问自定义特性
* 执行动态方法

##### 1.1.1	查看类型信息

```c#
// 获取程序集 Assembly
Assembly ass = typeof(System.IO.Path).Assembly;
/* Assembly 静态方法 */
var ass1 = Assembly.GetAssembly(typeof(System.IO.Path));
var ass2 = Assembly.GetCallingAssembly();
var ass3 = Assembly.GetEntryAssembly();
var ass4 = Assembly.GetExecutingAssembly();

// 获取Type,一旦获取 Type 对象，可通过多种方式来查看该类型成员的相关信息。
/* 使用Assembly.GetType或Assembly.GetTypes从尚未加载的程序集中获取Type对象，传入所需类型的名称 */
Type type = ass.GetType("System.IO.Path");
Type[] types = ass.GetTypes();
/* 使用 Type.GetType 从已加载的程序集中获取 Type 对象 */
Type t0 = Type.GetType("System.IO.Path");
/* Module.GetType 和 Module.GetTypes 获取模块 Type 对象 */
Module[] moduleArray = typeof(System.IO.Path).Assembly.GetModules(false);
Type t1 = moduleArray[0].GetType("System.IO.Path");
Type[] ts2 = moduleArray[0].GetTypes();

// 查看程序集类型信息
/* System.Type 类是反射的中心。 当反射提出请求时，公共语言运行时为已加载的类型创建 Type。 可使用 Type 对象的方法、字段、属性和嵌套类来查找该类型的任何信息。 
使用 MemberInfo、MethodInfo、FieldInfo 或 PropertyInfo 对象获取类型的方法、属性、事件和字段的相关信息。PropertyInfo类发现属性 (Property) 的属性 (Attribute) 并提供对属性 (Property) 元数据的访问。
*/
// This program lists all the members of the
// System.IO.BufferedStream class.
using System;
using System.IO;
using System.Reflection;

class ListMembers
{
    public static void Main()
    {
        // Specifies the class.
        Type t = typeof(System.IO.BufferedStream);
        Console.WriteLine("Listing all the members (public and non public) of the {0} type", t);

        // Lists static fields first.
        FieldInfo[] fi = t.GetFields(BindingFlags.Static |
            BindingFlags.NonPublic | BindingFlags.Public);
        Console.WriteLine("// Static Fields");
        PrintMembers(fi);

        // Static properties.
        PropertyInfo[] pi = t.GetProperties(BindingFlags.Static |
            BindingFlags.NonPublic | BindingFlags.Public);
        Console.WriteLine("// Static Properties");
        PrintMembers(pi);

        // Static events.
        EventInfo[] ei = t.GetEvents(BindingFlags.Static |
            BindingFlags.NonPublic | BindingFlags.Public);
        Console.WriteLine("// Static Events");
        PrintMembers(ei);

        // Static methods.
        MethodInfo[] mi = t.GetMethods (BindingFlags.Static |
            BindingFlags.NonPublic | BindingFlags.Public);
        Console.WriteLine("// Static Methods");
        PrintMembers(mi);

        // Constructors.
        ConstructorInfo[] ci = t.GetConstructors(BindingFlags.Instance |
            BindingFlags.NonPublic | BindingFlags.Public);
        Console.WriteLine("// Constructors");
        PrintMembers(ci);

        // Instance fields.
        fi = t.GetFields(BindingFlags.Instance | BindingFlags.NonPublic |
            BindingFlags.Public);
        Console.WriteLine("// Instance Fields");
        PrintMembers(fi);

        // Instance properites.
        pi = t.GetProperties(BindingFlags.Instance | BindingFlags.NonPublic |
            BindingFlags.Public);
        Console.WriteLine ("// Instance Properties");
        PrintMembers(pi);

        // Instance events.
        ei = t.GetEvents(BindingFlags.Instance | BindingFlags.NonPublic |
            BindingFlags.Public);
        Console.WriteLine("// Instance Events");
        PrintMembers(ei);

        // Instance methods.
        mi = t.GetMethods(BindingFlags.Instance | BindingFlags.NonPublic
            | BindingFlags.Public);
        Console.WriteLine("// Instance Methods");
        PrintMembers(mi);

        Console.WriteLine("\r\nPress ENTER to exit.");
        Console.Read();
    }

    public static void PrintMembers (MemberInfo [] ms)
    {
        foreach (MemberInfo m in ms)
        {
            Console.WriteLine ("{0}{1}", "     ", m);
        }
        Console.WriteLine();
    }
}
```



##### 1.1.2	动态加载和动态创建对象

```c#
/* 动态加载Dll有3个函数：
public static Assembly Load(string assemblyString);
    该方法传入的是Dll的名字，该Dll必须位于全局缓存GAC中才行，不然会报“System.IO.FileLoadException: 未能加载文件或程序集”的异常。
public static Assembly LoadFile(string path);
    这个LoadFile最方便，参数就是dll的路径。
public static Assembly LoadFrom(string assemblyFile);
    这个方法也可以，参数同样是dll路径。
*/

namespace Contoso.Libraries
{
   public class Person
   {
      private string _name;
   
      public Person()
      { }
   
      public Person(string name)
      {
         this._name = name;
      }
   
      public string Name
      { 
         get { return this._name; }
         set { this._name = value; } 
      }
       
      public void SayHello() {
          Console.WriteLine($"Hello, {Name}");
      }
   
      public override string ToString()
      {
         return this._name;
      }
   }
}


// 加载dll
Assembly asm = Assembly.Load($"{DllPath}");
string classFullName = "Contoso.Libraries.Person";
// 获取类型
Type type = asm.GetType(classFullName);
// 创建该类的实例
var instance = asm.CreateInstance(classFullName);
// 设置属性
type.GetProperty("Name").SetValue(instance, "druihng");
// 获取方法
var method = type.GetMethod("SayHello");
method.Invoke(instance, null);


```

```c#
// 使用反射将委托挂钩

using System;
using System.Reflection;
using System.Reflection.Emit;
using System.Windows.Forms;

class ExampleForm : Form 
{
    public ExampleForm() : base()
    {
        this.Text = "Click me";
    }
}

class Example
{
    public static void Main()
    {
        Example ex = new Example();
        ex.HookUpDelegate();
    }

    private void HookUpDelegate()
    {
        // Load an assembly, for example using the Assembly.Load
        // method. In this case, the executing assembly is loaded, to
        // keep the demonstration simple.
        //
        Assembly assem = typeof(Example).Assembly;
 
        // Get the type that is to be loaded, and create an instance 
        // of it. Activator.CreateInstance has other overloads, if
        // the type lacks a default constructor. The new instance
        // is stored as type Object, to maintain the fiction that 
        // nothing is known about the assembly. (Note that you can
        // get the types in an assembly without knowing their names
        // in advance.)
        //
        Type tExForm = assem.GetType("ExampleForm");
        Object exFormAsObj = Activator.CreateInstance(tExForm);

        // Get an EventInfo representing the Click event, and get the
        // type of delegate that handles the event.
        //
        EventInfo evClick = tExForm.GetEvent("Click");
        Type tDelegate = evClick.EventHandlerType;

        // If you already have a method with the correct signature,
        // you can simply get a MethodInfo for it. 
        //
        MethodInfo miHandler = 
            typeof(Example).GetMethod("LuckyHandler", 
                BindingFlags.NonPublic | BindingFlags.Instance);
            
        // Create an instance of the delegate. Using the overloads
        // of CreateDelegate that take MethodInfo is recommended.
        //
        Delegate d = Delegate.CreateDelegate(tDelegate, this, miHandler);

        // Get the "add" accessor of the event and invoke it late-
        // bound, passing in the delegate instance. This is equivalent
        // to using the += operator in C#, or AddHandler in Visual
        // Basic. The instance on which the "add" accessor is invoked
        // is the form; the arguments must be passed as an array.
        //
        MethodInfo addHandler = evClick.GetAddMethod();
        Object[] addHandlerArgs = { d };
        addHandler.Invoke(exFormAsObj, addHandlerArgs);

        // Event handler methods can also be generated at run time,
        // using lightweight dynamic methods and Reflection.Emit. 
        // To construct an event handler, you need the return type
        // and parameter types of the delegate. These can be obtained
        // by examining the delegate's Invoke method. 
        //
        // It is not necessary to name dynamic methods, so the empty 
        // string can be used. The last argument associates the 
        // dynamic method with the current type, giving the delegate
        // access to all the public and private members of Example,
        // as if it were an instance method.
        //
        Type returnType = GetDelegateReturnType(tDelegate);
        if (returnType != typeof(void))
            throw new ApplicationException("Delegate has a return type.");
            
        DynamicMethod handler = 
            new DynamicMethod("", 
                              null,
                              GetDelegateParameterTypes(tDelegate),
                              typeof(Example));

        // Generate a method body. This method loads a string, calls 
        // the Show method overload that takes a string, pops the 
        // return value off the stack (because the handler has no
        // return type), and returns.
        //
        ILGenerator ilgen = handler.GetILGenerator();

        Type[] showParameters = { typeof(String) };
        MethodInfo simpleShow = 
            typeof(MessageBox).GetMethod("Show", showParameters);

        ilgen.Emit(OpCodes.Ldstr, 
            "This event handler was constructed at run time.");
        ilgen.Emit(OpCodes.Call, simpleShow);
        ilgen.Emit(OpCodes.Pop);
        ilgen.Emit(OpCodes.Ret);

        // Complete the dynamic method by calling its CreateDelegate
        // method. Use the "add" accessor to add the delegate to
        // the invocation list for the event.
        //
        Delegate dEmitted = handler.CreateDelegate(tDelegate);
        addHandler.Invoke(exFormAsObj, new Object[] { dEmitted });

        // Show the form. Clicking on the form causes the two
        // delegates to be invoked.
        //
        Application.Run((Form) exFormAsObj);
    }

    private void LuckyHandler(Object sender, EventArgs e)
    {
        MessageBox.Show("This event handler just happened to be lying around.");
    }

    private Type[] GetDelegateParameterTypes(Type d)
    {
        if (d.BaseType != typeof(MulticastDelegate))
            throw new ApplicationException("Not a delegate.");

        MethodInfo invoke = d.GetMethod("Invoke");
        if (invoke == null)
            throw new ApplicationException("Not a delegate.");

        ParameterInfo[] parameters = invoke.GetParameters();
        Type[] typeParameters = new Type[parameters.Length];
        for (int i = 0; i < parameters.Length; i++)
        {
            typeParameters[i] = parameters[i].ParameterType;
        }
        return typeParameters;
    }

    private Type GetDelegateReturnType(Type d)
    {
        if (d.BaseType != typeof(MulticastDelegate))
            throw new ApplicationException("Not a delegate.");

        MethodInfo invoke = d.GetMethod("Invoke");
        if (invoke == null)
            throw new ApplicationException("Not a delegate.");

        return invoke.ReturnType;
    }
}
```





## 序列化









## 语言集成查询（LINQ）

语言集成查询 (LINQ) 是一系列直接将查询功能集成到 C# 语言的技术统称。借助 LINQ，LINQ可以用相同的语法访问不同的数据源。LINQ提供了不同数据源的抽象层，所以可以使用相同的语法。LINQ 系列技术提供了针对对象 (LINQ to Objects)、关系数据库 (LINQ to SQL) 和 XML (LINQ to XML) 的一致查询体验。





## 字符串格式化





## 数据类型转换





## 委托和事件





## 文件操作





## 网络编程





## 并行编程

