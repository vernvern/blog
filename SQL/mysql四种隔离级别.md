

## Read Uncommitted（未提交读）

A事务修改某条数据未提交，B事务读取这条数据的时候已经可以读到A事务修改的内容。(脏读)

A事务 | B事务
---|---
A begin |
   ||B begin
update T set test = '新的值' where id = 1|
   || selct test from T where id = 1  -- test = '新的值',可以读到A事务修改过但未提交的内容(脏读)
   || B commit
A commit |



## Read Committed（读提交）

A事务修改某条数据未提交，B事务读取这条数据还是原来的值，这时候A事务提交，B事务再次读取这个数据，会是新的值

A事务 | B事务
---|---
A begin |
   ||B begin
update T set test = '新的值' where id = 1|
   || selct test from T where id = 1  -- test = '原来的值'
A commit |
   || selct test from T where id = 1  -- test = '新的值'
   || B commit

## Repeatable Read（可重读）

A事务修改某条数据未提交，B事务读取这条数据还是原来的值，这时候A事务提交，B事务再次读取这个数据，还是原来的值

A事务 | B事务
---|---
A begin |
   ||B begin
update T set test = '新的值' where id = 1|
   || selct test from T where id = 1  -- test = '原来的值'
A commit |
   || selct test from T where id = 1  -- test = '原来的值'， 幻读
   || B commit


## Serializable（可串行化）

强制事务排序，不可能产生冲突，但是可能造成大量的超时和竞争锁现象

