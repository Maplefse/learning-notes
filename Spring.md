## 1、Spring

### 简介

spring理念:使现有的技术更加容易使用,它本身就是一个大杂烩,整合了现在的技术框架

SSH:  Struct2+Spring+Hibernate

SSM: SpringMvc+Spring+Mybatis

```xml
    <dependencies>
		<!--SpringMvc依赖-->
		<dependency>
   			<groupId>org.springframework</groupId>
    		<artifactId>spring-webmvc</artifactId>
    		<version>5.2.7.RELEASE</version>
		</dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-beans</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-expression</artifactId>
            <version>5.2.7.RELEASE</version>
        </dependency>

        <!--junit测试依赖-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
//spring的@Resource自动注入依赖
          <dependency>
            <groupId>javax.annotation</groupId>
            <artifactId>javax.annotation-api</artifactId>
            <version>1.3.2</version>
        </dependency>
```

### 优点

- Spring是一个开源的免费框架(容器)
- Spring是一个轻量级的、非入侵式的框架（表示引入Spring不会对原先代码造成任何影响）
- 控制反转（IOC）、面向切面编程（AOP）
- 支持事务的管理，对框架整合的支持



Spring Boot

​	一个快速开发的脚手架

​	基于SpringBoot可以快速的开发单个微服务

​	约定大于配置

Spring Cloud

​	SpringCloud是基于SpringBoot实现的



现在大部分公司都用SpringBoot进行快速开发,<font color="red">学习SpringBoot的前提,需要完全掌握Spring及SpringMVC!</font>

弊端:发展太久之后违背了原来的理念!配置十分繁琐



## 2、IOC理论推导

1. UserDao接口

2. UserDaoImpl实现类

3. UserService业务接口
4. UserService业务实现类

```java
/**dao层*/
public class UserDaoImpl implements UserDao {
    public void getUser() {
        System.out.println("默认获取用户数据");
    }
}

//在上方的三层架构访问顺序中,我们一般采用以下方式访问Dao层
public class UserServiceImpl implements UserService {

    private UserDao userDao = new UserDaoImpl();

    public void getUser() {
        userDao.getUser();
    }
}
//在这种情况下,当用户需要其它的要求的时候,我们就要修改DAO层的代码
//当代码体量过大时,修改代码就会特别繁琐
```

```java
/**dao层*/
public class UserDaoImpl implements UserDao {
    public void getUser() {
        System.out.println("默认获取用户数据");
    }
}

/**service层*/
public class UserServiceImpl implements UserService {
    private UserDao userDao;
    //使用set方法动态实现需求的注入
    public void setUserDao(UserDao userDao){
        this.userDao=userDao
    }
    
    public void getUser() {
        userDao.getUser();
    }
}
//在这种情况下,当用户需要变更需求,我们只需要对Dao层添加需求就好
//我们只需要在用户层动态的对需求进行访问,就不需要频繁的对Dao进行修改

public staitc void main(String[] args){
     //用户实际调用的是业务层,不需要接触dao层
        UserServiceImpl userService = new UserServiceImpl();
    	userService.setUserDao(new /*用户的需求*/)
        userService.getUser();
}
```

## 3、Spring托管对象

- 当spring配置完成之后，我们可以更进一步的优化上方的代码
- 在resource创建spring的config.xml配置文件

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
           
    <!--使用Spring来创建对象,在Spring中称为Bean
        bean=对象
        id=变量名
        class = new 的对象
        property 相当于给对象中的属性设定一个值
    -->
    <!--把Bean理解为类的代理或代言人（实际上确实是通过反射、代理来实现的），这样它就能代表类拥有该拥有的东西了-->

    <bean id="userImpl" class="com.jbit.dao.UserDaoImpl"/>
    <bean id="UserServiceImpl" class="com.jbit.service.UserServiceImpl">
        <!--ref :  引用Spring容器中创建好的对象
            value: 具体的值,基本数据类型
        -->
        <property name="userDao" ref="userImpl"/>
    </bean>
</beans>
```

- 在配置文件中对javabean进行托管，以后JavaBean都由spring进行管理
- 通过以下代码对spring托管的内容进行调用

```java
//获取Spring的上下文对象
        ApplicationContext ac = new ClassPathXmlApplicationContext("config.xml");
        //现在对象已经交由Spring进行管理,需要使用直接在spring中拿取
		//hello表示spring中bean的id值
        UserServiceImpl userServiceImpl = (UserServiceImpl)ac.getBean("UserServiceImpl");
        userServiceImpl.getUser();
```

- 使用spring对javaBean进行管理后，我们再对程序进行拓展时，只需要去修改配置文件即可让用户访问到不同的内容，大大提高了程序的可修改性

## 4、IOC创建对象的方式

1. 在配置文件加载的时候，spring容器管理的对象就已经帮我们加载了这个对象。
2. 使用无参构造创建对象，默认行为。
3. 有参构造创建对象

```java
 <!--有参构造方法注入-->
    <bean id="user" class="com.jbit.entity.User">
        <!--第一种方式,通过下标赋值-->
        <constructor-arg index="0" value="张三"/>
        <!--第二种方式,通过类型赋值。但是有多个同类型时使用不方便，不推荐使用-->
        <constructor-arg type="java.lang.String" value="张三"/>
        <!--第三种方式,直接通过参数名设置-->
        <constructor-arg name="name" value="张三"/>

    </bean>
```

## 5、Spring配置

#### 5.1、别名

```xml
<!--添加别名,别名严格区分大小写,添加后可以通过别名或者原本参数名任意访问数据.-->
    <alias name="user" alias="USER"/>
```

#### 5.2、Bean的配置

```
id: bean的唯一标识符,相当于对象名
class: bean对象所对应的全限定名
name:也是别名,而且name可以同时取多个别名
```

#### 5.4、import

import一般用于团队开发,他可以将多个配置文件合并导入

假设项目中有多个人开发,三个人负责不同的类开发,不同的类需要注册在不同的bean中,就可以利用import将所有人的beans.xml合并为一个总的



## 6、依赖注入

#### 6.1、构造器注入

[点击跳转构造器注入](#4、IOC创建对象的方式)

//按住ctrl点击跳转

#### 6.2、Set方式注入

- 依赖注入：本质是Set注入
  - 依赖：bean对象的创建依赖于容器
  - 注入：bean对象中的所有属性由容器来注入

```java
//实体类
private String name;
    private Address address;
    private String[] books;
    private List<String> hobbys;
    private Map<String,String> card;
    private Set<String> games;
    private Properties info;
//省略get/set方法
```

```xml
    <bean id="address" class="com.jbit.entity.Address">
        <property name="address" value="广州"/>
    </bean>
    <bean id="student" class="com.jbit.entity.Student">
        <!--普通依赖注入-->
        <property name="name" value="张三"/>

        <!--Bean引用类型注入-->
        <property name="address" ref="address"/>

        <!--数组注入-->
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>水浒传</value>
                <value>西游记</value>
                <value>三国演义</value>
            </array>
        </property>

        <!--list数组注入-->
        <property name="hobbys">
            <list>
                <value>list1</value>
                <value>list2</value>
            </list>
        </property>

        <!--Map注入-->
        <property name="card">
            <map>
                <entry key="账号" value="admin"/>
                <entry key="密码" value="123456"/>
            </map>
        </property>

        <!--Set注入-->
        <property name="games" >
            <set>
                <value>A</value>
                <value>B</value>
                <value>C</value>
            </set>
        </property>

        <!--Properties注入-->
        <property name="info">
            <props>
                <prop key="学号">20210205</prop>
                <prop key="性别">男</prop>
            </props>
        </property>
    </bean>
```



#### 6.3、拓展方式注入

可以使用 p命名空间和c命名空间进行注入

```xml
<!--p命名空间注入,可以直接注入属性的值-->
    <!--<bean id="user" class="com.jbit.entity.User" p:name="张三" p:age="18" />-->

    <!--c命名空间注入,通过构造器注入:constructor。只有类有有参构造方法时才能使用-->
    <bean id="user" class="com.jbit.entity.User" c:age="18" c:name="张三" />
```

注意点:使用p命名空间和c命名空间注入需要在<beans>标签中添加

```xml
xmlns:p="http://www.springframework.org/schema/p"
xmlns:c="http://www.springframework.org/schema/c"
```

#### 6.4、bean的作用域

1. 单例模式（Spring默认机制）

   ```xml
   <bean id="user" class="com.jbit.entity.User" c:age="18" c:name="张三" scope="singleton" />
   ```

2. 原型模式：每次从容器中get的时候，获取的都是新的对象

   ```xml
   <bean id="user" class="com.jbit.entity.User" c:age="18" c:name="张三" scope="prototype" />
   ```

3. 其余的request，session，application，只能在web项目中使用

## 7、bean的自动装配

- 自动装配是Spring满足bean依赖的一种方式
- Spring会在上下文中自动寻找，并自动给bean装配属性

Spring中有三种自动装配的方式

1. 在xml中显示的配置
2. 在java中显示配置
3. 隐式的自动装配bean

#### 7.1、ByName自动装配

```xml
<!--
        byName 会自动在容器上下文中查找,和自己对象set方法后面的值对应的beanid
    -->
    <bean id="people" class="com.jbit.entity.People" autowire="byName">
        <property name="name" value="张三"/>
        <property name="dog" ref="dog"/>
        <property name="cat" ref="cat"/>
```

7.2、ByType自动装配

```xml
<!--
        byType 会自动在容器上下文中查找,和自己对象set方法后面的类型对应的beanid
    -->
    <bean id="people" class="com.jbit.entity.People" autowire="byType">
        <property name="name" value="张三"/>
        <property name="dog" ref="dog"/>
        <property name="cat" ref="cat"/>
    </bean>
```

- byname的时候,需要保证所有bean的id唯一,并且这个bean需要和自动注入的属性的set方法的值一致
- byname的时候,需要保证所有bean的class唯一,并且这个bean需要和自动注入的属性类型一致

#### 7.3、使用注解开发

jdk1.5开始支持注解,spring2.5开始支持注解

##### 使用注解须知:

1. 导入约束
2. 配置注解的支持

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!--开启注解的包扫描,不开启无法使用注解-->
    <context:annotation-config/>
    
```

3. @Autowired：可以在类上，或者属性，set方法上使用。

   使用Autowired后就可以不用编写set方法，前提是这个自动装配的属性在IOC容器中存在，且符合名字byname

4. 如果显示定义了Autowired的required属性为false，说明这个对象可以为null，否则不允许为空

5. 如果@Autowired自动装配的环境比较复杂，自动装配无法通过一个注解完成的时候，可以使用@Qualifier（value=”xxx“）配合使用，指定一个唯一的bean对象进行注入

6. @Resource注解

```java
public class People{
	@resource(name = "cat")
	private Cat cat;

	@Resource
	private Dog dog;
}
```

#### 小结:

@Resource和@AutoWired的区别

- 都是用来自动装配，都可以放在属性字段上
- AutoWired默认通过byType方式实现，如果有多个相同类型，则通过byName实现
- Resource默认通过byname的方式实现，如果找不到名字则通过byType实现

## 8、使用注解开发

在Spring4之后，要使用注解开发就必须保证aop包的导入

使用注解还要导入context的约束，增加对注解的支持：[约束跳转](#使用注解须知:)//按住ctrl点击跳转

1. bean

2. 属性如何注入

   ```xml
   //等价于 <bean id="user" class="com.jbit.entity.User" />
   @Component
   public class User {
       //相当于<property name="name" value="张三"/>
       @Value("张三")
       private String name;
   }
   ```

   

3. 衍生的注解

   @Component有几个衍生注解,在web开发中,会按照mvc三层架构分层!

   - dao [@Repository]
   - service [@Service]
   - Controller [@Controller]

   这四个注解功能都是一样的,代表将某个类注册到Spring中,装备Bean

4. 自动装配

   [按照ctrl点击跳转](#7.3、使用注解开发)

5. 作用域

6. 小结

   xml与注解:

   - xml更加万能,适用于任何场合,维护简单方便
   - 注解不是自己的类使用不了,且维护相对复杂

   xml与注解最佳使用方式:

   - xml用来管理bean;
   - 注解只负责完成属性的注入
   - 必须注意一点,使用注解必须在xml中开启注解扫描



## 9、使用java的方式配置Spring

现在完全不使用spring的xml配置，全权交给java

JavaConfig是Spring的一个子项目，在Spring4之后，它成为了一个核心功能



## 10、代理模式

代理模式是SpringAOP的底层

代理模式的分类：

- 静态代理
- 动态代理

#### 10.1、静态代理

角色分析：

- 抽象角色：一般会使用接口或者抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，一般会对其做一些其它操作
- 客户：访问代理对象的人



代码步骤：

1. 接口

```java
//租房
public interface Rent {

    public void rent();
}
```



1. 真实角色

```java
//房东
public class Host implements Rent {
    @Override
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```



1. 代理角色

```java
public class proxy implements Rent {
    private Host host;

    public proxy() {
    }

    public proxy(Host host) {
        this.host = host;
    }

    @Override
    public void rent() {
        setHost();
        host.rent();
        heton();
        fare();
    }

    //看房
    public void setHost(){
        System.out.println("看房");
    }

    //收中介费
    public void fare(){
        System.out.println("收费");
    }

    public void heton(){
        System.out.println("签合同");
    }
}
```



1. 用户

```java
public static void main(String[] args) {
        Host host = new Host();
        //代理
        proxy pro = new proxy(host);
        pro.rent();
    }
```





代理模式的好处：

- 可以使真实角色的操作更加纯粹，不用去处理一些公共的行为
- 公共任务交给代理角色，实现了业务的分工
- 公共业务发生扩展的时候，方便集中管理

缺点：

- 一个真实角色就产生一个代理角色；代理量就会翻倍

#### 10.2动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理类是动态生成的,不是我们直接写好的
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口----JDK动态代理
  - 基于类：cglib
  - java字节码实现：javasist

需要了解两个类：Proxy 代理 ，Invocation Handler：调用处理程序



## 11、Spring实现Aop

使用AOP织入，需要导入一个依赖包

```xml
		<dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.6</version>
        </dependency>
```

方式一:使用sping的API接口 [主要是SpringAPI接口实现]

```java
public class AfterLog implements AfterReturningAdvice {
    //returnValue : 返回值
    @Override
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了"+method.getName()+"返回结果为"+returnValue);
    }
}
```

```xml
<!--方式1:使用原生的API接口-->
    <!--配置aop:需要导入aop的约束-->
    <!--<aop:config>-->
    <!--切入点: expression:表达式,execution(要执行的位置:)-->
        <aop:pointcut id="pointcut" expression="execution(* com.jbit.service.UserServiceImpl.*(..))"/>
-->
        <!--执行环绕增加-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
    </aop:config>
```



方式二:使用自定义类实现AOP [主要是切面定义]

```java
public class DiyPointCut {

    public void diy1(){
        System.out.println("方法执行前进行处理");
    }

    public void diy2(){
        System.out.println("方法执行后进行处理");
    }

}
```

```xml
    <!--方式2:自定义类-->
    <bean id="diy" class="com.jbit.diy.DiyPointCut"/>
    <aop:config>
        自定义切面,ref要引用的类
        <aop:aspect ref="diy">
            切入点
            <aop:pointcut id="point" expression="execution(* com.jbit.service.UserServiceImpl.*(..))"/>
            通知
            <aop:before method="diy1" pointcut-ref="point"/>
            <aop:after method="diy2" pointcut-ref="point"/>
        </aop:aspect>
    </aop:config>
```



方式三:使用注解实现

```java
@Aspect //标注这个类是一个切面
public class AnnotationPointCut {

    @Before("execution(* com.jbit.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("方法执行前操作");
    }

    @After("execution(* com.jbit.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("方法执行后");
    }

    //在环绕增强中,可以给定一个参数,代表要获取切入的点
    @Around("execution(* com.jbit.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable {
        System.out.println("环绕前");

        Signature signature = jp.getSignature();//获取签名
        System.out.println(signature);
        //执行方法
        Object proceed = jp.proceed();

        System.out.println("环绕后");
    }
}
```

```xml
    <!--方式3-->
    <bean id="annotationPointCut" class="com.jbit.diy.AnnotationPointCut"/>
    <!--开启注解支持-->
    <aop:aspectj-autoproxy/>
```



## 12、整合MyBatis

步骤：

1. 导入jar包
   - junit
   - mybatis
   - mysql数据库
   - spring相关
   - aop织入
   - mybatis-spring
   
2. 编写配置文件

   ```xml
   <!--applicationContext.xml-->
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
   
       <import resource="spring-dao.xml"/>
   
       <bean id="userMapper" class="com.jbit.mapper.UserMapperImpl2">
           <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
       </bean>
   
   </beans>
   ```

   ```xml
   <!--spring-dao.xml-->
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
   
       <!--DataSource:使用Spring的数据源替换myBatis的配置
           这里使用Spring提供的JDBC
       -->
       <!--导入外部的资源文件-->
       <context:property-placeholder location="classpath:jdbc.properties"/>
       <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
           <property name="driverClassName" value="${driver}"/>
           <property name="url" value="${url}"/>
           <property name="username" value="${user}"/>
           <property name="password" value="${pwd}"/>
           <!--设置连接的信息-->
       </bean>
   
       <!--sqlSessionFactory-->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
           <property name="dataSource" ref="dataSource"/>
           <!--<property name="configLocation" value="classpath:mybatis-config.xml"/>-->
           <property name="mapperLocations" value="classpath:com/jbit/mapper/UserMapper.xml"/>
       </bean>
   
       <!--SqlSessionTemplate-->
       <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
           <!--只能使用构造器注入sqlSessionFactory,因为它没有set方法-->
           <constructor-arg index="0" ref="sqlSessionFactory"/>
       </bean>
   
       <bean id="userMapper" class="com.jbit.mapper.UserMapperImpl">
           <property name="sqlSession" ref="sqlSession"/>
       </bean>
   
   
   </beans>
   ```

   

3. 测试

   ```java
   public void test2(){
           ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
           UserMapper userMapper = ac.getBean("userMapper", UserMapper.class);
           for (SmbmsUser smbmsUser : userMapper.selUser()) {
               System.out.println(smbmsUser);
           }
       }
   ```

   



### 12.1、回忆mybatis

1. 编写实体类
2. 编写核心配置文件
3. 编写接口
4. 编写Mapper.xml

### 12.2、Mybatis-spring

1.编写数据源配置

2.sqlSessionFacotry

3.sqlSessionTemplate

4.需要给接口加实现类【】

5.将自己写的实体类,注入到Spring中

6.测试使用



## 13、声明式事务

1、回顾事务

- 把一组业务当成一个整体要么都成功，要么都失败
- 事务在项目开发中，十分的重要，涉及到数据的一致性问题，不能马虎
- 确保完整性和一致性

事务的ACID原则：

- 原子性
- 一致性
- 隔离性
  - 多个业务可能操作同一个资源，防止数据损坏

- 持久性
  - 事务一旦提交，无论系统发生什么问题，结果都不会再被影响。被持久化的写到存储器中

2、spring中的事务管理

- 声明式事务

```xml
    <!--配置声明式事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>
    <!--结合AOP实现事务的织入-->
    <!--配置事务通知-->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <!--name: 给哪些方法配置事务-->
        <!--配置事务的传播特性:propagation-->
        <tx:caching>
            <tx:method name="add" propagation="REQUIRED">
        </tx:caching>
    </tx:advice>

    <!--配置事务切入-->
    <aop:config>
        <aop:pointcut id="txPointCut" expression="execution(* com.jbit.mapper.*.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```

- 编程式事务

为什么需要事务？

- 如果不使用事务，可能存在数据提交不一致的情况
- 如果步骤Spring中去配置声明式事务，我们就需要在代码中手动配置事务







## 小结

Spring的IOC与AOP底层还需进一步了解

注解的使用需要了解

spring底层需要了解
