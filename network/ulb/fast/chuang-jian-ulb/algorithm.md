{{indexmenu_n>5}}

# 负载均衡算法

### 负载均衡算法

* **轮询**。ULB接收到新的TCP连接后, 依次转给每个后端主机。
* **源地址**。ULB会根据TCP连接的源地址，利用一定的哈希算法将请求其转给某台主机。之后用户再以相同IP访问, 如主机数量不变时，访问还是会落到该台主机。
* **源地址（计算端口）**。ULB会根据TCP连接的源地址和源端口，利用一定的哈希算法将请求其转给某台主机。（仅报文转发模式支持）
* **一致性哈希。**一致性哈希算法是根据源目的IP，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。（仅报文转发模式支持）
* **一致性哈希（计算端口）**。根据源目的IP、源目的端口，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。（仅报文转发模式支持）
* **加权轮询。**ULB接收到新的TCP连接后，将根据您指定的后端主机的不同权重，按照概率分配给各个后端主机。
* **最小连接数**。ULB接受到新的TCP连接后，会实时统计ULB到后端主机的连接数，选择连接数最低的主机建立新连接并发送数据。（仅请求代理模式支持）



增加创建描述，哪种业务场景推荐那种算法


