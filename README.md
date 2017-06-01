#学习webpack的记录
==========
第一步 安装  
---
    
```
mkdir app    //(创建文件夹，然后进入该文件夹)
```
   
  
```
npm init    //(初始化，生成package.json文件)
```    
          
```
cnpm install webpack --save   //（--save是将webpack安装在当前文件夹）
```
    
```
cnpm install webpack-dev-server --g   //（全局安装静态资源服务器）
```    
   
第二步 配置  
---
创建demo1.js    
```
require("!style-loader!css-loader!./style.css");
document.write(require("./demo2.js"));
```
创建demo2.js
```
module.exports = "It works from demo2.js.";
```
创建index.html
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
	<script type="text/javascript" src="bundle.js"></script>
</body>
</html>
```


