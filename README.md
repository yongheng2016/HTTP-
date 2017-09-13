# HTTP-Cache

> + 缓存是以url为依据的，缓存只会针对同一个url
> + 如果请求头里面有request-header设置了cache-contro，就以请求头为主
> + 浏览器第一个请求默认不会读取缓存（至少要有一个请求发送到服务端保存联系）
---
+ `Cache-Control`(不要和Expire同时使用)
   * 相对时间，`max-age=xxx (s)`
```
Cache-Control: public, max-age=86400
```
     
+ `Expires`(格林梅治世界)
   * 和用户的本地时间做对比
   * 不易把控，假如用户的本地时间不准

不好写，可以在控制台打印一下，复制下来，注意时区，8小时的差异

![image](https://user-images.githubusercontent.com/24493052/29121435-15d72bea-7d41-11e7-9c6d-75c5233aeb9f.png)

     
     
+ `Last-Modified`(上次修改时间)
   * 如果没有设置过期时间或日期，若有`Last-Modified`字段浏览器会计算一个缓存时间（less   ##10%）
```
Last-Modified: Fri, 22 Jul 2016 01:47:00 GMT
```
> md5

+ ETag
   * lient端第一次请求时，服务端给client端响应头一个Etag哈希值，等下次访问时，会连同这个hash一起放在请求头发送，到达后和后端hash比对`last-none-match`
```
Etag: "5d8c72a5edda8d6a:3239"
```
+ cookie
   + 服务器可以设置cookie给浏览器
   + 相同域名的所有请求都会带上此cookie
   + 例：读取cookie达到用户自动登陆
之前访问过某网站并记录下了cookie，下次登陆自动读取cookie进行自动验证  
   + 有问题，document.cookie可以设置、更改，不可靠
![image](https://user-images.githubusercontent.com/24493052/29127244-23430c9c-7d53-11e7-948b-ff3fc18064a6.png)

+ Session
   + 上面的问题可以通过把用户名密码存储在session[id]中
   + 给每个用户分配一个唯一的id
   + 验证id和session中的id是否匹配
   + 再做一次hash加密，基本不能预测了


参考：[http://imweb.io/topic/5795dcb6fb312541492eda8c](http://imweb.io/topic/5795dcb6fb312541492eda8c)
