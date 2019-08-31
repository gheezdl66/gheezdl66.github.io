### [Spring Boot 实战](内嵌tomcat可以直接运行启动类启动)

####1、创建数据库

> create table demo1(
>
> ​        id int primary key auto_increment,
>
> ​        dname varchar(25),
>
> ​        dtype varchar(25)
>
> )charset=utf8;
>
> insert into demo values(default, 'aaa','aaa1');
>
> insert into demo values(default, 'bbb','bbb1');
>
> insert into demo values(default, 'ccc','ccc1');

####2.创建Spring boot 项目工程：Spring Initiallizr(要联网)

>**1. 选择依赖包**
>
>> 根据idea版本不同自带的spring boot版本不同，若spring boot版本为默认2.1.4版本则根据如下选则：
>> **Web**-->Web
>>
>> ![1565516601977](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565516601977.png)
>>
>> **Template Engines**-->[Thymeleaf](纯HTML+CSS+js)
>>
>> ![1565515540739](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565515540739.png)
>>
>> **SQL**-->Mysql; JDBC; Mybatis
>>
>> ![1565515687218](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565515687218.png)
>>
>> ***NoSql***-->分布式缓存，全文检索可自行选择
>>
>> ![1565515817467](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565515817467.png)
>>
>> 
>>
>> 根据idea版本不同自带的spring boot版本不同，若IDEA版本较高spring boot默认2.1.7版本则根据如下选则：
>>
>> **Web**-->Spring Web Starter
>>
>> ![1565515962971](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565515962971.png)
>>
>> **Template Engines**-->Thymeleaf
>>
>> ![1565516097284](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565516097284.png)
>>
>> **SQL**--> MySQL Drier; JDBC API; MyBatis Framework
>>
>> ![1565516167415](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565516167415.png)
>>
>> **NoSQL**-->和上一个版本一样自行选择
>>
>> ![1565516245739](C:\Windows\system32\config\SYSTEM~1\AppData\Local\Temp\1565516245739.png)

#### 3. pom.xml文件查包，添加jar包直接导

#### 4. 连接数据库，创建实体类

#### 5. dao(mapper)接口开始查询

#### 6. [映射文件](路径：1. dao层下 2. Resources下xml目录)

> 文件头：
>
> ```
> <?xml version="1.0" encoding="UTF-8"?>
> <!DOCTYPE mapper
>         PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
>         "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
> <mapper namespace="com.koem.mapper.EbookEntryMapper">
>     <select id="方法名" resultType="全限定类名/别名">
>         select * from table
>     </select>
> </mapper>
> ```

#### 7. [service接口层](同mapper/dao接口)

#### 8. 实现Service层

> **8.1 打注解 ==》@Service**
>
> > @Service
> >
> > public class BookinfoServiceImpl implements BookinfoService{
> >
> > ​        @override
> >
> > ​        public List<Bookinfo> queryXxxx(){
> >
> > ​                return bookinfoMapper;
> >
> > ​        }
> >
> > }
>
> **8.2 实现类内部注入dao层 ==》@Resource **
>
> > @Service
> >
> > public class BookinfoServiceImpl implements BookinfoService{
> >
> > ​        @Resource
> >
> > ​        private BookinfoMapper bookinfoMapper;
> >
> > 
> >
> > ​        @override
> >
> > ​        public List<Bookinfo> queryXxxx(){
> >
> > ​                return bookinfoMapper;
> >
> > ​        }
> >
> > }

#### 9. 写controller控制层

> **9.1 注解 @Controller**
>
> **9.2 内部注入service接口**
>
> **9.3 开始业务逻辑实现及跳转index页面**

#### 10.前端页面展示









