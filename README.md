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

7. **Prime Numbers** (`examples/primes.vi`) - Finds and displays prime numbers below 100 using a simple primality test.

## Vine Language Syntax

### Basic Structure

```vine
// Import standard library
use std::IO;

// Main function with IO parameter
pub fn main(&io: &IO) {
  io.println("Hello, Vine!")
}
```

### Variables and Data Types

```vine
// Variable declaration with implicit type inference
let number = 42
let is_active = true
let text = "Hello"

// Arrays/Lists
let numbers = []
numbers.push(10)
numbers.push(20)
```

### Control Flow

```vine
// If statements
if condition {
  io.println("Condition is true")
}

// While loops
let i = 0
while i < 10 {
  io.println("{i}")
  i = i + 1
}

// Conditional while loops
while i < 10 && is_valid {
  // Loop body
}
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
let is_less = a < b
let is_less_or_equal = a <= b
let is_greater = a > b

// Logical
let both_true = condition1 && condition2
```

### String Interpolation

```vine
let name = "Vine"
io.println("Hello, {name}!")
```

### Function Definition

```vine
fn calculate_sum(a: Int, b: Int) -> Int {
  return a + b
}
```

## Running the Examples

To run these examples, you need to have the Vine compiler installed. Once installed, you can run an example using:

```bash
cargo run -r --bin vine run examples/hello_world.vi
```

Replace `hello_world.vi` with the example you want to run.

## Note

The Vine language is still under heavy development, and syntax and features may change over time. These examples represent my understanding of the language based on available information.
