# for ... of

无法取到index，只能取到value。
原生的Object不可以使用for of

## for of与for in的区别
> Both `for...in` and `for...of` statements iterate over something. The main difference between them is in what they iterate over.

The `for...in` statement iterates over the **enumerable properties** of an object, in an arbitrary order.

The `for...of` statement iterates over data that **iterable object** defines to be iterated over.

## 可使用for in的类型
- Array
- String
- arguments (an array like object)
- NodeList
- TypedArray (new in ES2017)
- Map
- Set