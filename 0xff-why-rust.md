## (DRAFT) 0xff - Why Rust?

> TODO

* encourages functional programming
    * minimize mutations
    * minimize side effects
* iterator pattern (zero-cost abstraction)
* statically and strongly typed
* `Results` & `Option` instead of exceptions (errors are treated as values and are part of the type system)
* traits instead of classes
* no null
* enums with data attached (called custom types in elm)
* developer experience (package management, build system, compiler messages, rust-analyzer, clippy)
* everything is an expression (`if-else`)
* pattern matching
* ownership system (no garbage-collection)
* performance 

---

## ✅ Goals

The goal of this talk is to set the basis for the next weeks, where we take a deep dive into the Rust language.

* Overview of the language
    * What differentiates Rust from other mainstream languages?
    * Get familiar with the standard library - https://docs.rs/std
* Overview of ecosystem
    * Tooling - `rustc`, `cargo`, `rust-analyzer`, and `clippy`
    * Libraries (e.g. tokio) - https://crates.io
    * Where to find learning material - https://www.rust-lang.org/learn
    * How to read the documentation? - https://docs.rs

## 📝 Resources

Rust has extremly good documentation:

* Official Learning Material - https://www.rust-lang.org/learn
* The Rust Book - https://doc.rust-lang.org/book/
* The Rustling Course - https://github.com/rust-lang/rustlings/
* Rust by Example - https://doc.rust-lang.org/stable/rust-by-example/
* The Standard Library Prelude - https://doc.rust-lang.org/stable/std/prelude/
* Documentation of Rust crates - https://docs.rs/
* The Rust Language Cheat Sheet - https://cheats.rs/

## Features

Advantages of languages like Haskell, Rust, or Elm:

* These languages focus on reliability and long-term productivity
* Fully sound type system (type system is always right)
* Extremely good error messages
* No run-time exceptions (literally zero)
* Algebraic data types (Sum Types) + exhaustive pattern matching
* `Result` instead of exceptions (error unions)
* `Maybe`/`Option` instead of `null`
* Exceptional developer experience (language server and package management)
* You basically get tests for free (because of the type system)
* Very easy to refactor (the compiler gives you a lot of confidence)

Rust-specific advantages:

* Zero-cost abstractions - high-level constructs or compiled down high performance machine instructions (often not even heap allocation)
* Most performant language out there
* Extremely memory efficient
* Save concurrency
* Very well suited for backend or high-throughput applications
* Data is immutable by default (but you can opt-in)
* Runs everywhere (compiles to native and has best WebAssembly support)

## Is Rust a functional programming language

IMO, no! But it has a lot of features associated with functional languages like Haskell.

### What is functional programming?

Is a collection of loosely coupled ideas. Most common definition is:

* avoid mutation
* avoid side effects (pure functions)

But people also assosiate it with:

* strong type system
* pattern matching
* algebraic data types
* no shared state
* prefer expressions over statements
* no exceptions
* iterators - transports intent better than raw loops
* higher-order function (either receive a function as an argument or return a function)

### What Problem does functional programming solve?

A very common class of bugs is accidental mutation. Functional languages solve this by using persistent data structures (always copy). Rust solves the same problem with the so called ownership system.

## What does reliability mean?

The language helps you to write correct software

## What makes a programming language a good language?

1. Semantics - Quality of language - (see below)
2. Ergonomics - error messages, language support, linter, build system, package manager
3. Ecosystem - libraries, frameworks, templates, and tutorials,
4. Syntax - theoretically irrelevant and should be an editor setting in 2022

### What are good semantics?

IMO a good language should help you to avoid bugs. In a perfect world, a program which passes the compiler has no bugs.

Common classes of bugs:

* Runtime errors - can be fixed by a type system
* Data model errors (values which are valid according by type system but represent an impossible state) - can be often fixed by a sum type
* Accidental mutations - either fixed by functional programming (persistent data structures) or a borrow checker (Rust)
* Incorrectly implemented or flawed Business Logic - There is no help

## What differentiates Rust from other mainstream languages?

Python, Java, C#, JavaScript, C/C++, etc.

* Sum types
* Ownership system

## Sum Types

* They replace exceptions
* They replace `null`
* They help to make illegal states unrepresentable
* They are great in combination with exhaustive pattern matching

## Lifetimes

```rs
fn select<'a, 'b, 'c>(first: bool, a: &'a str, b: &'b str) -> &'c str
where
    'a: 'c,
    'b: 'c,
{
    if first {
        a
    } else {
        b
    }
}

fn main() {
    let longer = String::from("longer");
    {
        let shorter = String::from("shorter");

        let selected = select(true, &longer, &shorter);
        println!("the selected value was: {selected}");
    }
}
```