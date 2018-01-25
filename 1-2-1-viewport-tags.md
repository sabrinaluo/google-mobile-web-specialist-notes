# Appropriate document type declaration and viewport tags

## Viewport

viewport是众多 meta tag 中的一个，是专门为手机浏览器定义的一个标签。通常用来控制页面宽度和缩放，一般写成这样:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

* 设置页面宽度与设备宽度相同
* 设置初始缩放为1，使 css 像素与 device-independent 像素对应关系为1:1
* 使用不同属性间用**逗号**隔开，确保一些版本较旧的浏览器也能正确解析相关属性

_由于 iphone 等高分辨率的手机使用 retina 屏幕，其像素密度大于1，默认情况下，电脑里的10px，在 iphone 上看起来像是只有一半甚至1/3大小，设置 _`initial-scale=1`_ 可以使电脑和手机里看起来大小一样。_

### 可用属性

| 属性 | 值 | 描述 |
| :--- | :--- | :--- |
| width | 正整数，或 device-width |  |
| height | 正整数，或 device-height |  |
| initial-scale | 0.0 到 10.0 之间的数 |  |
| minimum-scale | 0.0 到 10.0 之间的数 |  |
| maximum-scale | 0.0 到 10.0 之间的数 |  |
| user-scalable | yes 或 no |  |

### Best Practice

* 不要使用固定宽度的元素
* 网页内容不应该依赖某个特定宽度
* 使用百分比来设置元素的宽度`100%`



