# Vue学习笔记

## 知识点

```bash
# 三要素
el(挂载点),data(数据),methods(方法)

# v-text
设置元素的文本值
<p v-text="aaa"></p>等价于<p>aaa</p>

# v-html
与v-text用法一致，只是内容可以嵌套html语句

# v-on
绑定事件
<input type="button" @click="fun">

# v-show
根据表达式的真假，切换元素的显示和隐藏
<img src="xxx" v-show="age>=18">

# v-if
跟v-show用法一致

# v-bind
设置元素的属性（比如src，title，class）
<img :src="imgSrc" :class="{active:isActive}">

# v-for
根据数据生成列表结构
<li v-for="item in arr">
<li v-for="(item,index) in arr">

# v-mode
获取和设置表单元素的值（双向数据绑定）
<input type="text" v-mode="message">
```



## 模板

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue</title>
    <!-- 导入vue -->
    <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        
    </div>
    <script>
        var app = new Vue({
            el: "#app",
            data: {
                num: 1
            },
            methods: {
                fun: function () {
                    
                }
            }
        })
    </script>
</body>

</html>
```

