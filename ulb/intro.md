# 产品简介

## ULB简介

负载均衡（ULB）能够为多个主机或其它服务实例提供基于网络报文或代理方式的流量分发的功能。用于在高并发服务环境下，构建由多个服务节点组成的“负载均衡服务集群”。“服务集群”能够扩展服务的处理及容错能力，并可自动消除由于单一服务节点故障对服务整体的影响，提高服务的可用性。

目前ULB针对七层支持HTTP、HTTPs协议（类Nginx或HAproxy）；针对四层支持TCP协议及UDP协议（类LVS）。并且TCP协议支持两种方式：报文转发与请求代理。报文转发与请求代理模式详情可参考[TCP的请求代理与报文转发](https://docs.ucloud.cn/network/ulb/intro#tcp%E7%9A%84%E8%AF%B7%E6%B1%82%E4%BB%A3%E7%90%86%E4%B8%8E%E6%8A%A5%E6%96%87%E8%BD%AC%E5%8F%91)。四层ULB支持外网与内网两种模式，而七层ULB目前仅支持外网。您可以参考[如何选择ULB](https://docs.ucloud.cn/network/ulb/common#%E5%A6%82%E4%BD%95%E9%80%89%E6%8B%A9ulb)选择哪一层ULB来部署业务

## ULB基本概念

### ULB服务的结构

ULB服务主要由以下三个部分构成：

* ULB服务实例（LoadBalancer）
* 虚拟服务器（VServer）
* 后端服务器（Backend）

结构图如下所示：

