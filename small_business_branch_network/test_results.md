> *You are here: TEST_RESULTS file for small_business_branch_network in cpt-projects.*
>
> Note before reading:
>
> 1. The content of the README is written in **Simplified Chinese**.
>
> 2. Due to limited ability and time, mistakes are inevitable in the project. I would be most grateful if you could share your insights with me or point out any mistakes!

### 网络测试

#### 1. 终端连通性

a. PC11 `ping` PC42：

```shell
C:\>ping 10.1.40.2

Pinging 10.1.40.2 with 32 bytes of data:

Reply from 10.1.40.2: bytes=32 time<1ms TTL=127
Reply from 10.1.40.2: bytes=32 time=1ms TTL=127
Reply from 10.1.40.2: bytes=32 time<1ms TTL=127
Reply from 10.1.40.2: bytes=32 time<1ms TTL=127

Ping statistics for 10.1.40.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

b. PC22 `ping` PC31：

```shell
C:\>ping 10.1.30.1

Pinging 10.1.30.1 with 32 bytes of data:

Reply from 10.1.30.1: bytes=32 time<1ms TTL=127
Reply from 10.1.30.1: bytes=32 time<1ms TTL=127
Reply from 10.1.30.1: bytes=32 time=1ms TTL=127
Reply from 10.1.30.1: bytes=32 time<1ms TTL=127

Ping statistics for 10.1.30.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

c. PC12 `ping` Public PC：

```shell
C:\>ping 200.200.200.253

Pinging 200.200.200.253 with 32 bytes of data:

Reply from 200.200.200.253: bytes=32 time<1ms TTL=124
Reply from 200.200.200.253: bytes=32 time<1ms TTL=124
Reply from 200.200.200.253: bytes=32 time<1ms TTL=124
Reply from 200.200.200.253: bytes=32 time<1ms TTL=124

Ping statistics for 200.200.200.253:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

d. PC52 `ping` Public PC：

```shell
C:\>ping 200.200.200.253

Pinging 200.200.200.253 with 32 bytes of data:

Reply from 200.200.200.253: bytes=32 time<1ms TTL=125
Reply from 200.200.200.253: bytes=32 time<1ms TTL=125
Reply from 200.200.200.253: bytes=32 time<1ms TTL=125
Reply from 200.200.200.253: bytes=32 time<1ms TTL=125

Ping statistics for 200.200.200.253:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

e. PC32 `ping` PC52：

```shell
C:\>ping 10.8.5.2

Pinging 10.8.5.2 with 32 bytes of data:

Reply from 10.8.5.2: bytes=32 time<1ms TTL=125
Reply from 10.8.5.2: bytes=32 time<1ms TTL=125
Reply from 10.8.5.2: bytes=32 time<1ms TTL=125
Reply from 10.8.5.2: bytes=32 time<1ms TTL=125

Ping statistics for 10.8.5.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

#### 2. 远程登录

a. 在Public PC上登录R-Edge：

```shell
C:\>ssh -l ray 218.12.10.1

Password: 



DS1>
```

b. 在Public PC上登录ISP：

```shell
C:\>ssh -l ray 218.12.10.2

Password: 



ISP>
```

c. 在Public PC上登录QD-Router：

```shell
C:\>ssh -l ray 218.12.11.2

Password: 



QD-Router>
```

#### 3. 网站访问

a. 在PC11上访问www.ray.edu.cn的主页：

![image](https://s41.ax1x.com/2026/01/24/pZ2p9cq.png)

b. 在PC11上访问www.ray.com的主页：

![image](https://s41.ax1x.com/2026/01/24/pZ2pFBT.png)

c. 在PC61上访问www.ray.edu.cn的其它页面：

![image](https://s41.ax1x.com/2026/01/24/pZ2pZ4J.png)

d. 在PC61上访问www.ray.com的其它页面：

![image](https://s41.ax1x.com/2026/01/24/pZ2pmC9.png)

#### 4. 文件备份

a. 在AS-1上将文件备份到内网的TFTP服务器上：

```shell
AS-1#copy startup-config tftp: 
Address or name of remote host []? 10.3.100.6
Destination filename [AS-1-confg]? 

Writing startup-config....!!
[OK - 2540 bytes]

2540 bytes copied in 3.003 secs (845 bytes/sec)
```

b. 在AS-2上将文件备份到内网的TFTP服务器上：

```shell
AS-2#copy startup-config tftp:
Address or name of remote host []? 10.3.100.6
Destination filename [AS-2-confg]? 

Writing startup-config....!!
[OK - 2540 bytes]

2540 bytes copied in 3.002 secs (846 bytes/sec)
```

c. 在DS1上将文件备份到内网的TFTP服务器上：

```shell
DS1#copy startup-config tftp: 
Address or name of remote host []? 10.3.100.6
Destination filename [DS1-confg]? 

Writing startup-config...!!
[OK - 2488 bytes]

2488 bytes copied in 0 secs
```

d. 在R-Edge上将文件备份到内网的TFTP服务器上：

```shell
R-Edge#copy startup-config tftp: 
Address or name of remote host []? 10.3.100.6
Destination filename [R-Edge-confg]? 

Writing startup-config...!!
[OK - 1495 bytes]

1495 bytes copied in 0 secs
```

e. 在ISP上将文件备份到内网的TFTP服务器上：

```shell
ISP#copy startup-config tftp: 
Address or name of remote host []? 218.12.10.1
Destination filename [ISP-confg]? 

Writing startup-config...!!
[OK - 1155 bytes]

1155 bytes copied in 0.001 secs (1155000 bytes/sec)
```

f. 在DS2上将文件备份到内网的TFTP服务器上：

```shell
DS2#copy startup-config tftp: 
Address or name of remote host []? 218.12.10.1
Destination filename [DS2-confg]? 

Writing startup-config...!!
[OK - 1721 bytes]

1721 bytes copied in 0 secs
```

g. 在QD-Router上将文件备份到内网的TFTP服务器上：

```shell
QD-Router#copy startup-config tftp: 
Address or name of remote host []? 218.12.10.1
Destination filename [QD-Router-confg]? 

Writing startup-config...!!
[OK - 1852 bytes]

1852 bytes copied in 0 secs
```

h. 在AS2-1上将文件备份到内网的TFTP服务器上：

```shell
AS2-1#copy startup-config tftp: 
Address or name of remote host []? 10.3.100.6
Destination filename [AS2-1-confg]? 

Writing startup-config...!!
[OK - 2571 bytes]

2571 bytes copied in 0 secs
```

