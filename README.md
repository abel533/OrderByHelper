# MyBatis 排序插件 OrderByHelper

类似分页插件 [PageHelper](https://github.com/pagehelper/Mybatis-PageHelper) 用法，支持对任意查询（Select）SQL 进行排序，如果原 SQL 存在排序，使用后会替换默认的排序。

当前支持的功能和分页插件 4.2.x 及以前版本的功能一样，没有特别的地方。

目前不支持参数形式用法，以后会根据反馈逐步完善。

## 引入依赖
```xml
<dependency>
    <groupId>tk.mybatis</groupId>
    <artifactId>orderby-helper</artifactId>
    <version>0.0.2</version>
</dependency>
```

## 配置拦截器
Spring 配置方式：
```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <!-- 其他配置 -->
    <property name="plugins">
        <array>
            <!-- 分页插件或其他插件，OrderBy 一定要在分页插件下面（主要是为了避免 count 也被增加排序） -->
            <bean class="tk.mybatis.orderbyhelper.OrderByHelper"/>
        </array>
    </property>
</bean>
```
Mybatis XML 配置方式：
```xml
<plugins>
    <!-- 分页插件或其他插件，OrderBy 一定要在分页插件下面（主要是为了避免 count 也被增加排序） -->
    <plugin interceptor="tk.mybatis.orderbyhelper.OrderByHelper"/>
</plugins>
```

如果使用 Spring Boot，可以参考 [Spring Boot - 配置排序依赖技巧](http://blog.csdn.net/isea533/article/details/53975720) 写个简单配置引入，并且保证在分页插件自动配置后执行。

## 0.0.2 更新日志 - 2017-05-18

- 更新cacheKey，防止缓存错误[#3](https://github.com/abel533/OrderByHelper/issues/3)

## 使用方式
在任意查询方法前调用，后面紧跟查询（避免中间出现可能存在异常或导致不执行查询的条件判断代码）：
```java
OrderByHelper.orderBy("id desc");
return mapper.select(country);
```

## 和 Spring Boot 集成

使用 [cuisongliu](https://github.com/cuisongliu) 提供的 https://github.com/cuisongliu/orderbyhelper-boot-starter

按照该项目首页的文档进行配置即可。

## 作者信息

MyBatis 工具网站:[http://mybatis.tk](http://www.mybatis.tk)

作者博客：http://blog.csdn.net/isea533

作者邮箱： abel533@gmail.com

Mybatis工具群： <a target="_blank" href="http://shang.qq.com/wpa/qunwpa?idkey=29e4cce8ac3c65d14a1dc40c9ba5c8e71304f143f3ad759ac0b05146e0952044"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="Mybatis工具" title="Mybatis工具"></a>

推荐使用Mybatis分页插件:[PageHelper分页插件](https://github.com/pagehelper/Mybatis-PageHelper)
