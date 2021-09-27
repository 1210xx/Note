使用MyBatis提供的[[ORM]]机制，对业务逻辑人员而言，面对的纯粹的Java对象，这一层与通过[[Hibernate]]实现ORM而言基本一致。

对于其他的操作，Hibernate会自动生成SQL语言，而MyBatis需要开发者编写具体的SQL语句。

相对于Hibernate等的全自动ORM机制而言，MyBatis以SQL开发的工作量和数据库移植性上的让步，为系统设计提供了更大的自由空间。