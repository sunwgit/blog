## 基础

### Dart 语言

#### 内置类型(built-in types)

- **Numbers-数值类型** `int double`
- **Strings**

  - 可以用`$str`的方式在字符串中插入字符串变量值；
  - 可以用`+`连接字符串
  - 可以使用成对的`'''`创建多行字符串，类似于 es6 中的模板字符串
  - **布尔值** 值为`true/false`而且只能用这两个值表示。不能像 js 那样用 0 或 null 等表示 false
  - **List** 可以看做 js 中的数组
  - **Maps** `key-value`对象，`key`唯一。

#### 变量

`var` 关键字定义变量: `var num = 999`;

Dart 属于动态类型语言，支持闭包。

Dart 不需要给变量设置`setter getter`方法。基本类型、类都继承于 `Object`, **默认值都是 `null`**.

#### 常量

Dart 中`final 和 const` 修饰常量，`static const` 代表静态常量。
`const` 修饰的常量在编译期确定,所以必须在定义时就初始化，`final` 修饰的常量在运行时确定。

#### 一些特殊操作符

- **`~/`** 取商的整数位 `print(4~/3); // 1`

- **`as`** 类型转换

- **`is`** 如果`Demo` 实现了 `T` 接口，那么`Demo() is T` 返回 `true`.

- **`is!`** 与 `is` 相反。

- **`??=`** 赋值操作符，`a ??= b;` 如果 `a` 为空，则将 `b` 赋值给 `a`,否则 `a` 保持不变。

- **`expr1 ?? expr2`** 如果 `expr1` 非空，返回 `expr1` 的值，否则，返回 `expr2` 的值

- **`..`** 级联操作符，类似 jquery 链式编程

- **`?.`** `foo?.bar` 访问`foo`的`bar`属性，如果 f`oo`为空，则直接返回空，而不会报空指针

#### 方法&函数

Dart 支持箭头函数，但是与 js 不同的是，如果参数只有一个也必须写上括号，不能省略括号`(param)=>expr;`

##### 参数

- 参数有两种类型：**必需，可选**

  表现在定义上：

  ```dart
  void foo(String name,int age){}//必需
  void foo1({@reqired String name}){}//必需,需要引入flutter/material库
  void foo2({name}){}//可选
  void foo3([name = 'xxxx']){}//可选,初始化
  ```

  表现在调用上： 如果用了对象方式定义参数列表，则调用时需要指明参数名称，这种参数叫做**命名参数**

  ```dart
  foo('xxx',23);
  foo1(name: 'sdfa');
  foo2();
  foo2(name: 'xxx);
  foo3();//name->xxx
  foo3('yyy');//name->yyy
  ```

- 默认参数

  Dart 可以像 js 那样指定默认参数值

  ```dart
  void foo(String name,{int age = 20}){
    print('name:$name,age:$age');
  }
  foo('xxx'); // name:xxx,age:20
  ```

#### Class - 类

需要明白的一些术语：

- `接口`: 在 Dart 中，接口相当于抽象类：`abstract class`
- `接口实现`：普通类继承抽象类
- `Mixin`: 类似于多重继承，需要用到`with`关键字，解决 Dart 语言的单继承问题，实现原理有点类似 js 的原型链，具体可看[这篇文章](https://juejin.im/post/5bb204d3e51d450e4f38e2f6)

Dart 是一个面向对象编程语言，同时支持基于 mixin 的继承机制。

基于 `Mixin` 的继承 意味着每个类（`Object` 除外） 都只有一个超类，一个类的代码可以在其他多个类继承中重复使用。

##### 实例化

在函数实例化时会自动生成实例变量的 _getter_ 方法，如果实例变量没有被 `final` 修饰，那么也会自动生成对应的 _setter_ 方法，_g/setter_ 方法都是隐式的。

##### Constructor - 构造函数

- 每个类都有默认的构造函数，如果不手动定义，则隐式存在一个默认的。
- 构造函数不可继承。
- 可以用命名构造函数定义多个构造函数

  ```dart
  class Demo{
    String x;
    Demo(this.x);
    Demo.fromJson(Map json){
      x = json['x'];
    }
  }
  ```

- 构造函数执行顺序

  1. 子类初始化参数列表
  2. 超类的默认构造函数
  3. 子类构造器

  子类自动调用的只能是超类的默认无参构造器，如果超类没有无参构造器，子类如果需要调用超类构造器，则需要手动调用：

  ```dart
  class Demo extends Foo{
    String x;
    // super调用超类构造器最好写在初始化列表后边
    Demo(this.x):this.x='xxx',super.fromJson(getFooData()){
    //...
    };
  }
  ```
