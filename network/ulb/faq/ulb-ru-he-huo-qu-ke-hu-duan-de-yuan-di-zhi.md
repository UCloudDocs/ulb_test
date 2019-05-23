# ULB如何获取客户端的源地址？

VServer支持报文转发、请求代理两种类型。报文转发模式支持TCP、UDP等协议，请求代理模式支持HTTP、HTTPS、TCP等协议。

报文转发模式下，后端服务节点收到的请求的源地址就是实际的源地址。

请求代理模式下，ULB已经默认开启了x-Forwarded-For选项，可以从HTTP报头中的X-Forward-For字段中获取客户端的源地址。

```text
# Nginx示例
log_format  upstream  '$time_iso8601 $http_x_forwarded_for $host $upstream_response_time $request $status $upstream_addr';

# Apache示例
SetEnvIf REMOTE_ADDR "(.+)" CLIENTIP=$1
SetEnvIf X-Forwarded-For "^([0-9.]+)" CLIENTIP=$1
LogFormat "%{CLIENTIP}e %D %u %t \"%r\" %>s %O \"%{Referer}i\" \"%{User-Agent}i\"" trueip_combined
CustomLog logs/access_log trueip_combined

# tomcat 的server.xml文件修改如下参数：
    <Host name="localhost" appBase="webapps" 
        unpackWARs="true" autoDeploy="true"> 
        <Valve className="org.apache.catalina.valves.AccessLogValve" 
        directory="logs" 
        prefix="tomcat_access." 
        suffix=".log" 
       pattern="%{X-FORWARDED-FOR}i %l %u %t %r %s %b %D %q %{User-Agent}i %T" resolveHosts="false"/> 
</Host>
```

###  <a id="&#x7ECF;&#x5E38;&#x53D1;&#x73B0;ulb&#x540E;&#x7AEF;&#x4E91;&#x4E3B;&#x673A;&#x7684;&#x8BBF;&#x95EE;&#x65E5;&#x5FD7;&#x4E2D;&#x6709;&#x5927;&#x91CF;&#x7684;&#x5185;&#x7F51;ip&#x8BBF;&#x95EE;_&#x8BF7;&#x95EE;&#x662F;&#x6B63;&#x5E38;&#x8BBF;&#x95EE;&#x4E48;"></a>

