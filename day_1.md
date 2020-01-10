# web建站常用技术

2020年1月10日

### HTML与CSS
HTML：一种标记语言

CSS：定义样式

### HTML5与XHTML
HTML5：一个比较新的标准

XHTML：XML和HTML的“杂交品种”，对语法比较严格，且为了兼容XML，在语法上与HTML有一些不同

### JavaScript与浏览器脚本
CSS+HTML：得到的是静态脚本，没什么动画，按F5才会刷新数据；Javascript（JS）可以给页面添加一些动态的效果

**AJAX** ：不用刷新就能与服务器进行交互，更新页面的一小部分

### Web Server和Web Services

HTTP协议：浏览器给服务器发一个请求，服务器不是一看就知道怎么响应。这些请求和响应要有一个通用的写法，也就是要有一个协议，常用的是HTTP协议。

客户端与服务器的交互的主体、客体、载体是五花八门的：

* 服务器可以是大型机也可以是个人电脑，只要能跑相应的程序就行。
* 客户端可以是各种软件（这些软件不一定运行在个人电脑上，可以是手机、平板、智能穿戴设备等等）
* 有时候不是传生成好的HTML文件或者其他服务器上已经有的文件，而是传输经过一定逻辑处理后生成的字符串或者其他各种封装好的数据。

需要先对机器如何达成共识，指明一种协议（比如HTTP/HTTPS）和一种数据封装格式（比如HTML/XML），Web Server提供的Web Service指的就是这种协议+格式的交流体系。

Web Service传输的数据再经由本地客户端的分析渲染，就能以普通人能够理解的形式展现出来。此外还有一些Web Service并不是为普通用户设计的，eg，微博API，就是给程序员来进行二次开发的。

除了提供Web Service，Web Server还会兼顾很多功能，例如：提供缓存、平衡负载，这样在访问量比较大的时候能有条不紊地接客。常见的现成的Web Server有Apache、Nginx和微软的IIS，也可以用一些工具（比如Node.js）自己定制一个。因为Web Server需要比较好的性能，所以投产时用的Web Server通常是C/C++/Java写的。

### PHP，服务器脚本，Web Framework

服务器还要接收你发过来的各种请求，去操作本地的文件or数据库，服务器那边少不了要有代码了，这些代码就是服务器脚本。Web Service传输的数据，也是由服务器脚本生成，再交由Web Server，按照某种协议套好整个相应格式，返回给客户端的。服务器脚本就是利用已知的数据，在因人而异的地方填入相应的内容，生成给每个人看的页面。

PHP是一种常见的用来写服务器脚本的语言，只要是能拿来写大家传输数据的通用接口（CGI）的语言都可以用来写服务器脚本。

在写服务器脚本的时候，通常还会用同个语言写的 **Web Framework** 来处理各种细节，防御一些常见的攻击，提供跨站认证（比如用已有的微博账号注册其他网站）的接口，利用cookie处理登录状态和用户设置，生成网页模板之类的。如果用C#或者Visual Basic写服务器脚本，就可以用**ASP.NET**这个框架实现这些功能。不过现在不少人是反过来为了一个好用的Web Framework去选择它对应的服务器脚本语言的。

### 一个普通网站的访问过程

1. 用户操作浏览器访问，浏览器向服务器发出一个HTTP请求。
2. 服务器接收到HTTP请求，Web Server进行相应的初步处理，使用服务器脚本生成页面。
3. 服务器脚本（利用Web Framework）调用本地和客户端传来的数据，生成页面。
4. Web Server将生成的页面作为HTTP相应的body，根据不同的处理结果生成HTTP header，发回给客户端。
5. 客户端（浏览器）接受到 HTTP 响应，通常第一个请求得到的 HTTP 响应的 body 里是 HTML 代码，于是对 HTML 代码开始解析
6. 解析过程中遇到引用的服务器上的资源（额外的 CSS、JS代码，图片、音视频，附件等），再向 Web Server 发送请求，Web Server 找到对应的文件，发送回来；
7. 浏览器解析 HTML 包含的内容，用得到的 CSS 代码进行外观上的进一步渲染，JS 代码也可能会对外观进行一定的处理；
8. 用户与页面交互（点击，悬停等等）时，JS 代码对此作出一定的反应，添加特效与动画；
9. 交互的过程中可能需要向服务器索取或提交额外的数据（局部的刷新，类似微博的新消息通知），一般不是跳转就是通过 JS 代码（响应某个动作或者定时）向 Web Server 发送请求，Web Server 再用服务器脚本进行处理（生成资源or写入数据之类的），把资源返回给客户端，客户端用得到的资源来实现动态效果或其他改变。

### 服务器端语言

近几年，热起来的语言有：
* Python： Tornado（知乎、Quora）、Django（Instagram、Pinterest）
* Ruby：Rails（Github、早期的Twitter）
* JavaScript：有了Node.js这个平台，Web Server、服务器脚本和浏览器脚本全都可以用JavaScript来写，Node.js上最常用的Framework是Express
* 微软家的则跟着 ASP.NET 转移到了C# 或者 Visual Basic
* Erlang：擅长大规模的并发，不少游戏公司拿来写服务器，靠几十个工程师支撑几亿用户的WhatsApp
 
 ### 几种常见的架构
 * LAMP = Linux+Apache+MySQL+PHP(P还可能是Python或Perl，有时候L会改成W=Windows)。都是开源技术，网站起步时用起来的成本比较低，是普通网站里的常见架构，对于发展的很大的网站会遇到很多瓶颈。
 * J2EE：Java世界的架构，比较常见的会搭配一种UNIX做操作系统，Apache做Web Server，Tomcat转换到JSP到Java给服务器程序用，Oracle数据库等等。
 * ASP.NET：微软家的架构
 * MEAN架构：MongoDB做数据库，Express做 Web Framework，Angular 做前端的 JavaScript 框架，Node.js 用于编写 Web Server。神奇之处在于这几个东西的语言都是 JavaScript （MongoDB的实现不是，但与外界沟通用的语言是）。因为是比较新的架构，还有待时间的考验，不过被很多人（尤其是靠 JavaScript 吃饭的前端程序猿们）热切关注。

 

&copy; 张秋怡，https://www.zhihu.com/question/22689579/answer/22318058
