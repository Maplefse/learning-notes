# 1、SSM整合

spring、springMVC、myBatis

1. 引入依赖
   1. myBatis的依赖
      1. MyBatis 的jar包
      2. MyBatis整合Spring的jar包
      3. MySQL数据库依赖
      4. 连接池依赖
   2. Spring的依赖
      1. 4个核心jar包
      2. 事务依赖
      3. AOP的jar包
   3. SpingMVC的依赖
      1. SpringWEBjar包
      2. SpringMVCjar包
   4. ............
      1. 文件上次的jar包
      2. 日志jar包
      3. 分页jar包
      4. json的jar包
      5. JSTL的jar包
      6. servlet的jar包

2、配置Spring的配置文件

1. 引入
2. 配置数据源
3. 配置myBatis的核心工厂，SqlSessionFactory
4. 配置mapper扫描
5. 配置包扫描

3、配置SpringMVC的配置文件

1. 开启包扫描——扫描controller
2. 配置视图解析器

4、在web.xml中进行配置

1. 引入Spring的配置文件
2. 配置监听—监听Spring的配置文件
3. 配置核心控制器



spring不能处理静态资源文件，比如css，js，image

因为在配置springmvc的核心控制器的时候，拦截的路径是所有请求，所有的请求也包括静态资源。所有的静态资源都进入了mvc的核心控制器

springmvc的核心控制器是不具备处理静态资源的能力，所以在游览器中不能加载静态资源

解决方案：

1. 将静态资源交由默认的servlet进行处理
2. 在web.xml中配置相应的信息,将静态资源交由默认的servlet处理,只需配置servletMapping就行

注:此种方式的静态资源必须房在web的根目录下,且必须在核心控制器的拦截路径上面进行配置



- 让springMVC对静态资源进行放行
- 在SpringMVC文件中进行配置

此种方式静态资源可以在根目录下,也可以在web



1. 在SpringMVC中将静态资源交由默认的servlet处理
2. 在springmvc的配置文件中进行配置

# springMVC接收前端的参数

直接将前端发送的参数,作为控制器的方法的参数。要求：url当中参数的名称与方法参数名称一致

@RequestParam注解

​	属性：

​			value|name：参数的名称

​			required：

​			defaultvalue：

# springMVC编码格式的处理

通过过滤器进行配置：在web.xml中进行配置



# 页面的跳转

1. 重定项：
2. 转发



HttpServletRequest，HttpServletResponse，HttpSession

将 servlet中的对线作为控制器中，方法的参数进行传入



# 拦截器

SpringMVC中的拦截器相当于Servlet中的过滤器，用于对处理器进行预处理和后处理

SpringMVC中提供了HandlerInterceptor，它是所有拦截器的父类



步骤：

1. 创建拦截器并实现HandlerInterceptor接口
2. 重写拦截器接口中的方法
3. 在SpringMVC的配置文件中配置拦截器（拦截的url和放行的url）

注意:

1. 预处理方法其实就是拦截器的主要方法，当返回false的时候就被拦截，返回true的时候放行，进入控制器方法
2. 后处理方法会获取到控制器返回的modelAndView对象，在此方法中可以修改modelAndView中的数据和视图
3. 最后执行的方法是在将视图发送给用户之后进行执行，在此方法中只进行资源的清空
4. 一般自定义的拦截器只需要重写方法就行
5. Spring中的拦截器只能拦截controller中的方法，不能拦截jsp，css，html，js，images

SpringMVC中的拦截器和servlet中的过滤器的区别：

​	过滤器是servlet中的一部分，可以使用在任何的web项目中

​	拦截器是SpringMVC框架中的内容，只能使用在SpringMVC框架中

​	过滤器在url-pattern中配置了/*，可以对所有要访问的资源进行过滤

​	拦截器只拦截控制器中的方法，如果访问其它的内容，将不会被拦截



# Spring中的异常处理

在SpringMVC中使用的是统一,全局异常处理

dao，service，uitl抛给核心控制器统一处理

SpringMVC提供了一个异常处理器：HandlerException

方法：

1. 配置SpringMVC的异常处理器进行异常处理，直接在SpringMVC的配置文件中进行配置

   使用SimpleMapping

2. 自定义的异常处理类，实现SpringMVC提供的异常处理接口。

   实现后要将异常处理类注册到容器中



# SpringMVC中JSON数据处理

1. 通过Ajax发送请求，控制器返还的数据在Ajax中都是通过response body