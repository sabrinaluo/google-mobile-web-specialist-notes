# Client storage
Providing client storage that is appropriate to a web application’s data persistence needs
使用客户端storage实现data persistence

## session状态管理
TODO: 

## cache [experimental]
TODO: 缓存请求及响应，（主要用在service worker？？）


## storage (local, session)
浏览器/客户端中中的storage分为两种，分别是`localStorage`和`sessionStorage`。
storage只能在对应的（当前）域名下读写，也就是说A域名下的storage在B域名下是无法读写的。

这两项都可以在chrome dev tool中的Application标签下查看。

其中`sessionStorage`在session断开后自动清除，`localStorage`则会一直保留。

**注意！两种storage都是没有expiry date的**
要实现expire storage只能手动添加timestamp进行检测

两种storage都有以下方法
- key(index) - 获取第x个项目的key，index从0开始，（应该是按照storage创建的先后顺序排列）
- getItem(key) - 获取一个项目
- setitem(key, val) - 设置某个项目，如果该项目不存在则创建一个新的项目，如果存在则更新项目
- removeItem(key) - 删除某个项目
- clear() - 清除所有项目

**storage是key-value的形式，其value是字符串类型，可以使用`JSON.stringify` `JSON.parse`来实现对象的存储**

### localStorage与cookie的区别
cookie会自动被添加在请求的头部，服务器可以识别cookie，通常会加密  
localStorage不会出现在请求中，服务器无法识别，通常不加密，用户可以随意改动，不适合储存安全敏感信息

## IndexedDB
IndexedDB适合存储大量结构性的数据，检索性能较好；  
web storage只适合存储小量数据。(似乎indexedDB比较适合web worker使用，web worker和service worker又是不同的😓 
TODO: 研究一下各种worker)

IndexedDB是事务性数据库，类似于SQL那样的关系型数据库。

https://developer.mozilla.org/en-US/docs/Web/API/Cache
https://developer.mozilla.org/en-US/docs/Web/API/Storage
https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API