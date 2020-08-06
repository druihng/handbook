# 1.	.NET体系结构



## 1.1	.NET 平台

.NET 是一个通用开发平台，支持多种编程语言。.NET实现**公共语言基础结构（CLI）**，它指定与语言无关的运行时环境和语言互操作性，即它提供了一个跨语言的统一编程环境。目前能在 .NET 平台上使用的开发语言很多，例如 Visual Basic .NET、Python、C#、Visual C++.NET 等，而C# 是一种在 .NET 开发平台上使用最多的编程语言。



### 1.1.1	跨语言互操作

**互操作性**（英文：**Interoperability**；中文又称为：**协同工作能力**，**互用性**）作为一种特性，它指的是不同的系统和组织机构之间相互合作，协同工作（即互操作）的能力。[IEEE](https://zh.wikipedia.org/wiki/IEEE)（Institute of Electrical & Electronic Engineers，电气与电子工程师协会）对互操作性做出了如下定义：

> *两个或多个系统或组成部分之间交换信息以及对所交换的信息加以使用的能力*。

**语言互操作性**是一种代码与使用其他编程语言编写的另一种代码进行交互的能力。语言互操作性可以有助于最大程度地提高代码的重复使用率，从而提高开发过程的效率。

因为开发人员使用多种工具和技术，每一种工具和技术都支持不同的功能和类型，这就形成了确保语言互操作性较为困难的历史根源。CLI定义了一个语言无关的跨体系结构的运行环境，这使得开发者可以用**规范内定义**的各种高级语言来开发软件，然后将程序编译成中间语言最后执行，实现多语言的互操作性。

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

交由运行时管理执行的过程称为托管，在这种情况下，相关的运行时称为公共语言运行时，不管使用的是哪种实现（[Mono](https://www.mono-project.com/)、.NET Framework 或.NET Core）。托管代码就是执行过程交由运行时管理的代码。托管代码具有许多优点，例如：跨语言集成、跨语言异常处理、增强的安全性、版本控制和部署支持、简化的组件交互模型、调试和分析服务等。CLR 负责提取托管代码，将其编译成机器代码，然后执行它。 除此之外，运行时还提供多个重要服务，例如自动内存管理、安全边界、类型安全，等等。相反，如果运行 C/C++ 程序，则运行的代码也称为“非托管代码”。 在非托管环境中，程序员需要亲自负责处理相当多的事情。 实际的程序在本质上是操作系统 (OS) 载入内存，然后启动的二进制代码。



#### 托管

托管执行过程包括下列步骤：

1. [选择编译器](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/cds9hbbb(v=vs.90))。

   为获得公共语言运行库提供的优点，必须使用一个或多个针对运行库的语言编译器。

2. 将代码编译为 [Microsoft 中间语言 (MSIL)](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/c5tkafs1(v=vs.90))。

   编译将源代码翻译为 MSIL 并生成所需的元数据。

3. [将 MSIL 编译为本机代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/ht8ecch6(v=vs.90))。

   在执行时，实时 (JIT) 编译器将 MSIL 翻译为本机代码。在此编译过程中，代码必须通过验证过程，该过程检查 MSIL 和元数据以查看是否可以将代码确定为类型安全。

4. [运行代码](https://docs.microsoft.com/zh-cn/previous-versions/visualstudio/visual-studio-2008/8t3521k6(v=vs.90))。

   公共语言运行库提供使执行能够发生以及可在执行期间使用的各种服务的结构。

   


#### 内存管理





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

