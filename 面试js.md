## 前端js面试题合集
### 1、ES6语法知道哪些？分别怎么用
1. 新增声明命令 let 和 const， let表示变量 const表示常量
2. 模板字符串用一对反引号(``)标识，它可以当做普通字符串使用，也可以用来定义多行字符串。也可以在字符串中嵌入变量，JS表达式，或函数。需要写在${}中
```
var str = `abc
def
gh`;
console.log(str);
let name = '明'；
function a(){
  return 'ming'
}
console.log(`我的名字叫做${name},年龄${17+5}岁，我的性别是${'男'},游戏ID：${a()})
```
3. 函数的默认参数ES6为参数提供了默认值，在定义函数的时候，便初始化了这个参数，以便在参数没有被传递进去的时候使用。
```
function A(a,b=1){
  console.log(a+b)  
  console.log(a);
  console.log(b);
}
A(1);   // 2, 1,1
A(2,3);   //5,2,3
````
4. Object.keys()方法，获取对象的所有属性名和方法名。不包括原型的内容，返回一个数组
```
var person = {name:"john",age:20,study(){alert('study')}};
console.log(Object.keys(person))    //  ["name", "age", "study"]

console.log(Object.keys(['aa','bb','cc']);      //["0", "1", "2"]
console.log(Object.keys('abcdef'));      //["0", "1", "2", "3", "4", "5"]
```
5. Object.assign()方法 这个方法将多个原对象的属性和方法，合并到了目标对象上面。
可以接收多个参数，第一个参数是目标对象，后边都是源对象
```
var target ={}
var obj1 = {
  name:'petter',
  age:20,
  sex:'女'
}
var obj2 = {
  sex:'男',
  score:100
}

Object.assign(target,obj1,obj2);
console.log(target);  
//{age: 20,name: "petter", score: 100, sex: "男"}
```
6.  for...of循环是遍历所有数据结构的统一方法。for...of循环可以使用的范围包括数组，Set，Map结构，某写类数组对象（arguments, DOM NodeList对象）以及字符串。
```
var arr = ["水星","金星","地球","火星"];
for(var s of arr){
  console.log(s);   //"水星"   "金星"   "地球"   "火星"
}
```
7. Promise对象 Promise是异步编程的一种解决方案，将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数<br/>它有三种状态，分别是 pending-进行中，resolved-已完成，rejected-已失败<br/>Promise构造函数接收一个参数，这个参数是函数，并且这个函数传入两个参数，分别是 resolve 和 reject，分别是异步操作执行成功后的回调函数，和异步操作执行失败后的回调函数。（按照标准来讲，resolve是将Promise的状态置为fullfiled，reject是将Promise的状态置为rejected。）
所以我们用Promise的时候一般是包在一个函数中，在需要的时候去运行这个函数，如：
```
function runAsync(){
  var p = new Promise((resolve,reject)=>{
      setTimeout(function(){
        console.log('执行完成');
        resolve('随便什么数据')
}，2000)
})  
return p;  
}

runAsync();
```
8. Promise.all()提供了并行执行异步操作的能力。并且在所有异步操作执行完成以后，才执行回调
```
Promise
.all([runAsync1(), runAsync2(), runAsync3()])
.then(function(results){
    console.log(results);
});
```
9. Promise.all方法，实际上是谁跑的慢，以谁为准执行回调。那么相对的就有另外一个方法，以谁跑的块，以谁为准执行回调。<br/>就是race方法，这个词本来就是赛跑的意思。race的用法与all一样。我们修改下上边的计时器的时间：
```
function runAsync1(){
    var p = new Promise(function(resolve, reject){
        //做一些异步操作
        setTimeout(function(){
            console.log('异步执行1完成');
            resolve('随便什么数据1');
        }, 1000);
    });
    return p;            
}
function runAsync2(){
    var p = new Promise(function(resolve, reject){
        //做一些异步操作
        setTimeout(function(){
            console.log('异步执行2完成');
            resolve('随便什么数据2');
        }, 3000);
    });
    return p;            
}
function runAsync3(){
    var p = new Promise(function(resolve, reject){
        //做一些异步操作
        setTimeout(function(){
            console.log('异步执行3完成');
            resolve('随便什么数据3');
        }, 2000);
    });
    return p;            
}
Promise
.race(runAsync1(),runAsync2(),runAsync3())
.then(function(results){
  console.log(results);
})

//1秒后打印
"异步执行1完成"
//再过1秒后打印
"异步执行3完成"
//再过2秒后打印
"异步执行2完成"
```
这个race有什么用呢？使用场景还是很多的，比如我们可以用race给某个异步请求设置超时时间，并且在超时后执行相应的操作，代码如下：
```
//请求某个图片资源
function requestImg(){
    var p = new Promise(function(resolve, reject){
        var img = new Image();
        img.onload = function(){
            resolve(img);
        }
        img.src = 'xxxxxx';
    });
    return p;
}
 
//延时函数，用于给请求计时
function timeout(){
    var p = new Promise(function(resolve, reject){
        setTimeout(function(){
            reject('图片请求超时');
        }, 5000);
    });
    return p;
}
 
Promise
.race([requestImg(), timeout()])
.then(function(results){
    console.log(results);
})
.catch(function(reason){
    console.log(reason);
});
```
requestImg函数会异步请求一张图片，我把地址写为"xxxxxx"，所以肯定是无法成功请求到的。timeout函数是一个延时5秒的异步操作。我们把这两个返回Promise对象的函数放进race，于是他俩就会赛跑，如果5秒之内图片请求成功了，那么遍进入then方法，执行正常的流程。如果5秒钟图片还未成功返回，那么timeout就跑赢了，则进入catch，报出“图片请求超时”的信息。
### 2、函数节流和函数防抖
前提条件：一个函数在短时间内被多次执行。
但是这种短时间内多次重复执行，通常情况下是没有必要的。我们需要优化这种高频执行的JS。
>优化的方法就是 函数节流 和 函数防抖<br/>
>函数节流：<br/>
>让函数在特定的时间之内只执行一次。特定时间内如果多次触发函数，只有一次生效。<br/>
>应用场景 ：下拉加载。<br/>

>函数防抖：<br/>
>频繁触发某一事件，其中两次触发间隔时间大于等于特定时间，才执行代码一次。如果在特定时间内，又触发了一次事件，那么重新开始计算函数执行时间。简单的说，一个动作连续触发，只执行最后一次。<br/>
>应用场景：搜索框搜索输入，比如用户输入字母间隔超过2秒再发送请求。<br/>
```
函数节流的例子
<button id="btn">大招<button>

<script>
  var cd = false;  //cd用来记录大招是否冷却，默认是没有冷却

  function attack(){
        console.log('发起攻击')
  }
  var button = document.queryselector('#btn');
   button.onclick = function(){
      if(cd){
           //点击大招按钮的时候判断一下，如果大招冷却，给出提示。
           console.log('大招冷却，无法攻击！')
      }else{
            //如果大招没有冷却，发起攻击
            attack();
            cd = true;     //发起攻击后，技能状态调整为冷却
            var timer = setTimeout(function(){
                cd = false;  //3秒钟后，技能冷却结束
            },3000)
      }
  }
</script>
```
```
//函数防抖例子
//公交关门
function close(){
  console.log('关门');
}

var button = document.querySelector('#btn');

var timer = null ;  //定时器一开始是空的
button.onclick = function(){
  //如果点击了按钮，发现上一个计时器还存在，那么就把它清除掉。
  if(timer){
    window.clearTimeout(timer);
  }
  //如果5秒种之内没有再点，就设置一个定时器，并执行关门函数，并且把定时器清除掉。
    timer = setTimeout(function(){
    close();
    timer= null;
  },5000)                   
}
```
### 3这段代码里的this是什么？
```
fn()   // this指向 window/global
obj.fn()  //  this 指向 obj
fn.call(xx)  //this 指向 xx
fn.bind(xx)  //this指向 xx
new Fn()   //this指向 新的对象
fn  = ()=>{}   //this 指向外边的this



判断的通用方法
function fn(a,b){
    console.log(this)
}

fn(1,2);//这句等价于下边
fn.call(undefined,1,2);
fn.apply(undefined,[1,2]);
注意：
在严格模式下 'use strict'  ,此时 fn里的this,就是call和apply的第一个参数，也就是 undefined
在非严格模式下，也就是不用 'use strict' ，call和apply里的第一个参数如果是undefined或者是null,那么this会默认替换为 window


在看一个例子：
var  obj = {
    fn:function(a,b){
        console.log(this)
    },
    child:{
        fn2:function(){
            console.log(this)
        }
    }
}
obj.fn(1,2); 等价于  
obj.fn.call(obj,1,2);
obj.fn.apply(obj,[1,2]);  //所以this是obj

obj.child.fn2();等价于
obj.child.fn2.call(obj.child);
obj.child.fn2.apply(obj.child);   //所以this是 obj.child
```
### 4、闭包和立即执行函数是什么？
* 闭包：<br/>就是能读取其他函数内部变量的函数，在JS中，只有函数内部的子函数，能够读取函数内部的局部变量。所以闭包可以理解为，定义在一个函数内部的函数。
* 闭包的缺点：<br/>让变量始终保持在内容中，内存消耗会很大。
* 什么是词法作用域？<br/>词法作用域就是函数创建的时候所在的作用域。<br/>所以，函数在执行的时候，使用的变量，会先从自己内部去找，如果自己内部没有定义，就到自己的词法作用域(scopes)去找。
```
function car(){
  var speed = 0;
  function fn(){
      speed++;
      console.log(speed);
  }
  return fn;
}

var speedUp = car();
speedUp();  //1
speedUp();  //2

// 如果在car函数里，再声明一个函数fn,并返回fn，fn()内部又使用了car声明的变量，然后调用car函数并赋值给 一个全局变量speedUp
// 因为speedUp 属于全局作用域，而全局作用域在页面没有关闭的时候，是不会销毁的。所以也就导致了fn函数不会被销毁
// 执行speedUp就相当于 执行fn()，而fn()函数内部有用到局部变量speed,按照作用域链来寻找，fn()函数内没有声明
// 继续往上一级找，fn()函数是声明在car()内的，而speed是在car内声明的
// 所以第一次执行 speedUp() 的时候，结果是1；执行之后，speed是没有被销毁的
// 再次执行就是2



//再看个例子
var fnArr = [];
for(var i=0;i<10;i++){
  fnArr[i] = function(){
      return i;
  }
}

console.log(fnArr[1]);   //  这个时候数组里存的都是函数 function(){ return i}
console.log(fnArr[2]())   //10
console.log(fnArr[5]())   //10
console.log(fnArr[7]())   //10

//为什么会输出10呢？  分析一下
fnArr[2]本身是一个函数，加括号，表示执行它指向的那个函数。
函数内部 return i，用到了i这个变量，所以会从自己内部去找这个变量，发现没有声明i，然后在去函数声明的作用域去找，函数是在for里声明的，但是for本身并不是函数，所以function函数声明的作用域是全局作用域。而全局作用域里，for循环完以后，i已经变为10了，所以fnArr[i]()会输出10.

那么如果我们想输出 0，1，2，3，4，5，....怎么办呢？
用立即执行函数
var fnArr = [];
for(var i=0;i<10;i++){
  fnArr[i] =( function(j){
      return j;
  })(i)
}

console.log(fnArr[0])   //0
console.log(fnArr[5])   //5
console.log(fnArr[7])   //7



再看个例子
for(var i=0;i<5;i++){
  setTimeout(function(){
    console.log(i)
  },2000)
}
//这里2秒后会输出5个5


for(var i=0;i<5;i++){
  (function(j){
    setTimeout(function(){
    console.log(j)
  },2000)
  })(i)
}
//这里2秒后会输出 0，1，2，3，4
```
### 5、作用链
```
var x = 10
function foo(){
  console.log(x);
}
foo();   //10  

function bar(){
  var x = 20;
  foo();
}
bar();  //10
执行bar就是执行foo,foo输出x,先从自己内部去找
发现没有声明x,然后到foo声明的作用域去找
foo是声明在全局作用域的，而全做作用域下，有声明变量x，所以输出10


//下边之所以输出30 是因为foo是在bar内部声明的。
 var x = 10;
 bar();  //30

 function bar(){
 var x = 30;
  function foo(){
        console.log(x); 
   }
    foo();
}
```
### 6、什么是JSONP,什么是CORS,什么是跨域？
1. 同源策略：提到跨域，就不得不说一下同源策略，同源策略是NetScape提出的浏览器的一种安全策略，也就是指a网站，不能随便读取b网站的内容。
2. 所谓同源：指的是，协议、域名、端口、相同
3. 最常见的应用是，当我们调用ajax接口时，如果不设置跨域，浏览器会报错。这证明使用XMLHttpRequest对象不能发送跨域请求。
4. 解决跨域最常见的方式是 jsonp。
>先弄清楚 json和jsonp的区别<br/>
>json （JavaScript Object Notation）是一种轻量级的数据交换格式，用来在浏览器和服务器之间交换数据。<br/>
>jsonp (JSON With Padding) 就是打包在函数中调动的json,或者包裹的json<br/>
>json 是一种数据格式；jsonp是一种数据调用方式
5. jsonp是jquery给我们封装的一个方法，使用方法如下：
```
$.ajax({
  ulr:'xxx',
  type:'GET',
  dataType:'jsonp',
  success:function(data){
    console.log(data)
  }
})
```
6. 利用`<script src="">`来完成一个跨域请求。
```
 <div class="container">
        <ul class="news"></ul>
        <button class="show">show news</button>
 </div>

 $('.show').addEventListener('click', function () {
            var script = document.createElement('script');
            script.src = 'http://127.0.0.1:8080/getNews?callback=appendHtml';
            document.head.appendChild(script);
            // document.head.removeChild(script);  //为了保持代码的整洁，直接删除了新增的标签，但是标签的作用已经起到了
        })

        function appendHtml(news) {
            var html = '';
            for (var i = 0; i < news.length; i++) {
                html += '<li>' + news[i] + '</li>';
            }
            console.log(html);
            $('.news').innerHTML = html;
        }
```
jsonp跨域的原理：

使用script标签发送请求，这个标签支持跨域访问<br/>
在script标签里，给服务器传递一个callback<br/>
callback的值对应到页面上定义的一个全局函数(为什么是全局函数呢？因为服务器接收到callback函数后，会返回页面中的script去寻找，如果不写到全局作用域中，根本找不到)。<br/>
服务器端返回的是一个函数的调用，调用的时候会把返回数据作为参数包裹在这个函数里。
* 缺点： jsonp只能解决get方式的跨域。如果传输的数据比较大，这种方式就不行了。
7. cors跨域<br/>cors (cross origin resource sharing) 全称 '跨域资源共享'<br/>
相对于jsonp， cors支持所有类型的HTTP请求，并且实施起来非常简单。
>cors原理：
>当使用XMLHttpRequest发送请求的时候，浏览器发现该请求不符合同源策略，会给该请求加一个请求头 origin,后台会进行一系列的处理，如果确定接受请求，则在返回结果中，加入一个响应头 Access-Control-allow-origin；浏览器判断该响应头中是否包含 origin的值，如果有，则浏览器会处理响应，我们就拿到数据。如果没有，则浏览器会直接驳回，我们就拿不到数据。
8. JSONP和CORS的区别？
> 1. JSONP只支持GET请求，而CORS支持所有类型的HTTP请求。
> 2. 使用CORS，开发者可以使用普通的XMLHttpRequest对象发起请求和获得数据。比起JSONP有更好的错误处理。
> 3. JSONP主要被老的浏览器支持，它们往往不支持CORS，而绝大多数的现代浏览器都已经支持了CORS
### 7、async/await 怎么用？ 怎么捕获异常？
async是异步的缩写。而await 可以认为是 async wait的缩写。 

async作为一个关键字放在函数前面，用来声明这个函数是一个异步函数。既然是异步函数就意味着该函数的执行不会阻塞后边的代码；  
async函数返回的是一个Promise对象。  

await用于等待一个异步方法执行完成，await等待的是一个表达式，而表达式的计算结果是一个Promise对象或者其他值。
(await相当于运算符，用于组成表达式，await表达式的运算结果取决于它等到的东西)  
如果等到的不是一个Promise对象，那么await表达式的运算结果就是它等到的东西。  
如果它等到的是一个Promise对象，await就忙起来了，它会阻塞后面的代码，等待Promise对象resolve,然后得到resolve的值。作为await表达式的运算结果。  
await只能用到async函数中。  
```
 function sayHi(name){
  return new Promise((resolve,reject)=>{
    setTimeout(()=>{
      resolve('Hi'+name);
    },2000)
  })
}

async function test(){
  var result = await sayHi('小明');
  console.log(result);
}

test();
```
### 8、如何实现深拷贝
1. JSON.parse(JSON.stringify(objectToClone)) #这种方法能解决绝大部分业务
```
var arr=[{a:1,b:2},{c:1,d:2}];
var arr2=JSON.parse(JSON.stringify(arr));
    
arr2[1].d=7;
console.log(arr,arr2)
```
2. 通过递归自定义函数实现深拷贝
```
var deepCopy = function(obj){
  var cloneObj = Array.isArray(obj)? []:{};
  if(obj && typeof obj === 'object' ){
    for(var key in obj){
      if(obj.hasOwnProperty(key)){
        cloneObj[key] = typeof obj[key] === 'object'?deepCopy(obj[key]):obj[key]
      }
    }
  }
  return cloneObj;
}
```
### 9、