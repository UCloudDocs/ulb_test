# 创建VServer

### 创建VServer监听器 <a id="&#x521B;&#x5EFA;vserver&#x76D1;&#x542C;&#x5668;"></a>

完成实例创建后，页面会自动跳转到VServer管理页面。或可通过点击实例列表中的“管理”按钮进入VServer管理页面。

在VServer管理页面中点击“添加”按钮，即可进入VServer创建流程。

[![image](https://docs.ucloud.cn/_media/network/ulb/ulb5.png)](https://docs.ucloud.cn/_detail/network/ulb/ulb5.png?id=network%3Aulb%3Acommon)

[![image](https://docs.ucloud.cn/_media/network/ulb/vserver%E5%BB%BA%E7%AB%8Btcp.png)](https://docs.ucloud.cn/_detail/network/ulb/vserver%E5%BB%BA%E7%AB%8Btcp.png?id=network%3Aulb%3Acommon)

在选择TCP协议中有“报文转发模式”与“请求代理模式”两种，TCP报文转发模式目前支持内网、外网访问两种，TCP请求代理模式仅支持外网访问。 [![image](https://docs.ucloud.cn/_media/network/ulb/%E6%B7%BB%E5%8A%A0vserver-tcp.png)](https://docs.ucloud.cn/_detail/network/ulb/%E6%B7%BB%E5%8A%A0vserver-tcp.png?id=network%3Aulb%3Acommon)

创建VServer监听器的选项包含以下内容：

| VServer名称 | VServer监听器管理名称 |
| :--- | :--- |
| 监听器类型 | 在选择TCP协议中有“报文转发模式”与“请求代理模式”两种，TCP报文转发模式目前支持内网、外网访问两种，TCP请求代理模式仅支持外网访问。 |
| 协议和端口 | 监听器所监听的协议及端口，包含HTTP/HTTPS/TCP/UDP四种协议 |
| 负载均衡算法 | 监听器对数据包的负载方式，包含轮询/源地址模式，以及一致性哈希模式（仅TCP/UDP）。 |
| 服务节点 | 一般情况，添加服务节点是需要在VServer监听器创建完成后再进行。 该选项提供了从其他VServer复制服务节点池配置的方法，以便利用原有配置快速创建。 |
| 服务会话保持 | 对于http/https协议，使用默认/自定义关键词对用户登录态的保持。 |
| 连接保持时间 | 客户端请求连接的有效时间。可选时间范围\[1-86400\]秒 |
| 节点健康检查 | 根据所选协议不同，检查方式包含服务地址/端口检查和HTTP检查两种方式。 |

当节点健康检查选择HTTP检查时，负载均衡的健康检查通过HTTP HEAD探测来获取状态信息。ULB实例向后端服务节点发送HTTP HEAD请求，后端服务节点收到请求后，根据相应服务的运行情况，返回 HTTP状态码。ULB实例根据HTTP状态码判断健康检查成功或失败。

### 会话保持

针对HTTP协议、HTTPS协议（七层服务）ULB基于Cookie支持会话保持功能。用户在配置时可以选择开启会话保持功能。会话保持支持两种方式：

**Cookie插入**：选择自动生成key，客户端的cookie插入操作都由ULB来分配和管理。

**用户指定Cookie插入**：用户可自定义key，ULB使用客户的key来分配和管理对客户端进行的Cookie插入操作

针对TCP协议的报文转发模式或UDP协议时（四层服务），是基于IP地址的会话保持。ULB会将来自同一IP地址的访问请求转发到同一台后端云服务器进行处理。

TCP协议的请求代理模式，不支持会话保持。

### 健康检查

ULB健康检查可判断后端服务器是否正常，对于异常的后端服务器，ULB将其从后端服务器池中移除，客户端请求将会在其他服务器之间进行分发。对于处于异常状态的服务器恢复正常时，会被ULB恢复至后端服务器池中。

**端口检查** ULB在每个可用区内部署专用服务器对会探测后端节点的IP+端口是否正常。探测频率为1s，连续三次探测失败后端服务器状态异常，连续三次探测正常，则后端服务器状态正常。注意：数据更新有6s延迟，故健康检查状态或有6s延迟。

![VServer&#x914D;&#x7F6E;&#x754C;&#x9762;](../../../.gitbook/assets/image%20%284%29.png)

所有协议均支持端口检查。但检测状态略有不同：HTTP、HTTPS以及TCP的请求代理模式的端口检查是用TCP进行探测。而TCP的报文转发模式及UDP协议则是使用选择的四层协议做端口探测。

**HTTP检查** 通过HTTP HEAD请求检查后端服务器上的应用是否可用。要求后端服务器支持HEAD请求。

用户使用HTTP健康检查，需要配置HTTP检查路径和HTTP检查域名，两者拼接组成了HTTP检查的URL，ULB会对此URL发起HTTP HEAD请求，请求响应码为2xx或3xx则认为后端服务器正常。健康检查探测周期为2s，连续3次探测失败后端节点变更为不健康，连续两次正常变更为健康

![VServer&#x914D;&#x7F6E;&#x754C;&#x9762;](../../../.gitbook/assets/image%20%286%29.png)

HTTP检查路径，最多为227个字符，直接填写域名或IP地址后的相对路径文件。可以选择首页、出现异常概率较小的页面、专门为健康检查准备的空文件（HTTP HEAD请求可以获得200的响应码即可），选择首页可能会加大服务器压力，不建议选择首页作为HTTP健康检查的域名和路径。

HTTP检查域名，不建议填写"http:_"或"https:_"，直接填写域名或IP地址即可。支持主域名、二级域名等多级域名。

HTTP检查支持的协议:HTTP协议、HTTPS协议（七层服务）。

