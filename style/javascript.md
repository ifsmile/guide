## js文件书写规范
> AMD 即异步模块定义,是适用于浏览器端的一种模块加载方式。

### 定义模块
```js
define(function() {
    ...
    return {} //没有输出时可以省略
})
```

### 引用模块
```js
(function() { // 立即执行函数，防止变量全局污染
    require(['a', 'b'], function(a, b) {
        console.log(a, b)
    })
})()
```
require有两个参数
+ `模块名称` （数组，与回调函数的参数按顺序照应）
+ `回调函数` （参数为所模块的输出）

### 引用公共模块
```js
require()
```

### 在本项目中的script标签中引入js
```html
<script data-main="/js/home" src="/lib/require/require.js"></script>
```
- src需要引入require.js
- data-main 为入口js文件
- 在home.js中需要先引入公共模块common.js

```js
(function() {
    require(['common'], function() { // 引入common.js
        require(['css!/css/common.css']) // 引入css,路径需要以css!开头
        require(['jquery', 'easyui'], function($, easyui) { // 引入common之后再引入其他依赖
            ...
        })
    })
})()
```