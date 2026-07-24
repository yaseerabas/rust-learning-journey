# [Data Types](https://doc.rust-lang.org/book/ch03-02-data-types.html)
- Rust is a **statically typed language** (must know the data type at compile time)
- There are *two* types of data in rust:
## Scalar Types
- A scalar type represents a single value.
- Rust has *four* primary scalar types:
### Integers
- An integer is a number without fractional component.
- There are *two categories* of integer types:
#### Signed
- Represent with `i`, and can be negative
- `i32` is Rust default
- Signed variant can store numbers from `-(2{n-1})` to `2{n-1} - 1`
- `i8` can store number from -128 to 127
#### Unsigned
- Represent with `u`, and always postive/zero
- Unsigned variants can store numbers from 0 to `2{n − 1}`
- `u8` can store numbers from 0 to 28 − 1, which equals 0 to 255.

> The `isize` and `usize` types depend on the architecture of the computer your program is running on: 64 bits if you’re on a *64-bit architecture* and 32 bits if you’re on a *32-bit architecture*.
### Floating-Point Numbers
- Floating-Point Numbers are numbers with decimal points.
- Rust’s floating-point types are `f32` and `f64`
- The default type is `f64` because on modern CPUs, it’s roughly the same speed as `f32` but is capable of more precision. 
- All floating-point types are **signed**.
- Example:
```rust
fn main() {
    let x = 2.0; // f64 (Infer automatically)

    let y: f32 = 3.0; // f32
}
```
### Booleana
- Booleans are primarily two possible values, i.e., `true` or `false`.
- These are one byte in size
- Specified using `bool`
- Example:
```rust
fn main() {
    let t = true;

    let f: bool = false; // with explicit type annotation
}
```
### Characters
- Unlike string literals, we use `char` to store a single character.
- `char` type is 4 bytes in size
- Represent a lot more than just ASCII (Unicode scalar value).
- Example:
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```
## Compound Types
- Compound types can group multiple values into one type. 
- Rust has two primitive compound types: tuples and arrays.
### Tuple Type
- Used to store multiple values with varity of types into a single variable.
- Tuples have fix length and it is immutable (can't grow or shrink in size)
- Example:
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
- Direct element access through index:
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
- Decunstructing a Tuple:
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```
- Using `()`, we can declear an empty tuple
### Array Type
- Another method to store multiple values within a single variable.
- Unlike Tuple, every element of array must have same data type
- It also have fix lenght
- Declearing an array:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```
- Array syntax:
```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```
Here, `i32` is the type of each element, and `5` is the length of the array
- You can **access any element of an array** using indexing:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

> You can read more about Data types in [Data Types Notes](./notes/rust-data-types-notes.md) comperehensivly
---