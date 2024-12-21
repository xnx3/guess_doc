##  在application中配置

```
database.name=数据库名
database.ip=服务器ip地址
spring.datasource.url=jdbc:postgresql://${database.ip}:5432/${database.name}?currentSchema=架构名/模式名
spring.datasource.username= #数据库用户名
spring.datasource.password= #数据库密码

#PostgreSQL 驱动
spring.datasource.driver-class-name=org.postgresql.Driver
```

  

## 添加pom依赖

```
	<--PostgreSQL驱动-->
	<dependency>
      <groupId>org.postgresql</groupId>
      <artifactId>postgresql</artifactId>
      <version>42.7.4</version>
    </dependency>
```

​    