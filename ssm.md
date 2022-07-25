# 初识spring

![image-20220629163716211](img/image-20220629163716211.png)

------



# Spring Framework系统架构

![image-20220629164804138](img/image-20220629164804138.png)



## IOC控制反转

![image-20220629165449549](img/image-20220629165449549.png)

![image-20220629170135042](img/image-20220629170135042.png)

## DI

![image-20220629170159130](img/image-20220629170159130.png)





![image-20220629170325803](img/image-20220629170325803.png)



![image-20220629170415807](img/image-20220629170415807.png)

## IOC入门案例

![image-20220717230628555](img/image-20220717230628555.png)

![image-20220717230705030](img/image-20220717230705030.png)

![image-20220717230845395](img/image-20220717230845395.png)

![image-20220717230913078](img/image-20220717230913078.png)

![image-20220717230942549](img/image-20220717230942549.png)

## DI入门案例

![image-20220717231834726](img/image-20220717231834726.png)



![image-20220717231850215](img/image-20220717231850215.png)

**注意**：spring会自动调用该setter方法，所以需提供对应方法

![image-20220717231938735](img/image-20220717231938735.png)

![image-20220717232033720](img/image-20220717232033720.png)

### **注意**

​	property内name属性需与serive中dao的名字相同，ref需与bean容器的dao名字相同

### **小总结**

​	bean相当于生成对象的容器，在DI案例中当主程序生成bean中的bookServiceImpl对象时，由于与bookDao有绑定关系，会先生成一个bookDaoImpl对象，然后将其通过setter方法传入bookServiceImpl类中，所以当主程序调用Service的save方法时会调用到Dao的save方法

## bean基础配置

![image-20220717234939913](img/image-20220717234939913.png)

### **别名配置**

![image-20220717235059260](img/image-20220717235059260.png)

### bean的作用范围配置

![image-20220717235611285](img/image-20220717235611285.png)

**小理解**

​	bean默认造出的对象都是一个对象，即bean造出的所有引用的地址相同,都指向一个对象,scope配置可以修改默认行为。

**作用范围说明**

![image-20220718000352952](img/image-20220718000352952.png)

## 实例化bean的四种方式

### **1.构造方法（常用）**

![image-20220718001505018](img/image-20220718001505018.png)

### 2.静态工厂（了解）

![image-20220718002737537](img/image-20220718002737537.png)

**作用：**若需在工厂中有必要的配置，则有必要用该方式实例化

### 3.实例工厂（了解）

![image-20220718003751333](img/image-20220718003751333.png)

**知识：**先造工厂的实例再通过方法造想要的对象

### 4.FactoryBean方式（实用）

第3种方式的优化版

![image-20220718004517811](img/image-20220718004517811.png)

## bean生命周期

![image-20220718005943041](img/image-20220718005943041.png)

### **bean销毁时机**

![image-20220718010056630](img/image-20220718010056630.png)

## 依赖注入四种方式

### 1.setter注入--引用类型

![image-20220718232808831](img/image-20220718232808831.png)

### 2.setter注入--简单类型

![image-20220718233339474](img/image-20220718233339474.png)

### 3.构造器注入--引用类型

![image-20220718234603478](img/image-20220718234603478.png)

### 4.构造器注入--简单类型

![image-20220718234710898](img/image-20220718234710898.png)

### 构造器注入--参数适配（了解）

![image-20220718234816817](img/image-20220718234816817.png)

### 依赖注入方式选择

![image-20220718234919041](img/image-20220718234919041.png)

### 依赖自动装配

![image-20220718235959045](img/image-20220718235959045.png)

![image-20220719000044781](img/image-20220719000044781.png)

### 依赖自动装配特征

![image-20220719000215575](img/image-20220719000215575.png)

## 注入集合对象

![image-20220719001012200](img/image-20220719001012200.png)

![image-20220719001025809](img/image-20220719001025809.png)

![image-20220719001058944](img/image-20220719001058944.png)

![image-20220719001111388](img/image-20220719001111388.png)

![image-20220719001129404](img/image-20220719001129404.png)

## 第三方数据管理对象使用

![image-20220719002259511](img/image-20220719002259511.png)

## 加载properties文件

![image-20220720002332684](img/image-20220720002332684.png)

**加载properties文件时注意要项**

![image-20220720003057390](img/image-20220720003057390.png)

## 创建容器的方式

![image-20220720003701485](img/image-20220720003701485.png)

## 获取bean的方式

![image-20220720004014410](img/image-20220720004014410.png)

## 容器类层次结构图

![image-20220720004532408](img/image-20220720004532408.png)

![image-20220720004643288](img/image-20220720004643288.png)

## 小总结

### 1.容器相关

![image-20220720004929413](img/image-20220720004929413.png)

### 2.bean相关

![image-20220720005017857](img/image-20220720005017857.png)

### 3.依赖注入相关

![image-20220720005221614](img/image-20220720005221614.png)

## 注解开发定义bean

![image-20220720113005638](img/image-20220720113005638.png)

## 纯注解开发

纯注解开发不再需要ApplicationContext.properties文件形式，改用注解形式进行开发，但需创建一个SpringConfig类

```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Configuration
@ComponentScan("Dao")
//组件扫描路径
public class SpringConfig {
}
```

```java
public class test {
    public static void main(String[] args) {
        //ApplicationContext ctx=new ClassPathXmlApplicationContext("applicationContext.xml");
        //原先的ClassPathXmlApplicationContext方式获取容器改为
        //AnnotationConfigApplicationContext注解方式获取
        ApplicationContext ctx=new AnnotationConfigApplicationContext(SpringConfig.class);
        BookDao bookDao = ctx.getBean("bookDao", BookDao.class);
        bookDao.save();
    }
}
```

![image-20220721004258692](img/image-20220721004258692.png)

![image-20220721004353284](img/image-20220721004353284.png)

### 注解开发bean作用范围与生命周期管理

![image-20220721010420165](img/image-20220721010420165.png)

```java
//jdk8之后想使用@PostConstruct和@PreDestory需引入以下依赖
<dependency>
  <groupId>javax.annotation</groupId>
  <artifactId>javax.annotation-api</artifactId>
  <version>1.3.2</version>
</dependency>
```

![image-20220721010702491](img/image-20220721010702491.png)

### 依赖注入

![image-20220721012231745](img/image-20220721012231745.png)

![image-20220721012410322](img/image-20220721012410322.png)

![image-20220721012443441](img/image-20220721012443441.png)

### 加载properties文件

![image-20220721012545786](img/image-20220721012545786.png)

### 第三方bean管理

![image-20220721095638159](img/image-20220721095638159.png)

**一般不写在SpringConfig类中，使用独立的配置类管理第三方bean**

```java
//在Config包下新建一个jdbc配置类
public class jdbcConfig {
    @Bean
    public DataSource dataSource(){
        DruidDataSource ds=new DruidDataSource();
        ds.setDriverClassName("com.mysql.jdbc.Driver");
        ds.setUrl("jdbc:mysql://localhost:3306/hrdb");
        ds.setUsername("root");
        ds.setPassword("123456");
        return ds;
    }
}
```

**将独立的配置类加入核心配置**

##### 方式一：导入式(推荐)

```java
public class jdbcConfig {
    @Bean
    public DataSource dataSource(){
        DruidDataSource ds=new DruidDataSource();
        //相关配置
        return ds;
    }
}
```

**使用@Import注解手动加入配置类到核心配置，此注解只能添加一次，多个数据请用数组格式**

```java
@Configuration
@Import(jdbcConfig.class)
public class SpringConfig {

}
```

##### 方式二：扫描式

```java
@Configuration
public class jdbcConfig {
    @Bean
    public DataSource dataSource(){
        DruidDataSource ds=new DruidDataSource();
        //相关配置
        return ds;
    }
}
```

```java
@Configuration
@ComponentScan({"config","Dao","Service"})
public class SpringConfig {

}
```

### 第三方bean依赖注入

​	**简单类型的依赖注入**

```java
public class jdbcConfig {
    @Value("com.mysql.jdbc.Driver")
    //也可将文件写到jdbc.properties中,如
    //@Value("${driverName}")
    private String DriverName;
    @Value("jdbc:mysql://localhost:3306/hrdb")
    private String Url;
    @Value("root")
    private String Username;
    @Value("123456")
    private String Password;
    @Bean
    public DataSource dataSource(){
        DruidDataSource ds=new DruidDataSource();
        ds.setDriverClassName(DriverName);
        ds.setUrl(Url);
        ds.setUsername(Username);
        ds.setPassword(Password);
        return ds;
    }
}
```

​	**引用类型的依赖注入**

![image-20220721103308588](img/image-20220721103308588.png)

## Xml配置对比注解配置

![image-20220721103734190](img/image-20220721103734190.png)

## Spring整合MyBatis

**需要的包：**druid(造dataSource) mybaties(3.5.6) mysql-connection mybaties-spring(1.3.0) spring-jdbc spring-context

```java
public class MybatisConfig {
    @Bean
    public SqlSessionFactoryBean sqlSessionFactoryBean(DataSource dataSource){
        SqlSessionFactoryBean sfb=new 		SqlSessionFactoryBean();
        //设置实体类包的别名
        sfb.setTypeAliasesPackage("domain");
        sfb.setDataSource(dataSource);
        return sfb;
    }
    @Bean
    public MapperScannerConfigurer mapperScannerConfigurer(){
        MapperScannerConfigurer msc=new MapperScannerConfigurer();
        //设置mapper所在的包
        msc.setBasePackage("Dao");
        return msc;
    }

}
```

![image-20220722233444035](img/image-20220722233444035.png)

```java
@Configuration
@ComponentScan({"Dao","Service"})
@PropertySource("classpath:jdbc.properties")
@Import({MybatisConfig.class,jdbcConfig.class})

public class SpringConfig {

}
```

```java
public class jdbcConfig {
    @Value("${jdbc.DriverName}")
    private String DriverName;
    @Value("${jdbc.Url}")
    private String Url;
    @Value("${jdbc.Username}")
    private String Username;
    @Value("${jdbc.Password}")
    private String Password;
    @Bean
    public DataSource dataSource(){
        DruidDataSource ds=new DruidDataSource();
       ds.setDriverClassName(DriverName);
        ds.setUrl(Url);
        ds.setUsername(Username);
        ds.setPassword(Password);
        return ds;
    }
}
```

```java
//jdbc.properties
jdbc.DriverName=com.mysql.cj.jdbc.Driver
jdbc.Url=jdbc:mysql://localhost:3306/hrdb
jdbc.Username=root
jdbc.Password=123456
```

```java
public class test {
    public static void main(String[] args) throws IOException {
        AnnotationConfigApplicationContext ctx=new AnnotationConfigApplicationContext(SpringConfig.class);
        UserService userService = ctx.getBean(UserService.class);
        System.out.println(userService.selectALL());
    }
}
```

​	Spring整合mybaties,其中mybaties的datasource来自druid(jdbcConfig）,druid的相关配置写在外面的resources下的jdbc.properties文件中

![image-20220721110658040](img/image-20220721110658040.png)

![image-20220721110746844](img/image-20220721110746844.png)

## Spring整合Junit

**需要的包：**junit   spring-test

![image-20220721112000017](img/image-20220721112000017.png)

## Aop

### Aop简介

![image-20220722234752047](img/image-20220722234752047.png)

![image-20220722235216098](img/image-20220722235216098.png)

### 核心概念

![image-20220722235535695](img/image-20220722235535695.png)

### 入门案例思路分析

![image-20220722235655801](img/image-20220722235655801.png)

![image-20220723000553854](img/image-20220723000553854.png)

![image-20220723000623136](img/image-20220723000623136.png)

![image-20220723000659872](img/image-20220723000659872.png)

![image-20220723000719777](img/image-20220723000719777.png)

![image-20220723000823648](img/image-20220723000823648.png)

![image-20220723000850000](img/image-20220723000850000.png)

![image-20220723000914312](img/image-20220723000914312.png)

### 工作流程

![image-20220723103840721](img/image-20220723103840721.png)

### 核心概念

![image-20220723104000721](img/image-20220723104000721.png)

### 切入点表达式

![image-20220723104339217](img/image-20220723104339217.png)

![image-20220723104641880](img/image-20220723104641880.png)

### 表达式通配符

![image-20220723104916081](img/image-20220723104916081.png)

![image-20220723110120999](img/image-20220723110120999.png)

### Aop通知类型

![image-20220723110536291](img/image-20220723110536291.png)

##### 前置通知

![image-20220723111958132](img/image-20220723111958132.png)

##### 后置通知

![image-20220723112028262](img/image-20220723112028262.png)

##### 环绕通知

![image-20220723112118530](img/image-20220723112118530.png)

![image-20220723112148909](img/image-20220723112148909.png)

##### 正常执行通知

![image-20220723112229122](img/image-20220723112229122.png)

##### 异常通知

![image-20220723112250079](img/image-20220723112250079.png)

### 测量业务层接口万次执行效率

![image-20220723183803394](img/image-20220723183803394.png)

![image-20220723183844500](img/image-20220723183844500.png)

![image-20220723183900799](img/image-20220723183900799.png)

### 通知获取数据

![image-20220723184125251](img/image-20220723184125251.png)

##### 获取切入点方法的参数

![image-20220723185426586](img/image-20220723185426586.png)

##### 获取返回值数据

![image-20220723185749884](img/image-20220723185749884.png)

##### 获取异常数据（了解）

![image-20220723185920103](img/image-20220723185920103.png)

### 百度网盘密码数据兼容处理

![image-20220723191233225](img/image-20220723191233225.png)

## Spring事务

### 简介

![image-20220724134948786](img/image-20220724134948786.png)

### 银行账户转账案例

![image-20220724140918449](img/image-20220724140918449.png)

![image-20220724140954456](img/image-20220724140954456.png)

![image-20220724141113458](img/image-20220724141113458.png)

![image-20220724141132130](img/image-20220724141132130.png)

![image-20220724141224060](img/image-20220724141224060.png)

### 事物角色

![image-20220724141731198](img/image-20220724141731198.png)

![image-20220724141940242](img/image-20220724141940242.png)

### 事物相关配置

![image-20220724142106313](img/image-20220724142106313.png)

**注意：**有些事物遇到异常是会回滚的（error,部分异常），ioExpection等不回滚，所以需要设置rollbackFor

### 事物的传播行为

![image-20220724143249868](img/image-20220724143249868.png)

##### 转帐业务追加日志

![image-20220724144111374](img/image-20220724144111374.png)

![image-20220724143614990](img/image-20220724143614990.png)

![image-20220724143657406](img/image-20220724143657406.png)

## Postman插件工具

![image-20220724212103064](img/image-20220724212103064.png)

## SpringMVC

### 概述

Spring与Servlet技术等同，但更简洁

![image-20220724145612551](img/image-20220724145612551.png)

**注意：**Springmvc和Spring使用的是不同的容器

### 入门案例

![image-20220724151605412](img/image-20220724151605412.png)

**注意：**还需引入tomcat插件，且将servlet坐标的scope设置为provided，因为tomcat7也有servlet坐标

![image-20220724151749702](img/image-20220724151749702.png)

![image-20220724151813285](img/image-20220724151813285.png)

![image-20220724151852118](img/image-20220724151852118.png)

**启动tocat时需要加载Springmvc技术**

![image-20220724152241102](img/image-20220724152241102.png)

![image-20220724152305500](img/image-20220724152305500.png)

![image-20220724152331413](img/image-20220724152331413.png)

![image-20220724152600502](img/image-20220724152600502.png)

![image-20220724152648683](img/image-20220724152648683.png)

![image-20220724152718786](img/image-20220724152718786.png)

![image-20220724152817557](img/image-20220724152817557.png)

### 入门案例工作流程

![image-20220724153336778](img/image-20220724153336778.png)

### Controller加载控制与业务bean加载控制

![image-20220724211104375](img/image-20220724211104375.png)

![image-20220724211214189](img/image-20220724211214189.png)

![image-20220724211328502](img/image-20220724211328502.png)

![image-20220724211635904](img/image-20220724211635904.png)

### 请求

##### 请求映射路径

![image-20220725224842580](img/image-20220725224842580.png)

##### Get请求传参

![image-20220725230208233](img/image-20220725230208233.png)

##### Post请求传参

![image-20220725230252766](img/image-20220725230252766.png)

##### Post请求中文乱码处理

![image-20220725230357135](img/image-20220725230357135.png)

##### 请求传参5种类型

**1.普通参数（地址名与形参变量名相同**）

![image-20220725231539903](img/image-20220725231539903.png)

**2.普通参数（地址名与形参变量名不同**）

![image-20220725231438861](img/image-20220725231438861.png)

**3.POJO参数**

![image-20220725231806728](img/image-20220725231806728.png)

**4.嵌套POJO参数**

![image-20220725232010648](img/image-20220725232010648.png)

![image-20220725232045710](img/image-20220725232045710.png)

**5.数组参数**

![image-20220725232134578](img/image-20220725232134578.png)

**6.集合参数**

![image-20220725232310444](img/image-20220725232310444.png)

##### **@RequestParam注解**

![image-20220725231724760](img/image-20220725231724760.png)

##### 接收请求中的json数据

![image-20220725233308173](img/image-20220725233308173.png)

![image-20220725233325531](img/image-20220725233325531.png)

![image-20220725233350693](img/image-20220725233350693.png)

![image-20220725233412857](img/image-20220725233412857.png)

##### @EnableWebMvc注解

![image-20220725233506034](img/image-20220725233506034.png)

##### @RequestBody

![image-20220725233609086](img/image-20220725233609086.png)

##### @RequestBody与@RequestParam区别

![image-20220725233715174](img/image-20220725233715174.png)

##### 日期类型参数传递

![image-20220725234402671](img/image-20220725234402671.png)

##### 类型转换器

![image-20220725234635511](img/image-20220725234635511.png)

### 响应

##### 响应页面

![image-20220725235341644](img/image-20220725235341644.png)

##### 响应文本数据

![image-20220725235400241](img/image-20220725235400241.png)

##### 响应json数据

![image-20220725235424847](img/image-20220725235424847.png)

![image-20220725235459630](img/image-20220725235459630.png)

##### @ResponseBody注解

![image-20220725235559540](img/image-20220725235559540.png)

##### 类型转换器

![image-20220725235646981](img/image-20220725235646981.png)

### 注意：请求和响应json数据都需依赖json jar包