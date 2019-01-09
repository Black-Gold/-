# Linux Virtual Server

```txt
Linux虚拟服务器是一个高度可扩展且高度可用的服务器，构建在真实服务器集群上。服务器群集的体系结构对最终用户完全透明，用户与群集系统进行交互，就好像它只是一个高性能的虚拟服务器一样。
```

![figure](http://www.linuxvirtualserver.org/VirtualServer.png)

```txt
真实服务器和负载平衡器可以通过高速LAN或地理上分散的WAN互连。负载均衡器可以将请求分派给不同的服务器，并使群集的并行服务在单个IP地址上显示为虚拟服务，请求分派可以使用IP负载平衡技术或应用级负载均衡技术。通过透明地添加或删除集群中的节点来实现系统的可伸缩性。通过检测节点或守护程序故障并适当地重新配置系统来提供高可用性。
```

```txt
构建服务器集群方法：
DNS负载平衡：
简单，利用域名系统将域名解析到服务器不同的IP来分发请求，DNS服务器根据调度策略(如循环方式)发出服务器IP地址，然后使用相同的本地缓存域名服务器在指定的域名解析生存时间(TTL)中发送到同一个服务器。
但是，由于客户端和分层DNS系统的缓存特性，很容易导致服务器之间的动态负载不平衡，因此服务器不容易处理其峰值负载。在DNS服务器上无法很好地选择名称映射的TTL值，小值DNS流量很高且DNS服务器将成为瓶颈，并且具有高值，动态负载不平衡将变得更糟。即使TTL值设置为零，调度粒度是每个主机，不同用户的访问模式可能会导致动态负载不平衡，因为有些人可能从网站上抽取大量页面，而其他人可能只是浏览几页然后去远。此外，它不太可靠，当服务器节点发生故障时，将名称映射到IP地址的客户端将发现服务器已关闭

基于调度程序的负载平衡群集：
可用于在群集中的服务器之间分配负载，以便服务器的并行服务可以在单个IP地址上显示为虚拟服务，并且最终用户可以像单个服务器一样进行交互不知道集群中的所有服务器。与基于DNS的负载平衡相比，调度程序可以以精细的粒度（例如每个连接）调度请求，以便在服务器之间实现更好的负载平衡。当一台或多台服务器发生故障时，可以屏蔽故障。服务器管理变得越来越容易，管理员可以随时使用服务器或更多服务器，这不会中断最终用户的服务。

负载均衡可以在两个级别完成，即应用级和IP级。将HTTP请求转发到集群中的不同Web服务器，获取结果，然后将其返回给客户端。由于在应用程序级别处理HTTP请求和回复的开销很高，当服务器节点数量增加到5或更多时，应用程序级负载均衡器将成为新的瓶颈，这取决于每个服务器节点的吞吐量服务器
```

```txt
LinuxVirtualServer以三种IP负载均衡技术(数据包转发方法)实现。
1. NAT方式
2. IP隧道
3. 直接路由
```

VS/NAT，VS/TUN和VS/DR的比较：