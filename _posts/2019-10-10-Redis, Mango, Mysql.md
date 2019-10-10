# Redis, Mango, Mysql
1. Redis用于高速缓存常用的数据，方便存取
2. Mango用于存储逐渐递增的数据，这些数据不会被经常存取，逐渐递增保存
3. Mysql服务于业务逻辑，存储结构化的数据

# 查询mangoDB日志的sql: 
$regex 正则表达式的方式匹配/1909254028000000002/
db.payment_log.find({formattedMessage:{$regex:/1909254028000000002/}},{formattedMessage: 1}).sort({timeStamp: -1}).limit(5);

