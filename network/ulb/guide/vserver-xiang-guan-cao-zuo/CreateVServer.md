{{indexmenu_n>1}}

# 添加VServer

### 操作步骤 <a id="&#x521B;&#x5EFA;vserver&#x76D1;&#x542C;&#x5668;"></a>

ULB实例创建完成后，可点击**详情**进入**VServer管理页面**添加VServer。

1，在VServer管理页面中点击**添加VServer**。

2，填写配置信息，进行VServer创建。详细配置说明见下方。

[![image](https://docs.ucloud.cn/_media/network/ulb/vserver%E5%BB%BA%E7%AB%8Btcp.png)](https://docs.ucloud.cn/_detail/network/ulb/vserver%E5%BB%BA%E7%AB%8Btcp.png?id=network%3Aulb%3Acommon)

注意：外网ULB，TCP协议支持“报文转发模式”与“请求代理模式”；内网ULB，TCP协议仅支持“报文转发模式“

 [![image](https://docs.ucloud.cn/_media/network/ulb/%E6%B7%BB%E5%8A%A0vserver-tcp.png)](https://docs.ucloud.cn/_detail/network/ulb/%E6%B7%BB%E5%8A%A0vserver-tcp.png?id=network%3Aulb%3Acommon)

### 配置说明

创建VServer监听器的选项包含以下内容：

|VServer名称|	VServer监听器管理名称|
|-|-|
|VServer名称|	VServer名称，必填项。|
|协议和端口|	监听器所监听的协议及端口，包含HTTP/HTTPS/TCP/UDP四种协议。|
|监听器类型|	HTTP、HTTPS默认为请求代理模式，UDP默认为报文转发模式。外网ULB，TCP协议支持“报文转发模式”与“请求代理模式”；内网ULB，TCP协议仅支持“报文转发模式“。|
|负载均衡算法|监听器对数据包的负载方式|
|服务节点	|一般情况，添加服务节点是需要在VServer监听器创建完成后再进行。 该选项提供了从其他VServer复制服务节点池配置的方法，以便利用原有配置快速创建。|
|服务会话保持|	对于HTTP/HTTPS协议，使用默认/自定义关键词对用户登录态的保持。|
|连接保持时间|	TCP请求代理模式下，或HTTP、HTTPS协议，可选择客户端请求连接的有效时间。可选时间范围[1-86400]秒|
|节点健康检查|根据所选协议不同，检查方式包含服务地址/端口检查和HTTP检查两种方式。|


负载均衡算法包含如下几种：
- 轮询。ULB接收到新的TCP连接后, 依次转给每个后端主机。
- 源地址。ULB会根据TCP连接的源地址，利用一定的哈希算法将请求其转给某台主机。之后用户再以相同IP访问, 如主机数量不变时，访问还是会落到该台主机。
- 源地址（计算端口）。ULB会根据TCP连接的源地址和源端口，利用一定的哈希算法将请求其转给某台主机。（仅报文转发模式支持）
- 一致性哈希。一致性哈希算法是根据源目的IP，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。（仅报文转发模式支持）
- 一致性哈希（计算端口）。根据源目的IP、源目的端口，使用一致性哈希算法的结果选择后端主机。如果增加或者删减后端主机，仅仅会影响小部分连接。（仅报文转发模式支持）
- 加权轮询。ULB接收到新的TCP连接后，将根据您指定的后端主机的不同权重，按照概率分配给各个后端主机。
最小连接数。
