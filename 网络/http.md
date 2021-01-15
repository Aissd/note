https://www.cnblogs.com/kaishirenshi/p/12575847.html

##### http的基本优化
影响一个http网络请求的因素主要有两个：带宽和延迟。
延迟：
* 浏览器阻塞（HOL blocking）：浏览器对于同一个域名同时只能有4个连接（不同浏览器内核有差异），超出最大连接限制就会被阻塞。
* DNS查询（DNS Lookup）：浏览器需要知道目标服务器的ip才能建立连接。将域名解析为ip的这个系统就是DNS。通常利用DNS缓存结果来达到减少时间的目的。
* 建立连接（Initial connection）：http是基于TCP协议的，浏览器最快也要第三次握手是才能捎带http请求报文，达到真正的建立连接，但是这些连接无法复用会导致每次请求都要经历三次握手和慢启动。三次握手在高延迟的场景下影响较明显，慢启动则对文件类大请求影响较大。

##### http1.0和http1.1的一些区别
* 缓存处理：
在http1.0中主要使用header里的if-modified-since，expires来做缓存判断的标准，http1.1则引入了更多的缓存控制策略例如entity tag，if-unmodified-since，if-match，uf-none-match等。
* 带宽优化及网络连接的使用：
http1.1在请求头引入range头域，它允许只请求资源的某个部分，即返回码是206（partial content），这样就方便了开发者自由的选择以便于充分利用带宽和连接。
* 错误通知的管理
http1.1中新增了24个错误状态响应码。如409（Conflict)表示请求的资源与资源的当前状态发生冲突；401（Gone）表示服务器上的某个资源被永久性的删除。
* Host头处理
在http1.0中认为每台服务器都绑定一个唯一的ip地址，因此请求信息中的url并没有传递主机名（hostname）。
随着虚拟主机的发展，一台物理服务器上可以存在多个虚拟主机，并且共享一个ip地址。
http1.1的请求信息和响应信息都支持host头域，且请求消息中如果没有host头域会报告一个错误（400 Bad Request）
* 长链接：
http1.1支持场链接和请求的流水线处理，在一个tcp连接上可以传送多个http请求和响应，减少了建立和关闭连接的消耗和延迟，在http1.1中默认开启connection:keep-alive，一定程度上弥补了http1.0每次请求都要创建连接的缺点。

##### http1.x和http2.0的区别

* http1.x是文本（字符串）传送，http2使用二进制传送
二进制的单位是帧和流，帧组成流，同时流还有id标识

* http2支持多路复用
因为有流id，所以通过同一个http请求实现多个http请求传输变成了可能，可以通过流id来标识究竟是哪个流从而定位到时哪个http请求

* http2头部压缩
http2通过gzip和compress压缩头部然后再发送，同时客户端和服务器端同时维护一张头信息表，所有字段都记录在这张表中，然后后面每次传输只需要传输表里的索引id就行，通过索引id查询表头的值。

* http2支持服务器推送
支持在未经客户端许可的情况下，主动向客户端推送内容

##### http和https的区别
* https协议需要到ca申请证书，免费的很少，需要交费

* http协议运行在tcp之上，所有传输的内容都是明文。https协议运行在SSL/TLS之上，SSL/TLS运行在tco之上，所有传输内容都经过加密的。

* http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443

* https可以有效防止运营商劫持

    ![img](http://mmbiz.qpic.cn/mmbiz_png/cmOLumrNib1cfBOtIMQ6JfSibJdd6QkQribXL5PwzkqQdmyY9egu2hpzzMCgz2F5HhhkdSNc5eYJ9UGMDBGjeCGiag/0?wx_fmt=png)

    

##### dns优化

