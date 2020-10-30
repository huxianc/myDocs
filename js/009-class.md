<!--
 * @Description:
 * @Author: huxianc
 * @Date: 2020-10-26 17:47:10
 * @LastEditors: huxianc
 * @LastEditTime: 2020-10-27 14:01:55
-->

## 静态类方法

可以在类上定义静态方法。这些方法通常用于执行不特定于实例的操作，也不要求存在类的实例

与原型成员类似，静态成员每个类上只能有一个

静态类方法只有类自己本身才能调用

```js
class Person {
  constructor() {
    // 添加到 this 的所有内容都会存在于不同的实例上
    this.locate = () => console.log("instance", this);
  }
  // 定义在类的原型对象上
  locate() {
    console.log("prototype", this);
  }
  // 定义在类本身上
  static locate() {
    console.log("class", this);
  }
}
let p = new Person();
p.locate(); // instance, Person {}
Person.prototype.locate(); // prototype, {constructor: ... }
Person.locate(); // class, class Person {}
```

## 继承

- 使用 extends 可以继承所有拥有[[Construct]]和原型的对象
- 子类如果继承父类，必须在 construct 中第一时间调用 super()，不要在调用 super()之前引用 this，否则会抛出 ReferenceError
- 在静态方法中可以通过 super 调用继承的类上定义的静态方法

```js
class Vehicle {
  static identify() {
    console.log("vehicle");
  }
}
class Bus extends Vehicle {
  static identify() {
    super.identify();
  }
}
Bus.identify(); // vehicle
```

- 如果在派生类中显式定义了构造函数，则要么必须在其中调用 super()，要么必须在其中返回一个对象
