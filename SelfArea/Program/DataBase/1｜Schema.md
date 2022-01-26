在数据库中，schema（发音 “skee-muh” 或者“skee-mah”，中文叫模式）是数据库的组织和结构，schemas和schemata都可以作为复数形式。模式中包含了schema对象，可以是**表**(table)、**列**(column)、**数据类型**(data type)、**视图**(view)、**存储过程**(stored procedures)、**关系**(relationships)、**主键**(primary key)、**外键(**foreign key)等。数据库模式可以用一个可视化的图来表示，它显示了数据库对象及其相互之间的关系


## Schema和DataBase是否等同？

涉及到数据库的模式有很多疑惑，问题经常出现在模式和数据库之间是否有区别，如果有，区别在哪里。

### 取决于数据库供应商

对schema（模式）产生疑惑的一部分原因是数据库系统倾向于以自己的方式处理模式

（1）MySQL的文档中指出，在物理上，模式与数据库是同义的，所以，模式和数据库是一回事。

（2）但是，Oracle的文档却指出，某些对象可以存储在数据库中，但不能存储在schema中。 因此，模式和数据库不是一回事。

（3）而根据这篇SQL Server技术文章[SQLServer technical article](https://technet.microsoft.com/en-us/library/dd283095%28v=sql.100%29.aspx)，schema是数据库SQL Server内部的一个独立的实体。 所以，他们也不是一回事。

因此，取决于您使用的RDBMS，模式和数据库可能不一样。