> *You are here: README file for switched_enterprise_network in cpt-projects.*
>
> Note before reading:
>
> 1. The content of the README is written in **Simplified Chinese**.
> 2. Due to limited ability and time, mistakes are inevitable in the project. I would be most grateful if you could share your insights with me or point out any mistakes!

### 一、快速介绍

1. 项目名称：**搭建交换式企业网络**
2. 功能与服务：直连路由、静态路由和单臂路由；VLAN、Trunk、HSRP、STP、VTP和SVI；特权密码、Telnet、文件备份、DHCP和ACL；WEB、DNS、DHCP和FTP；NAT、PPP和GRE VPN。

### 二、设备列表与拓扑

|类别|型号|数量|备注|
|:---:|:---:|:---:|:---:|
|计算机|PC-PT|16|暂无|
|服务器|Server-PT|5|暂无|
|交换机|2960-24TT|5|AS-1、AS-2、AS-3、AS-4、AS-5|
|交换机|3650-24PS|2|DS-1、DS-2|
|路由器|1941|1|WJ-R|
|路由器|2911|1|ISP-1|
|路由器|4321|1|Router-Edge|

![拓扑图](topo.png)

### 三、网络规划

#### 1. VLAN规划

|ID|名称|设备|接口|
|:---:|:---:|:---:|:---:|
|VLAN 10|BM1|AS-1、AS-2、AS-3|F0/1|
|VLAN 20|BM2|AS-1、AS-2、AS-3|F0/2|
|VLAN 30|BM3|AS-1、AS-2、AS-3|F0/3|
|VLAN 40|BM4|AS-1、AS-2、AS-3|F0/4|
|VLAN 101|ADMIN|AS-1、AS-2、AS-3|-|
|VLAN 100|SERVER-W-D|Router-Edge|G0/1/0-1|
|VLAN 200|SERVER-M-F|Router-Edge|G0/1/2-3|
|VLAN 4|ADMIN|AS4、AS5|-|
|VLAN 5|BM5|AS4、AS5|F0/1-12|
|VLAN 6|BM6|AS4、AS5|F0/13-22|
|VLAN 7|BM7|AS4、AS5|G0/2|

#### 2. 交换设备地址规划

a. AS-1

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至AS-2 G0/1|
|G0/2|-|连接至DS-1 G1/0/1|
|VLAN 10|-|BM1|
|VLAN 20|-|BM2|
|VLAN 30|-|BM3|
|VLAN 40|-|BM4|
|VLAN 101|10.0.101.1/24|ADMIN|

b. AS-2

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至AS-1 G0/1|
|G0/2|-|连接至AS-3 G0/1|
|VLAN 10|-|BM1|
|VLAN 20|-|BM2|
|VLAN 30|-|BM3|
|VLAN 40|-|BM4|
|VLAN 101|10.0.101.2/24|ADMIN|

c. AS-3

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至AS-2 G0/2|
|G0/2|-|连接至DS-2 G1/0/1|
|VLAN 10|-|BM1|
|VLAN 20|-|BM2|
|VLAN 30|-|BM3|
|VLAN 40|-|BM4|
|VLAN 101|10.0.101.3/24|ADMIN|

d. DS-1

|接口|地址|描述|
|:---:|:---:|:---:|
|G1/0/1|-|连接至AS-1 G0/2|
|G1/0/2|10.0.13.1/24|连接至Router-Edge G0/0/0|
|VLAN 10|10.1.10.253/24|BM1|
|VLAN 20|10.2.20.253/24|BM2|
|VLAN 30|10.3.30.253/24|BM3|
|VLAN 40|10.4.40.253/24|BM4|
|VLAN 101|10.0.101.253/24|ADMIN|
|Loopback0|10.1.1.1/32|-|

e. DS-2

|接口|地址|描述|
|:---:|:---:|:---:|
|G1/0/1|-|连接至AS-2 G0/2|
|G1/0/2|10.0.23.2/24|连接至Router-Edge G0/0/1|
|VLAN 10|10.1.10.252/24|BM1|
|VLAN 20|10.2.20.252/24|BM2|
|VLAN 30|10.3.30.252/24|BM3|
|VLAN 40|10.4.40.252/24|BM4|
|VLAN 101|10.0.101.252/24|ADMIN|
|Loopback0|10.2.2.2/32|-|

f. AS-4

|接口|地址|描述|
|:---:|:---:|:---:|
|F0/23|-|连接至AS-5 F0/23|
|F0/24|-|连接至AS-5 F0/24|
|G0/1|-|连接至WJ-R G0/0|
|G0/2|-|连接至WEB/DHCP(Server-PT) Gig0|
|VLAN 4|10.8.4.1/24|ADMIN|
|VLAN 5|-|BM5|
|VLAN 6|-|BM6|
|VLAN 7|-|BM7|

g. AS-5

|接口|地址|描述|
|:---:|:---:|:---:|
|F0/23|-|连接至AS-4 F0/23|
|F0/24|-|连接至AS-4 F0/24|
|VLAN 4|10.8.4.2/24|ADMIN|
|VLAN 5|-|BM5|
|VLAN 6|-|BM6|
|VLAN 7|-|BM7|

#### 3. 路由设备地址规划

a. Router-Edge

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/0/0|10.0.13.3/23|连接至DS-1 G1/0/2|
|G0/0/1|10.0.23.3/23|连接至DS-2 G1/0/2|
|S0/2/0|218.12.17.1/30|连接至ISP-1 S0/0/0|
|VLAN 100|10.5.100.254/24|BM5|
|VLAN 200|10.6.200.254/24|BM6|
|Tunnel 0|10.10.10.1/30|-|
|Loopback0|10.3.3.3/32|-|

b. WJ-R

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/0/0|218.12.18.1/30|连接至ISP-1 G0/2/0|
|G0/0/1|-|连接至AS-4 G0/1|
|G0/0.4|10.8.4.254/24|-|
|G0/0.5|10.8.5.254/24|-|
|G0/0.6|10.8.6.254/24|-|
|G0/0.7|10.8.7.254/24|-|
|Tunnel 0|10.10.10.2/30|-|

c. ISP-1

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/2/0|218.12.18.2/30|连接至WJ-R G0/0/0|
|S0/0/0|218.12.17.2/30|连接至Router-Edge S0/2/0|
|Loopback0|200.200.200.200/32|-|

#### 4. 终端设备地址规划

|名称|接口|地址|描述|
|:---:|:---:|:---:|:---:|
|PC11、PC12、PC13|网卡|DHCP|-|
|PC21、PC22、PC23|网卡|DHCP|-|
|PC31、PC32、PC33|网卡|DHCP|-|
|PC41、PC42、PC43|网卡|DHCP|-|
|PC51、PC52|网卡|DHCP|-|
|PC61、PC62|网卡|DHCP|-|
|WEB|网卡|10.5.100.253/24|连接至Router-Edge G0/1/0|
|DNS|网卡|10.5.100.252/24|连接至Router-Edge G0/1/1|
|E-MAIL|网卡|10.6.200.253/24|连接至Router-Edge G0/1/2|
|FTP|网卡|10.6.200.252/24|连接至Router-Edge G0/1/3|
|WEB/DHCP|网卡|10.8.7.253/24|连接至AS-4 G0/2|

### 四、测试

详见[测试结果（test_results.md）](test_results.md)。

### 五、运行

查阅[思科网络学院有关Cisco Packet Tracer的介绍](https://www.netacad.com/cisco-packet-tracer)并按步骤操作即可获取最新版Cisco Packet Tracer软件。

请使用Cisco Packet Tracer 9.0.0或未来版本打开`switched_enterprise_network.pkt`即可查看、测试和修改。对于旧版本Cisco Packet Tracer的兼容性未知，请自行参阅官方文档。
