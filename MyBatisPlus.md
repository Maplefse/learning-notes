# MyBatisPlus

## 概述

MyBatisPlus可以节省大量工作时间，所有的crud代码它都可以自动化完成

### 简介

官网：https://mp.baomidou.com/

[MyBatis-Plus (opens new window)](https://github.com/baomidou/mybatis-plus)（简称 MP）是一个 [MyBatis (opens new window)](http://www.mybatis.org/mybatis-3/)的增强工具，在 MyBatis 的基础上只做增强不做改变，为简化开发、提高效率而生。

### 特性

- **无侵入**：只做增强不做改变，引入它不会对现有工程产生影响，如丝般顺滑
- **损耗小**：启动即会自动注入基本 CURD，性能基本无损耗，直接面向对象操作
- **强大的 CRUD 操作**：内置通用 Mapper、通用 Service，仅仅通过少量配置即可实现单表大部分 CRUD 操作，更有强大的条件构造器，满足各类使用需求
- **支持 Lambda 形式调用**：通过 Lambda 表达式，方便的编写各类查询条件，无需再担心字段写错
- **支持主键自动生成**：支持多达 4 种主键策略（内含分布式唯一 ID 生成器 - Sequence），可自由配置，完美解决主键问题
- **支持 ActiveRecord 模式**：支持 ActiveRecord 形式调用，实体类只需继承 Model 类即可进行强大的 CRUD 操作
- **支持自定义全局通用操作**：支持全局通用方法注入（ Write once, use anywhere ）
- **内置代码生成器**：采用代码或者 Maven 插件可快速生成 Mapper 、 Model 、 Service 、 Controller 层代码，支持模板引擎，更有超多自定义配置等您来使用
- **内置分页插件**：基于 MyBatis 物理分页，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询
- **分页插件支持多种数据库**：支持 MySQL、MariaDB、Oracle、DB2、H2、HSQL、SQLite、Postgre、SQLServer 等多种数据库
- **内置性能分析插件**：可输出 Sql 语句以及其执行时间，建议开发测试时启用该功能，能快速揪出慢查询
- **内置全局拦截插件**：提供全表 delete 、 update 操作智能分析阻断，也可自定义拦截规则，预防误操作



## 快速上手

1. 创建数据库`mybatis_plus`

   ```mysql
   # 省略建表过程
   CREATE TABLE USER
   (
   	id BIGINT(20) NOT NULL COMMENT '主键ID',
   	NAME VARCHAR(30) NULL DEFAULT NULL COMMENT '姓名',
   	age INT(11) NULL DEFAULT NULL COMMENT '年龄',
   	email VARCHAR(50) NULL DEFAULT NULL COMMENT '邮箱',
   	PRIMARY KEY (id)
   );
   
   DELETE FROM USER;
   
   INSERT INTO USER (id, NAME, age, email) VALUES
   (1, 'Jone', 18, 'test1@baomidou.com'),
   (2, 'Jack', 20, 'test2@baomidou.com'),
   (3, 'Tom', 28, 'test3@baomidou.com'),
   (4, 'Sandy', 21, 'test4@baomidou.com'),
   (5, 'Billie', 24, 'test5@baomidou.com');
   ```

   

2. 创建一个springboot项目，并导入依赖

   ```xml
   <!--数据库驱动-->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
   </dependency>
   <!--mybatis-plus-->
   <dependency>
       <groupId>com.baomidou</groupId>
       <artifactId>mybatis-plus-boot-starter</artifactId>
       <version>3.4.3.1</version>
       <!--该版本为2021.6.17的最新版本-->
   </dependency>
   ```

   注意：尽量不要同时导入mybatis和mybais plus

3. 连接数据库，这一步和mybatis相同

   ```yml
   spring:
     datasource:
       username: root
       password:
       #?serverTimezone=UTC解决时区的报错
       url: jdbc:mysql://localhost:3306/mybatis_plus?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
   ```

   

4. mapper接口

   ```java
   package com.maplef.mapper;
   
   import com.baomidou.mybatisplus.core.mapper.BaseMapper;
   import com.maplef.entity.User;
   import org.springframework.stereotype.Repository;
   
   //在对应的mapper上继承基本的类 BaseMapper
   @Repository //代表持久层
   public interface UserMapper extends BaseMapper<User> {
   
   }
   ```

   

5. 主方法

   需要在主启动类上扫描mapper接口才能使用

   ```java
   //扫描mapper文件夹
   @MapperScan("com.maplef.mapper")
   @SpringBootApplication
   public class DemoApplication {
   
       public static void main(String[] args) {
           SpringApplication.run(DemoApplication.class, args);
       }
   
   }
   ```

6. 测试

   ```java
       //继承了BaseMapper,所有的方法都来自父类
       @Autowired
       private UserMapper userMapper;
   
       @Test
       void contextLoads() {
   
           //查询全部用户
           // 参数是一个Wrapper,条件构造器,不使用,用null即可
           List<User> users = userMapper.selectList(null);
           users.forEach(System.out::print);
           //循环输出
       }
   
   ```

## 配置日志

经过上面的配置与操作,已经能够正常使用MyBatisPlus，但是所有的sql操作都是不可见的，在开发流程中，需要知道它是如何执行的，所以需要日志功能。

```yaml
# 配置日志
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

运行效果

![image-20210617153950789](\assets\image-20210617153950789.png)



## CRUD扩展

### 插入操作

1. ##### 插入

   ```java
       //测试插入
       @Test
       public void testInsert(){
           User user = new User();
   
           user.setName("maplef");
           user.setAge(18);
           user.setEmail("1371730063@qq.com");
   
           int resutl = userMapper.insert(user);   //会自动生成id
           System.out.println(resutl); //受影响的行数
   
           System.out.println(user);   //返回插入完后的实体类,发现id会自动回填
       }
   
   //注意:实体类和数据库数据类型一定要一致!!!!
   ```

   运行效果:![image-20210617184448949](\assets\image-20210617184448949.png)

   执行插入语句时,会自动往其中插入一个默认的id值

2. ##### 主键生成策略

   分布式系统唯一id生成方案:https://www.cnblogs.com/haoxinyue/p/5208136.html

   ##### 雪花算法：

   snowflake是Twitter开源的分布式ID生成算法，结果是一个long型的ID。其核心思想是：使用41bit作为毫秒数，10bit作为机器的ID（5个bit是数据中心，5个bit的机器ID），12bit作为毫秒内的流水号（意味着每个节点在每毫秒可以产生 4096 个 ID），最后还有一个符号位，永远是0。具体实现的代码可以参看https://github.com/twitter/snowflake。雪花算法支持的TPS可以达到419万左右（2^22*1000）。

   雪花算法在工程实现上有单机版本和分布式版本。单机版本如下，分布式版本可以参看美团leaf算法：https://github.com/Meituan-Dianping/Leaf

3. 主键自增

   需要配置主键自增：

   1. 实体类字段上增加`@TableId(type = IdType.AUTO)`
   2. 数据库字段一定要是自增
   3. 再次运行插入方法即可

4. 源码解析

   ```java
   public enum IdType {
       ATUO(0),//数据库id自增
       NONE(1),//未设置主键
       INPUT(2),//手动输入
       ASSIGN_ID(3),//自动分配id,使用雪花算法
       ASSIGN_UUID(4);//自动分配UUID
   }
   ```



### 更新操作

1. ```java
   //测试更新
   @Test
   public void testUpdate(){
       User user = new User();
   
       // 通过条件自动拼接动态sql
       user.setId(5L);
       user.setName("maplef");
       user.setAge(20);
   
       int i = userMapper.updateById(user);
       //虽然方法名叫ById,但它需要的是一个对象
       System.out.println(i);
   }
   ```

2. 运行效果

   ![image-20210619203808088](\assets\image-20210619203808088.png)

3. 所有的sql都会自动帮你配置

### 自动填充

在正常的数据库中，常常包含创建时间，修改时间这两条数据，这些操作普遍都是自动完成的，不想，也懒得去手动更新

有以下两种方法进行自动化

> 方法一：数据库级别

1. 在表中新增字段，create_time,update_time
2. ![image-20210619204643505](\assets\image-20210619204643505.png)
3. 测试插入方法(记得同步实体类)
4. ![image-20210619205105023](\assets\image-20210619205105023.png)
5. 更改第5条数据，修改时间已经变更
6. 工作中不建议使用，可能会因为更改数据库，出大问题

> 方法二：代码级别

先将数据库的默认值删掉

1. 实体类的字段属性上增加注解

   ```java
     // 字段添加填充内容
     @TableField(value = "create_time",fill = FieldFill.INSERT)
     private Date createTime;
     // 字段修改填充内容
     @TableField(value = "update_time", fill = FieldFill.UPDATE)
     private Date updateTime;
   ```

   

2. 编写处理器处理注解

   ```java
   import com.baomidou.mybatisplus.core.handlers.MetaObjectHandler;
   import org.apache.ibatis.reflection.MetaObject;
   import org.springframework.stereotype.Component;
   
   import java.sql.Date;
   
   
   @Component  //一定要将处理器加入到IOC容器中!
   public class MyMetaBojectHandler implements MetaObjectHandler {
       java.util.Date date = new java.util.Date();
       //插入时的填充策略
       @Override
       public void insertFill(MetaObject metaObject) {
           //插入值的时候自动对这个数据库字段进行值的填充
           this.strictInsertFill(metaObject,"createTime", Date.class,new Date(date.getTime()));
           this.strictUpdateFill(metaObject, "updateTime", Date.class,new Date(date.getTime()));
       }
   
       //更新时的填充策略
       @Override
       public void updateFill(MetaObject metaObject) {
           //更新的时候只修改更新的字段
           this.strictUpdateFill(metaObject, "updateTime", Date.class,new Date(date.getTime()));
       }
   
   }
   ```

   **注意：自动更新的值的数据类型，一定要与实体类的数据类型相同，否则会发生包括：报错、运行后值为null等bug**

3. 运行插入的效果![image-20210619213334584](\assets\image-20210619213334584.png)

4. 运行修改的效果

   为了演示效果将update的值修改![image-20210619213707104](\assets\image-20210619213707104.png)

   修改后，update的值成功被修改![image-20210619213738350](\assets\image-20210619213738350.png)

### 乐观锁

乐观锁与悲观锁的说明在Redis中有过记载

> 乐观锁：它认为什么时候都不会出现问题，所以不会上锁！更新数据的时候去判断一下，在此期间是否有人修改过这个数据
>
> 悲观锁：它很悲观，认为什么时候都会出现问题，无论什么操作都会加锁

乐观锁实现方式：

- 取出记录时，获取当前version
- 更新时带上这个version
- 执行更新时，set version = newVersion where version = oldVersion
- 如果version不对，更新失败

```sql
在执行数据操作时,先查询,获得version。假如当前version = 1
现在有两个线程
--- A线程	A线程抢先完成
update user set name = "maplef",version = version+1
where id = 1 and version = 1
---	B线程	B线程在A线程之后,这时,version已经不等于1,sql语句执行失败
update user set name = "maplef",version = version+1
where id = 1 and version = 1
```

#### Mybatis-Plus测试

1. 数据库添加如下列

   ![image-20210619215203186](\assets\image-20210619215203186.png)

2. 更改实体类

   ```java
   @Version  //乐观锁Version注解
   private Integer version;
   //这个Version注解导入的是Mybatis-Plus包下的,别导错了
   ```

   

3. 注册组件

   ```java
   @EnableTransactionManagement
   @Configuration  //配置类
   public class MyBatisPlusConfig {
   
       //注册乐观锁插件
       @Bean
       public MybatisPlusInterceptor mybatisPlusInterceptor() {
           MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
           interceptor.addInnerInterceptor(new OptimisticLockerInnerInterceptor());
           return interceptor;
       }
   ```

4. 运行测试

   ```java
       //测试乐观锁,正常成功运行效果
       @Test
       public void testOptimisticLocker(){
           //1.查询用户信息
           User user = userMapper.selectById(1L);
           //2.修改用户信息
           user.setName("maplef");
           user.setEmail("1371730063@qq.com");
           //3.执行更新操作
           userMapper.updateById(user);
       }
   ```

   ![image-20210619220453949](\assets\image-20210619220453949.png)运行结果，更新操作成功执行，且version自增1变成了2


   运行失败效果

   ```java
   //测试乐观锁,失败效果
       @Test
       public void testOptimisticLocker2(){
           //1.查询用户信息
           User user = userMapper.selectById(1L);
           //2.修改用户信息
           user.setName("maplef111");
           user.setEmail("1371730063@qq.com");
   
           //模拟另一个线程执行插队操作
           User user2 = userMapper.selectById(1L);
           user2.setName("maplef222");
           user2.setEmail("1371730063@qq.com");
           userMapper.updateById(user2);
   
           //3.执行更新操作
           userMapper.updateById(user);    //如果没有乐观锁,maplef111就会覆盖maplef222的修改
       }
   ```

   运行结果

   ![image-20210619221911848](\assets\image-20210619221911848.png)

   ![image-20210619221942796](\assets\image-20210619221942796.png)





### 查询操作

普通的查询在上方多次使用，不再赘述

1. 批量,多结果查询

   ```java
   @Test
   public void testSelectByBatchId(){
       List<User> users = userMapper.selectBatchIds(Arrays.asList(1, 2, 3));
       users.forEach(System.out::println);
   }
   
   //查询结果
   /*
   User{id=1, name='maplef222', age=18, email='1371730063@qq.com'}
   User{id=2, name='Jack', age=20, email='test2@baomidou.com'}
   User{id=3, name='Tom', age=28, email='test3@baomidou.com'}
   */
   ```

   

2. 自定义条件查询

   ```java
   //条件查询
   @Test
   public void testSelectByBatchIds(){
       HashMap<String, Object> map = new HashMap<>();
   
       // 自定义查询条件
       map.put("name","maplef");
       //key为数据库列名,value为查询条件
   
       List<User> users = userMapper.selectByMap(map);
       users.forEach(System.out::println);
   }
   
   
   /*
   	查询结果
   	User{id=5, name='maplef', age=20, email='test5@baomidou.com'}
   */
   ```

### 分页查询

MyBatisPlus内置了分页插件

1. 配置拦截器组件

   ```java
   // 最新版
   @Bean
   public MybatisPlusInterceptor mybatisPlusPageInterceptor() {
       MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
       interceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.H2));
       return interceptor;
   }
   ```

   

2. 直接使用Page对象

   ```java
   //测试分页查询
   @Test
   public void testPage(){
       //参数一:当前页
       //参数二:页面大小
       Page<User> objectPage = new Page<>(1,5);
       userMapper.selectPage(objectPage,null);
   
       // 不进行 count sql 优化，解决 MP 无法自动优化 SQL 问题，这时候你需要自己查询 count 部分
       // page.setOptimizeCountSql(false);
       // 当 total 为小于 0 或者设置 setSearchCount(false) 分页插件不会进行 count 查询
       // 要点!! 分页返回的对象与传入的对象是同一个
       objectPage.getRecords().forEach(System.out::println);
   }
   ```

3. 运行结果

   ![image-20210619234432161](\assets\image-20210619234432161.png)

分页后，一般页面需要的数据，例如页面总数等，使用`objectPage.getTotal()`就能拿到



### 删除操作

1. 根据id删除数据

   ```java
   //根据id删除数据
   @Test
   public void testDeleteById(){
       userMapper.deleteById(5L);
   }
   ```

2. 批量删除

   ```java
   //批量删除
   @Test
   public void testDeleteBatchId(){
       userMapper.selectBatchIds(Arrays.asList(1L,2L,3L,4L));
   }
   ```

   

3. 条件删除

   ```java
   //条件删除
   @Test
   public void testDeleteMap(){
       HashMap<String, Object> map = new HashMap<>();
       map.put("name","maplef");
       userMapper.deleteByMap(map);
   }
   ```

   

4. 删除操作没什么特别的地方，方法的名字和使用与查询，更新一样



### 逻辑删除

> 逻辑删除：数据并没有直接从数据库删除，而是通过一列数据让它失效！ delete =  0 => deleted = 1

数据很重要!，用不到的数据不等于永远用不到，不可能不用了就一次性把数据清空！

使用操作

1. 数据库增加字段

   ![image-20210620000217027](\assets\image-20210620000217027.png)

2. 实体类同步

   ```java
   @TableLogic //逻辑删除注解
   private Integer deleted;
   ```

3. 配置

   ```yaml
   mybatis-plus:
     global-config:
       db-config:
         logic-delete-field: flag  # 全局逻辑删除的实体字段名(since 3.3.0,配置后可以忽略不配置步骤2)
         logic-delete-value: 1 # 逻辑已删除值(默认为 1)
         logic-not-delete-value: 0 # 逻辑未删除值(默认为 0)
   ```

   

4. 运行测试

   ![image-20210620000738147](\assets\image-20210620000738147.png)

   可以看到，运行删除方法后，执行一个更新操作，将逻辑删除列的值改变

   查询的时候也会自动过滤被逻辑删除的字段



## 性能分析插件

在平时的开发中，会遇到一些慢sql。通过一些性能测试工具去查看这些sql，进行一些操作

MyBatisPlus也提供了性能分析插件，如果一条sql语句超过特定的事件，强制停止运行

注：在3.2.0以前的版本由MyBatisPlus内置，现在已经移除,更换为外置的`p6spy`组件

使用流程

1. 导入插件

   ```xml
   <dependency>
       <groupId>p6spy</groupId>
       <artifactId>p6spy</artifactId>
       <version>3.9.1</version>
   </dependency>
   ```

2. yml配置

   ```yaml
   spring:
     datasource:
       driver-class-name: com.p6spy.engine.spy.P6SpyDriver
       url: jdbc:p6spy:mysql://localhost:3306/....
   ```

3. 配置`spy.properties`

   ```properties
   #3.2.1以上使用
   modulelist=com.baomidou.mybatisplus.extension.p6spy.MybatisPlusLogFactory,com.p6spy.engine.outage.P6OutageFactory
   #3.2.1以下使用或者不配置
   #modulelist=com.p6spy.engine.logging.P6LogFactory,com.p6spy.engine.outage.P6OutageFactory
   # 自定义日志打印
   logMessageFormat=com.baomidou.mybatisplus.extension.p6spy.P6SpyLogger
   #日志输出到控制台
   appender=com.baomidou.mybatisplus.extension.p6spy.StdoutLogger
   # 使用日志系统记录 sql
   #appender=com.p6spy.engine.spy.appender.Slf4JLogger
   # 设置 p6spy driver 代理
   deregisterdrivers=true
   # 取消JDBC URL前缀
   useprefix=true
   # 配置记录 Log 例外,可去掉的结果集有error,info,batch,debug,statement,commit,rollback,result,resultset.
   excludecategories=info,debug,result,commit,resultset
   # 日期格式
   dateformat=yyyy-MM-dd HH:mm:ss
   # 实际驱动可多个
   #driverlist=org.h2.Driver
   # 是否开启慢SQL记录
   outagedetection=true
   # 慢SQL记录标准 2 秒
   outagedetectioninterval=2
   ```



## 条件构造器

在写一些复杂的sql的时候，就可以使用`Wrapper`它来替代

wrapper使用**链式编程**

#### 简单测试使用

```java
@Test
void contextLoads() {
    //查询name不为空的用户,并且邮箱不为空的用户,年龄大于等于20岁的
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    wrapper.isNotNull("name")
        .isNotNull("email")
        .ge("age",20);
    userMapper.selectList(wrapper).forEach(System.out::println);
}
```

执行后返回的sql

```sql
SELECT 
id,name,age,email,version,deleted,create_time,update_time
FROM user WHERE deleted=0 
AND (name IS NOT NULL AND email IS NOT NULL AND age >= 20)
```



#### 其它的使用方式

```java
@Test
void contextLoads2() {
    //查询特定的名字
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    wrapper.eq("name","maplef");
    User user = userMapper.selectOne(wrapper);
    //One是查询一个数据,出现多个结果用List或者Map
}

@Test
void contextLoads3() {
    //查询年龄在 20 - 25之内的用户量
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    wrapper.between("age",20,25);
    Integer integer = userMapper.selectCount(wrapper);
    //count,查询结果集数量
}

//模糊查询
@Test
void contextLoads4() {
    //查询名字中不包含
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //notLike表示不包含的模糊查询
    //likeRight/Left表示模糊查询的%号在左还是在右
    wrapper.notLike("name","f").
        likeRight("email","t");
    List<Map<String, Object>> maps = userMapper.selectMaps(wrapper);
    maps.forEach(System.out::println);
}


//子查询
@Test
void contextLoads5() {
    //查询年龄在 20 - 25之内的用户量
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //id在子查询中查处理
    wrapper.inSql("id","select id from where id<3");
    List<Object> objects = userMapper.selectObjs(wrapper);
    objects.forEach(System.out::println);
}


//排序
@Test
void contextLoads6() {
    //通过id降序排序
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    wrapper.orderByDesc("id");
    List<User> users = userMapper.selectList(wrapper);
    users.forEach(System.out::println);
}
```

小结：Wrapper的使用方法，和sql语句的其实差不太多，具体使用的时候，如果真遇到不知道的或是不清楚的，可以去官网看



## 代码自动生成器

dao、entity、service、controller全都自动生成

AutoGenerator 是 MyBatis-Plus 的代码生成器，通过 AutoGenerator 可以快速生成 Entity、Mapper、Mapper XML、Service、Controller 等各个模块的代码，极大的提升了开发效率。



MyBatis-Plus 从 `3.0.3` 之后移除了代码生成器与模板引擎的默认依赖，需要手动添加相关依赖：

```xml
<!--代码生成器依赖-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.4.1</version>
</dependency>

<!-- 默认模板引擎 -->
<dependency>
    <groupId>org.apache.velocity</groupId>
    <artifactId>velocity-engine-core</artifactId>
    <version>2.3</version>
</dependency>
```

生成配置编写

```java
import com.baomidou.mybatisplus.annotation.DbType;
import com.baomidou.mybatisplus.annotation.FieldFill;
import com.baomidou.mybatisplus.generator.AutoGenerator;
import com.baomidou.mybatisplus.generator.config.DataSourceConfig;
import com.baomidou.mybatisplus.generator.config.GlobalConfig;
import com.baomidou.mybatisplus.generator.config.PackageConfig;
import com.baomidou.mybatisplus.generator.config.StrategyConfig;
import com.baomidou.mybatisplus.generator.config.po.TableFill;
import com.baomidou.mybatisplus.generator.config.rules.DateType;
import com.baomidou.mybatisplus.generator.config.rules.NamingStrategy;

import java.util.ArrayList;

/**
 * 代码自动生成器
 */
public class MpalefCode {

    public static void main(String[] args) {
        //需要构建一个代码生成器对象
        AutoGenerator autoGenerator = new AutoGenerator();

        //配置策略
        // 1.全局配置
        GlobalConfig gc = new GlobalConfig(); //导包一定是mybatisplus.generator下
        String property = System.getProperty("user.dir");   //当前项目路径
        gc.setOutputDir(property+"/src/main/java")  //生成在当前项目中的:src/main/java路径下
                .setAuthor("Maplef")    //创建的作者名
                .setOpen(false) //创建完成是否打开windows的文件夹
                .setFileOverride(false) //是否覆盖
                .setServiceName("%sService")    //去掉service的I前缀
                .setDateType(DateType.ONLY_DATE)
                .setSwagger2(true);  //是否添加Swagger,添加就需要导入Swagger的依赖,不然生成后注解报错
        autoGenerator.setGlobalConfig(gc);

        //2、设置数据源
        DataSourceConfig dsc = new DataSourceConfig();
        dsc.setUrl("jdbc:mysql://localhost:3306/smbms?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8")
                .setDriverName("com.mysql.cj.jdbc.Driver")
                .setUsername("root")
                .setPassword("")
                .setDbType(DbType.MYSQL);   //连接数据库的参数,不赘叙

        autoGenerator.setDataSource(dsc);

        //3.包的配置
        PackageConfig pc = new PackageConfig();
        pc.setModuleName("demo")    //设置生成后的父包名
                .setParent("com.maplef")    //设置在上方总目录下,生成的位置,在这里设置后,生成的位置为 :   src/main/java/com/maplef/demo
                .setEntity("entity")
                .setMapper("mapper")
                .setController("controller")
                .setService("service");
                //设置各层级的包名
        autoGenerator.setPackageInfo(pc);

        //4.策略配置
        StrategyConfig strategy = new StrategyConfig();
        strategy.setInclude("t_user","smbms_user");   //设置表名,和数据库表名对应,填写多个参数即可一次性生成多张表
        strategy.setNaming(NamingStrategy.underline_to_camel);
        strategy.setColumnNaming(NamingStrategy.underline_to_camel);
        strategy.setRestControllerStyle(true);
        strategy.setLogicDeleteFieldName("deleted");//设置逻辑删除,参数与数据库列名相同

        //自动填充配置
        TableFill gmt_create = new TableFill("gmt_create", FieldFill.INSERT);
        TableFill gmt_modified = new TableFill("gmt_modified", FieldFill.INSERT_UPDATE);
        ArrayList<TableFill> tableFills = new ArrayList<>();
        tableFills.add(gmt_create);
        tableFills.add(gmt_modified);
        strategy.setTableFillList(tableFills);

        //乐观锁配置,参数与数据库列名相同
        strategy.setVersionFieldName("version");

        strategy.setRestControllerStyle(true);
        strategy.setControllerMappingHyphenStyle(true);


        autoGenerator.setStrategy(strategy);

        autoGenerator.execute();//执行
    }

}
```

运行后，获得如下内容：

![image-20210620155928483](\assets\image-20210620155928483.png)

小结：代码自动生成非常好用，自己写项目时推荐使用，但是在公司看情况。

​	在自动代码生成的配置不止这些内容，如果用到上方未设置的配置，去官方查看
