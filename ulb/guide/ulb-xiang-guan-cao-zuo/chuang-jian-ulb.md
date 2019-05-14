# 创建ULB

### 操作步骤

1、进入**负载均衡 ULB**页面后。

2，点击**创建负载均衡**进行ULB实例创建。

![](../../../.gitbook/assets/image%20%287%29.png)

[![image](https://docs.ucloud.cn/_media/network/ulb/ulb2.png)](https://docs.ucloud.cn/_detail/network/ulb/ulb2.png?id=network%3Aulb%3Acommon)

3、填写配置信息，进行ULB实例创建。详细配置说明见下方。

[![image](https://docs.ucloud.cn/_media/network/ulb/%E5%88%9B%E5%BB%BAulb-%E5%90%AB%E9%98%B2%E7%81%AB%E5%A2%99.png)](https://docs.ucloud.cn/_detail/network/ulb/%E5%88%9B%E5%BB%BAulb-%E5%90%AB%E9%98%B2%E7%81%AB%E5%A2%99.png?id=network%3Aulb%3Acommon)

### 配置说明

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x914D;&#x7F6E;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x5730;&#x57DF;</td>
      <td style="text-align:left">ULB&#x6240;&#x5C5E;&#x7684;&#x5730;&#x57DF;&#x3002;&#x9009;&#x5B9A;&#x5730;&#x57DF;&#x540E;&#xFF0C;&#x540E;&#x7AEF;&#x670D;&#x52A1;&#x8282;&#x70B9;&#x53EA;&#x80FD;&#x6DFB;&#x52A0;&#x540C;&#x5730;&#x57DF;&#x7684;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x4E1A;&#x52A1;&#x7EC4;</td>
      <td style="text-align:left">ULB&#x6240;&#x5C5E;&#x7684;&#x7BA1;&#x7406;&#x4E1A;&#x52A1;&#x7EC4;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6240;&#x5C5E;VPC</td>
      <td style="text-align:left">ULB&#x6240;&#x5C5E;&#x7684;VPC&#x7F51;&#x7EDC;&#x3002;&#x9009;&#x5B9A;VPC&#x540E;&#xFF0C;&#x540E;&#x7AEF;&#x670D;&#x52A1;&#x8282;&#x70B9;&#x53EA;&#x80FD;&#x6DFB;&#x52A0;&#x540C;VPC&#x4E0B;&#x7684;&#x4E91;&#x8D44;&#x6E90;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x7F51;&#x7EDC;&#x6A21;&#x5F0F;</td>
      <td style="text-align:left">
        <p>&#x5206;&#x4E3A;&#x5185;&#x7F51;&#x3001;&#x5916;&#x7F51;&#x4E24;&#x79CD;&#x6A21;&#x5F0F;&#x3002;&#x8BE6;&#x7EC6;&#x8BF4;&#x660E;&#x53EF;&#x53C2;&#x8003;&#xFF08;&#x5982;&#x4F55;&#x52A0;&#x76F8;&#x5BF9;&#x8DEF;&#x5F84;&#xFF09;</p>
        <ul>
          <li>&#x5185;&#x7F51;&#xFF0C;ULB&#x5BF9;&#x5916;&#x63D0;&#x4F9B;&#x670D;&#x52A1;&#x7684;&#x5730;&#x5740;&#x4E3A;&#x5185;&#x7F51;IP&#x5730;&#x5740;</li>
          <li>&#x5916;&#x7F51;&#xFF0C;ULB&#x5BF9;&#x5916;&#x63D0;&#x4F9B;&#x670D;&#x52A1;&#x7684;&#x5730;&#x5740;&#x4E3A;&#x5916;&#x7F51;&#x5F39;&#x6027;IP&#x3002;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">&#x6240;&#x5C5E;&#x5B50;&#x7F51;</td>
      <td style="text-align:left">&#x9009;&#x62E9;&#x5185;&#x7F51;&#x540E;&#xFF0C;&#x9700;&#x9009;&#x62E9;&#x6240;&#x5C5E;&#x5B50;&#x7F51;&#x3002;&#x4ECE;&#x8BE5;&#x5B50;&#x7F51;&#x4E2D;&#x5206;&#x914D;&#x5185;&#x7F51;IP&#x5730;&#x5740;&#x4F5C;&#x4E3A;ULB&#x5BF9;&#x5916;&#x63D0;&#x4F9B;&#x670D;&#x52A1;&#x7684;IP&#x5730;&#x5740;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5F39;&#x6027;IP</td>
      <td style="text-align:left">&#x9009;&#x62E9;&#x5916;&#x7F51;&#x540E;&#xFF0C;&#x9700;&#x8981;&#x914D;&#x7F6E;&#x5916;&#x7F51;&#x5F39;&#x6027;IP&#x4F5C;&#x4E3A;ULB&#x5BF9;&#x5916;&#x63D0;&#x4F9B;&#x670D;&#x52A1;&#x7684;IP&#x5730;&#x5740;&#x3002;&#x53EF;&#x9009;&#x62E9;&#x201C;&#x65B0;&#x8D2D;&#x201D;&#x6216;&#x201C;&#x73B0;&#x6709;&#x201D;&#x5916;&#x7F51;&#x5F39;&#x6027;IP&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x8BA1;&#x8D39;&#x65B9;&#x5F0F;</td>
      <td style="text-align:left">&#x9009;&#x62E9;&#x201C;&#x65B0;&#x8D2D;&#x201D;&#x5916;&#x7F51;&#x5F39;&#x6027;IP&#x65F6;&#xFF0C;&#x9700;&#x9009;&#x62E9;IP&#x8BA1;&#x8D39;&#x65B9;&#x5F0F;&#x3002;&#x53EF;&#x9009;&#x5E26;&#x5BBD;&#x3001;&#x6D41;&#x91CF;&#x3001;&#x5171;&#x4EAB;&#x5E26;&#x5BBD;&#x7B49;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5E26;&#x5BBD;</td>
      <td style="text-align:left">&#x9009;&#x62E9;&#x201C;&#x65B0;&#x8D2D;&#x201D;&#x5916;&#x7F51;IP&#x65F6;&#xFF0C;&#x9700;&#x9009;&#x62E9;IP&#x7684;&#x5E26;&#x5BBD;&#x503C;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x5916;&#x7F51;&#x9632;&#x706B;&#x5899;</td>
      <td style="text-align:left">&#x5916;&#x7F51;&#x6A21;&#x5F0F;&#x4E0B;&#xFF0C;&#x53EF;&#x7ED1;&#x5B9A;&#x5916;&#x7F51;&#x9632;&#x706B;&#x5899;&#x8FDB;&#x884C;&#x8BBF;&#x95EE;&#x63A7;&#x5236;&#x3002;&#x53EF;&#x9009;&#x4E0D;&#x7ED1;&#x5B9A;&#x3001;&#x7ED1;&#x5B9A;&#x3002;</td>
    </tr>
  </tbody>
</table>