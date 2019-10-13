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

```js
Function.prototype.call = function(ctx) {
    if(ctx == null) ctx = window
    else if(typeof ctx === 'string') ctx = new String(ctx)
    else if(typeof ctx === 'number') ctx = new Number(ctx)
    else if(typeof ctx === 'boolean') ctx = new Boolean(ctx)
    ctx.__fn__ = this

    let args = [...arguments].slice(1)
    let result = ctx.__fn__(...args)
    delete ctx.__fn__
    return result
}
```

```js
Function.prototype.apply = function(ctx) {
    if(ctx == null) ctx = window
    else if(typeof ctx === 'string') ctx = new String(ctx)
    else if(typeof ctx === 'number') ctx = new Number(ctx)
    else if(typeof ctx === 'boolean') ctx = new Boolean(ctx)
    ctx.__fn__ = this

    let args = arguments[1]
    let result
    if(args) {
        result = ctx.__fn__(...args)
    } else {
        result = ctx.__fn__()
    }
    delete ctx.__fn__
    return result
}
```

```js
Function.prototype.bind = function(ctx) {
    if(ctx == null) ctx = window
    else if(typeof ctx === 'string') ctx = new String(ctx)
    else if(typeof ctx === 'number') ctx = new Number(ctx)
    else if(typeof ctx === 'boolean') ctx = new Boolean(ctx)
    ctx.__fn__ = this
    
    let args = [...arguments].slice(1)
    let result = function() {
        let _args = [...arguments, ...args]
        ctx.__fn__(..._args)
    }
    return result
}
```

### Promise原理，手写Promise


### 实现Generator

### JS事件


### 原生ajax


### Event Loop


### JS作用域链


### JS深拷贝


