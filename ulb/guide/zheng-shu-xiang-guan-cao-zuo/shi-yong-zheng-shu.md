# 使用证书

您在证书管理中上传证书后，在创建监听HTTPS的VServer时，就可以使用已经上传的证书

操作步骤： 1、选择某个ULB实例，点击管理

2、点击添加VServer，增加监听规则

3、选择监听类型为请求代理（七层），监听协议为HTTPS后，选择SSL证书，此时可以选择证书管理系统中存储的证书。（注：建议HTTPS端口使用443）

[![](https://docs.ucloud.cn/_media/network/ulb/%E4%BD%BF%E7%94%A8%E8%AF%81%E4%B9%A63.png)](https://docs.ucloud.cn/_detail/network/ulb/%E4%BD%BF%E7%94%A8%E8%AF%81%E4%B9%A63.png?id=network%3Aulb%3Acommon)

4、配置完成后可在左侧看到新增的VServer，并可以VServer的证书。

[![](https://docs.ucloud.cn/_media/network/ulb/%E4%BD%BF%E7%94%A8%E8%AF%81%E4%B9%A64.png)](https://docs.ucloud.cn/_detail/network/ulb/%E4%BD%BF%E7%94%A8%E8%AF%81%E4%B9%A64.png?id=network%3Aulb%3Acommon)  


