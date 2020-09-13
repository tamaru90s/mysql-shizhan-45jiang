# 06-global-lock-and-table-lock

根据加锁的范围，MySQL里面的锁大致可以分成全局锁、表级锁和行锁三类。

## 全局锁

加全局读锁的方法，命令是Flush tables with read lock（FTWRL）。

全局锁的典型使用场景是，做全库逻辑备份。

对于全部是InnoDB引擎的库，建议选择使用-single-transaction参数。

## 表级锁

表锁的语法是 lock tables ... read/write

在还没有出现更细粒度的锁的时候，表锁是最常用的处理并发的方式。而对于InnoDB这种支持行锁的引擎， 一般不使用lock table命令来控制并发。

另一种表级锁是MDL（metadata lock）。MDL不需要显式使用，在访问一个表的时候会被自动加上。

当对一个表做增删改查操作的时候，加MDL读锁；当要对表做结构变更操作的时候，加MDL写锁。

如何安全地给小表加字段？ 比较理想的机制是，在alter table语句里面设定等待时间。

