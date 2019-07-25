[推荐教程](http://docs.jinkan.org/docs/flask/quickstart.html )

[基础知识](https://blog.csdn.net/qq_36143023/article/details/79097402，https://blog.csdn.net/langkew/article/details/51839536 )

[修饰器](https://mp.weixin.qq.com/s/vB03tMtgRcmZw2nhTZqpkw )

1.WSGI简介 

Python标准库支持网络通信，库中的一些模块能够实现基础的网络通信服务，如创建网络服务器、实现TCP/UDP层的通信、HTTP应用层的通信等。就比如SimpleHttpServer这个模块定义了简单的GET、HEAD、POST请求方法等HTTP通信服务。 
Python标准库中关于网络通信的基本过程：创建一个服务器、创建请求处理程序，以WEB编程为例： 
一个WEB应用包括了： 
（1）浏览器发送一个HTTP请求 
（2）服务器收到请求生成一个HTML文档 
（3）服务器把HTML文档作为HTTP响应的body发送给浏览器 
（4）浏览器收到HTTP响应，从HTTP Body取出HTML文档并显示 
面向http的python程序需要关心（具体了参考http请求、响应报文格式）： 
（1）请求 
请求的方法method 
请求的地址url 
请求的内容 
请求的头部header 
请求的环境信息 
（2）响应 
状态码 
响应的数据 
响应的头部 
将数据在http server和python程序之间简单友好地传递是复杂的。正确的做法是底层代码由专门的服务器软件实现，而用Python专注于生成HTML文档。因为我们不希望接触到TCP连接、HTTP原始请求和响应格式，所以需要一个统一的中间件，提供给http server和python程序遵守的一定的规范，实现在网络的数据流和python的结构体之间的转换，让我们专心用Python编写Web业务，这就是WSGI的作用。 
WSGI的全称是Web Server Gateway Interface。WSGI是一种规范，不是服务器、python模块、框架。定义了web server和web application两者进行通信的接口规范。 服务器端和应用端都必须遵循这套规范。当一个应用程序是按照WSGI规范开发的，那么它可以在任意遵循该规范的服务器上运行。 
在WSGI的规范里，一个web服务流程得到了简化。wsgi把web组件分成三个部分：wsgi server (服务器端)，wsgi middleware (中间件)，wsgi application (应用端)。一个遵循WSGI规范的服务器工作逻辑很简繁，可以理解为从客户端接收一个请求，传递给应用程序，然后将应用返回的响应发送回客户端，这其中所有复杂的细节工作都交由接口另一侧的中间件或应用程序去完成。 
Python 2.5及之后的版本都内置了一个WSGI服务器，这对于我们学习来说是非常方便的。 
2.应用程序端Application ：WSGI规定每个python程序（Application）必须是一个可调用的对象，要接受两个参数environ（WSGI环境信息）和start_response(开始响应请求的函数)。其中，environ是包含了环境信息的字典、Application内部在返回前调用start_response、start_response也必须接收两个必须的参数，即status（HTTP状态）和response_headers（响应消息的头）。
