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

method - `GET`, `POST`, `PUT`, `DELETE`, `HEAD`
url - URL of the request
headers - 请求的头
referrer - referrer of the request
mode - `cors`, `no-cors`, `same-origin`
credentials - 请求是否包含cookies `omit`, `same-origin`
redirect - `follow`, `error`, `manual`
integrity - subresource integrity value
cache - 缓存模式 (`default`, `reload`, `no-cache`)

 

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

## Response
### Response对象的属性：
type - 请求类型
- `same-origin`
- `cors`
- `cors-with-forced-preflight`
- `no-cors`

url - 请求地址
useFinalURL - Boolean for if url is the final URL
status - 状态码 (ex: 200, 404, etc.)
ok - 请求是否成功 (状态码为 200-299)
statusText - status code (eg. OK)
headers - 与response相关的头.

### Response对象的方法
clone() - 克隆response对象
error() - Returns a new Response object associated with a network error.
redirect() - Creates a new response with a different URL.
arrayBuffer() - 返回一个promise，resolve的是ArrayBuffer.
blob() - 返回一个promise，resolve的是Blob.
formData() - 返回一个promise，resolve的是FormData object.
json() - 返回一个promise，resolve的是JSON object.
text() - 返回一个promise，resolve的是USVString (text).

[^1]: https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters


