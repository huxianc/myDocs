<!--
 * @Description: 
 * @Author: huxianc
 * @Date: 2020-09-29 17:27:40
 * @LastEditors: huxianc
 * @LastEditTime: 2020-09-30 17:50:25
-->
## 变量提升

1. let 声明的范围是块作用域，var 是函数作用域

```js
// var
if (true) {
  var name = "Matt";
  console.log(name); // Matt
}
console.log(name); // Matt

// let
if (true) {
  let age = 26;
  console.log(age); // 26
}
console.log(age); // ReferenceError: age 没有定义

// const
if (true) {
  const age = 26;
  console.log(age); // 26
}
console.log(age); // ReferenceError: age 没有定义

if (true) {
  const name = "Matt";
  console.log(name); // Matt
}
console.log(name); // 空字符串
```