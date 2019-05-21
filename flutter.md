## 基础

### 1.Dart 语言

- 基本类型
  
  `var` 关键字定义变量: `var num = 999`; Dart 属于动态类型语言，支持闭包。

- 变量
  
  Dart 不需要给变量设置`setter getter`方法。基本类型、类都继承于 `Object`,默认值都是 `null`.

- 常量
  
  Dart 中`final 和 const` 表示常量，`static const` 代表静态常量。
  `const` 修饰的常量在编译期确定,所以必须在定义时就初始化，`final` 修饰的常量在运行时确定。

- 特殊操作符
  
  `~/` 取商的整数位 `print(4~/3); // 1`
  `as` 类型转换
  `is` 如果`Demo` 实现了 `T` 接口，那么`Demo() is T` 返回 `true`.
  `is!` 与 `is` 相反。
  `??=` `a ??= b;` 如果 `a` 为空，则将 `b` 赋值给 `a`,否则 `a` 保持不变。
  `expr1 ?? expr2` 如果 `expr1` 非空，返回 `expr1` 的值，否则，返回 `expr2` 的值
  `..` 级联操作符，类似链式变成:

  ```Dart
  querySelector('#confirm') // 获取一个对象
  ..text = 'Confirm' // 使用它的成员
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'));
  ```

  `?.` `foo?.bar` 访问`foo`的`bar`属性，如果 f`oo`为空，则直接返回空，而不会报空指针

- 方法&函数
  参数列表和 js 类似，可以初始化参数类表

```dart
void foo(String name,{int age = 20})
```
