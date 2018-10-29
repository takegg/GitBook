# 撑开父层

## 方法一：

```html
<style>
.example{
  background: #008000;
  width: 400px;
  margin: 10px;
  padding: 10px;
}
.example .childrenDiv{
  float: left;
  height: 100px;
  width: 100px;
  word-break: break-all;
  word-wrap: break-word;
}
</style>
<!--示例-->
<div class="example">
    <div class="childrenDiv" style="background: #e9b216;">tatatattttaatatatatatatata</div>
    <div class="childrenDiv" style="background: #df4744;">tatatattttaatatatatatatata</div>
    <!--解决方法-->
    <div style="clear: both;"></div>
</div>
```

## 方法二：**推荐**
```html
<style>
.clearfix:after{
            content:".";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
}
/* Hides from IE-mac \*/
*html.clearfix{height: 1%;}
/*end hide from IE-mac*/
</style>

<!--方法二-->
<div class="clearfix example">
    <div class="childrenDiv" style="background: #e9b216;">tatatattttaatatatatatatata</div>
    <div class="childrenDiv" style="background: #df4744;">tatatattttaatatatatatatata</div>
</div>
```
>分析：
父div作为外部容器，子div设置了float样式，则外部容器div因为内部没有clear导致不能被撑开，即内部div因为float：left之后，就丢失了clear：both和display：block的样式。

## 方法三：

```html
<!--方法三-->
<div class="example" style="overflow: hidden;">
    <div class="childrenDiv" style="background: #e9b216;">tatatattttaatatatatatatata</div>
    <div class="childrenDiv" style="background: #df4744;">tatatattttaatatatatatatata</div>
</div>
```

## 方法四：
```html
<!--方法四-->
<div class="example" style="display: table;">
    <div class="childrenDiv" style="background: #e9b216;">tatatattttaatatatatatatata</div>
    <div class="childrenDiv" style="background: #df4744;">tatatattttaatatatatatatata</div>
</div>
```