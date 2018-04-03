# Fetch data
`fetch()` 是一个与 XHR 类似的用于发送请求获取数据的API。

`fetch()`是基于promise的，API简单，且能够使用Promise chain来避免callback hell。对于不支持`fetch()`的浏览器，可以使用github的[fetch polyfill](https://github.com/github/fetch)

目前暂时还不支持cancel一个fetch请求。

## 使用`fetch()`获取数据 GET
```javascript
fetch('./api/data.json' /* {options} */)
  .then(response => {
    console.log(response);
    return response.json(); // 返回一个promise
  })
  .catch(err => {
    console.log(err);
  })
  .then(data => {
    console.log(data); // json数据
  });
```

需要注意的是，与[axios](https://github.com/axios/axios)之类的库不同，通常情况下fetch返回的都是一个resolved promise (then)，需要通过判断`response.status`来确定服务器返回的是否是error。

只有当**浏览器级别**的error发生时，才会返回一个rejected promise (catch)，也就是说，服务器端的任何error都不会反应在`catch`中。

### `options`
`options`中可以设置`method`、`headers`等选项，具体请参考文档[^1]

- method - `GET`, `POST`, `PUT`, `DELETE`, `HEAD`
- url - 请求地址
- headers - 请求的头
- referrer - 请求的来源地址
- mode - 请求模式（不知道干什么用的，不设置的话会有什么问题？）
  - `cors`
  - `no-cors`
  - `same-origin`
- credentials - 请求是否包含cookies `omit`, `same-origin`
- redirect - 重定向模式，当收到301/302时如何处理
  - `follow` 自动重定向（旧版本浏览器默认值）
  -  `error` 抛出异常
  - `manual` 手动处理重定向（新版本浏览器默认值）
- integrity - 包括请求的 subresource integrity 值 （不知道是啥）
- cache - 缓存模式 (`default`, `reload`, `no-cache`)

### request 对象

除了上述的请求方式，还可以创建一个`request`对象作为`fetch()`的参数
```javascript
const myRequest = new Request(url, options);
fetch(myReuqest)
  .then(/* do somthing */);
```

!注意，request对象由于被设计成stream方式，所以只能被使用（读取）一次，但可以传入一个存在的request对象来生成一个拷贝
```javascript
const anotherRequest = new Request(myRequest);
```

## 使用`fetch()`发送数据 POST

```javascript
fetch(url, {
    method: 'post',
    headers: {},
    body: {}
  })
  .then(response => {
    console.log(response);
    return response.json(); // 返回一个promise
  })
  .catch(err => {
    console.log(err)
  })
  .then(data => {
    console.log(data); // json数据
  });
```

## Response [^2]
### Response对象的属性：
- type - 请求类型
  - `same-origin`
  - `cors`
  - `cors-with-forced-preflight`
  - `no-cors`
- url - 请求地址
- useFinalURL - Boolean 是否是这个response的最终url（不知道干啥的，可能和重定向有关）
- status - 状态码 (ex: 200, 404, etc.)
- ok - 请求是否成功 (状态码为 200-299)
- statusText - 状态信息 (eg. OK)
- headers - 与response相关的头

### Response对象的方法
- clone() - 创建一个response对象的拷贝
- error() - 返回一个绑定了网络错误的response对象
- redirect() - ongoing另一个URL创建一个新的response对象

- arrayBuffer() - 返回一个promise，resolve的是ArrayBuffer
- blob() - 返回一个promise，resolve的是Blob
- formData() - 返回一个promise，resolve的是FormData object
- json() - 返回一个promise，resolve的是JSON object
- text() - 返回一个promise，resolve的是USVString (text)

前三个方法都不知道是干啥的…

[^1]: https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters
[^2]: https://developer.mozilla.org/en-US/docs/Web/API/Response


