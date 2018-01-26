# Media queries that provide fluid breakpoints across different screen sizes

### Media type

Media type 用于描述设备的类型[^1]，可能的值为 `all` `screen` `print` `speech`

### Media feature

Media feature 用于描述设备、浏览器、环境的特定属性，常用到的有 `width` `height` `orientation` ，其中长宽分别都可以设置最大最小值 `max-width` `min-width` `max-height` `min-height`, 其他还有很多属性 →[^1]

> 注意！`device-width` `device-height` 为已弃用属性

### Logical operators {#Logical_operators}

可用的逻辑操作符为`and` `not` `only` `,`

> 注意！操作符中没有 `or` 但可以使用逗号，逗号的作用类似于or

#### and

当设备为“屏幕”，并且方向为“竖向”时，使用该样式

```css
@media screen and (orientation: portrait) {...}
```

#### not

> The `not` keyword can't be used to negate an individual feature expression, only an entire media query.

`not` 是对整个媒体查询表达式做“非”处理，而非单个表达式

对“除了屏幕宽度大于320px以外的”其他设备使用该样式

```css
@media not screen and (min-width: 320px) {...}
```

以下两种方式的代码效果是相等的，使用或不使用括号，都不会影响 `not` 只作用于**整个 media query**

```css
@media not screen and (color), print and (color) { ... }
```

```css
@media (not (screen and (color))), print and (color) { ... }
```

旧的浏览器无法识别`not` 这种类型，因此可以用来隐藏样式表，以下样式不会应用在旧的浏览器中

```html
<link rel="stylesheet" media="not screen and (color)" href="example.css" />
```

#### only

在使用only时，必须明确指定media type

只对“屏幕”宽度在320px到480px之间的设备使用该样式：

```css
@media only screen and (min-width: 320px) and (max-width: 480px) {...}
```

除此之外，`only`还可以用来在旧的浏览器中“隐藏”样式表，旧的浏览器只能够识别media type，而only不属于media type之一，因此会自动忽略`only` 开头的样式

> The keyword `only` can also be used to hide style sheets from older user agents. User agents must process media queries starting with `only` as if the `only` keyword was not present [^2] [^3]

（上面这句英文我实在是看不懂，到底是说旧的浏览器只能处理`only` 开头的语句还是说无法处理？？？）

> The `only` keyword prevents older browsers that do not support media queries with media features from applying the given styles. It has no effect on modern browsers. —— _MDN_ [^4]

这句说的比较清楚，我的理解是，早期的浏览器只支持media type，而不支持media queries with media features，如果没有`only`关键字， 以下将会被识别为 `screen`而宽度条件将会被忽略，导致所有`screen`都将应用该样式
```css
@media screen and (min-width: 320px) and (max-width: 480px) {...}
```

> #### 向早期浏览器隐藏媒体查询
>
> 媒体查询规范还提供了关键字only，它用于向早期浏览器隐藏媒体查询。类似于not，该关键字必须位于声明的开头。例如：
>
> ```
> media="only screen and (min-width: 401px) and (max-width: 600px)"
> ```
>
> 无法识别媒体查询的浏览器要求获得逗号分割的媒体类型列表，规范要求，它们应该在第一个不是连字符的非数字字母字符之前截断每个值。所以，早期浏览器应该将上面的示例解释为：
> ```
> media="only"
> ```
> 因为没有only这样的媒体类型，所以样式表被忽略。类似地，早期浏览器应该将以下语句解释为media="screen"：
>
> ```
> media="screen and (min-width: 401px) and (max-width: 600px)"
> ```
> 换句话说，它应该将样式规则应用于所有屏幕设备，即使它不知道媒体查询的含义。不幸的是，IE 6–8未能正确实现该规范。没有将样式应用到所有屏幕的设备，它将整个样式表一起忽略。
>
> 尽管存在此行为，如果希望向其他不太常用的浏览器隐藏样式，仍然建议在媒体查询前面添加上only。
>
> —— _infoQ_ [^5]

旧的浏览器中，不会应用该样式。新的浏览器中，只对彩色屏幕的设备使用该样式

```html
<link rel="stylesheet" media="only screen and (color)" href="example.css" />
```

（我还有个疑问，旧的浏览器是有多旧呢？）

#### , \(comma-separated-list\)

逗号用来分隔多个media query表达式，与or的作用相同。下例中对**最小宽度为680px或者屏幕为竖向**的设备应用该样式
```css
@media (min-height: 680px), screen and (orientation: portrait) { ... }
```

[^1]: https://developer.mozilla.org/en-US/docs/Web/CSS/@media#Media_types
[^2]: https://www.w3.org/TR/css3-mediaqueries/#media0
[^3]: https://stackoverflow.com/questions/8549529/what-is-the-difference-between-screen-and-only-screen-in-media-queries
[^4]: https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries
[^5]: http://www.infoq.com/cn/news/2011/12/introducing-media-queries

