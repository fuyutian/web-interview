## http请求
1. Promise对象是什么？
> Promise对象是ES6（ ECMAScript 2015 ）对于异步编程提供的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。Promise对象有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。   

2. axios、fetch与ajax有什么区别？
>ajax：
        + ajax本身是针对mvc编程，不符合现在前端mvvm的浪潮
        + 基于原生XHR开发，XHR本身的架构不清晰
        + 不符合关注分离的原则
        + 配置和调用方式非常混乱，而且基于事件的异步模型不友好
    axios：
        + 从浏览器中创建xmlhttprequest
        + 支持promise API
        + 客户端支持防止csrf
        + 提供了一些并发请求的接口（重要）
        + 从node.js中创建http请求
        + 拦截请求和相应
        + 转换请求和响应数据
        + 自动转换json数据
        + 体积小
        防止csrf：让每一个请求都带一个从cookie中拿的key，根据浏览器的同源策略，假冒网站是拿不到你cookie中的key的，这样，后台就可以轻松辨别出这个请求是否是用户在假冒网站上误导输入，从而采取正确的策略。
    fetch：
        是ajax的替代品，实在es6中出现的，使用了promise对象，fetch是基于promise设计的。fetch的代码结构比ajax简单多了，参数有点像jquery ajax，但是fetch不是ajax的进一步封装，而是原生js，没有使用xmlhttprequest。
        + 语法简洁
        + 基于promise实现，支持async和await
        + 同构方便
        + 更加底层
        + 脱离了XHR，是es规范里新的实现方式。
        + 用起来不是太舒服
3. 什么是JS的同源策略和跨域问题？
> 所谓同源，就是指两个页面具有相同的协议，主机（也常说域名），端口，三个要素缺一不可。   
前置条件是我们在WEB服务器或者服务端脚本中设置ACCESS-CONTROL-ALLOW-ORIGIN头部，如果设置了这些头部并允许某些域名跨域访问，则浏览器就会跳过同源策略的限制返回对应的内容。此外，如果你不是通过浏览器去获取资源，比如你通过一个python脚本去调用接口或者获取js文件，也不在这个限制之内。
4. 如何解决跨域问题？
> jsonp 代理 core
5. vue-cli中如何使用JSON数据模拟？
> 1、使用express搭建静态服务，mock数据写在json文件中，proxyTable 里将接口代理到具体mock数据json文件上。
> cli3.0 根目录下创建一个vue.config.js 
```
module.exports = {
  devServer: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        pathRewrite: {
          '^/api': '/mock'
        }
      }
    }
  }
}

axios
 .get('/api/home.json')
 .then(this.handler)
```
6. vue-cli中http请求的统一管理。

7. axios有什么特点？
> 一、Axios 是一个基于 promise 的 HTTP 库，支持promise所有的API   
> 二、它可以拦截请求和响应   
> 三、它可以转换请求数据和响应数据，并对响应回来的内容自动转换成 JSON类型的数据  
> 四、安全性更高，客户端支持防御 XSRF

## UI样式
1. vue组件的scoped属性的作用
> 样式只在本组件中生效
2. 如何让CSS只在当前组件中起作用？
> `<style scoped="scoped"></style>`
3. vue-cli中常用的UI组件库
> emelent-ui, iView UI组件库,Vux UI组件库,Mint UI组件库,Vant UI组件库
4. 如何适配移动端？【 经典 】
> 首先添加meta标签，响应式布局，通过媒体查询实现。通过动态rem实现，flex 弹性布局
5. 移动端常用媒体查询的使用

6. 垂直居中对齐
```
 display: flex;
    justify-content: center;
    align-items: center;
```
```
position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
```
7. vue-cli中如何使用背景图片？

8. 使用表单禁用时移动端样式问题

9. 多种类型文本超出隐藏问题
## 常用功能
1. vue中如何实现tab切换功能？

2. vue中如何利用 keep-alive 标签实现某个组件缓存功能？

3. vue中实现切换页面时为左滑出效果

4. vue中父子组件如何相互调用方法？

5. vue中央事件总线的使用
## 混合开发
1. vue如何调用 原生app 提供的方法？

2. 原生app 调用 vue 提供的方法，并将值传递到 .vue 组件中
## 生产环境
1. vue打包命令是什么？

2. vue打包后会生成哪些文件？

3. 如何配置 vue 打包生成文件的路径？

4. vue如何优化首屏加载速度？
## MVVM设计模式
1. MVC、MVP与MVVM模式

2. MVC、MVP与MVVM的区别

3. 常见的实现MVVM几种方式

4. Object.defineProperty()方法

5. 实现一个自己的MVVM（原理剖析）

6.  ES6中类和定义

7. JS中的文档碎片

8. 解构赋值

9. Array.from与Array.reduce

10. 递归的使用

11. Obj.keys()与Obj.defineProperty

12. 发布-订阅模式

13. 实现MVVM的思路分析
## 源码剖析
1. vue内部与运行机制：

Vue.js 全局运行机制
响应式系统的基本原理
什么是 Virtual DOM？
如何编译template 模板？
diff算法
批量异步更新策略及 nextTick 原理？
proxy代理？
2、vuex工作原理详解

Vue.mixin
Vue.use
## 深入拓展
1、vue开发命令 npm run dev 输入后的执行过程

2、vue的服务器端渲染

3、从零写一个npm安装包

4、vue-cli中常用到的加载器

5、webpack的特点