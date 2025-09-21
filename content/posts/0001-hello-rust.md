---
date: '2025-09-12T17:15:24+07:00'
draft: false
title: 'Hello Rust !'
showToc: true
---
As I mention on my previous post, this blog will contains the documentation or progress of my learning process. Right now, the **Rust programming language** is attracting my attention, so I want to start a project with it. 

The posts would be posted continuously, according on how far the project would be grow. I intent to use the posts as my design right before I implement them to code.

> Follow the installation in this link: [Rust Official Page](https://www.rust-lang.org/)

# Code Repository
I think one of the best way to learn is create a project with Rust. So, I will use this repository to store the code and history of it.

[Ilm - Github Repository](https://github.com/edmaputra/ilm)

With this project, we are going to make **Project Management** system, and it's trying to do what Jira can do. And if possible, we are going to improve and some special features to it.

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
name = "ilm"
version = "0.1.0"
edition = "2024"

[dependencies]
```
# References
- [Rust Official Page](https://www.rust-lang.org/)