### 理解变量声明提升

```javascript
// 因为变量提升 所以不会有报错
console.log(test); // undefined

// 相当于把 var test提升到顶部 赋值部分 test = 1 还是在原来的位置;
// 如果把下面这句话注释掉的话,上面的语句就会报错。
var test = 1;
```
[源码](item12/demo.js)

------

### 谨记
+ **在代码块中的变量声明会被隐式地提升到封闭函数的顶部**
+ **重声明一个变量会被视为单个变量**
+ **考虑手动提升局部变量的声明,从而避免混淆**