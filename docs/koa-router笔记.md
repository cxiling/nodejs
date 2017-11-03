访问的路径在路由中找不到匹配的，则抛出404
可以在router文件中，所有正常路径最后加
```js
router.all('*', async (ctx, next) => {
    ctx.throw(404);
})
```
[https://cnodejs.org/topic/57ac2ec1476898b472247e14](https://github.com/superalsrk/koa2-boilerplate/blob/master/src/routes/index.js)

[https://cnodejs.org/topic/57ac2ec1476898b472247e14](https://cnodejs.org/topic/57ac2ec1476898b472247e14)