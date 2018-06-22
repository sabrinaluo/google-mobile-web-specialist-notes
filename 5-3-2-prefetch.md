# Prefeching files
## prefetch
prioriy较低，对当前页面用处不大。浏览器会优先下载有`preload`的资源。

### Link Prefetching
告诉浏览器去拿resource然后存在cache中，等到用户需要打开相关页面/资源时，无需再次下载以节约下载时间。（需要自己预测哪些资源/页面用户很可能会在接下来点击）

这个请求可以在HTML里做，也可以在HTTP Header里做。

HTML中：
```html
<link rel=”prefetch” href=”/uploads/images/pic.png“>
```

HTTP Header中：
```
Link: </uploads/images/pic.png>; rel=prefetch
```

### DNS Prefetching
当请求一个页面时，如果浏览器对这个domain没有执行过DNS Lookup（查询DNS记录，查看服务器是否能够正常解析域名），则需要一定时间来执行。DNS请求的数据量很小，但是延迟却很高。
通常当页面的某些resource放在CDN上或是通过url引用了第三方资源，第一次加载时就会需要执行DNS Lookup

在chrome中可以通过地址栏访问`chrome://dns/`来查看那些DNS已经解析过了

```html
<link rel="dns-prefetch" href="http://www.example.com/">
```