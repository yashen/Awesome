* https://cn.vuejs.org/
* https://cn.vuejs.org/v2/api/

#属性
## el
指定Vue实例的挂载目标,可以是css选择器或者一个HtmlElement对象

可以使用xx.$el访问到挂载的HtmlElement对象


## data
指定所绑定的数据对象,可以通过app.$data到原始数据对象

另外实例对象也代理了data对象上所有的属性，因此可以直接操作实例对象来操作数据属性

## methods
定义Vue实例的方法

methods的值是一个对象，对象里的属性名是方法名，值是实例的方法,其中方法中的this自动绑定到Vue实例



# 模板
## 表达式

模板中的表达式只支持单个表达式,复杂的表达式可以封装为方法

## 文本
使用双大括号{{ expression }}

## HTML
上面的语法并不能展示html,html需要使用v-html指令
```
<div v-html="rawHtml"></div>
```

## 绑定属性
使用v-bind指令
```
<tag v-bind:href="href">
```

## 绑定事件
使用v-on

```
<a v-on:click="..">

```

## 条件
```
<div v-if="condition">
```
同一系列的还有v-else-if,v-else

## 条件成立时显示
```
v-show="condition"
```
## 遍历对象
使用v-for指令,内容中使用特定语法 alias in expression，为当前遍历的元素提供别名

遍历时还可以指定索引

```
<div v-for="(item, index) in items"></div>
```

一般对数组进行遍历，还可以变量对象
```
<div v-for="(val, key) in object"></div>
<div v-for="(val, key, index) in object"></div>
```