# [Learn Rust - Day One](https://doc.rust-lang.org/book/title-page.html)
- `rustup` - install lastest and stble version of rust
- `rustup - update` update to lastest version of rust
- `rustc` - rust compiler
- `rustfmt <file-path>` to formate any rust file
- Cargo
  - `cargo new <project-name>` - create a new rust project/directory
  - `cargo init` - initalize a rust project
  - `cargo build` - compile and build project, and produce executable file (`.exe`)
  - `.\target\debug\<executable-name.exe>` - run executalbe
  - `cargo run` - compile and run the resultant executable at a time
  - `cargo check` build project without producing a binary to check for error. (run periodically)
  - `cargo build --release` - compile with optimization. Build for release

Workspace directory: [Hello Cargo](./hello_cargo/)