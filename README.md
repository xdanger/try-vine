# Try Vine Compiler

This repository contains example programs written in the Vine programming language, showcasing various features and programming paradigms supported by Vine.

## About Vine

Vine is an experimental programming language based on interaction nets, featuring seamless interoperability between functional and imperative programming patterns. It compiles to Ivy, a low-level interaction-combinator language, which runs on the IVM (Interaction Virtual Machine).

For more information, visit [vine.dev](https://vine.dev/).

## Examples

This repository includes the following examples:

1. **Hello World** (`examples/hello_world.vi`) - A simple "Hello World" program that demonstrates basic syntax.

2. **Factorial** (`examples/factorial.vi`) - An iterative implementation of the factorial function, demonstrating basic arithmetic and loops.

3. **Fibonacci** (`examples/fibonacci.vi`) - A non-recursive implementation of Fibonacci sequence calculation, showing how to avoid stack overflow issues.

4. **Interaction Nets** (`examples/interaction_nets.vi`) - A conceptual demonstration of Vine's underlying interaction net model.

5. **Functional and Imperative** (`examples/functional_imperative.vi`) - Shows how Vine blends functional and imperative programming paradigms seamlessly.

6. **Data Structures** (`examples/data_structures.vi`) - Demonstrates working with basic variables, conditionals, loops, and simple calculations.

7. **Prime Numbers** (`examples/primes.vi`) - Finds and displays prime numbers below 1000 using a simple primality test.

8. **Simple Example** (`examples/simple_example.vi`) - A comprehensive demonstration of basic Vine syntax including variables, conditionals, loops, and boolean operations.

## Understanding Interaction Nets

Vine is based on interaction nets, which are a theoretical model of computation. Here's a brief introduction to help you understand this concept:

### What are Interaction Nets?

Interaction nets are a graphical model of computation where:

- **Cells** are the basic computational units, with ports for connections
- **Connections** (or wires) link ports between cells
- **Interactions** occur when two cells are connected by their principal ports
- **Reduction rules** define how interactions transform the network

Think of interaction nets as a graph-based model where computation happens through local interactions between connected nodes, following specific rules.

### How Vine Uses Interaction Nets

In Vine:

- Your code gets translated into an interaction net representation
- Computation proceeds through interactions between cells
- The interaction virtual machine (IVM) manages these interactions efficiently
- The metric "interactions" in performance reports counts how many cell interactions were processed

Understanding this model isn't necessary for basic Vine programming, but it helps explain the execution model and performance characteristics.

### Practical Implications

- **Performance**: The number of interactions often correlates with computational complexity
- **Parallelism**: Interaction nets are inherently parallel, though current Vine may not fully exploit this
- **Memory usage**: Each cell and connection requires memory allocation

## Vine Language Syntax

### Basic Structure

```vine
// Import standard library for I/O operations
use std::IO;

// Main function with IO parameter
// The &io parameter is required for I/O operations
pub fn main(&io: &IO) {
  io.println("Hello, Vine!")
}
```

### Variables and Data Types

```vine
// Variable declaration with implicit type inference
// No semicolons needed at the end of statements
let number = 42
let is_active = true
let text = "Hello"

// Variables can be reassigned
number = number + 1

// Maps/Dictionaries
let map = {}
map[key] = value

// Boolean values
let a = true
let b = false

// Note: Global variables (at file level) are not supported
// All variables must be declared within functions
```

### Control Flow

```vine
// If statements
if condition {
  io.println("Condition is true")
} else {
  io.println("Condition is false")
}

// While loops
let i = 0
while i < 10 {
  io.println("{i}")
  i = i + 1
}

// Compound conditions in while loops
while i < 10 && is_valid {
  // Loop body
}

// Note: For loops and break statements are not supported in the current version
```

### Operators

```vine
// Arithmetic
let sum = a + b
let difference = a - b
let product = a * b
let quotient = a / b
let remainder = a % b

// Comparison
let is_equal = a == b
let is_not_equal = a != b
let is_less = a < b
let is_less_or_equal = a <= b
let is_greater = a > b
let is_greater_or_equal = a >= b

// Logical
let and_result = condition1 && condition2
let or_result = condition1 || condition2
let not_result = !condition1
```

### String Interpolation

```vine
let name = "Vine"
let age = 42
// Use curly braces to insert variable values into strings
io.println("Hello, {name}! You are {age} years old.")
```

### Functions

```vine
// Function definitions appear to require explicit type annotations
// (Based on testing, though we've had mixed results)
fn add(a, b) {
  return a + b
}

// Functions using the return keyword
fn is_even(n) {
  if n % 2 == 0 {
    return true
  }
  return false
}

// Functions with expression as last statement (no return needed)
fn multiply(a, b) {
  a * b
}
```

### Simple Example

```vine
// A comprehensive example demonstrating basic Vine syntax
use std::IO;

pub fn main(&io: &IO) {
  io.println("Simple Vine Example")

  // Variables and arithmetic
  let x = 10
  let y = 5
  let sum = x + y
  let product = x * y

  io.println("x = {x}, y = {y}")
  io.println("x + y = {sum}")
  io.println("x * y = {product}")

  // Conditional statements
  if x > y {
    io.println("x is greater than y")
  } else {
    io.println("x is not greater than y")
  }

  // While loop
  let count = 1
  while count <= 5 {
    io.println("Count: {count}")
    count = count + 1
  }

  // Boolean operations
  let a = true
  let b = false
  io.println("a AND b: {a && b}")
  io.println("a OR b: {a || b}")
  io.println("NOT a: {!a}")
}
```

### Prime Number Example

```vine
// Finding prime numbers below 1000
use std::IO;

pub fn main(&io: &IO) {
  io.println("Finding prime numbers below 1000:")

  // Check each number from 2 to 999
  let n = 2
  while n < 1000 {
    let is_prime = true

    // Check divisibility up to sqrt(n)
    let i = 2
    while i * i <= n && is_prime {
      if n % i == 0 {
        is_prime = false
      }
      i = i + 1
    }

    if is_prime {
      io.print("{n} ")
    }

    n = n + 1
  }

  io.println("")
}
```

## Running the Examples

To run these examples, you need to have the Vine compiler installed. Once installed, you can run an example using:

```bash
vine run examples/hello_world.vi
```

Replace `hello_world.vi` with the example you want to run.

## Note

The Vine language is still under heavy development, and syntax and features may change over time. These examples represent my understanding of the language based on testing and experimentation.

## Common Issues and Best Practices

Based on practical experience with Vine, here are some common issues you might encounter and how to avoid them:

### I/O Operations

- **Always import the IO module**: Every program that needs to print output must include `use std::IO;`
- **Main function must accept IO parameter**: Always define your main function as `pub fn main(&io: &IO)`
- **Use the IO reference**: All print operations must use the io reference: `io.println()` and `io.print()` instead of directly using `println()` or `print()`

### Recursion Limitations

- **Stack overflow risks**: Deep recursion may cause stack overflow errors
- **Use iteration instead**: For algorithms like factorial or Fibonacci, prefer iterative implementations over recursive ones:

```vine
// Prefer this iterative approach for factorial
fn factorial(n) {
  let result = 1
  let i = 1
  while i <= n {
    result = result * i
    i = i + 1
  }
  return result
}

// Instead of this recursive approach
fn factorial_recursive(n) {
  if n <= 1 {
    return 1
  }
  return n * factorial_recursive(n - 1) // Risk of stack overflow for large n
}
```

### Arrays and Data Structures

- **Array indexing issues**: Complex array operations may have syntax limitations
- **For simple cases, use individual variables**: When working with a small fixed number of values, consider using individual variables instead of arrays
- **Be careful with array indexing**: Make sure array indices are valid and that the array has been properly initialized

```vine
// If you encounter issues with array indexing:
// Instead of:
let numbers = [1, 2, 3, 4, 5]
let sum = 0
let i = 0
while i < 5 {
  sum = sum + numbers[i]
  i = i + 1
}

// Consider:
let num1 = 1
let num2 = 2
let num3 = 3
let num4 = 4
let num5 = 5
let sum = num1 + num2 + num3 + num4 + num5
```

### Type System

- **Implicit type inference**: Vine generally infers types automatically, but be explicit when needed
- **Function parameters**: For complex functions, consider adding type annotations if you encounter errors
- **Return types**: Implicit return types work for simple functions, but explicit types might be needed for more complex cases

### Performance Considerations

- **Check interaction metrics**: Vine shows performance metrics after execution, including:
  - Total interactions (indicates computational complexity)
  - Memory usage
  - Execution time
  - Speed (Interactions Per Second)
- **Optimize high-interaction code**: If you see a very high number of interactions, consider algorithm optimization

### Debugging Tips

- **Error messages**: Vine error messages will point to the line number where the syntax error was detected
- **Isolate complex expressions**: If you get syntax errors in a complex expression, break it down into simpler parts with intermediate variables
- **Add debug prints**: Use `io.println()` statements to trace execution flow and inspect variable values

### Language Limitations

- **No global variables**: All variables must be defined within functions
- **No for loops or break statements**: Use while loops with counter variables instead
- **Limited library functions**: Compared to mature languages, Vine has a smaller standard library

### Running Programs

- **Command line execution**: Run programs using `vine run filename.vi`
- **Compilation errors**: Syntax errors will be reported before execution begins
- **Runtime errors**: Pay attention to the error messages which point to specific lines/issues

Following these guidelines should help you avoid common pitfalls when programming in Vine and make your development experience smoother.
