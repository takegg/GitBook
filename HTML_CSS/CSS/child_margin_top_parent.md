# 子元素margin-top为何会影响父元素

```html
<style type="text/css">
        *{
            margin: 0px; padding: 0px; 
        }
        .show{
            margin: 0px auto;
            width: 200px;
            height: 100px;
            background-color: #999999;
        }
        .show h2{
            margin-top: 50px;/*important*/
            cursor: pointer;
        }
    </style>
    <div class="show">
        <h2>crystal</h2>
    </div>
```
## 来看css2.1盒模型中规定的内容：
> 所有毗邻的两个或更多盒元素的margin将会合并为一个margin共享之。毗邻的定义为：同级或者嵌套的盒元素，并且它们之间没有非空内容、Padding或Border分隔。

因为嵌套也属于毗邻，所以在样式表中优先级更高的 .show h2的margin覆盖了之前外层div定义的margin，导致最终整个div产生10px的间距。 
若给h2也添加一个class，并且在.show之前定义，则最终结果如第一个图所示，最终margin显示为0；

解决办法：

1. 父级或子元素使用浮动或者绝对定位absolute
浮动或绝对定位不参与margin的折叠

2. 父级overflow:hidden;

3. 父级设置padding（破坏非空白的折叠条件）

4. 父级设置border
