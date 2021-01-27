---
layout: post
title: Computer Networks-layer 2 Technology
subtitle: PART 1 Data link layer and Ethernet Switching lecture 
date: 2021-01-27
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - Computer Networks
     - Net
     - lecture
     - Ethernet
---

>   链路层同样非常重要，它有着承上启下的作用。

 # Function
  
The data link layer provides reliable transmission of data across a physical link, thus it concerns with media access, physical addressing, network topology, error notification, ordered delivery of frames, and flow control. 

Layer 2 addresses the limitations in layer 1:

     Layer 1 cannot decide which host will transmit binary data from a group that are all trying to transmit at the same time. 
     Layer 2 uses a system called Media Access Control (MAC) to choose which host will transmit binary data.
     Layer 1 cannot name or identify a host.
     Layer 2 uses an flat addressing (or flat naming) process. 
     Layer 1 can only describe streams of bits.
     Layer 2 uses framing to organize or group the bits. 
     Layer 1 cannot communicate with the upper layers. Layer 2 does that with Logical Link Control (LLC). 
	  For a host, the important layer 2 functions are performed by the network adapters (Network Interface Card, NIC). 

 数据链路层在物理链路上提供可靠的数据传输，因此它涉及到介质访问、物理寻址、网络拓扑、错误通知、帧的有序交付和流控制。

第2层解决了第1层的限制。

第1层不能决定由哪台主机传输一组二进制数据。

都试图在同一时间传输。

第2层使用名为 "媒体访问控制"（MAC）的系统来选择哪个主机将传输二进制数据。

第1层不能对主机进行命名或标识。

第2层使用扁平寻址（或扁平命名）过程。

第1层只能描述比特流。

第2层使用框架来组织或分组比特。

第1层不能与上层通信。第2层通过逻辑链路控制(LLC)来实现。

对于主机来说，重要的第2层功能由网络适配器（网络接口卡，NIC）执行。

# MAC子层和LLC子层

链路层按标准分LLC和MAC。

mac子层主要是调用接口。和物理相关的放在mac层, 和控制相关放在LLC层。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn22xht8d4j30sc0c3416.jpg)

LLC:独立于技术的逻辑链路控制 (LLC)，它定义了为网络层协议提供服务的软件进程。
MAC: 独立于技术的媒体访问控制（MAC），它定义了由硬件执行的媒体访问流程。

The Media Access Control (MAC) sublayer defines the rules (or methods) for access to different media. The MAC protocols determines which host on a shared-medium environment is allowed to transmit the data. There are two categories of Media Access Control methods: 

介质访问控制（MAC）子层定义了访问不同介质的规则（或方法）。MAC协议决定了共享介质环境中哪台主机可以传输数据。介质访问控制方法有两类。

Deterministic (taking turns), for example, IEEE 802.5 Token Ring. （事先分配事先确定）

Non-deterministic (first come, first served), for example, IEEE 802.3 CSMA/CD or Ethernet. 

MAC is implemented by hardware, typically in the network adapter of a host.

 
The Logical Link Control (LLC) sublayer is defined in the IEEE 802.2 specification, which allows part of the data link layer to function independently from existing technologies. 

LLC participates in the encapsulation process. （参与封装过程）The LLC PDU is sometimes called an LLC packet. LLC takes the network layer PDU, a packet, and adds more control information to help deliver the packet to its destination. 

LLC adds two addressing components of the 802.2 specification, the Destination Service Access Point (DSAP) and the Source Service Access Point (SSAP)（接口）. This repackaged packet then travels to the MAC sublayer for handling by the required specific technology for further encapsulation and data.

LLC is implemented by software (typically in the driver of a network adapter), and its implementation is independent of the hardware. 

# Ethernet

Ethernet operates in two areas of the OSI model, the lower half of the data link layer, known as the MAC sublayer and the physical layer. 

以太网工作在OSI模型的两个区域，即数据链路层的下半部分，即MAC子层和物理层。

重点：如何进行多用户协调？

# 冲突域

The underlying logical topology of Ethernet is a multi-access bus, therefore all devices on a share the medium, called collision domain. If multiple devices attempt to forward data simultaneously, the data will collide resulting in corrupted, unusable data. 
A collision domain （冲突域）is a connected physical network segment where collisions can occur. Using the layer 1 device likes repeater or hub extends the collision domain. The network on both sides is one larger collision domain. 

冲突域是指可能发生碰撞的连接物理网段。利用第1层设备如中继器或集线器扩展了冲突域。两边的网络就是一个较大的冲突域。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn23qmx6t1j30ky06jt9j.jpg)

	Reapeater,hub工作在物理层。有线方式一起构成冲突域。
	
以太网提供了一种基于竞争（非确定性）的MAC方法，即带碰撞检测的载波感知多址（CSMA/CD），用于控制主机如何访问共享介质。

CSMA是一个简单的系统，每次只允许一个主机传输。网络上的主机可以在任何时候访问介质。在发送数据之前，CSMA主机会监听网络，以确定网络是否已经在使用中。

 如果在使用中，则主机等待。
 如果不在使用中，则进行传输。

       CSMA第一步：先看看信道是否空闲。
       第二步：“有可能两个人看信道都是空闲的，同时说话，冲突。”
       第三步：冲突检测，“一边讲，一边还要听”
       真正发生冲突了停下来，止损。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn23w94objj30bj0c6jt2.jpg)

虽然使用CSMA，但由于电信号在电缆上传播需要时间（延迟），因此有可能有多个站在同一时间或接近同一时间开始传输，从而导致碰撞。每当网络上发生碰撞时，所有的传输都会停止一段时间。
使用CSMA/CD，主机在传输数据的同时检测到碰撞。一旦检测到碰撞，发送主机就会发送一个32位的 "干扰 "信号，将强制碰撞。这样做是为了使正在传输的任何数据彻底损坏，所有主机都有机会检测到碰撞。

“发生冲突时看到jam，其他主机相当于得到更明确的通知。“之后back off.

总结：

1. 两台主机监听以确保电缆是空闲的，然后进行传输。主机1在信号还没有到达最后一段电缆之前，就能传输相当比例的帧。

2. 主机2在开始自己的传输之前，还没有接收到传输的第一比特，只能在网卡感知到碰撞之前发送几比特。

3. 当主机2检测到碰撞时，它立即截断当前的传输，替换32位的干扰信号，并停止所有的传输。

4. 主机2在碰撞传播回主机1之前，完成了32位干扰信号的传输，并变得无声无息，而主机1仍未察觉到碰撞，继续传输。

5. 当碰撞碎片最终到达主机1时，它也截断了当前的传输，用一个32位干扰信号代替它正在传输的剩余帧。在发送32位干扰信号后，主机1停止了所有的传输。

# 冲突检测


当两个或两个以上以半双工方式工作的以太网主机在碰撞域内同时传输时，通常会发生碰撞。如果连接的主机是以全双工方式工作，那么主机可以同时发送和接收，不应该发生碰撞。碰撞的类型有三种。

1. 局部碰撞，在半双工的UTP电缆上，在RX处和TX处同时检测到信号，或者在同轴电缆上感应到过电压信号的碰撞。

2. 远端碰撞，指损坏的帧（碰撞碎片）的帧大小小于最小字节（64八位字节），且FCS无效的碰撞。它也会发生在中继器的远端，但不表现出过电压或同时RX/TX活动的局部碰撞症状。在UTP网络中，这是观察到的最常见的一种碰撞。

3. 晚期碰撞，是指在前64个八位组数据发送完毕后发生的碰撞。对于这种类型的碰撞，网卡不会自动重传。即槽位时间过后发生的同步传输。

# Slot Time

 以太网的时隙有它自己的特定意义.
 
    （1）在以太网CSMA/CD规则中，若发生冲突，则必须让网上每个主机都检测到。但信号传播到整个介质需要一定的时间。 
    （2）考虑极限情况，主机发送的帧很小，两冲突主机相距很远。在A发送的帧传播到B的前一刻，B开始发送帧。这样，当A的帧到达B时，B检测到了冲突，于是发送阻塞信号。 
    （3）但B的阻塞信号还没有传输到A，A的帧已发送完毕，那么A就检测不到冲突，而误认为已发送成功，不再发送。 
    （4）由于信号的传播时延，检测到冲突需要一定的时间，所以发送的帧必须有一定的长度。这就是时隙需要解决的问题。

           
       1,电磁波在1KM电缆的传输时延约为5us,如果在理想情况下。
       2，在10Mbps的以太网中有个5-4-3的问题:10 Mb/s以太网最多只能有5个网段，4个转发器，而其中只允许3个网段有设备，其他两个只是传输距离的延长。按照标准，10Mbps以太网采用中继器时，连接最大长度为2500米!
       
       那么在理想的情况下,时隙可以为2500/1000*5*2us=25us。
       
 在以太网在,时隙也可以叫做争用期,只有经过争用期这段时间没有检测到冲突碰撞,发送端才能肯定这次发送不会发生碰撞.然后当发生了碰撞而停止之后,以太网上的机器会再次侦听,再发送,这就有个再次碰撞的可能性,这里以太网使用了截断二进制指数类型的退避算法来解决,在碰撞之后,会推迟一个随机时间(具体略),这也会对争用期的选择有些影响.

# 帧间间隔

MAC子层的标准还规定了帧间最小的间隔是9.6us,相当于96bit的发送时间,就是说一个主机在检测到总路线开始空闲后,还要等待9.6us才能发送数据.这样做是为了使刚刚收到的数据帧的主机的接收缓存来得及清理,做好接收下一帧的准备。

100Mbps以太网改变了10Mbps以太网的某些规定,其中最主要的是要在数据发送速率提高时使"单程传播时延与帧的发送时延之比"(a参数)仍然保持不变或者保持为较小的数值。(这个值可以影响以太网信道的利用率)

而为了使a参数保持不变,可以把帧度L增大到原来10倍(100M/10M),也可把网络的线长到原来的10分之1。

在100Mbps的以太网中采用的是保持原来的最短帧不变(和10M的兼容,同为64B),但把线长减到100米.而帧间隔由10M的9.6us减到0.96us。

       对于10Mbps以太网来说,10Mb/s*51.2us=512bit,所以一般说的512bit时隙长度就是这样来的,这个长度为512/8=64字节.
       以太网在发送数据时,如果在前面64字节没有发生冲突的话,那么后续的数据就不会发生冲突,以太网就认为这个数据的发送是成功的。

# 回退算法

以太网中传输的时序根据不同情况而不同。

1. 如果没有发生碰撞。

在一帧发送后，所有主机都需要等待一个最小的96位时间间隔，然后任何站才可以合法地发送下一帧。这是从第一帧的最后一位到第二帧序言的第一位来衡量的。这个间隔间隙称为帧间间隔。帧间间隔是两个非冲突帧之间的最小间隔。
所有版本以太网的帧间间隔保持不变，为96位-次，但在速度更快的版本以太网上，该间隔所需的时间相应变短。

2. 如果发生了碰撞。

发生碰撞后，所有主机都允许电缆成为空闲状态(每个主机都会等待完整的帧间间隔)，那么发生碰撞的主机在尝试重传碰撞的帧之前，必须等待一个额外的、可能逐渐延长的时间。等待时间被有意设计成随机的，这样两个主机在重传前就不会延迟相同的时间，这样会导致更多的碰撞。这部分是通过扩大每次重传尝试时随机重传时间的选择间隔来实现的。等待时间以参数槽时间的增量来衡量。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn25g8pujnj30g701caa7.jpg)

指数回退算法,这里，n=尝试次数。

如果MAC层在16次尝试后无法发送帧，就会放弃并向上层（网络层）产生错误。这种情况相当少见，只有在网络负荷极重的情况下或网络上存在物理问题时才会发生。


 







