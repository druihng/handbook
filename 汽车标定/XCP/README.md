# XCP





## 概述

#### 标准介绍

XCP标准主要分为五部分：

Part 1 – Overview。XCP协议概述，包括XCP的特点描述以及XCP协议的基本原理。

Part 2 – Protocol Layer Specification。对协议层进行详细的规范和说明，包括XCP数据包类型、格式以及各命令使用说明。

Part 3 – Transport Layer Specification。该部分包含5份文档，分别对应5个不同的传输层（CAN，Ethernet/TCP_IP，FlexRay，SxI/SCI&SPI，USB），规定不同总线下传输层的实现。

Part 4 – Interface Specification。该部分对A2L描述文件、秘钥与种子加解密、数据校验功能说明。

Part 5 – Example Communication Sequences。该部分描述了部分通信数据流，演示如何使用XCP协议的命令同ECU进行通讯。



#### XCP通信协议方式

XCP数据包主要有两种形式：传输控制命令的CTO(Command Transfer Object)和同步数据包DTO(Data Transfer Object)。主从节点间的XCP通信方式如图1所示。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibqwPzK0sZdrJOSTMCmccFK3twUgM9gwR3nOgqzTy5ETBzRVHYk9lMEw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图1 XCP主从机交互

CTO用于传输控制命令，包含五种形式：

1.CMD(Protocol Command)，PID范围为0xC0~0xFF，主机向从机发送的命令请求，从机据此识别命令。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibsN3AMpe9XN06qiamNJrCnOic8lCfBxrLG8rIvTPbID51Ddzbyj02wCJw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

2.RES(Transferring Command Responses)，PID值为0FF，从机在接收到主机的CMD后，当命令被执行成功时，从机向主机发送肯定响应数据包。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UiblQfxicfkQpK9siberyKokMsBffNxM692U0m7QaEt6WE8pKw57zf9BhEw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

3.ERR(Error Packets)，PID值为0XFE，当命令执行发生错误时，从机反馈错误数据包。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibOOnavR8EvUkVwHzA88bf6KUPa7ntWAf5bEFVtA3jjouTHL2JnyFVww/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

4.EV(Event)，PID值为0xFD，当从机向主机报告一个异步的事件时，发送次数据包。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibAIPkAx224q63IBPib1vwN4YX02BrMtaHLGjqkicV9kglJx7O9n7TKHTg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

5.SERV(Service Request Packets)，PID值为0xFC，当从机需要主机做出某些动作时，从机向主机发送此数据包。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibibEYp0bMjQzOsueYur79kLZJlIasXbh9Ez65vWic165WUFnXwy2vTsaA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

DTO数据包传输同步数据包DAQ(Data Acquisition)和同步激励数据STIM(Data Stimulation packet)。在DAQ模式下，从机周期性上传数据，STIM模式正好相反，主机周期性的向从机下载数据。





#### 基于CAN总线的XCP报文格式

在汽车ECU的标定中，通常使用CAN总线。基于CAN的XCP报文帧结构如图2所示，其中PID用于标识XCP报文的类型，PID与任务的对应表如表1所示，FILL用于描述报文对齐信息，DAQ表示DAQ列表的标识符，TIMSTAMP为可选项，Data存放数据。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/CvyFYUrD5pdOmcoldZITqA4Iw5yx90UibPbh7132q0I7QxDGXcu0sH7DrvfXfSJOcia5pDvLHvkY5tKmU25YdgoA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

图2 基于CAN的XCP帧格式



| *指令类别*              | *PID**指令码* | *指令用途*                                         |
| ----------------------- | ------------- | -------------------------------------------------- |
| *标准指令 STD*          | *0xF1~0xFF*   | *请求连接、上传、设定位移地址、断开连接等基本命令* |
| *标定指令 CAL*          | *0xEC~0xF0*   | *标定任务的基本指令*                               |
| *页面切换命令 PAG*      | *0xE4~0xEB*   | *标定内存页操作指令*                               |
| *数据采集和请求指令DAQ* | *0xD3~0xE3*   | *DAQ* *数据采集和请求指令*                         |
| *内存编程指令 PGM*      | *0xC8~0xD2*   | *ECU* *内存管理指令*                               |

表1 PID与任务的对应关系





