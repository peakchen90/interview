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


### 实现原生AJAX

```js
function ajax(method, url, data, onSuccess, onError) {
    onSuccess = onSuccess || () => {}
    onError = onError || () => {}

    let xhr = new XMLHttpRequest()
    xhr.open(method, url, true)
    xhr.send(data)
    xhr.onreadystatechange = function() {
        if(xhr.readyState === 4) {
            if(xhr.status === 200) {
                onSuccess(xhr.responseText)
            } else {
                onError(xhr)
            }
        }
    }
    xhr.ontimeout = onError
    xhr.onerror = onError
}
```


### Event Loop


### JS作用域链


### JS深拷贝
```js
function deepClone(target) {
    function clone(obj, parent = [], newParent = []) {
        let index = parent.findIndex(p => p === obj)
        if(index !== -1) {
            return newParent[index]
        }

        let newObj

        if(Object.prototype.toString.call(obj) === '[object Object]') {
            newObj = {}
        } else if(Array.isArray(obj)) {
            newObj = []
        } else {
            return obj
        }

        parent = [...parent, obj]
        newParent = [...newParent, newObj]
        Object.keys(obj).forEach(key => {
            newObj[key] = clone(obj[key], parent, newParent)
        })

        return newObj
    }

    if(
        Object.prototype.toString.call(target) === '[object Object]'
        || Array.isArray(target)
    ) {
        return clone(target)
    }

    return target
}
```

实现思路：递归拷贝一个数组或对象，递归调用时，将所有父级的引用传到下一级，以判断是否循环引用，如果是循环引用，则将引用的对象替换成新的拷贝对象。

### 实现防抖函数(debounce)


### 实现节流函数(throttle)


