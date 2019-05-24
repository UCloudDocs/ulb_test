{{indexmenu_n>1}}

# 什么是ULB

### ULB简介

负载均衡（ULB）能够为多个主机或其它服务实例提供基于网络报文或代理方式的流量分发的功能。用于在高并发服务环境下，构建由多个服务节点组成的“负载均衡服务集群”。“服务集群”能够扩展服务的处理及容错能力，并可自动消除由于单一服务节点故障对服务整体的影响，提高服务的可用性。

ULB针对七层协议支持HTTP、HTTPS协议（类Nginx或HAproxy）；四层协议支持TCP协议及UDP协议（类LVS）。

### ULB组成

ULB服务主要由以下三个部分构成：

* ULB服务实例（LoadBalancer）：用来接收流量并进行流量分发。
* 虚拟服务器／监听器（VServer）：ULB监听器，每个VServer是一组负载均衡前端端口配置。
* 服务节点（RealServer／Backend）：后端真实处理请求的云资源。

![ULB&#x67B6;&#x6784;&#x56FE;](../../.gitbook/assets/image%20%286%29.png)


