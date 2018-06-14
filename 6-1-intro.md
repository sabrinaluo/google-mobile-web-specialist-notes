# Testing and Debugging

## Unit test

## Setting breakpoints
- event listener breakpoint
- conditional breakpoint
- XHR breakpoint
- DOM changeb breakpoint
- function breakpoint
```javascript
function sum(a, b){
	let result = a+ b;
	return result;
}
debug(sum) //注意这里传入函数对象
sum(1, 2); //执行sum函数时，会自动调用debugger
```

## Console log
- `console.log`
- `console.warn`
- `console.error`
- `console.group` / `console.groupEnd` 
在GA Debugger中经常见到的log输出，将相关的log放在同一组，可以折叠； 组与组可以嵌套
- `console.assert`
当断言结果为`true`，则不会输出任何log，为`false`则输出`Asserion failed: xxx`错误
```javascript
console.assert(list.childNodes.length <= 500, "Node count is > 500");
```
- `console.dir` 
可以将DOM以js object的形式输出

### 字符串替代及格式化
|Specifier|Output|
|----|----|
|%s|Formats the value as a string|
|%i or %d|Formats the value as an integer|
|%f|Formats the value as a floating point value|
|%o|Formats the value as an expandable DOM element. As seen in the Elements panel|
|%O|Formats the value as an expandable JavaScript object|
|%c|Applies CSS style rules to the output string as specified by the second parameter|

## Reproducing & fixing bugs

## Other
- blackbox
- source tab下按esc会弹出console