---
layout: post
title:  "Google Comprehensive Rust Course"
---


# Comprehensive Rust 🦀

## Basics

### Hello World!

```rust
fn main() {
    println!("Hello 🌍!");
}
````
- Functions are introduced with `fn`.

- Blocks are delimited by curly braces.

- The main function is the entry point of the program.

- Rust has hygienic macros, `println!` is an example of this.

- Rust strings are UTF-8 encoded and can contain any Unicode character.


### Variables

```rust
fn main() {
    let mut x: i32 = 10;
    println!("x: {x}");
    x = 20;
    println!("x: {x}");
}
```
- The `mut` keyword to allow changes.

- The `i32` here is the type of the variable.

### Values

Here are some basic built-in types, and the syntax for literal values of each type.

|                      | Types                           | Literals                 |
|----------------------|---------------------------------|--------------------------|
| Signed integers      | i8, i16, i32, i64, i128, isize    | -10,  0,  1_000,  123_i64     |
| Unsigned integers    | u8, u16, u32, u64, u128, usize      |  0,  123,  10_u16              |
| Floating point numbers| f32, f64                         |  3.14, -10.0e20,  2_f32        |
| Unicode scalar values| char                            | 'a', 'α', '∞'               |
| Booleans            | bool                            | true, false               |

The types have widths as follows:

- `iN`, `uN`, and `fN` are `N` bits wide,
- `isize` and `usize` are the width of a pointer,
- `char` is 32 bits wide,
- `bool` is 8 bits wide.


### Arithmetic

```rust
fn interproduct(a: i32, b: i32, c: i32) -> i32 {
    return a * b + b * c + c * a;
}

fn main() {
    println!("result: {}", interproduct(100, 110, 120));
}
```
If we change the `i32’s` to `i16` to see an integer overflow, which panics (checked) in a debug build and wraps in a release build. 


### Strings

- `String` : a modifiable, owned string.
- `&str`   : a read-only string. String literals have this type.

```rust

fn main() {
    // Concatenating strings
    let greeting: &str = "Hello";
    let name: &str = "Murali";
    let mut message = String::new();
    message.push_str(greeting);
    message.push_str(" ");
    message.push_str(name);
    println!("Message: {}", message);

    // Slicing a string
    let full_name: &str = "Murali Gari";
    let first_name = &full_name[0..4]; // Slice from index  0 to 4
    println!("First name: {}", first_name);

    // Modifying a string
    let mut greeting = String::from("Good morning");
    greeting.push_str(", ");
    greeting.push_str("world!");
    println!("Greeting: {}", greeting);

    // String interpolation
    let name = "Murali";
    let age =  21;
    let greeting = format!("Hello, {}! You are {} years old.", name, age);
    println!("{}", greeting);

    // String concatenation using `+`
    let hello = String::from("Hello");
    let world = String::from("World!");
    let hello_world = hello + " " + &world; // `&world` to create a reference
    println!("{}", hello_world);
}
```


### Type Inference

Type inference in Rust allows the compiler to deduce the type of an expression without explicit type annotations.

1. **Literal Type Inference**:
   ```rust
   let x =  10; // x is inferred to be i32
   let y =  10.0; // y is inferred to be f64
   let z = true; // z is inferred to be bool
   ```

2. **Function Return Type Inference**:
   ```rust
   fn add(a: i32, b: i32) -> i32 {
       a + b
   } // The return type is inferred to be i32
   ```

3. **Variable Type Inference**:
   ```rust
   let x =  10; // x is inferred to be i32
   let y = x +  20; // y is inferred to be i32
   ```

4. **Struct Type Inference**:
   ```rust
   struct Point {
       x: i32,
       y: i32,
   }

   let p = Point { x:  10, y:  20 }; // p is inferred to be Point
   ```

5. **Enum Type Inference**:
   ```rust
   enum Message {
       Quit,
       Move { x: i32, y: i32 },
       Write(String),
       ChangeColor(i32, i32, i32),
   }

   let m = Message::Write(String::from("hello")); // m is inferred to be Message
   ```

6. **Trait Object Type Inference**:
   ```rust
   trait Animal {
       fn make_noise(&self);
   }

   let animal: &dyn Animal = &Dog; // animal is inferred to be &dyn Animal
   ```

7. **Closure Type Inference**:
   ```rust
   let add_one = |x| x +  1; // add_one is inferred to be a closure that takes an i32 and returns an i32
   ```

8. **Generic Type Inference**:
   ```rust
   fn largest<T>(list: &[T]) -> T {
       let mut largest = list[0];
       for &item in list.iter() {
           if item > largest {
               largest = item;
           }
       }
       largest
   }

   let number_list = vec![34,  50,  25,  100,  65];
   let result = largest(&number_list); // result is inferred to be i32
   ```

9. **Type Inference with `let` Statements**:
   ```rust
   let guess = "42".parse().expect("Not a number!"); // guess is inferred to be i32
   ```

10. **Type Inference with `match` Statements**:
    ```rust
    let value = Some(5);
    match value {
        Some(i) => println!("Got an integer: {}", i), // i is inferred to be i32
        _ => (),
    }
    ```

Rust's type inference system determines the type of the variable or expression based on the context in which it is used.

```rust
fn takes_u32(x: u32) {
    println!("u32: {x}");
}

fn takes_i8(y: i8) {
    println!("i8: {y}");
}

fn main() {
    let x = 10;
    let y = 20;

    takes_u32(x);
    takes_i8(y);
    // takes_u32(y);
}
```
When nothing constrains the type of an integer literal, Rust defaults to `i32`. Similarly, floating-point literals default to `f64`.

```rust
fn main() {
    let x = 3.14;
    let y = 20;
    assert_eq!(x, y);
    // ERROR: no implementation for `{float} == {integer}`
}
```



## Loops

### while
```rust
fn main() {
     let mut x = 60;
     while x >= 10 {
         x = x / 2;
     }
     println!("Final x: {x}");
}
```


### for
```rust
fn main() {
    for x in 1..5 {
        println!("x: {x}");
    }
}
// loop : loop forever until a break statement
fn main() {
    let mut i = 0;
    loop {
        i += 1;
        println!("{i}");
        if i > 100 {
            break;
        }
    }
}

```



## Outer and inner labels in nested loops

loop labels are required to `break` or `continue` out of multiple levels of a nested loop.

```rust
fn main() {
    'outer: for x in 1..5 {
        println!("x: {x}");
        let mut i = 0;
        while i < x {
            println!("x: {x}, i: {i}");
            i += 1;
            if i == 4 {
                break 'outer;
            }
        }
    }
}

```
### Break
```rust
fn main() {
    let (mut a, mut b) = (100, 52);
    let result = loop {
        if a == b {
            break a;
        }
        if a < b {
            b -= a;
        } else {
            a -= b;
        }
    };
    println!("{result}");
}
```

## functions

```rust
fn gcd(a: u32, b: u32) -> u32 {
    if b > 0 {
        return gcd(b, a % b);
    }
    else {
        return a;
    }
}

fn main() {
    println!("gcd is {}", gcd(6543, 432));
}
```

## Macros

Macros are distinguished by a `!` at the end.

- `println!(format, ..)` prints a line to standard output, applying formatting described in `std::fmt.`

- `format!(format, ..)` works just like println! but returns the result as a string.

- `dbg!(expression)` logs the value of the expression and returns it.

- `todo!()` marks a bit of code as not-yet-implemented. If executed, it will panic.

- `unreachable!()` marks a bit of code as unreachable. If executed, it will panic.


```rust

fn factorial(n: u32) -> u32 {
    let mut product = 1;
    for i in 1..=n {
        product *= dbg!(i);
    }
    product
}

fn fizzbuzz(n: u32) -> u32 {
    todo!()
}

fn main() {
    let n = 4;
    println!("{n}! = {}", factorial(n));
}
```


## Collatz Sequence

**Determine the length of the collatz sequence beginning at `n`.**
```rust
fn collatz_length(mut n: i32) -> u32 {
    let mut count = 0;

    while n != 1 {
        if n % 2 == 1 {
            n = 3 * n + 1;
        }
        else if n % 2 == 0 {
            n = n / 2;
        }
        else {
            return count;
        }
        count += 1; 
    }
    count
}

fn main() {
  println!("Length is {}", collatz_length(10))
}
```


## Transposed matrix

```rust
fn transpose(matrix: [[i32; 3]; 3]) -> [[i32; 3]; 3] {
   let mut transposed = [[0; 3]; 3];
   for i in 0..3 {
       for j in 0..3 {
           transposed[j][i] = matrix[i][j];
       }
   }
   transposed
}

fn main() {
   let matrix = [
       [101, 102, 103],
       [201, 202, 203],
       [301, 302, 303],
   ];

   println!("matrix: {:#?}", matrix);
   let transposed = transpose(matrix);
   println!("transposed: {:#?}", transposed);
}
```



## Structs

```rust
struct Foo {
    x: (u32, u32),
    y: u32,
}

#[rustfmt::skip]
fn main() {
    let foo = Foo { x: (1, 2), y: 3 };
    match foo {
        Foo { x: (1, b), y } => println!("x.0 = 1, b = {b}, y = {y}"),
        Foo { y: 2, x: i }   => println!("y = 2, x = {i:?}"),
        Foo { y, .. }        => println!("y = {y}, other fields were ignored"),
    }
}
```

## Enums

```rust
enum Result {
    Ok(i32),
    Err(String),
}

fn divide_in_two(n: i32) -> Result {
    if n % 2 == 0 {
        Result::Ok(n / 2)
    } else {
        Result::Err(format!("cannot divide {n} into two equal parts"))
    }
}

fn main() {
    let n = 100;
    match divide_in_two(n) {
        Result::Ok(half) => println!("{n} divided in two is {half}"),
        Result::Err(msg) => println!("sorry, an error happened: {msg}"),
    }
}

```



## Reverse a string

```rust
fn main() {
    let mut name = String::from("Comprehensive Rust 🦀");
    while let Some(c) = name.pop() {
        println!("character: {c}");
    }
}
```



## Vec

```rust
fn main() {
    let mut v1 = Vec::new();
    v1.push(42);
    println!("v1: len = {}, capacity = {}", v1.len(), v1.capacity());

    let mut v2 = Vec::with_capacity(v1.len() + 1);
    v2.extend(v1.iter());
    v2.push(9999);
    println!("v2: len = {}, capacity = {}", v2.len(), v2.capacity());

    // Canonical macro to initialize a vector with elements.
    let mut v3 = vec![0, 0, 1, 2, 3, 4];

    // Retain only the even elements.
    v3.retain(|x| x % 2 == 0);
    println!("{v3:?}");

    // Remove consecutive duplicates.
    v3.dedup();
    println!("{v3:?}");
}
```

## HashMap

```rust
use std::collections::HashMap;

fn main() {
    let mut page_counts = HashMap::new();
    page_counts.insert("Adventures of Huckleberry Finn".to_string(), 207);
    page_counts.insert("Grimms' Fairy Tales".to_string(), 751);
    page_counts.insert("Pride and Prejudice".to_string(), 303);

    if !page_counts.contains_key("Les Misérables") {
        println!(
            "We know about {} books, but not Les Misérables.",
            page_counts.len()
        );
    }

    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        match page_counts.get(book) {
            Some(count) => println!("{book}: {count} pages"),
            None => println!("{book} is unknown."),
        }
    }

    // Use the .entry() method to insert a value if nothing is found.
    for book in ["Pride and Prejudice", "Alice's Adventure in Wonderland"] {
        let page_count: &mut i32 = page_counts.entry(book.to_string()).or_insert(0);
        *page_count += 1;
    }

    println!("{page_counts:#?}");
}
```


## Triats

```rust

trait Shape {
    fn area(&self) -> f64;
}

struct Circle {
    radius: f64,
}

impl Shape for Circle {    // Implement the 'Shape' trait for a 'Circle' struct
    fn area(&self) -> f64 {
        std::f64::consts::PI * self.radius * self.radius
    }
}

struct Rectangle {
    width: f64,
    height: f64,
}

impl Shape for Rectangle {    // Implement the 'Shape' trait for a 'Rectangle' struct
    fn area(&self) -> f64 {
        self.width * self.height
    }
}

fn main() {
    // Create instances of 'Circle' and 'Rectangle'
    let circle = Circle { radius: 5.0 };
    let rectangle = Rectangle { width: 4.0, height: 6.0 };

    println!("Circle area: {}", circle.area());

    println!("Rectangle area: {}", rectangle.area());
}

```


## From and Into

```rust
// From
fn main() {
    let s = String::from("hello");
    let addr = std::net::Ipv4Addr::from([127, 0, 0, 1]);
    let one = i16::from(true);
    let bigger = i32::from(123_i32);
    println!("{s}, {addr}, {one}, {bigger}");
}

// Intro
fn main() {
    let s: String = "hello".into();
    let addr: std::net::Ipv4Addr = [127, 0, 0, 1].into();
    let one: i16 = true.into();
    let bigger: i32 = 123_i16.into();
    println!("{s}, {addr}, {one}, {bigger}");
}
```



## Casting: as, TryFrom, TryInto

```rust
// as

fn main() {
    let value: i64 = 1000;
    println!("as u16: {}", value as u16);
    println!("as i16: {}", value as i16);
    println!("as u8: {}", value as u8);
}

use std::convert::TryFrom;
use std::convert::TryInto;

fn main() {
    let value: u32 =  1000;

    // Attempt to cast to u16
    match value.try_into() {
        Ok(val) => println!("Value as u16: {}", val),
        Err(_) => println!("Failed to convert to u16"),
    }

    // Attempt to cast to i16
    match value.try_into() {
        Ok(val) => println!("Value as i16: {}", val),
        Err(_) => println!("Failed to convert to i16"),
    }

    // Attempt to cast to u8
    match value.try_into() {
        Ok(val) => println!("Value as u8: {}", val),
        Err(_) => println!("Failed to convert to u8"),
    }
}
```




## Trait objects

```rust
#[allow(dead_code)]
struct Dog {
    name: String,
    age: i8,
}
struct Cat {
    lives: i8,
}

trait Pet {
    fn talk(&self) -> String;
}

impl Pet for Dog {
    fn talk(&self) -> String {
        format!("My name is {}!", self.name)
    }
}

impl Pet for Cat {
    fn talk(&self) -> String {
        String::from("Mia!")
    }
}

fn main() {
    let pets: Vec<Box<dyn Pet>> = vec![
        Box::new(Cat { lives: 9 }),
        Box::new(Dog { name: String::from("Fida"), age: 5 }),
    ];
    for pet in pets {
        println!("Hi, who are you? {}", pet.talk());
    }
    println!("{} {}", std::mem::size_of::<Dog>(), std::mem::size_of::<Cat>());
    println!("{} {}", std::mem::size_of::<&Dog>(), std::mem::size_of::<&Cat>());
    println!("{}", std::mem::size_of::<&dyn Pet>());
    println!("{}", std::mem::size_of::<Box<dyn Pet>>());
}
```


## Borrowing Value

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn add(p1: &Point, p2: &Point) -> Point {  // The add function borrows two points and returns a new point.
    Point(p1.0 + p2.0, p1.1 + p2.1)
}

fn main() {
    let p1 = Point(3, 4);
    let p2 = Point(10, 20);
    let p3 = add(&p1, &p2);
    println!("{p1:?} + {p2:?} = {p3:?}");
}
```


## Borrow Checking
```rust
fn main() {
    let mut a: i32 = 10;
    let b: &i32 = &a;
    println!("b: {b}"); // The code does not compile because a is borrowed as mutable (through c) and as immutable (through b) at the same time.

    {
        let c: &mut i32 = &mut a;
        *c = 20;
    }

    println!("a: {a}");
    // println!("b: {b}");
}
```

## Slicing
```rust
fn main() {
    let mut a: [i32; 6] = [10, 20, 30, 40, 50, 60];   
    println!("a: {a:?}");  

    let s: &[i32] = &a[2..4];   //If the slice starts at index 0, &a[0..a.len()] and &a[..a.len()] are identical.

    println!("s: {s:?}");
}
```


## Number Validation
```rust
use std::io;

fn main(){

   let mut x = String::new();

   println!("Please enter a number: ");

   io::stdin().read_line(&mut x).unwrap();

   let x: i32 = match x.trim().parse() {    
    Ok(num) => num,
    Err(_) => {                
        println!("That's not a valid number!");
        return;
    },
   };

    if x < 50 {        
        println!("small");
    }
    else if x < 100 {
        println!("Medium");
    }
    else {
        println!("Large");
    }    
}
```

## String References

```rust
fn main() {
    let s1: &str = "World";
    println!("s1: {s1}");

    let mut s2: String = String::from("Hello ");
    println!("s2: {s2}");
    s2.push_str(s1);
    println!("s2: {s2}");

    let s3: &str = &s2[6..];
    println!("s3: {s3}");
}
```

## Lifetime Annotations

```rust
#[derive(Debug)]
struct Point(i32, i32);

fn left_most<'a>(p1: &'a Point, p2: &'a Point) -> &'a Point {
    if p1.0 < p2.0 {
        p1
    } else {
        p2
    }
}

fn main() {
    let p1: Point = Point(10, 10);
    let p2: Point = Point(20, 20);
    let p3 = left_most(&p1, &p2); // What is the lifetime of p3?
    println!("p3: {p3:?}");
}
```

`Lifetimes in Function Calls:`:
- Each argument which does not have a lifetime annotation is given one.

- If there is only one argument lifetime, it is given to all un-annotated return values.

- If there are multiple argument lifetimes, but the first one is for self, that lifetime is given to all un-annotated return values.



## Fibonacci using Iterator trait
```rust
struct Fibonacci {
    curr: u32,
    next: u32,
}

impl Iterator for Fibonacci {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.curr + self.next;
        self.curr = self.next;
        self.next = new_next;
        Some(self.curr)
    }
}

fn main() {
    let fib = Fibonacci { curr: 0, next: 1 };
    for (i, n) in fib.enumerate().take(10) {
        println!("fib({i}): {n}");
    }
}
```

- `IntoIterator` defines how to create an iterator for a type.

- `FromIterator` lets you build a collection from an Iterator.


## Modules

```rust
mod foo {
    pub fn do_something() {
        println!("In the foo module");
    }
}

mod bar {
    pub fn do_something() {
        println!("In the bar module");
    }
}

fn main() {
    foo::do_something();
    bar::do_something();
}
```

### Filesystem hierarchy

- The main reason to introduce `filename.rs` as alternative to `filename/mod.rs` was because many files named `mod.rs` can be hard to distinguish in IDEs.

- Deeper nesting can use folders, even if the main module is a file:
```
src/
├── main.rs
├── top_module.rs
└── top_module/
    └── sub_module.rs
```

### Visibility

Modules are a privacy boundary:

- Module items are private by default (hides implementation details).

- Parent and sibling items are always visible.

- In other words, if an item is visible in module foo, it’s visible in all the descendants of foo.

```rust
mod outer {
    fn private() {
        println!("outer::private");
    }

    pub fn public() {
        println!("outer::public");
    }

    mod inner {
        fn private() {
            println!("outer::inner::private");
        }

        pub fn public() {
            println!("outer::inner::public");
            super::private();
        }
    }
}

fn main() {
    outer::public();
}
```

In Rust, `use`, `super`, and `self` are used to refer to modules and their items.

```rust
// src/lib.rs
mod foo {
    pub fn function() {
        println!("Called foo's function");
    }

    pub mod bar {
        pub fn function() {
            println!("Called bar's function");
        }
    }
}

// src/main.rs
use crate::foo::bar;

fn main() {
    bar::function(); 
    super::foo::function(); 
    self::foo::function(); 
}
```

- `use crate::foo::bar;` imports the `bar` module from the `foo` module into the current scope.

- `super::foo::function();` calls the `function` from the `foo` module using `super`, which refers to the parent module.

- `self::foo::function();` calls the `function` from the `foo` module using `self`, which refers to the current module.

The `use` keyword is used to bring items into scope, `super` is used to refer to the parent module, and `self` is used to refer to the current module.


## Testing

### Unit Tests
- Unit tests are supported throughout the code.

- Unit tests are often put in a nested tests module, using `#[cfg(test)]` to conditionally compile them only when building tests.

- The `#[cfg(test)]` attribute is only active when you run `cargo test`.

```rust
pub fn do_something(name: &str) -> String {
    format!("Hello {}", name)
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn check_name() {
        let result = do_something("Murali");
        assert!(result.contains("Murali"));
    }

    #[test]
    fn check_lowercase() {
        let result = do_something("Murali");
        assert_eq!(result.to_lowercase(), "hello murali");
    }

    #[test]
    fn check_starts_with() {
        let result = do_something("Murali");
        assert!(result.starts_with("Hello"));
    }

    #[test]
    fn check_ends_with() {
        let result = do_something("Murali");
        assert!(result.ends_with("Murali"));
    }

    #[test]
    fn check_len() {
        let result = do_something("Murali");
        assert_eq!(result.len(), 12);
    }

    #[test]
    fn check_is_empty() {
        let empty_string = "";
        assert!(empty_string.is_empty());
    }

    #[test]
    fn check_trim() {
        let result = do_something("Murali");
        assert_eq!(result.trim(), "Hello Murali");
    }
}
```

```rust
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(idx) => &text[..idx],
        None => &text,
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_empty() {
        assert_eq!(first_word(""), "");
    }

    #[test]
    fn test_single_word() {
        assert_eq!(first_word("Hello"), "Hello");
    }

    #[test]
    fn test_multiple_words() {
        assert_eq!(first_word("Hello Murali"), "Hello");
    }
}
```

### Integration Tests

If we want to test our library as a client, use an integration test.

Create a `.rs` file under `tests/`:

```rust
// tests/integration_test.rs

use my_crate::my_function;

#[test]
fn test_my_function() {
    let input = "some input";
    let expected_output = "expected output";

    assert_eq!(my_function(input), expected_output);
}
```

```rust
// tests/my_library.rs

use my_library::init;

#[test]
fn test_init() {
    assert!(init().is_ok());
}
```

- In this example, the `test_init` function tests the init function of `my_library`. It asserts that the `init` function returns `Ok`, indicating that the initialization was successful.

- To run your integration tests, we can use the `cargo test` command.




### GoogleTest Crate
- The `GoogleTest` crate allows for flexible test `assertions` using `matchers`:

```rust
use googletest::prelude::*;

#[test]
fn fails_and_panics() {
    let value = 2;
    assert_that!(value, eq(4));
}

#[googletest::test]
fn two_logged_failures() {
    let value = 2;
    expect_that!(value, eq(4)); // Test now failed, but continues executing.
    expect_that!(value, eq(5)); // Second failure is also logged.
}

#[test]
fn fails_immediately_without_panic() -> Result<()> {
    let value = 2;
    verify_that!(value, eq(4))?; // Test fails and aborts.
    verify_that!(value, eq(2))?; // Never executes.
    Ok(())
}

#[test]
fn simple_assertion() -> Result<()> {
    let value = 2;
    verify_that!(value, eq(4)) // One can also just return the last assertion.
}

#[test]
fn test_multiline_string_diff() {
    let haiku = "Memory safety found,\n\
                 Rust's strong typing guides the way,\n\
                 Secure code you'll write.";
    assert_that!(
        haiku,
        eq("Memory safety found,\n\
            Rust's silly humor guides the way,\n\
            Secure code you'll write.")
    );
}

#[googletest::test]
fn contains_at_least_one_item_at_least_3() {
    let value = vec![1, 2, 3];
    expect_that!(value, contains(ge(3)));
}

#[googletest::test]
fn strictly_between_9_and_11() {
    let value = 10;
    expect_that!(value, gt(9).and(not(ge(11))));
}

```

### Mocking

- Mocking: While not directly part of the `googletest` crate, Rust has its own ecosystem for mocking, such as the `mockall` crate, which can be used in conjunction with googletest to create mock objects for testing.

```rust
use std::time::Duration;

#[mockall::automock]
pub trait Pet {
    fn is_hungry(&self, since_last_meal: Duration) -> bool;
}

#[test]
fn test_robot_dog() {
    let mut mock_dog = MockPet::new();
    mock_dog.expect_is_hungry().return_const(true);
    assert_eq!(mock_dog.is_hungry(Duration::from_secs(10)), true);
}

#[test]
fn test_robot_cat() {
    let mut mock_cat = MockPet::new();
    mock_cat
        .expect_is_hungry()
        .with(mockall::predicate::gt(Duration::from_secs(3 * 3600)))
        .return_const(true);
    mock_cat.expect_is_hungry().return_const(false);
    assert_eq!(mock_cat.is_hungry(Duration::from_secs(1 * 3600)), false);
    assert_eq!(mock_cat.is_hungry(Duration::from_secs(5 * 3600)), true);
}
```

## Error Handling

### Panics

- Rust will trigger a panic if a fatal error happens at runtime:

```rust
fn main() {
    let v = vec![10, 20, 30];
    println!("v[10]: {}", v[10]); // v[0]
}
```
    Compiling playground v0.0.1 (/playground)
        Finished dev [unoptimized + debuginfo] target(s) in 0.54s
        Running `target/debug/playground`
    thread 'main' panicked at src/main.rs:3:28:
    index out of bounds: the len is 3 but the index is 10
    note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace


`panic!` Macro:

The `panic!` macro is used to create a panic, which is an unrecoverable error. When a panic occurs, the program will print a failure message, unwind and clean up the stack, and then quit.

```rust
fn main() {
    panic!("This is a panic!");
}
```

### Try Operator

The try-operator `?` is used to return errors to the caller.

```rust
match some_expression {
    Ok(value) => value,
    Err(err) => return Err(err),
}
```
It's a shorthand for handling `Result` types, making error handling more concise and readable.

```rust
use std::fs::File;
use std::io::{self, Read};
use std::path::Path;

fn read_file_to_string<P: AsRef<Path>>(path: P) -> io::Result<String> {
    let mut file = File::open(path)?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}

fn main() {
    match read_file_to_string("/file.txt") {
        Ok(contents) => println!("File contents: {}", contents),
        Err(e) => println!("Error reading file: {}", e),
    }
}
```
If either of these operations returns an `Err`, the `?` operator will immediately return this error from the `read_file_to_string` function. If both operations succeed, the function returns the contents of the file wrapped in an `Ok`.


### thiserror  and anyhow

The `thiserror` and `anyhow` crates are widely used to simplify error handling.

- `thiserror` is often used in libraries to create custom error types that implement `From<T>`.  It allows you to define your own error types that implement the `std::error::Error` trait.

- `anyhow` is often used by applications to help with error handling in functions, including adding contextual information to your errors.

```rust
use anyhow::{bail, Context, Result};
use std::fs;
use std::io::Read;
use thiserror::Error;

#[derive(Clone, Debug, Eq, Error, PartialEq)]
#[error("Found no username in {0}")]
struct EmptyUsernameError(String);

fn read_username(path: &str) -> Result<String> {
    let mut username = String::with_capacity(100);
    fs::File::open(path)
        .with_context(|| format!("Failed to open {path}"))?
        .read_to_string(&mut username)
        .context("Failed to read")?;
    if username.is_empty() {
        bail!(EmptyUsernameError(path.to_string()));
    }
    Ok(username)
}

fn main() {
    //fs::write("config.dat", "").unwrap();
    match read_username("config.dat") {
        Ok(username) => println!("Username: {username}"),
        Err(err) => println!("Error: {err:?}"),
    }
}
```

## Unsafe Rust

### Unsafe

Can trigger undefined behavior if preconditions are violated.

In both unsafe functions and unsafe blocks, Rust will let you do three things that you normally can not do.
they are:

- Access or update a static mutable variable.
- Dereference a raw pointer.
- Call unsafe functions. This is the most powerful ability.

`unsafe` is used in four contexts:

1. The first one is to mark a function as `unsafe`:

```rust

#![allow(unused_variables)]
fn main() {
unsafe fn danger_will_robinson() {
    // Scary stuff...
}
}
```
2. The second use of unsafe is an `unsafe block`:

```rust

#![allow(unused_variables)]
fn main() {
unsafe {
    // Scary stuff...
}
}
```

3. The third is for `unsafe traits`:
```rust

#![allow(unused_variables)]
fn main() {
unsafe trait Scary { }
}
```

4. And the fourth is for `impl`ementing one of those traits:

```rust

#![allow(unused_variables)]
fn main() {
unsafe trait Scary { }
unsafe impl Scary for i32 {}
}
```

### Mutable Static Variables

It is safe to read an immutable static variable:

```rust
static HELLO_WORLD: &str = "Hello, world!";

fn main() {
    println!("HELLO_WORLD: {HELLO_WORLD}");
}
```

However, since data races can occur, it is unsafe to read and write mutable static variables:

```rust
static mut COUNTER: u32 = 0;

fn add_to_counter(inc: u32) {
    unsafe {
        COUNTER += inc;
    }
}

fn main() {
    add_to_counter(42);

    unsafe {
        println!("COUNTER: {COUNTER}");
    }
}
```

### Unions

In Rust, a `union` is a type that allows you to store different types of data in the same memory location.

`Unions` are similar to `structs`, but they do not have a constructor and do not automatically implement any `traits`. Instead, they are used for low-level programming tasks where you need to manually manage the memory layout.

```rust
#[repr(C)]
union MyUnion {
    i: u8,
    b: bool,
}

fn main() {
    let u = MyUnion { i: 42 };
    println!("int: {}", unsafe { u.i });
    println!("bool: {}", unsafe { u.b }); // Undefined behavior!
}
```

### Unsafe Functions


```rust
unsafe fn dangerous_operation() {
    let mut num =  5;
    let r1 = &num as *const i32;
    let r2 = &mut num as *mut i32;

    unsafe {
        *r2 =  10;
        println!("r1 is: {}", *r1);
    }
}

fn main() {
    dangerous_operation();
}
```

Here, `dangerous_operation` is an unsafe function that creates a raw pointer to an integer and then modifies the value through the raw pointer.


### Implementing Unsafe Traits

Like with functions, We can mark a trait as `unsafe` if the implementation must guarantee particular conditions to avoid undefined behaviour.

```rust

use std::mem::size_of_val;
use std::slice;

/// ...
/// # Safety
/// The type must have a defined representation and no padding.
pub unsafe trait AsBytes {
    fn as_bytes(&self) -> &[u8] {
        unsafe {
            slice::from_raw_parts(
                self as *const Self as *const u8,
                size_of_val(self),
            )
        }
    }
}

// Safe because u32 has a defined representation and no padding.
unsafe impl AsBytes for u32 {}

fn main() {
    let value: u32 =  42;
    let bytes = value.as_bytes();
    println!("Bytes of u32: {:?}", bytes);
}
```


### Additional Resources
- [Google Comprehensive Rust Course](https://google.github.io/comprehensive-rust/)
- [Comprehensive Rust](https://github.com/google/comprehensive-rust)
- [Rust Documentation](https://doc.rust-lang.org/)
- [Cargo Guide](https://doc.rust-lang.org/cargo/)
- [Rust Testing](https://doc.rust-lang.org/book/ch11-00-testing.html)