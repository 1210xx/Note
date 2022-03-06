## JSP
Java Server Pages

[[Servlet]]就是一个能处理HTTP请求，发送HTTP响应的小程序，而发送响应无非就是获取`PrintWriter`，然后输出HTML：

```
PrintWriter pw = resp.getWriter();
pw.write("<html>");
pw.write("<body>");
pw.write("<h1>Welcome, " + name + "!</h1>");
pw.write("</body>");
pw.write("</html>");
pw.flush();
```

只不过，用PrintWriter输出HTML比较痛苦，因为不但要正确编写HTML，还需要插入各种变量。如果想在Servlet中输出一个类似新浪首页的HTML，写对HTML基本上不太可能。

那有没有更简单的输出HTML的办法？


那就是JSP


它的文件必须放到`/src/main/webapp`下，文件名必须以`.jsp`结尾，整个文件与HTML并无太大区别，但需要插入变量，或者动态输出的地方，使用特殊指令`<% ... %>`。

JSP和Servlet有什么区别？其实它们没有任何区别，因为JSP在执行前首先被编译成一个Servlet。在Tomcat的临时目录下，可以找到一个`hello_jsp.java`的源文件，这个文件就是Tomcat把JSP自动转换成的Servlet源码。

JSP本质上就是一个Servlet，只不过无需配置映射路径，Web Server会根据路径查找对应的`.jsp`文件，如果找到了，就自动编译成Servlet再执行。在服务器运行过程中，如果修改了JSP的内容，那么服务器会自动重新编译。


JSP是一种在HTML中嵌入动态输出的文件，它和[[Servlet]]正好相反，Servlet是在Java代码中嵌入输出HTML；

JSP可以引入并使用JSP Tag，但由于其语法复杂，不推荐使用；

**JSP本身目前已经很少使用，我们只需要了解其基本用法即可。**


-   Servlet适合编写Java代码，实现各种复杂的业务逻辑，但不适合输出复杂的HTML；
-   JSP适合编写HTML，并在其中插入动态内容，但不适合编写复杂的Java代码。

通过结合Servlet和JSP的MVC模式，我们可以发挥二者各自的优点：

-   Servlet实现业务逻辑；
-   JSP实现展示逻辑。

但是，直接把MVC搭在Servlet和JSP之上还是不太好，原因如下：

-   Servlet提供的接口仍然偏底层，需要实现Servlet调用相关接口；
-   JSP对页面开发不友好，更好的替代品是模板引擎；
-   业务逻辑最好由纯粹的Java类实现，而不是强迫继承自Servlet。