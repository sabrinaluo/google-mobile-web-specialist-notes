# Promise

通过最近几年的历练，对promise的使用比较熟悉，再次就不作多详细的解释说明了。

需要注意的是，在使用promise的时候要避免嵌套promise，把promise写成callback hell的形式…而是应该在`then`和`catch`中return promise，之后在最外层使用`then`将多个promise连起来。

[1]: http://sabrinaluo.github.io/tech/2016/01/23/excecute-parallel-promise-and-sequential-promise/
[2]: http://sabrinaluo.github.io/tech/2016/01/23/excecute-parallel-promise-and-sequential-promise/