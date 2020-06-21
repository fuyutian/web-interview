[toc]
## vue核心知识点
### 1、对于Vue是一套渐进式框架的理解
> 渐进式代表的含义：没有多做职责之外的事情，vue.js只提供了vue-cli生态中最核心的组件系统和双向数据绑定。
1. 可以在原有的系统上，把一两个组件改用他，就像jquery
2. 可以整个用它全家桶开发
3. 可以使用它的视图，搭配自己设计的整个下层
4. 底层数据逻辑可以使用其他理念，也可以函数式
### 2、vue.js的两个核心是什么？
> 组件系统和双向数据绑定
### 3、请问 v-if 和 v-show 有什么区别
> v-if如果为false时，页面是不会渲染的，v-show如果为false时，页面仍会渲染，但是会隐藏掉和display：none的作用相同
### 4、vue常用的修饰符
> * .stop 阻止点击事件冒泡
> * .prevent 防止执行预设的行为
> * .capture 与事件冒泡的方向相反，事件捕获由外到内,捕获事件：嵌套两三层父子关系，然后所有都有点击事件，点击子节点，就会触发从外至内 父节点-》子节点的点击事件
> * .self 只会触发自己范围内的事件，不包含子元素
> * .once 只执行一次，如果我们在@click事件上添加.once修饰符，只要点击按钮只会执行一次。
### 5、v-on可以监听多个方法吗？
> 可以的
### 6、vue中 key 值的作用
> key的作用是为了高效的更新虚拟DOM，在使用相同的标签名切换时，为了让vue区分它们，否则只会替换内部属性而不会触发过度效果
### 7、vue-cli工程升级vue版本
> npm install -g @vue/cli
### 8、vue事件中如何使用event对象？
1. 使用不带圆括号的形式，event对象将被自动当做实参传入
2. 使用带圆括号的形式，我们需要使用 $event 变量显式传入 event 对象。
### 9、$nextTick的使用
> this.$nextTick()  
> Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新。$nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM，
### 10、Vue 组件中 data 为什么必须是函数
> 因为组件是可以被复用的，一个组件可以在多个地方使用。不管被使用多少次，组件中的数据都是项目隔离的，互不影响。组件被复用一次，data被复制一次。如果使用对象，data是被引用的，一个地方修改，其他地方全部修改。使用函数可以返回一份data的独立拷贝。
### 11、v-for 与 v-if 的优先级
> v-for的优先级高于v-if，如果使用了v-for后又使用了v-if。v-if会重复运行于v-for循环中，最好不要这样使用
### 12、vue中子组件调用父组件的方法
> 1. 方式一 this.$parent.父组件的方法  
> 2. 方式二 this.$emit调用父组件方法
### 13、vue中 keep-alive 组件的作用
> 缓存组件，使组件不被销毁，避免二次渲染，节省性能
### 14、vue中如何编写可复用的组件？
> * prop 允许外部环境传递数据给组件，在vue-cli工程中也可以使用vuex等传递数据。
> * 事件允许组件触发外部环境的 action
> * slot 允许外部环境将内容插入到组件的视图结构内。
### 15、什么是vue生命周期和生命周期钩子函数？
> 通俗来说 vue的生命周期就是vue实例从创建到销毁的过程   
>钩子函数   
>beforeCreate,created,beforeMount,mounted,beforeUpdate,updated,beforeDestroy,destroyed
### 16、vue生命周期钩子函数有哪些？
>beforeCreate,created,beforeMount,mounted,beforeUpdate,updated,beforeDestroy,destroyed
### 17、vue如何监听键盘事件中的按键？
> @keyup.delete	delete（删除）/BackSpace（退格）   
> .tab	Tab    
> .enter	Enter（回车）    
> ..esc	Esc（退出）         
> .space	Space（空格键）    
> .left	Left（左箭头）    
> .up	Up（上箭头）    
> .right	Right（右箭头）     
> .down	Down（下箭头）    
> .ctrl	Ctrl   
> .alt	Alt   
> .shift	Shift   
> .meta	(window系统下是window键，mac下是command键)   
### 18、vue更新数组时触发视图更新的方法
> Vue 包含一组观察数组的变异方法，所以它们也将会触发视图更新。这些方法如下   
push()
pop()
shift()
unshift()
splice()
sort()
reverse()
### 19、vue中对象更改检测的注意事项
> Vue无法检测到以下方式变动的数组   
* 当你利用索引直接设置一个项时，例如：vm.items[index] = newValue
* 当你修改数组的长度时，例如：vm.items.length = newLength
> Vue无法检测到对象属性的添加和删除。对于已经创建的实例，Vue 不能动态添加根级别的响应式属性，可以使用 Vue.set(object, key, value) 方法向嵌套对象添加响应式属性。     
Vue 不能动态添加根级别的响应式属性：
### 20、解决非工程化项目初始化页面闪动问题
> 使用v-cloak指令，v-cloak不需要表达式，它会在Vue实例结束编译时从绑定的HTML元素上移除，经常和CSS的display:none配合使用。
`<div id="app" v-cloak>`  `[v-cloak]{
    display:none;
}`
### 21、v-for产生的列表，实现active的切换
> active就是选中状态的切换
### 22、v-model语法糖的组件中的使用
> 首先在props里面接收一下value值，然后初始化到newValue里面，然后监听newValue值变化，变化后发射事件到父组件
```
watch:{
  newValue(){
    this.$emit('input', this.newValue)
  }
}
```
### 23、十个常用的自定义过滤器
```
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
function trim(value, trim) {
    switch (trim) {
        case 1:
            return value.replace(/\s+/g, "");
        case 2:
            return value.replace(/(^\s*)|(\s*$)/g, "");
        case 3:
            return value.replace(/(^\s*)/g, "");
        case 4:
            return value.replace(/(\s*$)/g, "");
        default:
            return value;
    }
}
//任意格式日期处理
//使用格式：
// {{ '2018-09-14 01:05' | formaDate(yyyy-MM-dd hh:mm:ss) }} 
// {{ '2018-09-14 01:05' | formaDate(yyyy-MM-dd) }} 
// {{ '2018-09-14 01:05' | formaDate(MM/dd) }} 等
function formaDate(value, fmt) {
    var date = new Date(value);
    var o = {
      "M+": date.getMonth() + 1, //月份
      "d+": date.getDate(), //日
      "h+": date.getHours(), //小时
      "m+": date.getMinutes(), //分
      "s+": date.getSeconds(), //秒
      "w+": date.getDay(), //星期
      "q+": Math.floor((date.getMonth() + 3) / 3), //季度
      "S": date.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt)) fmt = fmt.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o) {
      if(k === 'w+') {
        if(o[k] === 0) {
          fmt = fmt.replace('w', '周日');
        }else if(o[k] === 1) {
          fmt = fmt.replace('w', '周一');
        }else if(o[k] === 2) {
          fmt = fmt.replace('w', '周二');
        }else if(o[k] === 3) {
          fmt = fmt.replace('w', '周三');
        }else if(o[k] === 4) {
          fmt = fmt.replace('w', '周四');
        }else if(o[k] === 5) {
          fmt = fmt.replace('w', '周五');
        }else if(o[k] === 6) {
          fmt = fmt.replace('w', '周六');
        }
      }else if (new RegExp("(" + k + ")").test(fmt)) {
        fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
      }
    }
    return fmt;
  }
//字母大小写切换
/*type
 1:首字母大写
 2：首页母小写
 3：大小写转换
 4：全部大写
 5：全部小写
 * */
function changeCase(str, type) {
    function ToggleCase(str) {
        var itemText = ""
        str.split("").forEach(
            function (item) {
                if (/^([a-z]+)/.test(item)) {
                    itemText += item.toUpperCase();
                } else if (/^([A-Z]+)/.test(item)) {
                    itemText += item.toLowerCase();
                } else {
                    itemText += item;
                }
            });
        return itemText;
    }
    switch (type) {
        case 1:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
            });
        case 2:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toLowerCase() + word.substring(1).toUpperCase();
            });
        case 3:
            return ToggleCase(str);
        case 4:
            return str.toUpperCase();
        case 5:
            return str.toLowerCase();
        default:
            return str;
    }
}

//字符串循环复制,count->次数
function repeatStr(str, count) {
    var text = '';
    for (var i = 0; i < count; i++) {
        text += str;
    }
    return text;
}

//字符串替换
function replaceAll(str, AFindText, ARepText) {
    raRegExp = new RegExp(AFindText, "g");
    return str.replace(raRegExp, ARepText);
}

//字符替换*，隐藏手机号或者身份证号等
//replaceStr(字符串,字符格式, 替换方式,替换的字符（默认*）)
//ecDo.replaceStr('18819322663',[3,5,3],0)
//result：188*****663
//ecDo.replaceStr('asdasdasdaa',[3,5,3],1)
//result：***asdas***
//ecDo.replaceStr('1asd88465asdwqe3',[5],0)
//result：*****8465asdwqe3
//ecDo.replaceStr('1asd88465asdwqe3',[5],1,'+')
//result："1asd88465as+++++"

function replaceStr(str, regArr, type, ARepText) {
    var regtext = '',
        Reg = null,
        replaceText = ARepText || '*';
    //repeatStr是在上面定义过的（字符串循环复制），大家注意哦
    if (regArr.length === 3 && type === 0) {
        regtext = '(\\w{' + regArr[0] + '})\\w{' + regArr[1] + '}(\\w{' + regArr[2] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[1]);
        return str.replace(Reg, '$1' + replaceCount + '$2')
    }
    else if (regArr.length === 3 && type === 1) {
        regtext = '\\w{' + regArr[0] + '}(\\w{' + regArr[1] + '})\\w{' + regArr[2] + '}'
        Reg = new RegExp(regtext);
        var replaceCount1 = this.repeatStr(replaceText, regArr[0]);
        var replaceCount2 = this.repeatStr(replaceText, regArr[2]);
        return str.replace(Reg, replaceCount1 + '$1' + replaceCount2)
    }
    else if (regArr.length === 1 && type === 0) {
        regtext = '(^\\w{' + regArr[0] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
    else if (regArr.length === 1 && type === 1) {
        regtext = '(\\w{' + regArr[0] + '}$)'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
}

//格式化处理字符串
//ecDo.formatText('1234asda567asd890')
//result："12,34a,sda,567,asd,890"
//ecDo.formatText('1234asda567asd890',4,' ')
//result："1 234a sda5 67as d890"
//ecDo.formatText('1234asda567asd890',4,'-')
//result："1-234a-sda5-67as-d890"
function formatText(str, size, delimiter) {
    var _size = size || 3, _delimiter = delimiter || ',';
    var regText = '\\B(?=(\\w{' + _size + '})+(?!\\w))';
    var reg = new RegExp(regText, 'g');
    return str.replace(reg, _delimiter);
}

//现金额大写转换函数
//ecDo.upDigit(168752632)
//result："人民币壹亿陆仟捌佰柒拾伍万贰仟陆佰叁拾贰元整"
//ecDo.upDigit(1682)
//result："人民币壹仟陆佰捌拾贰元整"
//ecDo.upDigit(-1693)
//result："欠人民币壹仟陆佰玖拾叁元整"
function upDigit(n) {
    var fraction = ['角', '分', '厘'];
    var digit = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];
    var unit = [
        ['元', '万', '亿'],
        ['', '拾', '佰', '仟']
    ];
    var head = n < 0 ? '欠人民币' : '人民币';
    n = Math.abs(n);
    var s = '';
    for (var i = 0; i < fraction.length; i++) {
        s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, '');
    }
    s = s || '整';
    n = Math.floor(n);
    for (var i = 0; i < unit[0].length && n > 0; i++) {
        var p = '';
        for (var j = 0; j < unit[1].length && n > 0; j++) {
            p = digit[n % 10] + unit[1][j] + p;
            n = Math.floor(n / 10);
        }
        s = p.replace(/(零.)*零$/, '').replace(/^$/, '零') + unit[0][i] + s;
        //s = p + unit[0][i] + s;
    }
    return head + s.replace(/(零.)*零元/, '元').replace(/(零.)+/g, '零').replace(/^整$/, '零元整');
} 

//保留2位小数
function toDecimal2(x){
  var f = parseFloat(x);
  if (isNaN(f)) {
    return false;
  }
  var f = Math.round(x * 100) / 100;
  var s = f.toString();
  var rs = s.indexOf('.');
  if (rs < 0) {
    rs = s.length;
    s += '.';
  }
  while (s.length <= rs + 2) {
    s += '0';
  }
  return s;
}

export{
    trim,
    changeCase,
    repeatStr,
    replaceAll,
    replaceStr,
    checkPwd,
    formatText,
    upDigit,
    toDecimal2,
    formaDate
}
```
### 24、vue等单页面应用及其优缺点
> 优点：   
Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件，核心是一个响应的数据绑定系统。MVVM、数据驱动、组件化、轻量、简洁、高效、快速、模块友好。
> 缺点：   
不支持低版本的浏览器，最低只支持到IE9；不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；第一次加载首页耗时相对长一些；不可以使用浏览器的导航按钮需要自行实现前进、后退。
### 25、什么是vue的计算属性？
> 模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护
> 在一个计算属性里可以完成各种复杂的逻辑，包括运算、函数调用等，只要最终返回一个结果就可以。
### 26、vue-cli提供的几种脚手架模板
> webpack  webpack-simple
### 27、vue父组件如何向子组件中传递数据？
props $emit 
### 28、vue-cli开发环境使用全局常量
> 在vue.config.js的同级新建文件
> 编写文件，设置变量全局变量仅除NODE_ENV和BASE_URL这两个保留变量外，其余自定义变量都需使用VUE_APP开头
```
NODE_ENV = 'development'//设置环境
VUE_APP_API_MemberCard='http://api/http-service-engine/callServiceByJson/'
VUE_APP_API_Coupon='http://api/http-service-engine/callServiceByJson'
VUE_APP_API_Activite='http://api/http-service-engine/callServiceByJson'
VUE_APP_API_Label='http://api/memberManager/callServiceByJson'
VUE_APP_API_Store='http://api/http-service-engine/callServiceByJson'
```
>到上一步网上都有很多教程，使用时process.env.变量名即可,不可以有注释
### 29、vue-cli生产环境使用全局常量
> 开发环境：创建.env.development文件，同时配置.env.development和.env同时存在，系统默认访问.env.development

> 生产环境：创建.env.production文件；配置好了.env.production后使用build，系统默认访问.env.production里面的全局变量
### 30、vue弹窗后如何禁止滚动条滚动？
```
methods : {
   //禁止滚动
   stop(){
        var mo=function(e){e.preventDefault();};
        document.body.style.overflow='hidden';
        document.addEventListener("touchmove",mo,false);//禁止页面滑动
    },
    /***取消滑动限制***/
    move(){
        var mo=function(e){e.preventDefault();};
        document.body.style.overflow='';//出现滚动条
        document.removeEventListener("touchmove",mo,false);
    }
}
```
### 31、计算属性的缓存和方法调用的区别
> 1、我们可以将同一函数定义为一个方法或是一个计算属性。两种方式的最终结果确实是完全相同的。不同的是计算属性是基于它们的依赖进行缓存的。只在相关依赖发生改变时它们才会重新求值。相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。

> 2、使用计算属性还是methods取决于是否需要缓存，当遍历大数组和做大量计算时，应当使用计算属性，除非你不希望得到缓存。

> 我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 A，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 A 。如果没有缓存，我们将不可避免的多次执行 A 的 getter！如果你不希望有缓存，请用方法来替代。

> 3、计算属性是根据依赖自动执行的，methods需要事件调用。
### 32、vue-cli中自定义指令的使用
```
1.创建局部指令
var app = new Vue({
    el: '#app',
    data: {    
    },
    // 创建指令(可以多个)
    directives: {
        // 指令名称
        dir1: {
            inserted(el) {
                // 指令中第一个参数是当前使用指令的DOM
                console.log(el);
                console.log(arguments);
                // 对DOM进行操作
                el.style.width = '200px';
                el.style.height = '200px';
                el.style.background = '#000';
            }
        }
    }
})
```
```
2.全局指令
Vue.directive('dir2', {
    inserted(el) {
        console.log(el);
    }
})
```
```
<div id="app">
    <div v-dir1></div>
    <div v-dir2></div>
</div>
```