# node主要使用模块(express,mysql连接)

## express简介与使用场景

1. express是基于http模块上封装过的第三方模块
2. 用于web服务端

## express搭建基本的web服务器

1. 下载好express后导入express模块

   ```javascript
   const express=require("express")
   ```

2. 创建web服务器

   ```
   const app=express()
   ```

3. 创建路由

   ​    app.get("/",(req,res)=>{

   ​        res.send()

   })

4. 启动web服务器

```
app.listen("80",function(){

​           })
```

  		第一个参数:端口号

​          第二个参数:回调函数

## express基本使用

1. app.get():处理客户端通过get请求端口

2. app.post():处理客户端通过post请求端口

    get和post的参数是一致的:第一个是请求的url

   ​											 第二个是请求的回调函数:回调参数包括req和res
   
   ​														 req:客户端的信息；
   
   ​                           							  res: 服务器需要响应的结果


​       

## express路由

1. 配置路由建议是创建express路由实例，然后再去配置具体的路径:

   ```javascript
   const express=require('express')
   const router=express.router()
   router.get('/',function(){
   })
   router.post('/home',function{
               })
   //所有类型的请求都可以访问
   router.all("/main",funciton(){
              
              })
   ```

2. 一般将express路由创建一个单独的模块，然后使用module.exports暴露出去

   ```js
   module.exports={
       router
   }
   ```

## express中间件

1. 全局中间件：通过app.use()注册 =>全局生效

   ```js
   app.use((req,res,next)=>{
       //匿名函数式创建中间件
       req和res是公用的参数，后面的路由或者中间件都是同一个参数
       next()//一定要调用next方法，才会跳转到下一个中间件或者路由
   })
   ```

2. 局部中间件:在路由模块中注册  =>只对当前的路由模块生效

   ```js
   conse mw=function(req,res,next){
       next()
   }
   app.get('/',mw,function(req,res){
       
   })
   ```

3. 中间件除了错误类型的中间件，其他中间件必须在路由设置之前配置

4. express错误中间件:  =>捕获整个流程过程中发生的错误

   ```js
   app.use((error,req,res,next)=>{
           console.log(error.message)
           })
   ```

5. express内置的中间件

   a.express.static:快速托管静态资源的内置中间件

   b.express.json：解析JSON格式的请求体数据（用兼容性，4.16.0+版本至以上）

   ​	req.body:获取客户端发送的请求体

   c.express.urlencoded ：解析URL-encoded格式的请求体数据(（用兼容性，4.16.0+版本上）

## 连接数据库

1. 链接数据库

    	a.npm下载mqsql

   ​	 b.创建数据库连接实例

   ```js
   const mysql=require('mysql')
   //通过mysql的createPool()方法创建mysql实例连接
   const mq=mysql.createPool({
     host:'127.0.0.1',//连接的主机ip
   	user:'root',//用户名
   	password:'123455',//密码
   	database:'tealist'//数据库名称
   });
   ```

2. 操作数据库:  =>使用mq.query()方法

   ```js
    mq.query('select 1',(err,res)=>{
        //第一个参数是sql语句，第二个参数是回调函数
   	if(err) return console.log(err.message)
    	else console.log(res)
    })
   ```

3. 插入语句操作

   ```js
   //？是占位符
   let str='insert into teas(name,price) values(?,?)'
   let msg={
   	name:'雪茶',
   	price:100
   }
   mq.query(str,[msg.name,msg.price],(err,res)=>{
       //当插入语句时，第一个是插入语句，第二个是插入的值(占位符的值)，第三个是回调函数
   	if(err) console.log(err.message)
       //当是插入语句是回调函数里面的res参数是对象
   	if(res.affectedRows===1){
   		console.log("数据插入成功")
   	}
   })
   ```

   ​		插入语句的便捷方式:如果数据对象的每个属性和数据表的字段一一对应，则通过快速方式

   ```js
   //通过set和？
   const sqlStr='insert into teas set ?'
   ```

4. 更改语句操作	

   ```js
   let str='update teas set name=?,price=? where id=2'
   let msg={
   	name:'雪茶',
   	price:100
   }
   mq.query(str,[msg.name,msg.price],(err,res)=>{
       //当插入语句时，第一个是更改语句，第二个是插入的值(占位符的值)，第三个是回调函数
   	if(err) console.log(err.message)
       //当是插入语句是回调函数里面的res参数是对象
   	if(res.affectedRows===1){
   		console.log("数据插入成功")
   	}
   })
   ```

   ​            更改语句简便方式:

   ```js
   const sqlStr='update teas set ? where id=?'
   ```

5. 删除语句操作（不建议使用）

   ```js
   const str='delect from teas where id=2'
   ```

6. 标记删除操作（实际开发推荐使用）=>为每行字段设置一个status的标记，然后通过update把status的状态值更改以至于达到删除效果，实际该行字段没有删除

   ```javascript
   const str='update teas set status=1 where id=?'
   ```

   