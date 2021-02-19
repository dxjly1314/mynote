# spring学习

#### 介绍
spring学习笔记

#### 软件架构
软件架构说明


#### 安装教程

1.  xxxx
2.  xxxx
3.  xxxx

#### 使用说明

1.  xxxx
2.  xxxx
3.  xxxx

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


#### 码云特技

1.  使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2.  码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3.  你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4.  [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5.  码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6.  码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)


# spring

maven仓库：
```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.4.RELEASE</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-jdbc</artifactId>
    <version>5.2.4.RELEASE</version>
</dependency>
```

spring 的优点：

- spring是一个免费的开源框架（容器）
- spring是一个轻量级的，非入侵的框架
- 控制反转（IOC）面向切面的编程（AOP）
- 支持事务处理，对框架整合的支持

Spring就是一个轻量级，非入侵的控制反转（IOC）和面向切面（AOP）的框架！！

Spring Boot-构建一切

Spring Cloud-协调一切

Spring Cloud Date Flow-连接一切

![spring](./img/spring.png)

## 1.IOC理论推导

看代码略

对象的创建由用户创建，低层代码中不写明确的实现类。


## 2.IOC本质
控制反转：是一种设计思想，DI（依赖注入是实现IOC的一种方式）。

- 控制反转：一种通过描述xml文件或注解，并通过第三方去产生或者获取特点对象的方式。

- 在spring中控制反转就是IOC容器，其实现方式就是依赖注入。

## 3.hello Spring
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="..." class="...">  
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <bean id="..." class="...">
        <!-- collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions go here -->

</beans>
```

**IOC创建bean的两种方式：**

1. 无参构造

   - 先使用无参构造器创建出对象

   - 再使用set方法将对于的值一 一赋值进去

   结论：使用无惨构造就一定要有   **无参构造器和set方法**

   ```xml
   <bean id="student1" class="com.summer.pojo.Student">
           <property name="name" value="summer"></property>
   </bean>
   ```
property：属性
ref：对象
value：值
2. 有参构造

   - 有参构造在创建对象的时候就将值赋值进去，无需set方法

​        结论：使用无惨构造就一定要有   **有参构造器**

有参构造的方法：

   1. 下标赋值

      ```xml
      <!--    下标-->
          <bean id="student2" class="com.summer.pojo.Student">
             <constructor-arg index="0" value="summer"></constructor-arg>
              <constructor-arg index="1" value="20"></constructor-arg>
          </bean>
      ```

   2. 类型赋值（不建议使用）

      ```xml
      <!--    类型-->
          <bean id="student3" class="com.summer.pojo.Student">
              <constructor-arg type="java.lang.String" value="summer"></constructor-arg>
              <constructor-arg type="int" value="20"></constructor-arg>
          </bean>
      ```

   3. 参数名(掌握)

      ```xml
      <!--    名称-->
          <bean id="student4" class="com.summer.pojo.Student">
              <constructor-arg name="name" value="summer"></constructor-arg>
              <constructor-arg name="age" value="20"></constructor-arg>
          </bean>
      ```

IOC容器在创建对象的时候会把容器中的所有的对象都创建出来。（是不是单利模式蛤）

spring这个容器类似于婚介网站！！
只会创建一个实例

## 4.spring配置说明

### 4.1别名

```xml
<!--别名-->
    <alias name="student1" alias="student-NoParameters"></alias>
```

### 4.2Bean的配置

```xml
<!--    下标-->
    <bean id="student2" class="com.summer.pojo.Student" name="stu1 stu2,stu3;stu4">
       <constructor-arg index="0" value="summer"></constructor-arg>
        <constructor-arg index="1" value="20"></constructor-arg>
    </bean>
```

id：唯一标识

class：全类名：报名+类名

name 也可以取别名，并且可以取多个别名      分割符可以为：1. 空格  2. 逗号  3. 分号

### 4.3 import

```xml
<import resource="beans.xml"></import>
```

将不同的xml文件导入，很智能，自动寻找需要的bean文件

## 5.DI依赖注入

1.构造器注入

​	如上文所述

2.set方式注入

依赖注入
- 依赖：bean的创建是依赖于spring容器来创建的。
- 注入：bean的参数注入是由set方法来注入的。

Student 类

```java
public class Student {
    private String name;
    private Address address;
    private String[] books;
    private List<String> hobbys;
    private Map<String,String> card;
    private Set<String> game;
    private String wife;
    private Properties info;
}
```

xml文件注入

```xml
 <bean id="student" class="com.summer.pojo.Student">
        <property name="name" value="summer"></property>
        <property name="address" ref="address"></property>
        <property name="books">
            <array>
                <value>红楼梦</value>
                <value>水浒传</value>
                <value>三国演义</value>
            </array>
        </property>
        <property name="hobbys">
            <list>
                <value>唱跳</value>
                <value>篮球</value>
                <value>rap</value>
            </list>
        </property>
        <property name="card">
            <map>
               <entry key="卡号" value="212121"></entry>
               <entry key="密码" value="231212"></entry>
            </map>
        </property>
        <property name="game">
            <set>
                <value>刀塔</value>
                <value>lol</value>
            </set>
        </property>
        <property name="info">
            <props>
                <prop key="username">summer</prop>
            </props>
        </property>
        <property name="wife">
            <null></null>
        </property>
    </bean>
```

3.其他拓展注入

- p 命名空间

  约束：

  ```xml
  xmlns:p="http://www.springframework.org/schema/p"     
  ```
  使用:
  ```xml
  <bean id="userp" class="com.summer.pojo.User" p:name="summer" p:age="20"/>
  ```

- c  命名空间

  约束：

  ```xml
   xmlns:c="http://www.springframework.org/schema/c"
  ```
  使用:
  ```xml
  <bean id="userc" class="com.summer.pojo.User" c:name="summer" c:age="20"/>
  ```


## 6.Bean Scops

![TIM截图20200330202155](./img/TIM截图20200330202155.png)

单利模式(singleton)：

```xml
<bean id="userp" class="com.summer.pojo.User" scope="singleton"/>
```

原型模式(prototype)：

```xml
<bean id="userc" class="com.summer.pojo.User" scope="prototype"/>
```

## 7.Bean的自动装配

开启自动装配之后，spring会在beans上下文中自动去寻找所需的类型进行装配。

主要是一个类中有其他类需要注入其他类才可以完成注入的情形。

### 1.autowire

```xml
<bean id="userp" class="com.summer.pojo.User" autowire="byName"/>
<bean id="userc" class="com.summer.pojo.User" autowire="byType"/>
```

### 2.使用注解实现自动装配

- 开启支持注解

  ```xml
  <context:annotation-config/>
  ```
- 将所需的bean在xml文件中配置
	```xml
	<bean id="dog" class="com.summer.pojo.Dog"/>
  <bean id="cat" class="com.summer.pojo.Cat"/>
  <bean id="people" class="com.summer.pojo.People"/>
	```
- 在对应的类中加入注解
	```java
	@Autowired
    private Cat cat;
  @Autowired
    private Dog dog;
	```
这样就可以实现自动注入了。

#### 三种注解：
1. @Autowired（基本都是这个）
   对应autowire="byName"

2. @Qualifier
   对应autowire="byType"

3. @Resource
   java中的原生注解，功能强大，具有byName和byType两个功
   先通过名字查找，再通过类型查找，都找不到则报错。

## 8.注解开发：

上述都为简化bean的配置的方法，那么如何做到最少配置和0配置呢？

那么就需要我们使用注解进行开发了。

### 1.最少配置

- 开启扫描包

  ```xml
  <context:component-scan base-package="com.summer.pojo"/>
  ```

  spring 会自动的去扫描这个包下面的所有类，带有@Component注解的类spring就会在beans中自动创建。

  注意：

  ```xml
  <context:annotation-config/>
  <!--component-scan就不需要annotation-config了-->
  ```

- 在类上加@Component

  ```java
  @Component
  public class User {
      @Value("summer")
      private String name;
      private int age;
      @Autowired
      private Dog dog;
      @Autowired
      private Cat cat;
  }
  ```

#### 补充：

@Component的作用相当于：

```xml
 <bean id="user" class="com.summer.pojo.User"/>
```

 @Autowired的作用相当于

```xml
 <bean id="user" class="com.summer.pojo.User" autowire="byName"/>
```

  @Component的衍生注解：

- @Repository（dao层）
- @Service（service层）
- @Controller（controller层）

  @Value()
  简单的注入可以使用@Value()进行赋值

  复杂的DI注入还是使用配置文件

### 2. 0配置文件`@Bean` and `@Configuration`

本质就是将xml 文件变成了java类（好处就是更加的灵活）

- 写一个配置类

  ```java
  @Configuration
  @ComponentScan("com.summer.pojo")
  public class appconfig {
      @Bean
      public User user(){
          return new User();
      }
  }
  ```
  

补充：

1.加上@Configuration相当于

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans></beans>
```
  spring就会把这个类当成一个配置文件处理
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans></beans>
```

  spring就会把这个类当成一个配置文件处理

  2.加上@Bean相当于

```xml
<bean id="user" class="com.summer.pojo.User"/>
```

  2.加上@Bean相当于

  ```xml
<bean id="user" class="com.summer.pojo.User"/>
  ```

  3.加上@ComponentScan("com.summer.pojo")相当于

  ```xml
<context:component-scan base-package="com.summer.pojo"/>
  ```

  4.方法名就是id（首字母小写）

  5.返回值就是class

## 9.代理模式：

1. 接口
2. 真实角色
3. 代理角色
4. 客户端访问代理角色
静态代理：


动态代理：1.基于接口2.基于类的动态代理

- 基于接口：JDK动态代理
- 基于类：cglib
- java字节码实现：javasist

了解两个类：

- Proxy：代理
- Invocationhandler: 调用处理程序

## 10.spring实现AOP

注意点：动态代理代理的是一类接口

环境搭建

- UserServer

```java
public interface UserServer {
    void add();
    void delete();
    void update();
    void select();
}

```

- UserServerImpl

```java
public class UserServerImpl implements UserServer {
    public void add() {
        System.out.println("add");
    }

    public void delete() {
        System.out.println("delete");
    }

    public void update() {
        System.out.println("update");
    }

    public void select() {
        System.out.println("select");
    }
}
```

### 方式一：使用Spring的API接口

- Log类

```java
public interface Log {
    void message();
}
```

- BeforeLog

```java
public class BeforeLog implements Log, MethodBeforeAdvice {
    public void message() {
        System.out.println("BeforeLog");
    }

    public void before(Method method, Object[] objects, Object o) throws Throwable {
        message();
    }
}
```

- AfterLog

```java
public class AfterLog implements AfterReturningAdvice,Log {

    public void afterReturning(Object o, Method method, Object[] objects, Object o1) throws Throwable {
        message();
    }

    public void message() {
        System.out.println("AfterLog");
    }
}
```

- applicationcontext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="userServer" class="com.summer.server.UserServerImpl"/>
    <bean id="AfterLog" class="com.summer.log.AfterLog"/>
    <bean id="beforeLog" class="com.summer.log.BeforeLog"/>
    <aop:aspectj-autoproxy/>

    <aop:config>
        <aop:pointcut id="pointcut" expression="execution(* com.summer.server.UserServerImpl.*(..))"/>
        <aop:advisor advice-ref="beforeLog" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="AfterLog" pointcut-ref="pointcut"/>
    </aop:config>

</beans>
```

- 测试

```java
public class mytest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationcontext.xml");
        UserServer userServer = (UserServer) context.getBean("userServer");
        userServer.add();
    }
}
```

### 方式二:   使用自定义接口来实现AOP

- DiyPointCut

```java
public class DiyPointCut {

    public void before(){
        System.out.println("before");
    }
    public void after(){
        System.out.println("after");
    }
}
```

- applicationcontext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="userServer" class="com.summer.server.UserServerImpl"/>
    <bean id="diyPointCut" class="com.summer.diy.DiyPointCut"/>

    <aop:config>
        <aop:aspect ref="diyPointCut">
            <aop:pointcut id="pointcut" expression="execution(* com.summer.server.UserServerImpl.*(..))"/>
            <aop:before method="before" pointcut-ref="pointcut"/>
            <aop:after method="after" pointcut-ref="pointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```

- 测试

```java
public class mytest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationcontext.xml");
        UserServer userServer = (UserServer) context.getBean("userServer");
        userServer.add();
    }
}
```

### 方式三：使用注解实现

- AnnotationPointCut

```java
public class AnnotationPointCut {
    @Before("execution(* com.summer.server.UserServerImpl.*(..))")
   public void before(){
       System.out.println("before");
   }

    @After("execution(* com.summer.server.UserServerImpl.*(..))")
   public void after(){
       System.out.println("after");
   }
}
```

- applicationcontext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="userServer" class="com.summer.server.UserServerImpl"/>
    <bean id="annotationPointCut" class="com.summer.diy.AnnotationPointCut"/>
      <!--开启注解支持-->
    <aop:aspectj-autoproxy/>

</beans>
```

- 测试

```java
public class mytest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationcontext.xml");
        UserServer userServer = (UserServer) context.getBean("userServer");
        userServer.add();
    }
}
```

## 12.整合Mybatis

1.导入相关jar包

1. log4j
2. junit
3. mybatis
4. mysql-connection-java
5. spring-webmvc
6. spring-jdbc
7. aspectj
8. mybatis-spring
9. lombok

```xml
   <dependencies>
        <!-- https://mvnrepository.com/artifact/log4j/log4j -->
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>

        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>


        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.47</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.10.RELEASE</version>
        </dependency>

        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.1.10.RELEASE</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.4</version>
        </dependency>

        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>

        <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.8</version>
            <scope>provided</scope>
        </dependency>

    </dependencies>
```
### 原来编写mybatis的方式：

1. 编写实体类：Student

   ```java
   package com.summer.pojo;
   
   import java.util.Date;
   
   public class Student {
       private int id;
       private String name;
       private String unick;
       private String ugender;
       private String upass;
       private Date addtime;
       //get set  toString
   }
   
   ```

   

2. 编写核心配置文件：

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE configuration
     PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
     "http://mybatis.org/dtd/mybatis-3-config.dtd">
   <configuration>
     <environments default="development">
       <environment id="development">
         <transactionManager type="JDBC"/>
         <dataSource type="POOLED">
           <property name="driver" value="${driver}"/>
           <property name="url" value="${url}"/>
           <property name="username" value="${username}"/>
           <property name="password" value="${password}"/>
         </dataSource>
       </environment>
     </environments>
     <mappers>
       <mapper resource="org/mybatis/example/BlogMapper.xml"/>
     </mappers>
   </configuration>
   ```

   

3. 编写接口

   ```java
   public interface StudentDaoMapper {
       public List<Student> selectAll();
   }
   ```

   

4. 编写Mapper.xml文件

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.summer.dao.StudentDaoMapper">
       <select id="selectAll" resultType="Student">
           select * from student;
       </select>
   </mapper>
   ```

   

5. 测试

   ```java
    @Test
    public void test01() throws IOException {
    	String res = "mybatis-config.xml";
       InputStream inputStream = Resources.getResourceAsStream(res);
        
       SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        
       SqlSession sqlSession = sqlSessionFactory.openSession(true);
        
       UserDaoMapper mapper = sqlSession.getMapper(UserDaoMapper.class);
       List<Student> list = mapper.selectAll();
       System.out.println(list);
    }
   ```

## 13.使用spring整合mybatis

我们在测试类中看见

```java
String res = "mybatis-config.xml";
InputStream inputStream = Resources.getResourceAsStream(res);     
SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
SqlSession sqlSession = sqlSessionFactory.openSession(true);
```

我们需要在代码中手动创建SqlSessionFactory和SqlSession

现在我们可以通过spring的IOC容器来帮助我们自动创建他们

### 整合步骤：

pojo依然使用上面的student

### 使用SqlSessionTemplate

1.编写一个spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
<!--DataSource-->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="url" value="jdbc:mysql://localhost/jspdatabase"/>
        <property name="username" value="jspdatabase"/>
        <property name="password" value="root"/>
    </bean>
<!--sqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
        <!--绑定mybatis的配置文件的位置-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
        <property name="mapperLocations" value="classpath:com/summer/dao/*.xml"/>
    </bean>
<!--SqlSessionTemplate-->
    <bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
        <constructor-arg index="0" ref="sqlSessionFactory"/>
    </bean>
</beans>
```

2.编写实现类

```java
public class StudentDaoImpl implements StudentDaoMapper{

    private SqlSessionTemplate sqlSession;

    public StudentDaoImpl(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<Student> selectAll() {
        StudentDaoMapper mapper = sqlSession.getMapper(StudentDaoMapper.class);
        return mapper.selectAll();
    }
}
```

代码可以看到我们只是在原来的基础上多封装了一层，每次调用的时候不需要sqlsession了，而是在基础代码中已经使用过了sqlsession。

3.编写ApplicationContext.xml将bean交给IOC

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <import resource="spring-dao.xml"/>
    <bean id="studentMapper" class="com.summer.dao.StudentDaoImpl">
        <constructor-arg index="0" ref="sqlSession"/>
    </bean>
</beans>
```

4.测试

```java
    @Test
    public void test01() throws IOException {
       ApplicationContext context = new ClassPathXmlApplicationContext("ApplicationContext.xml");
        StudentDaoMapper userMapper = context.getBean("studentMapper", StudentDaoMapper.class);
        List<Student> list = userMapper.selectAll();
        System.out.println(list);
    }
```

### 使用SqlSessionDaoSupport

我们在实现类上面继承一个SqlSessionDaoSupport

我们就可以不用在spring-dao.xml 中创建SqlSessionTemplate

而我们在创建这个实现类的时候要将sqlSessionFactory丢到这个实现类中

因为我们继承了SqlSessionDaoSupport，而这个SqlSessionDaoSupport在他的实现类中使用sqlSessionFactory获得了SqlSessionTemplate。并用getSqlSession方法，返回SqlSessionTemplate。

1.StudentDaoImpl2

```java
public class StudentDaoImpl2 extends SqlSessionDaoSupport implements StudentDaoMapper {
    public List<Student> selectAll() {
        return getSqlSession().getMapper(StudentDaoMapper.class).selectAll();
    }
}
```

2.ApplicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
    <import resource="spring-dao.xml"/>
    <bean id="studentMapper2" class="com.summer.dao.StudentDaoImpl2">
        <property name="sqlSessionFactory" ref="sqlSessionFactory"/>
    </bean>
</beans>
```

## 14.声明式事务

### 1.回顾事务

- 要么都成功，要么都失败！
- 保证数据的一致性

### 2.事务的ACID原则

- 原子性
- 一致性
- 隔离性
- 持久性 

### 3.spring 开启事务的管理

- 编程式事务（在代码中添加事务）
- 声明式事务（AOP）

配置事务：

​	在spring-dao.xml 中开事务，并将事务使用aop横切进入代码中

```xml
	<!--开启事务-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <constructor-arg ref="dataSource" />
    </bean>

     <tx:advice id="txAdvice" transaction-manager="transactionManager">
		<!--配置事务的特性-->
         <tx:attributes>
             <tx:method name="*" propagation="REQUIRED"/>
         </tx:attributes>
     </tx:advice>

    <aop:config>
	<!--配置切点-->
     <aop:pointcut id="txPointCut" expression="execution(* com.summer.mapper.*.*(..))"/>
		<!--配置切面-->
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointCut"/>
    </aop:config>
```

## 补充：

spring 的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

  

</beans>
```

mybatis的配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>


</configuration>
```










