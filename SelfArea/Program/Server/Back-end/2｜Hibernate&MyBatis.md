ORM:Objec-Realtional Mapping 对象关系映射。ORM既可以把记录转换成Java对象，也可以把Java对象转换为行记录。
在Java中的具体是指：将关系数据库中的表记录映射为Java对象


可以手动编写ORM(见Java300的ORM代码)，可以借助工具实现ORM：
- Spring JdbcTemplate 配合RowMapper 见Model代码
- Hibernate 实现更自动化的ORM，结合Javax.JPA(Java Persistence API)
	- JPA就是JavaEE的一个ORM标准，它的实现其实和Hibernate没啥本质区别，但是用户如果使用JPA，那么引用的就是`javax.persistence`这个“标准”包，而不是`org.hibernate`这样的第三方包。因为JPA只是接口，所以，还需要选择一个实现产品，跟JDBC接口和MySQL驱动一个道理。
- MyBatis是一种半自动化ORM框架[[#^0bda80|MyBatis]]

Hibernate和JPA的`SessionFactory`与`EntityManagerFactory`，MyBatis与之对应的是`SqlSessionFactory`和`SqlSession`

![[Pasted image 20220316103133.png]]

ORM的设计套路都是类似的。使用MyBatis的核心就是创建`SqlSessionFactory`，这里我们需要创建的是`SqlSessionFactoryBean`：

Spring提供的JdbcTemplate，它和ORM框架相比，主要有几点差别：

1.  查询后需要手动提供Mapper实例以便把ResultSet的每一行变为Java对象；
2.  增删改操作所需的参数列表，需要手动传入，即把User实例变为[user.id, user.name, user.email]这样的列表，比较麻烦。

但是JdbcTemplate的优势在于它的确定性：即每次读取操作一定是数据库操作而不是缓存，所执行的SQL是完全确定的，缺点就是代码比较繁琐，构造`INSERT INTO users VALUES (?,?,?)`更是复杂。


#Mybatis 介于全自动ORM如Hibernate和手写全部如JdbcTemplate之间，还有一种半自动的ORM，它只负责把ResultSet自动映射到Java Bean，或者自动填充Java Bean参数，但仍需自己写出SQL。MyBatis就是这样一种半自动化ORM框架。 ^0bda80



ORM框架是如何跟踪Java Bean的修改，以便在`update()`操作中更新必要的属性？

答案是使用Proxy模式，从ORM框架读取的User实例实际上并不是User类，而是代理类，代理类继承自User类，但针对每个setter方法做了覆写



Hibernate和JPA为了实现兼容多种数据库，它使用HQL或JPQL查询，经过一道转换，变成特定数据库的SQL，理论上这样可以做到无缝切换数据库，但这一层自动转换除了少许的性能开销外，给SQL级别的优化带来了麻烦。


ORM框架通常提供了缓存，并且还分为一级缓存和二级缓存。

一级缓存是指在一个Session范围内的缓存，常见的情景是根据主键查询时，两次查询可以返回同一实例

二级缓存是指跨Session的缓存，一般默认关闭，需要手动配置。二级缓存极大的增加了数据的不一致性，原因在于SQL非常灵活，常常会导致意外的更新。


