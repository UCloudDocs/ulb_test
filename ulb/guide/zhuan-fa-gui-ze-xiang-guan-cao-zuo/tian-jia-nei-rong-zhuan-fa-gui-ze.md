# 添加内容转发规则

### 添加转发规则 <a id="&#x6DFB;&#x52A0;&#x8F6C;&#x53D1;&#x89C4;&#x5219;"></a>

内容转发允许VServer（HTTP/HTTPS协议）根据转发策略匹配域名或访问路径，能够将匹配请求转发到后端特定主机，对后端服务节点进行精细化管理。

在VServer监听器管理页面，点击“内容转发”标签进入转发规则设置页面。

[![image](https://docs.ucloud.cn/_media/network/ulb/ulb10.png)](https://docs.ucloud.cn/_detail/network/ulb/ulb10.png?id=network%3Aulb%3Acommon)

默认情况下，会存在一条叫做“默认转发规则”的策略，该策略在所有请求均未匹配成功时生效，会按照通常的转发规则进行转发。

点击“添加规则”按钮来添加规则，每条规则均需要与已经存在于服务实例池中的服务节点进行关联。输入规则，并选择服务节点后点击确定进行保存。

[![image](https://docs.ucloud.cn/_media/network/ulb/ulb11.png)](https://docs.ucloud.cn/_detail/network/ulb/ulb11.png?id=network%3Aulb%3Acommon)

内容转发规则分为“域名转发”与“路径转发”两种，这两种转发方式均可使用正则表达式或通配符进行描述，如“www.\[123\].demo.com”或“/path/img/\*.jpg”，创建规则时规则内容不可为空。

TCP/UDP协议暂不支持内容转发策略。  


