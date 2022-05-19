## SpringMVC

#### 三层架构和MVC模型

##### 	三层架构

- ​	用户界面:web层(视图层)，和客户进行数据的交互
- ​	业务层：处理具体的业务逻辑
- ​	数据访问层：与数据库进行数据的交互

##### 	MVC模型

- ​	MVC：（Model-VIew-Controller）
- ​	JSP：Model2模式
  - 视图：（JSP/HTML）负责格式化数据，并展示给用户
  - 控制器：（Servlet）负责接收并转发请求，对请求进行处理后指派视图将响应结果展示给用户
  - 模型（Model）：（JavaBean）是系统的主体部分，对请求进行相应的业务处理

## SpringMVC概述

- SpringMVC是一种基于Java的实现MVC设计模型的请求驱动类型的轻量级web框架。
- 属于Spring Framework的产品，Spring框架提供了构建web程序的全功能MVC模块

## SpringMVC在三层架构中的位置

## 环境搭建

- 引入相应的依赖

  ```xml
  	<!--MVC依赖-->
  	<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>5.2.7.RELEASE</version>
      </dependency>
  	<!--web依赖-->
      <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>5.2.7.RELEASE</version>
      </dependency>
  	<!--servlet依赖-->
      <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>javax.servlet-api</artifactId>
        <version>4.0.1</version>
      </dependency>
  ```

- 核心控制器(DispatcherServlet)

  - 本质就是一个servlet
  - 用于接收用户的请求
  - 需要在web.xml中配置核心控制器

- ```xml
    <!--配置springMVC核心控制器-->
    <servlet>
      <servlet-name>springmvc</servlet-name>
      <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    </servlet>
    
    <servlet-mapping>
      <servlet-name>springmvc</servlet-name>
      <!--配置请求的拦截路径 -> 使用/表示拦截所有的请求-->
      <url-pattern>/</url-pattern>
    </servlet-mapping>
    ```


      <!--加载SpringMVC的配置文件-->
      <init-param>
        <param-name>contextConfigLocation</param-name>
          <!---->
        <param-value>classpath:SpringMVC.xml</param-value>
      </init-param>
  ```

- 创建控制器

  - 是具体处理请求的控制器 -> 请求控制器相对应

  - 创建的控制器必须继承AbstractController类

    ```java
    /*
    自定义的处理器,用于处理请求
     */
    public class HelloContrcller extends AbstractController {
        /*
        执行请求的方法
         */
        @Override
        protected ModelAndView handleRequestInternal(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {
            System.out.println("SpringMVC框架搭建成功");
            return null;
        }
  ```

​    

- 配置Spring的配置文件

  ```xml
  <!--配置请求路径和控制器-->
      <!--name:表示请求的路径,必须以"/"开头
          class:控制器全类名
      -->
      <bean name="/login"  class="contrcller.HelloContrcller"/>
  ```

## SpringMVC的执行过程及其组件



1. 中央控制器，

   接收用户的请求，相当于MVC中的C。是整个流程的中心

2. 处理器映射器（HandlerMapping）

   保存所有的请求和控制器之间的映射管理

3. 处理器适配器（HandlerAdapter）

   通过处理器适配器对处理器进行执行，采用的是适配器设计模式。通过扩充适配器可以对更多类型的处理器进行执行

4. 处理器（Controller）

   执行处理请求的操作，然后获取到要响应给用户的model和view

5. 视图解析器（ViewResolver）

   负责处理结果，生成view视图，根据获取到的逻辑视图名，在指定的位置将逻辑视图名转换为物理试图名，生成view对象

6. 视图（View）

   将展示的数据进行渲染，然后显示给客户

   ​	

## @Controller和@RequestMapping注解

@Controller注解：用于标识控制器，是写在类上面的

​	注：在SpringMVC中的配置文件中必须开启包扫描

@RequestMapping注解：用于映射指定的url和方法之间的关系。可以写在类上面，也可以写在方法上面。必须以"/"开头

​	属性: value	path	mathod



## 如何跳转页面(处理器方法的返回值)

1. ModelAndView：可以封装响应页面的名称和返还给用户的数据。model中的数据是保存在request中的，页面的跳转采用转发方式。



使用分页查询进行分页查询是,MyBatis使用的时查询所有的sql语句

在service中设置分页信息

PageHelper.startPage(当前页数和页面大小)

在设置了分页查询后的第一条sql语句可以实现分页,以后的sql语句是不能分页的

在控制器中使用pageinfo类保存分页信息



## 文件上传

1. 文件上传的要素
   1. 表单中有file元素
   2. 文件上传必须使用post提交方式
   3. 表单的enctuype属性修改成为多部分表单形式(enctype=multipart/from-data)
   4. 引入文件上传的依赖
      1. common-fileupload
      2. common-io
   5. 在springmvc中配置文件上传解析器