> *You are here: TEST_RESULTS file for switched_enterprise_network in cpt-projects.*
>
> Note before reading:
>
> 1. The content of the README is written in **Simplified Chinese**.
>
> 2. Due to limited ability and time, mistakes are inevitable in the project. I would be most grateful if you could share your insights with me or point out any mistakes!

### 网络测试

#### 1. 终端连通性

a. PC42访问WEB服务器：

![image](https://s41.ax1x.com/2026/01/31/pZhsP54.png)

b. PC61访问WEB服务器：

![image](https://s41.ax1x.com/2026/01/31/pZhsA2R.png)

c. PC12 `tracert` 公网环回地址：

```shell
C:\>tracert 200.200.200.200

Tracing route to 200.200.200.200 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      10.1.10.253
  2   0 ms      0 ms      0 ms      10.0.13.3
  3   0 ms      1 ms      0 ms      200.200.200.200

Trace complete.
```

d. PC21 `tracert` 公网环回地址：

```shell
C:\>tracert 200.200.200.200

Tracing route to 200.200.200.200 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      10.2.20.252
  2   0 ms      0 ms      0 ms      10.0.13.3
  3   1 ms      1 ms      1 ms      200.200.200.200

Trace complete.
```

e. PC51 `ping` 公网环回地址：

```shell
C:\>ping 200.200.200.200

Pinging 200.200.200.200 with 32 bytes of data:

Reply from 200.200.200.200: bytes=32 time<1ms TTL=254
Reply from 200.200.200.200: bytes=32 time<1ms TTL=254
Reply from 200.200.200.200: bytes=32 time<1ms TTL=254
Reply from 200.200.200.200: bytes=32 time<1ms TTL=254

Ping statistics for 200.200.200.200:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

#### 2. 远程登录

a. 在PC43上 `telnet` DS-2：

```shell
C:\>telnet 10.2.2.2
Trying 10.2.2.2 ...Open


User Access Verification

Username: ray
Password: 
DS-2>enable
Password: 
DS-2#
```

#### 3. 文件备份

a. 将交换机AS-1的配置文件备份到FTP服务器上：

```shell
AS-1#copy startup-config ftp: 
Address or name of remote host []? 10.6.200.252
Destination filename [AS-1-confg]? 

Writing startup-config...
[OK - 1707 bytes]

1707 bytes copied in 0.01 secs (170000 bytes/sec)
```

b. 将路由器Router-Edge的配置文件备份到FTP服务器上：

```shell
Router-Edge#copy startup-config ftp: 
Address or name of remote host []? 10.6.200.252
Destination filename [Router-Edge-confg]? 

Writing startup-config...
[OK - 2350 bytes]

2350 bytes copied in 0.01 secs (235000 bytes/sec)
```

#### 4. 软件防火墙

a. 配置DNS服务器防火墙前在PC11上进行的 `ping` 测试：

```shell
C:\>ping 10.5.100.252

Pinging 10.5.100.252 with 32 bytes of data:

Reply from 10.5.100.252: bytes=32 time<1ms TTL=126
Reply from 10.5.100.252: bytes=32 time<1ms TTL=126
Reply from 10.5.100.252: bytes=32 time<1ms TTL=126
Reply from 10.5.100.252: bytes=32 time<1ms TTL=126

Ping statistics for 10.5.100.252:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

b. 配置DNS服务器防火墙后再次在PC11上进行的 `ping` 测试：

```shell
C:\>ping 10.5.100.252

Pinging 10.5.100.252 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 10.5.100.252:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```

#### 5. VTY限制

a. PC11 `telnet` DS-1：

```shell
C:\>telnet 10.1.1.1
Trying 10.1.1.1 ...Open

[Connection to 10.1.1.1 closed by foreign host]
```

b. PC41 `telnet` DS-1：

```shell
C:\>telnet 10.1.1.1
Trying 10.1.1.1 ...Open


User Access Verification

Username: ray
Password: 
DS-1>en
Password: 
DS-1#
```

#### 6. 扩展ACL

a. PC11无法访问FTP服务器：

```shell
C:\>ftp 10.6.200.252
Trying to connect...10.6.200.252

%Error opening ftp://10.6.200.252/ (Timed out)
.



(Disconnecting from ftp server)
```

b. PC31可以访问FTP服务器：

```shell
C:\>ftp 10.6.200.252
Trying to connect...10.6.200.252
Connected to 10.6.200.252
220- Welcome to PT Ftp server
Username:ray
331- Username ok, need password
Password:***
230- Logged in
(passive mode On)
ftp>dir

Listing /ftp directory from 10.6.200.252: 
0   : AS-1-confg                                         1707
1   : AS-2-confg                                         1667
2   : AS-3-confg                                         1667
3   : AS-4-confg                                         2563
4   : AS-5-confg                                         2497
5   : DS-1-confg                                         3300
6   : DS-2-confg                                         3422
7   : Router-Edge-confg                                  2350
8   : WJ-R-confg                                         1512
```
