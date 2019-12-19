以伪装双Host免流模式为例。伪装双Host免流模式即伪装起来的双Host字段请求头——去掉原请求头中请求方法后跟的Host，并且添加一个新的Host字段，使修改后的请求头实际上拥有两个Host字段。由于现在绝大多数运营商计费检测系统屏蔽了（不免流）双Host流量，所以必须把其中一个Host字段通过某种方式伪装起来，使计费检测系统识别不了它，具体实现方式是通过免流模式向请求头中加进混淆信息。

以一款名为“离调双Host”的Tiny免流模式为例，下图为该免流模式配置，其中http_ip表示代理服务器IP、http_port表示代理服务器监听端口、http_del表示删除原请求头中的指定字段、http_first表示按指定格式修改请求头首行。
```
#HTTP模块

http_ ip=10.0.0.172;http port=80;

http_ del="Host, X-Online-Host"; 

http_ first=" [method] [uri] HTTP/1.1\r\n离调\rHost: [host] \r\nHost:wap.10086.cn\r\n";

#HTTPS模块

https_ connect=on;

https_ ip=10.0.0.172;https_ port=80;

https_ del="Host, X-Online-Host";

https_ first="CONNECT / HTTP/1.1 \rHost : [host] \r\nHost: wap.10086.cn\r\n";
```
设备中各应用程序发起的网络请求（除跳点外）在进入运营商代理服务器之前，会被核心模块按照以上文件配置进行修改，如下图左的请求头被修改后将会变成如下

特指出
```
符号           ASCII码        意义
\n               10          换行
\r               13          回车CR
```
原请求头
```
Get http://www.baidu.com/kl/mm HTTP/1.0
Host:www.baidu.com
```

新请求头
```
Get /k/mm HTTP/1.1
离调Host:www.baidu.com
Host:wap.10086.cn
```
经该免流模式处理过之后，原HTTP请求头中出现了两个Host，其中一个Host前有两个中文字符，而请求方法行中已经没有了Host信息。根据另一篇博客《运营商解析方式》一文中提到的第（2）种固定请求头格式，对于新请求头，运营商代理服务器读取到的Host是*www.baidu.com*， 而对于计费检测系统，因为有两个中文混淆字符，其不能从第二行开头获取Host字段标识，所以它选择从第三行的Host字段去获取Host——wap.10086.cn这个免流Host，因此最终达到了免流的目的。

以上只给出了一种经典的免流模式案例，现今存活的很多免流模式伪装方式千奇百怪，但万变不离其宗，最终的效果都是要欺骗计费检测系统去获取免流Host并以此实现免流。
