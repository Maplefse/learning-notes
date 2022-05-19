# ElasticSearch

ElasticSearchs 基于Lucene做了一些封装和增强

而Lucene是一套信息检索工具包，包括索引结构，读写索引的工具，排序，搜索规则

## ElasticSearch概述

Elaticsearch，简称为es ，es是一个开源的高扩展的**分布式全文检索引擎**，它可以近乎**实时的存储、检索数据**；本身扩展性很好，可以扩展到上百台服务器，处理PB级别的数据。es也使用Java开发并使用Lucene作为其核心来实现所有索引和搜索的功能，但是它的目的是通过简单的RESTful APl来隐藏Lucene的复杂性，从而让全文搜索变得简单。



## ElasticSearch简介

Elasticsearch是一个实时分布式搜索和分析引擎。它让你以前所未有的速度处理大数据成为可能。

它用于**全文搜索、结构化搜索、分析**以及将这三者混合使用:
维基百科使用Elasticsearch提供全文搜索并**高亮关键字**，以及输入实时搜索(search-asyou-type)和搜索纠错(did-you-mean)等搜索建议功能。
英国卫报使用Elasticsearch结合用户日志和社交网络数据提供给他们的编辑以实时的反馈，以便及时了解公众对新发表的文章的回应。
StackOverflow结合全文搜索与地理位置查询，以及more-like-this功能来找到相关的问题和答案。Github使用Elasticsearch检索1300亿行的代码。
但是Elasticsearch不仅用于大型企业，它还让像DataDog以及Klout这样的创业公司将最初的想法变成可扩展的解决方案。Elasticsearch可以在你的笔记本上运行，也可以在数以百计的服务器上处理PB级别的数据。
Elasticsearch是一个基于Apache Lucene(TM)的开源搜索引擎。无论在开源还是专有领域，Lucene可以被认为是迄今为止最先进、性能最好的、功能最全的搜索引擎库。
但是，Lucene只是一个库。想要使用它，你必须使用ava来作为开发语言并将其直接集成到你的应用中，更糟糕的是，Lucene非常复杂，你需要深入了解检索的相关知识来理解它是如何工作的。
Elasticsearch也使用Java开发并使用Lucene作为其核心来实现所有索引和搜索的功能，但是它的目的是通过简单的
RESTful API来隐藏Lucene的复杂性，从而让全文搜索变得简单。



## ElasticSearch安装

**es要求JDK版本最低1.8**

### Linux安装



### Windows安装

es官网：https://www.elastic.co/cn/elasticsearch/

下载地址：https://www.elastic.co/cn/downloads/elasticsearch

下载后解压即用

解压后文件

![image-20210621113424761](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210621113424761.png)

目录说明：

```
bin 启动文件
config 配置文件
	log4j2 日志配置文件
	jvm.options java虚拟机相关配置
	elasticsearch.yml es的配置文件 默认9200端口
lib 	相关jar包
logs	日志
modules	功能模块
plgins	插件!
```



启动：在bin目录下，启动`elasticsearch.bat`文件即可

访问它给出的端口号9200

![image-20210621114255703](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210621114255703.png)

获得如下内容

![image-20210621114309370](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210621114309370.png)



## 安装可视化界面 ElasticSearch head

**必须要有node.js环境才能安装**

下载地址：https://github.com/mobz/elasticsearch-head

1. 下载完成后解压

   ![image-20210621115407820](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210621115407820.png)

2. 在目录中开启cmd,执行 `npm install` 安装

   ![image-20210621133723960](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210621133723960.png)

3. 想要使用还需要解决跨域问题

4. 在elasticsearch-7.13.2\config目录下的`elasticsearch.yml`文件中最下方新增语句

   ```yaml
   http.cors.enabled: true			//开启跨域支持
   http.cors.allow-origin: "*"		//允许什么访问
   ```

5. 打开es服务，`npm run start`运行es-head，访问`localhost:9100`端口,连接es

   ![image-20210622002419144](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622002419144.png)

   

   

## Kibana安装

> 了解ELK

ELK是Elasticsearch、Logstash、Kibana三大开源框架首字母大写简称。市面上也被成为Elastic Stack。其中Elasticsearch是一个基于Lucene、分布式、通过Restful方式进行交互的近实时搜索平台框架。像类似百度、谷歌这种大数据全文搜索引擎的场景都可以使用Elasticsearch作为底层支持框架，可见Elasticsearch提供的搜索能力确实强大,市面上很多时候我们简称Elasticsearch为es。Logstash是ELK的中央数据流引擎，用于从不同目标（文件/数据存储/MQ)收集的不同格式数据，经过过滤后支持输出到不同目的地(文件/MQ/redis/elasticsearch/kafka等)。Kibana可以将elasticsearch的数据通过友好的页面展示出来，提供实时分析的功能。
市面上很多开发只要提到ELK能够一致说出它是一个日志分析架构技术栈总称，但实际上ELK不仅仅适用于日志分析，它还可以支持其它任何数据分析和收集的场景，日志分析和收集只是更具有代表性。并非唯一性。

### 安装

Kibana是一个针对Elasticsearch的开源分析及可视化平台，用来搜索、查看交互存储在Elasticsearch索引中的数据。使用Kibana ,可以通过各种图表进行高级数据分析及展示。Kibana让海量数据更容易理解。它操作简单，基于浏览器的用户界面可以快速创建仪表板 ( dashboard ) 实时显示Elasticsearch查询动态。设置Kibana非常简单。无需编码或者额外的基础架构，几分钟内就可以完成Kibana安装并启动Elasticsearch索引监测。

官网：https://www.elastic.co/cn/kibana

**Kibana版本要和Es版本一致**

下载后解压，获得如下文件：

![image-20210622005334086](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622005334086.png)

启动在bin目录中的`kibana.bat`即可使用

kibana默认端口`http://localhost:5601`

访问后获得如下页面

![image-20210622010102554](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622010102554.png)

在右边菜单点击Dev Tools，来到开发工具页面

![image-20210622010351100](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622010351100.png)



在这里即可编写请求，并进行访问

![image-20210622010504697](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622010504697.png)



### 汉化

在主目录下的config中，修改`kibana.yml`配置文件如图

![image-20210622010924634](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622010924634.png)

即可切换成中文,修改完后要重启

ps：汉化后Dev Tools变成开发工具



## ES核心概念

了解**集群、节点、索引、类型、文档、分片、映射**是什么

### 关系型数据库与es的对比

> elasticsearch是面向文档存储的,关系型数据库和elasticscarch客观的对比

![image-20220411235038242](assets\image-20220411235038242.png)

elasticsearch(集群)中可以包含多个索引(数据库)，每个索引中可以包含多个类型(表)，每个类型下又包含多个文档(行)，每个文档中又包含多个字段(列)。

### 核心概念的说明

**物理设计**：

elastic search在后台把每个**索引划分成多个分片**，每分分片可以在集群中的不同服务器间迁移

一个人就是一个集群！默认的集群名就是 elasticsearch

**逻辑设计**：

一个索引类型中，包含多个文档，比如说文档1，文档2。当我们索引一篇文档时，可以通过这样的顺序找到它:索引→类型→文档ID，通过这个组合我们就能索引到某个具体的文档。注意:ID不必是整数，实际上它是个字符串。

#### **文档**

可以这么理解：**文档就是一条条数据**

之前说elasticsearch是面向文档的，那么就意味着索引和搜索数据的最小单位是文档，elasticsearch中，文档有几个重要属性:

- 自我包含，一篇文档同时包含字段和对应的值，也就是同时包含key:value ! I
- 可以是层次型的，一个文档中包含自文档，复杂的逻辑实体就是这么来的!（就是一个json对象）
- 灵活的结构，文档不依赖预先定义的模式，我们知道关系型数据库中，要提前定义字段才能使用，在elasticsearch中，对于字段是非常灵活的，有时候，我们可以忽略该字段，或者动态的添加一个新的字段。

尽管我们可以随意的新增或者忽略某个字段，但是，每个字段的类型非常重要，比如一个年龄字段类型，可以是字符串也可以是整形。因为elasticsearch会保存字段和类型之间的映射及其他的设置。这种映射具体到每个映射的每种类型，这也是为什么在elasticsearch中，**类型有时候也称为映射类型**。

#### **类型**\映射

![image-20210622014038633](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622014038633.png)

类型是文档的逻辑容器，就像关系型数据库一样，表格是行的容器。**类型中对于字段的约束定义称为映射**，比如 name映射为字符串类型。我们说文档是无模式的，它们不需要拥有映射中所定义的所有字段，比如新增一个字段，那么elasticsearch是怎么做的呢?elasticsearch会自动的将新字段加入映射，但是这个字段的不确定它是什么类型，elasticsearch就开始猜，如果这个值是18，那么elasticsearch会认为它是整形。但是elasticsearch也可能猜不对，所以最安全的方式就是提前定义好所需要的映射，这点跟关系型数据库殊途同归了，先定义好字段，然后再使用，别整什么幺蛾子。

#### **索引**

**索引就是数据库**

索引是映射类型的容器，elasticsearch中的索引是一个非常大的**相同类型的文档集合**。索引存储了映射类型的字段和其他设置。然后它们被存储到了各个分片上了。我们来研究下分片是如何工作的。

**物理设计：节点和分片如何工作**

一个集群至少有一个节点，而一个节点就是一个elasricsearch进程，节点可以有多个索引默认的，如果你创建索引，那么索引将会有个5个分片 ( primary shard ,又称主分片)构成的，每一个主分片会有一个副本( replica shard ,又称复制分片)

![image-20210622012555100](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622012555100.png)

上图是一个有3个节点的集群，可以看到主分片和对应的复制分片都不会在同一个节点内，这样有利于某个节点挂掉了，数据也不至于丢失。实际上，一个分片是一个Lucene索引，一个包含倒排索引的文件目录，倒排索引的结构使得elasticsearch在不扫描全部文档的情况下，就能告诉你哪些文档包含特定的关键字。不过，等等，倒排索引是什么鬼?

#### **倒排索引**

elasticsearch使用的是一种称为倒排索引的结构，采用Lucene倒排索作为底层。这种结构适用于快速的全文搜索，一个索引由文档中所有不重复的列表构成，对于每一个词，都有一个包含它的文档列表。例如，现在有两个文档，每个文档包含如下内容:

```
Study every day, good good up to forever #文档1包含的内容
To forever, study erery day, good good up #文档2包含的内容
```

为了创建倒排索引，我们首先要将每个文档拆分成独立的词(或称为词条或者tokens)，然后创建一个包含所有不重复的词条的排序列表，然后列出每个词条出现在哪个文档:

![image-20210622012821772](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622012821772.png)

现在，我们试图搜索 to forever，只需要查看包含每个词条的文档

![image-20210622012918195](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622012918195.png)

两个文档都匹配，但是第一个文档比第二个匹配程度更高。如果没有别的条件，现在，这两个包含关键字的文档都将返回。

再来看一个示例，比如我们通过博客标签来搜索博客文章。那么倒排索引列表就是这样的一个结构:

![image-20210622013003570](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622013003570.png)

如果要搜索含有python标签的文章，那相对于查找所有原始数据而言，查找倒排索引后的数据将会快的多。只需要
查看标签这一栏，然后获取相关的文章ID即可。

elasticsearch的索引和Lucene的索引对比

在elasticsearch中，索引这个词被频繁使用，这就是术语的使用。在elasticsearch中，索引被分为多个分片，每份分片是一个Lucene的索引。所以一个elasticsearch索引是由多个Lucene索引组成的。别问为什么，谁让elasticsearch使用Lucene作为底层呢!
如无特指，说起索引都是指elasticsearch的索引。

接下来的一切操作都在kibana中Dev Tools下的Console里完成。基础操作!



## **IK分词器**

分词∶即把一段中文或者别的划分成一个个的关键字，我们在搜索时候会把自己的信息进行分词，会把数据库中或者索引库中的数据进行分词，然后进行一个匹配操作，默认的中文分词是将每个字看成一个词，比如“"你好世界"会被分为"你""好""世""界"，这显然是不符合要求的，所以我们需要安装中文分词器ik来解决这个问题。

如果要使用中文，建议使用ik分词器

IK提供了两个分词算法:ik_smart和ik_max_word，其中ik_smart为最少切分，ik_max_word为最细粒度划分!一会我们测试!



### 安装

最新版下载地址：https://github.com/medcl/elasticsearch-analysis-ik/releases

下载后解压，获得如下文件

![image-20210622111930132](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622111930132.png)

将其放在`ElasticSearch\elasticsearch-7.13.2\plugins\ik`该目录下，在plugins中创建ik文件夹存放

注意：plugins中除了ik目录，**不要放其它的任何东西**，不然启动报错

​			**ik与es的版本同样要对应**

完成后需要重启

![image-20210622112631106](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622112631106.png)可以看到加载了ik分词器



也可以使用es的bin目录下运行cmd，执行`elasticsearch-plugin list`语句

运行后可以看到，获取倒了ik

![image-20210622112839513](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622112839513.png)



### 使用kibana进行测试

不同的分词算法测试：

ik_smart：

最少切分会将数据按照尽量少的次数进行划分，可以狠明显的看到，划分出来的3条数据中，没有重复的内容

![image-20210622114110405](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622114110405.png)



ik_max_word：

最细粒度划分会将数据中所有能划分的数据划分，可以发现划分出来的数据内容其实是有重复的

![image-20210622114134600](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622114134600.png)



### 分词器字典

分词条是通过它的字典对数据进行切分的，如果有些词语不在字典中，就会默认的逐个切分：

`狂神说应该是一个整体,因为字典中没有,它被逐个的切分了`

![image-20210622114730724](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622114730724.png)

所以这种自己需要的词语，就需要自己手动添加到分词器的字典中！

在分词器目录下的config目录中配置

![image-20210622115024332](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622115024332.png)

打开后获得如下内容

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
	<comment>IK Analyzer 扩展配置</comment>
	<!--用户可以在这里配置自己的扩展字典 -->
	<entry key="ext_dict"></entry>
	 <!--用户可以在这里配置自己的扩展停止词字典-->
	<entry key="ext_stopwords"></entry>
	<!--用户可以在这里配置远程扩展字典 -->
	<!-- <entry key="remote_ext_dict">words_location</entry> -->
	<!--用户可以在这里配置远程扩展停止词字典-->
	<!-- <entry key="remote_ext_stopwords">words_location</entry> -->
</properties>
```

通过编写自己的.dic字典文件添加分词内容

![image-20210622115508180](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622115508180.png)

如图，现在狂神说就会被认为是一个整体

注意：**.dic的编码格式要为UTF**(UTF-8就行了)

重启es后生效



## Rest风格操作索引

一种软件架构风格，而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。

ES则通过Restful风格的请求来操作索引库、文档。请求内容用DSL语句来表示。

基本Rest命令说明：

![image-20210622132321029](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622132321029.png)

### 索引的基本操作

基础测试：

1. 创建索引

   ```
   PUT /索引名/~类型名~/文档id
   {请求体}
   ```

   ![image-20210622132928406](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622132928406.png)

   完成了自动增加索引，数据也成功的添加

   ![image-20210622133106477](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622133106477.png)

#### mapping约束

1. 那么name这个字段用不用指定类型呢？毕竟关系型数据库都是需要指定类型的！答案是当然需要！

   在es中，我们将**索引中的文档的类型约束称之为mapping**，也就是关系型数据库中的类型！常见的mapping属性包括：

   - type：字段数据类型，常见的简单类型有：
     - 字符串：text（可分词的文本）、keyword（精确值，例如：品牌、国家、ip地址）
     - 数值：long、integer、short、byte、double、float、
     - 布尔：boolean
     - 日期：date
     - 对象：object
   - index：是否创建索引（创建倒排索引），默认为true
   - analyzer：使用哪种分词器
   - properties：该字段的子字段

2. 指定字段的约束类型

   ![image-20210622133804738](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622133804738.png)

   创建一个规则

3. 完整的格式示例

   格式：

   ```json
   PUT /索引库名称
   {
     "mappings": {
       "properties": {
         "字段名":{
           "type": "text",
           "analyzer": "ik_smart"
         },
         "字段名2":{
           "type": "keyword",
           "index": "false"
         },
         "字段名3":{
           "properties": {
             "子字段": {
               "type": "keyword"
             }
           }
         },
         // ...略
       }
     }
   }
   ```

   示例：

   ```sh
   PUT /heima
   {
     "mappings": {
       "properties": {
         "info":{
           "type": "text",
           "analyzer": "ik_smart"
         },
         "email":{
           "type": "keyword",
           "index": "falsae"
         },
         "name":{
           "properties": {
             "firstName": {
               "type": "keyword"
             }
           }
         },
         // ... 略
       }
     }
   }
   ```

4. get请求

   ![image-20210622133928016](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622133928016.png)

   可以通过get请求获取具体的信息

5. 查看默认的信息

   ![image-20210622134802240](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622134802240.png)**如果自己的文档字段没有指定mapping映射，es也会默认配置字段类型**

6. 拓展命令：

   - 通过get _cat/ 可以获得es的当前的很多信息

7. 修改索引

   - 倒排索引结构虽然不复杂，但是一旦数据结构改变（比如改变了分词器），就需要重新创建倒排索引，这简直是灾难。因此索引库**一旦创建，无法修改mapping**。

     虽然无法修改mapping中已有的字段，但是却允许添加新的字段到mapping中，因为不会对倒排索引产生影响。

     ```
     PUT /索引库名/_mapping
     {
       "properties": {
         "新字段名":{
           "type": "integer"
         }
       }
     }
     ```

8. 删除索引：`DELETE 索引\文档`

   通过DELETE命令实现删除，根据你的请求来判断是删除索引还是删除文档记录



### 文档的基本操作

1. 创建数据

   ```java
   PUT /test3/_doc/3		//  /索引库名/_doc/文档id
   {
     "name": "李四",
     "age": 22,
     "birth": "2000-01-01"
   }
   ```

   

   ![image-20210622160937527](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622160937527.png)

2. 获取数据

   ```
   GET /索引库名/_doc/文档id
   ```

   

   ![image-20210622161053812](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622161053812.png)

3. 简单的条件查询

   - `GET 索引/_search?q=name:查询内容`

     ![image-20210622161948347](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210622161948347.png)

4. 删除文档

   ```
   语法:
   DELETE /索引库名/_doc/文档id
   
   示例:
   DELETE /test3/_doc/3
   ```

   

5. 修改文档

   ```
   方式一: 全量修改，会删除旧的文档，再添加新文档
   语法:
   PUT /索引库名/_doc/文档id
   {
   	"字段1": "值1",
   	"字段2": "值2"
   }
   
   方式二: 增量修改,修改指定字段值
   语法:
   POST /索引库名/_update/文档id
   {
   	"doc": {
   		"字段名1": "新的值",
   		"字段名2": "新的值"
   	}
   }
   ```



### 复杂查询

#### 1.1.DSL查询分类

Elasticsearch提供了基于JSON的DSL（[Domain Specific Language](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html)）来定义查询。常见的查询类型包括：

- **查询所有**：查询出所有数据，一般测试用。例如：
  - match_all
- **全文检索（full text）查询**：利用分词器对用户输入内容分词，然后去倒排索引库中匹配。例如：
  - match_query
  - multi_match_query
- **精确查询**：根据精确词条值查找数据，一般是查找keyword、数值、日期、boolean等类型字段。例如：
  - ids
  - range
  - term
- **地理（geo）查询**：根据经纬度查询。例如：
  - geo_distance
  - geo_bounding_box
- **复合（compound）查询**：复合查询可以将上述各种查询条件组合起来，合并查询条件。例如：
  - bool
  - function_score

查询的语法基本一致：

```json
GET /indexName/_search
{
  "query": {
    "查询类型": {
      "查询条件": "条件值"
    }
  }
}
```

我们以查询所有为例，其中：

- 查询类型为match_all
- 没有查询条件

```json
// 查询所有
GET /indexName/_search
{
  "query": {
    "match_all": {
    }
  }
}
```

其它查询无非就是**查询类型**、**查询条件**的变化。



#### 1.2.全文检索查询



##### 1.2.1.使用场景

全文检索查询的基本流程如下：

- 对用户搜索的内容做分词，得到词条
- 根据词条去倒排索引库中匹配，得到文档id
- 根据文档id找到文档，返回给用户

比较常用的场景包括：

- 商城的输入框搜索
- 百度输入框搜索

例如京东：

![image-20210721165326938](assets\image-20210721165326938.png)



因为是拿着词条去匹配，因此参与搜索的字段也必须是可分词的text类型的字段。



##### 1.2.2.基本语法

常见的全文检索查询包括：

- match查询：单字段查询
- multi_match查询：多字段查询，任意一个字段符合条件就算符合查询条件

match查询语法如下：

```json
GET /indexName/_search
{
  "query": {
    "match": {
      "FIELD": "TEXT"
    }
  }
}
```

mulit_match语法如下：

```json
GET /indexName/_search
{
  "query": {
    "multi_match": {
      "query": "TEXT",
      "fields": ["FIELD1", " FIELD12"]
    }
  }
}
```



##### 1.2.3.示例

match查询示例：

![image-20210721170455419](assets\image-20210721170455419.png)



multi_match查询示例：

![image-20210721170720691](assets\image-20210721170720691.png)



可以看到，两种查询结果是一样的，为什么？

因为我们将brand、name、business值都利用copy_to复制到了all字段中。因此你根据三个字段搜索，和根据all字段搜索效果当然一样了。

但是，搜索字段越多，对查询性能影响越大，因此建议采用copy_to，然后单字段查询的方式。



##### 1.2.4.总结

match和multi_match的区别是什么？

- match：根据一个字段查询
- multi_match：根据多个字段查询，参与查询字段越多，查询性能越差



#### 1.3.精准查询

精确查询一般是查找keyword、数值、日期、boolean等类型字段。所以**不会**对搜索条件分词。常见的有：

- term：根据词条精确值查询
- range：根据值的范围查询



##### 1.3.1.term查询

因为精确查询的字段搜是不分词的字段，因此查询的条件也必须是**不分词**的词条。查询时，用户输入的内容跟自动值完全匹配时才认为符合条件。如果用户输入的内容过多，反而搜索不到数据。



语法说明：

```json
// term查询
GET /indexName/_search
{
  "query": {
    "term": {
      "FIELD": {
        "value": "VALUE"
      }
    }
  }
}
```



示例：

当我搜索的是精确词条时，能正确查询出结果：

![image-20210721171655308](assets\image-20210721171655308.png)

但是，当我搜索的内容不是词条，而是多个词语形成的短语时，反而搜索不到：

![image-20210721171838378](assets\image-20210721171838378.png)





##### 1.3.2.range查询

范围查询，一般应用在对数值类型做范围过滤的时候。比如做价格范围过滤。



基本语法：

```json
// range查询
GET /indexName/_search
{
  "query": {
    "range": {
      "FIELD": {
        "gte": 10, // 这里的gte代表大于等于，gt则代表大于
        "lte": 20 // lte代表小于等于，lt则代表小于
      }
    }
  }
}
```



示例：

![image-20210721172307172](assets\image-20210721172307172.png)





##### 1.3.3.总结

精确查询常见的有哪些？

- term查询：根据词条精确匹配，一般搜索keyword类型、数值类型、布尔类型、日期类型字段
- range查询：根据数值范围查询，可以是数值、日期的范围



#### 1.4.地理坐标查询

所谓的地理坐标查询，其实就是根据经纬度查询，官方文档：https://www.elastic.co/guide/en/elasticsearch/reference/current/geo-queries.html

常见的使用场景包括：

- 携程：搜索我附近的酒店
- 滴滴：搜索我附近的出租车
- 微信：搜索我附近的人



附近的酒店：

![image-20210721172645103](assets\image-20210721172645103.png) 

附近的车：

![image-20210721172654880](assets\image-20210721172654880.png) 



##### 1.4.1.矩形范围查询

矩形范围查询，也就是geo_bounding_box查询，查询坐标落在某个矩形范围的所有文档：

![DKV9HZbVS6](assets\DKV9HZbVS6.gif)

查询时，需要指定矩形的**左上**、**右下**两个点的坐标，然后画出一个矩形，落在该矩形内的都是符合条件的点。

语法如下：

```json
// geo_bounding_box查询
GET /indexName/_search
{
  "query": {
    "geo_bounding_box": {
      "FIELD": {
        "top_left": { // 左上点
          "lat": 31.1,
          "lon": 121.5
        },
        "bottom_right": { // 右下点
          "lat": 30.9,
          "lon": 121.7
        }
      }
    }
  }
}
```





这种并不符合“附近的人”这样的需求，所以我们就不做了。



##### 1.4.2.附近查询

附近查询，也叫做距离查询（geo_distance）：查询到指定中心点小于某个距离值的所有文档。



换句话来说，在地图上找一个点作为圆心，以指定距离为半径，画一个圆，落在圆内的坐标都算符合条件：

![vZrdKAh19C](assets\vZrdKAh19C.gif)

语法说明：

```json
// geo_distance 查询
GET /indexName/_search
{
  "query": {
    "geo_distance": {
      "distance": "15km", // 半径
      "FIELD": "31.21,121.5" // 圆心
    }
  }
}
```



示例：

我们先搜索陆家嘴附近15km的酒店：

![image-20210721175443234](assets\image-20210721175443234.png)

发现共有47家酒店。



然后把半径缩短到3公里：

![image-20210721182031475](assets\image-20210721182031475.png)

可以发现，搜索到的酒店数量减少到了5家。



#### 1.5.复合查询

复合（compound）查询：复合查询可以将其它简单查询组合起来，实现更复杂的搜索逻辑。常见的有两种：

- fuction score：算分函数查询，可以控制文档相关性算分，控制文档排名
- bool query：布尔查询，利用逻辑关系组合多个其它的查询，实现复杂搜索



##### 1.5.1.相关性算分

当我们利用match查询时，文档结果会根据与搜索词条的关联度打分（_score），返回结果时按照分值降序排列。

例如，我们搜索 "虹桥如家"，结果如下：

```json
[
  {
    "_score" : 17.850193,
    "_source" : {
      "name" : "虹桥如家酒店真不错",
    }
  },
  {
    "_score" : 12.259849,
    "_source" : {
      "name" : "外滩如家酒店真不错",
    }
  },
  {
    "_score" : 11.91091,
    "_source" : {
      "name" : "迪士尼如家酒店真不错",
    }
  }
]
```



在elasticsearch中，早期使用的打分算法是TF-IDF算法，公式如下：

![image-20210721190152134](assets\image-20210721190152134.png)



在后来的5.1版本升级中，elasticsearch将算法改进为BM25算法，公式如下：

![image-20210721190416214](assets\image-20210721190416214.png)





TF-IDF算法有一各缺陷，就是词条频率越高，文档得分也会越高，单个词条对文档影响较大。而BM25则会让单个词条的算分有一个上限，曲线更加平滑：

![image-20210721190907320](assets\image-20210721190907320.png)



小结：elasticsearch会根据词条和文档的相关度做打分，算法由两种：

- TF-IDF算法
- BM25算法，elasticsearch5.1版本后采用的算法



##### 1.5.2.算分函数查询

根据相关度打分是比较合理的需求，但**合理的不一定是产品经理需要**的。

以百度为例，你搜索的结果中，并不是相关度越高排名越靠前，而是谁掏的钱多排名就越靠前。如图：

![image-20210721191144560](assets\image-20210721191144560.png)



要想认为控制相关性算分，就需要利用elasticsearch中的function score 查询了。



###### 1）语法说明

![image-20210721191544750](assets\image-20210721191544750.png)



function score 查询中包含四部分内容：

- **原始查询**条件：query部分，基于这个条件搜索文档，并且基于BM25算法给文档打分，**原始算分**（query score)
- **过滤条件**：filter部分，符合该条件的文档才会重新算分
- **算分函数**：符合filter条件的文档要根据这个函数做运算，得到的**函数算分**（function score），有四种函数
  - weight：函数结果是声明的常量
  - field_value_factor：以文档中的某个字段值作为函数结果
  - random_score：以随机数作为函数结果
  - script_score：自定义算分函数算法
- **运算模式**：算分函数的结果、原始查询的相关性算分，两者之间的运算方式，包括：
  - multiply：相乘
  - replace：用function score替换query score
  - 其它，例如：sum、avg、max、min



function score的运行流程如下：

- 1）根据**原始条件**查询搜索文档，并且计算相关性算分，称为**原始算分**（query score）
- 2）根据**过滤条件**，过滤文档
- 3）符合**过滤条件**的文档，基于**算分函数**运算，得到**函数算分**（function score）
- 4）将**原始算分**（query score）和**函数算分**（function score）基于**运算模式**做运算，得到最终结果，作为相关性算分。



因此，其中的关键点是：

- 过滤条件：决定哪些文档的算分被修改
- 算分函数：决定函数算分的算法
- 运算模式：决定最终算分结果



###### 2）示例

需求：给“如家”这个品牌的酒店排名靠前一些

翻译一下这个需求，转换为之前说的四个要点：

- 原始条件：不确定，可以任意变化
- 过滤条件：brand = "如家"
- 算分函数：可以简单粗暴，直接给固定的算分结果，weight
- 运算模式：比如求和

因此最终的DSL语句如下：

```json
GET /hotel/_search
{
  "query": {
    "function_score": {
      "query": {  .... }, // 原始查询，可以是任意条件
      "functions": [ // 算分函数
        {
          "filter": { // 满足的条件，品牌必须是如家
            "term": {
              "brand": "如家"
            }
          },
          "weight": 2 // 算分权重为2
        }
      ],
      "boost_mode": "sum" // 加权模式，求和
    }
  }
}
```



测试，在未添加算分函数时，如家得分如下：

![image-20210721193152520](assets\image-20210721193152520.png)

添加了算分函数后，如家得分就提升了：

![image-20210721193458182](assets\image-20210721193458182.png)



###### 3）小结

function score query定义的三要素是什么？

- 过滤条件：哪些文档要加分
- 算分函数：如何计算function score
- 加权方式：function score 与 query score如何运算



##### 1.5.3.布尔查询

布尔查询是一个或多个查询子句的组合，每一个子句就是一个**子查询**。子查询的组合方式有：

- must：必须匹配每个子查询，类似“与” “&&”
- should：选择性匹配子查询，类似“或” ,“||“
- must_not：必须不匹配，**不参与算分**，类似“非”，” ! “
- filter：必须匹配，**不参与算分**，” = “



比如在搜索酒店时，除了关键字搜索外，我们还可能根据品牌、价格、城市等字段做过滤：

![image-20210721193822848](assets\image-20210721193822848.png)

每一个不同的字段，其查询的条件、方式都不一样，必须是多个不同的查询，而要组合这些查询，就必须用bool查询了。



需要注意的是，搜索时，参与**打分的字段越多，查询的性能也越差**。因此这种多条件查询时，建议这样做：

- 搜索框的关键字搜索，是全文检索查询，使用must查询，参与算分
- 其它过滤条件，采用filter查询。不参与算分



###### 1）语法示例：

```json
GET /hotel/_search
{
  "query": {
    "bool": {
      "must": [			//必须有上海
        {"term": {"city": "上海" }}		
      ],
      "should": [		//为其中的一个
        {"term": {"brand": "皇冠假日" }},
        {"term": {"brand": "华美达" }}
      ],
      "must_not": [		//值大于500
        { "range": { "price": { "lte": 500 } }}
      ],
      "filter": [		//等于45
        { "range": {"score": { "gte": 45 } }}
      ]
    }
  }
}
```



###### 2）示例

需求：搜索名字包含“如家”，价格不高于400，在坐标31.21,121.5周围10km范围内的酒店。

分析：

- 名称搜索，属于全文检索查询，应该参与算分。放到must中
- 价格不高于400，用range查询，属于过滤条件，不参与算分。放到must_not中
- 周围10km范围内，用geo_distance查询，属于过滤条件，不参与算分。放到filter中



![image-20210721194744183](assets\image-20210721194744183.png)





###### 3）小结

bool查询有几种逻辑关系？

- must：必须匹配的条件，可以理解为“与”
- should：选择性匹配的条件，可以理解为“或”
- must_not：必须不匹配的条件，不参与打分
- filter：必须匹配的条件，不参与打分



### 查询结果处理

搜索的结果可以按照用户指定的方式去处理或展示。

##### 2.1.排序

elasticsearch默认是根据相关度算分（_score）来排序，但是也支持自定义方式对搜索[结果排序](https://www.elastic.co/guide/en/elasticsearch/reference/current/sort-search-results.html)。可以排序字段类型有：keyword类型、数值类型、地理坐标类型、日期类型等。

###### 2.1.1.普通字段排序

keyword、数值、日期类型排序的语法基本一致。

**语法**：

```json
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "FIELD": "desc"  // 排序字段、排序方式ASC、DESC
    }
  ]
}
```

排序条件是一个数组，也就是可以写多个排序条件。按照声明的顺序，当第一个条件相等时，再按照第二个条件排序，以此类推



**示例**：

需求描述：酒店数据按照用户评价（score)降序排序，评价相同的按照价格(price)升序排序

![image-20210721195728306](assets\image-20210721195728306.png)



###### 2.1.2.地理坐标排序

地理坐标排序略有不同。

**语法说明**：

```json
GET /indexName/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "_geo_distance" : {
          "FIELD" : "纬度，经度", // 文档中geo_point类型的字段名、目标坐标点
          "order" : "asc", // 排序方式
          "unit" : "km" // 排序的距离单位
      }
    }
  ]
}
```

这个查询的含义是：

- 指定一个坐标，作为目标点
- 计算每一个文档中，指定字段（必须是geo_point类型）的坐标 到目标点的距离是多少
- 根据距离排序



**示例：**

需求描述：实现对酒店数据按照到你的位置坐标的距离升序排序

提示：获取你的位置的经纬度的方式：https://lbs.amap.com/demo/jsapi-v2/example/map/click-to-get-lnglat/



假设我的位置是：31.034661，121.612282，寻找我周围距离最近的酒店。

![image-20210721200214690](assets\image-20210721200214690.png)





##### 2.2.分页

elasticsearch 默认情况下只返回top10的数据。而如果要查询更多数据就需要修改分页参数了。elasticsearch中通过修改from、size参数来控制要返回的分页结果：

- from：从第几个文档开始
- size：总共查询几个文档

类似于mysql中的`limit ?, ?`

###### 2.2.1.基本的分页

分页的基本语法如下：

```json
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "from": 0, // 分页开始的位置，默认为0
  "size": 10, // 期望获取的文档总数
  "sort": [
    {"price": "asc"}
  ]
}
```





###### 2.2.2.深度分页问题

现在，我要查询990~1000的数据，查询逻辑要这么写：

```json
GET /hotel/_search
{
  "query": {
    "match_all": {}
  },
  "from": 990, // 分页开始的位置，默认为0
  "size": 10, // 期望获取的文档总数
  "sort": [
    {"price": "asc"}
  ]
}
```

这里是查询990开始的数据，也就是 第990~第1000条 数据。

不过，elasticsearch内部分页时，必须先查询 0~1000条，然后截取其中的990 ~ 1000的这10条：

![image-20210721200643029](assets\image-20210721200643029.png)



查询TOP1000，如果es是单点模式，这并无太大影响。

但是elasticsearch将来一定是集群，例如我集群有5个节点，我要查询TOP1000的数据，并不是每个节点查询200条就可以了。

因为节点A的TOP200，在另一个节点可能排到10000名以外了。

因此要想获取整个集群的TOP1000，必须先查询出每个节点的TOP1000，汇总结果后，重新排名，重新截取TOP1000。

![image-20210721201003229](assets\image-20210721201003229.png)



那如果我要查询9900~10000的数据呢？是不是要先查询TOP10000呢？那每个节点都要查询10000条？汇总到内存中？



当查询分页深度较大时，汇总数据过多，对内存和CPU会产生非常大的压力，因此elasticsearch会禁止from+ size 超过10000的请求。



针对深度分页，ES提供了两种解决方案，[官方文档](https://www.elastic.co/guide/en/elasticsearch/reference/current/paginate-search-results.html)：

- search after：分页时需要排序，原理是从上一次的排序值开始，查询下一页数据。官方推荐使用的方式。
- scroll：原理将排序后的文档id形成快照，保存在内存。官方已经不推荐使用。



###### 2.2.3.小结

分页查询的常见实现方案以及优缺点：

- `from + size`：
  - 优点：支持随机翻页
  - 缺点：深度分页问题，默认查询上限（from + size）是10000
  - 场景：百度、京东、谷歌、淘宝这样的随机翻页搜索
- `after search`：
  - 优点：没有查询上限（单次查询的size不超过10000）
  - 缺点：只能向后逐页查询，不支持随机翻页
  - 场景：没有随机翻页需求的搜索，例如手机向下滚动翻页

- `scroll`：
  - 优点：没有查询上限（单次查询的size不超过10000）
  - 缺点：会有额外内存消耗，并且搜索结果是非实时的
  - 场景：海量数据的获取和迁移。从ES7.1开始不推荐，建议用 after search方案。





##### 2.3.高亮

###### 2.3.1.高亮原理

什么是高亮显示呢？

我们在百度，京东搜索时，关键字会变成红色，比较醒目，这叫高亮显示：

![image-20210721202705030](assets\image-20210721202705030.png)

高亮显示的实现分为两步：

- 1）给文档中的所有关键字都添加一个标签，例如`<em>`标签
- 2）页面给`<em>`标签编写CSS样式



###### 2.3.2.实现高亮

**高亮的语法**：

```json
GET /hotel/_search
{
  "query": {
    "match": {
      "FIELD": "TEXT" // 查询条件，高亮一定要使用全文检索查询
    }
  },
  "highlight": {
    "fields": { // 指定要高亮的字段
      "FIELD": {
        "pre_tags": "<em>",  // 用来标记高亮字段的前置标签
        "post_tags": "</em>" // 用来标记高亮字段的后置标签
      }
    }
  }
}
```



**注意：**

- 高亮是对关键字高亮，因此**搜索条件必须带有关键字**，而不能是范围这样的查询。
- 默认情况下，**高亮的字段，必须与搜索指定的字段一致**，否则无法高亮
- 如果要对非搜索字段高亮，则需要添加一个属性：required_field_match=false



**示例**：

![image-20210721203349633](assets\image-20210721203349633.png)





##### 2.4.总结

查询的DSL是一个大的JSON对象，包含下列属性：

- query：查询条件
- from和size：分页条件
- sort：排序条件
- highlight：高亮条件

示例：

![image-20210721203657850](assets\image-20210721203657850.png)









## SpringBoot整合

官方文档：https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/java-rest-high.html

1. 创建springboot项目，勾选以下初始配置

   ![image-20210623110938223](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623110938223.png)

2. 注意：一定要保证导入的依赖和es的版本一致

   在`spring-boot-dependencies`中找到`<elasticsearch.version>7.13.2</elasticsearch.version>`版本，修改为自己本地版本

3. 创建配置类

   ```java
   @Configuration
   public class ElasticSearchClientConfig {
   
   
       @Bean
       public RestHighLevelClient restHighLevelClient(){
           RestHighLevelClient client = new RestHighLevelClient(
                   RestClient.builder(
                           new HttpHost("localhost", 9200, "http"))
                   
           );
           return client;
           
       }
   
   }
   ```

   即可使用



## SpringBoot中操作API

### 索引的操作

#### 基础的索引创建

```java
@SpringBootTest
class MaplefEsApiApplicationTests {

    @Autowired
    @Qualifier("restHighLevelClient")
    private RestHighLevelClient client;
    
    //  测试索引的创建
    @Test
    void testCreateIndex() throws IOException {
        //1.创建索引请求   参数为索引名称
        CreateIndexRequest request = new CreateIndexRequest("maplef_test");
        
        //2.准备请求的参数: DSL语句与参数类型格式
        hotel.source(MAPPING_TEMPLATE, XContentType.JSON);

        //3.客户端执行请求,请求后获得响应
        CreateIndexResponse response = client.indices().create(request, RequestOptions.DEFAULT);
        System.out.println(response);
    }

}
```

运行后查看

<img src="C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623160846463.png" alt="image-20210623160846463" style="zoom: 50%;" />成功创建索引

#### 获取索引

```java
// 测试获取索引
@Test
void testExistIndex() throws IOException {
    GetIndexRequest request = new GetIndexRequest("maplef_test");
    
    //获取索引是否存在,返回boolean
    boolean exists = client.indices().exists(request, RequestOptions.DEFAULT);
    System.out.println(exists);
}
```

运行效果：![image-20210623161223591](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623161223591.png)

#### 删除索引

```java
// 测试删除索引
@Test
void testDeleteIndex() throws IOException {
    DeleteIndexRequest request = new DeleteIndexRequest("maplef_test");
    //删除索引
    AcknowledgedResponse delete = client.indices().delete(request, RequestOptions.DEFAULT);
    System.out.println(delete.isAcknowledged());    //获取删除后的状态,如果为true证明成功删除
}
```

运行效果：

![image-20210623161718507](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623161718507.png)





### 文档的操作

首先，先创建一个实体类

```java
@Data  //get/set
@AllArgsConstructor //有参
@NoArgsConstructor  //无参
@Component
public class User {

    private String name;
    private int age;

}
```

#### 添加文档数据

```java
//  测试添加文档
@Test
void testAddDocument() throws IOException {
    // 创建对象
    User maplef = new User("maplef", 20);
    // 创建请求
    IndexRequest request = new IndexRequest("maplef_test");
    // 规则   put /maplef_test/_doc/1
    request.id("1");
    request.timeout(TimeValue.timeValueSeconds(1)); //设置过期时间为1s
    // 将数据放入请求, json格式
    request.source(JSON.toJSONString(maplef), XContentType.JSON);
    //客户端发送请求,获取响应的结果
    IndexResponse index = client.index(request, RequestOptions.DEFAULT);

    System.out.println(index.toString());
    System.out.println(index.status());

}
```

运行效果：

![image-20210623163751555](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623163751555.png)

数据成功添加：![image-20210623163817340](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623163817340.png)

#### 查询文档是否存在

```java
//判断文档是否存在
@Test
void testIsExists() throws IOException {
    GetRequest getRequest = new GetRequest("maplef_test", "1");

    //不获取返回的_source的上下文
    getRequest.fetchSourceContext(new FetchSourceContext(false));
    getRequest.storedFields("_none_");

    boolean exists = client.exists(getRequest, RequestOptions.DEFAULT);
    System.out.println(exists);
	//会返回一个Boolean值
}
```



#### 查询文档的信息

```java
//获取文档的信息
@Test
void testGetDocument() throws IOException {

    GetRequest getRequest = new GetRequest("maplef_test", "1");

    GetResponse getResponse = client.get(getRequest, RequestOptions.DEFAULT);
    System.out.println(getResponse.getSourceAsString());    //打印文档内容
    //也可以转换成map等,封装到list集合或实体类都行
    System.out.println(getResponse);    //打印完整的信息
    //返回的全部内容喝命令其实是一样的
}
```

运行效果：

![image-20210623165936408](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623165936408.png)

#### 修改文档信息

```java
//修改文档的信息
@Test
void testUpdateDocument() throws IOException {

    //1. 创建request对象
    UpdateRequest updateRequest = new UpdateRequest("maplef_test","1");
    updateRequest.timeout("1s");

    //2. 准备更新的参数
    //2.1 直接使用实体类
    User user = new User("hello,world", 18);
    updateRequest.doc(JSON.toJSONString(user),XContentType.JSON);
    //2.2 或直接在参数列表中声明
    updateRequest.doc(			//key value 键值对
        "sex", "1",
        "name", "张三"
    );
    
    //3. 更新请求
    UpdateResponse update = client.update(updateRequest, RequestOptions.DEFAULT);
    System.out.println(update);
    System.out.println(update.status());

```

运行效果：

![image-20210623170454304](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623170454304.png)

#### 删除文档信息

```java
//删除文档信息
@Test
void testDeleteRequest() throws IOException {
    DeleteRequest request = new DeleteRequest("maplef_test", "3");	//没有3的数据
    request.timeout("1s");

    DeleteResponse delete = client.delete(request, RequestOptions.DEFAULT);
    System.out.println(delete.status());
    //返回not_found
}
```



运行效果：

![image-20210623171130661](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623171130661.png)

#### 批量插入

```java
// 批量插入数据,在正常项目中一般都会一次性插入大批量的数据
@Test
void testBulkRequest() throws IOException {
    BulkRequest bulkRequest = new BulkRequest();
    bulkRequest.timeout("10s");

    ArrayList<User> userLsit = new ArrayList<>();
    userLsit.add(new User("maplef1",18));
    userLsit.add(new User("maplef2",18));
    userLsit.add(new User("maplef3",18));
    userLsit.add(new User("maplef4",18));
    userLsit.add(new User("xiao1",18));
    userLsit.add(new User("xiao2",18));
    userLsit.add(new User("xiao3",18));
    userLsit.add(new User("xiao4",18));

    for (int i = 0; i< userLsit.size() ; i++){
        //批量更新与删除在这里修改对应的请求就可以了
        bulkRequest.add(new IndexRequest("maplef_for_test").id(""+(i+1))
                        //不设置id,会生成一个随机id
			.source(JSON.toJSONString(userLsit.get(i)),XContentType.JSON));
    }
    
    BulkResponse bulk = client.bulk(bulkRequest, RequestOptions.DEFAULT);
    System.out.println(bulk.hasFailures()); 
    //返回false表示成功插入

}
```

运行效果：

![image-20210623174644692](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623174644692.png)

![image-20210623174655046](C:\Users\13717\AppData\Roaming\Typora\typora-user-images\image-20210623174655046.png)



### 高级查询

```java
//查询
// SearchRequest 搜索请求
// SearchSourceBuilder  搜索条件构造
// SourceBuilder.highlighter()设置高亮
// TermQueryBuilder 构建精确查询
@Test
void testSearch() throws IOException {
    //在真实项目中,库名往往会设置成常量去拿取
    SearchRequest searchRequest = new SearchRequest("maplef_for_test");

    //构建搜索的条件
    SearchSourceBuilder SourceBuilder = new SearchSourceBuilder();
    

    //查询条件,可以使用QueryBuilders快速匹配,它的方法就是各种查询条件
    //trem,精确匹配
    TermQueryBuilder termQueryBuilder = QueryBuilders.termQuery("name", "maplef1");
    //MatchAllQueryBuilder matchAllQueryBuilder = QueryBuilders.matchAllQuery();    匹配所有

    SourceBuilder.query(termQueryBuilder);
    //设置分页数据
    SourceBuilder.from(0);
    SourceBuilder.size(5);
    SourceBuilder.timeout(new TimeValue(60, TimeUnit.SECONDS));     //设置查询时间不超过60s
    searchRequest.source(SourceBuilder);
    SearchResponse search = client.search(searchRequest, RequestOptions.DEFAULT);
    System.out.println(JSON.toJSONString(search.getHits()));
    System.out.println("-------------------------------------------");
    for (SearchHit documentFields : search.getHits().getHits()){
        System.out.println(documentFields.getSourceAsMap());
    }
}
```



文档的查询同样适用 RestHighLevelClient对象，基本步骤包括：

- 1）准备Request对象
- 2）准备请求参数
- 3）发起请求
- 4）解析响应



#### 快速入门

我们以match_all查询为例

#### 发起查询请求

![image-20210721203950559](assets\image-20210721203950559.png)

代码解读：

- 第一步，创建`SearchRequest`对象，指定索引库名

- 第二步，利用`request.source()`构建DSL，DSL中可以包含查询、分页、排序、高亮等
  - `query()`：代表查询条件，利用`QueryBuilders.matchAllQuery()`构建一个match_all查询的DSL
- 第三步，利用client.search()发送请求，得到响应



这里关键的API有两个，一个是`request.source()`，其中包含了查询、排序、分页、高亮等所有功能：

![image-20210721215640790](assets\image-20210721215640790.png)

另一个是`QueryBuilders`，其中包含match、term、function_score、bool等各种查询：

![image-20210721215729236](assets\image-20210721215729236.png)



#### 解析响应

响应结果的解析：

![image-20210721214221057](assets\image-20210721214221057.png)



elasticsearch返回的结果是一个JSON字符串，结构包含：

- `hits`：命中的结果
  - `total`：总条数，其中的value是具体的总条数值
  - `max_score`：所有结果中得分最高的文档的相关性算分
  - `hits`：搜索结果的文档数组，其中的每个文档都是一个json对象
    - `_source`：文档中的原始数据，也是json对象

因此，我们解析响应结果，就是逐层解析JSON字符串，流程如下：

- `SearchHits`：通过response.getHits()获取，就是JSON中的最外层的hits，代表命中的结果
  - `SearchHits#getTotalHits().value`：获取总条数信息
  - `SearchHits#getHits()`：获取SearchHit数组，也就是文档数组
    - `SearchHit#getSourceAsString()`：获取文档结果中的_source，也就是原始的json文档数据



#### 完整代码

完整代码如下：

```java
@Test
void testMatchAll() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    request.source()
        .query(QueryBuilders.matchAllQuery());
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);

    // 4.解析响应
    handleResponse(response);
}

private void handleResponse(SearchResponse response) {
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        System.out.println("hotelDoc = " + hotelDoc);
    }
}
```



#### 小结

查询的基本步骤是：

1. 创建SearchRequest对象

2. 准备Request.source()，也就是DSL。

   ① QueryBuilders来构建查询条件

   ② 传入Request.source() 的 query() 方法

3. 发送请求，得到结果

4. 解析结果（参考JSON结果，从外到内，逐层解析）





#### match查询

全文检索的match和multi_match查询与match_all的API基本一致。差别是查询条件，也就是query的部分。

![image-20210721215923060](assets\image-20210721215923060.png) 



因此，Java代码上的差异主要是request.source().query()中的参数了。同样是利用QueryBuilders提供的方法：

![image-20210721215843099](assets\image-20210721215843099.png) 

而结果解析代码则完全一致，可以抽取并共享。



完整代码如下：

```java
@Test
void testMatch() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    request.source()
        .query(QueryBuilders.matchQuery("all", "如家"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```





#### 精确查询

精确查询主要是两者：

- term：词条精确匹配
- range：范围查询

与之前的查询相比，差异同样在查询条件，其它都一样。

查询条件构造的API如下：

![image-20210721220305140](assets\image-20210721220305140.png) 





#### 布尔查询

布尔查询是用must、must_not、filter等方式组合其它查询，代码示例如下：

![image-20210721220927286](assets\image-20210721220927286.png)



可以看到，API与其它查询的差别同样是在查询条件的构建，QueryBuilders，结果解析等其他代码完全不变。



完整代码如下：

```java
@Test
void testBool() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.准备BooleanQuery
    
    BoolQueryBuilder boolQuery = QueryBuilders.boolQuery();
    // 2.2.添加term
    boolQuery.must(QueryBuilders.termQuery("city", "杭州"));
    // 2.3.添加range
    boolQuery.filter(QueryBuilders.rangeQuery("price").lte(250));

    request.source().query(boolQuery);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```



#### 排序、分页

搜索结果的排序和分页是与query同级的参数，因此同样是使用request.source()来设置。

对应的API如下：

![image-20210721221121266](assets\image-20210721221121266.png)



完整代码示例：

```java
@Test
void testPageAndSort() throws IOException {
    // 页码，每页大小
    int page = 1, size = 5;

    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.query
    request.source().query(QueryBuilders.matchAllQuery());
    // 2.2.排序 sort
    request.source().sort("price", SortOrder.ASC);
    // 2.3.分页 from、size
    request.source().from((page - 1) * size).size(5);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```



#### 高亮

高亮的代码与之前代码差异较大，有两点：

- 查询的DSL：其中除了查询条件，还需要添加高亮条件，同样是与query同级。
- 结果解析：结果除了要解析_source文档数据，还要解析高亮结果

##### 高亮请求构建

高亮请求的构建API如下：

![image-20210721221744883](assets\image-20210721221744883.png)

上述代码省略了查询条件部分，但是大家不要忘了：高亮查询必须使用全文检索查询，并且要有搜索关键字，将来才可以对关键字高亮。

完整代码如下：

```java
@Test
void testHighlight() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.query
    request.source().query(QueryBuilders.matchQuery("all", "如家"));
    // 2.2.高亮
    request.source().highlighter(new HighlightBuilder().field("name").requireFieldMatch(false));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);

}
```



##### 高亮结果解析

高亮的结果与查询的文档结果默认是分离的，并不在一起。

因此解析高亮的代码需要额外处理：

![image-20210721222057212](assets\image-20210721222057212.png)

代码解读：

- 第一步：从结果中获取source。hit.getSourceAsString()，这部分是非高亮结果，json字符串。还需要反序列为HotelDoc对象
- 第二步：获取高亮结果。hit.getHighlightFields()，返回值是一个Map，key是高亮字段名称，值是HighlightField对象，代表高亮值
- 第三步：从map中根据高亮字段名称，获取高亮字段值对象HighlightField
- 第四步：从HighlightField中获取Fragments，并且转为字符串。这部分就是真正的高亮字符串了
- 第五步：用高亮的结果替换HotelDoc中的非高亮结果



完整代码如下：

```java
private void handleResponse(SearchResponse response) {
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        // 获取高亮结果
        Map<String, HighlightField> highlightFields = hit.getHighlightFields();
        if (!CollectionUtils.isEmpty(highlightFields)) {
            // 根据字段名获取高亮结果
            HighlightField highlightField = highlightFields.get("name");
            if (highlightField != null) {
                // 获取高亮值
                String name = highlightField.getFragments()[0].string();
                // 覆盖非高亮结果
                hotelDoc.setName(name);
            }
        }
        System.out.println("hotelDoc = " + hotelDoc);
    }
}
```



