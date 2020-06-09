# 4	XCP FEATURES AND CONCEPTS



## 4.1	数据传输同步



### 4.1.1	DAQ, STIM AND ODT

[![t5lj6s.png](https://s1.ax1x.com/2020/06/09/t5lj6s.png)

**DTO**

DTO (Data Transfer Object) 数据传输对象，位于从节点内存中的数据元素是以DTO进行传输的，DAQ是从到主，而STIM是主到从。

**ODT**

ODT (Object Descriptor Table) 对象描述表，ODT描述了同步数据传输对象和从节点内存的映射。



A synchronous data transfer object is identified by its Packet IDentifier (PID) that identifies
the ODT that describes the contents of this synchronous data transfer object.  



### 4.1.2	ODT ENTRY

ODT条目通过它们的地址、扩展地址、以 *ADDRESS_GRANULARITY(AG)* 地址粒度来确定的元素size来引用数据元素，对于表示一个bit的数据元素，通过位偏移来引用。

**GRANULARITY_ODT_ENTRY_SIZE_x**

> determines the smallest size of a data element referenced by an ODT entry.
>
> *GRANULARITY_ODT_ENTRY_SIZE_x* must not be smaller than AG.
> GRANULARITY_ODT_ENTRY_SIZE_x[BYTE] >= AG[BYTE] 



**MAX_ODT_ENTRY_SIZE_x**

> The MAX_ODT_ENTRY_SIZE_x parameters indicate the upper limits for the size of the
> element described by an ODT entry in ADDRESS_GRANULARITY.  
>
> SizeOf(element described by ODT entry)[AG] <= MAX_ODT_ENTRY_SIZE_x[AG]  



**ODT_ENTRY_NUMBER **

> If a slave only supports elements with size = BYTE, the master has to split up multi-byte
> data elements into single bytes.
> An ODT entry is referenced by an ODT_ENTRY_NUMBER.  



### 4.1.3	OBJECT DESCRIPTOR TABLE

ODT entries are grouped in ODTs.
If DAQ lists are configured statically, MAX_ODT_ENTRIES specifies the maximum number
of ODT entries in each ODT of this DAQ list.
If DAQ lists are configured dynamically, MAX_ODT_ENTRIES is not fixed and will be 0.
For every ODT the numbering of the ODT entries through ODT_ENTRY_NUMBER restarts
from 0
ODT_ENTRY_NUMBER [0,1,..MAX_ODT_ENTRIES(DAQ list)-1]  



### 4.1.4	DAQ LIST

可以将若干的ODT组织进一个DAQ列表里。XCP允许多个DAQ列表同时处于活动状态。The sampling and transfer of each DAQ list is triggered by individual events in the slave (see SET_DAQ_LIST_MODE).  

![t5lXlj.png](https://s1.ax1x.com/2020/06/09/t5lXlj.png)
**MAX_ODT**

> If DAQ lists are configured statically, MAX_ODT specifies the number of ODTs for this
> DAQ list.
> If DAQ lists are configured dynamically, MAX_ODT is not fixed and will be 0.  

**MAX_DAQ**

> MAX_DAQ is the total number of DAQ lists available in the slave device. It includes the
> predefined DAQ lists that are not configurable (indicated with PREDEFINED at
> GET_DAQ_LIST_INFO) and the ones that are configurable. If DAQ_CONFIG_TYPE =
> dynamic, MAX_DAQ equals MIN_DAQ+DAQ_COUNT.  

**MIN_DAQ**

> MIN_DAQ is the number of predefined DAQ lists. For predefined DAQ lists,
> DAQ_LIST_NUMBER is in the range [0,1,..MIN_DAQ-1].  

**DAQ_COUNT**

> DAQ_COUNT is the number of dynamically allocated DAQ lists.  

MAX_DAQ-MIN_DAQ is the number of configurable DAQ lists. For configurable DAQ lists,
DAQ_LIST_NUMBER is in the range [MIN_DAQ,MIN_DAQ+1,..MAX_DAQ-1].  

Within one and the same XCP slave device, the range for the DAQ list number starts from
0 and has to be continuous.
DAQ_LIST_NUMBER [0,1,..MIN_DAQ-1] + [MIN_DAQ,MIN_DAQ+1,..MAX_DAQ-1]  

**ODT_NUMBER**

> For every DAQ list the numbering of the ODTs through ODT_NUMBER restarts from 0 and
> has to be continuous.
> ODT_NUMBER [0,1,..MAX_ODT(DAQ list)-1]  



### 4.1.5	



### 4.1.6	Dynamic DAQ Configuration

对于可配置的DAQ列表，从服务器可以对DAQ列表的数量、每个DAQ列表的ODT数量以及每个ODT的ODT条目数量进行固定限制。

从服务器同样也可以完全动态地配置DAQ列表。

可配置的DAQ列表是静态配置还是动态配置，取决于GET_DAQ_PROCESSOR_INFO上DAQ_PROPERTIES  的DAQ_CONFIG_TYPE   的标志。

























