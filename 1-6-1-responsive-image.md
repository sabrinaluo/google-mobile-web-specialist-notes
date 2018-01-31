# Responsive images 
that adjust for the dimensions and resolution of any mobile device

- 使用相对尺寸(relative size)以避免图片超出容器

### img
图片的分辨率分为：
- 自然分辨率(natural resolution)，图片原始大小
- 显示分辨率(display resolution)，图片在页面中显示大小

`<img>` 有 `width` 和 `height` 属性(html markup)，单位为`px`或`vw`/`vh` (viewport width / viewport height，相对长度单位)，`vmin` / `vmax`

html5中新增了`sizes`属性，其中包含两个值：
1. media condition，最后一项值中必须省略media condition，相当于else分支
2. 尺寸值

```html
<img src="400.png" 
     sizes="(min-width: 600px) 25vw, (min-width: 500px) 50vw, 100vw"
     srcset="100.png 100w, 200.png 200w, 400.png 400w,
             800.png 800w, 1600.png 1600w, 2000.png 2000w" alt="an example image">
```

上例中，当viewport宽度 > 600px 时，图片宽度为25vw，当500px < viewport宽度 < 600px 时，图片宽度为50vw，其他情况下图片宽度为**100vm** (最后一项值省略了media condition)

> media condition的顺序会影响显示结果，如果上例中如果调换顺序，`sizes="(min-width: 500px) 50vw, (min-width: 600px) 25vw, 100vw"`，25vw这个大小将永远不会显示

> 如果没有`srcset`属性或`srcset`属性中没有宽度描述符`w`d 值，`sizes`将会被忽略

### srcset
`srcset`是html5中的新属性。使用`srcset`时，浏览器可以自动选择最合适的图片进行显示。

srcset中的描述符可以是
- `w`，宽度，(px wide) 这个宽度将会除以`sizes`中的值，从而计算出像素密度
- `x`，密度
如果没有声明描述符，默认值为`1x`

```html
<img src="photo.png" srcset="photo@2x.png 2x" ...>
```

```html
<img src="lighthouse-200.jpg" sizes="50vw"
     srcset="lighthouse-100.jpg 100w, lighthouse-200.jpg 200w,
             lighthouse-400.jpg 400w, lighthouse-800.jpg 800w,
             lighthouse-1000.jpg 1000w, lighthouse-1400.jpg 1400w,
             lighthouse-1800.jpg 1800w" alt="a lighthouse">
```
下列表格详尽的展示了各种屏幕尺寸下使用的图片[^1]

|浏览器宽度|设备像素比例|使用的图片|有效的分辨率|
|:--|:--|:--|:--|
|400px|1|200.png|1x|
|400px|2|400.png|2x|
|320px|2|400.png|2.5x|
|600px|2|800.png|2.67x|
|640px|3|1000.png|3.125x|
|1100px|1|1400.png|1.27x|

这个计算公式计算是先算出各个图片的有效分辨率，与设备分辨率进行对比，从而选择最合适的，例如，浏览器640px，像素密度3，使用的图片为1000w
800 / (640 \* 50%) = 2.5
1000 / (640 \* 50%) = 3.125
1400 / (640 \* 50%) = 4.375
通过计算，发现1000w图片的有效分辨率是最接近3的，所以浏览器加载并显示1000w的图片

> IE 8及以下不支持`srcset`

### `<picture>`
如果希望在不同的设备上应用不同的图片，除了使用`<img>`元素之外，还可以使用`<picture>`元素。

```html
<picture>
  <source media="(min-width: 800px)" srcset="head.jpg, head-2x.jpg 2x">
  <source media="(min-width: 450px)" srcset="head-small.jpg, head-small-2x.jpg 2x">
  <img src="head-fb.jpg" srcset="head-fb-2x.jpg 2x" alt="a head carved out of wood">
</picture>
```

> IE 不支持`picture`元素

### 图片压缩
图片压缩工具
- http://imagemagick.org/
- https://imageoptim.com/mac

### font icon
尽量少使用图片，减少网络请求次数，从而提高网页速度。

一些图标可以直接使用 unicode-table.com/en ，在使用时，最好直接复制粘贴特殊符号，而不是html code

font icon
- weloveiconfonts.com
- zocial
- fontawesome

### 参考
[^1]: https://developers.google.com/web/fundamentals/design-and-ux/responsive/images
https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img

