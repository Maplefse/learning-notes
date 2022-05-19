# BootsStrap

### bootstrap介绍

一个前端框架，包含HTML，CSS，JavaScript

用于开发响应式及移动设备优先的web项目前端框架

### bootstrap的搭建

```html
<!DOCTYPE html>
<!--设置正确的文档类型,避免样式的异常问题-->
<html lang="zh-CN">
	<head>
		<meta charset="utf-8" />
		<title></title>
        <!--引入bootstarp的css主文件;必须要在所有css文件的最上方-->
		<link rel="stylesheet" type="text/css" href="css/bootstrap.min.css" />
	</head>
	<body>
	</body>
    <!--bootstrap的js依赖于jquery文件,所以首先导入jquery-->
	<script src="js/jquery.js"></script>
    <!--导入bootstrap的js主文件-->
	<script src="js/bootstrap.min.js"></script>
</html>
```

### bootstrap的主要容器

1. 流体容器

   ```html
   <div class="container-fluid">test</div>
   <!--流体容器会随着页面大小的更改自动适应容器自身的大小,相当于设置了width:100%-->
   ```

2. 固定容器

   ```html
   <div class="container">test</div>
   <!--固定容器有四个个固定的阈值-->
   <!--阈值		容器宽
   	1200	  1140
   	992		  960
   	768		  720
   	576		  540
      小于576	 auto
   当页面大于或者等于这些阈值的时候,容器会自动适应阈值对应的宽度
   -->
   ```

3. 栅格系统

   ```html
   <div class="container">
   	<div class="row">
   		<div class="col-lg-10">col-lg-10</div>
   		<div class="col-lg-2">col-lg-2</div>
   	</div>
   </div>
   <!--bootstrap默认将栅格一行分成12列
   	lg后面的数为占用的列数
   -->
   
   
   <div class="col-lg-2 col-md-4 col-sm-6 col-xs-8">col-lg-2</div>
   <!--栅格在创建时,使用这种方式,会自动适应屏幕分辨率对栅格占用大小进行改变
   lg
   
   -->
   ```

   栅格必须包含在容器之中

   在栅格系统中不同屏幕分辨率由不同的名字代替

   ```scss
   /* 超小屏幕（手机，小于 768px） */
   xs
   
   /* 小屏幕（平板，大于等于 768px） */
   sm
   
   /* 中等屏幕（桌面显示器，大于等于 992px） */
   md
   
   /* 大屏幕（大桌面显示器，大于等于 1200px） */
   lg
   ```

   ## 列偏移

   使用 `.col-md-offset-*` 类可以将列向右侧偏移。这些类实际是通过使用 `*` 选择器为当前元素增加了左侧的边距（margin）。例如，`.col-md-offset-4` 类将 `.col-md-4` 元素向右侧偏移了4个列（column）的宽度。

   ## 列排序

   通过使用 `.col-md-push-*` 和 `.col-md-pull-*` 类就可以很改变列（column）的顺序。

4. 