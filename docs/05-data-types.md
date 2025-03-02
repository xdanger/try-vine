# 数据类型与运算符

本章将详细介绍 Vine 语言中的数据类型和各种运算符。了解这些基础元素对于编写有效的 Vine 程序至关重要。

## 基本数据类型

Vine 语言支持多种基本数据类型，用于表示不同种类的值。这些类型构成了 Vine 程序的基础构建块。

### 数值类型

Vine 支持以下数值类型：

#### 整数 (Int)

整数是没有小数部分的数字：

```vine
let age = 30
let count = -5
let population = 7_900_000_000  // 下划线可用于提高大数字的可读性
```

整数类型可以表示正数、负数和零。Vine 的实现通常使用 64 位有符号整数，但具体范围可能取决于底层 IVM 的实现。

#### 浮点数 (Float)

浮点数用于表示带小数部分的数字：

```vine
let pi = 3.14159
let temperature = -42.5
let avogadro = 6.022e23  // 科学记数法
```

浮点数遵循 IEEE 754 标准，通常使用 64 位双精度实现。

### 字符串 (String)

字符串是文本数据的序列，在 Vine 中用双引号（`"`）括起来：

```vine
let name = "Alice"
let message = "Hello, World!"
let empty = ""  // 空字符串
```

字符串可以包含任何 Unicode 字符，Vine 原生支持 UTF-8 编码。

#### 字符串操作

Vine 提供了一些基本的字符串操作：

```vine
// 字符串连接
let first_name = "John"
let last_name = "Doe"
let full_name = first_name + " " + last_name  // "John Doe"

// 字符串插值
let age = 30
let greeting = "Hello, I am {first_name} and I am {age} years old."
```

### 布尔值 (Bool)

布尔类型表示逻辑值，只有两个可能的值：`true` 和 `false`：

```vine
let is_active = true
let has_completed = false
```

布尔值通常用于条件语句和逻辑运算。

### 单元类型 (Unit)

单元类型表示没有任何值，类似于其他语言中的 `void` 或 `null`。它通常用于不返回有意义值的函数：

```vine
// 单元类型通常隐式使用，很少显式声明
fn log_message(message) {
  // 打印消息但不返回值
  // 隐式返回单元类型
}
```

## 复合数据类型

除了基本类型外，Vine 还支持一些复合数据类型，用于组织和存储更复杂的数据结构。

### 数组 (Array)

数组是相同类型值的有序集合：

```vine
let numbers = [1, 2, 3, 4, 5]
let names = ["Alice", "Bob", "Charlie"]
let empty_array = []
```

#### 数组访问和操作

可以使用索引访问数组元素（索引从 0 开始）：

```vine
let names = ["Alice", "Bob", "Charlie"]
let first_name = names[0]  // "Alice"
let second_name = names[1]  // "Bob"

// 修改数组元素
names[1] = "Robert"  // 现在 names 是 ["Alice", "Robert", "Charlie"]
```

数组支持的基本操作：

```vine
// 获取数组长度
let names = ["Alice", "Bob", "Charlie"]
let count = names.length()  // 3

// 添加元素（如果实现支持）
names.push("David")  // ["Alice", "Bob", "Charlie", "David"]

// 移除最后一个元素（如果实现支持）
let last = names.pop()  // 返回 "David"，数组变为 ["Alice", "Bob", "Charlie"]
```

### 映射/字典 (Map)

映射（或称字典）是键值对的集合，允许通过唯一键快速查找值：

```vine
// 创建映射
let person = {
  "name": "Alice",
  "age": 30,
  "is_student": false
}
```

#### 映射访问和操作

可以使用键访问映射中的值：

```vine
let person = {"name": "Alice", "age": 30}

// 访问值
let name = person["name"]  // "Alice"
let age = person["age"]    // 30

// 修改值
person["age"] = 31

// 添加新键值对
person["email"] = "alice@example.com"
```

## 运算符

Vine 提供了多种运算符来执行各种操作。

### 算术运算符

```vine
let a = 10
let b = 3

let sum = a + b        // 加法: 13
let difference = a - b  // 减法: 7
let product = a * b    // 乘法: 30
let quotient = a / b   // 除法: 3.33333...
let remainder = a % b  // 取余: 1
```

### 赋值运算符

```vine
let x = 5       // 基本赋值

// 复合赋值运算符（如果支持）
x += 3          // 等同于 x = x + 3
x -= 2          // 等同于 x = x - 2
x *= 4          // 等同于 x = x * 4
x /= 2          // 等同于 x = x / 2
x %= 3          // 等同于 x = x % 3
```

### 比较运算符

比较运算符返回布尔值（`true` 或 `false`）：

```vine
let a = 10
let b = 5

let equal = a == b            // 等于: false
let not_equal = a != b        // 不等于: true
let greater = a > b           // 大于: true
let less = a < b              // 小于: false
let greater_or_equal = a >= b  // 大于等于: true
let less_or_equal = a <= b    // 小于等于: false
```

### 逻辑运算符

逻辑运算符用于组合布尔表达式：

```vine
let condition1 = true
let condition2 = false

let and_result = condition1 && condition2  // 逻辑与: false
let or_result = condition1 || condition2   // 逻辑或: true
let not_result = !condition1              // 逻辑非: false
```

## 类型转换

Vine 支持某些类型之间的转换。转换可以是隐式的（自动发生）或显式的（通过函数调用）。

### 隐式转换

在某些情况下，Vine 会自动执行类型转换：

```vine
let integer = 42
let float = 3.14
let result = integer + float  // 整数隐式转换为浮点数，结果为 45.14
```

### 显式转换

对于更复杂的转换，可以使用显式转换函数：

```vine
// 字符串转整数
let str_number = "42"
let number = parseInt(str_number)  // 42

// 整数转字符串
let integer = 100
let str_integer = toString(integer)  // "100"

// 浮点数转整数（可能会截断小数部分）
let pi = 3.14
let rounded = toInt(pi)  // 3
```

## 类型检查

Vine 使用隐式类型推断，但在某些情况下，可能需要检查变量的类型：

```vine
// 使用类型检查函数（如果实现支持）
let value = 42
let is_number = isNumber(value)  // true
let is_string = isString(value)  // false
```

## 常见的类型相关陷阱

使用 Vine 的数据类型时，需要注意以下几个常见陷阱：

### 1. 数值精度问题

浮点数计算可能导致精度问题：

```vine
let result = 0.1 + 0.2  // 可能不完全等于 0.3
let comparison = result == 0.3  // 可能为 false

// 解决方案：使用小误差范围比较
let is_close = abs(result - 0.3) < 0.0001  // true
```

### 2. 字符串与数值比较

当比较不同类型的值时，可能会出现意外结果：

```vine
let str_value = "42"
let num_value = 42

// 错误的比较方式
let direct_comparison = str_value == num_value  // false，类型不同

// 正确的比较方式
let parsed_value = parseInt(str_value)
let correct_comparison = parsed_value == num_value  // true
```

### 3. 数组索引越界

访问超出数组范围的索引可能导致错误：

```vine
let names = ["Alice", "Bob"]
let third_name = names[2]  // 错误：索引越界

// 解决方案：先检查索引是否有效
let index = 2
if index < names.length() {
  let name = names[index]
} else {
  // 处理索引越界情况
}
```

## 总结

Vine 的类型系统虽然简单但功能强大，支持常见的基本类型和复合类型。理解这些类型及其操作方式对于编写正确、高效的 Vine 程序至关重要。

在下一章中，我们将探讨 Vine 的[控制流](./06-control-flow.md)，包括条件语句、循环和分支结构。
