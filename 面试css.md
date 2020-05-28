## 前端面试css合集
### 1、两种盒模型
* 标准盒模型<br/>标准盒模型下 盒子的总宽度/高度=width/height+padding+border+margin,标准盒模型下 width是指content的宽度
* 怪异盒模型<br/>怪异盒模型下 盒子的总宽度/高度=width/height+margin,怪异盒模型下 width 指的是内容content+padding+border的宽度------IE6，7，8 不设置 <!DOCTYPE html> 情况下，是怪异盒模型，如果加了就是标准盒模型
### 2、BFC是什么？
* (Block Formatting Context)块级格式化上下文。BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也如此.并且在一个BFC中，块盒与行盒（行盒由一行中所有的内联元素所组成）都会垂直的沿着其父元素的边框排列。
### 3、选择器的优先级？
> !important 优先级最高  权值无穷大<br/>
> style 写在元素行的内联样式其次   权值1000<br/>
> id   权值100 <br/>
> class/伪类/属性     权值10 <br/>
> 标签选择器       权值1<br/>
> 通配符        权值0 <br/>

> 更准确的说法 <br/>
>1.越具体，优先级越高 <br/>
>2.写在后面的，会覆盖写在前面的 <br/>
>3.important优先级最高，但是要少用 <br/>