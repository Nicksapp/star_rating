# 星星评价组件

## 结构样式
```html
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <title>Document</title>
 <style>
 ul {
  padding-left: 0;
  overflow: hidden;
 }
 ul li {
  float: left;
  list-style: none;
  width: 27px;
  height: 27px;
  background: url(img/star.gif)
 }
 ul li a {
  display: block;
  width: 100%;
  padding-top: 27px;
  overflow: hidden;
 }
 ul li.light {
  background-position: 0 -29px;
 }
 </style>
</head>
<body>
 <ul>
  <li class="light"><a href="javascript:;">1</a></li>
  <li><a href="javascript:;">2</a></li>
  <li><a href="javascript:;">3</a></li>
  <li><a href="javascript:;">4</a></li>
  <li><a href="javascript:;">5</a></li>
 </ul>
</body>
</html>
```
li加了light的class就会变成亮星，就是换了背景位置，把空心的星星变成了实心的。所以js实现的时候点亮就是给li加一个light的类名。

## 交互js
```javascript
<script>
var num=finalnum = tempnum= 0;
var lis = document.getElementsByTagName("li");
//num:传入点亮星星的个数
//finalnum:最终点亮星星的个数
//tempnum:一个中间值
function fnShow(num) {
 finalnum= num || tempnum;//如果传入的num为0，则finalnum取tempnum的值
 for (var i = 0; i < lis.length; i++) {
  lis[i].className = i < finalnum? "light" : "";//点亮星星就是加class为light的样式
 }
}
for (var i = 1; i <= lis.length; i++) {
 lis[i - 1].index = i;
 lis[i - 1].onmouseover = function() { //鼠标经过点亮星星。
  fnShow(this.index);//传入的值为正，就是finalnum
 }
 lis[i - 1].onmouseout = function() { //鼠标离开时星星变暗
  fnShow(0);//传入值为0，finalnum为tempnum,初始为0
 }
 lis[i - 1].onclick = function() { //鼠标点击,同时会调用onmouseout,改变tempnum值点亮星星
  tempnum= this.index;
 }
}
</script>
```

这样设计的一个关键点在于，mouout时保存一个值用于让星星变暗，初始为0（0颗星变亮就是全暗），不点击的话只要鼠标离开所有星星都是暗的，click事件会触发一次mouseover和一次mouseout，所以点击时改变tempnum确定鼠标离开时几颗星亮，这个值会一直保持，直到下次点击时改变它。
