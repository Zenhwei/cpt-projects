> *You are here: TEST_RESULTS file for simple_micro_campus_network in cpt-projects.*
>
> Note before reading:
>
> 1. The content of the README is written in **Simplified Chinese**.
>
> 2. Due to limited ability and time, mistakes are inevitable in the project. I would be most grateful if you could share your insights with me or point out any mistakes!

### 网络测试

#### 1. DHCP测试

a. 将PC1（属于部门A）的IP Configuration设定为DHCP，发现：

|IPv4地址|掩码|默认网关|DNS服务器|
|:---:|:---:|:---:|:---:|
|192.168.10.1|255.255.255.0|192.168.10.254|192.168.50.1|

DHCP获取正常。

b. 将PC2（属于部门A）的IP Configuration设定为DHCP，发现：

|IPv4地址|掩码|默认网关|DNS服务器|
|:---:|:---:|:---:|:---:|
|192.168.10.2|255.255.255.0|192.168.10.254|192.168.50.1|

DHCP获取正常。

c. 将PC5（属于部门C）的IP Configuration设定为DHCP，发现：

|IPv4地址|掩码|默认网关|DNS服务器|
|:---:|:---:|:---:|:---:|
|192.168.30.1|255.255.255.0|192.168.30.254|192.168.50.1|

DHCP获取正常。

*其他部门的PC测试结果与上类同，均成功获取了配置。*

#### 2. 各部门PC之间的连通性测试

a. 部门B的PC4（192.168.20.2）`ping`部门D的PC7（192.168.40.1），发现：

```shell
C:\>ping 192.168.40.1
Pinging 192.168.40.1 with 32 bytes of data:

Reply from 192.168.40.1: bytes=32 time<1ms TTL=125
Reply from 192.168.40.1: bytes=32 time<1ms TTL=125
Reply from 192.168.40.1: bytes=32 time<1ms TTL=125
Reply from 192.168.40.1: bytes=32 time<1ms TTL=125

Ping statistics for 192.168.40.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

PC4与PC7连通正常。

b. 部门C的PC5（192.168.30.1）`ping`部门A的PC2（192.168.10.2），发现：

```shell
C:\>ping 192.168.10.2

Pinging 192.168.10.2 with 32 bytes of data:

Reply from 192.168.10.2: bytes=32 time<1ms TTL=125
Reply from 192.168.10.2: bytes=32 time=1ms TTL=125
Reply from 192.168.10.2: bytes=32 time<1ms TTL=125
Reply from 192.168.10.2: bytes=32 time<1ms TTL=125

Ping statistics for 192.168.10.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

PC5与PC2连通正常。

*其他部门的PC测试结果与上类同，均成功连通。*

#### 3. 各部门PC与园区服务器（Server2和Server3）的连通性测试

a. 部门A的PC1（192.168.10.1）`ping`Server2（192.168.50.1），发现：

```shell
C:\>ping 192.168.50.1

Pinging 192.168.50.1 with 32 bytes of data:

Reply from 192.168.50.1: bytes=32 time=1ms TTL=126
Reply from 192.168.50.1: bytes=32 time<1ms TTL=126
Reply from 192.168.50.1: bytes=32 time<1ms TTL=126
Reply from 192.168.50.1: bytes=32 time=1ms TTL=126

Ping statistics for 192.168.50.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

PC1与Server2连通正常。

b. 部门B的PC4（192.168.20.2）`ping`Server3（192.168.50.2），发现：

```shell
C:\>ping 192.168.50.2

Pinging 192.168.50.2 with 32 bytes of data:

Reply from 192.168.50.2: bytes=32 time<1ms TTL=126
Reply from 192.168.50.2: bytes=32 time=1ms TTL=126
Reply from 192.168.50.2: bytes=32 time<1ms TTL=126
Reply from 192.168.50.2: bytes=32 time<1ms TTL=126

Ping statistics for 192.168.50.2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

PC4与Server3连通正常。

*其他部门PC与Server2和Server3的连通测试结果与上类同，均成功连通。*

#### 4. 各部门PC访问Intranet WEB服务器（web.ray.com）和Internet WEB服务器（www.ray.cn）的测试

a. 部门C的PC6（192.168.30.2）通过Web Browser访问Intranet WEB服务器（web.ray.com）和Internet WEB服务器（www.ray.cn），发现：

|URL|结果|
|:---:|:---:|
|web.ray.com|加载了预先编写的HTML页面，成功访问。|
|www.ray.cn|加载了预先编写的HTML页面，成功访问。|

*其他部门PC访问Intranet WEB服务器和Internet WEB服务器的测试结果与上类同，均成功访问。*

#### 5. 各部门PC访问Intranet FTP服务器（ftp.ray.com）的测试

a. 部门A的PC1（192.168.10.1）通过命令行访问Intranet FTP服务器（ftp.ray.com），发现：

```shell
C:\>ftp ftp.ray.com
Trying to connect...ftp.ray.com
Connected to ftp.ray.com
220- Welcome to PT Ftp server
Username:ray
331- Username ok, need password
Password:***
230- Logged in
(passive mode On)
ftp>quit

221- Service closing control connection.
```

PC1与FTP服务器连通正常。

*其他部门PC访问Intranet FTP服务器的测试结果与上类同，均成功访问。*
