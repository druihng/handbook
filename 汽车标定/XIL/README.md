# XIL





# Foreword

ASAM developed HIL API as a standard for the communication between test automation
software and hardware-in-the-loop (HIL) testbenches. HIL API enables users to choose
products freely according to their requirements, independent of the vendor.   

**The standard consists of different parts:**

* one part for the base standard specification (programmers guide)
* one part for the mapping rules of each technology reference and
* one part for the XIL support library documentation  

**The base standard contains the major parts  **

* Framework
* Testbench

**The XIL support library contains open source software, which can be used by test case
developers and framework vendors to realize vendor independent common tasks. Such
tasks are**

* for framework and test case
  o Unit Converter
  o Data type converter
* for Framework
  o Mapping reader (which generates a memory image from mapping file
  information with access possibility)
  o Creation of Framework variables (ready for usage) based on mapping
  information's
* for Test case
  o Realization of Framework mapping Info API
  o Mathematical operations  





# 1	Introduction



## 1.1	Motivation

> HIL technology has been developed over the years by only a few suppliers. Due to several
> reasons the architecture of these HIL systems was characterized by a direct rigid coupling of
> test automation software and used test hardware. Therefore test cases directly depend on
> the used test hardware. The end users perspective is, that not always the ‘best’ test software
> could be combined with the ‘best’ testing hardware.
>
> Know-how could not be transferred from one testbench to the other. This resulted in
> additional training costs for employees. Switching to the newest testing technology and to a
> new development process stage was difficult because of tool specific formats and test hardware compatibility issues. This led to the consequence that the base pre-condition for an
> exchange of test cases, e.g. between OEM and supplier, was not fulfilled.
>
> The major goal of all standardization efforts is to allow for more reuse in test cases and to
> decouple test automation software from test hardware. Therefore the reuse of test cases
> within the same test automation software on different test hardware systems should be
> achieved. This will lead to a reduction of effort for test hardware integration into test
> automation software.
>
> Software investments and test case development efforts can be long-term protected. End
> users may decide on test automation software system on a perspective of many years
> without the coercion of being coupled to one test hardware supplier.  



## 1.2	Hardware in the Loop Simulation









## 1.1	Overview

ASAM XIL was developed to allow to exchange combinations of test automation software
and test hardware.
**The standard consists of two layers:**

* Testbench API: This API separate the test hardware from the test software and
  allow a standardized access to the Hardware
* Framework API: This API allow the exchange of the test automation software by a
  standardized access point for test cases, so a decoupling of test cases from real
  and virtual test systems takes place  

**The testbench API covers the access to the following hardware:**

* Model Access, provides access to the simulation model read and write
  parameters, capture and generate signals
* ECU Access, allows capturing and reading of measurement variables (M Port), is
  used for calibration (C Port)
* Stimulator functionality
* DIAG Access
* FIU Access
* Network Access

The Framework serves as a central infrastructure to handle all variables related to their
specific formats. Based on the framework the access to hardware is only realized by
variables, which can be read, write, captured or used in the signal generation. These
variables encapsulate the access to the testbench. 

**The framework API offers the following possibilities:**

* Mapping to exchange test case variables with port elements
* control of port life cycle
* configuration of used testbench ports  





## 4.3	Framework Variables



### 4.3.1	What is a framework variable

Framework variables play a central role in the XIL-API standard. They allow an abstract 
vendor independent mechanism for data access by providing a connection between test 
case values and “physical” testbench port values. Framework variables are the primary data 
access mechanism in the XIL API Framework.



As it is shown in *Figure 40* test cases access the values/variables of a testbench port through 
framework variable objects that are connected to the corresponding testbench port. The 
connection between a framework variable and a variable of a testbench port is a multiple-to-
one connection (multiple framework variables can be connected to the same testbench port 
variable) which is defined by the Mapping of the Framework. This unique abstract identifier is connected to a “concrete” identifier on the corresponding testbench port.

Note: The current version of the XIL API standard supports Framework Variables for the 
following testbench ports:  

* Model Access (MA) 
* ECU(MC)  
* Network 

Framework variables are not supported for the following testbench ports in the current 
version of the XIL API standard: 

* EES 
* Diagnostic 

**Since framework variables are accessed through their abstract identifiers it is guaranteed 
that test cases are independent of the underlying test system. By modifying the mapping of 
the Framework (and so the information about which abstract identifier is connected to which 
concrete identifier of a testbench port) the system can be easily adapted to new test system 
configurations without the need of changing the test cases. **

> For Example a test case can use the Framework variable with the abstract identifier 
> “engine_speed”  which  is  mapped  in  one  case  to  the  concrete  identifier 
> “myModel/myengine1/speed” of the MA Port and in another case with different mapping to 
> the concrete identifier “myECU/engineSpeed” of the ECU(MC) Port. Without any 
> modifications the test case can access the MA Port in the first case and the ECU(MC) port in 
> the second case. 

There are two ways to create an instance of a framework variable object: 
1. Using the CreateVariable()method of the Framework  

  In this case test cases provide the abstract identifier of the framework variable and 
  use the CreateVariable() method of the Framework.  

2. Loading signals from file  

  Measuring uses framework variables in order to define the signals, which are to be 
  recorded. 





### 4.3.2	Framework variable classes

The XIL API standard defines the following five main types of the framework variable: 

* Scalar variables 
* Vector variables 
* Matrix variables 
* Curve variables 
* Map variables 



## 4.4	Measuring

In the context of XIL API measuring describes the process of collecting time traces of 
variables, e. g. for analyzing the effects of changes within simulation models and ECUs.

