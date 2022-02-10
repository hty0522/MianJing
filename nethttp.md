![image-20211114161206950](D:\typora\file\nethttp.assets\image-20211114161206950.png)

- 客户端发送请求；
- 服务器中的多路复用器收到请求；
- 多路复用器根据请求的 URL 找到注册的处理器，将请求交由处理器处理；
- 处理器执行程序逻辑，必要时与数据库进行交互，得到处理结果；
- 处理器调用模板引擎将指定的模板和上一步得到的结果渲染成客户端可识别的数据格式（通常是 HTML）；
- 最后将数据通过响应返回给客户端；
- 客户端拿到数据，执行对应的操作，如渲染出来呈现给用户。



http.HandleFunc：

​			该方法接收两个参数，一个是路由匹配的字符串，另外一个是 `func(ResponseWriter, *Request)` 类型的函数

为指定URL注册一个处理器，将处理器注册到DefaultServeMux中

Handle:

http.Handle:

`		http.Handle(pattern string, handler Handler)` 接收两个参数，一个是路由匹配的字符串，另外一个是 `Handler` 类型的值：