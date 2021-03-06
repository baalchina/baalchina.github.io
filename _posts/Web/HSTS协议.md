#HSTS协议

##说明
- HSTS是HTTP Strict Transport Security的缩写，即：“HTTP严格传输安全”。
- 服务器端配置支持HSTS后，会在给浏览器返回的HTTP首部中携带HSTS字段。浏览器获取到该信息后，会将所有HTTP访问请求在内部做307跳转到HTTPS。而无需任何网络过程。
- HSTS是有缺陷的，第一次访问网站的客户端，HSTS并不工作。 要解决这个问题，就要了解我们下面要讲解的HSTS preload list。
- `HSTS preload list`是Chrome浏览器中的HSTS预载入列表，在该列表中的网站，使用Chrome浏览器访问时，会自动转换成HTTPS。Firefox、Safari、Edge浏览器也在采用这个列表。
- 加入`HSTS preload list`不但不麻烦，而且Chrome也鼓励HTTPS网站能够主动加入。申请的方法和需要满足的条件在https://hstspreload.appspot.com网站上都有具体说明。

##理解
- 大意就是，大家习惯通过`www.taobao.com`访问
- 这时候服务器通过302跳转实现跳转到`https://www.taobao.com`，但实际上前两个请求还是通过`http`来完成的
- 如果有了`hsts`，只要浏览器还保留了响应头，下次访问的时候就直接通过`https`了。
- 缺点是第一次访问，仍然需要通过`http`

参考：
1. https://blog.wilddog.com/?page_id=1493
2. https://zh.wikipedia.org/wiki/HTTP%E4%B8%A5%E6%A0%BC%E4%BC%A0%E8%BE%93%E5%AE%89%E5%85%A8
3. http://www.barretlee.com/blog/2015/10/22/hsts-intro/