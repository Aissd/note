cookie的属性
```
name:存储到cookie的键（key）
value：name对应的值（value）
domain：域，一般指允许访问的域名，修改domain可以用来跨域
path：访问路径
expires：cookie的过期时间，现在已经被max-age代替
max-age：最大生存时间
cache-control：与expires的作用一致，都是指名当前资源的有效期，控制浏览器是否直接从浏览器缓存取数据还是重新发请求到服务器取数据。只不过cache-control选择更多，设置更细致，同时设置的话，其优先级高于expires
size：存储cookie的字节
http：http协议
secure：获取或设置cookie的安全级别
samesite：用于定义cookie如何跨域发送，这是谷歌开发的一种安全机制，目的是尝试阻止CSRF（跨站请求伪造）以及XSSI（跨站脚本）攻击
```