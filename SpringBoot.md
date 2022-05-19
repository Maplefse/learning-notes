SpringBoot

### Spring是什么?

Spring是为了解决企业级应用开发的复杂性而创建的，简化开发。

[SpringBoot中文文档](http://felord.cn/_doc/_springboot/2.1.5.RELEASE/_book/)

### 如何简化？

为了简化开发的复杂性，Spring采用了以下4种关键策略：

1. 基于POJO的轻量级和最小侵入性编程
2. 通过IOC，依赖注入（DI）和面向接口实现松耦合：
3. 基于切面（AOP）和惯例进行声明式编程
4. 通过切面和模板减少样式代码

### SpringBoot是什么？

SpringBoot基于Spring开发，用于快速，敏捷的开发新一代基于Spring框架的应用程序。

它是和Spring框架紧密结合用于提示Spring开发体验的工具，SpringBoot以约定大于配置的核心思想，默认帮我们进行了很多设置。多数SpringBoot应用只需要很少的Spring配置，同时它集成了大量常用的第三方配置，SpringBoot应用中这些第三方库几乎可以零配置的开箱即用

Spring的主要优点：

- 为所有的Spring开发者更快的入门
- 开箱即用，提供各种默认配置来简化项目
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

# 微服务

### 微服务是什么

--以下资料来源于Martion Flower的《微服务》论文

在开始介绍微服务风格前，比较一下整体风格是很有帮助的：一个完整应用程序构建成一个单独的单元。企业级应用通常被构建成三个主要部分：客户端用户界面（由运行在客户机器上的浏览器的 HTML 页面、Javascript 组成）、数据库（由许多的表构成一个通用的、相互关联的数据管理系统）、服务端应用。服务端应用处理 HTTP 请求，执行领域逻辑，检索并更新数据库中的数据，使用适当的 HTML 视图发送给浏览器。服务端应用是完整的 ，是一个单独的的逻辑执行。任何对系统的改变都涉及到重新构建和部署一个新版本的服务端应用程序。

虽然这样的整体应用程序十分好用，但是**一旦变更应用程序的一小部分，就要整个重新构建和部署**。随着时间推移就很难继续保持模块化结构，一个模块的变更很难不影响到其它模块，扩展就需要对整个引用程序进行扩展。

这导致了微服务架构风格的出现：**把应用程序构建为一套服务。事实是，服务可以独立部署和扩展，每个服务提供了一个坚实的模块边界，甚至不同的服务可以用不同的编程语言编写。它们可以被不同的团队管理。**

微服务风格要求：在开发一个应用的时候，这个应用**必须构建成一系列小服务的组合，可以通过http的方式进行互通。**

**微服务风格不是什么新东西，它至少可以追溯到 Unix 的设计原则**

![](\assets\整体架构与微服务架构.png)

上图为整体架构与微服务架构

## 微服务风格的特性

### 组件化与服务



# 第一个SpringBoot程序

### 创建SpringBoot项目的两种方式

1. 在官网配置之后直接下载，导入idea开发
2. 直接在idea创建一个springboot项目（一般开发直接在idea中创建）
   1. idea创建新项目中选择"Spring Initializr" ->next
   2. 设置项目配置 ->next
   3. 选择项目初始配置 ->next
   4. 项目存放路径 ->next
   5. 创建完成

### SpringBoot项目文件

![QQ截图20210423093949](\assets\QQ截图20210423093949.png)

1. pom.xml中的依赖说明

```xml
<!--父依赖-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.5</version>
        <relativePath/> 
    </parent>

    <groupId>com.jbit</groupId>
    <artifactId>springboot_demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot_demo</name>
    <description>Demo project for Spring Boot</description>
    <properties>
        <java.version>11</java.version>
    </properties>

    <dependencies>

        <!--web依赖:tomcat,dispatcherServlet.xml-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>


        <!--单元测试-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
        </dependency>
        <!--springboot热部署依赖-->

        <!--所有的springboot依赖都是使用'spring-boot-starter'开头的-->
    </dependencies>

    <build>
        <!--打包插件-->
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

2. src下的java路径中SpringbootDemoApplication为SpringBoot程序的主入口,它本身是一个Spring的组件，运行这个类即可启动springboot程序

![QQ截图20210423094334](\assets\QQ截图20210423094334.png)

3. 在主程序的同级目录下，新建一个controller包，**一定要在同级目录下，否则识别不到**

   在包中创建一个类

   ```java
   @RestController
   public class HelloWorld {
   
       @RequestMapping("/hello")
       public String hello(){
           return "hello,world";
       }
   
   }
   ```

   启动项目,游览器请求hello这个路径即可拿取到hello,world数据

4. resources下,application.properties配置文件中通过`server.port=8080`设置端口号

5. 在resources中新建banner.txt文件,修改springboot运行后的显示样式



# SpringBoot自动装配原理

#### **pom.xml**

- spring-boot-dependencies:核心依赖在父工程中
- 因为有这些版本仓库,所以在导入SpringBoot依赖的时候不需要指定版本

#### **启动器**

- ```xml
  <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>2.4.5</version>
        <scope>compile</scope>
  </dependency>
  ```

- 启动器:Springboot的启动场景

- 比如spring-boot-starter-web，它会帮我们自动导入web环境所有的依赖

- springboot会将所有的功能场景，都变成启动器

- 我们要使用什么功能，就只需要找到对应的启动器就可以了 `starter`

#### **主程序**

```java
//它本身就是Spring的一个组件
//程序的主入口
//@SpringBootApplication:标注这个类是一个springboot的应用
@SpringBootApplication
public class SpringbootDemoApplication {

    public static void main(String[] args) {

        //将springboot应用启动
        SpringApplication.run(SpringbootDemoApplication.class, args);
    }

```

点进`@SpringBootApplication`注解，可以看到这样一个类

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited

//重点在以下2个注解
@SpringBootConfiguration
@EnableAutoConfiguration


@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    //省略其中代码
}
```

#### 注解

```java
@SpringBootConfiguration //springboot的配置
//其中有
    @Configuration	//表示这是一个配置类，和以前编写的配置文件一样，也可以给容器中添加组件
    @Component		//说明这也是一个spring的组件


@EnableAutoConfiguration	//启用 SpringBoot 的自动配置机制
//其中有
	@AutoConfigurationPackage	//自动配置包
	@Import(AutoConfigurationImportSelector.class)	//导入选择器
```

#### **Conditional**

SpringBoot核心注解`@Conditional`它//根据不同的条件判断，如果满足指定的条件，整个配置类里面的配置就会生效；

Conditional相关的其它注解：

- @ConditionalOnBean	在某个 bean 存在的时

- @ConditionalOnMissingBean	在某个 bean 不存在的时候

- @ConditionalOnClass	当前 classPath 下可以找到某个 class 的时候

- @ConditionalOnMissingClass	当前 classPath 下无法找到某个 class 的时候

- @ConditionalOnResource	当前 classPath 下是否存在某个资源文件

- @ConditionalOnProperty	当前 JVM 是否包含某个属性值

- @ConditionalOnWebApplication	当前 Spring context 是否是 web 应用程序

#### ImportResource

@ImportResource注解用于导入Spring的配置文件，让配置文件里面的内容生效

Spring Boot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别；
想让Spring的配置文件生效，加载进来；将@ImportResource标注在**主程序类上**。


# yaml

Springboot中，除了properties文件作为配置文件，还有yaml文件同样可以作为配置文件使用

SpringBoot使用一个全局的配置文件 ， 配置文件名称是固定的

- application.properties

- - 语法结构 ：key=value

- application.yml

- - 语法结构 ：key：空格 value

正常的情况是先加载yml，接下来加载properties文件。如果相同的配置存在于两个文件中。最后会使用properties中的配置。最后读取的优先级最高。

 两个配置文件中的端口号不一样会读取properties中的端口号

```yaml
# yaml语法
# 对空格的要求十分严格
# key:(空格)value

# 存储对象
student:
  name: maplef
  age: 20

#行内写法

student: {name: maplef,age: 20}

# 数组
pest:
  - cat
  - dog
  - pig

# 数组行内写法
pest: [cat,dog,pig]
```

yaml可以直接给实体类赋值

现有如下实体类

```java
public class Person {

    private String name;
    private Integer age;
    private Boolean happy;
    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
    //省略get/set方法   
}
```

在yaml中编写实体类的数据

```yaml
person:
  name: maplef
  age: 20
  happy: true
  birth: 2021/1/1
  maps: {K1: v1,k2: v2}
  lists:
    - code
    - music
    - girl
  dog:
    name: 乖乖
    age: 3

```

yaml通过注解`@ConfigurationProperties(prefix = "person")`给实体类注入值

![image-20210426093231900](\assets\image-20210426093231900.png)



实体类中,使用@ConfigurationProperties注解需要通过上方的配置,如果不使用配置注解会报错,但是不影响使用

```java
@ConfigurationProperties(prefix = "person") 
//在实体类中，通过这个配置的prefix = "person"把这个实体类与yaml的配置文件值绑定。将yaml的值注册到实体类中

/*
 *将配置文件中配置的每一个属性的值,映射到这个组件中;
 *告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定
 *参数 prefix = "person" :将配置文件中的person下的所有属性一一对应
 *只有这个组件是容器中的组件,才能使用容器提供的@ConfigurationProperties功能
 */
```

**yaml的其它特性**

- 松散绑定:yaml中属性名为:last-name，在实体类中可以直接对lastName属性绑定，-后面跟着的第一个字母默认是大写，这就是松散绑定

- JSR-303校验：在后台字段增加一层过滤器验证，用于保证数据的合法性


- spring-boot中可以用@validated来校验数据，如果数据异常会统一抛出异常，方便异常中心统一处理


```java
@Validated  //JSR-303数据校验
public class Person {
    @Email		//表示email属性的值必须是Email邮箱格式
    private String email;
```

## 多个运行环境配置

```yaml
server:
	prot: 8080
String:
	profiles:
		active: dev
# 表示使用	profiles: dev的配置	
		
---
server:
	port: 8081
String:
	profiles: dev
	
# 用---分割不同的配置
---
server:
	prot: 8082
String:
	profiles: test
```

使用这种方式，就可以在一个文件中配置不同运行环境的配置

# SpringBoot Web开发

## 1、静态资源



addResourceHandlers

http://localhost:8080/webjars/jquery/3.6.0/jquery.js

在springboot中可以使用以下方式处理静态资源

1. webjars
2. public，static，/**，resources

静态资源访问的优先级：resources > static > public

静态资源就可以存放在以下路径

![image-20210608111328121](\assets\image-20210608111328121.png)

- resource下
- resource/public下
- resource/static下
- resource/resource下

## 2、页面

可以将html等页面放置在以下文件夹中

![image-20210428091754817](\assets\image-20210428091754817.png)

在templates目录下的所有页面，只能通过controller访问（需要模板引擎的支持）

## 3、模板引擎thymeleaf

##### 导入thymeleaf

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

导入后将html放在templates目录下即可通过controller访问

##### 数据传递

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

    <!--所有的html元素都可以被thymeleaf替换接管: th:属性名-->
    <h1 th:text="${message}" ></h1>
</body>
</html>
```

thymeleaf使用时要注意两点:

1. 在html标签内导入:'xmlns:th="http://www.thymeleaf.org"'

2. 接收属性使用：th:属性名   对标签的属性进行替换

3. 静态资源访问使用:th:href="@{/css/dashboard.css}"(最外层的resources路径与static路径直接省略)

   ps:所有的页面的静态资源推荐使用thymeleaf接管


##### thymeleaf语法

- ${message}   : 输出内容
- th:text=    ：直接将数据当成文本输出
- th:utext=   ：会将数据进行转义，如果数据带有html标签则转义成标签并输出
- th:each="user:${users}"    ：对users这个数据进行便利操作，输出user
- th:href="@{静态资源路径}"
- th:fragment="自定义名字" ：将html标签抽离出来
- th:insert="~{导入标签路径：：名字}"   ：将抽离出的html标签插入到当前标签中
- th:replace="~{导入标签路径：：名字}"   ：将抽离出的html标签替换当前标签（**一般使用这种方式导入外部标签**）
  - 一般在项目中，将公用的html标签单独放置在一个文件夹，使用th语法抽离出来，再在需要的地方导入

## SpringMVC自动配置

我们可以在SpringBoot中对SpringMVC的一些功能自定义,然后交给SpringBoot自动装配。让SpringMVC的功能实现改为我们自定义的实现

自动配置在 Spring 默认功能上添加了以下功能：

- 引入 `ContentNegotiatingViewResolver` 和 `BeanNameViewResolver` bean。
- 支持服务静态资源，包括对 WebJar 的支持。
- 自动注册 `Converter`、`GenericConverter` 和 `Formatter` bean。
- 支持 `HttpMessageConverter`。
- 自动注册 `MessageCodesResolver`。
- 支持静态 index.html。
- 支持自定义 Favicon 。
- 自动使用 `ConfigurableWebBindingInitializer` bean。

如果您想保留 Spring Boot MVC 的功能，并且需要添加其他 [MVC 配置](https://docs.spring.io/spring/docs/5.1.3.RELEASE/spring-framework-reference/web.html#mvc)（interceptor、formatter 和视图控制器等），可以添加自己的 `WebMvcConfigurer` 类型的 `@Configuration` 类，但**不能**带 `@EnableWebMvc` 注解。如果想自定义 `RequestMappingHandlerMapping`、`RequestMappingHandlerAdapter` 或者 `ExceptionHandlerExceptionResolver` 实例，可以声明一个 `WebMvcRegistrationsAdapter` 实例来提供这些组件。

如果想完全掌控 Spring MVC，可以添加自定义注解了 `@EnableWebMvc` 的 @Configuration 配置类。

```java
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {
    
    //ViewResolver 实现了视图解析器接口的类,可以把它看作视图解析器
    //@Bean将我们自定义的视图解析器交给Springboot,
    @Bean
    public ViewResolver myViewResolver(){
        return new MyViewResplver();
    }
    //自定义了一个视图解析器
    public static class MyViewResplver implements ViewResolver{

        @Override
        public View resolveViewName(String viewName, Locale locale) throws Exception {
            return null;
        }
    }
}
```

如上所示:想要自定义SpringMVC的功能,只需要编写出对应功能的组件,将它交给SpringBoot(@Bean)，SpringBoot会帮我们自动装配

在SpringBoot中，会有非常多的xxxxConfiguration帮助进行拓展配置，只要看见了它就要小心了



## 项目国际化

国际化就是对网站语言的切换

在IDEA中首先要统一设置properties的编码为UTF-8

<img src="\assets\QQ截图20210509215220.png" alt="QQ截图20210509215220" style="zoom: 50%;" />

#### 配置文件编写

1. 随后在项目resources资源文件下新建一个i18n目录，存放国际化配置文件

2. 建立一个login.properties文件,一个login_zh_CN.properties文件，IDEA会自动识别它们为国际化的配置文件

3. ![QQ截图20210509215716](\assets\QQ截图20210509215716.png)对文件夹右键New即可创建新的配置文件

4. 接着通过![QQ截图20210509220313](\assets\QQ截图20210509220313.png)IDEA的视图去编写国际化的内容

5. ![QQ截图20210509220704](\assets\QQ截图20210509220704.png)

   通过+号，对页面的属性进行国际化内容的配置

   它会自动配置给properties文件，自此，配置文件的步骤完成

   #### 配置页面国际化

   1. 在国际化的配置文件编写完成后，首先要配置国际化的目录

      在springBoot的application配置文件中配置

      ```markdown
      # 配置国际化的文件真实路径
      spring.messages.basename=i18n/login
      # 我们国际化的文件放在i18n这个目录下,所以从i18n目录找起
      ```

   2. 在页面中去获取message的值，即可拿到国际化的内容，这里使用Thymeleaf的#{...}功能获取

      ![微信图片_20210509221409](\assets\微信图片_20210509221409.jpg)

   3. 设置根据按钮自动切换中英文

      在Spring中有一个国际化的Locale （区域信息对象）；里面有一个叫做LocaleResolver （获取区域信息对象）的解析器！

      那假如我们现在想点击链接让我们的国际化资源生效，就需要让我们自己的Locale生效！

      我们去自己写一个自己的LocaleResolver，可以在链接上携带区域信息！

      修改一下前端页面的跳转连接：

      ```html
      <!-- 这里传入参数不需要使用 ？使用 （key=value）-->
      <a class="btn btn-sm" th:href="@{/index.html(l='zh_CN')}">中文</a>
      <a class="btn btn-sm" th:href="@{/index.html(l='en_US')}">English</a>
      ```

      再去写一个处理的组件类

      ```java
      package com.kuang.component;
      
      import org.springframework.util.StringUtils;
      import org.springframework.web.servlet.LocaleResolver;
      
      import javax.servlet.http.HttpServletRequest;
      import javax.servlet.http.HttpServletResponse;
      import java.util.Locale;
      
      //可以在链接上携带区域信息
      public class MyLocaleResolver implements LocaleResolver {
      
          //解析请求
          @Override
          public Locale resolveLocale(HttpServletRequest request) {
      
              String language = request.getParameter("l");
              Locale locale = Locale.getDefault(); // 如果没有获取到就使用系统默认的
              //如果请求链接不为空
              if (!StringUtils.isEmpty(language)){
                  //分割请求参数
                  String[] split = language.split("_");
                  //国家，地区
                  locale = new Locale(split[0],split[1]);
              }
              return locale;
          }
      
          @Override
          public void setLocale(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Locale locale) {
      
          }
      }
      ```

      

   4. 为了让区域化信息能够生效，需要配置这个组件。在springboot的MvcConfig下添加bean

      ```java
      @Bean
      public LocaleResolver localeResolver(){
          return new MyLocaleResolver();
      }
      ```

## 异常处理

1. 在springboot中，自动配置了程序发生异常后的页面跳转路径

   ![image-20210615145224401](\assets\image-20210615145224401.png)

   将错误页面放置在如图的目录中，发生404报错时，自动访问404.html页面

2. 异常处理的自动装配解析

   1. 自动装配类名为：`ErrorMvcAutoConfiguration`这个类中自动配置了异常处理机制
   2. 组件：`public BasicErrorController basicErrorController(ErrorAttributes errorAttributes,ObjectProvider<ErrorViewResolver> errorViewResolvers)`
      - 处理默认的/error路径的请求,相应错误的页面
   3. 组件`public View defaultErrorView()`
      - 默认的响应错误页面
   4. `public BeanNameViewResolver beanNameViewResolver()` -> 视图解析器
      - 按照视图名，去容器中找到View对象
   5. `DefaultErrorViewResolver conventionErrorViewResolver()` 默认的错误视图解析器
      - 发生异常时，根据http的状态码作为视图的地址查找错误的页面
   6. `public DefaultErrorAttributes errorAttributes()`
      - 定义错误页面中可以包含的数据



### 自定义异常处理的几种方式

1. 使用`@ExceptionHandler`注解进行异常处理

   ```java
   //在controller类中编写
   @ExceptionHandler(value = Exception.class)
   //注解内的参数表示要处理的异常类型,Exception即表示处理所有的异常
   public String exceptionHandler(Exception e){
       return "出现异常!";
   }
   ```

   这种方式只能对编写异常方法的controller类生效，耦合度高

2. 在父类声明异常

   在controller中声明一个类`baseController`，将它作为所有controller的父类

   ```java
   public class baseController {
       @ExceptionHandler(value = Exception.class)
       public ModelAndView defaultErrorHandler(Exception e){
           ModelAndView mv = new ModelAndView();
           
           mv.addObject("message",e.getMessage());
           mv.addObject("status",102);
           
           mv.setViewName("error")	//自己定义的错误页面
           return mv;
       }
   }
   ```

   所有的controller继承这个类为父类即可使用异常声明

   比起上一种方法多了复用性，但还是与controller耦合在一起

3. 使用`@ControlleAdvice`和`@ExceptionHandler`注解处理异常

   先单独声明一个异常包和类![image-20210617000823931](\assets\image-20210617000823931.png)

   异常类内容：

   ```java
   @ControllerAdvice	//使用这个注解后,全部的异常都会由它处理
   public class GlobalExceptionHandler {
       @ExceptionHandler(value = Exception.class)
       @ResponseBody
       public Object globalException(Exception e){
           Map<String,Object> map = new HashMap<>();
           map.put("coe",100);
           map.put("message",e.getMessage);
       }
   }
   ```

   这种方式耦合度较低，且一次编写全局使用，一般情况下都使用这种方式



# 文件上传

## 文件上传的三要素

1. 表单中必须有文件域(type=file)
2. 表单提交方式必须是Post方式
3. 表单的enctype属性必须是多部分表单形式(enctype="nultipart/form-data")

## 文件上传的实现

1. 导入依赖

   ```xml
   <!--文件上传依赖-->
   <dependency>
       <groupId>commons-fileupload</groupId>
       <artifactId>commons-fileupload</artifactId>
       <version>1.4</version>
   </dependency>
   ```

2. 在配置文件中配置文件的最大上传大小

   ```properties
   spring.servlet.multipart.max-file-size=1GB
   spring.servlet.multipart.max-request-size=2GB
   ```

   

3. 实现方法

   ```java
   @Controller
   public class indexController {
   
       @GetMapping("/")
       public String indexPage(){
           return "index";
       }
   
       //用MultipartFile类型接收文件
       @PostMapping("/upload")
       public ModelAndView uploadFile(HttpServletRequest request, String username, List<MultipartFile> uploadFile) throws IOException {
           ModelAndView mv = new ModelAndView();
   
               //使用实体类来存储文件
               FilePojo pojo = new FilePojo();
               pojo.setUserName(username);
               pojo.setFileJpg(uploadFile);
   
               //文件上传操作
               //设置文件保存的路径
               String path = "D://temp//";
               System.out.println("path:"+path);
   
               //通过循环,拿取出所有的文件并保存
               for (int i = 0; i < pojo.getFileJpg().size(); i++) {
                   MultipartFile file = pojo.getFileJpg().get(i);
                   //获取文件名
                   String filename = file.getOriginalFilename();
                   //创建一个文件对象
                   File dest = new File(path,filename);
                   //判断保存文件的路径是否存在
                   if (!dest .getParentFile().exists()){
                       //没有则创建目录
                       dest .getParentFile().mkdirs();
   
   
                   }
                   //保存文件
                   file.transferTo(dest);
                   //将文件名与目录传输到前台方便回显
                   mv.addObject("uploadPath","/temp/"+filename);
                   System.out.println(path+filename);
               }
   
   
   
           mv.addObject("username",username);
           mv.addObject("fileName","上传成功");
           mv.setViewName("main");
           return mv;
       }
   
   }
   ```

   

4. 文件上传页面

   ```html
   <body>
       <form th:action="@{/upload}" method="post" enctype="multipart/form-data">
           用户名:<input type="text" name="username" placeholder="请输入用户名"/><br/>
           图片:<input type="file" name="uploadFile"/><br/>
           图片:<input type="file" name="uploadFile"/><br/>
           图片:<input type="file" name="uploadFile"/><br/>
           <input type="submit" value="提交"/>
       </form>
   
   </body>
   ```

   

5. 图片回显的设置

   ```java
   @Configuration
   public class MyWebAppConfigurer implements WebMvcConfigurer {
       @Override
       public void addResourceHandlers(ResourceHandlerRegistry registry) {
           registry.addResourceHandler("/temp/**").addResourceLocations("file:D:/temp/");
       }
   }
   ```

   



# 整合JSP

1. 导入依赖

   ```xml
   <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>javax.servlet-api</artifactId>
   </dependency>
   <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>jstl</artifactId>
   </dependency>
   <!--jasper是Tomcat使用JSP引擎,可以将项目与Tomcat分离-->
   <dependency>
       <groupId>org.apache.tomcat.embed</groupId>
       <artifactId>tomcat-embed-jasper</artifactId>
   </dependency>
   ```

2. 创建web目录，整体结构如下

   ![image-20210614233004485](\assets\image-20210614233004485.png)

3. 将webapp文件夹设置为根目录

   ![image-20210614233312459](\assets\image-20210614233312459.png)

4. 配置项目的资源路径和返回页面的类型

   在properties文件中配置

   ```properties
   #配置响应页面的前缀
   spring.mvc.view.prefix=/
   #配置响应页面的后缀
   spring.mvc.view.suffix=.jsp
   ```

5. 创建控制器和返回页面(同ssm项目一样,不做深入)

6. 修改工作目录

   ![image-20210614235346798](\assets\image-20210614235346798.png)

7. 运行,访问jsp页面

# SpringBoot拦截器

**spring中使用拦截器必须实现HandlerInterceptor接口**

1. `preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)`
   - 进行拦截处理，在控制器方法执行前执行
2. `postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)`
   - 进行响应处理，在控制器执行完成后但是没有对客户返回响应的时候执行
3. `public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)`
   - 在中央控制器完全处理完请求后执行，已经将响应页面发送给客户后
   - 一般用于资源的释放

### 使用

1. 创建自定义的拦截器，必须实现HandlerInterceptor接口

```java
public class LoginHandlerInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        //获取登录的用户
        Object loginuser = request.getSession().getAttribute("loginuser");

        //登录成功之后,应该有用户的session
        if (loginuser == null) {
            //等于null证明没有登录,拒绝访问
            request.setAttribute("msg", "请登录后操作");
            response.sendRedirect("/login.html");
            //注意:如果返回的地址不对,会出现重定项次数过多的bug
            return false;
        }
        return true;
        //返回true表示放行
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }
}
```

2. 注册拦截器

```java
@Configuration
//@EnableWebMvc //它只是导入了一个类:DelegatingWebMvcConfiguration:从容器中获取所有的WebmvcConfig
public class MyMvcConfig implements WebMvcConfigurer {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {

    }

    //重写拦截器的方法
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginHandlerInterceptor()).addPathPatterns("/**").
            excludePathPatterns("/login.html", "/login", "/user/login", "/", "/static/**", "***/error");
        //将自定义的拦截器添加给他,同时设置拦截的路径与放行的路径
        //addPathPatterns("/**")拦截的路径
        //excludePathPatterns()放行的路径
    }
}
```

注册后即可使用



# 数据访问

## JPA

1. jpa介绍

   JAP是Java持久化规范；通过JDK5.0注解或XML描述对象-关系表映射关系，并将运行期的实体对象持久化到数据库中

2. Spring Data JPA

   2.1标准化
   JPA 是 JCP 组织发布的 Java EE 标准之一，因此任何声称符合 JPA 标准的框架都遵循同样的架构，提供相同的访问API，这保证了基于JPA开发的企业应用能够经过少量的修改就能够在不同的JPA框架下运行。
   2.2容器级特性的支持
   JPA框架中支持大数据集、事务、并发等容器级事务，这使得 JPA 超越了简单持久化框架的局限，在企业应用发挥更大的作用。
   2.3简单方便
   JPA的主要目标之一就是提供更加简单的编程模型：在JPA框架下创建实体和创建Java 类一样简单，没有任何的约束和限制，只需要使用 javax.persistence.Entity进行注释，JPA的框架和接口也都非常简单，没有太多特别的规则和设计模式的要求，开发者可以很容易的掌握。JPA基于非侵入式原则设计，因此可以很容易的和其它框架或者容器集成。
   2.4查询能力
   JPA的查询语言是面向对象而非面向数据库的，它以面向对象的自然语法构造查询语句，可以看成是Hibernate HQL的等价物。JPA定义了独特的JPQL（Java Persistence Query Language），JPQL是EJB QL的一种扩展，它是针对实体的一种查询语言，操作对象是实体，而不是关系数据库的表，而且能够支持批量更新和修改、JOIN、GROUP BY、HAVING 等通常只有 SQL 才能够提供的高级查询特性，甚至还能够支持子查询。
   2.4高级特性
   JPA 中能够支持面向对象的高级特性，如类之间的继承、多态和类之间的复杂关系，这样的支持能够让开发者最大限度的使用面向对象的模型设计企业应用，而不需要自行处理这些特性在关系数据库的持久化。

### 使用JPA

1. 导入依赖

   ```java
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-jpa</artifactId>
   </dependency>
       
       <!--数据库依赖-->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
   </dependency>
   ```

   

2. 在properties.yml中配置

   ```yaml
   spring:
     datasource:
       url: jdbc:mysql://localhost:3306/mytest
       type: com.alibaba.druid.pool.DruidDataSource
       username: root
       password: root
       driver-class-name: com.mysql.jdbc.Driver 
       //数据库驱动
     jpa:
       hibernate:
         ddl-auto: update //自动更新
       show-sql: true  //日志中显示sql语句
   ```

3. 现在有这个实体类

   ```java
   @Entity//标识实体类
   @Table(name = "t_user")//映射的数据表
   public class Users {
   
       @Id	//标识它是主键
       @GeneratedValue(strategy = GenerationType.IDENTITY) //标识主键的生成策略
       private int id; //标识主键
   
       @Column(name ="user_name")//标识对应的列
       private String username;
   
       @Column(name = "true_name")
       private String truename;
   
       @Column(name = "email")
       private String email;
       
       //省略getset方法
   }
   ```

4. 接着在dao层中用接口实现

   dao继承CrudRepository接口，这个接口定义了操作数据的统一方法，自定义的接口中可以不用定义任何方法

   ```java
   /*
   接口中的泛型
       第一个参数:要操作的实体对象
       第二个参数:主键的数据类型
    */
   public interface UserRepository extends CrudRepository<Users,Integer> {
   }
   ```

5. 然后是service接口

   ```java
   public interface UserService {
   
       /*
       Iterable是一个array
        */
       Iterable<Users> fandAll();
       //fandAlll -> 拿取表中所有数据
   }
   ```

   service实现

   ```java
   @Service("userService")
   public class UserServiceImpl implements UserService {
   
       @Autowired
       private UserRepository userRepository;
   
       @Override
       public Iterable<Users> fandAll() {
           return userRepository.findAll();
       }
   }
   ```

6. controller层

   ```java
   @RestController
   public class IndexController {
       @Autowired
       private UserService userService;
   
       @GetMapping("/")
       public Object findAll(){
           Iterable<Users> users = userService.fandAll();
           //拿取到所有数据并返回
           return users;
       }
   }
   ```

### 使用PagingAndSortingRepository接口操作数据

`PagingAndSortingRepository`接口继承了`CrudRepository`接口；具有CrudRepository接口的所有功能，同时新增了排序和分页查询的功能

#### 排序的实现

1. 同CrudRepository接口一样，创建dao接口

   ```java
   public interface UserPageRepository extends PagingAndSortingRepository<Users,Integer> {
       //dao中不做任何处理
   }
   
   ```

2. 在service中声明

   ```java
   //接口中声明方法
   //排序
   Iterable<Users> findAllSort();
   ```

   ```java
   //service的实现类
   //排序
   @Autowired
   private UserPageRepository userPageRepository;
   
   @Override
   public Iterable<Users> findAllSort() {
   
       //设置排序对象
       //sort导入类是org.springframework.data.domain.Sort;
       Sort sort = Sort.by(Sort.Direction.DESC,"id");
       //by():创建排序对象,对id数据进行排序,第一个参数为排序的规则(ASC/DESC)
       return userPageRepository.findAll(sort);
   }
   ```

3. controller

   ```java
   @GetMapping("/sort")
   public Object findSort(){
       Iterable<Users> allSort = userService.fandAllSort();
       //拿取到排序后的所有数据并返回
       return allSort;
   }
   ```

#### 分页的实现

实现步骤同排序一样

1. service声明方法

   接口

   ```java
   //分页
   Page<Users> findAllPage(int pageIndex);
   ```

   实现类

   ```java
   @Autowired
   private UserPageRepository userPageRepository;
   
   @Override
   public Page<Users> findAllPage(int pageIndex) {
   
       //设置分页信息
       //PageRequest.of()设置分页的属性
       //参数: 当前页数(页数从0开始),页面大小,排序(可选)
       Pageable pageable = PageRequest.of(pageIndex-1,2);
       return userPageRepository.findAll(pageable)
   }
   ```

2. controller实现并返回（省略）

#### 条件查询

同上方步骤

1. service层

   ```java
   //创建接口
   //方法名不能随意命名,方法命名时要使用实体类中的属性
   //格式为:findBy+查询条件的实体类属性名
   Users findByUsername(String username);//username:查询条件
   
   
   //方法名等于查询条件
   //例如这个方法名
   Users findByUsernameAndEmail();
   //等于: 
   //select * from 表 where username=? and email=?
       
   
   //模糊查询
   Users findByUsernameLike(String username);
   //等于: select * from 表 where username like ?
   //在实现方法中,要对传进来的数据前后根据需求加上%号
   ```

   实现

   ```java
   @Autowired
   private UserJpaRepository userJpaRepository;
   
   //条件查询
   @Override
   public Users findByUsername(String username) {
       return userJpaRepository.findByName(username);
   }
   ```

2. controller层实现

   ```java
   @GetMapping("/byName")
   public Object byName(String username){
       Users user = userService.findByUsername(username);
       return user;
   }
   ```

   



## 整合JDBC

#### 配置JDBC

SpringBoot对于数据访问层，统一采用SpringData的方式处理

使用JDBC需要导入对应的启动器：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

还需要在配置文件中编写连接数据库的信息

```yml
spring:
  datasource:
    username: root		# 连接数据库账号
    password: ""		# 连接数据库密码
    # 假如时区报错了,增加一个时区配置就ok:serverTimezone=UTC
    # UTC时区可能会有两个小时的延迟
    url: jdbc:mysql://localhost:3306/smbms?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    # 连接数据库路径
    driver-class-name: com.mysql.jdbc.Driver

    type: com.alibaba.druid.pool.DruidDataSource
    # 指定自定义的数据源类型
```

配置完以上的东西后，就可以直接连接数据库了，springboot已经默认进行了自动配置

```java
@SpringBootTest
class SpringbootDataJdbcApplicationTests {

    //DI注入数据源
    @Autowired
    DataSource dataSource;

    @Test
    public void contextLoads() throws SQLException {
        //看一下默认数据源
        System.out.println(dataSource.getClass());
        //获得连接
        Connection connection =   dataSource.getConnection();
        System.out.println(connection);
        //关闭连接
        connection.close();
    }
}
```

在不手动配置数据源的情况下通过在test运行上方代码得知springboot给我们默认配置的数据源为:**class com.zaxxer.hikari.HikariDataSource**

**HikariDataSource 号称 Java WEB 当前速度最快的数据源，相比于传统的 C3P0 、DBCP、Tomcat jdbc 等连接池更加优秀；**



有了数据源之后，就可以通过spring封装后的JDBCTemplate进行数据库操作

#### JDBCTemplate

JDBCTemplate主要提供以下的方法：

- execute：可以执行任何SQL语句，一般用于执行DDL语句（创建、删除、修改：数据库、表结构等）
- update：用于执行新增、修改、删除等语句
- query或queryForXXX：执行查询等相关语句
- call：执行存储过程，函数相关语句

一个简单的运行代码：

```java
    @Autowired
    JdbcTemplate jdbcTemplate;
	//查询数据所有信息
    @RequestMapping("/userList")
    @ResponseBody
    public List<Map<String,Object>> userList(){
        String sql = "select * from smbms_user";
        List<Map<String, Object>> maps = jdbcTemplate.queryForList(sql);
        return maps;
    }
```



# 整合Druid

### 导入druid依赖

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.2.6</version>
</dependency>
```

导入后在application配置中配置type属性即可切换为druid

```yml
type: com.alibaba.druid.pool.DruidDataSource
```

### druid的属性配置

```yml
#Spring Boot默认是不注入这些属性值的,需要自己绑定#druid数据源专有配置
initialsize: 5
minIdle: 5
maxActive: 20
maxwait: 60000
timeBetweenEvictionRunsMillis: 60000
minEvictableIdleTimeMillis: 300000
validationQuery: SELECT 1 FROM DUAL
testwhileIdle: true
testOnBorrow: false
test0nReturn: false
poolPreparedstatements: true
#配置监控统计拦战的filters. stat:监控统计、Log4j;日志记录、wall:防御sqL注入
#如果允许时报错 java.Lang.CLassNotFoundException: org.apache.log4j .Priority
#则导入log4j依赖即可.Maven地址: https: / /mvnrepository.com/artifact/log4j/Log4j
filters: stat,wall,log4j
maxPoolPreparedstatementPerconnectionsize: 20
useGlobalDataSourcestat: true
connectionProperties: druid.stat.mergesql=true;druid.stat.slowSq1Millis=500

```

![640 (2)](\assets\640 (2).webp)

![640](\assets\640.webp)

![640 (1)](\assets\640 (1).webp)



通过SpringBoot的Config绑定配置文件

```java
@Configuration
public class DruidConfig {
    /*
       将自定义的 Druid数据源添加到容器中，不再让 Spring Boot 自动创建
       绑定全局配置文件中的 druid 数据源属性到 com.alibaba.druid.pool.DruidDataSource从而让它们生效
       @ConfigurationProperties(prefix = "spring.datasource")：作用就是将 全局配置文件中
       前缀为 spring.datasource的属性值注入到 com.alibaba.druid.pool.DruidDataSource 的同名参数中
     */
    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }

}
```

### Druid的数据源监控功能

Druid提供了监控数据源的功能,并自带了一个web界面

可以在SpringBoot的Config中配置，设置后台管理页面的登录账号，密码等

```java
    //后台监控功能
    @Bean
    public ServletRegistrationBean StatViewServlet(){
        ServletRegistrationBean<StatViewServlet> bean = new ServletRegistrationBean<>(new StatViewServlet(), "/druid/*");

        //后台需要进行登录
        HashMap<String, String> initParameters = new HashMap<>();
        //整加配置
        initParameters.put("loginUsername","admin");    //登录的key是固定的
        initParameters.put("loginPassword","123456");

        //允许谁可以访问
        initParameters.put("allow","");
        //参数为空,代表所有人都可以访问
        //参数为localhost表示本机访问

        //禁止谁能访问
        initParameters.put("maplef","192.168.1.1");
        //这个ip地址被禁止访问

        bean.setInitParameters(initParameters); //设置初始化参数

        return bean;
    }
```

配置完毕，即可访问：http://localhost:8080/druid/login.html



# 整合MyBatis

springboot中有两种整合myBatis的方式

## 1.采用Spring整合MyBatis方法

1. 引入依赖

   ```xml
   <!--引入依赖-->
   <dependency>
       <groupId>org.mybatis</groupId>
       <artifactId>mybatis</artifactId>
       <version>3.5.7</version>
   </dependency>
   <dependency>
       <groupId>org.mybatis</groupId>
       <artifactId>mybatis-spring</artifactId>
       <version>2.0.5</version>
   </dependency>
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-data-jdbc</artifactId>
       <version>2.5.1</version>
   </dependency>
   ```

   

2. 配置数据源

   由于引入了`spring-boot-starter-data-jdbc`，它已经自动在springBoot中配置了数据源，只要提供数据源配置的属性

   ```properties
   #配置数据源属性
   spring.datasource.driver-class-name=com.mysql.jdbc.Driver
   spring.datasource.url=jdbc:mysql://localhost:3306/crm
   spring.datasource.username=root
   spring.datasource.password=
   ```

   

3. 配置SqlSessionFactoryBean

   由于SpringBoot中没用XML文件，在配置类中配置SqlSessionFactoryBean

   ```java
   @Configuration
   public class SqlSessionFactoryConfig {
   
       //注入数据源
       @Autowired
       private DataSource dataSource;
   
       //注入SqlSessionFactoryBean组件
       @Bean
       public SqlSessionFactory sqlSessionFactoryBean() throws Exception {
           //创建SqlSessionFactoryBean组件
           SqlSessionFactoryBean sfb = new SqlSessionFactoryBean();
   
           //配置数据源
           sfb.setDataSource(dataSource);
   
           //配置别名
           sfb.setTypeAliasesPackage("com.maplef.entity");
   
           return sfb.getObject();
       }
   
   }
   ```

   

4. 配置MapperScannerConfigurer

   ```java
   @Configuration
   public class MapperScannerConfig {
   
       /*
       注入Mapper扫描组件
        */
       @Bean
       public MapperScannerConfigurer mapperScannerConfigurer(){
           MapperScannerConfigurer msc = new MapperScannerConfigurer();
           msc.setSqlSessionFactoryBeanName("sqlSessionFactoryBean");
   
           //配置Mapper扫描路径
           msc.setBasePackage("com.maplef.dao");
   
           return msc;
       }
   
   }
   ```

   

5. 实现三层操作并运行......

## 2.采用SpringBoot场景整合

1. 整合包：mybatis-spring-boot-starter

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.4</version>
</dependency>
```

2. 配置连接数据库信息同JDBC一样

   ```yaml
   spring:
     datasource:
       username: root
       password: 
       #?serverTimezone=UTC解决时区的报错
       url: jdbc:mysql://localhost:3306/smbms?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
       type: com.alibaba.druid.pool.DruidDataSource
   
       #Spring Boot 默认是不注入这些属性值的，需要自己绑定
       #druid 数据源专有配置
       initialSize: 5
       minIdle: 5
       maxActive: 20
       maxWait: 60000
       timeBetweenEvictionRunsMillis: 60000
       minEvictableIdleTimeMillis: 300000
       validationQuery: SELECT 1 FROM DUAL
       testWhileIdle: true
       testOnBorrow: false
       testOnReturn: false
       poolPreparedStatements: true
   
       #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
       #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
       #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
       filters: stat,wall,log4j
       maxPoolPreparedStatementPerConnectionSize: 20
       useGlobalDataSourceStat: true
       connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
   ```

3. 配置mybatis信息

   ```properties
   # 整合mybatis
   # 实体类位置
   mybatis.type-aliases-package=com.maplef.pojo
   # dao层对应的mybatis接口的位置
   mybatis.mapper-locations=classpath:mybatis/mapper/*.xml
   ```

   

4. 配置实体类

5. 创建mapper目录，与对应实体类的Mapper接口

   ```java
   //注解表示这是一个mybatis的mapper类
   @Mapper
   @Repository
   public interface UserMapper {
   
       List<SmbmsUser> queryUserList();
   
       SmbmsUser queryUserById(Integer id);
   
   }
   ```

   

6. 对应的Mapper.xml文件，SpringBoot中，xml配置文件存放在resources路径下。一般情况下，我们在其中单独创建mybatis/mapper文件夹,再在其中存放xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.maplef.mapper.UserMapper">
       <select id="queryUserList" resultType="com.maplef.pojo.SmbmsUser">
           select * from smbms_user
       </select>
       <select id="queryUserById" resultType="com.maplef.pojo.SmbmsUser">
           select * from smbms_user where id = #{id}
       </select>
   </mapper>
   ```

7. 使用Controller层进行测试

   ```java
   @Controller
   public class SmbmsUserController {
   
       @Autowired
       private UserMapper userMapper;
   
       @RequestMapping("/queryList")
       @ResponseBody
       public List<SmbmsUser> queryUserList(){
           List<SmbmsUser> smbmsUsers = userMapper.queryUserList();
           return smbmsUsers;
       }
   
   }
   ```

   

# Spring Security环境

### Spring Security是什么

Spring Security是一个功能强大且高度可定制的身份验证和访问控制框架。它实际上是保护基于spring的应用程序的标准。

Spring Security是一个框架，侧重于为Java应用程序提供身份验证和授权。与所有Spring项目一样，Spring安全性的真正强大之处在于它可以轻松地扩展以满足定制需求

Spring 是一个非常流行和成功的 Java 应用开发框架。Spring Security 基于 Spring 框架，提供了一套 Web 应用安全性的完整解决方案。一般来说，Web 应用的安全性包括用户认证（Authentication）和用户授权（Authorization）两个部分。用户认证指的是验证某个用户是否为系统中的合法主体，也就是说用户能否访问该系统。用户认证一般要求用户提供用户名和密码。系统通过校验用户名和密码来完成认证过程。用户授权指的是验证某个用户是否有权限执行某个操作。在一个系统中，不同用户所具有的权限是不同的。比如对一个文件来说，有的用户只能进行读取，而有的用户可以进行修改。一般来说，系统会为不同的用户分配不同的角色，而每个角色则对应一系列的权限。

对于上面提到的两种应用情景，Spring Security 框架都有很好的支持。在用户认证方面，Spring Security 框架支持主流的认证方式，包括 HTTP 基本认证、HTTP 表单验证、HTTP 摘要认证、OpenID 和 LDAP 等。在用户授权方面，Spring Security 提供了基于角色的访问控制和访问控制列表（Access Control List，ACL），可以对应用中的领域对象进行细粒度的控制。

### 使用方法

1. Spring Security是针对Spring项目的安全框架，它的主要目的是“认证”和“授权”

   **“认证”（Authentication）**

   身份验证是关于验证您的凭据，如用户名/用户ID和密码，以验证您的身份。

   身份验证通常通过用户名和密码完成，有时与身份验证因素结合使用。

    **“授权” （Authorization）**

   授权发生在系统成功验证您的身份后，最终会授予您访问资源（如信息，文件，数据库，资金，位置，几乎任何内容）的完全权限。

   主要记住以下3个类

   - WebSecurityConfigurerAdapter：自定义Security策略
   - AuthenticationManagerBuilder：自定义认证策略
   - @EnableWebSecurity：开启WebSecurity模式

2. 导入对应的包

```xml
<!--spring_security-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

3. Spring Security测试环境页面设置

   ![QQ截图20210509230236](\assets\QQ截图20210509230236.png)有如下的页面

   **index：首页，用于查看与跳转level1-3中的页面内容**

   **login：登录页面**

4. 配置Spring Security内容

   创建一个config配置

   ```java
   @EnableWebSecurity // 开启WebSecurity模式
   public class SecurityConfig extends WebSecurityConfigurerAdapter {
   
      @Override
      protected void configure(HttpSecurity http) throws Exception {
          //这里面我们可以定制请求的授权规则
          //它采用链式编程
          //设置拦截
          //.antMatchers("/").permitAll()
          //	这个路径的内容会被公开(.permitAll()公开这个页面)
          //.antMatchers("/level1/**").hasRole("vip1")
          //	/level1下的所有资源只有账号权限为vip1的用户才能访问   
          http.authorizeRequests().antMatchers("/").permitAll()
   .antMatchers("/level1/**").hasRole("vip1")
   .antMatchers("/level2/**").hasRole("vip2")
   .antMatchers("/level3/**").hasRole("vip3");
           //没有权限,默认回到登录页
   
           // 开启自动配置的登录功能
           // /login 请求来到登录页
           // /login?error 重定向到这里表示登录失败
           http.formLogin();
   
           //注销,注销后回到首页
           http.logout().logoutSuccessUrl("/");
     }
       
       //认证
       //在spring Secutiry 5.0+后,新增了很多的加满方式
       //它认为明文密码不安全,进行了限制
       @Override
       protected void configure(AuthenticationManagerBuilder auth) throws Exception {
           //当前测试我们明码编写几个账号,正常都是从数据库拿取
           //设置登录账户以及它们的权限
           auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
               .withUser("maplef").password(new BCryptPasswordEncoder().encode("123456")).roles("vip2","vip3").and()
               .withUser("root").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1","vip2","vip3").and()
               .withUser("guest").password(new BCryptPasswordEncoder().encode("123456")).roles("vip1");
       }
       
   }
   
   ```

   配置完以上内容后，我们没有权限访问的时候会回到登录页面

   ```html
   <a class="item" th:href="@{/logout}">
      <i class="address card icon"></i> 注销
   </a>
   <!--点击这个超链接即可访问到:http.logout().logoutSuccessUrl("/");
   于是我们进行注销操作并回到首页
   -->
   ```

   以上就是Spring Security的一些简单应用

5. 记住我功能

   - 开启记住我功能

     ```java
     //定制请求的授权规则
     @Override
     protected void configure(HttpSecurity http) throws Exception {
     //。。。。。。。。。。。
        //记住我
        http.rememberMe();
     }
     ```

   - 启动项目后即可发现登录页出现一个记住我功能，关闭游览器后重新访问，账号依旧存在。

   - 使用这个功能Spring Security会将账号保持到cookie，点击注销后它也会自动删除cookie

# Shiro

1. Apache Shiro 是一个java的安全框架
2. Shiro 可以非常容易的开发出足够好的应用,在JavaSE与JavaEE环境中均可使用
3. Shiro可以完成,认证,授权,加满,会话管理,Web集成,缓存等

## 使用shiro

1. 导入依赖

   ```xml
   	<dependency>
               <groupId>org.apache.shiro</groupId>
               <artifactId>shiro-core</artifactId>
               <version>1.7.1</version>
       </dependency>
   ```

   

2. 导入shiro.ini配置文件

3. Quickstart



shiro三大核心对象

- Subject	用户
- SecurityManager  管理所有用户
- Realm   连接数据



### Spring整合Shiro

1. 导入依赖	

   ```java
   <!--shiro整合spring的包-->
           <dependency>
               <groupId>org.apache.shiro</groupId>
               <artifactId>shiro-spring</artifactId>
               <version>1.7.1</version>
           </dependency>
   ```

   

2. 要使用shiro,还需要两个配置类![image-20210605165018400](\assets\image-20210605165018400.png)

3. `UserRealm`:

   ```java
   package com.maplef.config;
   
   import org.apache.shiro.authc.AuthenticationException;
   import org.apache.shiro.authc.AuthenticationInfo;
   import org.apache.shiro.authc.AuthenticationToken;
   import org.apache.shiro.authz.AuthorizationInfo;
   import org.apache.shiro.realm.AuthorizingRealm;
   import org.apache.shiro.subject.PrincipalCollection;
   
   //自定义的RsuerRealm
   public class UserRealm extends AuthorizingRealm {
       //授权
       @Override
       protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
           System.out.println("执行了=>授权doGetAuthorizationInfo");
           return null;
       }
   
       //认证
       @Override
       protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
           System.out.println("执行了=>认证doGetAuthenticationInfo");
           return null;
       }
   }
   ```

   

4. `ShiroConfig`

   ```java
   package com.maplef.config;
   
   import org.apache.shiro.spring.web.ShiroFilterFactoryBean;
   import org.apache.shiro.web.mgt.DefaultWebSecurityManager;
   import org.springframework.beans.factory.annotation.Qualifier;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   
   @Configuration
   public class ShiroConfig {
   
   
       //ShiroFilterFactoryBean
       @Bean
       public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("defaultWebSecurityManager") DefaultWebSecurityManager defaultWebSecurityManager){
           ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
           //设置安全管理器
           bean.setSecurityManager(defaultWebSecurityManager);
           return bean;
       }
   
       //DefaultWebSecurityManager
       @Bean
       public DefaultWebSecurityManager defaultWebSecurityManager(@Qualifier("userRealm") UserRealm userRealm){
           DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
           //关联UserRealm
           securityManager.setRealm(userRealm);
           return securityManager;
   
       }
   
       //创建 realm 对象 需要自定义
       @Bean
       public UserRealm userRealm(){
           return new UserRealm();
       }
   
   }
   ```

   

### 登陆拦截测试使用

### Shiro页面拦截

1. 搭建测试环境

controller类

```java
//主页
@RequestMapping({"/","/index"})
public String toIndex(Model model){
    model.addAttribute("msg","hello,world");
    return "index";
}

//添加页面
@RequestMapping("/add")
public String add(){
    return "user/add";
}

//修改页面
@RequestMapping("/update")
public String update(){
    return "user/update";
}

//登录页面
@RequestMapping("/toLogin")
public String toLogin(){
    return "login";
}
```





页面![image-20210605171406520](\assets\image-20210605171406520.png)

登录页代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>登录</title>
</head>
<body>
<h1>登录</h1>
<hr>
<form action="">
    <p>用户名: <input type="text" name="userName"></p>
    <p>密码: <input type="password" name="userPwd"></p>
    <p><input type="submit"/> </p>
</form>
</body>
</html>
```

首页代码

```html

<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>首页</title>
</head>
<body>
    <h1>首页</h1>
    <p th:text="${msg}"></p>
<hr>
<a th:href="@{/add}">添加</a>   |   <a th:href="@{/update}">修改</a>
</body>
</html>
<!--现在,我们可以在首页跳转到add页面和update页面-->
<!--我们要使用shiro,设置两个页面的权限,只有特定用户才可以访问到特定的页面-->
```



配置环境设置完成，现在来进行shiro的配置

在`ShiroConfig`这个类中的`getShiroFilterFactoryBean`方法中编写拦截设置

```java
@Bean
public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("defaultWebSecurityManager") DefaultWebSecurityManager defaultWebSecurityManager){
    ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
    //设置安全管理器
    bean.setSecurityManager(defaultWebSecurityManager);


    //添加shiro的内置过滤器
    /*
            anon:无需认证即可访问
            authc: 必须认证了才能访问
            user: 必须拥有记住我功能才能使用
            perms: 拥有对某个资源的权限才能访问
            role: 拥有某个角色权限才能访问
         */
    Map<String, String> filterMap = new LinkedHashMap<>();

    //将所有需要被shiro管理的页面路径,与过滤方式放置在map集合中
    filterMap.put("/add","authc");
    filterMap.put("/update","authc");

    //再将map集合给到这个方法,shiro即可对设置过的页面进行过滤
    bean.setFilterChainDefinitionMap(filterMap);

    //设置登录页面的路径
    bean.setLoginUrl("/toLogin");

    return bean;
}
```

shiro配置成功,现在进行测试

<img src="\assets\image-20210605172447173.png" alt="image-20210605172447173" style="zoom:80%;" />点击修改或添加后即可发现

<img src="\assets\image-20210605172602888.png" alt="image-20210605172602888" style="zoom:80%;" />shiro对这两个路径进行拦截

#### shiro的内置过滤方式

```
anon:无需认证即可访问
authc: 必须认证了才能访问
user: 必须拥有记住我功能才能使用
perms: 拥有对某个资源的权限才能访问
role: 拥有某个角色权限才能访问
```

### Shiro用户认证

接着上面的项目,在controller中增加一个登录的方法

```java
//登录方法
@RequestMapping("/login")
public String login(String userName,String userPwd,Model model){
    //获取当前用户,注意,这里需要导Shiro的包
    Subject subject = SecurityUtils.getSubject();

    //封装用户的登录数据
    UsernamePasswordToken token = new UsernamePasswordToken(userName, userPwd);

    try {
        subject.login(token);//执行登录的方法,如果没有异常,说明没有问题
        return "index"; //登录成功,返回首页
    } catch (UnknownAccountException e) {   //用户名不存在
        model.addAttribute("msg","用户名错误");
        return "login";
    } catch (IncorrectCredentialsException e){  //密码不存在
        model.addAttribute("msg","密码错误");
        return "login";
    }
}
```

在`UserRealm`这个类中

```java
//认证
@Override
protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
    System.out.println("执行了=>认证doGetAuthenticationInfo");

    //账户与密码应该在数据库拿取,这里l
    //认证用户名和密码
    String userName = "root";
    String userPwd = "123456";

    UsernamePasswordToken userToken = (UsernamePasswordToken)token;

    if (!userToken.getUsername().equals(userName)){
        return null;    //抛出异常  UnknownAccountException
    }

    //不需要手动密码认证,shiro自己去做了
    return new SimpleAuthenticationInfo("",userPwd,"");

}
```

运行效果:

<img src="\assets\image-20210605222608465.png" alt="image-20210605222608465" style="zoom:80%;" /><img src="\assets\image-20210605222622628.png" alt="image-20210605222622628" style="zoom:80%;" />

![image-20210605222724678](\assets\image-20210605222724678.png)![image-20210605222731506](\assets\image-20210605222731506.png)

### Shiro搭配Mybatis

我们需要先导入mybatis相关的依赖及配置，[这里跳转至整合MyBatis](#整合MyBatis)

编写一整套数据访问流程出来。

随后修改UserRealm的内容

```java
//自定义的RsuerRealm
public class UserRealm extends AuthorizingRealm {

    @Autowired
    private SmbmsUserService smbmsUserService;

    //省略授权方法

    //认证
    @Override
    protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
        System.out.println("执行了=>认证doGetAuthenticationInfo");



        UsernamePasswordToken userToken = (UsernamePasswordToken)token;
        //连接真实数据库
        //通过获取到的用户名去数据库查看信息
        SmbmsUser smbmsUser = smbmsUserService.querUserByName(userToken.getUsername());

        if (smbmsUser==null){
            //如果用户为空,证明没有这个账户
            return null;
        }

        //不需要手动密码认证,shiro自己去做了
        return new SimpleAuthenticationInfo("",smbmsUser.getUserPassword(),"");

    }
}
```

shiro可以进行的密码加密操作：

- MD5加密
- MD5盐值加密

### Shiro请求授权

前面的测试，只是进行了简单的拦截操作，并没有对权限进行管理

下面开始测试用户权限的管理

首先，`ShiroConfig`类设置页面的访问权限

```java
@Bean
public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("defaultWebSecurityManager") DefaultWebSecurityManager defaultWebSecurityManager){
    ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
    //设置安全管理器
    bean.setSecurityManager(defaultWebSecurityManager);
    //拦截
    Map<String, String> filterMap = new LinkedHashMap<>();

    //授权,正常的情况下,没有授权会跳转到未授权页面
    filterMap.put("/add","perms[user:add]");    
    //所有的用户,必须拥有user:add这个权限才能访问add页面
    filterMap.put("/update","authc");
    bean.setFilterChainDefinitionMap(filterMap);

    //未登录时跳转到哪里
    bean.setLoginUrl("/toLogin");
    //用户访问未授权后跳转到哪里
    bean.setUnauthorizedUrl("/noauth");

    return bean;
}
```

未授权时访问的页面

```java
@RequestMapping("/noauth")
@ResponseBody
public String unauthorized(){
    return "未经授权,无法访问此页面";
}
```

然后在`UserRealm`类中对用户的权限进行操作

```java
//授权
@Override
protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
    System.out.println("执行了=>授权doGetAuthorizationInfo");

    SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();

    //给用户增加user:add这个字符串,表示权限
    //这种硬编码方式并不推荐使用,一般正常的业务都是从数据库拿取访问权限
    info.addStringPermission("user:add");

    //拿到当前登录这个对象
    Subject subject = SecurityUtils.getSubject();
    SmbmsUser currentUser = (SmbmsUser) subject.getPrincipal(); 
    //通过认证方法的最后一行,这里可以拿到用户的对象

    //从数据库拿取权限,并设置当前用户的权限
    info.addStringPermission(currentUser.getUserRole().toString());

    return info;
}
```

用户对象是通过认证方法`return new SimpleAuthenticationInfo(smbmsUser,smbmsUser.getUserPassword(),"");`这一行代码中的smbmsUser(用户类)传输出去的

通过这种方式，对页面的访问权限进行设置。

## Shiro整合Thymeleaf

1. 首先导入整合包

   ```xml
   <!--shiro整合thymeleaf包-->
   <dependency>
       <groupId>com.github.theborakompanioni</groupId>
       <artifactId>thymeleaf-extras-shiro</artifactId>
       <version>2.0.0</version>
   </dependency>
   ```

2. 配置——在ShiroConfig中添加新的方法

   ```java
   //整合ShiroDialect:用来整合shir和thymeleaf
   @Bean
   public ShiroDialect getShiroDialect(){
       return new ShiroDialect();
   }
   ```

3. 前端页面中要导入新的命名空间

   ```html
   xmlns:shiro="http://www.pollix.at/thymeleaf/shiro"
   ```

4. 页面功能

   ```html
   <!--表示只有拥有这个user:add权限的人才会显示其中的a标签-->
   <div shiro:hasPermission="user:add">
       <a th:href="@{/add}">添加</a>
   </div>
   <!--这里同理-->
   <div shiro:hasPermission="user:update">
       <a th:href="@{/update}">修改</a>
   </div>
   
   <!--表示没有任何权限时显示,一般用于显示隐藏登录按钮等-->
   <div shiro:notAuthenticated="">
       <a th:href="@{/update}">登录</a>
   </div>
   
   ```



## 小结

1. 未学习shiro的加密
2. 未了解注销操作
3. 未了解底层



# Swagger

官网：https://swagger.io/

- **前后端分离**

  - 前端 -> 前端控制层、视图层
  - 后端 -> 后端控制层、服务层、数据访问层
  - 前后端通过API进行交互
  - 前后端相对独立且松耦合

  **产生的问题**

  - 前后端集成，前端或者后端无法做到“及时协商，尽早解决”，最终导致问题集中爆发

  **解决方案**

  - 首先定义schema [ 计划的提纲 ]，并实时跟踪最新的API，降低集成风险

  **Swagger**

  - 号称世界上最流行的API框架
  - Restful Api 文档在线自动生成器 => **API 文档 与API 定义同步更新**
  - 直接运行，在线测试API
  - 支持多种语言 （如：Java，PHP等）
  - 官网：https://swagger.io/



## SpringBoot集成

1. 新建一个SpingBoot项目

2. 导入依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
   <dependency>
       <groupId>io.springfox</groupId>
       <artifactId>springfox-swagger2</artifactId>
       <version>2.9.2</version>
   </dependency>
   <dependency>
       <groupId>io.springfox</groupId>
       <artifactId>springfox-swagger-ui</artifactId>
       <version>2.9.2</version>
   </dependency>
   
   ```

3. 一个能运行的helloworld类

4. 配置Swagger ==> Config

   ```java
   @Configuration
   @EnableSwagger2 //开启Swagger2
   public class SwaggerConfig {
   }
   //什么都不做,使用默认值
   ```

   

5. 启动项目访问http://localhost:8080/swagger-ui.html

   ![image-20210606172916588](\assets\image-20210606172916588.png)

## Swagger配置

Swagger的bean实例Docket

```java
@Configuration
@EnableSwagger2 //开启Swagger2
public class SwaggerConfig {


    //配置了Swagger Docket的bean实例
    @Bean
    public Docket docket(){
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo());
    }

    //配置Swagger信息=apiInfo
    private ApiInfo apiInfo(){
        Contact contact = new Contact
                ("肖峰", "www.baidu.com","1371730063@qq.com");

        return new ApiInfo(
                "Maplef的SwaggerAPI测试",
                "啊吧啊吧啊吧",
                "v1.0",
                "https://baidu.com/",
                contact,
                "Apach 2.0",
                "www.baidu.com",
                new ArrayList()
        );
    }
}
```

运行效果:

![image-20210606180111760](\assets\image-20210606180111760.png)



Swagger配置扫描接口

```java
@Bean
public Docket docket(){
    return new Docket(DocumentationType.SWAGGER_2)
        .apiInfo(apiInfo())
        //.enable(false)    是否启用Swagger,为false则不启动
        .select()
        //RequestHandlerSelectors   配置要扫描接口的方式
        //basePackage("包路径")   指定要扫描的包
        //.any()    扫描所有，项目中的所有接口都会被扫描到
        //.none()   不扫描
        // withMethodAnnotation(GetMapping.class)通过方法上的注解扫描,只扫描get请求
		//withClassAnnotation(Controller.class)通过类上的注解扫描,只扫描有controller注解的类中的接口
        .apis(RequestHandlerSelectors.basePackage("com.maplef.controller"))
        //paths()   过滤什么路径
        //.paths(PathSelectors.ant("/maplef/**"))
        .build();
}
```

> 配置Swagger开关

通过enable()方法配置是否启用swagger，如果是false，swagger将不能在浏览器中访问了

```java
@Bean
public Docket docket() {
   return new Docket(DocumentationType.SWAGGER_2)
      .apiInfo(apiInfo())
      .enable(false) //配置是否启用Swagger，如果是false，在浏览器将无法访问
      .select()// 通过.select()方法，去配置扫描接口,RequestHandlerSelectors配置如何扫描接口
      .apis(RequestHandlerSelectors.basePackage("com.kuang.swagger.controller"))
       // 配置如何通过path过滤,即这里只扫描请求以/kuang开头的接口
      .paths(PathSelectors.ant("/kuang/**"))
      .build();
}
```

动态配置

```java
@Bean
public Docket docket(Environment environment) {
   // 设置要显示swagger的环境
   Profiles of = Profiles.of("dev", "test");
   // 判断当前是否处于该环境
   // 通过 enable() 接收此参数判断是否要显示
   boolean b = environment.acceptsProfiles(of);
   
   return new Docket(DocumentationType.SWAGGER_2)
      .apiInfo(apiInfo())
      .enable(b) //配置是否启用Swagger，如果是false，在浏览器将无法访问
      .select()// 通过.select()方法，去配置扫描接口,RequestHandlerSelectors配置如何扫描接口
      .apis(RequestHandlerSelectors.basePackage("com.kuang.swagger.controller"))
       // 配置如何通过path过滤,即这里只扫描请求以/kuang开头的接口
      .paths(PathSelectors.ant("/kuang/**"))
      .build();
}
```



配置API文档的分组

```java
@Bean
public Docket docket(Environment environment) {
   return new Docket(DocumentationType.SWAGGER_2).apiInfo(apiInfo())
      .groupName("hello") // 配置分组
       // 省略配置....
}
```

配置多个分组，创建多个Docket实例即可

```java
public Docket docket1(){
    return new Docket(DocumentationType.SWAGGER_2).groupName("A");
}
public Docket docket2(){
    return new Docket(DocumentationType.SWAGGER_2).groupName("B");
}
public Docket docket3(){
    return new Docket(DocumentationType.SWAGGER_2).groupName("C");
}
```

> 实体类配置:

一个新的实体类

```java
//@Api(注释)
@ApiModel("用户实体类")
public calss User {
    @ApiModelProperty("用户名")
    private String username;
    @ApiModelProperty("密码")
    private String password;
    
    //省略get/set方法
}
```

只要实体类在请求接口的返回值上，都能映射到实体项中

```java
@RequestMapping("/getUser")
public User getUser(){
   return new User();
}
```

> ### 常用注解

Swagger的所有注解定义在io.swagger.annotations包下

下面列一些经常用到的，未列举出来的可以另行查阅说明：

| Swagger注解                                            | 简单说明                                             |
| ------------------------------------------------------ | ---------------------------------------------------- |
| @Api(tags = "xxx模块说明")                             | 作用在模块类上                                       |
| @ApiOperation("xxx接口说明")                           | 作用在接口方法上                                     |
| @ApiModel("xxxPOJO说明")                               | 作用在模型类上：如VO、BO                             |
| @ApiModelProperty(value = "xxx属性说明",hidden = true) | 作用在类方法和属性上，hidden设置为true可以隐藏该属性 |
| @ApiParam("xxx参数说明")                               | 作用在参数、方法和字段上，                           |

我们也可以给请求的接口配置一些注释

```
@ApiOperation("Maplef的接口")
@PostMapping("/maplef")
@ResponseBody
public String kuang(@ApiParam("这个名字会被返回")String username){
   return username;
}
```

这样的话，可以给一些比较难理解的属性或者接口，增加一些配置信息，让人更容易阅读！

相较于传统的Postman或Curl方式测试接口，使用swagger简直就是傻瓜式操作，不需要额外说明文档(写得好本身就是文档)而且更不容易出错，只需要录入数据然后点击Execute，如果再配合自动化框架，可以说基本就不需要人为操作了。

Swagger是个优秀的工具，现在国内已经有很多的中小型互联网公司都在使用它，相较于传统的要先出Word接口文档再测试的方式，显然这样也更符合现在的快速迭代开发行情。在正式环境要记得关闭Swagger，一来出于安全考虑二来也可以节省运行时内存。





# 任务

## 异步任务

现在,在项目中有这么一个功能:

```java
    public void hello(){

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("数据处理中");

    }
//它需要等待3s才能往下执行


//直接在controller中调用这个方法
    @RequestMapping("/hello")
    public String hello(){

        asyncService.hello();
        return "ok";
    }
```

运行查看效果

![image-20210607143912093](\assets\image-20210607143912093.png)访问这个方法，因为睡眠的原因，转了3s的圈，用户体验极差

使用异步即可解决这个问题

```java
    //在方法上加上@Async注解
	//告诉Spring,这是一个异步的方法
    @Async
    public void hello(){

        try {
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("数据处理中");

    }

	//在启动类上开启异步功能
    @EnableAsync
    @SpringBootApplication
    public class Springboot09TestApplication {

        public static void main(String[] args) {
            SpringApplication.run(Springboot09TestApplication.class, args);
        }

    }
```

再次运行,页面直接加载出来，不会去等待方法的3s睡眠时间





## 定时任务

```java
TaskScheduler	任务调度者
TaskExecutor	任务执行者
    
@EnableScheduling   //开启定时功能的注解,放在主启动类上
@Scheduled			//什么时候执行,放在需要执行的方法上
    
Cron表达式
```

测试使用

```java
    //在一个特定的时间执行这个方法

    //cron 表达式
    //秒 分   时   日   月   周几
	//在每个月的,每天18点35分0秒执行一次
    @Scheduled(cron = "0 35 18 * * ?")
    public void hello(){
        System.out.println("hello,你被执行了");
    }
```

**cron建议还是百度,现用现查**





## 邮件发送

使用邮件功能，首先导入启动器

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

在QQ邮箱中的设置->账户->开启pop3和smtp服务

![image-20210607152623727](\assets\image-20210607152623727.png)

配置发送邮箱

```properties
spring.mail.username=137173006@qq.com
spring.mail.password=授权码,qq邮箱那边给的
spring.mail.host=smtp.qq.com
# 开启加密验证
spring.mail.properties.mail.smtl.ssl.enable=true
```

一个测试类

```java
    @Autowired
    JavaMailSenderImpl mailSender;

    @Test
    void contextLoads() {

        //发送一封简单的邮件
        SimpleMailMessage mailMessage = new SimpleMailMessage();

        mailMessage.setSubject("邮件主体");
        mailMessage.setText("文本内容");

        mailMessage.setTo("发送给谁,邮箱号");
        mailMessage.setFrom("接收邮箱,邮箱号");


        mailSender.send(mailMessage);

    }
```

复杂的邮件

```java
    @Test
    void contextLoads2() throws MessagingException {

        //发送一封复杂的邮件
        MimeMessage mimeMessage = mailSender.createMimeMessage();
        //组装
        MimeMessageHelper helper = new MimeMessageHelper(mimeMessage);

        helper.setSubject("邮件主题");
        //编写html代码,文字特效等
        helper.setText("<p style='color:red'>html标签内容</p>",true);

        //发送附件
        helper.addAttachment("1.jpg",new File("文件路径"));

        helper.setTo("发送给谁,邮箱号");
        helper.setFrom("接收邮箱,邮箱号");

        mailSender.send(mimeMessage);

    }
```

在正式的项目中使用，可以把参数设置为实体类，传输数据进入方法动态生成邮件





# 分布式

在《分布式系统原理与范型》一书中有如下定义：“分布式系统是若干独立计算机的集合，这些计算机对于用户来说就像单个相关系统”；

分布式系统是由一组通过网络进行通信、为了完成共同的任务而协调工作的计算机节点组成的系统。分布式系统的出现是为了用廉价的、普通的机器完成单个计算机无法完成的计算、存储任务。其目的是**利用更多的机器，处理更多的数据**。

分布式系统（distributed system）是建立在网络之上的软件系统。

首先需要明确的是，只有当单个节点的处理能力无法满足日益增长的计算、存储任务的时候，且硬件的提升（加内存、加磁盘、使用更好的CPU）高昂到得不偿失的时候，应用程序也不能进一步优化的时候，我们才需要考虑分布式系统。因为，分布式系统要解决的问题本身就是和单机系统一样的，而由于分布式系统多节点、通过网络通信的拓扑结构，会引入很多单机系统没有的问题，为了解决这些问题又会引入更多的机制、协议，带来更多的问题。。。

## Dubbo文档

随着互联网的发展，网站应用的规模不断扩大，常规的垂直应用架构已无法应对，分布式服务架构以及流动计算架构势在必行，急需**一个治理系统**确保架构有条不紊的演进。

在Dubbo的官网文档有这样一张图

![image-20210701004135164](\assets\image-20210701004135164.png)

> 单一应用架构

当网站流量很小时，只需一个应用，将所有功能都部署在一起，以减少部署节点和成本。此时，用于简化增删改查工作量的数据访问框架(ORM)是关键。

![image-20210701004211345](\assets\image-20210701004211345.png)

适用于小型网站，小型管理系统，将所有功能都部署到一个功能里，简单易用。

**缺点：**

1、性能扩展比较难

2、协同开发问题

3、不利于升级维护

> 垂直应用架构

当访问量逐渐增大，单一应用增加机器带来的加速度越来越小，将应用拆成互不相干的几个应用，以提升效率。此时，用于加速前端页面开发的Web框架(MVC)是关键。

![image-20210701004246892](\assets\image-20210701004246892.png)

通过切分业务来实现各个模块独立部署，降低了维护和部署的难度，团队各司其职更易管理，性能扩展也更方便，更有针对性。

缺点：公用模块无法重复利用，开发性的浪费

> 分布式服务架构

当垂直应用越来越多，应用之间交互不可避免，将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求。此时，用于提高业务复用及整合的**分布式服务框架(RPC)**是关键。

![image-20210701004309883](\assets\image-20210701004309883.png)

> 流动计算架构

当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于**提高机器利用率的资源调度和治理中心**(SOA)[ Service Oriented Architecture]是关键。

![image-20210701004332278](\assets\image-20210701004332278.png)



## RPC是什么

RPC【Remote Procedure Call】是指远程过程调用，是一种进程间通信方式，他是一种技术的思想，而不是规范。它允许程序调用另一个地址空间（通常是共享网络的另一台机器上）的过程或函数，而不用程序员显式编码这个远程调用的细节。即程序员无论是调用本地的还是远程的函数，本质上编写的调用代码基本相同。

也就是说两台服务器A，B，一个应用部署在A服务器上，想要调用B服务器上应用提供的函数/方法，由于不在一个内存空间，不能直接调用，需要通过网络来表达调用的语义和传达调用的数据。为什么要用RPC呢？就是无法在一个进程内，甚至一个计算机内通过本地调用的方式完成的需求，比如不同的系统间的通讯，甚至不同的组织间的通讯，由于计算能力需要横向扩展，需要在多台机器组成的集群上部署应用。RPC就是要像调用本地的函数一样去调远程函数；

推荐阅读文章：https://www.jianshu.com/p/2accc2840a1b

### RPC基本原理

![image-20210701004415977](\assets\image-20210701004415977.png)

**步骤解析:**

![image-20210701004436316](\assets\image-20210701004436316.png)

RPC两个核心模块：通讯，序列化。



## Dubbo与Zookeeper安装

### Dubbo

Apache Dubbo |ˈdʌbəʊ| 是一款高性能、轻量级的开源Java RPC框架，它提供了三大核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现。

Zookeeper官网：https://zookeeper.apache.org/

![image-20210701004550713](\assets\image-20210701004550713.png)

**服务提供者**（Provider）：暴露服务的服务提供方，服务提供者在启动时，向注册中心注册自己提供的服务。

**服务消费者**（Consumer）：调用远程服务的服务消费方，服务消费者在启动时，向注册中心订阅自己所需的服务，服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。

**注册中心**（Registry）：注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者

**监控中心**（Monitor）：服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心

**调用关系说明**

l 服务容器负责启动，加载，运行服务提供者。

l 服务提供者在启动时，向注册中心注册自己提供的服务。

l 服务消费者在启动时，向注册中心订阅自己所需的服务。

l 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。

l 服务消费者，从提供者地址列表中，基于软负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用。

l 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心。

> Dubbo环境搭建

点进dubbo官方文档，推荐我们使用Zookeeper 注册中心

### window下安装zookeeper

在官网中下载压缩包并解压，获得以下内容：

![image-20210629000049183](\assets\image-20210629000049183.png)

在bin目录下，运行`zkServer.cmd`与`zkCleanup.sh`

可能遇到问题：闪退 !

解决方案：编辑zkServer.cmd文件末尾添加pause 。这样运行出错就不会退出，会提示错误信息，方便找到原因。

![image-20210701004723852](\assets\image-20210701004723852.png)

修改zoo.cfg配置文件

将conf文件夹下面的zoo_sample.cfg复制一份改名为zoo.cfg即可。

注意几个重要位置：

dataDir=./  临时数据存储的目录（可写相对路径）

clientPort=2181  zookeeper的端口号

修改完成后再次启动zookeeper



**使用zkCli.cmd测试**

ls /：列出zookeeper根下保存的所有节点

```
[zk: 127.0.0.1:2181(CONNECTED) 4] ls /
[zookeeper]
```

`create –e /kuangshen 123`：创建一个kuangshen节点，值为123

![image-20210701004811323](\assets\image-20210701004811323.png)

`get /kuangshen`：获取/kuangshen节点的值

![image-20210701004851797](\assets\image-20210701004851797.png)



### window下安装dubbo-admin

dubbo本身并不是一个服务软件。它其实就是一个jar包，能够帮你的java程序连接到zookeeper，并利用zookeeper消费、提供服务。

但是为了让用户更好的管理监控众多的dubbo服务，官方提供了一个可视化的监控程序dubbo-admin，不过这个监控即使不装也不影响使用。



**1、下载dubbo-admin**

地址 ：https://github.com/apache/dubbo-admin/tree/master

**2、解压进入目录**

修改 dubbo-admin\src\main\resources \application.properties 指定zookeeper地址

```properties
server.port=7001
spring.velocity.cache=false
spring.velocity.charset=UTF-8
spring.velocity.layout-url=/templates/default.vm
spring.messages.fallback-to-system-locale=false
spring.messages.basename=i18n/message
spring.root.password=root
spring.guest.password=guest

dubbo.registry.address=zookeeper://127.0.0.1:2181
```

**3、在项目目录下**打包dubbo-admin

```cmd
mvn clean package -Dmaven.test.skip=true
```

只需要`dubbo-admin`打包成功即可使用

4、执行 dubbo-admin\target 下的dubbo-admin-0.0.1-SNAPSHOT.jar

```java
java -jar dubbo-admin-0.0.1-SNAPSHOT.jar
```

【注意：zookeeper的服务一定要打开！】

执行完毕，我们去访问一下 http://localhost:7001/ ， 这时候我们需要输入登录账户和密码，我们都是默认的root-root；

登录成功后，查看界面

![image-20210701005158389](\assets\image-20210701005158389.png)

安装成功!

## SpringBoot中使用Dubbo与zookeeper

**1. 启动zookeeper ！**

**2. IDEA创建一个空项目；**

**3.创建一个模块，实现服务提供者：provider-server ， 选择web依赖即可**

**4.项目创建完毕，我们写一个服务，比如卖票的服务；**

编写接口

```java
package com.kuang.provider.service;

public interface TicketService {
   public String getTicket();
}
```

编写实现类

```java
package com.kuang.provider.service;

public class TicketServiceImpl implements TicketService {
   @Override
   public String getTicket() {
       return "《dubbo与zookeeper测试》";
  }
}
```

**5.新创建一个模块，实现服务消费者：consumer-server ， 选择web依赖即可**

**6.项目创建完毕，我们写一个服务，比如用户的服务；**

编写service

```java
package com.kuang.consumer.service;

public class UserService {
   //我们需要去拿去注册中心的服务
}
```

**需求：现在我们的用户想使用买票的服务，这要怎么弄呢 ？**

### 服务提供者

**1、将服务提供者注册到注册中心，我们需要整合Dubbo和zookeeper，所以需要导包**

**我们从dubbo官网进入github，看下方的帮助文档，找到dubbo-springboot，找到依赖包**

```xml
<!-- Dubbo Spring Boot Starter -->
<dependency>
   <groupId>org.apache.dubbo</groupId>
   <artifactId>dubbo-spring-boot-starter</artifactId>
   <version>2.7.3</version>
</dependency>    
```

**zookeeper的包我们去maven仓库下载，zkclient；**

```xml
<!-- https://mvnrepository.com/artifact/com.github.sgroschupf/zkclient -->
<dependency>
   <groupId>com.github.sgroschupf</groupId>
   <artifactId>zkclient</artifactId>
   <version>0.1</version>
</dependency>
```

**【新版的坑】zookeeper及其依赖包，解决日志冲突，还需要剔除日志依赖；**

```xml
<!-- 引入zookeeper -->
<dependency>
   <groupId>org.apache.curator</groupId>
   <artifactId>curator-framework</artifactId>
   <version>2.12.0</version>
</dependency>
<dependency>
   <groupId>org.apache.curator</groupId>
   <artifactId>curator-recipes</artifactId>
   <version>2.12.0</version>
</dependency>
<dependency>
   <groupId>org.apache.zookeeper</groupId>
   <artifactId>zookeeper</artifactId>
   <version>3.4.14</version>
   <!--排除这个slf4j-log4j12-->
   <exclusions>
       <exclusion>
           <groupId>org.slf4j</groupId>
           <artifactId>slf4j-log4j12</artifactId>
       </exclusion>
   </exclusions>
</dependency>
```

**2、在springboot配置文件中配置dubbo相关属性！**

```properties
#当前应用名字
dubbo.application.name=provider-server
#注册中心地址
dubbo.registry.address=zookeeper://127.0.0.1:2181
#扫描指定包下服务
dubbo.scan.base-packages=com.kuang.provider.service
```

**3、在service的实现类中配置服务注解，发布服务！注意导包问题**

```java
import org.apache.dubbo.config.annotation.Service;
import org.springframework.stereotype.Component;

@Service //将服务发布出去,最新版dubbo的servev被弃用,改为DubboServe
@Component //放在容器中
public class TicketServiceImpl implements TicketService {
   @Override
   public String getTicket() {
       return "《dubbo与zookeeper测试》";
  }
}
```

**逻辑理解 ：应用启动起来，dubbo就会扫描指定的包下带有@component注解的服务，将它发布在指定的注册中心中！**



### 服务消费者

**1、导入依赖，和之前的依赖一样；**

```xml
<!--dubbo-->
<!-- Dubbo Spring Boot Starter -->
<dependency>
   <groupId>org.apache.dubbo</groupId>
   <artifactId>dubbo-spring-boot-starter</artifactId>
   <version>2.7.3</version>
</dependency>
<!--zookeeper-->
<!-- https://mvnrepository.com/artifact/com.github.sgroschupf/zkclient -->
<dependency>
   <groupId>com.github.sgroschupf</groupId>
   <artifactId>zkclient</artifactId>
   <version>0.1</version>
</dependency>
<!-- 引入zookeeper -->
<dependency>
   <groupId>org.apache.curator</groupId>
   <artifactId>curator-framework</artifactId>
   <version>2.12.0</version>
</dependency>
<dependency>
   <groupId>org.apache.curator</groupId>
   <artifactId>curator-recipes</artifactId>
   <version>2.12.0</version>
</dependency>
<dependency>
   <groupId>org.apache.zookeeper</groupId>
   <artifactId>zookeeper</artifactId>
   <version>3.4.14</version>
   <!--排除这个slf4j-log4j12-->
   <exclusions>
       <exclusion>
           <groupId>org.slf4j</groupId>
           <artifactId>slf4j-log4j12</artifactId>
       </exclusion>
   </exclusions>
</dependency>
```

2、**配置参数**

```properties
#当前应用名字
dubbo.application.name=consumer-server
#注册中心地址
dubbo.registry.address=zookeeper://127.0.0.1:2181
```

**3. 本来正常步骤是需要将服务提供者的接口打包，然后用pom文件导入，我们这里使用简单的方式，直接将服务的接口拿过来，路径必须保证正确，即和服务提供者相同；**

![image-20210701005659354](\assets\image-20210701005659354.png)

**4. 完善消费者的服务类**

```java
package com.kuang.consumer.service;

import com.kuang.provider.service.TicketService;
import org.apache.dubbo.config.annotation.Reference;
import org.springframework.stereotype.Service;

@Service //注入到容器中
public class UserService {

   @Reference //远程引用指定的服务，他会按照全类名进行匹配，看谁给注册中心注册了这个全类名
   TicketService ticketService;

   public void bugTicket(){
       String ticket = ticketService.getTicket();
       System.out.println("在注册中心买到"+ticket);
  }

}
```

**5. 测试类编写；**

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class ConsumerServerApplicationTests {

   @Autowired
   UserService userService;

   @Test
   public void contextLoads() {

       userService.bugTicket();

  }

}
```



### 启动测试

**1. 开启zookeeper**

**2. 打开dubbo-admin实现监控【可以不用做】**

**3. 开启服务者**

**4. 消费者消费测试，查看结果**



小结

- 建议观看尚硅谷的SpringBoot视频了解底层，狂神视频底层讲的不是很好
- Security与Shiro两个安全框架的进阶使用
- 注解的详细功能与源码未了解



本笔记文档源自[狂神](https://space.bilibili.com/95256449?spm_id_from=333.788.b_765f7570696e666f.2)视频，跟着视频一起做的笔记





