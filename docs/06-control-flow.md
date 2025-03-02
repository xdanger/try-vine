# 控制流

控制流语句允许程序根据条件执行不同的代码路径，或者重复执行代码块。本章将详细介绍 Vine 语言中的控制流结构，这些结构是构建复杂程序逻辑的基础。

## 条件语句

条件语句允许程序根据特定条件执行不同的代码块。

### if 语句

`if` 语句是最基本的条件语句，当条件为真时执行代码块：

```vine
let temperature = 25

if temperature > 30 {
  io.println("It's hot outside!")
}
```

在这个例子中，只有当 `temperature` 大于 30 时，才会打印消息。

### if-else 语句

`if-else` 语句允许在条件为真时执行一个代码块，在条件为假时执行另一个代码块：

```vine
let temperature = 25

if temperature > 30 {
  io.println("It's hot outside!")
} else {
  io.println("It's not too hot.")
}
```

在这个例子中，由于 `temperature` 不大于 30，程序会执行 `else` 分支，打印 "It's not too hot."。

### if-else if-else 语句

对于多个条件，可以使用 `if-else if-else` 结构：

```vine
let temperature = 25

if temperature > 30 {
  io.println("It's hot outside!")
} else if temperature > 20 {
  io.println("It's warm outside.")
} else if temperature > 10 {
  io.println("It's cool outside.")
} else {
  io.println("It's cold outside!")
}
```

在这个例子中，程序会检查多个条件，并执行第一个条件为真的代码块。由于 `temperature` 是 25，程序会执行第二个分支，打印 "It's warm outside."。

### 嵌套条件语句

条件语句可以嵌套在其他条件语句内部：

```vine
let temperature = 25
let is_raining = true

if temperature > 20 {
  if is_raining {
    io.println("It's warm but raining.")
  } else {
    io.println("It's warm and sunny.")
  }
} else {
  if is_raining {
    io.println("It's cold and raining.")
  } else {
    io.println("It's cold but sunny.")
  }
}
```

虽然嵌套条件是可能的，但过多的嵌套可能导致代码难以阅读和维护。在这种情况下，考虑使用逻辑运算符组合条件。

### 使用逻辑运算符组合条件

逻辑运算符（`&&`、`||`、`!`）可以用来组合或修改条件：

```vine
let temperature = 25
let is_raining = true

if temperature > 20 && !is_raining {
  io.println("It's warm and sunny - perfect weather!")
} else if temperature > 20 && is_raining {
  io.println("It's warm but bring an umbrella!")
} else if temperature <= 20 && !is_raining {
  io.println("It's cool but at least it's not raining.")
} else {
  io.println("It's cool and raining - stay inside!")
}
```

使用逻辑运算符组合条件通常比嵌套的 `if` 语句更清晰。

## 循环语句

循环语句允许重复执行代码块，直到满足特定条件。

### while 循环

`while` 循环在条件为真时重复执行代码块：

```vine
let count = 1

while count <= 5 {
  io.println("Count: {count}")
  count = count + 1
}
```

这个循环会打印数字 1 到 5，然后退出。输出将是：

```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

### 无限循环和退出条件

可以创建无限循环，然后使用条件语句控制何时退出：

```vine
let count = 1
let should_continue = true

while should_continue {
  io.println("Count: {count}")
  count = count + 1

  if count > 5 {
    should_continue = false
  }
}
```

这个循环的效果与前一个示例相同，但使用了不同的结构来控制循环终止。

### 循环中的复杂条件

循环条件可以包含多个因素：

```vine
let i = 0
let sum = 0

while i < 100 && sum < 1000 {
  i = i + 1
  sum = sum + i
  io.println("i: {i}, sum: {sum}")
}

io.println("Final: i = {i}, sum = {sum}")
```

这个循环会一直执行，直到 `i` 达到 100 或者 `sum` 达到或超过 1000，以先满足的条件为准。

### 构建各种循环模式

虽然 Vine 目前主要支持 `while` 循环，但它足够灵活，可以实现其他常见的循环模式：

#### 计数循环（类似 for 循环）

```vine
// 从 0 计数到 9
let i = 0
while i < 10 {
  io.println("Number: {i}")
  i = i + 1
}
```

#### 遍历数组（类似 foreach 循环）

```vine
let fruits = ["Apple", "Banana", "Cherry", "Date"]
let index = 0

while index < fruits.length() {
  let fruit = fruits[index]
  io.println("Fruit {index + 1}: {fruit}")
  index = index + 1
}
```

#### do-while 风格循环（至少执行一次）

```vine
let number = 1

// 在循环前执行一次代码块
io.println("Number: {number}")
number = number + 1

// 然后进入条件循环
while number <= 5 {
  io.println("Number: {number}")
  number = number + 1
}
```

## 跳过和跳出循环

Vine 的当前实现可能不直接支持 `break` 和 `continue` 关键字，但可以使用条件变量模拟这些功能。

### 模拟 break 语句

使用布尔标志模拟 `break`：

```vine
let i = 0
let should_continue = true

while i < 100 && should_continue {
  i = i + 1

  if i == 10 {
    // 相当于 break
    should_continue = false
  } else {
    io.println("Number: {i}")
  }
}

io.println("Broke out of loop at i = {i}")
```

这个循环将在 `i` 达到 10 时提前退出。

### 模拟 continue 语句

使用条件结构模拟 `continue`：

```vine
let i = 0

while i < 10 {
  i = i + 1

  // 如果 i 是偶数，跳过当前迭代（模拟 continue）
  if i % 2 == 0 {
    // 相当于 continue - 跳过后面的代码
  } else {
    io.println("Odd number: {i}")
  }
}
```

这个循环只会打印奇数。

## 多重分支结构

虽然 Vine 可能不直接支持 `switch` 或 `match` 语句，但可以使用 `if-else if-else` 链实现类似功能：

```vine
let day_of_week = 3

let day_name = ""
if day_of_week == 1 {
  day_name = "Monday"
} else if day_of_week == 2 {
  day_name = "Tuesday"
} else if day_of_week == 3 {
  day_name = "Wednesday"
} else if day_of_week == 4 {
  day_name = "Thursday"
} else if day_of_week == 5 {
  day_name = "Friday"
} else if day_of_week == 6 {
  day_name = "Saturday"
} else if day_of_week == 7 {
  day_name = "Sunday"
} else {
  day_name = "Invalid day"
}

io.println("Day {day_of_week} is {day_name}")
```

## 控制流最佳实践

### 避免深度嵌套

过多的嵌套会降低代码的可读性。考虑提前返回、组合条件或提取辅助函数：

```vine
// 避免深度嵌套
fn process_data(value) {
  // 提前返回处理无效情况
  if value < 0 {
    return "Invalid negative value"
  }

  if value == 0 {
    return "Zero value"
  }

  // 处理有效情况
  return "Positive value: {value}"
}
```

### 使用明确的条件表达式

确保条件表达式清晰易懂：

```vine
// 避免:
if !(x != 10) {
  // ...
}

// 更好:
if x == 10 {
  // ...
}
```

### 选择合适的循环结构

根据需求选择最简单的循环结构：

```vine
// 已知次数的迭代使用计数循环
let i = 0
while i < 10 {
  // ...
  i = i + 1
}

// 条件迭代使用 while 和条件
let input = getValue()
while isValid(input) {
  process(input)
  input = getNextValue()
}
```

## 常见控制流陷阱和错误

### 无限循环

最常见的循环错误是忘记更新循环条件，导致无限循环：

```vine
// 错误 - 无限循环
let i = 0
while i < 10 {
  io.println("i is {i}")
  // 忘记增加 i
}

// 正确
let i = 0
while i < 10 {
  io.println("i is {i}")
  i = i + 1
}
```

### 边界条件错误

在循环和条件中经常出现的错误是边界条件错误：

```vine
// 错误 - 可能导致数组索引越界
let array = [1, 2, 3, 4, 5]
let i = 0
while i <= array.length() {  // 错误的条件，应该是 <
  io.println(array[i])
  i = i + 1
}

// 正确
let i = 0
while i < array.length() {  // 正确的条件
  io.println(array[i])
  i = i + 1
}
```

### 条件永远为真或永远为假

在编写条件语句时，确保条件表达式在某个时刻可以变为真或假：

```vine
// 错误 - 条件永远为真
let x = 10
if x >= 0 || x <= 100 {  // 这个条件对任何 x 值都为真
  // ...
}

// 正确
if x >= 0 && x <= 100 {  // 检查 x 是否在 0 到 100 之间
  // ...
}
```

## 总结

控制流结构是构建程序逻辑的基本构建块。Vine 提供了基本的条件语句和循环结构，它们可以组合使用以实现各种控制流模式。

虽然 Vine 的控制流语句相对简单，但通过创造性地组合它们，可以实现从简单到复杂的任何程序逻辑。掌握这些结构对于编写高效、易读和正确的 Vine 程序至关重要。

在下一章中，我们将探讨 Vine 中的[函数](./07-functions.md)，学习如何定义、调用函数以及处理参数和返回值。
