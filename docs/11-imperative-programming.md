# 命令式编程特性

命令式编程是一种描述计算机如何完成任务的编程范式，它使用语句来改变程序的状态。Vine 语言既支持函数式编程范式，也支持命令式编程范式，使开发者能够根据需要选择最合适的方法。本章将详细介绍 Vine 中的命令式编程特性及其应用。

## 命令式编程的基本概念

### 1. 语句和语句序列

命令式编程使用一系列语句来表达计算过程，每个语句执行一个动作：

```vine
// 命令式语句序列
let x = 5
let y = 10
let z = x + y
io.println("Sum: {z}")
```

在这个例子中，程序按顺序执行四个语句，每个语句修改或使用程序状态。

### 2. 变量和赋值

命令式编程的核心是变量及其值的变化：

```vine
// 变量声明和赋值
let counter = 0  // 初始化变量
counter = counter + 1  // 修改变量值
counter = counter * 2  // 进一步修改
```

### 3. 程序状态

命令式程序维护一个状态，由所有变量及其当前值组成：

```vine
// 程序状态随着执行而变化
let balance = 1000  // 初始状态
let withdrawal = 200

// 状态变化
balance = balance - withdrawal  // 新状态: balance 等于 800
```

### 4. 控制流

命令式编程使用控制流语句来决定执行哪些语句及其顺序：

```vine
// 条件控制流
let num = 15

if num > 10 {
  io.println("Number is greater than 10")
}

// 循环控制流
let i = 0
while i < 5 {
  io.println("Iteration {i}")
  i = i + 1
}
```

## Vine 中的命令式编程特性

### 1. 变量和赋值

Vine 允许声明变量并在程序执行过程中改变它们的值：

```vine
// 变量声明和赋值
let age = 25
io.println("Initial age: {age}")

// 变量重新赋值
age = 26
io.println("New age: {age}")

// 复合赋值 (如果 Vine 支持)
age = age + 1  // 或者简写为 age += 1 (如果支持)
io.println("Incremented age: {age}")
```

### 2. 块作用域

Vine 使用花括号 `{}` 定义代码块，并支持块级作用域：

```vine
// 块级作用域示例
let x = 10

{
  let y = 20  // y 只在这个块中可见
  io.println("Inside block: x = {x}, y = {y}")
}

// 这里可以访问 x，但不能访问 y
io.println("Outside block: x = {x}")
// io.println("y = {y}")  // 这会导致错误，因为 y 超出了作用域
```

### 3. 顺序执行

命令式程序默认按照语句的顺序执行：

```vine
// 顺序执行示例
let total = 0
io.println("Starting calculation...")
total = total + 10
io.println("Added 10: {total}")
total = total + 20
io.println("Added 20: {total}")
total = total + 30
io.println("Added 30: {total}")
io.println("Final total: {total}")
```

### 4. 条件语句

Vine 支持 `if`、`else if` 和 `else` 条件语句：

```vine
// 条件语句示例
let score = 85

if score >= 90 {
  io.println("Grade: A")
} else if score >= 80 {
  io.println("Grade: B")
} else if score >= 70 {
  io.println("Grade: C")
} else if score >= 60 {
  io.println("Grade: D")
} else {
  io.println("Grade: F")
}
```

### 5. 循环语句

Vine 提供了 `while` 循环来重复执行代码块：

```vine
// while 循环示例
let count = 0
while count < 5 {
  io.println("Count: {count}")
  count = count + 1
}

// 使用 while 循环实现数组遍历
let numbers = [10, 20, 30, 40, 50]
let i = 0
while i < numbers.length() {
  io.println("Element {i}: {numbers[i]}")
  i = i + 1
}
```

### 6. 提前返回

在函数中，命令式风格通常使用提前返回来处理特殊情况：

```vine
// 使用提前返回的函数
fn find_index(array, target) {
  let i = 0
  while i < array.length() {
    if array[i] == target {
      return i  // 找到目标时立即返回
    }
    i = i + 1
  }
  return -1  // 未找到时返回 -1
}

let numbers = [10, 20, 30, 40, 50]
let index = find_index(numbers, 30)
io.println("Found at index: {index}")
```

### 7. 原地修改数据结构

命令式编程通常直接修改数据结构，而不是创建新副本：

```vine
// 原地修改数组
let numbers = [1, 2, 3, 4, 5]
io.println("Original array: {numbers}")

// 修改数组元素
numbers[2] = 30
io.println("After modifying element: {numbers}")

// 添加元素
numbers.push(6)
io.println("After adding element: {numbers}")

// 删除元素 (如果 Vine 支持)
// numbers.pop()
// io.println("After removing element: {numbers}")
```

## 命令式编程的典型应用

### 1. 状态管理

命令式编程适合管理具有复杂状态变化的应用：

```vine
// 简单的银行账户状态管理
let account = {
  "number": "12345",
  "owner": "John Doe",
  "balance": 1000,
  "transactions": []
}

fn deposit(account, amount) {
  account.balance = account.balance + amount
  account.transactions.push({
    "type": "deposit",
    "amount": amount,
    "time": "current_time"  // 假设有一个获取当前时间的函数
  })
  return account.balance
}

fn withdraw(account, amount) {
  if amount <= account.balance {
    account.balance = account.balance - amount
    account.transactions.push({
      "type": "withdrawal",
      "amount": amount,
      "time": "current_time"
    })
    return account.balance
  }
  return -1  // 表示余额不足
}

// 使用账户
let new_balance = deposit(account, 500)
io.println("New balance after deposit: {new_balance}")

new_balance = withdraw(account, 200)
io.println("New balance after withdrawal: {new_balance}")

io.println("Transaction history:")
let i = 0
while i < account.transactions.length() {
  let tx = account.transactions[i]
  io.println("{tx.type}: {tx.amount}")
  i = i + 1
}
```

### 2. 交互式程序

命令式编程适合处理用户输入和响应等交互：

```vine
// 简单的交互式计算器
pub fn calculator(&io: &IO) {
  let running = true

  while running {
    io.println("Enter operation (add, subtract, multiply, divide) or 'exit' to quit:")
    let operation = io.read_line()

    if operation == "exit" {
      running = false
      continue
    }

    io.println("Enter first number:")
    let num1 = parseInt(io.read_line())

    io.println("Enter second number:")
    let num2 = parseInt(io.read_line())

    let result = 0

    if operation == "add" {
      result = num1 + num2
    } else if operation == "subtract" {
      result = num1 - num2
    } else if operation == "multiply" {
      result = num1 * num2
    } else if operation == "divide" {
      if num2 == 0 {
        io.println("Error: Cannot divide by zero")
        continue
      }
      result = num1 / num2
    } else {
      io.println("Unknown operation")
      continue
    }

    io.println("Result: {result}")
  }

  io.println("Calculator exiting...")
}
```

### 3. 算法实现

许多经典算法自然地适合命令式编程风格：

```vine
// 命令式冒泡排序实现
fn bubble_sort(array) {
  let n = array.length()
  let i = 0

  while i < n {
    let j = 0
    while j < n - i - 1 {
      if array[j] > array[j + 1] {
        // 交换元素
        let temp = array[j]
        array[j] = array[j + 1]
        array[j + 1] = temp
      }
      j = j + 1
    }
    i = i + 1
  }

  return array
}

let numbers = [64, 34, 25, 12, 22, 11, 90]
bubble_sort(numbers)
io.println("Sorted array: {numbers}")
```

## 命令式编程与函数式编程的对比

### 命令式编程的优势

1. **直观性**：命令式编程通常更符合人类思考问题的方式，特别是对初学者
2. **效率**：原地修改数据结构通常比创建新副本更高效（在内存使用方面）
3. **状态管理**：自然地处理有状态的程序和交互式应用
4. **学习曲线**：对大多数程序员来说更容易掌握，因为它是传统编程模型

### 函数式编程的优势

1. **可预测性**：纯函数更容易推理和测试
2. **并行性**：没有共享状态，更容易并行执行
3. **代码组织**：函数组合促进了更模块化的设计
4. **错误减少**：不可变数据减少了由于意外修改状态导致的错误

### 在 Vine 中结合两种范式

Vine 的优势在于它允许开发者结合命令式和函数式编程的优点：

```vine
// 结合两种范式的例子
// 使用函数式方法处理数据转换
fn transform_data(data) {
  // 创建数据的不可变副本
  let processed = []
  let i = 0
  while i < data.length() {
    processed.push(data[i] * data[i])  // 平方每个元素
    i = i + 1
  }
  return processed
}

// 使用命令式方法处理交互和 I/O
pub fn process_and_display(&io: &IO, data) {
  // 状态变量
  let running = true
  let current_data = data

  while running {
    io.println("Current data: {current_data}")
    io.println("Options: 1) Transform data 2) Add item 3) Exit")
    let choice = io.read_line()

    if choice == "1" {
      // 函数式转换 - 不修改原始数据
      current_data = transform_data(current_data)
    } else if choice == "2" {
      io.println("Enter value to add:")
      let value = parseInt(io.read_line())
      // 命令式修改 - 直接改变状态
      current_data.push(value)
    } else if choice == "3" {
      running = false
    } else {
      io.println("Invalid option")
    }
  }

  io.println("Final data: {current_data}")
}
```

## 命令式编程的最佳实践

### 1. 保持状态简单且局部化

尽量将状态限制在最小的必要范围内：

```vine
// 不好的做法：使用全局状态
let global_counter = 0

fn increment_counter() {
  global_counter = global_counter + 1
}

// 更好的做法：局部状态
fn create_counter(start) {
  let counter = start

  return {
    "increment": fn() {
      counter = counter + 1
      return counter
    },
    "get": fn() {
      return counter
    }
  }
}

// 使用局部化的状态
let my_counter = create_counter(0)
my_counter.increment()  // 1
my_counter.increment()  // 2
io.println("Counter value: {my_counter.get()}")
```

### 2. 明确的状态变化

使变量修改明确且有意图：

```vine
// 不好的做法：隐藏的状态变化
fn process_data(data) {
  // 修改传入的数据而不明确表示
  data[0] = data[0] * 2
  return data
}

// 更好的做法：明确的状态变化
fn process_data_clear(data, should_modify) {
  if should_modify {
    // 明确表示我们要修改数据
    data[0] = data[0] * 2
    return data
  } else {
    // 创建新副本而不是修改原始数据
    let new_data = []
    let i = 0
    while i < data.length() {
      if i == 0 {
        new_data.push(data[i] * 2)
      } else {
        new_data.push(data[i])
      }
      i = i + 1
    }
    return new_data
  }
}
```

### 3. 有意义的变量名

变量是命令式编程的核心，应该使用描述性名称：

```vine
// 不好的做法：不清晰的变量名
let x = 1000
let y = 0.05
let z = x * y
let a = x + z

// 更好的做法：有意义的变量名
let principal = 1000
let interest_rate = 0.05
let interest = principal * interest_rate
let total_amount = principal + interest
```

### 4. 分解复杂操作

将复杂的命令式代码分解为更小、更可管理的函数：

```vine
// 不好的做法：一个巨大的函数
fn process_order(&io: &IO, order) {
  // 验证订单
  if !order.has_key("items") || order.items.length() == 0 {
    io.println("Error: Empty order")
    return false
  }

  // 计算总价
  let total = 0
  let i = 0
  while i < order.items.length() {
    let item = order.items[i]
    total = total + item.price * item.quantity
    i = i + 1
  }

  // 应用折扣
  if total > 100 {
    total = total * 0.9  // 10% 折扣
  }

  // 添加税费
  let tax = total * 0.08
  total = total + tax

  // 更新订单
  order.total = total
  order.tax = tax

  io.println("Order processed. Total: {total}")
  return true
}

// 更好的做法：分解成更小的函数
fn validate_order(order) {
  return order.has_key("items") && order.items.length() > 0
}

fn calculate_subtotal(items) {
  let total = 0
  let i = 0
  while i < items.length() {
    total = total + items[i].price * items[i].quantity
    i = i + 1
  }
  return total
}

fn apply_discount(subtotal) {
  if subtotal > 100 {
    return subtotal * 0.9
  }
  return subtotal
}

fn calculate_tax(amount) {
  return amount * 0.08
}

fn process_order_better(&io: &IO, order) {
  if !validate_order(order) {
    io.println("Error: Invalid order")
    return false
  }

  let subtotal = calculate_subtotal(order.items)
  let discounted = apply_discount(subtotal)
  let tax = calculate_tax(discounted)
  let total = discounted + tax

  // 更新订单
  order.subtotal = subtotal
  order.discounted = discounted
  order.tax = tax
  order.total = total

  io.println("Order processed. Total: {total}")
  return true
}
```

### 5. 注意副作用

明确记录和管理函数的副作用：

```vine
// 不好的做法：未预期的副作用
fn get_total(cart) {
  let total = 0
  let i = 0
  while i < cart.items.length() {
    total = total + cart.items[i].price
    // 意外的副作用：修改购物车项目
    cart.items[i].processed = true
    i = i + 1
  }
  return total
}

// 更好的做法：分离关注点
fn calculate_total(cart) {
  // 纯计算函数，无副作用
  let total = 0
  let i = 0
  while i < cart.items.length() {
    total = total + cart.items[i].price
    i = i + 1
  }
  return total
}

fn mark_items_processed(cart) {
  // 明确的副作用函数
  let i = 0
  while i < cart.items.length() {
    cart.items[i].processed = true
    i = i + 1
  }
}
```

## 综合使用命令式和函数式特性

### 混合风格示例：任务管理器

下面是一个结合命令式和函数式编程风格的更复杂示例：

```vine
// 任务管理器
pub fn task_manager(&io: &IO) {
  // 命令式：维护程序状态
  let tasks = []
  let next_id = 1
  let running = true

  // 函数式：纯函数用于任务操作
  let filter_tasks = fn(status) {
    let filtered = []
    let i = 0
    while i < tasks.length() {
      if tasks[i].status == status {
        filtered.push(tasks[i])
      }
      i = i + 1
    }
    return filtered
  }

  let find_task = fn(id) {
    let i = 0
    while i < tasks.length() {
      if tasks[i].id == id {
        return tasks[i]
      }
      i = i + 1
    }
    return null
  }

  // 命令式：主循环和用户交互
  while running {
    io.println("\n===== Task Manager =====")
    io.println("1. Add Task")
    io.println("2. List All Tasks")
    io.println("3. List Pending Tasks")
    io.println("4. List Completed Tasks")
    io.println("5. Mark Task as Completed")
    io.println("6. Exit")
    io.println("Enter your choice:")

    let choice = io.read_line()

    if choice == "1" {
      io.println("Enter task description:")
      let description = io.read_line()

      // 命令式：修改状态
      tasks.push({
        "id": next_id,
        "description": description,
        "status": "pending",
        "created_at": "current_time"  // 假设有获取当前时间的函数
      })
      next_id = next_id + 1

      io.println("Task added successfully!")
    } else if choice == "2" {
      if tasks.length() == 0 {
        io.println("No tasks found.")
      } else {
        io.println("All Tasks:")
        let i = 0
        while i < tasks.length() {
          let task = tasks[i]
          io.println("{task.id}. {task.description} [{task.status}]")
          i = i + 1
        }
      }
    } else if choice == "3" {
      // 函数式：使用纯函数过滤任务
      let pending = filter_tasks("pending")

      if pending.length() == 0 {
        io.println("No pending tasks found.")
      } else {
        io.println("Pending Tasks:")
        let i = 0
        while i < pending.length() {
          let task = pending[i]
          io.println("{task.id}. {task.description}")
          i = i + 1
        }
      }
    } else if choice == "4" {
      // 函数式：使用纯函数过滤任务
      let completed = filter_tasks("completed")

      if completed.length() == 0 {
        io.println("No completed tasks found.")
      } else {
        io.println("Completed Tasks:")
        let i = 0
        while i < completed.length() {
          let task = completed[i]
          io.println("{task.id}. {task.description}")
          i = i + 1
        }
      }
    } else if choice == "5" {
      io.println("Enter task ID to mark as completed:")
      let id = parseInt(io.read_line())

      // 混合：使用函数式查找，然后命令式更新
      let task = find_task(id)

      if task == null {
        io.println("Task not found.")
      } else {
        task.status = "completed"
        io.println("Task marked as completed!")
      }
    } else if choice == "6" {
      running = false
      io.println("Exiting Task Manager...")
    } else {
      io.println("Invalid choice. Please try again.")
    }
  }
}
```

## 总结

命令式编程是 Vine 语言中的一个强大范式，它使开发者能够直观地表达状态变化和控制流程。虽然 Vine 也支持函数式编程，但其命令式特性对于某些类型的问题是不可或缺的，特别是那些需要状态管理和交互的应用程序。

通过理解命令式编程的核心概念，如变量、赋值、顺序执行和循环，并结合函数式编程的优点，您可以充分利用 Vine 的全部功能，为不同类型的问题选择最合适的编程风格。

命令式和函数式范式不是相互排斥的——它们可以协同工作，取长补短。Vine 的设计允许您灵活地混合这两种范式，使您能够编写既清晰又高效的代码。

在下一章中，我们将探讨 Vine 的[混合编程模式](./12-hybrid-patterns.md)，深入研究如何有效地结合不同的编程范式来解决复杂问题。
