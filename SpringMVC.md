# Spring MVC

---

## 1. MVC 是什么

MVC 是 Model-View-Controller（模型-视图-控制器） 的缩写，它是一种软件架构模式，用来实现业务逻辑与显示逻辑相分离。

早期 Web 开发中的 Servlet 加 JSP 就是一种典型的 MVC 模式，即 Servlet 充当控制器，调用相关业务逻辑处理后，将产生的数据模型转交给 JSP 等模版引擎来进行渲染，并将最终的页面返回给浏览器进行展示。

## 2. Spring MVC 是什么

Spring MVC 是 Spring Framework 中用于构建 Web 应用程序的一个子模块，全称 Spring Web MVC，它基于 MVC 架构模式，简化了传统的 Servlet 编程。

## 3. Spring MVC 的工作原理

在 Spring MVC 中，我们可以通过定义 Controller 方法来接收并处理请求。它的工作原理如下：

简单来说，Spring MVC 通过内置的 `DispatcherServlet` ，也叫前端控制器，来完成对所有请求的接收，然后根据请求路径将请求转发到对应的 Controller 方法。

更具体地说，`DispatcherServlet` 在接收到请求后，会根据 Spring MVC 中的 `HandlerMapping` 找到对应的 Controller 方法，这个 `HandlerMapping` 就维护了请求路径到 Controller 方法的映射，确定对应的 Controller 方法后，Spring MVC 会通过 `HandlerAdapter` 以适配器模式去调用对应的 Controller 方法。

## 4. Controller 控制器

* @Controller
* @RestController
* @RequestMapping
* @GetMapping
* @PostMapping
* @PutMapping
* @DeleteMapping
* @ResponseBody
* @RequestParam
* @RequestBody
* @PathVariable
* @DateParamFormat

## 5. 拦截器

* HandlerInterceptor

## 6. 全局异常处理器

* @ControllerAdvice
* @RestControllerAdvice
* @ExceptionHandler