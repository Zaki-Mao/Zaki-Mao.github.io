---
layout: post
title: Computer Networks-Data linked layer Part 2
subtitle: Framing and Ethernet Switching
date: 2021-01-29
author: Zaki
header-img: img/home-bg-o.jpg
catalog: true
tags:
     - Computer Networks
     - Computer
     - Net
     - lecture
---

> 接Computer Networks Layer 2 PART 1。

# Framing 

Framing is the layer 2 encapsulation process. A frame is the layer 2 protocol data unit. 

Only encoded bit streams (data) on physical media are not enough to make communication happen. Framing helps obtain essential information that could not be obtained with coded bit streams alone. Examples of such information are: 

Which computers are communicating with one another?

When communication between computers begins and terminates? ▪Provides a method for detection of errors in the communication. 

帧是第2层封装过程。帧是第2层协议数据单元。


只有物理介质上的编码比特流（数据）不足以实现通信。帧有助于获得仅用编码比特流无法获得的基本信息。这类信息的例子有：

哪些计算机在进行通信？

哪些计算机在互相通信？

计算机之间的通信何时开始，何时终止？

提供一种检测通信中错误的方法。

帧的头尾一定要标出来。

There are many different types of frames described by various standards. A single generic frame has sections called fields, and each field is composed of bytes. The names of the fields are as follows: 

     Start frame field
     Address field
     Length / Type field
     Data field
     Frame check sequence field 
     
各种标准所描述的帧有许多不同的类型。一个通用帧有一些称为字段的部分，每个字段由字节组成。字段的名称如下。

    起始帧字段
    地址栏
    长度/类型字段
    数据字段
    帧检查序列字段
    
![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn36zhjmhpj30hz06odgm.jpg)


A generic frame has following fields: 

Start frame field - indicates the beginning signaling sequence of bytes. 

Address field - contains naming information, such as the name of the source node (e.g. MAC address) and the name of the destination node (e.g. MAC address). 

Length/Type field - specifies the exact length of a frame in bytes, or specifies the layer 3 protocol making the sending request. 

Data field - The data package has two parts, the user data and the encapsulated bytes to be sent to the destination computer. Padding bytes may be added so frames have a minimum length for timing purposes. 

Frame check sequence field - contains a number that is calculated by the source node based on the data in the frame and is recalculated by the receiving device to check for damaged frames. 

一个通用帧有以下字段：

起始帧字段--表示字节的起始信令序列。

起始帧字段--表示字节的起始信令序列。

地址字段--包含命名信息，如源节点的名称（如MAC地址）和目的节点的名称（如MAC地址）。

Length/Type字段--以字节为单位指定帧的确切长度，或指定做出发送请求的第3层协议。

数据字段--数据包有两部分，即用户数据和要发送到目的计算机的封装字节。可以添加填充字节，以便帧有一个最小长度，用于计时目的。

帧检查序列字段--包含一个数字，该数字由源节点根据帧中的数据计算，并由接收设备重新计算，以检查帧是否损坏。


The Frame Check Sequence (FCS) is added to the end of the frame that is being sent. When the destination node receives the frame the FCS number is recalculated and compared with the FCS number included in the frame. If the two numbers are different, an error is assumed, the frame is discarded, and the source is asked to retransmit. 

帧检查序列（FCS）被添加到正在发送的帧的末端。当目的节点收到帧时，FCS号会被重新计算，并与帧中包含的FCS号进行比较。如果两个号码不同，则假设有错误，丢弃该帧，并要求源节点重新发送。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn379g9po7j30nl09bjtv.jpg)

前置部分一般不作为有用部分，padding也要算在里面。


# Ethernet Switching

Switching is the process of receiving an incoming frame on one interface and delivering that frame out another interface. 

The difference between layer 2 and layer 3 switching is the type of information inside the frame that is used to determine the correct output interface. 

Layer 2 switching is based on data-link layer information, e.g. MAC addresses. Switches (typically stands for layer 2 switches) use layer 2 switching to forward frames. 

Layer 3 switching is based on network layer addresses information, e.g. IP addresses. Routers or layer 3 switches use layer 3 switching to route a packet. 

切换是指在一个接口上接收一个传入的帧，并将该帧传送到另一个接口上的过程。

第2层和第3层交换之间的区别在于帧内用于确定正确输出接口的信息类型。

第2层交换基于数据链路层信息，如MAC地址。交换机（通常代表第2层交换机）使用第2层交换来转发帧。

第3层交换是基于网络层地址信息，如IP地址。路由器或第3层交换机使用第3层交换来路由数据包。

Switching简单来说就是把冲突域切开，切成小的隔开。缩小征用域的方式来达到目的。

帧携带地址，可以决定地址的发送目的。加一个判断的东西，来判断地址，大大缩小冲突域。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn37k1pp11j30a903wdfx.jpg)

MAC 地址（或物理地址）用于唯一识别主机和接口的方式，以便在本地传送帧。
 
MAC地址是一种扁平的（非等级）地址，长度为48位，用12个十六进制数字表示。没有两个MAC地址应该是完全相同的。MAC地址总共有1612个。

前六位十六进制数字，由IEEE管理，识别制造商或供应商。这一部分被称为OUI（组织唯一标识符）。

其余六位十六进制数字代表接口序列号，或由特定设备制造商管理的其他数值。

MAC地址有两种格式。0000.0c12.3456或00-00-0c-12-34-56.

在以太网中，所有主机都可以看到碰撞域内网络上的所有帧。每台主机都有一个唯一的MAC地址，它位于NIC上。NIC使用MAC地址来评估消息是否应该传递到OSI模型的上层。

当一台主机发送数据时。源主机附加一个带有预定目的地MAC地址的头，并将数据发送到网络上。当这些数据沿着网络介质传播时，网络上每台主机中的NIC会检查MAC地址是否与数据帧携带的物理目的地址相匹配。

如果不匹配，则 NIC 丢弃数据帧。

如果匹配，NIC将复制一份，并将该帧向上传递OSI层。

在以太网中，不同的MAC地址用于第2层单播、组播和广播通信。

单播 - 数据包包含的单播MAC地址是为了将数据传送到一个特定的目标主机。

广播--数据包包含一个广播MAC地址，是为了将数据传送给本地网络（广播域）上的所有主机。广播MAC地址的所有1都显示为十六进制FF-FF-FF-FF-FF-FF。

多播--数据包中包含的多播MAC地址是为了向本地网络上的一组主机传送数据。多播 MAC 地址只能作为数据包的目的地。源端总是有一个单播地址。多播MAC地址是一个特殊的值，以十六进制的01-00-5E开头。该值通过将IP组播组地址的低23位转换为以太网地址的剩余6个十六进制字符结束。MAC地址中剩余的位始终为 "0"。

# LAN Segmentation

Ethernet is a shared media, which means only one node can transmit data at a time. By increasing the number of nodes on a single segment, the probability of collisions increases, resulting in more retransmissions. A solution to the problem is to break the large segment into parts and separate it into isolated collision domains.

The size of collision domains can be reduced by using bridges, switches, and routers. This process is called segmentation.

以太网是一种共享媒体，这意味着一次只能传输一个节点的数据。增加单个网段上的节点数量，碰撞的概率就会增加，导致更多的重传。解决这个问题的方法是将大网段分成若干部分，并将其分离成孤立的碰撞域。

可以通过使用网桥、交换机和路由器来减小碰撞域的大小。这个过程称为分段。

网桥将一个碰撞域划分为两个网段。网桥通过建立一个地址表（命名为桥接表或交换表）来 "学习 "网段划分，该表包含每个设备的MAC地址以及使用哪个网段到达该设备。然后，网桥根据表项转发或丢弃帧。网桥就是这样控制两个碰撞域之间的流量。网桥被认为是一个存转设备，所以它在收到整帧后才会转发。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn383ctugoj30k606ygmx.jpg)

与网桥类似，以太网交换机仅根据第2层MAC地址执行交换和过滤。但是，交换机可以将一个局域网分割成微段，微段是单个主机段，通过使用虚拟电路，允许许多主机在一个无碰撞的环境中并行通信。

![](https://tva1.sinaimg.cn/large/008eGmZEgy1gn38oo1fdfj30n309ntaq.jpg)

# Latency

延迟（延迟）是指一个帧/包从源主机到网络上的目的主机所需的时间。延迟有一些来源。

1. 传播时延，即信号在电缆上传播所需的时间。(对于Cat 5 UTP来说，通常每100米约为0.556微秒)。

2. NIC延迟，指源NIC在线缆上放置电压脉冲和接收NIC解释这些脉冲所需的时间。(对于10BASE-T网卡来说，一般为1微秒左右)。

3. 设备延时，是指在两台通信主机之间的路径中，网络设备的使用所增加的时间。

4. 帧延迟，由帧的内容和在帧中哪些地方可以进行交换决策造成的。例如，设备在没有读取到目的MAC地址之前，不能将一帧路由到目的地。
 

