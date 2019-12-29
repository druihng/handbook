# 计算机终端（Computer-Terminal）

[TOC]

***前言***，在学习《Linux命令和Shell脚本编程大全》的第二章时遇到了困难，主要原因是对终端和及其相关的一些计算机概念、计算机发展史的不了解造成的。因此在参考了很多相关资料后，写下这篇文章帮助自己学习和理解，同时让大家来验证它的正确性。

由于人和机器是两个相互独立的实体，当人需要与机器进行交互而使用机器时，必须借助一个人机交互的接口（interface），它主要负责向主机输入信息，并把主机的结果对外输出显示。

> 终端（Terminal），其词汇本身的意义为「终点站；末端；（电路）的端子，线接头」。

> A **computer terminal** is an electronic or electromechanical [hardware](https://en.wikipedia.org/wiki/Computer_hardware) device that is used for entering data into, and displaying or printing data from, a [computer](https://en.wikipedia.org/wiki/Computer) or a [computing](https://en.wikipedia.org/wiki/Computing) system. 
>
> **终端**（英语：Computer terminal），是一台[计算机](https://zh.wikipedia.org/wiki/%E9%9B%BB%E8%85%A6)或者计算机系统，用来让用户输入数据，及显示其计算结果的机器。终端有些是全电子的，也有些是机电的。其又名**终端机**，它与一部独立的[计算机](https://zh.wikipedia.org/wiki/%E9%9B%BB%E8%85%A6)不同。
>
> —— 摘自 Wikipedia



## 1. 计算机终端的发展

很多计算机概念，随着计算机的发展，在历史上不断变化。因此对它们的理解，需要了解相关的计算机发展史，基于此才能正确的理解这些计算机概念。下面我们将介绍计算机终端的发展史，帮助我们理解计算机终端以及与它有关的计算机概念。



##1.1 控制台

早期的计算机，往往带有一个控制面板，这个控制面板具有大量的开和指示灯，它们和主机是一体的。用于操作计算机和显示结果，所以这个控制面板称为控制台。其概念来自于管风琴的控制台。一台电脑通常只能有一个Console，很多时候是电脑主机的一部分，和CPU共享一个机柜。

![Q9x7VA.jpg](https://s2.ax1x.com/2019/11/27/Q9x7VA.jpg)

![Q9xobd.jpg](https://s2.ax1x.com/2019/11/27/Q9xobd.jpg)

> 左边的控制面板是Console，右边的显示屏和键盘组成的是Terminal

思考题：下面红框里的设备是Console还是Terminal？

![Q9xfgO.jpg](https://s2.ax1x.com/2019/11/27/Q9xfgO.jpg)

答案：是Console，上面有显示寄存器状态的指示灯和直接操作寄存器的开关，而且它与电脑主机紧密结合，无法远程操作。

不过随着个人计算机的普及，控制台 (Console) 与终端 (Terminal)  的概念已经逐渐模糊。在现代，我们的键盘与显示器既可以认为是控制台，也可以认为是普通的终端。当你在管理系统时，它们是控制台；当你在做一般的工作时（浏览网页、编辑文档等），它们就是终端。我们自己既是一般用户，也是系统管理员。因此，现在 Console 与 Terminal 基本被看作是同义词。



##1.2 早期终端  tty

个人计算机是上世纪70年代末开始出现的。在此之前，人们只能在公司或大学里使用大型机(mainframe)和小型机(minicomputer)。Unix创始人肯•汤普逊和丹尼斯•里奇使用的PDP-7小型机当年的价格为72000美元，GE-45大型机价格高达1000万美元，这些计算机非常昂贵。Unix 的创始人 Ken Thompson 和 Dennis Ritchie 想让 Unix 成为一个多用户系统。多用户系统就意味着要给每个用户配置一个终端，每个用户都要有一个显示器、一个键盘。但当时所有的计算机设备都非常昂贵。

最后他们找到了价格低廉的 [ASR-33 电传打字机](https://en.wikipedia.org/wiki/Teletype_Model_33)，他们把很多台ASR-33连接到计算机上作为终端，打字机用来输入信息，打印纸输出结果，让每个用户都可以登录并操作主机。就这样，他们创造了计算机历史上第一个真正的多用户操作系统Unix，而电传打字机则成为了第一个Unix终端。

![Q9xIDH.jpg](https://s2.ax1x.com/2019/11/27/Q9xIDH.jpg)

电传打字机 (Teletype / Teletypewriter) 的英文缩写就是 tty，即 tty 这个名称的来源。在下图所示，早期 tty是最流行的终端设备。因此tty就成了终端的统称。Unix 系统为了支持这些电传打字机，就把电传打字机这个硬件设备抽象成位于 `/dev/tty*` 的tty设备文件。

![QdhNFJ.jpg](https://s2.ax1x.com/2019/12/09/QdhNFJ.jpg)



##1.3 字符终端和图形终端

在图形化桌面出现之前，和Unix系统交互的唯一方式就是通过shell提供的**文本命令行界面**(CLI, Command Line Interface)。

CLI只需一个输入文本然后显示文本和低级图形输出的终端（条件），就可以让计算机执行用户操作。因此，在早期，通常一个简单的哑终端就是和Unix系统交互所需要的所有设备了。哑终端（dumb terminal）通常就是通信电缆连接到装有Unix系统主机的显示器和键盘。这个简单的组合提供了向Unix系统输入文本数据和显示文本结果的一条捷径。

DEC 公司在 1978 年制造的 [VT100](https://en.wikipedia.org/wiki/VT100)，由于其设计良好并且是第一批支持 ANSI 转义序列与光标控制的智能终端，获得了空前的成功。VT100 不仅是史上最流行的字符终端，更是成为了字符终端事实上的标准。

![QdhYo4.jpg](https://s2.ax1x.com/2019/12/09/QdhYo4.jpg)

*▲ DEC VT100 终端（图片来源：Flickr - Jason Scott，CC-BY-2.0）*

**字符终端** (Character Terminal) 也叫文本终端 (Text Terminal)，是只能接收和显示文本信息的终端。早期的终端全部是字符终端。字符终端也分为 **哑终端** (Dumb Terminal) 和所谓的 **智能终端** (Intelligent Terminal)，因为后者可以理解转义序列、定位光标和显示位置，比较聪明，而哑终端不行。

**图形终端** (Graphical Terminal) 随着技术的进步也开始出现在公众的视野中。图形终端不但可以接收和显示文本信息，也可以显示图形与图像。著名的图形终端有 [Tektronix 4010](https://en.wikipedia.org/wiki/Tektronix_4010) 系列。

![Q9x5Ke.jpg](https://s2.ax1x.com/2019/11/27/Q9x5Ke.jpg)

▲ 4010终端绘制的图形（图片来源：Wikipedia）



##1.4 终端模拟器 （Terminal Emulator）

随着计算机的进化，我们已经见不到专门的终端硬件了，取而代之的则是键盘、显示器和终端模拟器。

图形界面GUI出现后，那些传统的、不兼容图形接口的命令行程序（比如说 GNU 工具集里的大部分命令），不能直接读取我们的键盘输入，也无法把结果显示在我们的显示器上。

为了兼容这些命令行程序，我们就需要一个程序来模拟传统的终端行为，这个程序即***终端模拟器*** (Terminal Emulator)。

> 严格来讲，Terminal Emulator 的译名应该是「终端仿真器」。

对于那些命令行 (CLI) 程序，终端模拟器会「假装」成一个传统终端设备；而对于现代的图形接口，终端模拟器会「假装」成一个 GUI 程序。一个终端模拟器的标准工作流程是这样的：

1. 捕获你的键盘输入；
2. 将输入发送给命令行程序（程序会认为这是从一个真正的终端设备输入的）；
3. 拿到命令行程序的输出结果（STDOUT 以及 STDERR）；
4. 调用图形接口（比如 X11），将输出结果渲染至显示器。

终端模拟器可以模拟GUI出现之前任何的早期终端——硬件终端（比如EC公司1978年制造的VT100终端，升级后的VT220终端，以及用于IBM大型机的3270终端等）。



##1.5 终端窗口和虚拟控制台 （Terminal Window and Virtual Console）

在上世纪七八十年代，在公司和大学里，一般人们只可以使用一个终端。但有一些重量级人物可以使用很多个终端，因为他们需要在同一时间内使用主机做不同的事，所以在他们的办公桌上会有四五个甚至六七个终端。

现在，我们不需要在桌上摆上这么多个终端。Unix允许用户在自己电脑上使用多个终端，其中有一个是图形终端，其他六个是字符终端。这七个终端使用同一个显示器和键盘。如果我们需要从一个终端切换到另外一个终端，只需按一下快捷键。一般情况下当我们启动Linux系统时，图形界面自动启动。但有一件事你可能不知道，实际上Linux会同时启动七个不同的终端模拟程序。这七个特殊的终端模拟程序叫做**虚拟控制台**。

第一个到第六个虚拟控制台是全屏的字符终端，第七个虚拟控制台是图形终端，用来运行GUI程序。从图形终端切换到字符终端，我们只需按快捷键CTRL+ALT+F1，或CTRL+ALT+F2…….CTRL+ALT+F6。要切换回图形终端，只需按快捷键CTRL+ALT+F7。当图形终端崩溃时，我们可以按快捷键切换到这六个字符终端的其中一个，然后输入命令修复问题或重启系统。

一般终端模拟器可以运行在两种模式下，非GUI和GUI模式。为了很好地解释，我们以Linux为例。Linux有5种运行模式，可以简单地划分为非GUI和GUI模式。Linux只有在执行命令 ***init 5*** ，Linux才会启动用户图形界面GUI，其他的模式下，用户图形界面都会被关闭。图形用户界面GUI内的终端仿真器，也就是第七个虚拟控制台（图形终端）通常称为**终端窗口**。



##1.6 终端模拟器安装包（终端模拟包）

终端模拟器有很多，这里就举几个经典的例子：

- GNU/Linux：gnome-terminal、Konsole；
- macOS：Terminal.app、iTerm2；
- Windows：[Win32 控制台](https://zh.wikipedia.org/wiki/Win32%E6%8E%A7%E5%88%B6%E5%8F%B0)、ConEmu 等。

在Linux的早期（20世纪90年代早期），系统上可用的仅是一个简单的与Linux系统交互的文本界面，即 CLI。随着Microsoft Windows的普及，PC用户也期望Linux图形化桌面环境的出现。这推动了OSS社区的更多开发活动，Linux随即出现了多种图形化桌面可供选择。比较流行的桌面系统包括，X Window系统、KDE（K Desktop Environment，K桌面环境）、GNOME（The GNU Network Object Model Environment）。

最早的也是最基本的X Window终端模拟包是xterm，默认包含在X Window包中。xterm包提供了一个基本的VT102/220终端模拟CLI和一个图形化Tektronix 4014环境。xterm是一个完整的终端模拟包。

KDE桌面项目创建了自己的终端模拟包，称为Konsole。Konsole包不仅集成了基本的xterm功能，而且还有一些我们所期望的在Windows应用中才有的高级功能。

GNOME桌面项目也有自己的终端模拟程序，是GNOME Terminal。GENOME Terminal软件包有许多跟xterm和Konsole相同的功能。

> **GNOME Terminal** is a [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator) for the [GNOME](https://en.wikipedia.org/wiki/GNOME) [desktop environment](https://en.wikipedia.org/wiki/Desktop_environment) written by [Havoc Pennington](https://en.wikipedia.org/wiki/Havoc_Pennington) and others. Terminal emulators allow users to access a [UNIX shell](https://en.wikipedia.org/wiki/UNIX_shell) while remaining on their graphical desktop.
>
> GNOME Terminal ('gnome-terminal' from the command line or [GNOME](https://en.wikipedia.org/wiki/GNOME)'s Alt-F2 launcher) emulates the [xterm](https://en.wikipedia.org/wiki/Xterm) terminal emulator and provides some of the same features.



##1.7 结语

在现代，专门的终端硬件（终端机器）已经基本仅存于计算机博物馆，随着计算机外设的发展和图形界面GUI的出现，控制台、终端的概念界线已经模糊，终端也由早期的计算机外设变成了运行在计算机系统上的一个程序，所以人们现在更多地是把它们当作终端模拟器，而tty则成为了终端在类Unix系统的一个指代别名。而计算机终端的统称（总指代），可以指代早期的终端硬件设备（即终端机器）和现在的终端模拟器。最后需要注意的是，计算机终端有别于计算机，它并不提供运算功能。



#2. 补充



##2.1 CLI和终端

人们所使用的计算机是由许多看得见摸得着的硬件和运行于其上的软件所组成的，但使用者并不能直接操作硬件，只能通过操作系统这个计算机中最重要的软件来和计算机交互。当前各种操作系统实现的人机交互接口中，最重要的两种为：`CLI`和`GUI`。
GUI或者说graphical user interface(图形用户接口)，允许用户使用鼠标和键盘操纵屏幕上的各种视觉元素来完成和计算机的交互。
CLI或者说command-line interface(命令行接口)，是一种通过在终端窗口中键入文本命令来实现与计算机交互的接口。

CLI是一个帮助用户与计算机进行交互的程序，它包含命令解释器的功能，依赖于终端的输入功能，（终端从用户那里接收输入，将输入转换为字符和控制序列，然后传输给CLI，CLI执行操作），于是将用户输入的文本转化为命令，并让计算机执行相应命令的操作，最后返回操作结果给终端，让终端显示结果给用户。

由于终端从计算机外设到计算机系统程序的转变，当你在Linux系统上打开一个终端，也即打开了一个CLI，CLI和终端的关系变得暧昧和模糊。



##2.2 Shell程序

许多设备(如计算机，路由器，交换机等)的操作系统中均包含命令行接口，命令行允许用户为命令指定特定的参数来更精确的控制计算机的执行。一些重复的任务可以写成脚本来执行，这样可以更高效和更少出错。通过命令行执行任务在一些情况下要比使用图形用户接口更快一些，但同时也需要使用者记住大量的命令。因此，命令行接口通常被更专业的用户来使用。

在类unix操作系统中的命令行接口称为shell，在linux的各种shell实现中，使用最为广泛的是bash。

#3. 自述

**尝试阐述一个问题，比普通的阅读学习要理解得更深刻。因为普通的阅读学习，一般只是单纯地拿来记忆和普通的了解学习，而很少质疑和考虑它的可靠性，甚至对于一些模糊的理解也会被忽视。阐述对于个人的要求很高，它需要阐述者对知识的深刻理解，以及对知识结构更有条理、更系统地消化。**



#参考链接

[终端，Shell，“tty” 和控制台（console）有什么区别？ - 知乎](https://www.zhihu.com/question/21711307/answer/118788917)

[你真的知道什么是终端吗？ - Linux 大神博客](https://www.linuxdashen.com/%E4%BD%A0%E7%9C%9F%E7%9A%84%E7%9F%A5%E9%81%93%E4%BB%80%E4%B9%88%E6%98%AF%E7%BB%88%E7%AB%AF%E5%90%97%EF%BC%9F)

[命令行界面 (CLI)、终端 (Terminal)、Shell、TTY，傻傻分不清楚？](https://segmentfault.com/a/1190000016129862)

[CLI简介与linux命令初步](https://segmentfault.com/a/1190000007216009)

[Terminal emulator - Wikipedia](https://en.wikipedia.org/wiki/Terminal_emulator)

[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal)



照片来自：

[带你逛西雅图活电脑博物馆（一） - 古董电脑室 - 知乎专栏](https://zhuanlan.zhihu.com/p/21767308)

[带你逛西雅图活电脑博物馆（五） - 古董电脑室 - 知乎专栏](https://zhuanlan.zhihu.com/p/21895357)

# 参考书籍

《Linux命令行与Shell脚本编程大全》























