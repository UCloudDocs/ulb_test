# FAQ

### ULB支持哪些协议？对于web应用, HTTP和TCP选哪个更好？ <a id="ulb&#x652F;&#x6301;&#x54EA;&#x4E9B;&#x534F;&#x8BAE;_&#x5BF9;&#x4E8E;web&#x5E94;&#x7528;_http&#x548C;tcp&#x9009;&#x54EA;&#x4E2A;&#x66F4;&#x597D;"></a>

* ULB VServer可以创建两种模式：请求代理模式和报文转发模式。请求代理模式支持TCP和HTTP（HTTPS）等协议. 对于web应用, 首选HTTP协议, 因为ULB能理解HTTP协议, 从而能更有针对性的进行负载均衡服务, 也可以提供基于HTTP协议的主机健康检查。对性能要求非常高的场景下, web应用跑TCP协议有略微的性能优势。报文转发模式则支持TCP协议和UDP协议，性能更强。对性能有需求的用户请优先选择报文转发模式。

### ULB支持哪些转发规则？哪种更好？ <a id="ulb&#x652F;&#x6301;&#x54EA;&#x4E9B;&#x8F6C;&#x53D1;&#x89C4;&#x5219;_&#x54EA;&#x79CD;&#x66F4;&#x597D;"></a>

ULB分为请求代理和报文转发两种模式。

* 目前请求代理模式支持轮询、源地址、加权轮询、最小连接数四种算法。

1. 轮询算法下, ULB接收到新的TCP连接后, 依次转给每个后端主机。
2. 源地址算法下, ULB会根据TCP连接的源地址，利用一定的哈希算法将请求其转给某台主机。之后用户再以相同IP访问, 如主机数量不变时，访问还是会落到该台主机。
3. 加权轮询算法下，ULB接收到新的TCP连接后，将根据您指定的后端主机的不同权重，按照概率分配给各个后端主机。
4. 最小连接数算法下，ULB接受到新的TCP连接后，会实时统计ULB到后端主机的连接数，选择连接数最低的主机建立新连接并发送数据。

* 目前报文转发模式支持轮询、源地址、一致性哈希、源地址（计算端口）、一致性哈希（计算端口）、加权轮询六种算法。

1. 轮询算法。同上。
2. 源地址算法。同上。
3. 一致性哈希算法。一致性哈希算法是根据源目的IP，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。
4. 源地址（计算端口）算法。ULB会根据TCP连接的源地址和源端口，利用一定的哈希算法将请求其转给某台主机。
5. 一致性哈希（计算端口）算法。根据源目的IP、源目的端口，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。
6. 加权轮询算法。同上。

一般情况下,使用轮询算法就可以满足绝大多数负载均衡场景的需求， 您也可以根据自己的业务场景选择恰当的算法。

### ULB的会话保持是什么？服务端插入与用户定义的区别是什么？ <a id="ulb&#x7684;&#x4F1A;&#x8BDD;&#x4FDD;&#x6301;&#x662F;&#x4EC0;&#x4E48;_&#x670D;&#x52A1;&#x7AEF;&#x63D2;&#x5165;&#x4E0E;&#x7528;&#x6237;&#x5B9A;&#x4E49;&#x7684;&#x533A;&#x522B;&#x662F;&#x4EC0;&#x4E48;"></a>

会话保持是ULB提供的高级功能，可以在轮询等负载均衡算法下，保证同一个源的请求，能够落在相同的后端主机上。

* 请求代理模式下，会话保持功能是利用cookie实现的。ULB会向源端写cookie，并根据请求带有的cookie信息，直接将请求送给对应的后端主机。服务端插入指, 由负载均衡生成cookie的key. 用户定义指由用户指定特征cookie的key.
* 报文转发模式下，会话保持功能是基于连接表实现的。

### ULB是否会宕机？ <a id="ulb&#x662F;&#x5426;&#x4F1A;&#x5B95;&#x673A;"></a>

* ULB采用集群架构，基于跨可用区的分布式部署，利用BGP+ECMP实现集群的自动容灾，保证在可用区级别的灾难下，依旧可以正常工作。

### ULB是否有性能的限制，例如带宽、请求数, 连接数？ <a id="ulb&#x662F;&#x5426;&#x6709;&#x6027;&#x80FD;&#x7684;&#x9650;&#x5236;_&#x4F8B;&#x5982;&#x5E26;&#x5BBD;_&#x8BF7;&#x6C42;&#x6570;_&#x8FDE;&#x63A5;&#x6570;"></a>

ULB的带宽是存在上限的，其带宽由EIP的带宽决定。由于ULB服务器的性能限制，单个ULB实例能够承载的带宽上限为4Gbps左右。

* 如果您使用的是ULB的请求代理模式，则每个ULB实例能支持HTTP请求的每秒新建连接数上限为8万；HTTPS每秒新建连接数上限为8千,至少可以支撑40万的并发连接。
* 如果您使用的是ULB的报文转发模式，则每个ULB实例能够支持40万每秒新建连接数，1000万包量，超过5000万并发连接。

### 为什么对ULB压测时会出现连接失败？ <a id="&#x4E3A;&#x4EC0;&#x4E48;&#x5BF9;ulb&#x538B;&#x6D4B;&#x65F6;&#x4F1A;&#x51FA;&#x73B0;&#x8FDE;&#x63A5;&#x5931;&#x8D25;"></a>

* 通常情况下，在使用Linux操作系统作为压测模拟客户端时，当压测性能达到ULB极限前，不会出现连接失败的情况。
* 但对于使用Windows作为压测的模拟客户端时，可能会出现TCP连接失败的问题。这是由于在压测场景下，Windows系统会快速复用客户端IP和端口发起TCP连接的建立，而在被压测ULB的后端Linux服务节点上TCP协议栈中，以相同的源地址及端口所建立的TCP连接可能尚未被释放完毕，若此时如果 "新建连接的序列号" 大于 "已存在连接的序列号"，Linux服务节点就会认为新建连接的SYN请求是已存在连接的重传，从而导致新的TCP连接建立失败。
* 所以在对ULB进行压测时，请尽量使用Linux作为压测模拟客户端，如果必须使用Windows系统作为压测模拟客户端，则需添加系统注册表中关于TCP时间戳的选项，该选项默认在Windows系统中是未激活的，具体配置参见 [Windows帮助文档](https://technet.microsoft.com/en-us/library/cc938205.aspx) 。

### web console中的"运行"状态, 是指什么? 怎样知道后端某台服务器的状态？ <a id="web_console&#x4E2D;&#x7684;_&#x8FD0;&#x884C;_&#x72B6;&#x6001;_&#x662F;&#x6307;&#x4EC0;&#x4E48;_&#x600E;&#x6837;&#x77E5;&#x9053;&#x540E;&#x7AEF;&#x67D0;&#x53F0;&#x670D;&#x52A1;&#x5668;&#x7684;&#x72B6;&#x6001;"></a>

* "运行"是指整个负载均衡的状态, 只要后端服务器有一台存活, 负载均衡还是运行状态. 后端服务器的状态通过绿色/红色指示灯表示. 要注意的是, 后端状态由负载均衡健康检查确定. 如果健康检查失败, 即使服务器还能ping通, 也认为是宕机.

### 为什么我使用了轮询, 但后端web server的日志中计算出的请求数不同？ <a id="&#x4E3A;&#x4EC0;&#x4E48;&#x6211;&#x4F7F;&#x7528;&#x4E86;&#x8F6E;&#x8BE2;_&#x4F46;&#x540E;&#x7AEF;web_server&#x7684;&#x65E5;&#x5FD7;&#x4E2D;&#x8BA1;&#x7B97;&#x51FA;&#x7684;&#x8BF7;&#x6C42;&#x6570;&#x4E0D;&#x540C;"></a>

* 负载均衡的轮询算法是针对连接的。同一个TCP连接,不会被同时负载到两台后端服务器。如果同一个连接上会发送数量不确定的多个请求，则可能会导致后端服务器上统计到的请求数不同。

### 目前ULB提供哪些监控信息？ <a id="&#x76EE;&#x524D;ulb&#x63D0;&#x4F9B;&#x54EA;&#x4E9B;&#x76D1;&#x63A7;&#x4FE1;&#x606F;"></a>

* 负载均衡提供出口带宽，VServer连接数，每秒新建连接数，包量，带宽以及后端节点健康检查监控。

### ULB是否支持SSL, 我该如何配置？ <a id="ulb&#x662F;&#x5426;&#x652F;&#x6301;ssl_&#x6211;&#x8BE5;&#x5982;&#x4F55;&#x914D;&#x7F6E;"></a>

* 支持SSL协议. 目前有两种可用的SSL支持模式：

  1、SSL Offloading, 即将SSL密钥配置在负载均衡设备上, 在请求量十分巨大时, 使用特殊的硬件设备优化SSL处理, 减少后端服务器的CPU压力. 缺点是需要把SSL密钥交给负载均衡设备, 降低安全性. 在这种模式下, 请将VServer的端口配置为443\(或您自定义的SSL端口\), 绑定SSL证书到VServer, 后端云主机的端口为正常服务监听的端口\(例如HTTP服务时, 主机池中的后端云主机请监听在80\).   
  2、后端云主机处理SSL证书. 在这种模式下, 请配置VServer的协议为TCP协议, VServer端口配置为443\(或您自定义的SSL端口\), 主机池中的后端云主机也需要监听在443端口\(或您自定义的SSL端口\).

### ULB目前是proxy模式还是类似LVS采用的NAT模式的? <a id="ulb&#x76EE;&#x524D;&#x662F;proxy&#x6A21;&#x5F0F;&#x8FD8;&#x662F;&#x7C7B;&#x4F3C;lvs&#x91C7;&#x7528;&#x7684;nat&#x6A21;&#x5F0F;&#x7684;"></a>

* ULB的请求代理模式是proxy模式，而报文转发则是DR模式。

### ULB如何获取客户端的源地址？ <a id="ulb&#x5982;&#x4F55;&#x83B7;&#x53D6;&#x5BA2;&#x6237;&#x7AEF;&#x7684;&#x6E90;&#x5730;&#x5740;"></a>

* ULB在创建VServer的时候，有两种模式可以选择，一种是请求代理模式，支持tcp/http/https等模式，一种是报文转发模式，支持tcp/udp模式。如果VServer使用的是请求代理模式，ULB已经默认开启了x-Forwarded-For选项，可以从HTTP报头中的X-Forward-For字段中获取客户端的源地址。如果VServer使用的是报文转发模式，那么后端Backend收到的请求的源地址就是实际的源地址。

### ULB后的HTTP服务, 如何配置才能取到客户端IP？ <a id="ulb&#x540E;&#x7684;http&#x670D;&#x52A1;_&#x5982;&#x4F55;&#x914D;&#x7F6E;&#x624D;&#x80FD;&#x53D6;&#x5230;&#x5BA2;&#x6237;&#x7AEF;ip"></a>

采用标准的X-Fowarded-For字段即可获取, 在web服务器上修改日志的格式即可

```text
# Nginx示例
log_format  upstream  '$time_iso8601 $http_x_forwarded_for $host $upstream_response_time $request $status $upstream_addr';

# Apache示例
SetEnvIf REMOTE_ADDR "(.+)" CLIENTIP=$1
SetEnvIf X-Forwarded-For "^([0-9.]+)" CLIENTIP=$1
LogFormat "%{CLIENTIP}e %D %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" trueip_combined
CustomLog logs/access_log trueip_combined

# tomcat 的server.xml文件修改如下参数：
    <Host name="localhost" appBase="webapps" 
        unpackWARs="true" autoDeploy="true"> 
        <Valve className="org.apache.catalina.valves.AccessLogValve" 
        directory="logs" 
        prefix="tomcat_access." 
        suffix=".log" 
       pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/> 
</Host>
```

### 经常发现ULB后端云主机的访问日志中有大量的内网IP访问，请问是正常访问么？ <a id="&#x7ECF;&#x5E38;&#x53D1;&#x73B0;ulb&#x540E;&#x7AEF;&#x4E91;&#x4E3B;&#x673A;&#x7684;&#x8BBF;&#x95EE;&#x65E5;&#x5FD7;&#x4E2D;&#x6709;&#x5927;&#x91CF;&#x7684;&#x5185;&#x7F51;ip&#x8BBF;&#x95EE;_&#x8BF7;&#x95EE;&#x662F;&#x6B63;&#x5E38;&#x8BBF;&#x95EE;&#x4E48;"></a>

* 这是正常的，因为 ULB在请求代理模式下，对后端云主机转发请求时，使用的是 ULB的内网代理IP。例如，用户在北京二的后端云主机访问日志中发现大量来自 10.10.251.0/24 网段的访问，实际上就是北京二 ULB 的内网代理 IP。 ULB 在各个区域的网段见[公共服务网段](https://docs.ucloud.cn/network/vpc/limit)。

### 我想禁止某些源地址访问我的后端主机，ULB能做到访问控制吗？ <a id="&#x6211;&#x60F3;&#x7981;&#x6B62;&#x67D0;&#x4E9B;&#x6E90;&#x5730;&#x5740;&#x8BBF;&#x95EE;&#x6211;&#x7684;&#x540E;&#x7AEF;&#x4E3B;&#x673A;_ulb&#x80FD;&#x505A;&#x5230;&#x8BBF;&#x95EE;&#x63A7;&#x5236;&#x5417;"></a>

目前ULB暂时不能做到防火墙功能，只能针对端口进行管理，但是可以通过修改Web server的配置对来源地址进行限制。 由于在ULB的HTTP模式下，真实源地址保存在HTTP消息的"X-Forwarded-For"字段中，目前大部分Web server对该字段都提供了屏蔽功能。 所以，如果用户急需要对某些源地址进行屏蔽，可以参考以下配置文件范例：

* 配置Apache屏蔽某源地址

参考下面的内容修改配置文件:

```markup
<Directory "/var/www/html">
#忽略其他配置
Order deny, allow
SetEnvIf X-Forwarded-For "^(192\.168\.0\.1)$" deny1
SetEnvIf X-Forwarded-For "^(172\.16\.0\.1)$" deny2
Deny from env=deny1
Deny from env=deny2
</Directory>
```

"Order deny, allow"的顺序可以根据使用方式自定义。 "SetEnvIf"用来定义一个环境变量。这里将"X-Forwarded-For"字段作为一个变量，并使用了一个正则表达式匹配某IP\(192.168.0.1\)。 后续的Deny将根据该变量将所匹配IP进行屏蔽。

* 配置Nginx屏蔽某源地址

参考下面的内容修改配置文件：

```text
set_real_ip_from  10.10.192.0/18;
real_ip_header X-Forwarded-For;
deny 192.168.0.1
```

其中"set\_real\_ip\_from"资源的"10.10.192.0/18"IP地址为北京二可用区C的ULB所在网段地址。 nginx会将来源为该网段的"X-Forwarded-For"作为真实IP地址。 deny后面的IP，既为所需要屏蔽的IP地址。

### 我想要使用websocket，请问如何支持？ <a id="&#x6211;&#x60F3;&#x8981;&#x4F7F;&#x7528;websocket_&#x8BF7;&#x95EE;&#x5982;&#x4F55;&#x652F;&#x6301;"></a>

* ULB默认支持websocket协议。

### 内网ULB的IP地址为何无法ping通？ <a id="&#x5185;&#x7F51;ulb&#x7684;ip&#x5730;&#x5740;&#x4E3A;&#x4F55;&#x65E0;&#x6CD5;ping&#x901A;"></a>

* 内网ULB仅保证支持同子网能ping通，您可以依靠端口的测试来确认内网ULB是否配置和工作正常。

### ULB报文转发监听端口和后端服务器监听端口不一致怎么办？ <a id="ulb&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x76D1;&#x542C;&#x7AEF;&#x53E3;&#x548C;&#x540E;&#x7AEF;&#x670D;&#x52A1;&#x5668;&#x76D1;&#x542C;&#x7AEF;&#x53E3;&#x4E0D;&#x4E00;&#x81F4;&#x600E;&#x4E48;&#x529E;"></a>

* 可以通过VM内配置IpTables端口转发规则实现，具体步骤如下：

1、修改/etc/sysctl.conf配置文件，设置 net.ipv4.ip\_forward = 1 默认是0。  
2、关闭防火墙 service iptables stop。  
3、配置规则：

```text
iptables -t nat -A PREROUTING –d $vip_ip -p tcp --dport $ulb4_port  -j DNAT --to-destination $vip_ip:$vm_port
```

其中：$vip\_ip指负载均衡器的内网IP，$ulb4\_port指ulb4的监听端口，$vm\_port为后端服务器的监听端口 例：负载均衡器的内网IP为：10.10.10.10，ulb\_4监听端口为80，后端服务器监听端口为8101，则规则为：

```text
iptables -t nat -A PREROUTING -d 10.10.10.10 -p tcp --dport 80 -j DNAT --to-destination 10.10.10.10:8101
```

4、保存配置：service iptables save  
5、启动iptables ：service iptables start

