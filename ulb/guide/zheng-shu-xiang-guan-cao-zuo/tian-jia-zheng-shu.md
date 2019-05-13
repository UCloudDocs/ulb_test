# 添加证书

您可以点击证书管理，将证书存储在我们的负载均衡的证书管理系统中，用于支持HTTPS功能。若您需要在不同的region中使用同一个证书，需要将证书存储在多个region的负载均衡证书管理系统中。

操作步骤： 1、登录控制台进入负载均衡产品页面。 2、在左侧导航中选择“证书管理” 3、点击左上角“添加证书”

[![](https://docs.ucloud.cn/_media/network/ulb/%E6%B7%BB%E5%8A%A0%E8%AF%81%E4%B9%A61.png)](https://docs.ucloud.cn/_detail/network/ulb/%E6%B7%BB%E5%8A%A0%E8%AF%81%E4%B9%A61.png?id=network%3Aulb%3Acommon)

4、填写证书名称，命名中可包含中英文、数字以及‘-’‘\_’‘.’ 选择本地上传或手动输入证书 5.1、本地上传证书，选择您本地的授权证书，包括.crt文件与.key文件。 5.2、选择手动输入证书，则需要在输入框中手动填写证书，证书格式见证书格式要求。

[![](https://docs.ucloud.cn/_media/network/ulb/%E6%B7%BB%E5%8A%A0%E8%AF%81%E4%B9%A62.png)](https://docs.ucloud.cn/_detail/network/ulb/%E6%B7%BB%E5%8A%A0%E8%AF%81%E4%B9%A62.png?id=network%3Aulb%3Acommon)

授权证书\(.crt文件\)：证书机构下发的公钥文件

授权证书\(.key文件\)：证书机构下发的私钥文件

CA机构证书\(.crt文件\)：证书机构证明自身是权威机构的证明，是可选项。

浏览器在是识别ca证书后，会自动将这个其下发的ssl证书认定为可行证书。

