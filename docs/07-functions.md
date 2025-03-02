# 函数

函数是 Vine 程序的基本构建块，允许将代码组织成可重用的单元。本章将详细介绍 Vine 中的函数定义、参数传递、返回值和函数作用域等概念。

## 基本函数定义

在 Vine 中，使用 `fn` 关键字定义函数：

```vine
fn add(a, b) {
  return a + b
}
```

这个简单的函数接受两个参数 `a` 和 `b`，并返回它们的和。

## 函数声明语法

Vine 函数声明的一般语法是：

```vine
fn function_name(parameter1, parameter2, ...) {
  // 函数体
  return result
}
```

函数声明包括以下部分：

- `fn` 关键字：表明这是一个函数定义
- `function_name`：函数的名称（标识符）
- 小括号 `()` 中的参数列表
- 花括号 `{}` 中的函数体
- `return` 语句（可选）：指定函数的返回值

## 参数和参数传递

### 基本参数传递

函数参数允许将值传递给函数：

```vine
fn greet(name) {
  return "Hello, {name}!"
}

let message = greet("Alice")  // 返回 "Hello, Alice!"
```

在调用函数时，参数可以是字面值、变量或复杂表达式：

```vine
let first_name = "Bob"
let greeting = greet(first_name)  // 使用变量
let another_greeting = greet("Char" + "lie")  // 使用表达式
```

### 参数数量

函数调用必须提供与函数定义相匹配的参数数量：

```vine
fn add(a, b) {
  return a + b
}

let sum1 = add(5, 3)  // 正确：两个参数
// let sum2 = add(5)    // 错误：参数不足
// let sum3 = add(5, 3, 1)  // 错误：参数过多
```

### 特殊参数：IO 参数

某些函数，特别是需要执行 IO 操作的函数，需要接收 IO 对象作为参数：

```vine
fn print_message(&io: &IO, message) {
  io.println(message)
}

pub fn main(&io: &IO) {
  print_message(io, "Hello, World!")
}
```

`&io: &IO` 语法表示函数接受一个 IO 类型的引用参数。

## 返回值

### 基本返回值

使用 `return` 关键字从函数中返回值：

```vine
fn square(x) {
  return x * x
}

let result = square(4)  // 结果为 16
```

### 隐式返回

Vine 函数中，函数体的最后一个表达式可以作为隐式返回值（无需 `return` 关键字）：

```vine
fn cube(x) {
  x * x * x  // 隐式返回，等同于 return x * x * x
}

let result = cube(3)  // 结果为 27
```

### 提前返回

`return` 语句可以用于在函数执行过程中提前退出：

```vine
fn abs(x) {
  if x < 0 {
    return -x
  }
  return x
}
```

### 没有返回值的函数

如果函数不需要返回值，可以省略 `return` 语句：

```vine
fn log_message(&io: &IO, message) {
  io.println("LOG: {message}")
  // 没有显式的 return 语句
}
```

不返回值的函数实际上返回单元类型（相当于其他语言中的 `void` 或 `null`）。

## 函数作用域和生命周期

### 局部变量

在函数内部声明的变量只在该函数体内可见：

```vine
fn calculate() {
  let x = 10  // 局部变量
  let y = 20  // 局部变量
  return x + y
}

// 在函数外部，x 和 y 不可访问
```

### 变量遮蔽

函数参数和内部变量可能会遮蔽外部同名变量：

```vine
let x = 100  // 外部变量

fn test(x) {  // 参数 x 遮蔽外部变量 x
  let y = x * 2  // 这里的 x 是参数值
  return y
}

let result = test(5)  // 结果为 10，而不是 200
```

### 闭包和嵌套函数

Vine 可能支持在函数内部定义函数，这些内部函数可以访问外部函数的变量：

```vine
fn counter_generator(start) {
  let count = start

  fn increment() {
    count = count + 1
    return count
  }

  return increment
}

let counter = counter_generator(0)
let value1 = counter()  // 1
let value2 = counter()  // 2
```

注意：Vine 的当前实现可能对闭包和嵌套函数的支持有限。

## 函数特性和高级用法

### 递归函数

函数可以调用自身，这称为递归：

```vine
fn factorial(n) {
  if n <= 1 {
    return 1
  }
  return n * factorial(n - 1)
}

let result = factorial(5)  // 5! = 120
```

递归函数必须有一个基本情况（终止条件），以防止无限递归。

### 相互递归

两个或多个函数可以相互调用：

```vine
fn is_even(n) {
  if n == 0 {
    return true
  }
  return is_odd(n - 1)
}

fn is_odd(n) {
  if n == 0 {
    return false
  }
  return is_even(n - 1)
}
```

### 公开和私有函数

使用 `pub` 关键字标记公开函数，这些函数可以从外部模块或文件访问：

```vine
pub fn public_function() {
  // 可以从其他模块访问
}

fn private_function() {
  // 只能在当前模块内访问
}
```

`main` 函数通常必须标记为 `pub`，因为它是程序的入口点。

## 函数作为值

### 函数引用和回调

在一些函数式编程场景中，函数可以作为值传递给其他函数：

```vine
fn apply_operation(x, y, operation) {
  return operation(x, y)
}

fn add(a, b) {
  return a + b
}

fn multiply(a, b) {
  return a * b
}

let sum = apply_operation(5, 3, add)  // 8
let product = apply_operation(5, 3, multiply)  // 15
```

注意：Vine 的当前实现可能对函数作为值的支持有限。

## 函数设计最佳实践

### 单一责任原则

函数应该只有一个明确的责任或目的：

```vine
// 不好的设计 - 函数做了两件事
fn process_and_print(&io: &IO, data) {
  let result = data * 2
  io.println("Result: {result}")
  return result
}

// 更好的设计 - 分为两个函数
fn process(data) {
  return data * 2
}

fn print_result(&io: &IO, result) {
  io.println("Result: {result}")
}
```

### 适当的函数大小

保持函数简短且专注：

- 通常不超过 20-30 行代码
- 一个函数应该可以在一个屏幕内完全显示
- 如果函数变得太大，考虑将其分解为多个小函数

### 有意义的命名

函数名应该清楚地表明它的目的和行为：

```vine
// 不好的命名
fn f(x) {
  return x * x
}

// 更好的命名
fn square(number) {
  return number * number
}
```

### 参数数量

函数参数数量应该适中：

- 理想情况下，不超过 3-4 个参数
- 如果需要更多参数，考虑使用结构来组织它们

```vine
// 参数过多
fn create_user(name, age, email, address, phone, role) {
  // ...
}

// 更好的方式 - 使用结构
fn create_user(user_data) {
  // user_data 是一个包含所有必要字段的结构
  // {name: "Alice", age: 30, email: "alice@example.com", ...}
}
```

## 常见函数错误和陷阱

### 忘记返回值

如果函数应该返回值但没有显式 `return` 语句，可能会导致意外行为：

```vine
// 错误 - 没有返回值
fn add(a, b) {
  let sum = a + b
  // 忘记 return
}

// 正确
fn add(a, b) {
  let sum = a + b
  return sum
}

// 或者
fn add(a, b) {
  a + b  // 隐式返回
}
```

### 副作用隐藏

函数应该明确其副作用，不要隐藏它们：

```vine
// 误导性函数 - 名称暗示只计算，但实际上还打印
fn calculate_sum(a, b, &io: &IO) {
  let sum = a + b
  io.println("Sum calculated: {sum}")  // 隐藏的副作用
  return sum
}

// 更好的设计 - 名称明确表示函数有副作用
fn calculate_and_print_sum(a, b, &io: &IO) {
  let sum = a + b
  io.println("Sum calculated: {sum}")
  return sum
}
```

### 递归栈溢出

深度递归可能导致栈溢出，特别是对于大输入值：

```vine
// 可能导致栈溢出的递归
fn factorial(n) {
  if n <= 1 {
    return 1
  }
  return n * factorial(n - 1)  // 对大 n 值可能栈溢出
}

// 更好的迭代实现
fn factorial_iterative(n) {
  let result = 1
  let i = 1
  while i <= n {
    result = result * i
    i = i + 1
  }
  return result
}
```

## 总结

函数是 Vine 编程的核心构建块，允许代码模块化和重用。理解函数定义、参数传递、返回值和作用域对于编写清晰、高效的 Vine 程序至关重要。

遵循良好的函数设计原则，如单一责任、适当大小和明确命名，可以显著提高代码的可读性和可维护性。

在下一章中，我们将探讨 Vine 的底层计算模型—[交互网络理论基础](./08-interaction-nets.md)，这是理解 Vine 独特特性的关键。
