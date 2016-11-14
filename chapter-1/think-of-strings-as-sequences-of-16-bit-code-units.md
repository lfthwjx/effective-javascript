### 把字符串当做16位编码单元的序列

```javascript
console.log("𝄞 clef".length); // 7
console.log("G clef".length); // 6

console.log("𝄞 clef".charCodeAt(0)); // 55348 (0xd834)
console.log("𝄞 clef".charCodeAt(1)); // 56606 (0xdd1e)

console.log("𝄞 clef".charAt(0));
console.log("𝄞 clef".charAt(1));

console.log("𝄞 clef".charAt(2) === " "); // true
console.log("𝄞 clef".charAt(1) === " "); // false

console.log(/^.$/.test("𝄞")); // false
console.log(/^..$/.test("𝄞")); // true ..表示两个16位编码的字符
```
[源码](item7/demo.js)

------

### 谨记
+ **JavaScript字符串由16位的代码单元组成,而不是由`Unicode`代码点组成。**
+ **JavaScript使用两个代码单元表示2^16及其以上的`Unicode`代码点。这两个代码单元被称为代理对。**
+ **代理对甩开了字符串元素计数,`length`,`charAt`,`charCodeAt`方法以及正则表达式模式(例如`.`)受到了影响。**
+ **使用第三方的库编写可识别代码点的字符串操作。**
+ **每当你使用一个含有字符串操作的库时,你都要查阅该库文档,看它如何处理代码点的整个范围。**