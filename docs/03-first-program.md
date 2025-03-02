# 第一个 Vine 程序

本章将指导您创建、编译和运行您的第一个 Vine 程序。通过一个简单的 "Hello, World!" 示例，您将学习 Vine 程序的基本结构，以及如何使用编译器。

## 创建 Hello World 程序

首先，创建一个新文件 `hello_world.vi`，并在其中输入以下代码：

```vine
// 导入标准库中的 IO 模块
use std::IO;

// 定义主函数
// 注意：&io 参数是必需的，用于输入和输出操作
pub fn main(&io: &IO) {
  io.println("Hello, World!")
}
```

保存文件后，您就创建了第一个 Vine 程序！

## 运行程序

要运行这个程序，请打开终端并导航到包含 `hello_world.vi` 文件的目录，然后执行：

```bash
vine run hello_world.vi
```

您应该会看到以下输出：

```
Hello, World!

Interactions
  Total                  263
  Annihilate             135
  ... (其他交互统计)

Memory
  Heap                   464 B
  ... (内存使用统计)

Performance
  Time                     0 ms
  Speed            7_678_832 IPS
```

恭喜！您已经成功运行了第一个 Vine 程序。

## 代码解释

让我们详细分析这个简单程序的各个部分：

### 导入 IO 模块

```vine
use std::IO;
```

这一行导入了标准库（`std`）中的 `IO` 模块。**这是所有需要输入或输出的 Vine 程序的必要步骤**。IO 模块提供了与控制台交互的功能，如 `println` 和 `print` 等方法。

### 主函数定义

```vine
pub fn main(&io: &IO) {
  // 函数体
}
```

这定义了程序的主入口点 `main` 函数：

- `pub` 关键字表示这个函数是公开的
- `fn` 关键字用于定义函数
- `main` 是特殊的函数名，表示程序的入口点
- `(&io: &IO)` 是参数列表，指定了一个名为 `io` 的 `IO` 类型引用参数
  - **注意**：这个参数是必需的，它允许函数调用 IO 操作

### 打印消息

```vine
io.println("Hello, World!")
```

这一行使用 `io` 对象的 `println` 方法打印字符串 "Hello, World!" 到控制台，并在末尾添加换行符。

注意以下几点：

1. 使用 `io.println` 而不是直接使用 `println`
2. 不需要在语句末尾添加分号
3. 字符串用双引号包围

### 输出解释

当您运行程序时，除了 "Hello, World!" 消息外，您还会看到一些性能统计信息：

- **Interactions**：显示程序执行过程中的交互次数和类型
- **Memory**：显示内存使用情况
- **Performance**：显示执行时间和每秒交互数（IPS）

这些信息对于理解和优化程序性能非常有用，特别是对于更复杂的应用程序。

## 常见错误和解决方案

编写第一个程序时可能会遇到一些常见错误，以下是解决方法：

### 1. 缺少 IO 导入

**错误**：

```
Error: Cannot find IO in scope
```

**解决方案**：确保添加 `use std::IO;` 到文件顶部

### 2. 错误的主函数签名

**错误**：

```
Error: Wrong main function signature
```

**解决方案**：确保主函数定义为 `pub fn main(&io: &IO)`，参数名称和类型都必须正确

### 3. 直接使用 println

**错误**：

```
Error: Cannot find println in this scope
```

**解决方案**：使用 `io.println` 而不是 `println`

### 4. 语法错误

**错误**：

```
Error: Expected ... found ...
```

**解决方案**：检查代码格式，注意括号匹配、引号使用等

## 扩展 Hello World 程序

让我们稍微扩展一下这个程序，添加更多功能：

```vine
use std::IO;

pub fn main(&io: &IO) {
  let name = "Vine"
  let year = 2023

  io.println("Hello, World!")
  io.println("Welcome to {name} programming!")
  io.println("This language was created in {year}")

  // 计算并显示一些简单的算术
  let sum = 5 + 7
  io.println("5 + 7 = {sum}")
}
```

这个扩展版本展示了变量声明、字符串插值和基本算术操作。运行这个程序，您将看到更丰富的输出。

## 下一步

现在您已经创建并运行了第一个 Vine 程序，您可以：

1. 尝试修改这个程序，添加更多的打印语句、变量或简单计算
2. 探索更多的[基本语法](./04-basic-syntax.md)，包括变量、表达式和语句
3. 查看示例目录中的其他简单程序，理解它们的工作原理

在下一章中，我们将深入探讨 Vine 的基本语法元素，包括变量、注释和表达式。
