# 添加服务节点

VServer监听器创建完毕后，需要为VServer添加服务节点才可完成负载均衡的整个服务配置。 在VServer管理页面中点击“添加”按钮，选择后端真实服务节点的“IP地址”，并填入服务的“端口”，点击确定即可完成节点添加。

[![image](https://docs.ucloud.cn/_media/network/ulb/ulb7.png)](https://docs.ucloud.cn/_detail/network/ulb/ulb7.png?id=network%3Aulb%3Acommon)

[![](https://docs.ucloud.cn/_media/network/ulb/%E6%B7%BB%E5%8A%A0%E8%8A%82%E7%82%B9.png)](https://docs.ucloud.cn/_detail/network/ulb/%E6%B7%BB%E5%8A%A0%E8%8A%82%E7%82%B9.png?id=network%3Aulb%3Acommon)

如VServer监听器类型为七层ULB或者四层ULB的请求代理模式，则相同后端真实服务节点可通过添加不同端口，实现同一IP不同服务实例；如采用四层ULB的UDP协议及TCP报文转发模式，则后端真实服务节点的端口必须与VServer监听端口保持一致。  


