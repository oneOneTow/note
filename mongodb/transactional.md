## mongodb 事务
#### 事务支持
* mongo从4.0开始就支持事务
* 在4.0版本mongo支持multi-document transactions在replica sets
* 在4.2版本mongo采用分布式事务，并且multi-document transactions开始支持sharded clusters，合并了已经存在的multi-document transactions on replica sets 
> 总的来说就是4.2搞了一个分布式事务，即支持sharded clusters也兼容replica sets
* drivers要与mongo版本一致
#### 事务与操作
* 不能在事务向[capped collections](https://docs.mongodb.com/manual/core/capped-collections/)插入数据
* 在config,admin,local database下不能在事务中对collections进行读写操作
* 在事务中不能向system.* collections写入数据
* 不能返回执行计划
> You cannot return the supported operation’s query plan
* 在事务外创建的游标,在事务内不能调用getMore
* 在事务内创建的游标，在事务外不能调用getMore
* 4.2开始，不能在事务内的第一个操作就是 killCursors
* 在事务内不能改变databanse的目录，例如创建或者删除collection,index
#### count operation
* 4.0提供了countDocuments() as helper method，并且 The 4.0 drivers have deprecated the count() API.
* Starting in MongoDB 4.0.3, the mongo shell provides the db.collection.countDocuments() helper method that uses the $group with a $sum expression to perform a count.
#### Transactions and Read Concern
##### local
* read concern local 将会返回the node（接收到read请求的node）最新可用的数据,这个数据可能会被回滚（其他事务未提交的数据）
> 类似数据的读未提交
* For transactions on sharded cluster, "local" read concern cannot guarantee that the data is from the same snapshot view across the shards. If snapshot isolation is required, use "snapshot" read concern.
##### majority
* read concern majority 将会返回在这replica set成员大多数确认的数据（即不能回滚的数据）
> 类似读提交
* If the transaction does not use write concern “majority” for the commit, the "majority" read concern provides no guarantees that read operations read majority-committed data.
*For transactions on sharded cluster, "majority" read concern cannot guarantee that the data is from the same snapshot view across the shards. If snapshot isolation is required, use "snapshot" read concern.

