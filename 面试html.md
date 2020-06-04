[toc]
## 前端基础面试题合集

### 1、常见的浏览器内核有哪些，对浏览器内核的理解
1. Trident内核：IE，maxThon,tt,The,world,360,搜狗浏览器等[又称MSHTML]
* Gecko内核：Mozilla Firefox
* WebKit内核：Safari Chrome
* Persto: OPeraPresto
> 浏览器内核主要分成两部分：渲染引擎(layout engineer或Rendering Engine)和JS引擎。
* 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。
* js引擎：解析和执行JavaScript来实现网页的动态效果
### 2、HTTP状态消息200 320 304 403 404 500 分别表示什么？
> * 100 Continue 继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
* 200：OK 请求已成功，请求所希望的响应头或数据体将随此响应返回。
* 201：Created 请求成功并且服务器创建了新的资源
* 202：Accepted 服务器已接受请求，但尚未处理
* 301：Moved Permanently 请求的网页已永久移动到新位置。
* 302： Found 临时性重定向。请求的资源临时从不同的 URL 响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在 Cache-Control 或 Expires 中进行了指定的情况下，这个响应才是可缓存的。
* 303：See Other 临时性重定向，且总是使用 GET 请求新的 URL
* 304：Not Modified 自从上次请求后，请求的网页未修改过。如果客户端发送了一个带条件的 GET 请求且该请求已被允许，而文档的内容（自上次访问以来或者根据请求的条件）并没有改变，则服务器应当返回这个状态码。304 响应禁止包含消息体，因此始终以消息头后的第一个空行结尾。
* 400：** Bad Request** 服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
* 401：** Unauthorized** 请求未授权。
* 403：Forbidden 禁止访问。服务器已经理解请求，但是拒绝执行它。
* 404：Not Found 找不到如何与 URL 相匹配的资源。请求失败，请求所希望得到的资源未被在服务器上发现。
* 500：Internal Server Error 最常见的服务器端错误。服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。一般来说，这个问题都会在服务器端的源代码出现错误时出现。
* 503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
### 3、一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）
> 注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句， 而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、 到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；
> 简洁版(4次“握手”)：
1. 浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
2. 服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
3. 浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
4. 载入解析到的资源文件，渲染页面，完成。
> 详细版：
1. 浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
2. 调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
3. 通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
4. 进行HTTP协议会话，客户端发送报头(请求报头);
5. 进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
6. 进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
7. 处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
8. 浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
9. 文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
10. 页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。
### 4、WEB应用从服务器主动推送Data到客户端有那些方式？
> * html5提供的Websocket
* 不可见的iframe
* WebSocket通过Flash
* XHR长时间连接
* XHR Multipart Streaming
* `<script>标签的长时间连接(可跨域)`
### 5、页面重构怎么操作？
> 该题应谨慎回答自己擅长的，避免给自己挖坑。
1. 表格(table)布局改为DIV+CSS
2. 使网站前端兼容于现代浏览器(针对于不合规范的CSS、如对IE6有效的)
3. 对于移动平台的优化
4. 针对于SEO进行优化
5. 减少代码间的耦合 让代码保持弹性
6. 严格按规范编写代码
7. 设计可扩展的API 代替旧有的框架、语言(如VB)
8. 压缩JS、CSS、image等前端资源(通常是由服务器来解决)
9. 采用CDN来加速资源加载
10. HTTP服务器的文件缓存
### 6、如何解决跨域问题?
>jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面
### 7、请描述一下 cookies，sessionStorage 和 localStorage 的区别？
>cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。<br/>cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。<br/>sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
>存储大小：cookie数据大小不能超过4k。
>sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。
>有期时间：localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；<br/>sessionStorage 数据在当前浏览器窗口关闭后自动删除。<br/>cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭
### 8、页面可见性（Page Visibility API） 可以有哪些用途？
> * 通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;
* 在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；
### 9、如何理解HTML语义化的？
* 我理解的HTML语义化是正确的标签做正确的事情，能够便于开发者阅读和写出更优雅的代码的同时，让网络爬虫更好的解析。
### 10、为什么要做到语义化？
* 有利于SEO，有利于搜索引擎爬虫更好的解析我们的页面，从而获取更多的有效信息，提升网页的权重。
* 在没有CSS的时候，能够清晰看出网页的结构，增强可读性。
* 便于团队合作开发和维护，提高开发效率
### 11、<!DOCTYPE> 文档声明
* <!DOCTYPE> 文档声明，它不是HTML标签，是一个指示web浏览关于页面使用哪个HTML版本编写的指令。<!DOCTYPE> 声明必须位于文档的第一行，位于<html>标签之前。
<!DOCTYPE html>
### 12、meta标签的几种用法
* meta指定文档编码<br/>
`<meta charset="UTF-8">`<br/>
* 适配移动页面<br/>
`<meta name="viewport" content="width=device-width,initial-scale=1.0">`<br/>
`<meta name="viewport"  content="width=device-width,initial-scale=1.0">`<br/>
* 添加页面描述<br/>
`<meta name="description" content="腾讯网(www.qq.com)是中国最浏览量最大的门户网站">`<br/>

