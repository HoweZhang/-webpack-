#学习webpack的记录
==========
第一步 安装  （基于node和cnpm）
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
cnpm install css-loader style-loader   //（安装一些需要的loader）
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
创建style.css
```
body {
    background: yellow;
}
```
创建webpack.config.js
```
module.exports = {
	entry:"./demo1.js",
	output:{
		path:__dirname,
		filename:"bundle.js"
	},
	module:{
		loaders:[
			{test:/\.css$/,loader:"style-loader!css-loader"}
		]
	}
}
```
第三步 运行  
---
```
webpack-dev-server --progress --colors
```
运行起来后直接修改css或者js，浏览器不用刷新也能看到改动后的结果。
退出 
---
```
Ctrl+c
```

