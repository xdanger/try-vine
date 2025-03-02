# Try Vine Compiler

This repository contains example programs written in the Vine programming language, showcasing various features and programming paradigms supported by Vine.

## About Vine

Vine is an experimental programming language based on interaction nets, featuring seamless interoperability between functional and imperative programming patterns. It compiles to Ivy, a low-level interaction-combinator language, which runs on the IVM (Interaction Virtual Machine).

For more information, visit [vine.dev](https://vine.dev/).

## Examples

This repository includes the following examples:

1. **Hello World** (`examples/hello_world.vi`) - A simple "Hello World" program that demonstrates basic syntax.

2. **Factorial** (`examples/factorial.vi`) - A recursive implementation of the factorial function.

3. **Fibonacci** (`examples/fibonacci.vi`) - Computation of Fibonacci numbers with memoization to improve performance.

4. **Interaction Nets** (`examples/interaction_nets.vi`) - Demonstrates Vine's core interaction net concept.

5. **Functional and Imperative** (`examples/functional_imperative.vi`) - Shows how Vine blends functional and imperative programming paradigms seamlessly.

6. **Data Structures** (`examples/data_structures.vi`) - Demonstrates working with various data structures like structs, maps, and arrays.

7. **Prime Numbers** (`examples/primes.vi`) - Finds and displays prime numbers below 1000 using a simple primality test.

8. **Simple Example** (`examples/simple_example.vi`) - A comprehensive demonstration of basic Vine syntax including variables, conditionals, loops, and boolean operations.

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
