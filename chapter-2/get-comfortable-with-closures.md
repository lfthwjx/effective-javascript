### 熟练掌握闭包

```javascript
// 我们利用闭包构建一个简单的容器
function Container() {
    var store = [];
    return {
        getItem: function(index) {
            return store[index];
        },
        addItem: function(obj) {
            var index = store.push(obj);
            return index - 1;

        },
        length: function() {
            return store.length;
        }
    }
}

var c = Container();
console.log(c.length()); // 0
var index1 = c.addItem({name: 'dreamapple'});
console.log(index1); // 0
console.log(c.length()); // 1
console.log(c.getItem(index1)); // Object {name: "dreamapple"}
```
[源码](item11/demo.js)

---

### 谨记
+ **函数可以引用定义在其外部作用域的变量**
+ **闭包比创建它们的函数有更长的生命周期**
+ **闭包在内部存储其外部变量的引用,并能读写这些变量**