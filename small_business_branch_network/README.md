> *You are here: README file for small_business_branch_network in cpt-projects.*
>
> Note before reading:
>
> 1. The content of the README is written in **Simplified Chinese**.
>
> 2. Due to limited ability and time, mistakes are inevitable in the project. I would be most grateful if you could share your insights with me or point out any mistakes!

### 一、快速介绍

1. 项目名称：**构建小型企业分支网络**

2. 功能与服务：直连路由、静态路由、RIPV2、路由重分布和单臂路由；VLAN、Trunk和SVI；特权密码、口令加密、Telnet和SSH；WEB、DNS、DHCP和TFTP；NAT和GRE VPN。

### 二、设备列表与拓扑

|类别|型号|数量|备注|
|:---:|:---:|:---:|:---:|
|计算机|PC-PT|13|暂无|
|服务器|Server-PT|4|暂无|
|交换机|2960-24TT|3|AS-1、AS-2、AS2-1|
|交换机|3650-24PS|2|DS1、DS2|
|路由器|1941|1|QD-Router|
|路由器|2901|1|R-Edge|
|路由器|2911|1|ISP|

![拓扑图](topo.png)

### 三、网络规划

#### 1. VLAN规划

|ID|名称|设备|接口|
|:---:|:---:|:---:|:---:|
|VLAN 10|TEACHER|AS-1|F0/1-12|
|VLAN 20|STUDENT|AS-1|F0/13-24|
|VLAN 30|STAFF|AS-2|F0/1-12|
|VLAN 40|WORKER|AS-2|F0/13-24|
|VLAN 99|ADMIN|AS-1、AS-2、AS2-1|-|
|VLAN 100|SERVER|DS1|G1/0/4-6|
|VLAN 5|BM1|AS2-1|F0/1-12|
|VLAN 6|BM2|AS2-1|F0/13-24|

#### 2. 交换设备地址规划

a. DS1

|接口|地址|描述|
|:---:|:---:|:---:|
|G1/0/1|-|连接至AS-1 G0/1|
|G1/0/2|-|连接至AS-2 G0/1|
|G1/0/3|10.0.100.2/30|连接至R-Edge G0/0|
|G1/0/4|-|连接至WEB Server（www.ray.edu.cn）|
|G1/0/5|-|连接至DNS Server|
|G1/0/6|-|连接至DHCP/TFTP Server|
|VLAN 10|10.1.10.254/24|TEACHER|
|VLAN 20|10.1.20.254/24|STUDENT|
|VLAN 30|10.1.30.254/24|STAFF|
|VLAN 40|10.1.40.254/24|WORKER|
|VLAN 99|10.0.12.254/24|ADMIN|
|VLAN 100|10.3.100.254/24|SERVER|

b. AS-1

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至DS1 G1/0/1|
|F0/1|-|连接至PC11 Fa0|
|F0/2|-|连接至PC12 Fa0|
|F0/13|-|连接至PC21 Fa0|
|F0/14|-|连接至PC22 Fa0|
|VLAN 10|-|TEACHER|
|VLAN 20|-|STUDENT|
|VLAN 99|10.0.12.1/24|ADMIN|

c. AS-2

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至DS1 G1/0/2|
|F0/1|-|连接至PC31 Fa0|
|F0/2|-|连接至PC32 Fa0|
|F0/13|-|连接至PC41 Fa0|
|F0/14|-|连接至PC42 Fa0|
|VLAN 30|-|STAFF|
|VLAN 40|-|WORKER|
|VLAN 99|10.0.12.2/24|ADMIN|

d. DS2

|接口|地址|描述|
|:---:|:---:|:---:|
|G1/1/1|217.9.5.2/30|连接至ISP G0/1/0|
|G1/1/2|222.138.4.254/30|连接至WEB Server（www.ray.com） Gig0|
|G1/1/3|200.200.200.254/30|连接至Public PC Gig0|

e. AS2-1

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/1|-|连接至QD-Router G0/0|
|F0/1|-|连接至PC51 Fa0|
|F0/2|-|连接至PC52 Fa0|
|F0/13|-|连接至PC61 Fa0|
|F0/14|-|连接至PC62 Fa0|
|VLAN 5|-|BM1|
|VLAN 6|-|BM2|
|VLAN 99|10.8.0.100/24|ADMIN|

#### 3. 路由设备地址规划

a. R-Edge

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/0/0|218.12.10.1/30|连接至ISP G0/0/0|
|G0/0|10.0.100.1/30|连接至DS1 Gig1/0/3|
|Tunnel 1|192.168.12.1/30|连接至QD-Router Tunnel 1|

b. QD-Router

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/0/0|218.12.11.2/30|连接至ISP G0/2/0|
|G0/0|-|连接至AS2-1 Gig0/1|
|Tunnel 1|192.168.12.2/30|连接至R-Edge Tunnel 1|
|VLAN 5|10.8.5.254/24|-|
|VLAN 6|10.8.6.254/24|-|
|VLAN 99|10.8.0.254/24|-|

#### 4. ISP设备地址规划

|接口|地址|描述|
|:---:|:---:|:---:|
|G0/0/0|218.12.10.2/30|连接至R-Edge G0/0/0|
|G0/1/0|217.9.5.1/30|连接至DS2 G1/1/1|
|G0/2/0|218.12.11.1/30|连接至QD-Router G0/0/0|

#### 5. 终端设备地址规划

|名称|接口|地址|描述|
|:---:|:---:|:---:|:---:|
|PC*x*|网卡|DHCP|-|
|WEB Server（www.ray.com）|网卡|222.138.4.253/30|连接至DS2 G1/1/2|
|Public PC|网卡|200.200.200.253/30|连接至DS2 G1/1/3|
|WEB Server（www.ray.edu.cn）|网卡|10.3.100.4/24|连接至DS1 G1/0/4|
|DNS Server|网卡|10.3.100.5/24|连接至DS1 G1/0/5|
|DHCP/TFTP Server|网卡|10.3.100.6/24|连接至DS1 G1/0/6|

### 四、测试

详见[测试结果（test_results.md）](test_results.md)。

### 五、运行

查阅[思科网络学院有关Cisco Packet Tracer的介绍](https://www.netacad.com/cisco-packet-tracer)并按步骤操作即可获取最新版Cisco Packet Tracer软件。

请使用Cisco Packet Tracer 9.0.0或未来版本打开`small_business_branch_network.pkt`即可查看、测试和修改。对于旧版本Cisco Packet Tracer的兼容性未知，请自行参阅官方文档。
