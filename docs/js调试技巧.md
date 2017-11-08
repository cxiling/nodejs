- ### 除了用```console.log```，还可以考虑用```debugger```打断点
```js
if (thisThing) {
    debugger;
}
```

- ### 为了更方便阅读obj的对象参数结构及内容，可以用```console.table```打印成表格
```js
var animals = [
    { animal: 'Horse', name: 'Henry', age: 43 },
    { animal: 'Dog', name: 'Fred', age: 13 },
    { animal: 'Cat', name: 'Frodo', age: 18 }
];
console.table(animals);
```
**output:**
![](https://github.com/cxiling/nodejs/blob/master/imgs/O%5BW_ZM%24QWR~M_2PN80AEXWA.png)

- ### 用```console.time()``` 和```console.timeEnd()```记录执行某段代码所消耗的时间
```js
console.time('Timer1');
 
var items = [];
 
for(var i = 0; i < 100000; i++){
   items.push({index: i});
}
 
console.timeEnd('Timer1');
```
**output:**
```
Timer1: 9.010986328125ms
```

- ### 追踪程序层层回调的函数序列
```js
var car;
var func1 = function() {
    func2();
}

var func2 = function() {
    func4();
}
var func3 = function() {
}

var func4 = function() {
    car = new Car();
    car.funcX();
}
var Car = function() {
    this.brand = 'volvo';
    this.color = 'red';
    this.funcX = function() {
        this.funcY();
    }

    this.funcY = function() {
        this.funcZ();
    }

    this.funcZ = function() {
        console.trace('trace car')
    }
}
func1();
```
**output:**

![](https://github.com/cxiling/nodejs/blob/master/imgs/UUMB%5BYPZECQK%7D%40%60W9G3J5EX.png)

- ### debug()
调试时常用到两种方法
1. 在调试工具上打断点
2. 在代码上加debugger(上文第一点)
这两种方法都要在需要知道指定函数所在的位置，而使用```debug()```就无须知道函数的位置了
使用方式

![](https://github.com/cxiling/nodejs/blob/master/imgs/5L5BUXB5E~DYQ%5D%5DP%60%5BC%25X%25Q.png)
