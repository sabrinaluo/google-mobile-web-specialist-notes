# Fluid break point of responsive design

### 如何选择 breakpoint
- 应该根据内容创建Breakpoint，不应该根据特定设备的大小
- 先从最小尺寸的设备开始设计，然后逐步增大尺寸
- 每行最多大约70到80个英文字符，大约40-50个中文汉字

#### Major breakpoint
设备尺寸大全：https://material.io/devices/

Major breakpoint 是用于布局宽度的主要breakpoint，可参考bootstrap的尺寸设计[^1]：

| size | min-width | max-width |
|---:|---:|---:|
| xs | - | 575px |
| sm | 576px | 767px |
| md | 768px | 991px |
| lg | 992px | 1199px |
| xl | 1200px | - |

- min-width与典型设备宽度相同
- max-width比典型设备宽度小1px

#### Minor breakpoint
Minor breakpoint 介于上述各breakpoint之间，主要用于处理padding、margin、font-size等内容尺寸，而非布局尺寸。例如。在`576px`到`767px`之间增加一个`650px`以实现同一布局下，字体大小的不同

### Best practice
- 不要因为无法适配而隐藏内容
- 对于大尺寸屏幕，最好限定其 `width` / `max-width`(显示效果为两边留白)，以免内容填充满整个屏幕影响阅读体验。


[^1]: https://v4-alpha.getbootstrap.com/layout/overview/
