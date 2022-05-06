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

1. 创建Symbol

Symbol(description)

2. 全局符号注册表

Symbol.for(description) 在全局符号注册表中搜索description, 如果有返回, 没有则创建后返回

Symbol.keyFor(description) 通过symbol值查询全局注册表,获取其description｜undefined

3. 内置符号

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

Symbol.isConcatSpreadable

一个布尔值, 表示对象是否应该使用Array.prototype.concat打平其数组元素

当为true时, concat拼接时 arrayLike也会被打平, 如果不能被打平, 则忽略它

```javascript
const a = [1];
const b = { length: 1, 0: 1 }
a.concat(b) // [1,{length:1,0:1}]
b[Symbol.isConcatSpreadable] = true
a.concat(b) // [1,1]
```

Symbol.match

```javascript

class FooMatcher {
  static [Symbol.match](target) {
    return target.includes('foo');
  }
}

// 调用FooMatcher的Symbol.match属性方法
'foobar'.match(FooMatcher) // true

// 所有正则表达式都默认实现了这个接口, 所以match方法可以接收所有正则表达式作为参数
```

Symbol.replace

```javascript
class FooReplacer {
  static [Symbol.replace](target, replacement) {
    return target.split('foo').join(replacement)
  }
}

class StringReplacer {
  constructor(str) {
    this.str = str
  }

  [Symbol.replace](target, replacement) {
    return target.split(this.str).join(replacement)
  }
}

'1foo2'.replace(FooReplacer, 'bar') // 1bar2
'1foo2'.replace(new StringReplacer('foo'), 'bar') // 1bar2
```

Symbol.search/split 类似与match与replace

Symbol.species

一个函数, 返回创建派生对象时的构造函数

```javascript
class Bar extends Array {}

class Baz extends Array {
  static get [Symbol.species]() {
    return Array
  }
}

let bar = new Bar()

bar instanceof Bar // true
bar instanceof Array // true
bar = bar.concat('bar')
bar instanceof Bar // true
bar instanceof Array // true

const baz = new Baz()
baz instanceof Baz // true
baz instanceof Array // true
baz = baz.concat('baz')
// concat创建了一个派生对象, 这个对象的构造函数是Array
baz instanceof Baz // false 
baz instanceof Array // true
```

Symbol.toPrimitive

一个函数, 将对象转换为原始值时调用的方法, 由ToPrimitive抽象操作使用

```javascript
class Bar {
  [Symbol.toPrimitive](hint) {
    switch (hint) {
      case 'number':
        return 3
      case 'string':
        return 'string bar'
      case 'default':
        return 'default bar'
    }
  }
}

const bar = new Bar()
// normal situation => bar's value
3 + bar // 3[object Object] => 3default bar 
3 - bar // NaN => 0 
String(bar) // [object Object] => string bar
```

Symbol.toStringTag

一个字符串, 用于创建对象的默认字符串描述, 由Object.prototype.toString 使用

```javascript
class Bar {
  static [Symbol.toStringTag] = 'Bar'
}

new Bar().toString() // [object Bar]
```

Symbol.unscopables 与with有关

### 3.4.8 Object类型

constructor

hasOwnProperty

isPrototypeOf

propertyIsEnumerable

toLocaleString

toString

valueOf

## 3.5 操作符

### 3.5.1 一元操作符

++/--

+/-

### 3.5.2 位操作符

正数 1位符号+31位

负数 对应正数的二补数(a的二补数为 ～a+1)

～/&/|

<</>> 右移是保留符号的, 也就是左侧空余的位置会由符号位补充而非0

<<</>>> 无符号移动, 左侧空余位由0填充(对正数无影响,而对负数则影响巨大)

### 3.5.3 布尔操作符

!/&&/||

### 3.5.4 乘性操作符

*/\//%

### 3.5.5 指数操作符

**

### 3.5.6 加性操作符

+/-

### 3.5.7 关系操作符

< / > / <= / >=

### 3.5.8 相等操作符

==/===/!=/!==

### 3.5.9 三元运算符

x?y:z

### 3.5.10 赋值运算符

=

### 3.5.11 逗号运算符

,

## 3.6 语句

if(){}

do-while

while

for

for-in

for-of

标签语句

break/continue

with

switch

## 3.7 函数
