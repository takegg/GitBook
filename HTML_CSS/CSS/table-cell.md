# table-cell

```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8" />
    <title>test</title>
    <style>
    p { margin:0; }
    .right-content-title111 {border:1px solid black; width:400px; margin-top:15px;}
    .right-content-title111 span{
        border : 1px solid red;
        display: table-cell;
        width: 70%;
        text-align: center;
        height: 22px;
        vertical-align: middle;
    }
    .right-content-title222 {border:1px solid black; width:400px; margin-top:1px;}
    .right-content-title222 span{
        border : 1px solid red;
        display: table-cell;
        width: 40%;
        text-align: center;
        height: 22px;
        vertical-align: middle;
    }
    .right-content-title333 {border:1px solid black; width:520px; margin-top:1px;}
    .right-content-title333 span{
        border : 1px solid red;
        display: table-cell;
        width: 10%;
        text-align: center;
        height: 22px;
        vertical-align: middle;
    }
    </style>
</head>
<body>
    <p class="right-content-title111"><span>短</span></p>
    <p class="right-content-title222"><span>短</span></p>
    <p class="right-content-title333"><span>短</span></p>
    <p class="right-content-title111"><span>中中</span></p>
    <p class="right-content-title222"><span>中中</span></p>
    <p class="right-content-title333"><span>中中</span></p>
    <p class="right-content-title111"><span>长长长</span></p>
    <p class="right-content-title222"><span>长长长</span></p>
    <p class="right-content-title333"><span>长长长</span></p>
</body>
</html>
```
<img src="/HTML_CSS/img/table-cell.png">