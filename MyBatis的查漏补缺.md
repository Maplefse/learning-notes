# MyBatis的查漏补缺

#### 1、Lombok的使用

1.  是一种 Java 实用工具，可用来帮助开发人员消除 Java 的冗长，尤其是对于简单的 Java 对象（POJO）。它可以通过注解来省略实体类中的get/set方法,toString方法等.....

2. maven依赖导入

   ```xml
       <dependency>
         <groupId>org.projectlombok</groupId>
         <artifactId>lombok</artifactId>
         <version>1.18.10</version>
       </dependency>
   ```

3. 偷懒专用,但一般不建议使用 

2、主要使用注解

1. @Data:自动实现无参构造、get、set、hashcode、equals
2. @AliArgsConstructor：自动实现有参构造
3. @NoArgsConstructor：自动实现无参构造
4. @ToString：自动生成ToString方法



#### 2、多对一处理

##### 

```java
//两个实体类

//学生实体类
public class Student{
    private Integer sid;
    private String sname;
    private Teacher teacher;
    //省略get/set方法
}

//老师实体类
public class Teacher{
    private Integer id;
    private Integer name;
    //省略get/set方法
}
```



  1. #####  按照查询嵌套处理

     ```xml
     
     	思路:查询所有的学生信息
     		根据查询出来的学生的tid.寻找对应的老师!子查询
     <select id="getstudent" resu1tMap="studentTeacher">
     		select  from student
     </select>
     <resu1tMap id="studentTeacher" type="student">
     	<result property="id" column="id" />
     	<result property="name" column="name" />
     	<!--复杂的属性，我们需要单独处理对象: associatio集合:collection -->
     	<association property="teacher" column="tid" javaType="Teacher" select="getTeacher" />
     </ resu1tMap>
     <select id="getreacher" resultType="Teacher">
     	select = from teacher where id = #{id}
     </select>
     
     ```

     当我们需要查询例如:多个学生的老师是同一个人的类似数据的时候,一般在实体类中添加一个引用类型的变量，通过这个变量获取老师的信息。但是一般情况下MyBatis自动映射无法获取老师的数据。这时候我们使用resultMap去手动配置映射。而复杂的数据我们对它进行单独的处理

     对象使用：association、集合使用collection

     ##### 2. 按照结果嵌套进行查询

     ```xml
     <select id="getStudent" resultMap="StudentTeacher">
     	select * from s.id sid,s.name sname,t.name tname
         from student s, teacher t
         where s.tid = t.id;
     </select>
     
     <resultMap id="StudentTeacher2" type="Student">
     	<result property="id" column="sid"/>	
         <result property="name" column="sname"/>	
         <association property="teacher" javaType="Teacher">			
             <result property="name" column="tname"/>
         </association>
     </resultMap>
     ```

#### 3.一对多处理

比如一个老师拥有多个学生,对于老师而言,就是一对多的关系

##### 

```java
//两个实体类

//学生实体类
public class Student{
    private Integer sid;
    private String sname;
    //省略get/set方法
}

//老师实体类
public class Teacher{
    private Integer id;
    private Integer name;
    private List<Student> student;
    //省略get/set方法
}
```

需求:获取某个老师及其所有学生的信息

```xml
<!--按结果嵌套查询-->
<select id="getTeacher" resultMap="">
	select sid,sname,tname,tid
    from student teacher
    where tid=id and id=#{id}
</select>

//对结果映射进行手动设置
<resultMape id="TeacherStudent" type="teacher">
	<result property="id" cloumn="tid"/>
    <result property="name" column="tname"/>
    <!-- 集合使用collection -->
    <collection property="students" ofType="Student">
    	<result property="id" column="sid"/>
        <result property="name" cplumn="sname"/>
        <result property="tid" column="tid"/>
    </collection>
</resultMape>
```

```xml
<!-- 按照查询嵌套处理 -->
<!-- 查询老师信息 -->
<select id="getTeacher" resultMap="">
	select * from teacher where id=#{id}
</select>

//对结果映射进行手动设置
<resultMape id="TeacherStudent" type="teacher">
	<result property="id" cloumn="tid"/>
    <result property="name" column="tname"/>
    <!-- 集合使用collection -->
    <collection property="students" javaType="ArrayList"  ofType="Student" select="getStudentByTeacherId" column="id">	
    </collection>
</resultMape>

<!--查询学生信息-->
<select id="getStudentByTeacherId" resultType="Student">
	select * from student where tid=#{id}
</select>
```

##### 小结

	1. 关联 - association (多对一)
	2. 集合 - collection (一对多)
	3. javaType & ofType
	  	1. javaType 用来指定实体类中属性的类型
	  	2. ofType 用来指定映射到List或者集合中的pojo类,泛型中的约束类型(引用类型)



#### 4、动态SQL

##### 	if标签

​		if标签等于java的if判断具体使用

```xml
<if test="1=1">
	and 1=1
</if>
```

#####  choose

​	类似于java中的switch语句

```xml
<choose>
	<when test="1=1">
    	sql语句
        <!--和java中的case代码块效果类似-->
    </when>
    <when test="1=2 and 1=1 ">
        sql语句
    </when>
    <otherwise>
    	sql语句
        <!--当所有when标签都不满足条件的时候则进入此标签-->
    </otherwise>
</choose>

<!--这个标签永远只会满足一个条件,当满足条件之后自动跳出整个标签-->
```

##### where

1. where标签只会在至少有一个子元素的条件返回SQL子句的情况下插入where语句,同时如果语句的开头是AND或者OR,where会自动将它们去除
2. where一般放在在所有判断标签的最外面

```xml
<where>
	<if></if>
    <choose>
    	<when></when>
        <otherwise></otherwise>
    </choose>
</where>
```

##### set

	1. set会自动给SQL语句添加SET

```XMl
<set>
	<if></if>
    <if></if>
</set>
```

##### trim

```xml
<trim prefix="" prefixOverrides="" suffix="" suffixOverrides="">
	
</trim>
```



​	





