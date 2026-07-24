# Rust Data Types — Beginner Notes

> **Source:** [The Rust Book — Chapter 3.2](https://doc.rust-lang.org/book/ch03-02-data-types.html)
> **Goal:** Understand the two main categories of data types in Rust — **scalar** and **compound** — with clear examples and visual explanations.

---

## Table of Contents

1. [Rust is Statically Typed](#1-rust-is-statically-typed)
2. [Scalar Types](#2-scalar-types)
3. [Compound Types](#3-compound-types)
4. [Quick Reference Cheatsheet](#4-quick-reference-cheatsheet)

---

## 1. Rust is Statically Typed

**What does "statically typed" mean?**
It means Rust must know the **type of every variable at compile time**. The compiler figures out the type automatically in most cases, but sometimes you must **tell Rust explicitly** what type you want.

### When to Write Type Annotations

```rust
// ✅ Rust infers: guess is a u32
let guess = "42".parse().expect("Not a number!");

// ❌ Error: Rust doesn't know which numeric type you want
let guess = "42".parse().expect("Not a number!");

// ✅ You must annotate explicitly
let guess: u32 = "42".parse().expect("Not a number!");
//          ^^^^ — tell Rust "I want an unsigned 32-bit integer"
```

### Why This Matters

```
┌──────────────────────────────────────────────────────┐
│  COMPILE TIME                                        │
│  Rust checks: "Does this variable have a type?"      │
│                       ✔️  Yes → Continue             │
│                       ❌ No  → Compiler Error         │
└──────────────────────────────────────────────────────┘
```

> **Tip:** Type annotations look like a colon `:` after the variable name, followed by the type: `let x: i32 = 5;`

---

## 2. Scalar Types

A **scalar type** represents a **single value**. Rust has four primary scalar types:

```
Scalar Types
├── 1. Integer Types       (whole numbers)
├── 2. Floating-Point Types (decimal numbers)
├── 3. Boolean Type        (true / false)
└── 4. Character Type      (single characters)
```

---

### 2.1 Integer Types

An **integer** is a whole number with no decimal point (e.g., `42`, `-7`, `0`).

#### Signed vs. Unsigned

| Term | Symbol | Can be negative? | Example |
|------|--------|------------------|---------|
| **Signed** | `i` | ✅ Yes | `i8`, `i16`, `i32`, `i64`, `i128` |
| **Unsigned** | `u` | ❌ No (always positive) | `u8`, `u16`, `u32`, `u64`, `u128` |

```
Positive numbers only:  u8  →  0 to 255
Can be negative:        i8  →  -128 to 127
```

#### Integer Types Table

| Size | Signed (`i`) | Unsigned (`u`) |
|------|-------------|---------------|
| 8-bit | `i8` | `u8` |
| 16-bit | `i16` | `u16` |
| 32-bit | `i32` | `u32` |
| 64-bit | `i64` | `u64` |
| 128-bit | `i128` | `u128` |
| Architecture-dependent | `isize` | `usize` |

> **`isize` / `usize`**: Size depends on your computer — 64-bit machine = 64 bits, 32-bit machine = 32 bits. Used mainly for indexing collections.

#### Default Integer Type

> **When in doubt, use `i32`** — it's Rust's default and is fast on most modern CPUs.

#### How to Write Integer Literals

| Literal Type | Example | Notes |
|-------------|---------|-------|
| Decimal | `98_222` | Use `_` as a thousands separator for readability |
| Hex | `0xff` | Base 16 |
| Octal | `0o77` | Base 8 |
| Binary | `0b1111_0000` | Base 2 |
| Byte (only for `u8`) | `b'A'` | ASCII byte value |

```rust
let decimal     = 98_222;       // easy to read!
let hex         = 0xff;         // 255 in decimal
let octal       = 0o77;         // 63 in decimal
let binary      = 0b1111_0000;  // 240 in decimal
let byte        = b'A';         // 65 in decimal (u8 only)
let with_suffix = 57u8;         // type suffix: 57 as u8
```

#### ⚠️ Integer Overflow — A Gotcha!

**What is it?**
If you store a value outside the type's range, overflow happens.

```rust
let mut x: u8 = 255;  // u8 max = 255
x = x + 1;            // ❗ Overflow! What happens?
```

**Two modes, two behaviors:**

| Mode | What Happens |
|------|-------------|
| **Debug build** | Program **panics** (crashes with error) |
| **Release build** (`--release`) | Wraps around (256 → 0, 257 → 1, etc.) |

> ⚡ **Don't rely on wrapping!** It's considered an error. Use standard library methods instead:
> - `wrapping_add()` — wrap explicitly
> - `checked_add()` — return `None` on overflow
> - `saturating_add()` — clamp to min/max

---

### 2.2 Floating-Point Types

A **floating-point** number has a decimal point (e.g., `3.14`, `-0.5`).

| Type | Size | Default? |
|------|------|---------|
| `f32` | 32 bits | No |
| `f64` | 64 bits | ✅ **Yes** (preferred on modern CPUs) |

```rust
let x = 2.0;      // ✅ f64 (default)
let y: f32 = 3.0; // ✅ f32 (explicit annotation)
```

> **Why `f64`?** On modern CPUs it's as fast as `f32` but with more precision.

---

### 2.3 Numeric Operations

Rust supports all basic math operators:

```rust
let sum       = 5 + 10;        // ➕ Addition
let diff      = 95.5 - 4.3;    // ➖ Subtraction
let product   = 4 * 30;        // ✖️ Multiplication
let quotient  = 56.7 / 32.2;   // ➗ Division
let truncated = -5 / 3;        // ➗ Division (truncates toward zero → -1)
let remainder = 43 % 5;        // 🔄 Remainder (modulo)
```

> **Note:** Integer division drops the fractional part (truncates toward zero).

---

### 2.4 Boolean Type

A **boolean** is the simplest type — only two possible values:

```rust
let t = true;              // ✅ inferred as bool
let f: bool = false;       // ✅ explicit annotation
```

**Primary use:** Controlling program flow with `if` statements.

```rust
if t {
    println!("It's true!");
}
```

---

### 2.5 Character Type (`char`)

A **`char`** represents a **single Unicode character** (not just ASCII!).

```rust
let c = 'z';                    // letter
let z: char = 'ℤ';              // Unicode letter
let emoji = '😻';               // Even emojis are valid chars!
```

#### Key Rules

- Use **single quotes** `' '` for `char`
- Use **double quotes** `" "` for `String` (different type!)
- `char` is **4 bytes** and can represent:
  - ASCII letters: `'A'`, `'x'`
  - Accented characters: `'é'`, `'ñ'`
  - Chinese/Japanese/Korean characters: `'中'`, `'あ'`
  - Emojis: `'🚀'`, `'💯'`

> **Note:** A "character" in Unicode is complex — Rust's `char` follows Unicode scalar values (U+0000 to U+D7FF and U+E000 to U+10FFFF).

---

## 3. Compound Types

Compound types **group multiple values into one type**.

```
Compound Types
├── 1. Tuple     (fixed-size, mixed types allowed)
└── 2. Array     (fixed-size, same type required)
```

---

### 3.1 Tuple

A **tuple** groups values of **different types** into one logical unit. **Fixed length** — cannot grow or shrink.

#### Creating a Tuple

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
//          ↑ type annotation  ↑ the tuple values
```

#### Destructuring a Tuple

"Pull apart" the tuple into individual variables:

```rust
let tup = (500, 6.4, 1);

let (x, y, z) = tup;  // destructuring

println!("The value of y is: {y}");  // y = 6.4
```

#### Accessing Tuple Elements by Index

Use a **dot `.`** followed by the **index** (0-based):

```rust
let tup = (500, 6.4, 1);

let five_hundred = tup.0;   // 500
let six_point_four = tup.1; // 6.4
let one = tup.2;            // 1
```

```
Index:    0       1      2
Value:   500    6.4      1
Type:   i32    f64      u8
```

#### The Unit Tuple `()`

An **empty tuple** is called **unit**. It represents:
- An empty value
- A function that returns nothing

```rust
let empty: () = ();  // unit
```

---

### 3.2 Array

An **array** holds multiple values of the **same type**. **Fixed length** — cannot grow or shrink.

#### Creating an Array

```rust
let a = [1, 2, 3, 4, 5];  // Rust infers type: [i32; 5]
```

#### When to Use an Array vs. Vector

| Feature | Array | Vector |
|---------|-------|--------|
| Fixed length | ✅ Yes | ❌ No (can grow/shrink) |
| Same type | ✅ Yes | ✅ Yes |
| Memory location | Stack | Heap |
| Flexibility | Low | High |

> **Use array** when you know the exact number of elements and it won't change (e.g., days of the week).
> **Use vector** when you need a dynamically growing list.

#### Declaring Array Type and Length Explicitly

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
//         ^^^^ 5 elements, all i32
```

#### Initialize with the Same Value

```rust
let a = [3; 5];  // [3, 3, 3, 3, 3]
//  ↑ value  ↑ count
```

#### Real-World Example: Days of the Month

```rust
let months = [
    "January",   "February", "March",    "April",
    "May",       "June",     "July",     "August",
    "September", "October",  "November", "December"
];
// Always 12 elements — perfect for an array!
```

#### Accessing Array Elements

```rust
let a = [1, 2, 3, 4, 5];

let first  = a[0];  // 1
let second = a[1];  // 2
```

#### ⚠️ Out-of-Bounds Access — Runtime Panic!

Rust **checks array indexes at runtime**. Accessing an invalid index causes a **panic** (crash):

```rust,ignore
let a = [1, 2, 3, 4, 5];
let element = a[10];  // ❌ Runtime panic!
                       // "index out of bounds: the len is 5 but the index is 10"
```

**Why can't the compiler catch this?**
Because the index often comes from **user input** at runtime — the compiler can't know what value it will be.

> 💡 This is Rust's **memory safety** in action. Many languages (C, C++) would silently access invalid memory — Rust refuses to do this.

---

## 4. Quick Reference Cheatsheet

### Scalar Types

| Type | Example | Description |
|------|---------|-------------|
| `i8` / `u8` | `42u8` | 8-bit integer |
| `i32` / `u32` | `42` | 32-bit integer (default) |
| `i64` / `u64` | `42i64` | 64-bit integer |
| `f32` | `3.14f32` | 32-bit float |
| `f64` | `3.14` | 64-bit float (default) |
| `bool` | `true` / `false` | Boolean |
| `char` | `'x'`, `'中'`, `'😻'` | Single Unicode character |

### Compound Types

| Type | Syntax | Mixed Types? |
|------|--------|-------------|
| Tuple | `(val1, val2, val3)` | ✅ Yes |
| Array | `[val1, val2, val3]` | ❌ No |

### Type Annotation Syntax

```rust
let x: i32  = 5;       // integer
let y: f64  = 3.14;    // float
let b: bool = true;    // boolean
let c: char = 'A';     // character
let t: (i32, f64) = (1, 2.0);  // tuple
let a: [i32; 3] = [1, 2, 3];   // array
```

---

## Key Takeaways

1. **Rust is statically typed** — types are resolved at compile time
2. **Scalar types** = single values: integers, floats, booleans, characters
3. **Compound types** = groups of values: tuples (mixed types), arrays (same type)
4. **Default integer = `i32`**, **default float = `f64`**
5. **Tuples** use `.index` or destructuring; **Arrays** use `[index]`
6. **Out-of-bounds array access causes a panic** — Rust protects you from memory errors

---

> **Next Steps:** Learn about [Control Flow](https://doc.rust-lang.org/book/ch03-05-control-flow.html) in Rust to see how these data types power conditionals and loops!