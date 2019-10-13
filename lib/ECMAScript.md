### JS数据类型
- 基本类型: string、number、boolean、null、undefined、symbol
- 引用类型: Object


### 手写`Array.prototype.map`方法

```js
Array.prototype.map = function(fn) {
    let arr = []
    for(let i = 0; i <= this.length - 1; i++) {
        let result = fn(this[i], i, this)
        arr.push(result)
    }
    return arr
}
```

### 手写`Array.prototype.reduce`方法

```js
Array.prototype.reduce = function(fn, initial) {
    let result = initial
    for(let i = 0; i <= this.length - 1; i++) {
        result = fn(result, this[i], i, this)
    }
    return result
}
```


### 手写`instanceof`

```js
function _instanceof(left, right) {
    const prototype = right.prototype
    left = Object.getPrototypeOf(left)
    while(left !== null) {
        if(left === prototype) {
            return true
        }
        left = Object.getPrototypeOf(left)
    }
    return false
}
```

### 实现函数的call、apply、bind方法


### Promise原理，手写Promise


### 实现Generator

### JS事件


### 原生ajax


### Event Loop


### JS作用域链


### JS深拷贝


