# 自动测试



## 自测金字塔

测试金字塔概念由[Mike Cohn](http://www.mountaingoatsoftware.com/)提出，并在其著作[《Succeeding with Agile》](http://www.amazon.com/gp/product/0321579364?ie=UTF8&tag=martinfowlerc-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0321579364)[译注1](http://zyzhang.github.io/blog/2013/04/28/test-pyramid/#MyAnnotation1)中做了详细论述。

* UI层：界面自动化测试。可以看出它的价值最小，所以适当的界面自动化测试是有必要的，但是没必要100%都自动化。
* Service层：接口/服务自动化测试。它的价值居中，覆盖大多数主要的接口是比较合适的。
* Unit层：单元测试。最有价值的测试，不过对于测试人员要求太高，而且开发和测试结对编程才能最好。

![Test Pyramid](http://zyzhang.github.io/assets/image/posts/TestPyramid.jpeg)

我们的公司的自动化测试，其实可以认为是服务和接口的自动化测试。

[![w1lYQg.png](https://s1.ax1x.com/2020/09/09/w1lYQg.png)](https://imgchr.com/i/w1lYQg)



## XIL能够解决什么范围内的问题？

[![w1Uf7F.png](https://s1.ax1x.com/2020/09/09/w1Uf7F.png)](https://imgchr.com/i/w1Uf7F)

HIL技术已经被开发多年而只有少数供应商。这些HIL系统有个很大的特点，就是自动测试软件和测试硬件是强耦合的。因此测试用例直接依赖于所使用的测试硬件。从用户角度来看，“最好的”测试软件并不总是能够与“最好的”测试硬件相结合。

专业技术不能从一个测试平台转移另一个测试平台，这导致了员工额外的培训成本。切换到新的测试技术和新的开发阶段是困难的，因为工具特定的格式和测试硬件的兼容问题。

标准化的主要目标是允许测试用例的重用，并将测试自动化软件和测试硬件进行解耦。因此，相同自动化测试软件的测试用例基于不同的测试硬件系统也可以重用。这将减少将测试硬件集成到测试自动化软件中的工作。

XIL主要分作两个部分：Framework和Testbench。Framework是为了实现测试用例的重用性而和底层测试系统去耦合。Testbench是打平各个底层测试系统的差异性，为Framework提供一个统一的标准化访问。



## 测试用例应该是什么样的？

XIL虽然描述了如何将自动测试工具和底层测试系统解耦，以及实现测试用例的重用性等问题，但是并没有给出测试用例的具体方案。所以测试用例应该是什么样的？这是一个问题。确定了测试用例是什么样子的，基本也就可以确定自动测试软件的发展方向。

对于测试人员而言，他们可能更多地是关注测试目标，同时测试用例应该是能够清晰和简单通俗易懂的方式来明确测试要做的事情。因此我觉得测试用例应该想自然语言一样，分步骤地来明确测试目标。

比如这样：

```
*** Test Cases ***
User can create an account and log in
    Create Valid User    fred    P4ssw0rd
    Attempt to Login with Credentials    fred    P4ssw0rd
    Status Should Be    Logged In
```

以上的例子是以关键字驱动测试的。



## 为什么使用 RobotFramework？

测试用例是以关键字驱动来编写的文本，那么如何组织和测试，这需要一套标准。最好这套标准能够被广泛应用。

Robot Framework是一个通用的，应用和技术无关的框架。它是一个基于Python的、可扩展的、关键字驱动的测试自动化框架。测试数据([test data](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/TestDataSyntax.html#test-data))使用非常简单、易于编辑的表格格式. Robot Framework会解析测试数据, [执行测试用例](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/BasicUsage.html#executing-test-cases), 并生成日志和报告. 框架本身对测试对象一无所知, 而是通过 [测试库](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExtendingRobotFramework/CreatingTestLibraries.html#creating-test-libraries) 与其交互. 测试库可能是直接使用被测应用程序的接口, 也可以使用其它底层的测试工具作为驱动.它的高度模块化的架构如下图所示：

![../_images/architecture.png](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/_images/architecture.png)

为什么选择Robot Framework

- 表格式的语法简单易用，以统一的方式 [创建测试用例](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestCases.html#creating-test-cases)
- 可以通过现有关键字创建可复用的 [高层关键字](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingUserKeywords.html#creating-user-keywords)
- 提供了直观的HTML格式的 [测试报告](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/OutputFiles.html#report-file) 和 [日志文件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/OutputFiles.html#log-file)
- 作为一个测试平台，是应用无关的
- 提供了 [测试库API](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExtendingRobotFramework/CreatingTestLibraries.html#creating-test-libraries)，可以轻易地使用Python或者Java创建自定义的测试库
- 提供了 [命令行接口](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/BasicUsage.html#executing-test-cases) 和基于XML的 [输出文件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/OutputFiles.html#output-file)，可以与现有框架集成（如持续集成系统）
- 提供了多种测试库支持，如用于web测试的Selenium，Java GUI测试，启动进程，Telnet，SSH等
- 可以创建 [数据驱动的测试用例](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestCases.html#data-driven-style)
- 内置支持 [变量](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/Variables.html#variables)，在不同的环境中特别实用
- 提供 标签 来分类和 [选择测试用例](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/ExecutingTestCases/ConfiguringExecution.html#selecting-test-cases)
- 非常容易与源码控制系统集成，因为 [测试套件](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#creating-test-suites) 就是文件夹和文本文件
- 提供了 [用例级别](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestCases.html#test-setup-and-teardown) 和 [测试套件级别](https://robotframework-userguide-cn.readthedocs.io/zh_CN/latest/CreatingTestData/CreatingTestSuites.html#suite-setup-and-teardown) 的setup和teardown
- 模块化的架构，支持针对不同接口的应用程序创建测试



我以为robotframework不只是一个框架，它也提供了一个测试平台的标准，它确定了测试用例的格式，同时也明确了测试用例的组织和执行等。这些可以直接参照RIDE软件。























![Test Pyramid](http://zyzhang.github.io/assets/image/posts/TestPyramid.jpeg)