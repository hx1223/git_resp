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