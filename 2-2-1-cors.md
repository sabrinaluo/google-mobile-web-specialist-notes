# Cross-Origin Resource Sharing

经常会在浏览器里看到有关CORS的报错，浏览器实现时，为了保证安全性，而采用了同源策略。

同源的意思是，必须要满足**协议、域名、端口**都相同，才是同源，否则为非同源。

如果希望某些数据能够被非同源的地址所访问，服务器端需要在response的headers中加入`alldow-control-allow-origin: *`这样便能让所有地址访问该资源。

如果希望只有特定的地址、域名能够访问该资源，则可以将`*`替换为对应的地址。

[1]: https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS
[2]: http://sabrinaluo.github.io/tech/2016/01/22/understanding-of-CORS/