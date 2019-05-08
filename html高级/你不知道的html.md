你不知道的HTML
======
文件夹小写
https://blog.csdn.net/ljc_563812704/article/details/53464039

## 一．开发工具 

    推荐 Sublime Text （最主要的优点：轻量、性能高）   
    插件推荐：   Emmet
    概括地说，Emmet（译者注：前身就是以前大名鼎鼎的Zen Coding，这个如果你没听说和使用过，就悲哀了）,
    一个可以让你更快更高效地编写HTML和CSS，节省你大量时间的插件。怎么使用？
    你只需按约定的缩写形式书写而不用写整个代码，然后按“扩展”键，这些缩写就会自动扩展为对应的代码内容。
    主题插件，界面看起来清爽优化。   Material Theme   Comic Sans MS
    这个是英文字体，一个看起来舒服的英文字体，能够让开发在写代码时，心情更加愉悦。
    
    备注：统一编辑器的好处
      1)作为团队开发，统一的编辑器可以尽量减少团队的沟通的成本。
      2)好的编辑器能够提高团队的开发效率，无论从写代码的角度，还是审美的角度。
      
https://material-ui.com/ 谷歌UI交互设计风格material  

https://github.com/equinusocio/material-theme  material github地址

https://chinagdg.org/2016/02/ttt2-seti-ui/  subime推荐主题

https://www.jianshu.com/p/13fedee165f1 插件主題配置介绍

https://www.jianshu.com/p/13fedee165f1 Sublime插件：主题篇
      
## 二. 前端跨域请求解决方案

1. 什么是同源
    * 协议
    * 端口
    * 域名
2. 浏览器不同的域名不能访问对应的cookie但是内部的表单没有限制
3. 同源策略限制的对象（跨域）
    * Cookie 、 LocalStorage 、 IndexDB无法读取
    * Dom 无法获得
    * Ajax 请求不能发送  
4. 如何设置同源策略（domain)
5. 怎么突破同源策略

### 1.同源(origin)策略

    同源策略是浏览器的一个安全功能，不同源的客户端脚本在没有明确授权的情况下，不能读写对方资源。
    所以a.com下的js脚本采用ajax读取b.com里面的文件数据是会报错的。
    不受同源策略限制的：
    1. 页面中的链接，重定向以及表单提交是不会受到同源策略限制的。
    2. 跨域资源的引入是可以的。但是js不能读写加载的内容。 --
       如嵌入到页面中的`<script src="..."></script>，<img>，<link>，<iframe>`等。

### 2.跨域

1、什么是跨域

受前面所讲的浏览器同源策略的影响，不是同源的脚本不能操作其他源下面的对象。想要操作另一个源下的对象是就需要跨域。

2、跨域的实现形式

``` html
  <img src="" alt="">
  <iframe src="" frameborder="0"></iframe>
  <script src="jsonp"></script>
  <link rel="stylesheet" href="">
  <style>background</style>
  <style>border-image</style>
```

#### 自己的理解

` 同源策略 `：   

    1.同源策略是1995年 Netscape 公司引入浏览器的，目前浏览器都是实行这个策略，
    2.同源策略是为了保证用户信息的安全，防止恶意的网站窃取数据的。
    3.同源指的是三个相同：协议相同、域名相同、端口号相同
    
    但是也是因为浏览器同源策略的原因，前端页面不能跨域请求所需资源
    但是在日常的WEB开发中，需要进行跨域请求:
    
http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html 阮一峰

##### JSONP实现跨域

    JSONP是服务器与客户端跨源通信的常用方法。
    最大特点就是简单适用，老式浏览器全部支持，服务器改造非常小。   
    JSONP的原理是利用script标签的src属性可以进行不受同源策略的限制，进行跨域请求数据的属性->
    在 HTML页面中添加一个script标签，向服务器发送请求,服务器收到请求后->
    返回数据，将数据放在指定的回调函数中，回调函数中可以对数据进行操作。

##### image实现跨域

    //测试一下手机网速webapp页面 根据这个网速 可以给用户出一些网速比较慢的解决方案
    //直接跳过简版 图片压缩 视屏 s.gid = 1kb
``` javascript
      var s = new Image();
      var start = Date.now();
      s.src = 'http://www.baidu.com/s,gif';
      s.onload = function(argument){
         var end = Date.now();
         t = end-start;
         v = 
      }
```

##### css实现跨域

    1.图片canvas压缩代码
    2.css background执行javascript代码
    
    跨域资源共享 CORS 详解

http://www.ruanyifeng.com/blog/2016/04/cors.html


##### 为什么jsonp只支持get  --src

    JSONP的原理
    JSONP 是一种【请求一段 JS 脚本，把执行这段脚本的结果当做数据】的玩法。所以，你能 POST 一段通过 script 标签引入的脚本吗？
    （如果看过 JSONP 库的源码就知道，常见的实现代码其实就是 document.createElement(‘script’) 生成一个 script 标签，->
    然后插 body 里而已。在这里根本没有设置请求格式的余地）。
    所以JSONP的实现原理就是创建一个script标签, 再把需要请求的api地址放到src里. 这个请求只能用GET方法, 不可能是POST
    
    1.拼接一个script标签，，从而触发对指定地址的GET请求 
    2.那服务器端对这个GET请求进行处理，并返回字符串 "myCallback('response value')"
    3.那前端script加载完之后，其实就是在script中执行myCallback('response value') 
    4.是不是就完成了跨域的请求， 
    5.是不是就是只能用GET
    所以jsonp不会对服务器端代码或者内容做更改，因为它只能发送get请求

## 三. HTML语义化

### 1、什么是HTML语义化？

    基本上都是围绕着几个主要的标签，像标题（H1~H6）、列表（li）、强调（strong em、段落（p）等等
    根据内容的结构化（内容语义化），选择合适的标签（代码语义化）。
        便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析。
    
### 2、为什么要语义化？

    1. 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构:为了裸奔时好看；
    2. 用户体验：例如title、alt用于解释名词或解释图片信息、label标签的活用；
    3. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
    4. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
    5. 便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。
    
### 3、写HTML代码时应注意什么？

    1. 尽可能少的使用无语义的标签div和span；
    2. 在语义不明显时，既可以使用div或者p时，尽量用p, 因为p在默认情况下有上下间距，对兼容特殊终端有利；
    3. 不要使用纯样式标签，如：b、font、u等，改用css设置。
    4. 需要强调的文本，可以包含在strong或者em标签中
      （浏览器预设样式，能用CSS指定就不用他们），strong默认样式是加粗（不要用b），em是斜体（不用i）；
    5. 使用表格时，标题要用caption，表头用thead，主体部分用tbody包围，尾部用tfoot包围。
      （表头和一般单元格要区分开，表头用th，单元格用td）
    6. 表单域要用fieldset标签包起来，并用legend标签说明表单的用途；
    7. 每个input标签对应的说明文本都需要使用label标签，并且通过为input设置id属性。
       在lable标签中设置for=someld来让说明文本和相对应的input关联起来。
      （lable标签：用于绑定一个表单元素，当点击lable标签的时候，被绑定的表单元素就会获得输入焦点。）

### 4、HTML5新增了哪些语义标签

    H5新增常用标签
    <body>

      <header>...</header>

      <nav>...</nav>

      <article>

        <section> 

          ...

        </section>
        
          <aside>...</aside>
           
      </article>
      
      <address> 标签，定义文档或文章的作者/拥有者的联系信息。 </address>
      
      <hgroup>标签是对网页或区段section的标题元素（h1-h6）进行组合。例如，在一区段中你有连续的h系列的标签元素</hgroup>
  
      <footer>...</footer>

    </body>


