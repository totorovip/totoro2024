### 如果做水平垂直居中

水平垂直居中是常见的布局需求，比如登录弹窗。

| 方法                          | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| 使用 Flexbox 布局             | 使用 Flexbox 布局可以轻松实现元素的水平和垂直居中。设置父元素的 `display: flex` 和 `justify-content: center; align-items: center;`。 |
| 使用 Grid 布局                | 使用 CSS Grid 布局同样可以实现元素的水平和垂直居中。将父元素设为网格容器，然后使用 `place-items: center;`。 |
| 使用绝对定位和 transform 属性 | 将要居中的元素设置为 `position: absolute`，然后利用 `top: 50%; left: 50%; transform: translate(-50%, -50%);` 来进行居中。 |
| 使用表格布局                  | 创建一个包含单元格的表格，然后将内容放置在表格单元格中，并设置单元格样式为 `text-align: center; vertical-align: middle;`。 |
| 使用绝对定位和负 margin 值    | 将要居中的元素设置为 `position: absolute`，然后使用 `top: 50%; left: 50%; margin: -128px(元素大小)` 来进行居中。 |

