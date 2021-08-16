# Mybatis分页查询

### 原由

***

截止目前在项目中ORM框架选用Mybatis-Plus居多，可是选用Mybatis的情况也有不少，在使用过两个框架后，我更喜欢Mybatis-Plus,它本身是对Mybatis的增强，在BaseMapper中提供了很多方法，很多时候我们可以一句SQL都不写的实现很多基本查询，而且代码可读性也不差。不过框架的使用是项目一开始就定的，所以今天记一下关于Mybatis分页查询的具体使用。

### 方法

---

通过PageHelper插件

### 关于PageHelper

---

[![fWJ41A.png](https://z3.ax1x.com/2021/08/16/fWJ41A.png)](https://imgtu.com/i/fWJ41A)

[PageHelper**码云项目地址**](https://gitee.com/free/Mybatis_PageHelper)

### 如何使用

---

- 在项目pom.xml文件中添加依赖

非SpringBoot项目

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>最新版本</version>
</dependency>
```

SpringBoot项目

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.3.1</version>
</dependency>
```

- 配置拦截器

如果不是SpringBoot项目则需要进行配置拦截器，SpringBoot项目则不用，已经帮我们自动装配。

- 配置一些基本参数

  ```yml
  
  #分页插件
  pagehelper.helper-dialect=mysql
  pagehelper.params=count=countSql
  pagehelper.reasonable=true
  pagehelper.support-methods-arguments=true
  ```

  

- 具体使用:`PageHelper.startPage` 静态方法调用

  ```java
  //获取第1页，10条内容，
  PageHelper.startPage(1, 10);
  //紧跟着的第一个select方法会被分页
  List<User> list = userMapper.selectAll();
  //用PageInfo对结果进行包装
  PageInfo page = new PageInfo(list);
  //测试PageInfo全部属性
  //PageInfo包含了非常全面的分页属性
  ```

  PageInfo里包含的信息

  [![fWcukj.png](https://z3.ax1x.com/2021/08/16/fWcukj.png)](https://imgtu.com/i/fWcukj)

嗯，够用了。然后，分页查询也就结束了。