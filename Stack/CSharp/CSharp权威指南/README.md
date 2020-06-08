# C# 权威指南





## C# 语言和 .NET Framework 简介



### C#语言

C# 是类型安全的面向对象的语言，可帮助开发者生成在 .NET Framework 上运行的各种安全可靠的应用程序



### .NET Framework 平台体系结构

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

