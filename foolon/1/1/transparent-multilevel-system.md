# 多级分流系统

- 客户端缓存
- 域名解析
- 传输链路
- 内容分发网络
- 负载均衡
- 服务端缓存

系统可以分为三种类型

- 边缘服务：例如浏览器缓存，cdn
- 易扩展服务：例如提供服务的集群
- 单点服务：例如数据库

在系统中，应该尽量减少单点服务的访问及流量，以及不要过于复杂，能满足要求的技术即可，过于复杂有可能适得其反。
## 客户端缓存
客户端缓存是为了减轻服务端的压力而设计的，因为http协议和服务器之间是无状态的，所以前后两次的访问请求，并没有什么关系，也就是独立的，这就造成http的每次请求都要带有重复的数据，一大堆的数据必然拖累了连接效率，所以尽量减少联接就称为了优化的方向，那么客户端的缓存就可以解决这个问题。

- 状态缓存

    指的是不经过服务器，直接进行**根据缓存信息**作出的行为，比如301强制重定向。

- 强制缓存

    根据服务器返回的参数，在某个时间点之前，浏览器**强制缓存不用请示服务器**，在浏览器的动作中，除了 “刷新” 动作会不使用这个缓存，其余动作，例如后退，前进，跳转，搜索，地址输入框输入地址，都会使用这个缓存。

    使用http1.1提供的 Cache-Control 参数可以设定失效时间其中它包含了一些参数，分别是：
    - max-age：请求缓存的时间 
    - s-maxage：共享缓存的请求时间，比如cdn，代理，public private：是否牵涉到隐私资源，如果是private那么cdn等共享的系统将无法获取此资源
    - no-cache no-store：表示此资源不应该被缓存
    - no-transform：禁止资源被修改min-fresh：只用于客户端的header，表示服务器返回的max-age的最小值
    - only-if-cached：客户端要求，服务器不必给它发送具体的缓存内容
    - must-revalidate proxy-revalidate：表示过期后，资源一定要从服务器中获取

- 协商缓存

    根据变化**不断检测**的一种缓存机制，跟强制缓存属于并行机制，
    - last-Modified 服务器响应字段，最后响应时间 
    - if-Modified-Since 客户端字段，表示资源最后的修改时间，如果服务器发现资源还没有过期直接返回304，如果发现过期了就返回真实的数据
    - Etag 服务器返回的资源唯一id
    - if-None-Match 客户端将id通过此字段传递给服务器用于验证资源

    协商缓存在用户刷新的时候同样有效果，这个比强制缓存还厉害
## 域名解析
dns是域名和IP地址的翻译系统，整个系统只有2mb大小，

## 传输链路

## 内容分发网络

## 负载均衡

## 服务端缓存