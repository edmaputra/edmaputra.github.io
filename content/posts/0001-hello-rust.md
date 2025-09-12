---
date: '2025-09-12T17:15:24+07:00'
draft: true
title: 'Hello Rust !'
showToc: true
---
In this page, I want to share about the progress on how I learn a new programming language called **Rust**.
> Follow the installation in this link: [Rust Official Page](https://www.rust-lang.org/)

# Code Repository
I think one of the best way to learn is create a project with Rust. So, I will use this repository to store the code and history of it.

[Nukar - Github Repository](https://github.com/edmaputra/nukar)

Let's name the application with **Nukar**. I will explain what does it mean on the different opportunity, if any. With this project, we are going to make **Point-Of-Sales (POS)** system. 

# Initialize the Project
I will clone it in my machine and init the project for Rust by execute this command:
```
cargo init
```
The cargo create files and directory with the following structure:
```
project-root/
├── src/
│   └── main.rs
└── Cargo.toml
```
# Project Information
Let's go to the `cargo.toml`. In the first step, we are going to:
1. Name the project
2. Set the version
3. Set the edition 
The `cargo.toml` will look like this:
```toml
[package]
name = "nukar"
version = "0.1.0"
edition = "2024"

[dependencies]
```
# References
- [Rust Official Page](https://www.rust-lang.org/)