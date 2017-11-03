# waterline
 ###### waterline是sails配套ORM

 ### 方法
 	
 	#### Models相关

 - ** .create() **
 	创建一条新的记录
 	```
 	Oauth.create({user: body.uid});
 	```
 - ** .find() **
 	查找匹配的所有记录，返回对象数组
 - ** .findOne() **
 	查找匹配的记录，返回一个对象，找不到则返回null
 - ** .update() **
 	更新匹配的所有记录，参数为```attrName:value```键值对
 - ** .destroy() **
 	销毁匹配的所有记录
 - ** .findOrCreate() **
 	查找匹配的记录，有则返回一个对象，没有则创建一条新的记录
 - ** .count() **
 	查找匹配的所有记录的数量
 - ** .native()/query() **
 	貌似和数据库操作有关的，还没具体了解，MongoDB适用.native()，其余SQL用.query()
 - ** .stream() **
 	返回一系列匹配的记录序列
 > https://sailsjs.com/documentation/reference/waterline-orm/models
