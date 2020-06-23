## vue-router
### 1、vue-router如何响应 路由参数 的变化？
```
const User = {
  template: '...',
  watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
    }
  }
}
或者
const User = {
  template: '...',
  beforeRouteUpdate (to, from, next) {
    // react to route changes...
    // don't forget to call next()
  }
}
```
### 2、完整的 vue-router 导航解析流程
```
1.导航被触发；

2.在失活的组件里调用beforeRouteLeave守卫；

3.调用全局beforeEach守卫；

4.在复用组件里调用beforeRouteUpdate守卫；

5.调用路由配置里的beforeEnter守卫；

6.解析异步路由组件；

7.在被激活的组件里调用beforeRouteEnter守卫；

8.调用全局beforeResolve守卫；

9.导航被确认；

10..调用全局的afterEach钩子；

11.DOM更新；

12.用创建好的实例调用beforeRouteEnter守卫中传给next的回调函数。

```

### 3、vue-router有哪几种导航钩子（ 导航守卫 ）？
```
// 路由配置守卫即配置在路由对象中

// 组件实力的导航守卫：beforeRouteLeave、beforeRouteEnter、beforeRouteUpdate

// 全局守卫：beforeEach、beforeResolve、afterEach

// 路由配置守卫：beforeEnter
```

### 4、vue-router的几种实例方法以及参数传递

### 5、vue-router的动态路由匹配以及使用

### 6、vue-router如何定义嵌套路由？

### 7、<router-link></router-link>组件及其属性

### 8、vue-router实现路由懒加载（ 动态加载路由 ）

### 9、vue-router路由的两种模式

### 10、history路由模式与后台的配合