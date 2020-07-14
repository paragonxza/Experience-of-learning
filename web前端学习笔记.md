# web前端学习笔记

## 第一章

### 1.1 浏览器内核

- JS引擎
- 渲染引擎
  - Trident（IE内核）；EdgeHTML（Edge内核）
  - Gecko（Firefox内核）
  - webkit（Safari内核）
  - Blink（Chrome内核）

### 1.2 web标准

- 结构标准：用于对网页元素进行整理和分类，主要包括XML和XHTML两部分，即.html。
- 样式标准：用于设置网页元素的外观样式，主要指CSS，即.css。
- 行为标准：指网页模型的定义及交互的编写，主要包括DOM和ECMAScrpit两部分，即.js。

## 第二章

### 2.1 HTML基本格式

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
</body>
</html>
```

### 2.2 webstorm常用快捷键

```html
<!--
>：下一个子标签
*：多少个标签
$：标签的名称序号
{}:标签的内容
[]:标签的引用属性
-->

<!--输入：h1,按tab键-->
<h1></h1>
 
<!--输入：div#abc,按Tab键-->
<div id="abc"></div>
 
<!--输入：div.abc,按Tab键-->
<div class="abc"></div>

<!--输入  ul>li*5>a[href=#]{我是第$个} 再按tab键-->
<ul>
    <li><a href="#">我是第1个</a></li>
    <li><a href="#">我是第2个</a></li>
    <li><a href="#">我是第3个</a></li>
    <li><a href="#">我是第4个</a></li>
    <li><a href="#">我是第5个</a></li>
</ul>
 
<!--输入 li*3>div.img>img[src='images/$.jpg'] 再按tab键-->
<li>
    <div class="img"><img src="images/1.jpg" alt=""></div>
</li>
<li>
    <div class="img"><img src="images/2.jpg" alt=""></div>
</li>
<li>
    <div class="img"><img src="images/3.jpg" alt=""></div>
</li>

<!--快速生成for循环-->
<script>
        /* for循环：输入itar,再点击tab键*/
        for (var i = 0; i < array.length; i++) {
            var obj = array[i]; 
        }
</script>


<!--div#tab1+div#tab2-->
 
<div id="tab1"></div>
<div id="tab2"></div>

<!--引入  link   加tab键-->
    <link rel="stylesheet" href="">
 
    <!--引入css   link:css   加tab键 -->
    <link rel="stylesheet" href="css/mycss.css">
 
    <!--引入js    script:src  加tab键-->
    <script src=""></script> 
 
    <!--html中插入js   script  加tab键-->
    <script></script>

<!--input:button 加tab键-->
<input type="button" value="">

<!--form:get-->
<form action="" method="get"></form>
<!--form:post-->
<form action="" method="post"></form>
```

### 2.3 