# Robot Framework

# 1.1	开始

### robot framework概述

Robot Framework is a Python-based, extensible keyword-driven automation framework for acceptance testing, acceptance test driven development (ATDD), behavior driven development (BDD) and robotic process automation (RPA). 

The framework has a rich ecosystem around it consisting of various generic libraries and tools that are developed as separate projects. 

Robot Framework is open source software released under the [Apache License 2.0](http://apache.org/licenses/LICENSE-2.0).

![](http://robotframework.org/robotframework/latest/images/architecture.png)

The [test data](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#creating-test-data) is in simple, easy-to-edit tabular format. When Robot Framework is started, it processes the data, [executes test cases](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#id173) and generates logs and reports. The core framework does not know anything about the target under test, and the interaction with it is handled by [libraries](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#creating-test-libraries). Libraries can either use application interfaces directly or use lower level test tools as drivers.



### 安装Robot Framework

Robot Framework is supported on [Python](http://python.org) (both Python 2 and Python 3), [Jython](http://jython.org) (JVM) and [IronPython](http://ironpython.net) (.NET) and [PyPy](http://pypy.org). The interpreter you want to use should be installed before installing the framework itself.

Which interpreter to use depends on the needed test libraries and test environment in general. Some libraries use tools or modules that only work with Python, while others may use Java tools that require Jython or need .NET and thus IronPython. There are also many tools and libraries that run fine with all interpreters.

[IronPython](http://ironpython.net) allows running Robot Framework on the [.NET platform](http://www.microsoft.com/net) and interacting with C# and other .NET languages and APIs. Only IronPython 2.7 is supported in general and IronPython 2.7.9 or newer is highly recommended.

* 安装Python2.7及其pip

* 配置pip源和安装robot framework

  ```
  1）、创建 C:\Users\{user-name}\pip\pip.ini
  [global]
  index-url=https://pypi.tuna.tsinghua.edu.cn/simple 
  [install]  
  trusted-host=pypi.tuna.tsinghua.edu.cn
  disable-pip-version-check = true  
  timeout = 6000 
  
  2）、安装package时设置源
  pip install package_name -i https://pypi.tuna.tsinghua.edu.cn/simple
  
  
  卸载
  pip uninstall robotframework
  
  升级
  # Upgrade to the latest stable version. This is the most common method.
  pip install --upgrade robotframework
  
  # Upgrade to the latest version even if it would be a preview release.
  pip install --upgrade --pre robotframework
  
  # Upgrade to the specified version.
  pip install robotframework==2.9.2
  
  ```

* 验证安装

  ```
  $ robot --version
  Robot Framework 3.0 (Python 2.7.10 on linux2)
  
  $ rebot --version
  Rebot 3.0 (Python 2.7.10 on linux2)
  ```

* docutils

  ```
  pip install docutils
  ```

  

* pip安装ride

  ```
  pip install robotframework-ride -i https://pypi.tuna.tsinghua.edu.cn/simple
  ```





## 1.2	示范

There are several demo projects that introduce Robot Framework and help getting started with it.

- [Quick Start Guide](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst)

  Introduces the most important features of Robot Framework and acts as an executable demo.

- [Robot Framework demo](https://github.com/robotframework/RobotDemo)

  Simple example test cases. Demonstrates also creating custom test libraries.

- [Web testing demo](https://github.com/robotframework/WebDemo)

  Demonstrates how to create tests and higher level keywords. The system under test is a simple web page that is tested using [SeleniumLibrary](https://github.com/robotframework/SeleniumLibrary).

- [SwingLibrary demo](https://github.com/robotframework/SwingLibrary/wiki/SwingLibrary-Demo)

  Demonstrates using [SwingLibrary](https://github.com/robotframework/SwingLibrary) for testing Java GUI applications.

- [ATDD with Robot Framework](https://code.google.com/p/atdd-with-robot-framework)

  Demonstrates how to use Robot Framework when following Acceptance Test Driven Development (ATDD) process.



## [Keywords](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst#id25)

Test cases are created from keywords that can come from two sources. [Library keywords](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst#library-keywords) come from imported test libraries, and so called [user keywords](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst#user-keywords) can be created using the same tabular syntax that is used for creating test cases.

### [Library keywords](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst#id26)

All lowest level keywords are defined in test libraries which are implemented using standard programming languages, typically Python or Java. Robot Framework comes with a handful of [test libraries](http://robotframework.org/#libraries) that can be divided to *standard libraries*, *external libraries* and *custom libraries*. [Standard libraries](http://robotframework.org/robotframework/#standard-libraries) are distributed with the core framework and included generic libraries such as `OperatingSystem`, `Screenshot` and `BuiltIn`, which is special because its keywords are available automatically. External libraries, such as [Selenium2Library](https://github.com/rtomac/robotframework-selenium2library/#readme) for web testing, must be installed separately. If available test libraries are not enough, it is easy to [create custom test libraries](https://github.com/robotframework/QuickStartGuide/blob/master/QuickStart.rst#creating-test-libraries).



# 创建测试库



#### [Supported programming languages](http://robotframework.org/robotframework/latest/RobotFrameworkUserGuide.html#id810)

Robot Framework itself is written with [Python](http://python.org) and naturally test libraries extending it can be implemented using the same language. When running the framework on [Jython](http://jython.org), libraries can also be implemented using [Java](http://java.com). Pure Python code works both on Python and Jython, assuming that it does not use syntax or modules that are not available on Jython. When using Python, it is also possible to implement libraries with C using [Python C API](http://docs.python.org/c-api/index.html), although it is often easier to interact with C code from Python libraries using [ctypes](http://docs.python.org/library/ctypes.html) module.







# 测试

Robot Framework 中的测试用例通过命令行执行, 执行的结果默认生成一个XML格式的 [输出文件(Output.xml)](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/OutputFiles.html#output-file) 和HTML格式的 report and log. 执行完毕后, 这些输出文件可以通过Rebot工具整合或者进行 [后期处理](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/PostProcessing.html#post-processing-outputs).



## 开始执行测试

```
robot [options] data_sources
python|jython|ipy -m robot [options] data_sources
python|jython|ipy path/to/robot/ [options] data_sources
java -jar robotframework.jar [options] data_sources
```



### 指定待执行的测试数据

Robot Framework 中的测试用例是通过 [文件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#test-case-files) 和 [目录](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#test-suite-directories) 的方式创建和组织的, 所以要执行时把这些文件或目录的路径传给执行脚本就可以了. 

指定的文件或者目录将被用来创建顶层测试套件, 除非通过命令行选项 `--name` [设置名字](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/ConfiguringExecution.html#setting-the-name), 否则这个测试套件的名字也就是 [文件或者目录名](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#test-suite-name-and-documentation). 还可以一次给出多个测试用例文件或目录, 之间用空格隔开. 这种情况下, Robot Framework自动创建顶层测试套件,  这些指定的文件和目录都成为它的子套件. 这个顶层的测试套件的名字由各子套件的名字使用 `` & `` 拼接而成. 例如,  下面的例子中的顶层套件的名字是 *My Tests & Your Tests*. 可以想见这个自动创建的名字将会非常冗长, 所以大多数情况下, 最好还是通过 `--name` 命令行选项来指定一个名字, 如下面的第二个例子:

```
robot my_tests.robot your_tests.robot
robot --name Example path/to/tests/pattern_*.robot
```



### 命令行选项

#### 短选项和长选项

选项总是有一个较长的名字, 如 `--name`, 最常用的那些选项同时还有一个短名字, 例如 `-N`. 此外, 长选项名称可以不用写全, 只要给出的部分是唯一无歧义的即可. 

短选项和截短的选项在手动执行测试用例时都挺实用, 不过在 start-up scripts 中推荐使用长选项名称, 因为它们更易懂.

长选项的格式是大小写无关的, 这有益于写出更易读的选项名字. 

#### 设置选项值

大多数的选项需要在选项名称后面给定一个值. 长选项和短选项都接受在空格后面跟上选项的值, 例如,  `--include tag` 或 `-i tag`. 同时对于长选项, 还可以使用等号(`=`), 例如 `--include=tag`, 而对于短选项, 中间的分隔符则是可用省略的, 如 `-itag`.

有的选项可用被指定多次. 例如, `--variable VAR1:value --variable VAR2:another` 设置了两个变量. 如果一个选项只能接受一个值而被指定了多次, 则生效的将是最后的那个.

#### 禁用不带值得选项

不接受值的选项可用通过在选项名前加上(或去掉)前缀 `no` 来禁用. 最后的那个选项优先级最高.

#### 简单模式









## [测试数据表格](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/TestDataSyntax.html#id43)

测试数据按结构划分有4种类型, 如下表所列. 这些测试数据表格由表格中第一个单元格标示. 4种表格的名称分别是 `Settings`, `Variables`, `Test Cases`, 和 `Keywords`. 匹配时不区分大小写, 同时单数形式如 `Setting` 和 `Test Case` 也可接受.

| Table      | Used for                                                     |
| ---------- | ------------------------------------------------------------ |
| Settings   | 1) 导入 [测试库](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/UsingTestLibraries.html#test-libraries), [资源文件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/ResourceAndVariableFiles.html#resource-files), [变量文件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/ResourceAndVariableFiles.html#variable-files). 2) 为 [创建测试套件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#test-suites) 和 test cases 定义元数据 |
| Variables  | 定义 [变量](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/Variables.html#variables) |
| Test Cases | [创建测试用例](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestCases.html#creating-test-cases) |
| Keywords   | [创建用户关键字](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingUserKeywords.html#creating-user-keywords) |









