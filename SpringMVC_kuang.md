# SpringMVC

SpringMVC：SpringMVC的执行流程

SpringMVC：SSM框架整合

## 什么是MVC？

1. 模型（dao，service）
2. 视图（jsp）
3. 控制器（servlet）

以前的开发流程：

dao -> service -> servlet



SpringMVC的特点:

1. 轻量级
2. 高效，基于请求响应的MVC框架
3. 与Spring兼容性好，无缝结合
4. 约定大于配置
5. 功能强大：RESTful，数据验证，格式化，本地化，主题等
6. 简洁灵活

## SpringMVC运行流程

1. 用户发起请求,请求进入DIspatcherServlet
2. DIspatcherServlet根据请求找到对应的映射器，再将映射器返回
3. 拿取返回的映射器去适配映射器（controller）
4. （controller）开始执行，然后返回 一个ModelAndView
5. 通过ModelAndView去配置具体的视图解析器
6. 视图解析器返回给前端调用

![QQ截图20210407232246](C:\Users\13717\Desktop\QQ截图20210407232246.png)

## SpringMVC具体使用



## RestFul风格

1. RestFul可以改变游览器URL地址资源的传输格式

原来: http://localhost:8080/login?a=1&b=2

RestFul:http://localhost:8080/login/1/2

它将url路径中的参数名省略，使用/分隔参数。某种程度上可以增强安全性

使用方式：

```java
//{a}和{b}就是参数列表中的a与b,我们的url请求过来的路径就会变成如下格式:/add/1/2

@RequestMapping("/add/{a}/{b}")
public String test1(@PathVariable int a，@PathVariable int b){
    //使用RestFul风格,接收参数时必须加上@PathVariable注解
    //能获取到a与b的数据
}

//一些常用的注解
@PostMapping  //表示只接收Post访问
@GetMapping   //表示只接收get访问
```

## 转发与重定项

在没有视图解析器的情况下

return "/index.jsp"	//表示转发

return "forward:/index.jsp" //第二种转发方式

return "redirect:/index.jsp" //重定项

在有视图解析器的情况下,重定项会无视视图解析器

## Controller层对View层参数的接收



## 乱码问题的解决

在过滤器中设置request、rsponse编码格式

```java
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        filterChain.doFilter(servletRequest, servletResponse);
    }
```

过滤器设置完后在web.xml配置文件中加载过滤器

```xml
	<filter>
        <filter-name>encoding</filter-name>
        <filter-class>com.jbit.filter.EncodingFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>encoding</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

或者直接在web.xml中配置SpringMVC的乱码过滤

```xml
	<filter>
        <filter-name>encoding</filter-name>
        <filter-class>com.jbit.filter.EncodingFilter</filter-class>
        <init-param>
        	<param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encoding</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

Tomcat乱码的解决

在tomcat根目录下的config文件中的server.xml中

找到<Connector>标签,修改如下方

```xml
    <Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443"
               URIEncoding="UTF-8"/>
```



## 前后端分离

后端部署后端,提供接口和数据

前端独立部署,负责渲染后端的数据

两者间主要通过json传输数据



## json

#### jackson依赖转换json格式使用流程

1. 导入依赖

   ```xml
   <dependency>
               <groupId>com.fasterxml.jackson.core</groupId>
               <artifactId>jackson-databind</artifactId>
               <version>2.10.2</version>
           </dependency>
   ```

2. ```java
   @RequestMapping(value = "/t1")
       @ResponseBody   //它不会走视图解析器,会直接返回一个字符串
       public String json1() throws JsonProcessingException {
           //创建ObjectMapper类,它用于转换json格式
           //jackson ObjectMapper,用于转换json格式
           ObjectMapper mapper = new ObjectMapper();
   
           User user = new User(1,"张三",20);
   
           //将数据转换为json格式
           String s = mapper.writeValueAsString(user);
           return s;
       }
   ```

3. jackson乱码问题解决

```xml
<!--在springvmc-servlet.xml中配置-->
    <!--JackSON乱码问题配置-->
    <mvc:annotation-driven>
        <mvc:message-converters register-defaults="true">
            <bean class="org.springframework.http.converter.HttpMessageConverter">
                <constructor-arg value="UTF-8"/>
            </bean>
            <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter">
                <property name="objectMapper">
                    <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean">
                        <property name="failOnEmptyBeans" value="false"/>
                    </bean>
                </property>
            </bean>
        </mvc:message-converters>
    </mvc:annotation-driven>
```





## ssm整合

创建一个完整的ssm项目的步骤

#### 导入依赖

```xml
<!--在pom.xml中导入依赖-->
<!--依赖:
            junit
            数据库驱动
            连接池
            servlet
            jsp
            mybatis
            mybatis-spring
            spring
            springmvc
    -->

    <dependencies>
        <!--junit测试-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <!--数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.40</version>
        </dependency>
        <!--数据库连接池: druid-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.1</version>
        </dependency>

        <!--servlet   jsp-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>

        <!--mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.6</version>
        </dependency>

        <!--spring-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>
    </dependencies>
```



#### 设置Maven的资源过滤

```xml
<!--在pom.xml中设置资源过滤-->
<!--静态资源导出问题-->
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```



#### 创建三层包结构

#### 创建resources包下的配置文件

##### spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--1.关联数据库配置文件-->
    <context:property-placeholder location="classpath:database.properties"/>

    <!--2.连接池
        dbcp:半自动化操作,不能自动连接
        c3p:自动化操作(自动化的加载配置文件,并且可以自动设置到对象中)
        druid:
        hikari:
    -->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="driverClassName" value="${jdbc.driver}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <!--设置连接的信息-->
    </bean>

    <!--3.sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定Mybatis的配置文件-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>

    <!--配置dao接口扫描包,动态的实现了Dao接口可以注入到Spring容器中!-->

    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!--注入 sqlSessionFactory-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
        <!--要扫描的dao包-->
        <property name="basePackage" value="com.jbit.mapper"/>
    </bean>



</beans>
```



##### spring-service.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"

       xmlns:tx="http://www.springframework.org/schema/tx" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd
       http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.3.xsd">

    <!--扫描service下的包-->
    <context:component-scan base-package="com.jbit.service"/>

<!--    &lt;!&ndash;将我们的所有业务类注入到spring,可以通过配置或者注解实现&ndash;&gt;
    <bean id="BookServiceImpl" class="com.jbit.service.BookServiceImpl">
        <property name="bookMapper" ref="bookMapper"/>
    </bean>-->

    <!--声明式事务配置-->
    <bean id="TransactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--注入数据源-->
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!--aop事务支持-->

    <!--配置增强-->
<!--    <tx:advice id="txadvice" >
        <tx:caching>
            <tx:method name="get"  read-only="true" />
            <tx:method name="add" propagation="REQUIRES_NEW"/>
            <tx:method name="update" propagation="REQUIRES_NEW"/>
            <tx:method name="insert" propagation="REQUIRES_NEW"/>
            <tx:method name="del" propagation="REQUIRES_NEW"/>
            <tx:method name="*" propagation="REQUIRES_NEW"/>
        </tx:caching>
    </tx:advice>-->

    <!--配置切点和切面-->

<!--    <aop:config proxy-target-class="true">
        &lt;!&ndash;配置切点&ndash;&gt;
        <aop:pointcut id="ps" expression="execution(* com.jbit.service..*.*(..))"/>
        &lt;!&ndash;配置切面&ndash;&gt;
        <aop:advisor advice-ref="txadvice" pointcut-ref="ps"/>
    </aop:config>-->

    <!--确定业务层的实现类是一个代理模式-->
    <aop:aspectj-autoproxy proxy-target-class="true"/>

</beans>
```

##### applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:mvc="http://www.alibaba.com/schema/stat" xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.alibaba.com/schema/stat
       http://www.alibaba.com/schema/stat.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--1.注解驱动-->
    <mvc:annotation-driven/>
    <!--2.静态资源过滤-->
    <mvc:default-servlet-handler/>
    <!--3.扫描包-->
    <context:component-scan base-package="com.jbit.controller"/>
    <!--4.视图解析器-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>


</beans>
```

##### mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    
    <!--配置数据源,交给spring去做-->
    <typeAliases>
        <package name="com.jbit.entity"/>
    </typeAliases>

    <mappers>
        <mapper class="com.jbit.mapper.BookMapper"/>
    </mappers>

</configuration>
```