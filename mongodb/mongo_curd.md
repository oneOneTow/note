# mongodb curd
## mongo query
### 条件操作符
* where score = 75 
> {“score”:75}
> db.collections.find({"score":"75"})
* where score < 75 
> {“score”:{$lt:75}}
> db.collections.find({"score":{$lt:750}});
* where score <= 75 
> {"score" :{$lte:75}}
> db.collections.find({"score":{$let:75}})
* where score > 75 
>{"score":{$gt:75}}
> db.collections.find({"score":{$gt:75}})
* where score >= 75 
>{"score": {$gte:75}}
> db.collections.find({"score":{$gte:75}})
* where score != 75 
>{"score": {$ne:75}

### 逻辑运算
* $and
> db.collections.find({"number":"002","name":"lzq"});
* $or
> db.collections.find({$or:[{"number":"020","name":"lzq"}]});
* $or和$and 联合查询
> db,collections.find({$and:[{"date":"2019-07-01"}],$or:[{"number":"002","name":"lzq"}]})
* $in和$nin
> db.collections.find({"number":{$in:["001","002"]}});
* $exists 用来判断一个field是否存在
> db.collections.find({"age":{$exists:true}});
* $mod 取模运算
> db.collections.find({"age":{$mod:[5,1]}}) //age对5取模值等于1
* null查找元素不存在并且元素对应值为null的文档
> db.orders.find({"age":null}) // null和age不存在的记录都会被查询出来

### 分页查询
db.collections.find().limit(2).skip(1);
### 排序
db.collections.find().sort({"create_time":1,"name":-1}) //1为升序，-1为降序
### 计数
db.collections.find(条件).count();
db.collections.count(条件);
### 去重
db.collections.distinct("name",{age:{$ge:18}}) //第一个字段描述去重字段，第二参数查询条件

### 数组查询
db.collections.find({"names":"lzq"}) //只要包含lzq的都会被查出来
* $all
> db.collections.find({"names":{$all:["lzq","sss","zhangsan"]}});
* 按照下标查询
> db.collections.find("names.2":"lzq")
* 查询特定长度的数组
> db.collections.find("names":{$size:2})

#### 只查询摸个字段
*  
### 模糊查询
db.partnerInteractiveLog.find({sourceSys:"XXWLH",requestUrl:{"$regex":"/v1/bab/issue\\?.*$"}})
   .sort({requestDate:-1})
