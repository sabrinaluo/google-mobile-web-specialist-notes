# Performance

性能影响用户体验，从而影响流量，研究显示页面加载越快，用户留存率越高，转换率越高
研究显示在手机页面上每减小1秒的加载时间，就能提高27%的转换率[^1]

## Tools
**性能比较工具**：
- https://www.thinkwithgoogle.com/feature/mobile/ 谷歌出品，缺点是有些网站可能没有被收录，好像只收录了顶级域名.com的网站

**性能测试工具**：
- lighthouse https://developers.google.com/web/tools/lighthouse/
- webpagetest https://www.webpagetest.org/ 可检测static assets， image压缩等
- pagespeed https://developers.google.com/speed/pagespeed/insights

### lighthouse
有三种方式可以运行lighthouse

- chrome extension
- `npm install -g lighthouse`
- devtools -> audit

可以生成多种格式的报告，点击分享选择“save as a gist” 之后可以在 https://googlechrome.github.io/lighthouse/viewer/ 中打开看到网页版的详细报告

### pagespeed insights
跟webPageTest类似，能够检测static assets，image压缩等问题

## 优化项目
- 避免重定向
- 压缩图片、字体等资源
- 考虑使用特定格式的图片以减小文件大小，例如`webp` `jpeg xr`
- 使用srcset，让浏览器选择性的加载不同分辨率的图片
- minify css, javscript
- 将可见内容优先级提高，换句话说就是把script放在`<body>`的底部
- 浏览器缓存
对于可缓存的资源，应该在响应的headers中设置`expiry date`或`maximum age`，这可以使浏览器从本地加载相关资源，而非重新从网络下载 (没有设置相应header则不会被缓存)
- 减少服务器响应时间
- 针对不同的viewport大小，发送不同的内容，例如针对手机发送精简的html
- 针对某些页面可以考虑使用inline css实现基本的样式，再异步加载(asynchronous laoding)额外的css //todo
- 按照重要性排序加载所需资源
- 减少dom深度，从而减少浏览器布局所需要的时间


## 其他
css is a render blocking resource

慎重使用Bootstrap、jquery(文件太大)，可以考虑使用zepto代替jquery，preact代替react

HTTP/1 时代，人们习惯将script、css打包成一个大的文件，因为多个请求的性能表现较差，但在HTTP/2 时代，上述问题已经不是一个问题，多个小的请求性能表现更好，因此可以将script拆开成较小的文件，每个页面只引用其所需的相关脚本即可[^2]

//todo 
rel="preload"
rel="preconnect"

[^1]: https://www.soasta.com/blog/mobile-web-performance-monitoring-conversion-rate/
[^2]: https://developers.google.com/web/fundamentals/performance/why-performance-matters/

