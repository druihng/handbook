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







