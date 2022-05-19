# Java

## 标识符

在Java中，标识符又可以称为变量名，声明变量名有以下注意点：

1. 所有的变量名只能以（A-z）或$，或下划线_开头
2. 不能使用关键字作为变量名或者方法名
3. 标识符**大小写敏感**
4. 可以使用中文命名

## 数据类型

Java是强类型语言，它要求变量的使用要严格的符合规定，所有的变量都必须先定义后才能使用

Java的数据类型主要分为两大类

1. 基本类型
2. 引用类型

### 基本类型

基本类型又有数值类型与boolean类型

数值类型主要有以下几种

- 整数类型
  - `byte`占1个字节范围，容纳范围为：-128 - 127
  - `short`占2个字节范围，容纳范围为：-32768 - 32767
  - `int`占4个字节范围，容纳范围为：-2147483648 - 2147483647
  - `long`占8个字节范围，容纳范围为：-9223372036854775808 - 9223372036854775807
    - 一般在定义`long`的时候，要在数字后面加上"L"以便和`int`进行区分
  
- 浮点类型（即为小数点类型）
  - `float`占4个字节范围，范围从10^-38到10^38 和 -10^38到-10^-38
    
    - float为单精度浮点型
    - **float类型定义的数据，末尾必须有"f"或者"F"以便和double进行区分**
    
  - `double`占8个字节范围，范围从10^-308到10^308 和 -10^-308到-10^-308
    
    - double为双精度浮点型
    
  - ```java
    //浮点数精数丢失
    
            float f = 0.1f;
            double d = 0.1;
    
            System.out.println(f==d); //false
            System.out.println(f);
            System.out.println(d);
    
            float d1 = 648641357465132f;
            float d2 = d1+1;
    
            System.out.println(d1 == d2);//true
            //浮点数是有限的离散数,
            //double与float的精度不同,接近,但不等于
            //所以,最好避免使用浮点数进行比较
    ```
  
    
  
- 字符类型
  - char占2个字节，可以存储单个中文字符
  
  - ```java
    //char类型字符转换
            //字符类型强制转换
            char c1 = 'a';
            char c2 = 'A';
            char c3 = '中';
            System.out.println(c1);
            System.out.println(c2);
            System.out.println(c3);
            //将字符类型强制进行转换
            System.out.println((int)c1);
            System.out.println((int)c2);
            System.out.println((int)c3);
    /**
    输出:
        a
        A
        中
        97
        65
        20013
    */
    //所有的字符本质还是数字
    //通过ASCII编码表进行转换,例如97 = a
    ```
  
    
  
- boolean类型
  - 占1位
  - 它只有两个值"true"和"false"，代表是与非

### 引用类型

Java中，对所有的数据类型都进行了包装，包装成类。



## 类型转换

 由于Java是强类型语言，所以不同类型在进行运算的时候，需要用到类型转换。

运算中，不同类型的数据先转化成同一类型，然后再进行运算。

**转换优先级由所占内容大小，从低到高进行转换**

```java
byte -> short -> char -> int -> long -> float -> double
//小数的优先级一定大于整数,因为浮点数的范围一定比整数大
    
//从高到低进行转换需要强制类型转换,例如
int i = 128;
byte b = (byte)i;
//否则会进行报错

//注意点
//从低到高进行转换则会自动进行转换
//无法对boolean进行转换
//无法将对象类型转换为不相干的类型
//转换时可能出现内存溢出或是精度问题

//精度问题
system.out.println((int)25.5)//输出结果:25，当把小数转换为整数的时候，会自动舍弃掉小数点后的数。
    
    
    
```

#### JDK7的新特性

```java
//在JDK7之后,数字之间可以使用下划线分割
int money = 10_0000_0000;
int year = 18;
int sum = money*18;
//两个不同类型的数据在计算之前,会先进行转型操作再开始计算
//在这里,两个int相乘,已经超过21e造成了内存溢出问题,即使用long来接收也是内存溢出后的数字
long sum2 = money * year;

//而在这里,将18先转换为long类型,由于在计算前优先进行类型转换操作
//且低类型自动向高类型转换,因此得到正常结果:1800000000
long sum3 = money * ((long)year);

System.out.println(money);
System.out.println(sum);    //输出结果820130816
System.out.println(sum2);   //输出结果820130816
System.out.println(sum3);   //输出结果1800000000
```



## 什么是字节

- 位(bit)：是计算机内部数据存储的最小单位，11001100是一个八位二进制数
- 字节（byte）：是计算机中数据处理的最级别单位，一般用大写B来表示
  - 1B（byte，字节） = 8bit（位）
- 字符：指计算机中使用的字母，数字，符号等



- 1bit表示1位
- 1Byte表示一个字节
- 1024B=1kb
- 1024KB = 1M
- 1024M = 1G

## 变量

变量：就是可以变化的量

Java是强类型语言，每个变量都必须声明其类型

Java变量是程序中最基本的存储单元，其要素包括变量名，变量类型和作用域

**注意：**

- 每个变量都要有类型，类型可以是基本类型，也可以是引用类型
- 变量名必须是合法的标识符
- 变量声明是一条完整的语句，因此每个声明都必须以分号( ;)结束

```java
//变量的基本声明方法
String  s   = "演示";
//类型 变量名 =   值 ;
```

### 变量的几种类型

1. 局部变量

   ```java
   public void test(){
       //局部变量
       int i;
       i = 1;
       System.out.println(i);
       /*
       局部变量声明在方法中,它只能在这个方法中使用。
       当方法结束，变量的生命周期也跟着结束
       */
       /*
       注意:局部变量声明时可以不用赋值.
       当它被调用的时候,这个变量一定被初始化过值
       否则无法调用,程序编译报错!!!
       */
   }
   ```

   

2. 实例变量

   ```java
   public class 变量 {
   
       //声明一个实例变量
       String  s   = "演示";
       
       public static void test(){
           System.out.println(s);	//程序报错
           
           变量 变量 = new 变量();
           System.out.println(变量.s);//正常运行输出:演示
       }
       
       public void test1(){
           System.out.println(s); 	//程序正常运行
       }
       
       /*
       实例变量声明在类中,方法外
       实例变量可以被普通的方法进行调用,无法被static修饰过的静态方法进行调用
       被static修饰过的静态方法只有实例化这个方法才能对实例变量进行调用
       它的声明周期和本类的实例相同,当这个类的实例被创建的时候,它跟着被创建,当实例被销毁的时候跟着销毁
       */
   }
   ```

   

3. 静态变量

   ```java
   //静态变量同实例变量的声明位置一样,但是类变量在声明前添加static进行修饰
   //它随着类一起生成,一起消失
   
   public class 变量 {
   
       //声明一个静态变量
       static String  s   = "演示";
       
       public static void test(){
           System.out.println(s);	//静态变量可以被静态方法直接调用
           
       }
       
       public void test1(){
           System.out.println(s); 	//正常运行
           //也可以被普通方法直接调用
       }
   }
   ```



## 常量

常量，即声明之后无法被变更的数据

```java
//常量使用final进行修饰
final double PI = 3.14;
//常量在定义的时候,常量名通常使用大写
//当常量被声明之后,它无法被修改!!
```



### 变量命名规范

- 所有的变量、方法、类名:**见名知意**!
- 类成员变量、局部变量：遵循驼峰命名，首字母小写：`userName`
- 常量：全大写与下划线：`MAX_VALUE`
- 类名：遵循驼峰命名，首字母大写：`UserName`
- 方法名：遵循驼峰命名，首字母小写：`test()`



## 运算符

**在java中同样遵循数学的优先级判断：从左往右开始计算，先乘除，后加减，有括号优先计算括号内**

Java中，运算符分为几个类型

- 算数运算符：+、-、*、/、%、++、--

  ```java
  //算数运算符和数学中没什么区别
  //%为取余的意思
  //注意++与--
  public static void main(String[] args) {
  
      int i1 = 10;
      int i2 = 20;
      int i3 = 33;
      int i4 = 44;
  
      System.out.println(i1+i2); //结果为30
      System.out.println(i1-i2); //结果为-10
      System.out.println(i1*i3); //结果为300
      System.out.println(i1/i2); //结果为0
      System.out.println(i3%i1); //结果为3
      //在这里33%10获取他们的余数,使用33除以10一次,剩下一个3,这个3就是余数
      
      System.out.println(i3++);  //结果为33
      System.out.println(i4--);  //结果为44
      //i3++就等于 i3+1,自己给自己本身+1,--也是
      //唯一要注意的是,++与--在变量前后的不同
      //在变量后面,为先用再+/-
      //在变量前面,为先+/-再用
      //例如:b=a++,就是先将b=a,再让a进行++操作
      //++放在前面就是先对a进行++再赋值给b
      
      int i5 = 11;
      int i6 = 22;
  
      System.out.println(++i5);   //结果为12
      System.out.println(--i6);   //结果为21
      
  
      //很多数学的运算,会使用一些工具类来帮助实现
      //Math就是Java帮助我们封装好的运算工具类
      
      
      
  }
  ```

  注意点：**+号在基本数据类型中表示数学中的+法，而在对字符串使用则代表字符串连接符，它将+号左右两边的字符串进行连接（只要有一边为字符串，另一边都会当成字符串处理）**。但是他依旧遵循从左往右的先后顺序

- 关系运算符：>、<、>=、<=、== 、!=

  ```java
  //关系运算符只会返回一个boolean值,也就是true和false
  //以上的运算符和数学中用法相同
  /*
  > 大于
  < 小于
  >= 大于等于
  <= 小于等于
  == 相等
  != 不相等
  */
  ```

  

- 逻辑运算符:&&、||、！

  ```java
  //逻辑运算符
  //逻辑运算符有三种
  // &&  ||  !   也称:与,或,非
  //当&&左右两遍的值都为true时,会返回true
  //当||左右两边的值,只要有一个为true时,就会返回true,
  //!对后面的值进行取反操作
  
  //注意,&&与||都是短路运算符
  //短路运算符的意思是,当&&前面的值为fales时,&&就会直接停止计算,不会继续执行&&后面的代码
  //而||当前面的值为true时,就不会再执行后面的代码
  
  boolean t = true;
  boolean f = false;
  
  System.out.println("a && b :"+ (t && f) );  //输出:a && b :false
  System.out.println("a || b :"+ (t || f) );  //输出:a || b :true
  System.out.println("!(a && b) :"+ !(t && f) ); //输出!(a && b) :true
  
  
  //与短路运算符相对应的就是非短路运算符
  // & 与 |
  //不管情况如何,程序一定会执行前后的代码!!
  ```

  

- 位运算符：&、|、^、~、>>、<<、>>>

  ```java
  //一般情况下&和|又被叫做非短路运算符
  //它们会对前后两边的数都进行计算再得出boolean值
  
  /*
      A = 0011 1100
      B = 0000 1101
  
      ---------------
  
      A&B = 0000 1100 //对二进制数进行对比,当左右两边的位数相同,且为1时,得到1
      A|B = 0011 1101 //对二进制数进行对比,当左右两边的位数相同,且都为0,得到0,否则得1
      //可以理解为对二进制数的每一位进行&&和||比较并得出值
      A^B = 0011 0001 //对二进制数进行对比,当左右两边的位数相同,且值相同则为0,否则为1
      ~B = 1111 0010  //就是对&的取反操作
  
  
      ----------------
      2*8 = 16 (2*2*2*2)
  
      <<   表示在二进制的情况下,位数往左位移一位。在数学中就代表 *2
      >>   表示在二进制的情况下,位数往右位移一位。在数学中就代表 /2
      >>和<<对数进行操作的时候,需要在后面添加一个数字
  
      记住:二进制位数往左位移一位代表*2,右位移一位代表/2
  
      因为是直接对二进制数进行操作,所以它的效率极高!!!!!
       */
  
  public static void main(String[] args) {
  
      System.out.println(2<<3);//结果:16
      //例如这里,就代表二进制位数往左位移3位,在数学中就表示 *2*2*2
      System.out.println(1<<4);//结果:16
  }
  ```

  

- 条件运算符：? :

  ```java
  //也称为三目运算符
  // x ? y : z
  //如果x为true,则结果为y,否则为z
  //也就是简略了if判断
  
  int score = 80;
  String type = score < 60 ? "不及格" : "及格";
  
  System.out.println(type)  //输出结果为及格
      
  //注意:使用三目运算符,前面一定要有变量对它进行接收!!
  ```

  

- 拓展赋值运算符：+=、-=、/=、*=

  ```java
  //+=、-=、/=、*=
  //这4个运算符其实就等于对值的本身进行+,-,*,/操作再赋值
  //例如
  a += b
  //它就相等于 a = a+b
  a -= b	//等于 a = a-b
  //加减乘除都是一样的用法
  ```

  

## Scanner对象

Scanner是Java5的新特性，可以通过Scanner类在控制台获取用户的输入

基本语法：

```java
Scanner s = new Scanner(System.in);
```

通过Scanner类的`next()`与`nextLine()`方法获取输入的字符串,在读取前一般需要使用`hasNext()`与`hasNextLine()`判断是否还有输入的数据



Scanner使用：

```java
public static void main(String[] args) {
    //创建一个扫描器对象，用于接受键盘数据
    Scanner scanner = new Scanner(System.in);

    System.out.println("使用Scanner接收用户输入内容:");
    //判断用户有没有输入字符串
    //假设现在程序运行,在控制台输入hello world
    if (scanner.hasNext()){
        String str = scanner.next();
        System.out.println(str);	//输出hello
    }
    
    if (scanner.hasNext()){
        String str = scanner.nextLine();
        System.out.println(str);	//输出hello world
    }
    
    //造成输出内容不同的原因在于:
    //next():
    //一定要读取到有效字符后才可以结束输入
    //对输入的有效字符之前遇到的空白,会自动进行省略。
    //对输入的有效字符之后的空白,会将其视为分隔符或结束符。
    //所以next()不能得到带空格的字符串
    
    //nextLine():
    //它将Enter视为结束符,也就是说nextLine()会获取输入回车之前的所有字符
    //也能获取到空白
    

    //凡是属于IO流的类,如果不关闭就会一直占用空间!
    scanner.close();

}
```





## if判断

if，在Java中它用来判断 条件从而决定接下来执行的内容

if最的结构为`if(){}`。括号中必须要存在一个Boolean值，当括号中的条件为true时，将执行{}中的代码，否则就跳过{}中的内容，继续往下执行代码

```java
//简单的if使用
public static void main(String[] args) {

    Scanner scanner = new Scanner(System.in);
    String s = scanner.nextLine();

    //使用控制台接收输入内容
    //在这之中判断接收到的内容是否为hello
    if (s.equals("hello")){
    	System.out.println(s);
        //当输入的内容为hello时,才会进入到这个大括号里面执行这条输出语句
    }
    scanner.close();

}
```

除了最简单的if结构,在{}的后面还能增加一个else{}。当if判断为false时就会进入else中执行代码。

```java
if(boolean表达式){
    //如果表达式为true执行这里的代码
}else{
    //如果表达式为false执行这里的代码
}
```

在else之后还有进阶版else if（）{}

```java
if(boolean表达式){
    //如果表达式为true执行这里的代码
    //为false则往下执行else if
}else if(boolean表达式){
    //如果表达式为true执行这里的代码
    //为false则继续往下执行
    //可以有无限个else if,但只能有一个if和else
}else{
    //在if(){}esle if(){}结构中,else可以自由的添加,删除
    //只有当if和else if()全部条件都不满足时,才会进入到else代码中
}
```

同时，在if结构中{}里面也能嵌套无限个if结构



## Switch结构

switch case 语句通常用于判断一个变量与一堆数据中的某个值是否相等，每个值都称为一个分支

switch括号中的变量类型可以是：byte、short、int、char、enum或者String

case后的值必须为一个字符串常量或者字母量

```java
//switch结构
switch(value2){
    case value1 :
        //代码内容
        break;//可写可不写
    case value2 :
        //代码内容
        break;//可写可不写
    default :	//可写可不写
        //代码内容
}
//以上就是一个最基本的switch结构
//它会拿括号中的value2去和case后的value从上到下轮流比对
//当比对结果相同时,就会执行:号后的代码内容。执行完成之后则会判断有无break;语句,有则跳出switch结构,没有则会将该case之后的case代码块全部输出!!
//所以为了代码规范,通常都会在case后加上break
//如果没有case的值相同,且写了default代码块的情况下,就会执行default中的内容
//
```

switch通常被用来代替大量的if else判断。大量的if else会造成代码可读性差，此时就可以使用switch来代替。



switch变形：

```java
//switch变形结构:
switch(value2){
    case value1 :
    case value2 :
        //代码内容1
        break;//可写可不写
    case value3 :
        //代码内容2
        break;//可写可不写
    default :	//可写可不写
        //代码内容
}

//这是一种switch的另类用法,当value1和value2满足其中一个,都会执行代码内容1的代码
```



## 循环

### while循环

while循环是java中最基本的循环，它的结构为：

```java
while(布尔表达式){
    //循环内容
}

//只要boolean表达式为true,它就会一直循环下去
```

### do....while循环

while循环只有在满足条件的情况下才会进入循环，而do...while不同，它会直接循环一次，然后再进行条件的判断，成立才继续循环

```java
do {
    //循环内容
}while(布尔表达式);

//while先判断后执行,do while先执行一次后判断
```

### for循环

虽然while与do...while已经可以完成所有的循环操作，但是java中有更方便快捷的for循环可以使用

for循环是支持迭代的一种通用结构，是最有效、最灵活的循环结构

```java
for循环执行的次数在执行前就确定的，语法如下:
for(初始化;布尔表达式;更新){
    //代码内容
}

//for循环的结构由3个参数与两个;号组成。
//for循环的3个参数是可选内容,而两个;号不可缺少!因此我们可以这么使用for循环
for(;;){
    //这就是一个死循环,等于while(true)
}
```

**idea中可以使用`100.for`+回车快速感应出一个循环100次的for循环**



## break与continue

- 在任何循环语句的主体部分，均可使用break控制循环的流程。break用于强行退出循环，停止循环中剩余的语句。也可用于switch语句
- continue在循环语句体重，用于终止某次循环过程，即跳过本次循环接下来的内容，直接执行下一次是否循环的判定。



## 方法

Java中的方法类似于其它语言的函数,是一段用来完成特定功能的代码片段，一般情况下，定义一个方法包含以下语法：

**声明方法时，最好保证一个方法只做一件事，即为保证方法的原子性**，方便对方法的修改

- 方法包含一个方法头和一个方法体，下面是一个方法的所有部分：

  - 修饰符：修饰符是一个可选的内容，告诉编译器如何调用该方法，定义了该方法的访问类型
  - 返回值类型：方法可能会返回值。returnValueType是方法返回值的数据类型，在没有返回值的情况下，returnValueType则为关键字void
  - 方法名：是方法的实际名称，方法名和参数表共同构成方法签名
  - 参数类型：参数像是一个占位符，放方法被调用时，传递值给参数。这个值被称为实参或者变量。参数列表是指方法的参数类型、顺序和参数的个数。参数是可选的，方法可以不包含任何参数。
    - 形式参数：在方法被调用时用于接收外界输入的数据
    - 实参：调用方法时实际传给方法的数据
  - 方法体：方法体包含具体的java代码，表示该方法的功能

  ```java
  修饰符 返回值类型 方法名(参数类型 参数名,参数类型 ....){
      方法体
      return 返回值
      //返回值的类型要与返回值类型相同
      //当返回值类型为void时,不需要return语句
  }
  ```

### 方法的重载

重载，就是在一个类中，有相同的方法名，但参数列表不同的函数。

方法重载的规则：

- 方法名必须相同。
- 参数列表必须不同（个数不同，类型不同、参数排列顺序不同等）。
- 方法的返回值类型可以相同也可以不同
- 仅返回值类型不同不足以成为方法的重载

实现理论：

- 方法名称相同时，编译器会根据调用方法的参数个数，参数类型等去逐个匹配，以选择对应的方法，如果匹配失败，则编译器报错。



## 可变参数

从JDK1.5开始，java支持传递同类型的可变参数给一个方法

在方法声明中，在指定参数类型后面加一个省略号。

一个方法只能指定一个可变参数，它必须是方法的最后一个参数，任何普通参数都必须在他之前声明。

```java
//创建一个排序方法,因为不清楚需要对多少数字进行排序,在参数列表中声明一个可变参数。接收任意数量的double类型参数
public void printTest(double... numbers){
    if(numbers.length ==0){
        System.out.println("No argument passed");
        return;
    }
    double result = numbers[0];
    
    //排序，获取最大的数字
    for (int i = 1; i< numbers.length; i++){
        if(numbers[i] > result){
            result = numbers[i];
        }
    }
    
    System.out.println("The max value is"+ result);
}
```



## 递归

**递归用白话解释就是：自己调用自己**

利用递归可以用简单的程序来解决一些复杂的问题。它通常把一个大型复杂的问题层层转化为一个与原问题相似的规模较小的问题来求解，递归策略只需少量的程序就可描述出解题过程所需要的多次重复计算，大大地减少了程序的代码量。递归的能力在于用有限的语句来定义对象的无限集合

递归结构包括两个部分：

- 递归头：什么时候不调用自身方法，如果没有头，将陷入死循环
- 递归体：什么时候需要调用自身方法。

```java
//一个简单的递归操作
    public static void main(String[] args) {
        //获取5的阶乘
        System.out.println(f(5));//值为120
    }

//阶乘值一个数从它自身开始从大到小依次相乘,直到1为止
//例如5的阶乘就是:5*4*3*2*1

    public static int f(int n){
        if (n==1){
            return 1;
        }else{
            return n*f(n-1);
        }
        //程序从传进来的5开始递归操作,直到参数为1的时候返回参数1
        //然后值依次从最里面的方法往外传递并计算
        //依次计算顺序为:
        //	2*1 -> 3*2 -> 4*6 -> 5*24 = 120
    }
```



## 数组

### 数组的定义

- 数组是相同类型的有序集合
- 数组描述的是相同类型的若干个元素，按照一定的先后次序排列组合而成
- 其中，每一个数据称作一个数组元素，每个数组元素可以通过一个下标来访问他们

### 声明数组

数据必须要进行声明才能使用

```java
//声明数组的语法

//dataType:变量类型
//arraySize:数组长度
dataType[] arrayRefVAr;		//首选声明方法

dataType arrayRefVar[];		//效果相同,但是不推荐此声明方式

//java中,数组通过new来创建

//一个完整的声明数组语法
dataType[] arrayRefVar = new dataType[arraySize];

//存储在中数组的元素通过索引(下标)来访问,索引从0开始
//当声明数组长度后,不对其进行赋值,数组会按照对应的数据类型给予对应的默认值

//使用数组
arrayRefVAr[0] = 1; //对数组下标为0的元素赋值
int i = arrayRefVAr[0]; //拿取数组下标为0的值

```

### 数组的三种初始化方式

- 静态初始化

  ```java
  int[] a = {1,2,3};
  Man[] mans = {new Man(1,1),new Man(2,2)};
  ```

- 动态初始化

  ```java
  int[] a = new int [2];
  a[0] = 1;
  a[1] = 2;
  ```

- 数组的默认初始化

  - 数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也按照实例变量同样的方式被隐式初始化（也就是给变量初始默认值）

## 多维数组

- 多维数组可以看成是数组的数组，比如二维数组就是一个特殊的一维数组，其每一个元素就是一个一维数组，简单来说就是数组中的值又是一个数组

- `int a[][] = new int[2][5]` 二维数组声明。这个二维数组可以看成一个两行五列的数组。如下：

  - ![image-20211116004904542](\assets\image-20211116004904542.png)

- ```java
  int [][] array = {{1,2,3,4,5},{1,2,3,4,5}}	//声明一个二维数组
  
  ```

## Arrays类

Arrays是java中的一个数组的工具类，由于数组对象本身并没有什么便捷方法可以使用，但API中提供了Arrays工具类给我们，可以对数组进行一些基础的操作

Arrays中中都是static修饰的静态方法，因此可以直接通过类名调用

```java
public static void main(String[] args) {
        int [] a = {1,2,6,7,3,4,5};
        System.out.println(a);//输出内存地址

        System.out.println(Arrays.toString(a));//打印数组元素Arrays.toString()

        Arrays.sort(a); //对数组进行排序
        System.out.println(Arrays.toString(a));
    }

/*
常用的Arrays方法
	1.fill()方法,给数组赋值
    2.sort()方法,按升序对数组排序
    3.equals()方法,比较数组中的元素值是否相等
    4.binarySearch()方法,能对排序好的数组进行二分查找法操作
*/
```

## 冒泡排序

```java
//冒泡排序
    //比较数组中两个相邻的元素,如果第一个数比第二个数大或小,就交换他们的位置
    //每一轮比较,就会产出一个最大或者最小的数组
    //下一轮循环就减少一次排序次数
    //依次循环直到结束

    public static void main(String[] args) {

        
        int[] array = {5,2,6,1,4,6,2,8,9};
        int temp = 0;
        //外层循环,判断循环需要进行多少次
        for (int i = 0; i < array.length-1; i++) {
            //内层循环进行数字交换
            for (int j = 0; j < array.length-1-i; j++) {
                if (array[j+1]>array[j]){
                    temp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = temp;
                }
            }

        }
        System.out.println(Arrays.toString(array));
    }
```

## 稀疏数组

当一个数组中大部分元素为0，或者为同一值的数组时，就可以使用稀疏数组来保存该数组

稀疏数组的处理方式是：

- 记录数组一共有几行几列，有多少个不同值
- 把具有不同值的元素和行列及值记录在一共小规模的数组中，从而缩小程序的规模

如下图：左边是原始数组，右边是稀疏数组

![image-20211118000048306](\assets\image-20211118000048306.png)

### 稀疏数组的生成，使用以及还原

```java
    public static void main(String[] args) {
        //1.创建一个二维数组, 11*11大小 0:没有棋子, 1:黑棋, 2:白棋

        int[][] array1 = new int[11][11];
        array1[1][2] = 1;
        array1[2][3] = 2;

        //输出原始的数组
        System.out.println("输出声明的数组");

        for (int[] ints : array1) {
            for (int anInt : ints) {
                System.out.print(anInt+"\t");
            }
            System.out.println();
        }

        //转换为稀疏数组保存
        int sum = 0;
        for (int i = 0; i < 11 ; i++) {
            for (int j = 0; j < 11; j++) {
                if (array1[i][j]!=0){
                    sum++;
                }
            }
        }
        System.out.println("有效值的个数:"+sum);

        //2.创建一个稀疏数组
        int[][] array2 = new int[sum+1][3];

        array2[0][0] = 11;
        array2[0][1] = 11;
        array2[0][2] = sum;

        //遍历二维数组,将非0的值存放到稀疏数组
        int count = 0;
        for (int i = 0; i < array1.length ; i++) {
            for (int j = 0; j < array1[i].length ; j++) {
                if (array1[i][j]!=0){
                    count++;
                    array2[count][0] = i;
                    array2[count][1] = j;
                    array2[count][2] = array1[i][j];
                }
            }
        }

        //3.打印稀疏数组
        System.out.println("============打印稀疏数组===========");
        for (int i = 0; i < array2.length ; i++) {
            System.out.println(array2[i][0]+"\t"+array2[i][1]+"\t"+array2[i][2]+"\t");
        }


        System.out.println("============还原稀疏数组===========");
        //读取稀疏数组的值
        int[][] array3 = new int[array2[0][0]][array2[0][1]];

        //给其中的元素还原它的值
        for (int i = 1; i < array2.length ; i++) {
            array3[array2[i][0]][array2[i][1]] = array2[i][2];
        }

        //打印还原的数组
        for (int[] ints : array3) {
            for (int anInt : ints) {
                System.out.print(anInt+"\t");
            }
            System.out.println();
        }

    }


```

### 输出结果

![image-20211118002638025](\assets\image-20211118002638025.png)

简单点来说：稀疏数组就是二维数组中，如果有大量的重复数据或者无效数据，**将数组中的有效数据和数量，以及坐标（下标）记录成一个新的二维数组**，通过数组转换的时间来换取数据存储的空间。

稀疏数组的头（第一行）存储二维数组的大小以及有效数据数量，下面则存储数据坐标以及值



## 面向对象

- 面向对象编程（Object-Oriented Programming，OOP）
- 面向对象编程的本质就是：以类的方式组织代码，以对象的方式组织数据。
- 抽象
- 三大特性：
  - [封装](#封装)
  - [继承](#继承)
  - [多态](#多态)
- 从认证论角度考虑是先有对象后有类。对象，是具体的事物。类，是抽象的，是对对象的抽象
- 从代码运行角度考虑是先有类后有对象。类是对象的模板。

### 封装

java程序设计追求`高内聚，低耦合`。高内聚就是类的内部数据操作细节自己完成，不允许外部干涉；低耦合：仅暴露少量的方法给外部使用。

通常，应禁止直接访问一个对象中数据的实际表现，而应通过操作接口来访问，这称为信息隐藏，也就是将类的属性进行私有化限制，由这个类提供对外的访问接口，限制外部的输入内容从而达到保护系统安全的功能

#### 封装的作用

1. 提高程序的安全性，保护数据
2. 隐藏代码的实现细节
3. 统一接口
4. 提高系统的可维护性

### 继承

继承的本质是对某一批类的抽象，从而实现对现实世界更好的建模

extends的意思是`扩展`。子类就是对父类的拓展，**也就是说子类可以使用父类的所有非私用属性与方法，同时子类还可以在其基础上进行拓展**。就如同现实中的父子关系，子继承父的基因，在其之下又会有新的个性

java中只有单继承，没有多继承。

**在java中，所有的类都默认继承object类，也就是说object类是所有类的父类**。

继承就是类和类之间的一种关系。除此之外，类和类之间的关系还有依赖、组合、聚合等

继承关系中的两个类，继承类称为子类，被继承类称为父类。子类继承父类使用关键字extends来表示。

### 方法重写

```java
//创建一个main方法调用重写后的子类与父类
public static void main(String[] args){
    B a = new A();
    a.test();	//输出:调用了A方法
    a.statictest(); //输出:调用了静态A方法
    
    B b = new A();
    b.test();	//输出:调用了A方法
    b.statictest;	//输出:调用了静态B方法
}
```

声明两个类，A类继承于B类

```java
public class A extends B{
    public void test(){
        System.out.print("调用了A方法")
    }
    
    public static void statictest(){
        System.out.print("调用了静态A方法")
    }
}
```

```java
public class B{
    
    @Override
    public void test(){
        System.out.print("调用了B方法")
    }
    
    public static void statictest(){
        System.out.print("调用了静态B方法")
    }
}
```

为何会出现静态方法与非静态方法调用输出结果不同的情况?

因为静态方法是类的成员，而非静态方法是对象的成员。

java在声明`B b = new A();`先声明了B，再由B的b去引用A，java会去找B是否有静态方法，**如果有static方法则直接调用B的static静态方法，因为b是由B类定义的。没有static时，b就会去调用对象的方法，而b是A对象的引用，所以调用的就是A的对象方法**

**所以重写跟静态方法没有关系，当子类和父类有相同方法名，相同参数列表的公开非静态方法时，就称之为重写**

子类对父类的重写，子类的重写方法修饰符权限只能大于等于父类

### 多态

- 即java中同一个方法可以根据发送对象的不同而采用多种不同的行为方式。

- 一个对象的实际类型是确定的，但可以指向对象的引用的类型有很多。也就是**父类引用指向子类对象**

- 多态的存在条件
  - 有继承关系
  - 子类重写父类方法
  - 父类引用指向子类对象
- 多态指方法的多态，属性没有多态性

```java
pulic void main(String[] args){
    Student s1 = new Student();
    Person s2 = new Student();
    Object s3 = new Student();
    
    //子类重写了父类的方法,执行子类的方法
    s1.run();	//正常输出son
    s2.run();	//正常输出son
    
    //Stuent能够调用自己或是继承、重写的父类方法
    s1.eat(); 	//正常输出eat
    s2.eat();	//编译报错
    //父类型可以指向子类,但是无法调用子类的方法,Person父类没有eat方法,编译直接报错
    
    //对象能够执行哪些方法,主要在于左边的类型!
    
}
```

```java
public class Student extends Person{
    
    @Override	//重写父类方法
    public void run(){
        System.out.println("son");
    }
    
    public void eat(){
        System.out.println("eat");
    }
    
}
```

### instanceof 

- instanceof用于判断一个变量指向的实例是否是指定类型对象，或是这个对象的子类

```java
pulic void main(String[] args){
    //    			父 > 子
    // Object > Person > Student
    Object object = new Student();
    System.out.println(object instanceof Student);//true
    System.out.println(object instanceof Student);//true
    System.out.println(object instanceof Person);//true
    System.out.println(object instanceof String);//false
    System.out.println(object instanceof Teacher);//false
}
```

instanceof会对左右两边的变量判断是否有线性父子关系，如果有则为true，没有则是false。左右两边比较前会先进行判断，左边能不能转换为右边的类型，如果不能则编译报错！

### 内部类

- 内部类就是在一个类里面再定义一个类，比如：A类中定义一个B类，那么B类就是A类的内部类，而A类相对于B类来说就是外部类了。
- 成员内部类
- 静态内部类
- 局部内部类
- 匿名内部类



声明内部类的实现

```java
public calss Outer{
    private int id = 1;
    private void out(){
        System.out.println("这是外部类的方法");
        
        //声明一个局部内部类
        class Inner2{
            
        }
        
    }
    
    //声明一个成员内部类
    public class Inner{
        public void in(){
            System.out.println("这是内部类的方法");
        }
        
        //内部类可以直接获得外部类的私有化属性
        public void getId(){
            System.out.println(id);	//输出1
        }
    }
}

//一个Java类中还可以写多个class类,但是只能有一个类被public修饰
class A{
    
}
```

如何使用内部类?

```java
public class Application{
    public static void main(String[] args){
        Outer outer = new Outer();
        //内部类的实例要通过外部类来实现
        Outer.Inner inner = outer.new Inner();	//实例化内部类
    }
}
```





## Java内存简单分析

堆：存放new的数组和对象       ->通过内存地址调用到栈区中的数据

栈：存放基础数据类型和引用变量

### 创建数组内存简单分析

![image-20211028003541895](\assets\image-20211028003541895.png)

java内存可以简单的分为图中三种

![image-20211028004319623](\assets\image-20211028004319623.png)

当数组被声明时，它先是在栈区开辟一个空间，随着数组被创建，java就在堆区中声明空间存储数组的值，将数组栈区的空间引用内存地址到堆区。

### 创建对象内存简单分析



## Java技巧

1. 在cmd命令行中，使用`javac 文件名.java`即可手动将一个java文件编译成class文件
2. 在cmd命令行中, `java 文件名`可以直接运行编译后的class文件(不需要带class后缀)
3. 快速循环输出一个集合：`users.forEach(System.out::print);`

