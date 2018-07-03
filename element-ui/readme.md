按需加载
~~~
npm i element-ui --save
npm install babel-plugin-component -D//安装按需引入的组件

//修改.babelrc的配置
"plugins": [
    "transform-vue-jsx",
    "transform-runtime",
    ["component",[
      {
        "libraryName":"element-ui",
        "styleLibraryName":"theme-chalk"
      }
    ]]
  ],
  "env": {
    "test": {
      "presets": ["env", "stage-2"],
      "plugins": ["transform-vue-jsx", "istanbul"]
    }
  }
~~~
具体参考[element-ui](http://element-cn.eleme.io/#/zh-CN/component/quickstart)
