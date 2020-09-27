1. 继承

   - 可以通过`extends`来继承
   - 也可以重写父类的属性和方法
   - 调用父类的方法可以通过`super`

2. public

   - 允许在类的内部和外部被调用

3. private
   - 只允许在类的内部被调用，外部不允许调用
4. protected

   - 允许在类内及继承的子类中使用

5. 子类继承父类的构造函数

```ts
class Person {
  constructor(public name: string) {}
}

class Teacher extends Person {
  constructor(public age: number) {
    super("huxianc"); // 父类的构造函数需要传参
  }
}

const teacher = new Teacher(18);
console.log(teacher.age); // 18
console.log(teacher.name); // huxianc
```

- 子类继承父类并有构造函数的原则，就是在子类里写构造函数时，必须用 super()调用父类的构造函数，如果需要传值，也必须进行传值操作。就是是父类没有构造函数，子类也要使用 super()进行调用，否则就会报错。

```ts
class Person {}

class Teacher extends Person {
  constructor(public age: number) {
    super();
  }
}

const teacher = new Teacher(18);
console.log(teacher.age);
```

6. static

   - 用 static 声明的属性和方法，不需要进行声明对象，就可以直接使用

   ```ts
   class Girl {
     static sayLove() {
       return "I Love you";
     }
   }
   console.log(Girl.sayLove());
   ```

7. abstract 抽象类

   - 抽象类的关键词是 abstract,里边的抽象方法也是 abstract 开头的

   ```ts
   abstract class Girl {
     abstract skill(); //因为没有具体的方法，所以我们这里不写括号
   }
   ```

   ```ts
   abstract class Girl {
     abstract skill(); //因为没有具体的方法，所以我们这里不写括号
   }

   class Waiter extends Girl {
     skill() {
       console.log("大爷，请喝水！");
     }
   }

   class BaseTeacher extends Girl {
     skill() {
       console.log("大爷，来个泰式按摩吧！");
     }
   }

   class seniorTeacher extends Girl {
     skill() {
       console.log("大爷，来个SPA全身按摩吧！");
     }
   }
   ```
