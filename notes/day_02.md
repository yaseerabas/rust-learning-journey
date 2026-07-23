# [Learn Rust - Day Two](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html)
## Guessing Game

Today I learned how to build a simple number guessing game in Rust while becoming familiar with the language's core concepts and development workflow.

Key concepts I learned
- Creating a Rust project using Cargo (`cargo new`) and running it with `cargo run`.
- Using variables with let and understanding mutability through `mut`.
- Reading user input from the terminal using `std::io`.
- Working with strings, particularly `String`, and storing user input.
- Handling errors using Result and the `expect()` method for simple error handling.
- Generating random numbers by adding the `rand` **crate** as a dependency in `Cargo.toml`.
- Converting data types, such as parsing a string into an integer with `parse()`.
- Using pattern matching with match to handle successful and failed parsing.
- Comparing values using the `cmp()` method and the `Ordering` enum (Less, Greater, Equal).
- Creating loops with `loop` to repeatedly ask the user for input until the correct guess is entered.
- Managing dependencies with Cargo and understanding how external crates are integrated into a Rust project.

What I built
I built a command-line guessing game that:
1. Generates a random secret number.
2. Prompts the user to enter a guess.
3. Validates and parses the input.
4. Compares the guess with the secret number.
5. Prints whether the guess is too low, too high, or correct.
6. Repeats until the correct number is guessed.

Main takeaway
This chapter introduced the fundamentals of Rust programming through a practical project. I gained experience with variables, user input, error handling, pattern matching, loops, external crates, and Cargo—the essential building blocks needed to write more complex Rust programs.

Workspace directory: [Guessing Game](./guessing_game/)