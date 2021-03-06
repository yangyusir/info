# 					一些简单的ES6特性

##### let

​		let跟var最大的不同是在定义变量的时候，给变量指定的作用域不同，let指定块状作用域，var指定函数作用域。

​		babel转换一般是将函数内的变量名字修改，避免和外部变量冲突，达到块状作用域的目的

```js
//es6
for(let i = 0 ; i<10;i++) {
	console.log(i)
}
console.log(i)

// 经babel转换过的
"use strict";
for (var _i = 0; _i < 10; _i++) {
  console.log(_i);
}
console.log(i);
```

也可以使用立即执行函数，直接锁死作用域。

```js
(function(){
    for(let i = 0 ; i<10;i++) {
        console.log(i)
    }
    console.log(i)
})()
```

##### const

​	const是es6中定义常量的修饰符，用于表示新建的变量不可更改，这里的**不可更改**实际上指的是**内存地址不变**，而不是指变量的值不变。因此在定义Object以及Array为常量的时候，需要特别注意。如果确定是表示引用类型不允许被修改，可以额外使用`freeze()`方法.

​	随便聊几句freeze方法，被冻结对象自身的所有属性都不可能以任何方式被修改。这种修改包括数组的各种操作，也包括使用访问器属性修改。如果一个属性的值是个对象，则这个对象中的属性是可以修改的，除非它也是个冻结对象

```js
var obj = {
  name:'jerry',
  gift:['dance','drinking']
}
Object.freeze(obj)

obj.name = 'tom'  //typeError,非严格模式不会报错，但不会成功
obj.gift.push('catch') // 成功

```



```  js
const name = "Tom"
name = "j1eey"  //报错

const person = {name:'Tom'}
person.name = "jerry"  // {name:'Jerry'}
person = {}      // 报错

const items = ['apple']
items.push('orange')  // ['apple','orange']
items = ['orange']    // 报错
```

