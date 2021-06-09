### 使用立即调用的函数表达式创建局部作用域

```javascript
// 新的函数才会产生新的作用域,JavaScript的循环没有新的作用域产生。

// 测试使用的数组
var testArr = [1, 2, 3];

// @1 不使用闭包的情况下我们使用的是的引用
function generateFunc(arr) {
    var result = [];
    var n = arr.length;
    for(var i = 0; i < n; i++) {
        result[i] = function() {
            return arr[i];
        }
    }
    return result;
}
// @1 产生新的函数
var g1 = generateFunc(testArr);
// 此时的i已经变成了3
console.log(g1[0]()); // undefined
console.log(g1[1]()); // undefined
console.log(g1[2]()); // undefined

// @2 使用闭包方式一
function generateFunc1(arr) {
    var result = [];
    var n = arr.length;
    for(var i = 0; i < n; i++) {
        (function(j) {
            result[j] = function() {
                return arr[j];
            }
        })(i)
    }
    return result;
}
// @2 产生新的函数
var g2 = generateFunc1(testArr);
console.log(g2[0]()); // 1
console.log(g2[1]()); // 2
console.log(g2[2]()); // 3

// @3 使用闭包方式二
function generateFunc2(arr) {
    var result = [];
    var n = arr.length;
    for(var i = 0; i < n; i++) {
        (function() {
            var j = i; // 注意这里
            result[i] = function() {
                return arr[j];
            }
        })()
    }
    return result;
}
// @3 产生新的函数
//var g3 = generateFunc1(testArr);
var g3 = generateFunc2(testArr);
console.log(g3[0]()); // 1
console.log(g3[1]()); // 2
console.log(g3[2]()); // 3
```
[源码](item13/demo.js)

------

### 谨记
+ **理解绑定与赋值的区别。**
+ **闭包通过引用而不是值捕获它们的外部变量。**
+ **使用立即调用的函数表达式(IIFE)来创建局部作用域。**
+ **当心在立即调用的函数表达式中包裹代码块可能改变其行为的情形。**
