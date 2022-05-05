# 第3章 语言基础

## 3.1 语法

### 3.1.1 区分大小写

### 3.1.2 标识符

最佳实践: 驼峰命名法

### 3.1.3 comment

//

/* */

### 3.1.4 strict mode

### 3.1.5 语句

最佳实践: 始终在控制语句中使用代码块 { }

## 3.2 关键字与保留字

break do in typeof case else instanceof var catch export new void class extends return while const finally super with
continue for switch yield debugger function this default if throw delete import try

始终保留

enum

严格模式下保留

implements package public interface protected static let private

模块代码下保留

await

## 3.3 变量

### 3.3.1 var

1. 存在函数声明作用域
2. 声明提升

### 3.3.2 let

1. 块级作用域
2. 暂时性死区TDZ
3. 全局声明不会成为window对象的属性
4. for循环中的let声明

### 3.3.3 const

1. 浅层readonly
2. 声明时必须初始化

### 3.3.4 声明风格及最佳实践

不使用var, 优先const, 其次let

## 3.4 数据类型

### 3.4.1 typeof

### 3.4.2 Undefined类型

Undefined只有一个值 undefined

变量的默认初始值

变量声明但未初始化(undefined)/未初始化(ReferenceError)

### 3.4.3 Null类型

只有一个值null

定义将来要保存对象的变量时, 建议使用null初始化

undefined由null派生而来

null语意即为空对象指针

### 3.4.4 Boolean类型

true/false

### 3.4.5 Number类型

双精度值
+-Infinite
Math.MAX_VALUE Math.MIN_VALUE
Math.POSITIVE_INFINITE MATH.NEGATIVE_INFINITE
NaN

parseFloat只解析十进制

### 3.4.6 String类型

immutable

number.toString(底数)

模板字符串

tag function

```javascript
// 会原样输出\n 
String.raw`first string\nsecond string`
``` 

### 3.4.7 Symbol类型

创建Symbol

Symbol(description)

全局符号注册表

Symbol.for(description) 在全局符号注册表中搜索description, 如果有返回, 没有则创建后返回

Symbol.keyFor(description) 通过symbol值查询全局注册表,获取其description｜undefined

内置符号

Symbol.iterator

Symbol.asyncIterator

```javascript
for await(const i of arr) { /* ... */ }
```

Symbol.hasInstance 由instanceof调用

```javascript
class Foo {
  static [Symbol.hasInstance](target) {
    return /* target is instanceof Foo? */
  }
}
```

Symbol.isConcatSpreadable 一个布尔值, 表示对象是否应该使用Array.prototype.concat打平其数组元素

当为true时, concat拼接时 arrayLike也会被打平, 如果不能被打平, 则忽略它

```javascript
const a = [1];
const b = { length: 1, 0: 1 }
a.concat(b) // [1,{length:1,0:1}]
b[Symbol.isConcatSpreadable] = true
a.concat(b) // [1,1]
```

