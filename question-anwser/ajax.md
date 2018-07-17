# Ajax

1.  Ajax 是什么

    Ajax（**Asynchronous JavaScript + XML**）即异步 JavaScript + XML。讲 Ajax 之前得先聊聊 HTTP。HTTP（超文本传输协议）协议规定了 Web 浏览器如何从服务器获取信息或者向服务器提交内容， 是 Web 数据通信的基础。

    Web 浏览器通常会处理大量的 HTTP 请求，一般主要对 HTTP 的控制算是有两类

    - 非脚本控制

      - 点击页面中的超链接，如`<a href="http://www.baidu.com">baidu</a>`
      - 点击提交表单 `<button type="submit">submit</submit>`， 会将页面信息提交到`<form>`标签的`action`地址，并跳转。
      - 直接在地址栏输入一个新的 URL

    - 脚本控制（通过 JavaScript 代码来操作 HTTP）

      - 通过对`window.location` 相关属改变或者方法的调用

      - 调用表单对象的`submit`方法

然而上述方法对 HTTP 请求的控制都会导致页面的重载，这就导致用户操作之后必须等到整个页面更新之后才能够做后续的操作，体验很差。但是通过**Ajax 应用可以实现操作 HTTP 和 Web 服务器之前的数据交换，而不导致页面的重载**。

Ajax 的实现也有很多中，从广义上来讲我们通过异步的方式和服务器进行数据的通讯，就算是一个 Ajax 的实现。例如：

1.  `<img src="https://www.baidu.com/img/bd_logo1.png" />` 通过`img`的`src`属性，虽然可以异步加载数据但是这种方式无法试下完整的数据交互，因为数据交互是单向的。

2.  通过`<iframe>`的`src`属性。

    1.  客户端指定一个需要请求的 URL；
    2.  设置`<iframe>`的`src`属性为此 URL;
    3.  浏览器解析`<iframe>`标签，像服务器发送一个请求；对应的服务器创建一个包含响应内容的 HTML 文档，把它返回给浏览器，并在`<iframe>`中显示。

3.  通过`<script>`设置`src`属性开发起 HTTP GET 请求。

4.  **XMLHttpRequest API**, 它定义了脚本操作 HTTP 的一些 API 从而实现异步通信，这也是我们通常说说的 Ajax 核心，所以我们一般常说的 Ajax 就是**使用 XMLHttpRequest 对象与服务器通信**。

Ajax 最主要的两个特性

- 在不重新加载页面的情况下发送请求给服务器。

- 接受并使用从服务器发来的数据。

2.  Ajax 原理

    Ajax 的原理简单来说通过 XMLHttpRequest 对象来向服务器发异步请求，从服务器获得数据，然后用 javascript 来操作 DOM 而更新页面。因此所以这里我们必须弄清楚 [XMLHttpRequest](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)。

    [**XMLHttpRequest**](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest)：XMLHttpRequest 是一个 API，它为客户端提供了在客户端和服务器之间传输数据的功能。它提供了一个通过 URL 来获取数据的简单方式，并且不会使整个页面刷新。这使得网页只更新一部分页面而不会打扰到用户。XMLHttpRequest 在 AJAX 中被大量使用。下面是一个完整的通过脚本凑操作 HTTP 的过程。

    ```javascript
    /**
     * => Ajax请求的整个过程
     * 1. 创建httpRequest对象；
     * 2. 设置响应的处理方法来处理服务器的响应；
     * 3. 调用httpRequest对象的open()方法定义要请求的URL和请求方式(GET、POST等)；
     * 4. 调用httpRequest对象的send()方法向服务器发送请求。
     */

    // 这里兼容了早起版本的 IE6，创建了一个httpRequest对象
    var httpRequest = null;
    if (window.XMLHttpRequest) {
      // 标准浏览器
      httpRequest = new XMLHttpRequest();
    } else if (window.ActiveXObject) {
      // IE6或早期浏览器
      httpRequest = new ActiveXObject('Microsoft.XMLHTTP');
    }

    if (!httpRequest) {
      alert('无法创建 XMLHTTP 实例');
      return;
    }

    // 客户端处理响应的方法
    httpRequest.onreadystatechange = function() {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
          console.log(httpRequest.responseText); // 处理请求成功数据
        } else {
          console.log('请求错误！');
        }
      }
    };
    httpRequest.open('GET', 'http://www.example.org/some.file', true);
    httpRequest.send();
    ```

    详细说明： https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX/Getting_Started

    关于 XMLHttpRequest 对象： https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest

3.  Ajax 相关面试题目

    - [ajax 常见面试题](https://juejin.im/post/5aa2b26b518825556020873f)
    - [AJAX 面试题都在这里](https://juejin.im/post/5a84357ef265da4e761fd061)
    - [经典的 20 道 AJAX 面试题](https://blog.csdn.net/chow__zh/article/details/9149811)
