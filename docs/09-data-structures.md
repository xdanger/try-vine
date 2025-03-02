# 常见数据结构

数据结构是组织和存储数据的方式，对于解决不同类型的问题至关重要。本章将详细介绍 Vine 中的常见数据结构，包括它们的声明、操作和应用场景。

## 数组

数组是最基本的集合类型，用于存储相同类型的元素序列。

### 数组声明和初始化

在 Vine 中创建数组有几种方式：

```vine
// 字面量初始化
let numbers = [1, 2, 3, 4, 5]
let names = ["Alice", "Bob", "Charlie"]

// 创建空数组
let empty_array = []

// 如果实现支持，可能有初始化特定大小的数组的方法
// let zeros = Array(5, 0)  // 创建包含 5 个 0 的数组
```

### 数组访问和修改

使用索引访问和修改数组元素（索引从 0 开始）：

```vine
let fruits = ["Apple", "Banana", "Cherry"]

// 访问元素
let first_fruit = fruits[0]  // "Apple"
let second_fruit = fruits[1]  // "Banana"

// 修改元素
fruits[1] = "Blueberry"  // 现在 fruits 是 ["Apple", "Blueberry", "Cherry"]
```

### 数组常见操作

以下是数组上常见的操作：

```vine
let numbers = [10, 20, 30, 40, 50]

// 获取数组长度
let count = numbers.length()  // 5

// 遍历数组
let i = 0
let sum = 0
while i < numbers.length() {
  sum = sum + numbers[i]
  i = i + 1
}
io.println("Sum: {sum}")  // 输出 "Sum: 150"

// 在数组末尾添加元素（如果实现支持）
numbers.push(60)  // 现在 numbers 是 [10, 20, 30, 40, 50, 60]

// 移除最后一个元素（如果实现支持）
let last = numbers.pop()  // last = 60，numbers 变为 [10, 20, 30, 40, 50]

// 查找元素（使用循环实现）
fn find_element(array, target) {
  let i = 0
  while i < array.length() {
    if array[i] == target {
      return i  // 返回找到的索引
    }
    i = i + 1
  }
  return -1  // 表示未找到
}

let index = find_element(numbers, 30)  // 返回 2
```

### 多维数组

Vine 可能支持多维数组，即数组的数组：

```vine
// 创建 2x3 矩阵
let matrix = [
  [1, 2, 3],
  [4, 5, 6]
]

// 访问元素
let element = matrix[0][1]  // 1行2列的元素：2

// 修改元素
matrix[1][0] = 7  // 将第2行第1列的元素修改为7
```

### 数组的常见算法

以下是使用数组实现的一些常见算法：

```vine
// 求数组最大值
fn find_max(array) {
  if array.length() == 0 {
    return 0  // 或者其他表示错误的值
  }

  let max = array[0]
  let i = 1

  while i < array.length() {
    if array[i] > max {
      max = array[i]
    }
    i = i + 1
  }

  return max
}

// 数组排序（冒泡排序示例）
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
}
```

## 映射（Map）

映射（也称为字典或关联数组）是键值对的集合，允许通过键快速查找值。

### 映射声明和初始化

```vine
// 创建字面量映射
let person = {
  "name": "Alice",
  "age": 30,
  "is_student": false
}

// 创建空映射
let empty_map = {}
```

### 映射访问和修改

```vine
let student = {"name": "Bob", "grade": "A", "age": 22}

// 访问值
let name = student["name"]  // "Bob"
let grade = student["grade"]  // "A"

// 修改值
student["grade"] = "B"  // 更新现有键的值

// 添加新键值对
student["email"] = "bob@example.com"

// 检查键是否存在（如果实现支持）
let has_phone = student.has_key("phone")  // false

// 删除键值对（如果实现支持）
student.remove("age")
```

### 映射迭代

遍历映射的所有键值对：

```vine
let config = {
  "debug": true,
  "max_connections": 100,
  "timeout": 30
}

// 如果 Vine 支持获取所有键
let keys = config.keys()
let i = 0

while i < keys.length() {
  let key = keys[i]
  let value = config[key]
  io.println("{key}: {value}")
  i = i + 1
}

// 如果不支持，可能需要预先知道所有可能的键
let known_keys = ["debug", "max_connections", "timeout"]
let j = 0

while j < known_keys.length() {
  let key = known_keys[j]
  if config.has_key(key) {
    let value = config[key]
    io.println("{key}: {value}")
  }
  j = j + 1
}
```

### 映射的应用场景

映射在以下场景特别有用：

1. **频率计数**：统计元素出现的次数
2. **缓存**：存储计算结果以避免重复计算
3. **配置存储**：管理程序设置和参数
4. **关联数据**：建立对象之间的关系

```vine
// 频率计数示例
fn count_frequencies(words) {
  let frequencies = {}
  let i = 0

  while i < words.length() {
    let word = words[i]

    if frequencies.has_key(word) {
      frequencies[word] = frequencies[word] + 1
    } else {
      frequencies[word] = 1
    }

    i = i + 1
  }

  return frequencies
}

// 使用映射作为缓存
let cache = {}

fn fibonacci_with_cache(n) {
  // 检查结果是否已缓存
  let key = toString(n)
  if cache.has_key(key) {
    return cache[key]
  }

  // 计算结果
  let result = 0
  if n <= 1 {
    result = n
  } else {
    result = fibonacci_with_cache(n - 1) + fibonacci_with_cache(n - 2)
  }

  // 缓存结果
  cache[key] = result
  return result
}
```

## 结构体（Struct）

结构体是用户定义的复合数据类型，可以将不同类型的数据组合在一起。

### 结构体声明和初始化

```vine
// 定义结构体类型
struct Point {
  x: Int,
  y: Int
}

// 创建结构体实例
let origin = Point{x: 0, y: 0}
let point = Point{x: 10, y: 20}
```

### 结构体访问和修改

```vine
// 访问结构体字段
let x_coordinate = point.x  // 10
let y_coordinate = point.y  // 20

// 修改结构体字段
point.x = 15  // 更新字段值

// 结构体作为函数参数和返回值
fn calculate_distance(p1: Point, p2: Point) -> Float {
  let dx = p2.x - p1.x
  let dy = p2.y - p1.y
  return sqrt(dx * dx + dy * dy)
}

let distance = calculate_distance(origin, point)
```

### 结构体方法

如果 Vine 支持为结构体定义方法：

```vine
impl Point {
  // 创建新点的方法
  fn new(x, y) -> Point {
    return Point{x: x, y: y}
  }

  // 计算距原点距离的方法
  fn distance_from_origin(&self) -> Float {
    return sqrt(self.x * self.x + self.y * self.y)
  }

  // 平移点的方法
  fn translate(&self, dx, dy) -> Point {
    return Point{x: self.x + dx, y: self.y + dy}
  }
}

// 使用方法
let p = Point.new(3, 4)
let dist = p.distance_from_origin()  // 5.0
let moved = p.translate(2, -1)  // Point{x: 5, y: 3}
```

## 枚举（Enum）

枚举允许定义由有限数量命名常量组成的类型。

### 枚举声明和使用

```vine
// 定义简单枚举
enum Color {
  Red,
  Green,
  Blue
}

// 使用枚举
let background = Color.Green

// 在条件语句中使用枚举
if background == Color.Red {
  io.println("Background is red")
} else if background == Color.Green {
  io.println("Background is green")
} else if background == Color.Blue {
  io.println("Background is blue")
}
```

### 带值的枚举

如果 Vine 支持带值的枚举（类似于代数数据类型）：

```vine
// 定义带值的枚举
enum Shape {
  Circle{radius: Float},
  Rectangle{width: Float, height: Float},
  Triangle{base: Float, height: Float}
}

// 创建枚举实例
let circle = Shape.Circle{radius: 5.0}
let rectangle = Shape.Rectangle{width: 10.0, height: 20.0}

// 使用模式匹配处理不同形状
fn calculate_area(shape) {
  match shape {
    Shape.Circle{radius} => 3.14159 * radius * radius,
    Shape.Rectangle{width, height} => width * height,
    Shape.Triangle{base, height} => 0.5 * base * height
  }
}

let area = calculate_area(circle)  // 约 78.54
```

## 队列和栈

虽然 Vine 可能没有内置的队列和栈类型，但您可以使用数组实现这些数据结构。

### 栈实现

栈是后进先出（LIFO）的数据结构：

```vine
// 使用数组实现栈
struct Stack {
  items: Array
}

impl Stack {
  fn new() -> Stack {
    return Stack{items: []}
  }

  fn push(&self, item) {
    self.items.push(item)
  }

  fn pop(&self) {
    if self.is_empty() {
      return nil  // 或者其他表示错误的值
    }
    return self.items.pop()
  }

  fn peek(&self) {
    if self.is_empty() {
      return nil
    }
    return self.items[self.items.length() - 1]
  }

  fn is_empty(&self) -> Bool {
    return self.items.length() == 0
  }

  fn size(&self) -> Int {
    return self.items.length()
  }
}

// 使用栈
let stack = Stack.new()
stack.push(1)
stack.push(2)
stack.push(3)

io.println(stack.pop())  // 3
io.println(stack.peek())  // 2
io.println(stack.size())  // 2
```

### 队列实现

队列是先进先出（FIFO）的数据结构：

```vine
// 使用数组实现队列
struct Queue {
  items: Array
}

impl Queue {
  fn new() -> Queue {
    return Queue{items: []}
  }

  fn enqueue(&self, item) {
    self.items.push(item)
  }

  fn dequeue(&self) {
    if self.is_empty() {
      return nil
    }

    // 获取第一个元素
    let item = self.items[0]

    // 移除第一个元素（通过创建新数组）
    let new_items = []
    let i = 1
    while i < self.items.length() {
      new_items.push(self.items[i])
      i = i + 1
    }
    self.items = new_items

    return item
  }

  fn peek(&self) {
    if self.is_empty() {
      return nil
    }
    return self.items[0]
  }

  fn is_empty(&self) -> Bool {
    return self.items.length() == 0
  }

  fn size(&self) -> Int {
    return self.items.length()
  }
}

// 使用队列
let queue = Queue.new()
queue.enqueue("first")
queue.enqueue("second")
queue.enqueue("third")

io.println(queue.dequeue())  // "first"
io.println(queue.peek())     // "second"
io.println(queue.size())     // 2
```

## 链表

链表是一种线性数据结构，其中每个元素包含数据和指向下一个元素的引用。

### 链表实现

```vine
// 定义链表节点结构
struct Node {
  value: Any,
  next: Node  // 引用下一个节点
}

// 定义链表结构
struct LinkedList {
  head: Node,
  size: Int
}

impl LinkedList {
  fn new() -> LinkedList {
    return LinkedList{head: nil, size: 0}
  }

  fn add_first(&self, value) {
    let new_node = Node{value: value, next: self.head}
    self.head = new_node
    self.size = self.size + 1
  }

  fn add_last(&self, value) {
    let new_node = Node{value: value, next: nil}

    if self.is_empty() {
      self.head = new_node
    } else {
      // 找到最后一个节点
      let current = self.head
      while current.next != nil {
        current = current.next
      }
      current.next = new_node
    }

    self.size = self.size + 1
  }

  fn remove_first(&self) {
    if self.is_empty() {
      return nil
    }

    let value = self.head.value
    self.head = self.head.next
    self.size = self.size - 1
    return value
  }

  fn is_empty(&self) -> Bool {
    return self.head == nil
  }

  fn get_size(&self) -> Int {
    return self.size
  }
}

// 使用链表
let list = LinkedList.new()
list.add_last(10)
list.add_last(20)
list.add_first(5)

io.println(list.get_size())  // 3
io.println(list.remove_first())  // 5
```

## 数据结构的选择指南

在选择使用哪种数据结构时，考虑以下因素：

1. **访问模式**：需要随机访问还是顺序访问？
2. **操作频率**：插入、删除和查找哪个操作更频繁？
3. **内存限制**：数据规模和可用内存大小
4. **时间复杂度要求**：对不同操作的性能要求

数据结构选择指南：

| 数据结构 | 适用场景 | 不适用场景 |
|---------|---------|-----------|
| 数组 | 需要随机访问、固定大小、简单结构 | 频繁插入/删除、未知大小 |
| 映射 | 键值查找、计数、缓存 | 需要保持顺序、复杂操作 |
| 结构体 | 复合数据、对象表示 | 大量相同类型数据 |
| 栈 | 解析表达式、撤销操作、深度优先搜索 | 随机访问 |
| 队列 | 任务调度、广度优先搜索 | 随机访问 |
| 链表 | 频繁插入/删除、未知大小 | 随机访问 |

## 实际应用示例

### 使用映射进行词频统计

```vine
use std::IO;

fn word_frequency(text) {
  let words = split_string(text, " ")
  let frequencies = {}

  let i = 0
  while i < words.length() {
    let word = words[i]

    if frequencies.has_key(word) {
      frequencies[word] = frequencies[word] + 1
    } else {
      frequencies[word] = 1
    }

    i = i + 1
  }

  return frequencies
}

pub fn main(&io: &IO) {
  let text = "the quick brown fox jumps over the lazy dog"
  let frequencies = word_frequency(text)

  // 打印结果
  let words = frequencies.keys()
  let i = 0

  while i < words.length() {
    let word = words[i]
    io.println("{word}: {frequencies[word]}")
    i = i + 1
  }
}
```

### 使用结构体和数组实现简单的联系人管理系统

```vine
use std::IO;

struct Contact {
  name: String,
  email: String,
  phone: String
}

struct ContactList {
  contacts: Array
}

impl ContactList {
  fn new() -> ContactList {
    return ContactList{contacts: []}
  }

  fn add_contact(&self, name, email, phone) {
    let contact = Contact{name: name, email: email, phone: phone}
    self.contacts.push(contact)
  }

  fn find_by_name(&self, name) {
    let i = 0
    while i < self.contacts.length() {
      if self.contacts[i].name == name {
        return self.contacts[i]
      }
      i = i + 1
    }
    return nil
  }

  fn show_all(&self, &io: &IO) {
    let i = 0
    while i < self.contacts.length() {
      let contact = self.contacts[i]
      io.println("Name: {contact.name}, Email: {contact.email}, Phone: {contact.phone}")
      i = i + 1
    }
  }
}

pub fn main(&io: &IO) {
  let contacts = ContactList.new()

  contacts.add_contact("Alice", "alice@example.com", "123-456-7890")
  contacts.add_contact("Bob", "bob@example.com", "234-567-8901")
  contacts.add_contact("Charlie", "charlie@example.com", "345-678-9012")

  io.println("All contacts:")
  contacts.show_all(io)

  io.println("\nLooking up Bob:")
  let bob = contacts.find_by_name("Bob")
  if bob != nil {
    io.println("Found: {bob.name}, {bob.email}, {bob.phone}")
  } else {
    io.println("Contact not found")
  }
}
```

## 总结

数据结构是解决问题的关键工具，Vine 提供了多种数据结构，从简单的数组到复杂的用户定义类型。选择合适的数据结构可以显著提高程序的效率和可维护性。

通过理解每种数据结构的特点、优势和局限性，您可以为不同的问题选择最合适的解决方案。在实践中，往往需要组合使用多种数据结构来构建复杂的应用程序。

在下一章中，我们将探讨 Vine 的[函数式编程特性](./10-functional-programming.md)，了解如何利用函数式编程范式编写更简洁、更可靠的代码。
