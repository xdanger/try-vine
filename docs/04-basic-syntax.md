# 基本语法

本章将详细介绍 Vine 语言的基本语法元素，包括变量声明、表达式、语句和注释。掌握这些基础知识对于编写任何 Vine 程序都至关重要。

## 代码结构

Vine 程序由以下基本元素组成：

- **导入语句**：导入标准库或其他模块
- **函数定义**：程序的主要构建块
- **变量声明和赋值**：创建和修改变量
- **表达式**：计算值的代码片段
- **语句**：执行操作的指令
- **注释**：代码说明

Vine 代码存储在扩展名为 `.vi` 的文件中。

## 注释

注释用于解释代码，不会被编译器执行。Vine 支持单行注释：

```vine
// 这是一个单行注释

let x = 5  // 这也是一个注释，位于代码之后
```

注释可以位于单独的行上，也可以位于代码行的末尾。

## 变量

### 变量声明

在 Vine 中，使用 `let` 关键字声明变量：

```vine
let name = "Alice"  // 声明一个字符串变量
let age = 30        // 声明一个数字变量
let is_active = true  // 声明一个布尔变量
```

Vine 使用隐式类型推断，这意味着编译器根据赋值自动确定变量类型。

### 变量命名规则

变量名必须遵循以下规则：

- 以字母或下划线开头
- 只能包含字母、数字和下划线
- 区分大小写
- 不能使用保留关键字

例如：

```vine
let user_name = "Bob"    // 有效
let _count = 42          // 有效
let 1st_place = "Gold"   // 无效（不能以数字开头）
let user-name = "Charlie"  // 无效（不能包含连字符）
```

### 变量赋值

声明变量后，可以使用赋值操作符 `=` 更改其值：

```vine
let counter = 0    // 初始值为 0
counter = counter + 1  // 增加到 1
counter = 10       // 设置为 10
```

## 数据类型

Vine 支持以下基本数据类型：

### 数值类型

```vine
let integer = 42       // 整数
let float = 3.14       // 浮点数
let negative = -10     // 负数
```

### 字符串

字符串是文本的序列，用双引号括起来：

```vine
let greeting = "Hello, Vine!"
let empty_string = ""
```

### 布尔值

布尔值表示真或假，只能是 `true` 或 `false`：

```vine
let is_completed = true
let has_errors = false
```

### 复合类型

Vine 也支持一些复合数据类型，如数组：

```vine
// 数组（注意：数组操作在本章中仅做简单介绍）
let numbers = [1, 2, 3, 4, 5]
let names = ["Alice", "Bob", "Charlie"]
```

## 表达式

表达式是计算并产生值的代码片段。

### 算术表达式

```vine
let sum = 5 + 3        // 加法
let difference = 10 - 4  // 减法
let product = 6 * 7    // 乘法
let quotient = 20 / 5  // 除法
let remainder = 10 % 3  // 取余
```

### 比较表达式

```vine
let is_equal = x == y      // 等于
let is_not_equal = x != y  // 不等于
let is_greater = x > y     // 大于
let is_less = x < y        // 小于
let is_greater_or_equal = x >= y  // 大于或等于
let is_less_or_equal = x <= y     // 小于或等于
```

### 逻辑表达式

```vine
let and_result = condition1 && condition2  // 逻辑与
let or_result = condition1 || condition2   // 逻辑或
let not_result = !condition               // 逻辑非
```

### 字符串插值

Vine 支持字符串插值，允许在字符串中嵌入变量值：

```vine
let name = "Vine"
let version = 1.0
let message = "Welcome to {name} version {version}!"
// 结果: "Welcome to Vine version 1.0!"
```

## 语句

语句是执行操作而不一定返回值的代码单元。

### 赋值语句

```vine
x = 10       // 将 10 赋值给变量 x
name = "Bob"  // 将 "Bob" 赋值给变量 name
```

### 条件语句

```vine
if x > 10 {
  io.println("x is greater than 10")
} else if x == 10 {
  io.println("x is exactly 10")
} else {
  io.println("x is less than 10")
}
```

### 循环语句

```vine
// while 循环
let i = 0
while i < 5 {
  io.println("Count: {i}")
  i = i + 1
}
```

注意：Vine 目前不支持 `for` 循环或 `break` 语句，所有循环控制都使用 `while` 实现。

## 空格和格式

Vine 对大多数空格和格式不敏感，但有一些约定：

```vine
// 这两种写法都是有效的
let x=5
let y = 10

// 缩进通常使用两个空格
if condition {
  // 代码块内缩进
  let z = 15
}
```

尽管 Vine 对格式不严格，但建议遵循一致的缩进和空格使用，以提高代码可读性。

## 文件结构示例

下面是一个完整的 Vine 文件结构示例：

```vine
// 导入标准库
use std::IO;

// 辅助函数定义
fn add(a, b) {
  return a + b
}

// 主函数
pub fn main(&io: &IO) {
  // 变量声明
  let x = 5
  let y = 10

  // 调用函数
  let sum = add(x, y)

  // 条件语句
  if sum > 10 {
    io.println("Sum is greater than 10")
  }

  // 字符串插值
  io.println("The sum of {x} and {y} is {sum}")

  // 循环
  let i = 0
  while i < 3 {
    io.println("Iteration {i}")
    i = i + 1
  }
}
```

## 常见陷阱和解决方案

初学者在使用 Vine 语法时可能会遇到一些常见问题：

### 1. 缺少括号

**错误**：

```vine
if x > 5
  io.println("x is greater than 5")
```

**解决方案**：始终在条件语句和循环中使用花括号：

```vine
if x > 5 {
  io.println("x is greater than 5")
}
```

### 2. 添加不必要的分号

**错误**：

```vine
let x = 5;
```

**解决方案**：Vine 不需要分号来结束语句：

```vine
let x = 5
```

### 3. 混淆变量声明和赋值

**错误**：

```vine
// 尝试在已声明的变量前再次使用 let
let x = 5
let x = 10  // 错误
```

**解决方案**：变量只需声明一次，之后直接赋值：

```vine
let x = 5
x = 10  // 正确
```

## 总结

在本章中，我们介绍了 Vine 的基本语法元素，包括：

- 注释和代码结构
- 变量声明和赋值
- 基本数据类型
- 表达式（算术、比较、逻辑）
- 字符串插值
- 条件语句和循环
- 代码格式和常见陷阱

掌握这些基础知识为学习更高级的 Vine 功能奠定了基础。在下一章中，我们将深入探讨 Vine 的[数据类型和运算符](./05-data-types.md)。
