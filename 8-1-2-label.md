# Appropriate label tags associated with inputs

label是可点击的，当点击lable时，对应的表单元素会被focused

```html
<div>
  <label for="username">Name: <abbr title="required">*</abbr></label>
  <input id="username" type="text" name="username">
</div>
```

### Best practice
- 为label设置`for`属性，值为对应`input`的`id`
- 尽量使label所占的区域大一些，方便点击，尤其是单选按钮和复选框的label
- 避免对同一个表单元素使用多个label，一些辅助设备可能无法正确识别多个label从而造成错误
