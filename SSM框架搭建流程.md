# SSM框架搭建流程

为了快速的搭建一个前后端分离的ssm框架，本文档将以全程图文的方式，手把手的从零开始搭建SSM框架。

需要前置条件如下：

1. JDK环境
2. IDEA开发工具
3. Maven
4. Radis（非必要，只是本项目后期需要Radis数据库）



## 搭建流程

1. 打开IDEA，创建一个新的项目

   ![image-20210602210829408](\assets\image-20210602210829408.png)

2. 选中Maven，在Project SDK中选择JDK版本。然后next进行下一步

   ![image-20210602210922781](\assets\image-20210602210922781.png)

3. 自定义项目名与存放的路径。然后点击Finish完成创建![image-20210602211235911](\assets\image-20210602211235911.png)

4. 创建完成后得到如下目录

   ![image-20210602212035671](\assets\image-20210602212035671.png)

   由于我们需要的是一个父项目，用于管理我们整个项目需要的所有依赖，

   将src整个目录直接删除

5. 删除完成之后，右击项目的根，创建一个子项目

   ![image-20210602212448346](\assets\image-20210602212448346.png)

6. 点击后来到第二步，不做改动->next

7. 来到新的界面，父项目默认选中，我们只需要修改子项目名

   ![image-20210602213207679](\assets\image-20210602213207679.png)

   这里的子项目名证明它在整个项目中，负责dao

   然后Finish

8. 随后在父项目中即可获得一个新的子项目

   ![image-20210602213452548](\assets\image-20210602213452548.png)

   子项目的pom.xml中有如下标签:

   ```xml
   <parent>
       <artifactId>crm_backDemo</artifactId>
       <groupId>org.example</groupId>
       <version>1.0-SNAPSHOT</version>
   </parent>
   <!--证明它是一个子项目,项目中所有的工程都依赖于父工程-->
   ```

   父项目的pom.xml则新增如下标签

   ```xml
   <modules>
   	<module>crm_backDemo_dao</module>
   </modules>
   <!--证明它有一个子项目,挂载在当前项目中-->
   ```

   

9. 按照前面的流程,我们继续创建3个子项目。分别是

   1. entity
   2. service
   3. web（在web子项目中，需要选择项目模板：**webapp**）

   获得如下项目路径

   ![image-20210602214305449](\assets\image-20210602214305449.png)

10. 整个项目结构创建完成后，我们需要对依赖进行导入，在父项目的pom.xml中导入依赖，具体常用依赖如下，按照自己需求导入

    ```xml
    <dependencies>
        
        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.11</version>
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
    
        <!--EL表达式-->
        <dependency>
          <groupId>javax.servlet</groupId>
          <artifactId>jstl</artifactId>
          <version>1.2</version>
        </dependency>
        <dependency>
          <groupId>taglibs</groupId>
          <artifactId>standard</artifactId>
          <version>1.1.2</version>
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
        <!--log4j日志依赖-->
        <dependency>
          <groupId>log4j</groupId>
          <artifactId>log4j</artifactId>
          <version>1.2.17</version>
        </dependency>
        <!--分页插件-->
        <dependency>
          <groupId>com.github.pagehelper</groupId>
          <artifactId>pagehelper</artifactId>
          <version>5.1.2</version>
        </dependency>
        <!--json-->
        <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>fastjson</artifactId>
          <version>1.2.75</version>
        </dependency>
    
        <!--jquery-->
        <dependency>
          <groupId>org.webjars.bower</groupId>
          <artifactId>jquery</artifactId>
          <version>3.3.1</version>
        </dependency>
    
        <dependency>
          <groupId>org.aspectj</groupId>
          <artifactId>aspectjweaver</artifactId>
          <version>1.9.6</version>
        </dependency>
    
        <!--io流-->
        <dependency>
          <groupId>commons-fileupload</groupId>
          <artifactId>commons-fileupload</artifactId>
          <version>1.4</version>
        </dependency>
        <dependency>
          <groupId>commons-io</groupId>
          <artifactId>commons-io</artifactId>
          <version>2.7</version>
        </dependency>
    
        <!--Redis依赖-->
        <dependency>
          <groupId>redis.clients</groupId>
          <artifactId>jedis</artifactId>
          <version>3.6.0</version>
        </dependency>
    
        <dependency>
          <groupId>org.springframework.data</groupId>
          <artifactId>spring-data-redis</artifactId>
          <version>1.6.1.RELEASE</version>
        </dependency>
    
    
      </dependencies>
    ```

    在父子项目中，父项目导入的依赖子项目也可以直接使用

11. 还需要添加子项目的pom.xml中添加子项目的相互依赖

    1. web子项目中需要

       ```xml
       <!--引用service和实体类的依赖-->
       <dependency>
           <groupId>org.example</groupId>
           <artifactId>crm_backDemo_service</artifactId>
           <version>1.0-SNAPSHOT</version>
       </dependency>
       <dependency>
           <groupId>org.example</groupId>
           <artifactId>crm_backDemo_entity</artifactId>
           <version>1.0-SNAPSHOT</version>
       </dependency>
       
       <!--我们同时需要删除build标签中的所有内容,包括build标签-->
       ```

    2. service子项目中需要

       ```xml
       <dependencies>
           <!--service需要dao层与实体类的依赖-->
           <dependency>
               <groupId>org.example</groupId>
               <artifactId>crm_backDemo_entity</artifactId>
               <version>1.0-SNAPSHOT</version>
           </dependency>
           <dependency>
               <groupId>org.example</groupId>
               <artifactId>crm_backDemo_dao</artifactId>
               <version>1.0-SNAPSHOT</version>
           </dependency>
       
           <dependency>
               <groupId>org.example</groupId>
               <artifactId>crm_backDemo_util</artifactId>
               <version>1.0-SNAPSHOT</version>
           </dependency>
       </dependencies>
       ```

       

    3. dao子项目中需要

       ```xml
       <dependencies>
           <!--dao层需要实体类的依赖-->
           <dependency>
               <groupId>org.example</groupId>
               <artifactId>crm_backDemo_entity</artifactId>
               <version>1.0-SNAPSHOT</version>
           </dependency>
       </dependencies>
       ```

       所有依赖导入完成之后,就需要创建ssm框架的配置文件

12. 在dao层的resource目录下,创建`database.properties`文件，与`redis.properties`文件

    ![image-20210602220635597](\assets\image-20210602220635597.png)

    在`database.properties`中编写数据库的配置

    ```properties
    #数据库资源文件
    jdbc.driver=com.mysql.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/crm 
    #连接数据库路径
    jdbc.user=root		
    #连接数据库用户名
    jdbc.pwd=			
    #连接数据库密码,没有就空着
    
    ```

    在`redis.properties`中编写redis的配置

    ```bash
    #redis的配置文件
    redis.host=localhost
    #redis连接路径
    redis.port=6379
    #redis连接端口号
    redis.timeout=100000
    #redis开启时间
    redis.maxTotal=300
    #redis的最大连接数
    redis.maxIdel=50
    #redis最大空闲数
    redis.maxWait=100000
    #redis最大等待时间
    redis.testOnReturn=true
    #redis在返回的时候是否需要验证
    redis.testOnBorrow=true
    #在连接redis时是否需要验证
    ```

    

    

13. 在dao子项目java文件中创建com.jbit.crm.dao文件夹
    随后在dao子项目中resources文件创建一个spring文件，再在spring中创建一个`applicationContext_dao.xml`配置文件。在其中编写如下配置

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    
        <!--引入外部资源文件-->
        <context:property-placeholder location="classpath:database.properties,classpath:redis.properties"/>
    
        <!--配置数据源-->
        <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
            <property name="driverClassName" value="${jdbc.driver}"/>
            <property name="url" value="${jdbc.url}"/>
            <property name="username" value="${jdbc.user}"/>
            <property name="password" value="${jdbc.pwd}"/>
        </bean>
    
        <!--配置Redis缓存-->
        <!--配置缓存的特性-->
        <bean id="jedisPoolConfig" class="redis.clients.jedis.JedisPoolConfig">
            <property name="maxTotal" value="${redis.maxTotal}"/>
            <property name="maxIdle" value="${redis.maxIdel}"/>
            <property name="maxWaitMillis" value="${redis.maxWait}"/>
            <property name="testOnReturn" value="${redis.testOnReturn}"/>
            <property name="testOnBorrow" value="${redis.testOnBorrow}"/>
        </bean>
        <!--配置Redis的连接池-->
        <bean id="jedisPool" class="redis.clients.jedis.JedisPool">
            <constructor-arg name="poolConfig" ref="jedisPoolConfig"/>
            <constructor-arg name="host" value="${redis.host}"/>
            <constructor-arg name="port" value="${redis.port}"/>
            <constructor-arg name="timeout" value="${redis.timeout}"/>
        </bean>
    
        <!--配置sqlsessionfactory-->
        <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
            <property name="dataSource" ref="dataSource"/>
            <!--配置mybatis特性-->
            <property name="typeAliasesPackage" value="com.jbit.crm.entity"/>
    
            <property name="configuration">
                <bean class="org.apache.ibatis.session.Configuration">
                    <!--日志输入的特性-->
                    <property name="logImpl" value="org.apache.ibatis.logging.stdout.StdOutImpl"/>
                    <!--数据库与实体类类名驼峰命名忽略-->
                    <property name="mapUnderscoreToCamelCase" value="true"/>
                </bean>
            </property>
            <!--配置分页插件-->
            <property name="plugins">
                <array>
                    <bean class="com.github.pagehelper.PageInterceptor">
                        <property name="properties">
                            <value>
                                helperDialect=mysql
                                reasonable=true
                            </value>
                        </property>
                    </bean>
                </array>
            </property>
    
        </bean>
    
        <!--配置Mapper代理-->
        <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
            <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
            <property name="basePackage" value="com.jbit.crm.dao"/>
        </bean>
    
    </beans>
    ```

    

14. 在service子项目java文件中创建com.jbit.crm.service文件夹
    接着在service子项目中同dao一样，子项目中resources文件创建一个spring文件，再在spring中创建一个`applicationContext_service.xml`配置文件。在其中编写如下配置

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
           xmlns:aop="http://www.springframework.org/schema/aop"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">
        
        <!--业务层配置文件-->
        <!--开启包扫描-->
        <context:component-scan base-package="com.jbit.crm.service">
            <context:include-filter type="annotation" expression="org.springframework.stereotype.Service"/>
        </context:component-scan>
    
        <!--配置事务管理器-->
        <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
            <property name="dataSource" ref="dataSource"/>
        </bean>
    
        <!--配置通知-->
        <tx:advice id="txAdvice">
            <tx:attributes>
                <tx:method name="add*" propagation="REQUIRES_NEW"/>
                <tx:method name="update*" propagation="REQUIRED"/>
                <tx:method name="del*" propagation="REQUIRED"/>
                <tx:method name="get*" read-only="true"/>
                <tx:method name="*" propagation="REQUIRES_NEW"/>
            </tx:attributes>
        </tx:advice>
        
        <!--配置切面和切点-->
        <aop:config>
            <aop:pointcut id="px" expression="execution(* com.jbit.crm.service.*.*(..))"/>
            <aop:advisor advice-ref="txAdvice" pointcut-ref="px"/>
        </aop:config>
    
    </beans>
    ```

15. 在web子项目中,我们需要将项目的文件创建成如下模样

    ![image-20210602230304282](\assets\image-20210602230304282.png)

    在springmvc配置文件中编写如下配置

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:mvc="http://www.springframework.org/schema/mvc"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    
        <!--开启包扫描-->
        <context:component-scan base-package="com.jbit.crm.controller">
            <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        </context:component-scan>
    
        <!--配置视图解析器(前后端分离项目,这个视图解析器可以没有)-->
        <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
            <property name="prefix" value="/"/>
            <property name="suffix" value=".jsp"/>
        </bean>
    
        <!--开启注解功能-->
        <mvc:annotation-driven/>
    
    </beans>
    ```

    在`applicationContext.xml`中编写如下配置

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <!--spring的主配置文件-->
        <!--引入service和dao层中的配置文件-->
        <import resource="classpath:spring/applicationContext_dao.xml"/>
        <import resource="classpath:spring/applicationContext_service.xml"/>
    
    
    </beans>
    ```

    在web.xml中编写如下配置

    ```xml
    <!DOCTYPE web-app PUBLIC
     "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
     "http://java.sun.com/dtd/web-app_2_3.dtd" >
    
    <web-app>
      <display-name>Archetype Created Web Application</display-name>
    
      <!--引入资源(引入spring的配置文件)-->
      <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:applicationContext.xml</param-value>
      </context-param>
    
      <!--配置字符过滤-->
      <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
          <param-name>encoding</param-name>
          <param-value>UTF-8</param-value>
        </init-param>
      </filter>
      <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
      </filter-mapping>
      
      <!--配置监听(让spring配置文件生效)-->
      <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
      </listener>
    
      <!--配置核心servlet-->
      <servlet>
        <servlet-name>dispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
          <param-name>contextConfigLocation</param-name>
          <param-value>classpath:springmvc.xml</param-value>
        </init-param>
      </servlet>
      <servlet-mapping>
        <servlet-name>dispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
      </servlet-mapping>
    </web-app>
    
    ```

    以上，smm框架的基本配置结束

16. 我们还需要Jedis和MD5加密的util工具类，同上面的步骤，创建一个util的子项目，完成之后还需要我们的包和工具类

    创建完成路径如下

    ![image-20210602230942414](\assets\image-20210602230942414.png)

    MD5Util类编写程序如下

    ```java
    package com.jbit.crm.util;
    
    import java.security.MessageDigest;
    import java.security.NoSuchAlgorithmException;
    import java.util.Base64;
    
    /**
     * 加密的工具类 -> MD5加密
     */
    public class MD5Util {
    
        /**
         * 加密方法
         * @param msg   要加密的数据
         * @return
         */
        public static String encode(String msg){
            //MessageDigest -> 为应用程序提供信息摘要算法(md5,sha算法等)
            //生成散序码
            try {
                MessageDigest md5 = MessageDigest.getInstance("md5");
                //md5.digest() 作用:完成哈希运算,获取哈希码,返回byte数组
                //Base64 -> 是一种使用64个字符表示二进制数据的方法
                return Base64.getEncoder().encodeToString(md5.digest(msg.getBytes()));
            } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
                return null;
            }
        }
    
    }
    
    ```

    RedisUtil编写程序如下

    ```java
    package com.jbit.crm.util;
    
    /*
    redis的工具类
     */
    
    import redis.clients.jedis.Jedis;
    import redis.clients.jedis.JedisPool;
    
    public class RedisUtil {
    
        /*定义Redis连接池*/
        private JedisPool jedisPool;
    
        public JedisPool getJedisPool() {
            return jedisPool;
        }
    
        public void setJedisPool(JedisPool jedisPool) {
            this.jedisPool = jedisPool;
        }
    
        //判断redis中是否有指定的数据
        public boolean existsKey(String key){
            Jedis jedis = null;
            try {
                jedis = jedisPool.getResource();
                return jedis.exists(key);
            } catch (Exception e) {
                e.printStackTrace();
                return false;
            } finally {
                jedisPool.returnResource(jedis);
            }
        }
    
        /*保存数据*/
        public String setStrValue(String key,String value){
            Jedis jedis = null;
            try {
                jedis = jedisPool.getResource();
                return jedis.set(key,value);
            } catch (Exception e) {
                e.printStackTrace();
                return null;
            } finally {
                jedisPool.returnResource(jedis);
            }
        }
    
        //获取数据
        public String getStringValue(String key){
            Jedis jedis = null;
            try {
                jedis = jedisPool.getResource();
                return jedis.get(key);
            } catch (Exception e) {
                e.printStackTrace();
                return null;
            } finally {
                jedisPool.returnResource(jedis);
            }
        }
    
    }
    
    ```

17. 至此，所有准备工作完成，现在开始编写测试代码

18. 首先在entity子项目中创建实体类![image-20210603104808440](\assets\image-20210603104808440.png)

19. 在dao层创建接口，绑定mybatis的mapper访问数据库

    需要如下目录与文件

    ![image-20210603105018324](\assets\image-20210603105018324.png)

    UserMapper中的代码

    ```java
    public interface UserMapper {
        //登录
        TUser login(String userName);
    }
    ```

    UserMapper.xml中的代码

    ```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="com.jbit.crm.dao.UserMapper">
    
    
        <select id="login" resultType="com.jbit.crm.entity.TUser">
            select * from t_user where user_name = #{userName}
        </select>
    </mapper>
    ```

20. 随后使用service层，编写业务

    service目录与文件如下

    ![image-20210603105311023](\assets\image-20210603105311023.png)

    UserService中创建dao层中方法的接口

    ```java
    public interface UserService {
        //登录
        TUser login(String userName,String userPwd);
    }
    ```

    UserServiceImpl实现service的接口

    ```java
    package com.jbit.crm.service.impl;
    
    import com.github.pagehelper.util.StringUtil;
    import com.jbit.crm.dao.UserMapper;
    import com.jbit.crm.entity.TUser;
    import com.jbit.crm.service.UserService;
    import com.jbit.crm.util.MD5Util;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Service;
    
    @Service("userService")
    public class UserServiceImpl implements UserService {
    
        @Autowired
        private UserMapper userMapper;
    
        /*
        1.服务器端的非空验证
        2.调用数据访问层,通过用户名获取用户信息,并返回用户对象
        3.判断用户对象是否为空
        4.验证密码是否正确
         */
        public TUser login(String userName, String userPwd) {
            //1.非空验证
            if (StringUtil.isEmpty(userName)|| StringUtil.isEmpty(userPwd)){
                return null;
            }
            //2.调用数据访问层,通过用户名获取用户信息,返回用户对象
            TUser login = userMapper.login(userName);
    
            //3.判断用户对象是否为空
            if (login==null){
                return null;
            }
            //4.验证密码是否正确
            //对密码进行加密,后验证
            userPwd = MD5Util.encode(userPwd);
            if (userPwd.equals(login.getUserPwd())){
                return login;
                //密码正确,将用户数据return回去
            }
            return null;
        }
    }
    ```

    

21. 最后一步来到controller层,需要目录及文件如下

    ![image-20210603105523415](\assets\image-20210603105523415.png)

    UserController层代码如下

    ```java
    package com.jbit.crm.controller;
    
    import com.alibaba.fastjson.JSON;
    import com.jbit.crm.entity.TUser;
    import com.jbit.crm.service.UserService;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;
    
    //restController :ResponseBody和Controller的结合体
    @RestController
    @RequestMapping("/user")
    public class UserController {
    
        @Autowired
        private UserService userService;
    
        @RequestMapping("/login")
        public String login(@RequestParam(name="userName",required = true) String userName, String userPwd){
            TUser login = userService.login(userName, userPwd);
            return JSON.toJSONString(login);
        }
    
    }
    ```

    

22. 至此，一个ssm框架搭建完成

