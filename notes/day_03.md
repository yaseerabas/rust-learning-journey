# [Variables and Mutablity](https://doc.rust-lang.org/book/ch03-01-variables-and-mutability.html)

## variable with `let` keyword
Creating variable using the `let` keyword will be immutable by default.
```rust
fn main() {
    let age = 20;
    age = 21;
    println!("Age = {age}")

// error: cannot assign twice to immutable variable `age`
```
But you can make it mutable using `mut` keyword.
```rust
fn main() {
    let mut age = 20;
    age = 21;
    println!("Age = {age}")

// Output: Age = 21
```
Variables with `let` valid inside the block {} where it is defined.
Rust variables are immutable by default to make code safer and easier to understand.
If a value cannot change, Rust can prevent accidental modifications and catch more bugs at compile time. 

## Variables with `const` keyword
- Creating variable using the `const` keyword will be immutable by always. 
- These aren’t just immutable by default. They’re always immutable. 
- You can't use `mut` keyword with constants.
- The type of the value must be annotated.
- Can be declared in the global scope (outside of functions).

## Shadowing
You can declare a new variable with the same name as a previous variable.
```rust
fn main() {
    let age = 22;
    let age = 32 + age;
    println!("{age}")
}
```