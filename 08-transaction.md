begin/start transaction命令并不是一个事务的起点，
在执行到它们之后的第一个操作InnoDB表的语句（第一个快照读语句），
事务才真正启动。
如果你想要马上启动一个事务，可以使用
start transaction with consistent snapshot这个命令。

InnoDB里面每个事务有一个唯一的事务ID，叫做transaction id。它是在
事务开始的时候想InnoDB的事务系统申请的，是按申请顺序严格递增的。

数据表中的一行记录，其实可能有多个版本（row），每个版本有自己的row trx_id。

![][08-01-row-stat.png]