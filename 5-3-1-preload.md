# Prefeching files
## preload
写在`<head>`中，用于声明之后很快会用到的资源，提前下载，不会阻塞页面渲染。
在需要使用这些资源的地方，按照通常的方法来使用，所以会见到两个包含某条url的`<link>`标签，一个用于提前下载，一个用于执行。例如：
```html
<head>
<meta charset="utf-8">
<title>JS and CSS preload example</title>

<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">

<link rel="stylesheet" href="style.css">
</head>

<body>
<h1>bouncing balls</h1>
<canvas></canvas>

<script src="main.js"></script>
</body>
```

### 语法
```html
<link rel="preload" href="image.png">
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
<link rel=“preload” href=“https://example.com/fonts/font.woff” as=“font” crossorigin>
<link rel="preload" href="https://blog.keycdn.com/blog/css/mystyles.css" as="style">
```

`preload` 可以用于包括以下几种类型：
- script
- style
- font
- image
- document (resource to be embedded inside `<frame>` or `<iframe>`)
- embed
- object (resource to be embedded inside `<embed>`)
- track (WebVTT file)
- worker (js web worker or shared worker)
- audio
- video

注意：当资源跨域时，需要加一个`crossorigin`属性，否则？？？ // todo

### `as` 属性
- Prioritize resource loading more accurately.
- Match future requests, reusing the same resource if appropriate.
- Apply the correct content security policy to the resource.
- Set the correct Accept request headers for it.

### `type`属性 | MIME type
```
<link rel="preload" href="sintel-short.mp4" as="video" type="video/mp4">
```
浏览器读取`type`属性后，如果支持该类型则会下载，如果不支持该类型则会忽略，不会下载，以免浪费

### cross-origin
```html
<link rel="preload" href="fonts/cicle_fina-webfont.woff2" as="font" type="font/woff2" crossorigin="anonymous">
```
如果资源是跨域的，需要添加crossorigin属性，否则？？？ //TODO  
对于字体font，不管是否跨域都需要使用anonymous mode CORS，如上所示

### media
```html
<link rel="preload" href="bg-image-narrow.png" as="image" media="(max-width: 600px)">
<link rel="preload" href="bg-image-wide.png" as="image" media="(min-width: 601px)">
```
支持media type / media query从而实现responsive preload

### script
通过preload还可以做到提前下载script但不执行，在需要的时候才执行
```javascript
// to preload the script
var preloadLink = document.createElement("link");
preloadLink.href = "myscript.js";
preloadLink.rel = "preload";
preloadLink.as = "script";
document.head.appendChild(preloadLink);

// to use it
var preloadedScript = document.createElement("script");
preloadedScript.src = "myscript.js";
document.body.appendChild(preloadedScript);
```

### 参考
[1] https://www.machmetrics.com/speed-blog/guide-to-browser-hints-preload-preconnect-prefetch/
[2] https://developer.mozilla.org/en-US/docs/Web/HTML/Preloading_content
[3] https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types
