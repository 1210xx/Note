# ORM：Object-Relational Mapping



## 手动 ORM：
手写方法绑定PO Bean与数据库 ：
1. 获取表的信息
2. 绑定到对应的PO Bean中
3. 实现SQL类型和Java类型转换
4. 封装SQL语句
6. 建立连接
7. 执行SQL
8. 利用第2步的绑定实现ORM

## Spring JdbcTemplate ORM
Spring JdbcTemplate ORM 需要手动在查询时提供RowMapper映射

无需通过注释或者配置映射对应的JavaBean

通过JdbcTemplate执行SQL，提供的SQL

## Hibernate ORM

Hibernate ORM 通过@Entity 以及 @Column 将SQL的执行结果与JavaBean对应

实现自动化的ORM

通过hibernateTemplate执行SQL，提供的SQL

## MyBatis ORM
MyBatis ORM 通过Mapper接口显式的通过注解配置SQL以及对应的JavaBean
但是Mapper不需要实现，只需要通过注解MapperScan来实现SQL以及ORM

通过Mapper执行SQL，自己写的SQL
