# C#

## C#是什么？

C# 是一个现代的、通用的、面向对象的编程语言，它是由微软（Microsoft）开发的。C# 是由 Anders Hejlsberg 和他的团队在 .Net 框架开发期间开发的。

C# 是专为公共语言基础结构（CLI）设计的。CLI 由可执行代码和运行时环境组成，允许在不同的计算机平台和体系结构上使用各种高级语言。



# .Net体系结构

.NET 是一个通用开发平台，支持多种编程语言。.NET实现**公共语言基础结构（CLI）**，它指定与语言无关的运行时环境和语言互操作性，即它提供了一个跨语言的统一编程环境。

![image.png](https://upload-images.jianshu.io/upload_images/1979022-801fe113610c2aaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## .NET 体系结构的组件

> A .NET app is developed for and runs in one or more *implementations of .NET*.  Implementations of .NET include the .NET Framework, .NET Core, and Mono. There is an API specification common to all implementations of .NET that's called the .NET Standard.

.NET应用的开发和运行可以基于一个或者多个.NET的实现。.NET的实现包括 .NET Framework，.NET Core，以及Mono。而.NET的所有实现都是基于.NET Standard这个通用API规范的。



### 1.	.NET Standard

.NET Standard是一组由 .NET实现的基类库实现的API。这样保证了不同 .NET实现间的可移植性。

.NET Standard 也是一个[目标框架](https://docs.microsoft.com/zh-cn/dotnet/standard/glossary#target-framework)。 如果代码面向 .NET Standard 版本，则它可在支持该 .NET Standard 版本的任何 .NET 实现上运行。



### 2.	.NET 实现

Each implementation of .NET includes the following components:

- One or more runtimes. Examples: CLR for .NET Framework, CoreCLR and CoreRT for .NET Core.
- A class library that implements the .NET Standard and may implement additional APIs. Examples: .NET Framework Base Class Library, .NET Core Base Class Library.
- Optionally, one or more application frameworks. Examples: [ASP.NET](https://www.asp.net/), [Windows Forms](https://docs.microsoft.com/zh-cn/dotnet/framework/winforms/windows-forms-overview), and [Windows Presentation Foundation (WPF)](https://docs.microsoft.com/zh-cn/dotnet/framework/wpf/) are included in the .NET Framework and .NET Core.
- Optionally, development tools. Some development tools are shared among multiple implementations.

There are four primary .NET implementations that Microsoft actively develops  and maintains: .NET Core, .NET Framework, Mono.

#### 2.1	.NET Core

.NET Core 是 .NET 的跨平台实现，专用于处理大规模的服务器和云工作负荷。 可在 Windows、macOS 和 Linux 上运行。 它实现 .NET Standard，因此面向 .NET Standard 的代码都可在 .NET Core 上运行。 [ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core)、[Windows 窗体](https://docs.microsoft.com/zh-cn/dotnet/framework/winforms/windows-forms-overview)和 [Windows Presentation Foundation (WPF)](https://docs.microsoft.com/zh-cn/dotnet/framework/wpf/) 都在 .NET Core 上运行。

#### 2.2	.NET Framework

.Net Framework 是自 2002 年起就已存在的原始 .NET 实现。 4.5 版以及更高版本实现 .NET Standard， 它还包含一些特定于 Windows 的 API，如通过 Windows 窗体和 WPF 进行 Windows 桌面开发的 API。

#### 2.3	Mono

MONO项目是由Ximian发起、Miguel de lcaza领导、Novell公司主持的项目。它是一个致力于开创.NET在Linux，FreeBSD，Unix，Mac OS  X和Solaris等其他平台使用的开源工程。它包含了一个C#语言的编译器，一个CLR的运行时，和一组类库，并逐渐实现了  ADO.NET、ASP.NET、WinForm、Silverlight（可惜没有实现强大的WPF），能够使得开发人员在其他平台用C#开发程序。



### 3.	.NET 运行时

运行时是用于托管程序的执行环境。 操作系统属于运行时环境，但不属于 .NET 运行时。 下面是 .NET 运行时的一些示例：

- .NET Framework 公共语言运行时 (CLR)
- .NET Core 核心公共语言运行时 (CoreCLR)
- 用于 Xamarin.iOS、Xamarin.Android、Xamarin.Mac 和 Mono 桌面框架的 Mono 运行时



### 4.	.NET 工具和常见基础结构

可访问一整套适用于每种 .NET 实现的工具和基础结构组件。 这些工具和组件包括：

- .NET 语言及其编译器
- .NET 项目系统（基于 .csproj  .vbproj  和 .fsproj  文件）
- [MSBuild](https://docs.microsoft.com/zh-cn/visualstudio/msbuild/msbuild)（用于生成项目的生成引擎）
- [NuGet](https://docs.microsoft.com/zh-cn/nuget/)（适用于.NET 的 Microsoft 程序包管理器）
- 开放源生成业务流程工具，例如 [CAKE](https://cakebuild.net/) 和 [FAKE](https://fake.build/)



### 5.	C# 和 .NET 的关系

C#就其本身而言只是一种语言，尽管它是用于生成面向.NET环境的代码，但它本身不是.NET的一部分。.NET 支持的一些特性，C#并不支持。而C#语言支持的另一些特性，.NET却不支持。

C# 只是一种在 .NET 开发平台上使用的编程语言，目前能在 .NET 平台上使用的开发语言很多，例如 Visual Basic .NET、[Python](http://c.biancheng.net/python/)、J#、Visual C++.NET 等。





## .NET 实现



### 跨语言互操作性

语言互操作性是一种代码与使用其他编程语言编写的另一种代码进行交互的能力。语言互操作性可以有助于最大程度地提高代码的重复使用率，从而提高开发过程的效率。

因为开发人员使用多种工具和技术，而每一种工具和技术都支持不同的功能和类型，这就形成了确保语言互操作性较为困难的历史根源。但是，面向公共语言运行库的语言编译器和工具却受益于运行库的内置语言互操作性支持。

公共语言运行库通过指定和强制公共类型系统以及提供元数据为语言互操作性提供了必要的基础。因为所有面向运行库的语言都遵循[通用类型系统](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/zcx1eb1e(v=vs.90))规则来定义和使用类型，类型的用法在各种语言之间是一致的。[元数据](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/xcd8txaw(v=vs.90))通过定义统一的存储和检索类型信息的机制使语言互操作性成为可能。编译器将类型信息存储为元数据，公共语言运行库使用该信息在执行过程中提供服务；因为所有类型信息都以相同的方式存储和检索，而与编写该代码的语言无关，所以运行库可以***管理多语言应用程序的执行***。

交由运行时管理执行的过程即为托管，在这种情况下，相关的运行时称为公共语言运行时，不管使用的是哪种实现（[Mono](https://www.mono-project.com/)、.NET Framework 或.NET Core）。托管代码就是执行过程交由运行时管理的代码。托管代码具有许多优点，例如：跨语言集成、跨语言异常处理、增强的安全性、版本控制和部署支持、简化的组件交互模型、调试和分析服务等。CLR 负责提取托管代码，将其编译成机器代码，然后执行它。 除此之外，运行时还提供多个重要服务，例如自动内存管理、安全边界、类型安全，等等。相反，如果运行 C/C++ 程序，则运行的代码也称为“非托管代码”。 在非托管环境中，程序员需要亲自负责处理相当多的事情。 实际的程序在本质上是操作系统 (OS) 载入内存，然后启动的二进制代码。 其他任何工作 - 从内存管理到安全考虑因素 - 对于程序员来说是一个不小的负担。

托管执行过程包括下列步骤：

1. [选择编译器](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/cds9hbbb(v=vs.90))。

   为获得公共语言运行库提供的优点，必须使用一个或多个针对运行库的语言编译器。

2. 将代码编译为 [Microsoft 中间语言 (MSIL)](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/c5tkafs1(v=vs.90))。

   编译将源代码翻译为 MSIL 并生成所需的元数据。

3. [将 MSIL 编译为本机代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/ht8ecch6(v=vs.90))。

   在执行时，实时 (JIT) 编译器将 MSIL 翻译为本机代码。在此编译过程中，代码必须通过验证过程，该过程检查 MSIL 和元数据以查看是否可以将代码确定为类型安全。

4. [运行代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/8t3521k6(v=vs.90))。

   公共语言运行库提供使执行能够发生以及可在执行期间使用的各种服务的结构。

自动内存管理是公共语言运行库在[托管执行过程](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/k5532s8a(v=vs.90))过程中提供的服务之一。公共语言运行库的垃圾回收器为应用程序管理内存的分配和释放。对开发人员而言，这就意味着在开发托管应用程序时不必编写执行内存管理任务的代码。









CLI（公共语言基础结构Common Language Infrastructure）

CTS（通用类型系统Common Type System）

CLS（公共语言规范Common Language Specification）

CLR（公共语言运行库Common Language Runtime）

CIL（公共中间语言Common Intermediate Language）



### 1.	公共语言



#### 1.1 CLI

CLI不是某种代码库或者程序，它是一项国际性的标准，全名是公共语言基础结构（Common Language Infrastructure），它是一系列规范的总称。CLI定义了一个语言无关的跨体系结构的运行环境，这使得开发者可以用规范内定义的各种高级语言来开发软件，实现多语言的互操作性。

CLI包含的规范有：

- 虚拟执行系统（VES）
- 公共中间语言（CIL）
- 公共类型系统（Common Type System，CTS）
- 公共语言规范（Common Language Specification，CLS）
- 元数据（Metadata）
- 框架（Framework）

CLI不是特定为C#服务的，它这套标准可以应用于多种语言，开发者可以依据CLI的规范实现各种编译平台并应用于多种语言和多种操作系统中。



#### 1.2	CTS

通用类型系统定义了如何在运行库中声明、使用和管理类型，同时也是运行库支持跨语言集成的一个重要组成部分。通用类型系统执行以下功能：

- 建立一个支持跨语言集成、类型安全和高性能代码执行的框架。
- 提供一个支持完整实现多种编程语言的面向对象的模型。
- 定义各语言必须遵守的规则，有助于确保用不同语言编写的对象能够交互作用。
- 提供包含应用程序开发中使用的基元数据类型（如[Boolean](https://msdn.microsoft.com/zh-cn/library/a28wyd50(v=vs.100))、[Byte](https://msdn.microsoft.com/zh-cn/library/yyb1w04y(v=vs.100))、[Char](https://msdn.microsoft.com/zh-cn/library/k493b04s(v=vs.100))、[Int32](https://msdn.microsoft.com/zh-cn/library/td2s409d(v=vs.100)) 和 [UInt64](https://msdn.microsoft.com/zh-cn/library/06cf7918(v=vs.100))）的库。



#### 1.3	CLS

要和其他对象完全交互，而不管这些对象是以何种语言实现的，对象必须只向调用方公开那些它们必须与之互用的所有语言的通用功能。 为此定义了公共语言规范 (CLS)，它是许多应用程序所需的一套基本语言功能。 CLS 规则定义了[常规类型系统](https://docs.microsoft.com/zh-cn/previous-versions/dotnet/netframework-4.0/zcx1eb1e(v=vs.100))的子集，即所有适用于常规类型系统的规则都适用于 CLS，除非 CLS 中定义了更严格的规则。 CLS 通过定义一组开发人员可以确信在多种语言中都可用的功能来增强和确保语言互用性。 CLS  还建立了 CLS 遵从性要求，这帮助您确定您的托管代码是否符合 CLS 以及一个给定的工具对托管代码（该代码是使用 CLS  功能的）开发的支持程度。

如果您的组件在对其他代码（包括派生类）公开的 API 中只使用了 CLS 功能，那么可以保证在任何支持 CLS 的编程语言中都可以访问该组件。 遵守 CLS 规则、仅使用 CLS 中所包含功能的组件叫做符合 CLS 的组件。

CLS 在设计上足够大，可以包括开发人员经常需要的语言构造；同时也足够小，大多数语言都可以支持它。 此外，任何不可能快速验证代码类型安全性的语言构造都被排除在 CLS 之外，以便所有符合 CLS 的语言都可以生成可验证的代码（如果它们选择这样做）。

#### BCL，基础类库（Base Class Library）

BCL是一个公共编程框架，称为基类库，所有语言的开发者都能利用它。是CLI（Common Language  Infrastructure，公共语言基础结构）的规范之一，主要包括：执行网络操作，执行I/O操作，安全管理，文本操作，数据库操作，XML操作，与事件日志交互，跟踪和一些诊断操作，使用非托管代码，创建与调用动态代码等，粒度相对较小，为所有框架提供基础支持。

#### FCL，框架类库（Framework Class Library）

FCL提供了大粒度的编程框架，它是针对不同应用设计的框架 ，FCL大部分实现都引用了BCL，例如我们常说的开发框架：ASP.NET、MVC、WCF和WPF等等，提供了针对不同层面的编程框架 。

## .NET Framework

![ .NET Framework的体系结构](http://c.biancheng.net/uploads/allimg/190313/4-1Z3131IF54N.gif)





# C#概述



## 程序结构

C# 中的关键组织结构概念包括***程序***、***命名空间***、***类型***、***成员***和***程序集***。 C# 程序由一个或多个源文件组成。 程序声明类型，而类型则包含成员，并被整理到命名空间中。 类型示例包括类和接口。 成员示例包括字段、方法、属性和事件。 编译完的 C# 程序实际上会打包到程序集中。 程序集的文件扩展名通常为 `.exe` 或 `.dll`，具体取决于实现的是***应用程序***还是***库***。（这里的**程序**即对应一个VS的项目）

程序集包含中间语言 (IL) 指令形式的可执行代码和元数据形式的符号信息。 执行前，.NET 公共语言运行时的实时 (JIT) 编译器会将程序集中的 IL 代码转换为特定于处理器的代码。

由于程序集是包含代码和元数据的自描述功能单元，因此无需在 C# 中使用 `#include` 指令和头文件。 只需在编译程序时引用特定的程序集，即可在 C# 程序中使用此程序集中包含的公共类型和成员。

使用 C#，可以将程序的源文本存储在多个源文件中。 编译多文件 C# 程序时，可以将所有源文件一起处理，并且源文件可以随意相互引用。从概念上讲，就像是所有源文件在处理前被集中到一个大文件中一样。 在 C# 中永远都不需要使用前向声明，因为声明顺序无关紧要（极少数例外情况除外）。 C# 并不限制源文件只能声明一种公共类型，也不要求源文件的文件名必须与其中声明的类型相匹配。

> 1）、不需要前向声明
>
> 2）、一个文件里可以放多个类
>
> 3）、文件名可以和文件里声明的类型名不一致



## 类型和变量

C# 有两种类型：*值类型*和*引用类型*。 值类型的变量直接包含数据，而引用类型的变量则存储对数据（称为“对象”）的引用。 对于引用类型，两个变量可以引用同一对象；因此，对一个变量执行的运算可能会影响另一个变量引用的对象。 借助值类型，每个变量都有自己的数据副本；因此，对一个变量执行的运算不会影响另一个变量（`ref` 和 `out` 参数变量除外）。

**以下大纲概述了 C# 的类型系统**

> - [值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/value-types)
>   - [简单类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/value-types#built-in-value-types)
>     - 有符号的整型：`sbyte`、`short`、`int`、`long`
>     - 无符号的整型：`byte`、`ushort`、`uint`、`ulong`
>     - Unicode 字符：`char`
>     - IEEE 二进制浮点：`float`、`double`
>     - 高精度十进制浮点数：`decimal`
>     - 布尔：`bool`
>   - [枚举类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/enum)
>     - 格式为 `enum E {...}` 的用户定义类型
>   - [结构类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/struct)
>     - 格式为 `struct S {...}` 的用户定义类型
>   - [可以为 null 的值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/nullable-value-types)
>     - 值为 `null` 的其他所有值类型的扩展
>   - [元组值类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/value-tuples)
>     - 格式为 `(T1, T2, ...)` 的用户定义类型
> - [引用类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/reference-types)
>   - [类类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/class)
>     - 其他所有类型的最终基类：`object`
>     - Unicode 字符串：`string`
>     - 格式为 `class C {...}` 的用户定义类型
>   - [接口类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/interface)
>     - 格式为 `interface I {...}` 的用户定义类型
>   - [数组类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/arrays/)
>     - 一维和多维，例如 `int[]` 和 `int[,]`
>   - [委托类型](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/delegate)
>     - 格式为 `delegate int D(...)` 的用户定义类型

**数据类型概述**

C# 的 `bool` 类型用于表示布尔值（`true` 或 `false`）。

C# 使用 Unicode 编码处理字符和字符串。 `char` 类型表示 UTF-16 代码单元，`string` 类型表示一系列 UTF-16 代码单元。

C# 程序使用*类型声明*创建新类型。 类型声明指定新类型的名称和成员。 用户可定义以下五种 C# 类型：类类型、结构类型、接口类型、枚举类型和委托类型。

`class` 类型定义包含数据成员（字段）和函数成员（方法、属性及其他）的数据结构。 类类型支持单一继承和多态，即派生类可以扩展和专门针对基类的机制。

`struct` 类型定义包含数据成员和函数成员的结构，这一点与类类型相似。 不过，与类不同的是，结构是值类型，通常不需要进行堆分配。 结构类型不支持用户指定的继承，并且所有结构类型均隐式继承自类型 `object`。

`interface` 类型将协定定义为一组已命名的公共函数成员。 实现 `interface` 的 `class` 或 `struct` 必须提供接口函数成员的实现代码。 `interface` 可以继承自多个基接口，`class` 和 `struct` 可以实现多个接口。

`delegate` 类型表示引用包含特定参数列表和返回类型的方法。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托类同于函数式语言提供的函数类型。 它们还类似于其他一些语言中存在的“函数指针”概念。 与函数指针不同，委托是面向对象且类型安全的。

`class`、`struct`、`interface` 和 `delegate` 类型全部都支持泛型，因此可以使用其他类型对它们进行参数化。

`enum` 类型是一种包含已命名常量的独特类型。 每个 `enum` 类型都有一个基础类型（必须是八种整型类型之一）。 `enum` 类型的值集与基础类型的值集相同。

C# 支持任意类型的一维和多维数组。 与上述类型不同，数组类型无需先声明即可使用。 相反，数组类型是通过在类型名称后面添加方括号构造而成。 例如，`int[]` 是 `int` 类型的一维数组，`int[,]` 是 `int` 类型的二维数组，`int[][]` 是由 `int` 类型的一维数组构成的一维数组。

可以为 null 的值类型也无需先声明即可使用。 对于所有不可以为 null 的值类型 `T`，都有对应的可以为 null 的值类型 `T?`，后者可以包含附加值 `null`。 例如，`int?` 是可以包含任何 32 位整数或值 `null` 的类型。

C# 采用统一的类型系统，因此任意类型的值都可视为 `object`。 每种 C# 类型都直接或间接地派生自 `object` 类类型，而 `object` 是所有类型的最终基类。 只需将值视为类型 `object`，即可将引用类型的值视为对象。 通过执行*装箱* 和*拆箱* 操作，可以将值类型的值视为对象。 在以下示例中，`int` 值被转换成 `object`，然后又恢复成 `int`。

```csharp
using System;
class BoxingExample
{
    static void Main()
    {
        int i = 123;
        object o = i;    // Boxing
        int j = (int)o;  // Unboxing
    }
}
```

将值类型的值分配给 `object` 对象引用时，会分配一个“箱”来保存此值。 该箱是引用类型的实例，此值会被复制到该箱。 相反，当 `object` 引用被显式转换成值类型时，将检查引用的 `object` 是否是具有正确值类型的箱。 如果检查成功，则会将箱中的值复制到值类型。

C# 的统一类型系统实际上意味着“按需”将值类型视为 `object` 引用。 鉴于这种统一性，使用类型 `object` 的常规用途库可以与派生自 `object` 的所有类型结合使用，包括引用类型和值类型。

> 装箱和拆箱操作
>
> 



**C#变量**

C# 有多种*变量*，其中包括字段、数组元素、局部变量和参数。 变量表示存储位置，每个变量都具有一种类型，用于确定可以在变量中存储哪些值。

> 如下文所述。
>
> - 不可以为 null 的值类型
>   - 具有精确类型的值
> - 可以为 null 的值类型
>   - `null` 值或具有精确类型的值
> - object
>   - `null` 引用、对任意引用类型的对象的引用，或对任意值类型的装箱值的引用
> - 类类型
>   - `null` 引用、对类类型实例的引用，或对派生自类类型的类实例的引用
> - 接口类型
>   - `null` 引用、对实现接口类型的类类型实例的引用，或对实现接口类型的值类型的装箱值的引用
> - 数组类型
>   - `null` 引用、对数组类型实例的引用，或对兼容的数组类型实例的引用
> - 委托类型
>   - `null` 引用或对兼容的委托类型实例的引用



## 表达式

*表达式*是在*操作数*和*运算符*的基础之上构造而成。 表达式的运算符指明了向操作数应用的运算。 运算符的示例包括 `+`、`-`、`*`、`/` 和 `new`。 操作数的示例包括文本、字段、局部变量和表达式。

如果表达式包含多个运算符，那么运算符的*优先级*决定了各个运算符的计算顺序。 例如，表达式 `x + y * z` 相当于计算 `x + (y * z)`，因为 `*` 运算符的优先级高于 `+` 运算符。

如果操作数两边的两个运算符的优先级相同，那么运算符的*结合性*决定了运算的执行顺序：

- 除了赋值运算符和 null 合并运算符之外，所有二元运算符均为左结合  运算符，即从左向右执行运算。 例如， `x + y + z` 将计算为 `(x + y) + z`。
- 赋值运算符、null 合并 `??` 和 `??=` 运算符和条件运算符 `?:` 为右结合  运算符，即从右向左执行运算。 例如， `x = y = z` 将计算为 `x = (y = z)`。

可以使用括号控制优先级和结合性。 例如，`x + y * z` 先计算 `y` 乘 `z`，并将结果与 `x` 相加，而 `(x + y) * z` 则先计算 `x` 加 `y`，然后将结果与 `z` 相乘。

大部分运算符可[*重载*](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/operator-overloading)。 借助运算符重载，可以为一个或两个操作数为用户定义类或结构类型的运算指定用户定义运算符实现代码。



## 语句

程序操作使用*语句*进行表示。 C# 支持几种不同的语句，其中许多语句是从嵌入语句的角度来定义的。

使用*代码块*，可以在允许编写一个语句的上下文中编写多个语句。 代码块是由一系列在分隔符 `{` 和 `}` 内编写的语句组成。

**语句类型**

* *声明语句*用于声明局部变量和常量。
* *表达式语句*用于计算表达式。 可用作语句的表达式包括方法调用、使用 `new` 运算符的对象分配、使用 `=` 和复合赋值运算符的赋值、使用 `++` 和 `--` 运算符和 `await` 表达式的递增和递减运算。
* *选择语句*用于根据一些表达式的值从多个可能的语句中选择一个以供执行。 此组包含 `if` 和 `switch` 语句。
* *迭代语句*用于重复执行嵌入语句。 此组包含 `while`、`do`、`for` 和 `foreach` 语句。
* *跳转语句*用于转移控制权。 此组包含 `break`、`continue`、`goto`、`throw`、`return` 和 `yield` 语句。
* `try`...`catch` 语句用于捕获在代码块执行期间发生的异常，`try`...`finally` 语句用于指定始终执行的最终代码，无论异常发生与否。
* `checked` 和 `unchecked` 语句用于控制整型类型算术运算和转换的溢出检查上下文。
* `lock` 语句用于获取给定对象的相互排斥锁定，执行语句，然后解除锁定。
* `using` 语句用于获取资源，执行语句，然后释放资源。



下面列出了可以使用的各种语句，以及每种语句的示例。

- 局部变量声明：

```csharp
static void Declarations(string[] args)
{
    int a;
    int b = 2, c = 3;
    a = 1;
    Console.WriteLine(a + b + c);
}
```

- 局部常量声明：

```csharp
static void ConstantDeclarations(string[] args)
{
    const float pi = 3.1415927f;
    const int r = 25;
    Console.WriteLine(pi * r * r);
}
```

- 表达式语句：

```csharp
static void Expressions(string[] args)
{
    int i;
    i = 123;                // Expression statement
    Console.WriteLine(i);   // Expression statement
    i++;                    // Expression statement
    Console.WriteLine(i);   // Expression statement
}
```

- `if` 语句：

```csharp
static void IfStatement(string[] args)
{
    if (args.Length == 0)
    {
        Console.WriteLine("No arguments");
    }
    else
    {
        Console.WriteLine("One or more arguments");
    }
}
```

- `switch` 语句：

```csharp
static void SwitchStatement(string[] args)
{
    int n = args.Length;
    switch (n)
    {
        case 0:
            Console.WriteLine("No arguments");
            break;
        case 1:
            Console.WriteLine("One argument");
            break;
        default:
            Console.WriteLine($"{n} arguments");
            break;
    }
}
```

- `while` 语句：

```csharp
static void WhileStatement(string[] args)
{
    int i = 0;
    while (i < args.Length)
    {
        Console.WriteLine(args[i]);
        i++;
    }
}
```

- `do` 语句：

```csharp
static void DoStatement(string[] args)
{
    string s;
    do
    {
        s = Console.ReadLine();
        Console.WriteLine(s);
    } while (!string.IsNullOrEmpty(s));
}
```

- `for` 语句：

```csharp
static void ForStatement(string[] args)
{
    for (int i = 0; i < args.Length; i++)
    {
        Console.WriteLine(args[i]);
    }
}
```

- `foreach` 语句：

```csharp
static void ForEachStatement(string[] args)
{
    foreach (string s in args)
    {
        Console.WriteLine(s);
    }
}
```

- `break` 语句：

```csharp
static void BreakStatement(string[] args)
{
    while (true)
    {
        string s = Console.ReadLine();
        if (string.IsNullOrEmpty(s))
            break;
        Console.WriteLine(s);
    }
}
```

- `continue` 语句：

```csharp
static void ContinueStatement(string[] args)
{
    for (int i = 0; i < args.Length; i++)
    {
        if (args[i].StartsWith("/"))
            continue;
        Console.WriteLine(args[i]);
    }
}
```

- `goto` 语句：

```csharp
static void GoToStatement(string[] args)
{
    int i = 0;
    goto check;
    loop:
    Console.WriteLine(args[i++]);
    check:
    if (i < args.Length)
        goto loop;
}
```

- `return` 语句：

```csharp
static int Add(int a, int b)
{
    return a + b;
}
static void ReturnStatement(string[] args)
{
   Console.WriteLine(Add(1, 2));
   return;
}
```

- `yield` 语句：

```csharp
static System.Collections.Generic.IEnumerable<int> Range(int start, int end)
{
    for (int i = start; i < end; i++)
    {
        yield return i;
    }
    yield break;
}
static void YieldStatement(string[] args)
{
    foreach (int i in Range(-10,10))
    {
        Console.WriteLine(i);
    }
}
```

- `throw` 和 `try` 语句：

```csharp
static double Divide(double x, double y)
{
    if (y == 0)
        throw new DivideByZeroException();
    return x / y;
}
static void TryCatch(string[] args)
{
    try
    {
        if (args.Length != 2)
        {
            throw new InvalidOperationException("Two numbers required");
        }
        double x = double.Parse(args[0]);
        double y = double.Parse(args[1]);
        Console.WriteLine(Divide(x, y));
    }
    catch (InvalidOperationException e)
    {
        Console.WriteLine(e.Message);
    }
    finally
    {
        Console.WriteLine("Good bye!");
    }
}
```

- `checked` 和 `unchecked` 语句：

```csharp
static void CheckedUnchecked(string[] args)
{
    int x = int.MaxValue;
    unchecked
    {
        Console.WriteLine(x + 1);  // Overflow
    }
    checked
    {
        Console.WriteLine(x + 1);  // Exception
    }
}
```

- `lock` 语句：

```csharp
class Account
{
    decimal balance;
    private readonly object sync = new object();
    public void Withdraw(decimal amount)
    {
        lock (sync)
        {
            if (amount > balance)
            {
                throw new Exception(
                    "Insufficient funds");
            }
            balance -= amount;
        }
    }
}
```

- `using` 语句：

```csharp
static void UsingStatement(string[] args)
{
    using (TextWriter w = File.CreateText("test.txt"))
    {
        w.WriteLine("Line one");
        w.WriteLine("Line two");
        w.WriteLine("Line three");
    }
}
```



## 类和对象

*类*是最基本的 C# 类型。 类是一种数据结构，可在一个单元中就将状态（字段）和操作（方法和其他函数成员）结合起来。 类为动态创建的类*实例*（亦称为“*对象*”）提供了定义。 类支持*继承*和*多态*，即*派生类*可以扩展和专门针对*基类*的机制。

类实例是使用 `new` 运算符进行创建，此运算符为新实例分配内存，调用构造函数来初始化实例，并返回对实例的引用。 以下语句创建两个 Point 对象，并将对这些对象的引用存储在两个变量中：

```csharp
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```

当无法再访问对象时，对象占用的内存会被自动回收。 既没必要，也无法在 C# 中显式解除分配对象。



## 数组

***数组***是一种数据结构，其中包含许多通过计算索引访问的变量。 数组中的变量（亦称为数组的***元素***）均为同一种类型，我们将这种类型称为数组的***元素类型***。

数组类型是引用类型，声明数组变量只是为引用数组实例预留空间。 实际的数组实例是在运行时使用 new 运算符动态创建而成。 new 运算指定了新数组实例的***长度***，然后在此实例的生存期内固定使用这个长度。 数组元素的索引介于 `0` 到 `Length - 1` 之间。 `new` 运算符自动将数组元素初始化为其默认值（例如，所有数值类型的默认值为 0，所有引用类型的默认值为 `null`）。

 C# 还支持***多维数组***。 数组类型的维数（亦称为数组类型的***秩***）。以下示例分别分配一维、二维、三维数组。

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```



## 接口

***接口***定义了可由类和结构实现的协定。 接口可以包含方法、属性、事件和索引器。 接口不提供所定义成员的实现，仅指定必须由实现接口的类或结构提供的成员。

接口可以采用***多重继承***。

```csharp
interface IControl
{
    void Paint();
}
interface ITextBox: IControl
{
    void SetText(string text);
}
interface IListBox: IControl
{
    void SetItems(string[] items);
}
interface IComboBox: ITextBox, IListBox {}
```

类和结构可以实现多个接口。 

```csharp
interface IDataBound
{
    void Bind(Binder b);
}
public class EditBox: IControl, IDataBound
{
    public void Paint() { }
    public void Bind(Binder b) { }
}
```

当类或结构实现特定接口时，此类或结构的实例可以隐式转换成相应的接口类型。 例如

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```

也可以使用动态类型显式转换功能。

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```

C# 还支持显式***接口成员实现代码***，这样类或结构就不会将成员设为公共成员。 显式接口成员实现代码是使用完全限定的接口成员名称进行编写。显式接口成员只能通过接口类型进行访问。

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() { }
    void IDataBound.Bind(Binder b) { }
}
```

```csharp
EditBox editBox = new EditBox();
editBox.Paint();            // Error, no such method
IControl control = editBox;
control.Paint();            // Ok
```





## 委托

***委托类型***表示对具有特定参数列表和返回类型的方法的引用。 通过委托，可以将方法视为可分配给变量并可作为参数传递的实体。 委托还类似于其他一些语言中存在的“函数指针”概念。 与函数指针不同，委托是面向对象且类型安全的。

委托不知道也不关心所引用的方法的类；只关心引用的方法是否具有与委托相同的参数和返回类型。





## 特性

C# 可以将用户定义类型的声明性信息附加到程序实体，并在运行时检索此类信息。 程序通过定义和使用***特性***来指定此类额外的声明性信息。









# C#编程指南























C# 程序可由一个或多个文件组成。 每个文件均可包含零个或多个命名空间。 一个命名空间可包含类、结构、接口、枚举、委托等类型以及其他命名空间。 下面是包含所有这些元素的 C# 程序主干。

```csharp
// A skeleton of a C# program
using System;
namespace YourNamespace
{
    class YourClass
    {
    }

    struct YourStruct
    {
    }

    interface IYourInterface
    {
    }

    delegate int YourDelegate();

    enum YourEnum
    {
    }

    namespace YourNestedNamespace
    {
        struct YourStruct
        {
        }
    }

    class YourMainClass
    {
        static void Main(string[] args)
        {
            //Your program starts here...
        }
    }
}
```