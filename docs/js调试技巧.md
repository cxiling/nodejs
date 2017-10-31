- 除了用```console.log```，还可以考虑用```debugger```打断点
```js
if (thisThing) {
    debugger;
}
```
结果;
- 为了更方便阅读obj的对象参数结构及内容，可以用```console.table```打印成表格
```js
var animals = [
    { animal: 'Horse', name: 'Henry', age: 43 },
    { animal: 'Dog', name: 'Fred', age: 13 },
    { animal: 'Cat', name: 'Frodo', age: 18 }
];
console.table(animals);
```
结果:


- 用```console.time()``` 和```console.timeEnd()```记录执行某段代码所消耗的时间
```js
console.time('Timer1');
 
var items = [];
 
for(var i = 0; i < 100000; i++){
   items.push({index: i});
}
 
console.timeEnd('Timer1');
```
