### 学习分号的插入机制

```javascript
var b = 12;
function f() {}

// 当@1和@2连在一起不能够解析的时候,分号才会自动插入
var a = b // @1
f() // @2

// 当@3和@4连在一起能够解析(虽然可能会解析失败)的时候,分号就不会自动插入了
// var c = b // @3
// (f()) // @4

// 在以`[`,`(`,`+`,`-`,`/`开头的语句前,永远不要省略分号
var d = 8;
var e = 3
+d

console.log(e); // 11

// 当连接不同的脚本的时候,要在不同的脚本之间插入分号。
(function() {
    console.log('hello')
})();(function() {
    console.log('world')
})()

// 不然就会解析出错
//(function() {
//    console.log('hello')
//})()(function() {
//    console.log('world')
//})()

// 参数之前含有`return`,`throw`,`break`,`continue`,`++`,`--`的,参数与它们之间不要换行。
function demoFunc() {
    return
    1
}
console.log(demoFunc()) // undefined 没有返回预期的结果

// 在循环语句的头部,分号不是用来当分隔符或者空语句使用的。
for(var i = 0; i < 3; i++) {
    console.log(i);
}

// 解析出错
//for(var i = 0
//        i < 3
//        i++) {
//    console.log(i);
//}
```
[源码](item6/demo.js)

----

### 谨记

+ **仅在`}`标记之前,一行的结束和程序的结束处推导分号。**
+ **仅在紧接着的标记不能被解析的时候推导分号。**
+ **在以`(`,`[`,`+`,`-`或`/`字符开头的语句前决不能省略分号。**
+ **当脚本连接的时候,在脚本之间显式地插入分号。**
+ **在`return`,`throw`,`break`,`continue`,`++`或`--`的参数之前决不能换行。**
+ **分号不能作为`for`循环的头部或空语句的分隔符而被推导出。**