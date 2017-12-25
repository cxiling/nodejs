# waterline
 ###### waterline是sails配套ORM

 ### 方法
 
  **Models相关**

 - **.create()**
 	创建一条新的记录
 	```
 	Oauth.create({user: body.uid});
 	```
 - **.find()**
 	查找匹配的所有记录，返回对象数组

```js
  userlist.find().paginate({page: 1, limit: 10}) //查询第一页，每页10条
  userlist.find({limit:2,skip:3}) //查询第三到第五条数据
  userlist.find().sort('id ASC') //按id顺序排序
```


 - **.findOne()**
 	查找匹配的记录，返回一个对象，找不到则返回null
 - **.update()**
 	更新匹配的所有记录，参数为```attrName:value```键值对
 - **.destroy()**
 	销毁匹配的所有记录,为确保记录是否存在，可以先用find判断下，但一般不建议
 - **.findOrCreate()**
 	查找匹配的记录，有则返回一个对象，没有则创建一条新的记录
 - **.count()**
 	查找匹配的所有记录的数量
 	返回总数

  ```js
  userlist.count()
  ```
 - **.native()/query()**
  貌似和数据库操作有关的，还没具体了解，MongoDB适用.native()，其余SQL用.query()
 - **.stream()**
  返回一系列匹配的记录序列

 > https://sailsjs.com/documentation/reference/waterline-orm/models

 - **.toJSON()**
 - **.toObject()**

 ### Model属性配置

 > https://sailsjs.com/documentation/concepts/models-and-orm/attributes

 
  - **type** 
   - string
   - text
   - integer
   - float
   - date
   - datetime
   - boolean
   - binary
   - array
   - json
   - mediumtext
   - longtext
   - objectid


  - **关联model**

  ```js
    // form models 定义 
    //一对一
    module.exports = {
        name:'string',
        title: 'string', //标题
        owner:{
          model:'user'
        }

    }

  ```

  ```js
    //Controller文件
    form.find({name:'e'}).populate('owner')//填入关联数据
  ```

  原数据：

  ```js
    {
      "owner": 3,
      "title": "m",
      "name": "e",
      "createdAt": "2017-11-23T06:33:43.314Z",
      "updatedAt": "2017-11-23T06:33:43.314Z",
      "id": 11006
    }
  ```


  output:

  ```js
    {
      "owner": {
        "account": "3634965",
        "mail": "chenxiling@52tt.com",
        "name": "secret",
        "password": "6fdb05818235c41717279c023cf6bb9567c0bdd6ec776e1ca14a6b1b29e29533",
        "head": "https://api.52tt.com/face?account=tt3634965",
        "phone": "",
        "sex": 0,
        "comments": null,
        "status": 0,
        "createdAt": "2017-11-03T03:39:49.427Z",
        "updatedAt": "2017-11-03T07:43:56.344Z",
        "id": 3,
        "lastLogin": "2017-11-03T07:43:56.342Z"
      },
      "title": "m",
      "name": "e",
      "createdAt": "2017-11-23T06:33:43.314Z",
      "updatedAt": "2017-11-23T06:33:43.314Z",
      "id": 11006
    }
  ```

  追加关联

  ```js
  finn.adoptedPets.add(jake.id);
  finn.save()
  ```

  移除关联

  ```js
  r[0].pets.remove(7);
  r[0].save(console.log)
  
  /*
  { pets:
      [
       {
         name: 'Rainbow Dash',
         color: 'blue',
         id: 8,
         createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
         updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) 
        },
        { 
          name: 'Applejack',
           color: 'orange',
           id: 9,
           createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
           updatedAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST) 
        }
      ],
    name: 'Mike',
    age: 16,
    createdAt: Wed Feb 12 2014 18:06:50 GMT-0600 (CST),
    updatedAt: Wed Feb 12 2014 19:30:54 GMT-0600 (CST),
    id: 7 
  }

  */

  ```

  - **生命周期**

```js
{
  identity:
  connection:
  attributes:{
    name:{type:'string',unique:true,required:true}
    ...
  },
  beforeValidate: fn(values, cb)
  afterValidate: fn(values, cb)
  beforeCreate: fn(values, cb)
  afterCreate: fn(newlyInsertedRecord, cb)
}
```


 - **unique**

 在```exec()```方法里不能获取unique错误，只能通过```try...catch(err)```

 - **查询条件**
   - '<' 
   - '<='
   - '>'
   - '>='
   - '!'
   - 'like' 从头匹配{'like':'123'},从尾匹配{'like':'%123'}
   - 'contains' 任意位置包含
   - 'startsWith'
   - 'endWith'

   ```js
    userlist.find({date:{'<':new Date('2/4/2014')}})
   ```

  - **主键**
默认指定数据库自动加的id为主键，
如果要自定义主键,需要对model加```autoPK:false```(不使用默认主键)，并在想要自定义的主键字段加上```primaryKey:true```
```js
const FormInfo = Waterline.Collection.extend({
    identity: "form_info",
    connection: "myMongo",
    attributes: {
        create_type: {type: 'integer', defaultsTo: 0},// 0 客服创建，1 邮件创建/旧版 
        cms_id:      {model:'form_user'},//客服CMS ID
        form_id:     {type: 'integer', required: true, unique: true, primaryKey:true},//工单ID
    },
    autoPK: false,
});
```
表关系关联只会通过主键id来获取
