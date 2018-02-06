# Form

### 表单元素 [^1]
- button
- datalist 很像select，区别是除了列出的选项，用户还可以随意输入任何值，同时也能根据用户输入的值过滤出一个符合的列表显示出来。safari不支持此元素。
- fieldset 默认样式是有个方框框起所有子元素
- form
- input
- label
- legend 通常是`fieldset`的子元素
- meter 类似于progress bar，IE不支持此元素
```html
<p>Heat the oven to <meter min="200" max="500" value="350">350 degrees</meter></p>
```
- optgroup 将select元素中的option分组，可在列表中显示每组的名称
- option
- output 配合form的oninput回调，能够根据函数动态显示输出值[^2]。IE不支持此元素
```html
<form oninput="result.value=parseInt(a.value)+parseInt(b.value)">
    <input type="range" name="b" value="50" /> +
    <input type="number" name="a" value="10" /> =
    <output name="result">60</output>
</form>
```
- progress progress bar
```html
<progress value="70" max="100">70 %</progress>
```
> 与`<meter>`的区别，大多数浏览器都支持progress，progress不可以设置最小值`min/low`

- select 支持多个属性，注意`multiple`多选，`size`设置后为带滚动条的方框，可以同时显示多个备选项
- textarea 多行文本输入

此外，在表单中使用h1, h2, div, p, span, section等元素都是比较常见的

### Best practice
- 不要嵌套form

[^1]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element#Forms
[^2]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/output