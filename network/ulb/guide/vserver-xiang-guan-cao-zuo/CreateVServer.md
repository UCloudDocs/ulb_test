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

<table>
  <thead>
    <tr>
      <th style="text-align:left">VServer&#x540D;&#x79F0;</th>
      <th style="text-align:left">VServer&#x76D1;&#x542C;&#x5668;&#x7BA1;&#x7406;&#x540D;&#x79F0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">VServer&#x540D;&#x79F0;</td>
      <td style="text-align:left">VServer&#x540D;&#x79F0;&#xFF0C;&#x5FC5;&#x586B;&#x9879;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x534F;&#x8BAE;&#x548C;&#x7AEF;&#x53E3;</td>
      <td style="text-align:left">&#x76D1;&#x542C;&#x5668;&#x6240;&#x76D1;&#x542C;&#x7684;&#x534F;&#x8BAE;&#x53CA;&#x7AEF;&#x53E3;&#xFF0C;&#x5305;&#x542B;HTTP/HTTPS/TCP/UDP&#x56DB;&#x79CD;&#x534F;&#x8BAE;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x76D1;&#x542C;&#x5668;&#x7C7B;&#x578B;</td>
      <td style="text-align:left">HTTP&#x3001;HTTPS&#x9ED8;&#x8BA4;&#x4E3A;&#x8BF7;&#x6C42;&#x4EE3;&#x7406;&#x6A21;&#x5F0F;&#xFF0C;UDP&#x9ED8;&#x8BA4;&#x4E3A;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x3002;&#x5916;&#x7F51;ULB&#xFF0C;TCP&#x534F;&#x8BAE;&#x652F;&#x6301;&#x201C;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x201D;&#x4E0E;&#x201C;&#x8BF7;&#x6C42;&#x4EE3;&#x7406;&#x6A21;&#x5F0F;&#x201D;&#xFF1B;&#x5185;&#x7F51;ULB&#xFF0C;TCP&#x534F;&#x8BAE;&#x4EC5;&#x652F;&#x6301;&#x201C;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x201C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8D1F;&#x8F7D;&#x5747;&#x8861;&#x7B97;&#x6CD5;</td>
      <td style="text-align:left">
        <p>&#x76D1;&#x542C;&#x5668;&#x5BF9;&#x6570;&#x636E;&#x5305;&#x7684;&#x8D1F;&#x8F7D;&#x65B9;&#x5F0F;&#xFF0C;&#x5305;&#x542B;</p>
        <ul>
          <li><b>&#x8F6E;&#x8BE2;</b>&#x3002;ULB&#x63A5;&#x6536;&#x5230;&#x65B0;&#x7684;TCP&#x8FDE;&#x63A5;&#x540E;,
            &#x4F9D;&#x6B21;&#x8F6C;&#x7ED9;&#x6BCF;&#x4E2A;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#x3002;</li>
          <li><b>&#x6E90;&#x5730;&#x5740;</b>&#x3002;ULB&#x4F1A;&#x6839;&#x636E;TCP&#x8FDE;&#x63A5;&#x7684;&#x6E90;&#x5730;&#x5740;&#xFF0C;&#x5229;&#x7528;&#x4E00;&#x5B9A;&#x7684;&#x54C8;&#x5E0C;&#x7B97;&#x6CD5;&#x5C06;&#x8BF7;&#x6C42;&#x5176;&#x8F6C;&#x7ED9;&#x67D0;&#x53F0;&#x4E3B;&#x673A;&#x3002;&#x4E4B;&#x540E;&#x7528;&#x6237;&#x518D;&#x4EE5;&#x76F8;&#x540C;IP&#x8BBF;&#x95EE;,
            &#x5982;&#x4E3B;&#x673A;&#x6570;&#x91CF;&#x4E0D;&#x53D8;&#x65F6;&#xFF0C;&#x8BBF;&#x95EE;&#x8FD8;&#x662F;&#x4F1A;&#x843D;&#x5230;&#x8BE5;&#x53F0;&#x4E3B;&#x673A;&#x3002;</li>
          <li><b>&#x6E90;&#x5730;&#x5740;&#xFF08;&#x8BA1;&#x7B97;&#x7AEF;&#x53E3;&#xFF09;</b>&#x3002;ULB&#x4F1A;&#x6839;&#x636E;TCP&#x8FDE;&#x63A5;&#x7684;&#x6E90;&#x5730;&#x5740;&#x548C;&#x6E90;&#x7AEF;&#x53E3;&#xFF0C;&#x5229;&#x7528;&#x4E00;&#x5B9A;&#x7684;&#x54C8;&#x5E0C;&#x7B97;&#x6CD5;&#x5C06;&#x8BF7;&#x6C42;&#x5176;&#x8F6C;&#x7ED9;&#x67D0;&#x53F0;&#x4E3B;&#x673A;&#x3002;&#xFF08;&#x4EC5;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x652F;&#x6301;&#xFF09;</li>
          <li><b>&#x4E00;&#x81F4;&#x6027;&#x54C8;&#x5E0C;&#x3002;</b>&#x4E00;&#x81F4;&#x6027;&#x54C8;&#x5E0C;&#x7B97;&#x6CD5;&#x662F;&#x6839;&#x636E;&#x6E90;&#x76EE;&#x7684;IP&#xFF0C;&#x4F7F;&#x7528;&#x4E00;&#x81F4;&#x6027;&#x54C8;&#x5E0C;&#x7B97;&#x6CD5;&#x7684;&#x7ED3;&#x679C;&#x9009;&#x62E9;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#x3002;&#x5982;&#x679C;&#x589E;&#x52A0;&#x6216;&#x8005;&#x5220;&#x51CF;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#xFF0C;&#x4EC5;&#x4EC5;&#x4F1A;&#x5F71;&#x54CD;&#x5C0F;&#x90E8;&#x5206;&#x8FDE;&#x63A5;&#x3002;&#xFF08;&#x4EC5;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x652F;&#x6301;&#xFF09;</li>
          <li><b>&#x4E00;&#x81F4;&#x6027;&#x54C8;&#x5E0C;&#xFF08;&#x8BA1;&#x7B97;&#x7AEF;&#x53E3;&#xFF09;</b>&#x3002;&#x6839;&#x636E;&#x6E90;&#x76EE;&#x7684;IP&#x3001;&#x6E90;&#x76EE;&#x7684;&#x7AEF;&#x53E3;&#xFF0C;&#x4F7F;&#x7528;&#x4E00;&#x81F4;&#x6027;&#x54C8;&#x5E0C;&#x7B97;&#x6CD5;&#x7684;&#x7ED3;&#x679C;&#x9009;&#x62E9;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#x3002;&#x5982;&#x679C;&#x589E;&#x52A0;&#x6216;&#x8005;&#x5220;&#x51CF;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#xFF0C;&#x4EC5;&#x4EC5;&#x4F1A;&#x5F71;&#x54CD;&#x5C0F;&#x90E8;&#x5206;&#x8FDE;&#x63A5;&#x3002;&#xFF08;&#x4EC5;&#x62A5;&#x6587;&#x8F6C;&#x53D1;&#x6A21;&#x5F0F;&#x652F;&#x6301;&#xFF09;</li>
          <li><b>&#x52A0;&#x6743;&#x8F6E;&#x8BE2;&#x3002;</b>ULB&#x63A5;&#x6536;&#x5230;&#x65B0;&#x7684;TCP&#x8FDE;&#x63A5;&#x540E;&#xFF0C;&#x5C06;&#x6839;&#x636E;&#x60A8;&#x6307;&#x5B9A;&#x7684;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#x7684;&#x4E0D;&#x540C;&#x6743;&#x91CD;&#xFF0C;&#x6309;&#x7167;&#x6982;&#x7387;&#x5206;&#x914D;&#x7ED9;&#x5404;&#x4E2A;&#x540E;&#x7AEF;&#x4E3B;&#x673A;&#x3002;</li>
          <li><b>&#x6700;&#x5C0F;&#x8FDE;&#x63A5;&#x6570;</b>&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x670D;&#x52A1;&#x8282;&#x70B9;</td>
      <td style="text-align:left">&#x4E00;&#x822C;&#x60C5;&#x51B5;&#xFF0C;&#x6DFB;&#x52A0;&#x670D;&#x52A1;&#x8282;&#x70B9;&#x662F;&#x9700;&#x8981;&#x5728;VServer&#x76D1;&#x542C;&#x5668;&#x521B;&#x5EFA;&#x5B8C;&#x6210;&#x540E;&#x518D;&#x8FDB;&#x884C;&#x3002;
        &#x8BE5;&#x9009;&#x9879;&#x63D0;&#x4F9B;&#x4E86;&#x4ECE;&#x5176;&#x4ED6;VServer&#x590D;&#x5236;&#x670D;&#x52A1;&#x8282;&#x70B9;&#x6C60;&#x914D;&#x7F6E;&#x7684;&#x65B9;&#x6CD5;&#xFF0C;&#x4EE5;&#x4FBF;&#x5229;&#x7528;&#x539F;&#x6709;&#x914D;&#x7F6E;&#x5FEB;&#x901F;&#x521B;&#x5EFA;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x670D;&#x52A1;&#x4F1A;&#x8BDD;&#x4FDD;&#x6301;</td>
      <td style="text-align:left">&#x5BF9;&#x4E8E;HTTP/HTTPS&#x534F;&#x8BAE;&#xFF0C;&#x4F7F;&#x7528;&#x9ED8;&#x8BA4;/&#x81EA;&#x5B9A;&#x4E49;&#x5173;&#x952E;&#x8BCD;&#x5BF9;&#x7528;&#x6237;&#x767B;&#x5F55;&#x6001;&#x7684;&#x4FDD;&#x6301;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8FDE;&#x63A5;&#x4FDD;&#x6301;&#x65F6;&#x95F4;</td>
      <td style="text-align:left">TCP&#x8BF7;&#x6C42;&#x4EE3;&#x7406;&#x6A21;&#x5F0F;&#x4E0B;&#xFF0C;&#x6216;HTTP&#x3001;HTTPS&#x534F;&#x8BAE;&#xFF0C;&#x53EF;&#x9009;&#x62E9;&#x5BA2;&#x6237;&#x7AEF;&#x8BF7;&#x6C42;&#x8FDE;&#x63A5;&#x7684;&#x6709;&#x6548;&#x65F6;&#x95F4;&#x3002;&#x53EF;&#x9009;&#x65F6;&#x95F4;&#x8303;&#x56F4;[1-86400]&#x79D2;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8282;&#x70B9;&#x5065;&#x5EB7;&#x68C0;&#x67E5;</td>
      <td style="text-align:left">&#x6839;&#x636E;&#x6240;&#x9009;&#x534F;&#x8BAE;&#x4E0D;&#x540C;&#xFF0C;&#x68C0;&#x67E5;&#x65B9;&#x5F0F;&#x5305;&#x542B;&#x670D;&#x52A1;&#x5730;&#x5740;/&#x7AEF;&#x53E3;&#x68C0;&#x67E5;&#x548C;HTTP&#x68C0;&#x67E5;&#x4E24;&#x79CD;&#x65B9;&#x5F0F;&#x3002;</td>
    </tr>
  </tbody>
</table>

#### 

#### 

