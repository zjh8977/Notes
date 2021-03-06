## 操作系统

### 1. 操作系统的概述

#### 1.1 操作系统的基本概念

- 操作系统定义及作用

  - 定义

    能有效的组织和管理系统中的各种软、硬件资源，合理的组织计算机系统工作流程，控制程序的执行，并向用户提供一个良好的工作环境和友好的接口

  - 作用

    1. 通过资源管理提高计算机系统的效率
    2. 改善人机界面向用户提供友好的工作环境

- 操作系统特征与功能

  - 4个特征

    并发性、共享性、虚拟性、不确定性

  - 功能

    操作系统的功能可分为进程管理、文件管理、存储管理、设备管理、作业管理

#### 1.2 操作系统分类及特点

- 批处理操作系统

  分为单道批处理和多道批处理。

  单道批处理指一次只有一个作业装入内存执行。

  多道批处理允许多个作业装入内存执行。多道批处理系统特点：多道、宏观上并行运行、微观上串行运行。

- 分时操作系统

  一个计算机系统与多个终端设备连接。特点：多路性、独立性、交互性、及时性。

- 实时操作系统

  分为实时控制系统（武器控制、飞机自动驾驶等）和实时信息处理系统（飞机订票系统、情报检索等）。

  实时系统与分时系统的区别：

  - 系统的设计目标不同
  - 交互性的强弱不同
  - 响应时间的敏感度不同

- 网络操作系统

  - 网络操作系统的功能

    主要包括高效、可靠的网络通信；对网络中共享资源的有效管理；提供电子邮件、文件传输、共享硬盘和打印机等服务；网络安全管理；提供互操作能力。

  - 网络操作系统分类
    1. 集中模式。系统基本单元由一台主机和若干与主机相连的终端构成，信息的处理和控制是集中的。UNIX就是这类操作系统的典型例子
    2. 客户端/服务器模式。这种模式网络可分为服务器和客户端。
    3. 对等模式（peer-to-peer）。在采用这种模式的操作系统网络中，各个站点是对等的。它既可以作为客户端区访问其它站点，也可以作为服务器向其它站点提供服务。可见该模式具有分布处理和分布控制的特征。

- 分布式操作系统
  
  由多个分散的计算机经连接而成的计算机系统，系统中的计算机无主、次之分，任一两台计算机可以通过通信交换信息。
  
- 微型计算机操作系统

  常见的有Windows、Mac OS、Linux。

- 嵌入式操作系统

  运行在嵌入式智能芯片环境中，对整个智能芯片以及它所操作、控制的各种部件装置等资源进行同意协调、处理、指挥和控制

  特点：微型化、可定制、实时性、可靠性、易移植性。

### 2. 进程管理

### 3. 存储管理

存储器管理的对象是主存存储器，简称主存或内存。

存储器管理的主要功能是包括主存空间的分配和回收、提高主存的利用率、扩充主存、对主存信息实现有效的保护。

存储管理的主要目的是解决多个用户使用主存的问题。管理方案包括分区存储管理、分页存储管理、分段存储管理、段页式存储管理以及虚拟存储管理。

#### 3.1 分区存储管理

将主存划分给每个用户，每个用户只能在自己的区域内使用。

- 缺点：用户程序必须装入连续的地址空间中，若无满足用户要求的连续空间，需要进行分区靠拢操作，这是以耗费系统时间为代价的

#### 3.2 分页存储管理

优缺点：**优点**是分页的过程由操作系统完成，对用户是透明的，所以用户不用关心分页的过程，**缺点**是不易实现共享。

1. 纯分页存储管理

   - 分页原理

     将进程的地址空间划分成多个大小相等的区域，称为页。主存空间划分成与页相同大小的若干个物理块，称为块或页框。

   - 地址结构

     分页系统由两部分组成：前一部分为页号P；后一部分为偏移量W，即页内地址。

   - 页表

     相当于一个目录，记录每一页对应的物理块。页表的作用是实现从页表到物理块号的地址映射。若访问越界，会产生越界中断。

2. 块表

   从地址映射的过程可以发现，页式存储管理至少需要两次访问主存。第一次访问页表得到数据的物理地址；第二次是存取数据。

   为了解决这个问题，在地址映射机构中增加一个小容量的联想存储器，联想存储器由一组高速存储器组成，称之为块表，用来保存当前访问频率高的少数活动页的页号及相关信息。

3. 两级页表机制

   为了减少页表所占用的连续的主存空间，建立一张页表，称为外层页表（页表目录），即第一级是页目录表，其中的每个表目是存放某个页表的物理地址；第二级是页表，其中的每个页目所存放的是页的物理块号。

#### 3.3 分段存储管理

优缺点：**优点**是段是信息的逻辑单位，易于实现段的分享，即允许若干个进程共享一个或多个段，而且对段的保护也比较简单。

作业的地址空间被划分为若干个段。在系统中为每个进程建立一张段映射表，称为“段表”，每个段在表中占有一个表项，在其中记录了该段在主存中的起始地址（基址）和段的长度

例题：系统采用段式存储管理方案，假设某作业的段表如下

| 段号 | 基地址 | 段长 |
| ---- | ------ | ---- |
| 0    | 219    | 600  |
| 1    | 2300   | 200  |
| 2    | 90     | 100  |
| 3    | 1327   | 580  |
| 4    | 1952   | 96   |

问：逻辑地址（0,168）、（1，58）、（2，98）、（3,300）和（4,100）能否转换成对应的物理地址。

答：第1,2,3,4都可以，但是最后一个会产生地址越界。

#### 3.4 段页式存储管理

优缺点：**优点**既具有分页系统能有效的提高主存利用率的优点，又具有分段系统能很好的满足用户需要的长处。

1. 原理

   将整个主存划分成大小相等的存储块（页框），将用户程序按程序的逻辑关系分为若干个段，并为每个段附一个段名，再将每个段分页。

2. 地址结构

   由段号、段内页号、页内地址组成

3. 为了实现从逻辑地址到物理地址的变换，系统中必须同事配置段表和页表。

4. 从逻辑地址到物理地址的变换过程

   - 根据段号S查段表，得到页表的起始地址
   - 根据页号P查页表，得到物理块号b
   - 将物理块号b拼页内地址W得到物理地址

#### 3.5 虚拟存储管理

如果一个作业只部分装入主存便可开始启动运行，其余部分暂时留在磁盘上，在需要时再装入主存，这样可以有效的利用主存空间。虚拟存储器是为了扩大主存容量采用的一种设计方法。

1. 程序局部性原理

   程序在执行时将呈现出局部性规律，即在一段时间内，程序的执行仅局限于某个部分。程序的局限性包括**时间局限性**和**空间局限性**

   - 时间局限性

     某条指令呗执行，在不久可能该指令还会被执行；如果某个存储单元呗访问，则不久后该存储单元可能再次被访问。产生的原因是由于程序中存在大量的循环操作。

   - 空间局限性

     某个存储单元被访问，那么其附近的存储单元也可能在不久被访问。产生的原因是程序是顺序执行的。

2. 虚拟存储器的实现

   虚拟存储器是具有**请求调入功能**和**置换功能**，能仅把作业的一部分装入主存便可以运行作业的存储器系统，是能从逻辑上对主存容量进行扩充的一种虚拟的存储器系统。

   - 请求分页系统。只装入若干页在主存中，其他的在使用的使用的时候再调入或置换
   - 请求分段系统。
   - 请求段页式系统

3. 请求分页系统的实现

   请求分页系统是在纯分页系统的基础上增加了请求调页功能、页面置换功能所形成的页式虚拟存储系统，是目前常用的虚拟存储器的方式。

   每当索要访问的页面不在主存时便要产生一个缺页中断

4. 页面置换算法

   - 最佳置换算法

     这是一种理想型的算法。

   - 先进先出(FIFO)置换算法

     一种最直观、性能最差的算法

   - 最近最少未使用(LRU)算法

     需要硬件的支持（寄存器和栈）

   - 最近未使用（NUR）置换算法

5. 工作集

   为了减小缺页率，适当增加存储储存的页数。

### 4. 设备管理

将负责管理设备和输入输出的机构称为I/O系统。因此，I/O系统由设备、控制器、通道、总线、I/O软件组成

#### 4.1 设备管理概述

1. 设备的分类

   - 按数据组织分类。分为块设备（如磁盘）和字符设备（如终端）。
   - 按设备的功能分类。分为输入设备、输出设备、存储设备、网络联网设备、供电设备等
   - 从资源分配角度分类。分为独占设备、共享设备和虚拟设备
   - 按数据传输率分类。分为低速设备、中速设备和高速设备

2. 设备管理的目标与任务

   目标是如何提高设备的利用率，为用户提供方便统一的界面。

   主要利用的技术有中断技术、DMA技术、通道技术和缓冲技术

#### 4.2 I/O软件

I/O设备管理软件分为4层：中断处理程序、设备驱动程序、与设备无关的系统软件和用户软件。

#### 4.3 设备管理采用的相关技术

1. 通道技术

   引入通道的目的是使数据的传输独立于CPU，使CPU从烦琐的I/O工作中解脱出来。

2. DMA技术

3. 缓冲技术

   缓冲技术可提高外设利用率，尽可能使外设处于忙状态。

   引入缓冲的主要原因有以下几个方面

   - 缓和CPU与I/O设备间速度不匹配的矛盾
   - 减少对CPU的中断频率，放宽对中断响应时间的限制
   - 提高CPU和I/O设备间的并行性

4. Spooling技术（外围设备联机操作）

   Spooling系统由**预输入程序**、**缓输出程序**、**井管理程序**、**输入和输出井**组成

   输入井中的作业有四种状态

   - 提交状态。作业正在预输入
   - 后备状态。作业输入结束，但未被选中执行
   - 执行状态。正在运行
   - 完成状态。作业的执行结果等待缓输出

#### 4.4 磁盘调度

磁盘调度分为移臂调度和旋转调度，并且是先进性移臂调度，再进行旋转调度

1. 磁盘驱动调度

   常用的磁盘调度算法

   - 先来先服务(FCFS)。哪个进程先访问磁盘，就先进行调度。平均寻道时间可能较长
   - 最短寻道时间优先(SSTF)。该算法选择这样的进程，其要求访问的磁道与当前磁头所在的磁道距离最近，使得每次的寻道时间最短。但是不能保证平均寻道时间最短
   - 扫描算法(SCAN)。不仅考虑要访问的磁道与当前磁道的距离，更优先考虑的是磁头的当前移动方向。该算法也叫电梯调度算法
   - 单向扫描算法(CSCAN)。磁头只做单向运动。

2. 旋转调度算法

   旋转调度算法应考虑如下情况

   - 进程请求访问的额是同一磁道上不同编号的扇区
   - 不同磁道上不同编号的扇区
   - 不同磁道上相同编号的扇区

   对于第1,2种，旋转调度总是让首先到达读/写磁头位置下的扇区先进行传送操作；对于第三种，旋转调度可以任选一个读/写磁头位置下的扇区进行传送操作。

### 5. 文件管理

