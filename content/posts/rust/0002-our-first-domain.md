---
title: "Our First Domain: Project and Task"
date: 2025-09-22T21:38:33+07:00
draft: false
---
Let's continue our learning process by create our first domain: **Project** and **Task**. 
# Requirement and Specification
Let's create the model first, and I will explain why we have to implement it based on the field it has. 

First, we are going to define the common requirement that going to be used across domain.

- The id of entity/model will using the `uuid` format
- Date and time is using `epoch` format, which is `i64` instead of specific DateTime type.

## Code
```rust
use serde::{Deserialize, Serialize};
use std::time::{SystemTime, UNIX_EPOCH};
use time::{OffsetDateTime, format_description};
use uuid::Uuid;

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct Project {
    pub id: Uuid,
    pub name: String,
    pub description: Option<String>,
    pub status: ProjectStatus,
    pub owner_id: Uuid,
    pub created_at: i64, 
    pub updated_at: i64,
    pub created_by: Uuid,
    pub updated_by: Uuid,
}

fn current_timestamp() -> i64 {
    SystemTime::now()
        .duration_since(UNIX_EPOCH)
        .expect("Time went backwards")
        .as_millis() as i64
}

impl Project {
    pub fn new(name: String, description: Option<String>, owner_id: Uuid, created_by: Uuid) -> Self {
        let now = current_timestamp();
        Self {
            id: Uuid::new_v4(),
            name,
            description,
            status: ProjectStatus::default(),
            owner_id,
            created_at: now,
            updated_at: now,
            created_by,
            updated_by: created_by,
        }
    }
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub enum ProjectStatus {
    Active,
    Archived,
    Completed,
}

impl Default for ProjectStatus {
    fn default() -> Self {
        ProjectStatus::Active
    }
}

#[derive(Debug, Clone, Serialize, Deserialize)]
pub struct Task {
    pub id: Uuid,
    pub title: String,
    pub description: Option<String>,
    pub status: TaskStatus,
    pub priority: TaskPriority,
    pub project_id: Uuid,
    pub assignee_id: Option<Uuid>,
    pub due_date: Option<i64>,
    pub created_at: i64,
    pub updated_at: i64,
    pub created_by: Uuid,
    pub updated_by: Uuid,
}

impl Task {
    pub fn new(
        title: String,
        description: Option<String>,
        project_id: Uuid,
        assignee_id: Option<Uuid>,
        due_date: Option<i64>,
        created_by: Uuid,
    ) -> Self {
        let now = current_timestamp();
        Self {
            id: Uuid::new_v4(),
            title,
            description,
            status: TaskStatus::default(),
            priority: TaskPriority::default(),
            project_id,
            assignee_id,
            due_date,
            created_at: now,
            updated_at: now,
            created_by,
            updated_by: created_by,
        }
    }
}

```
# What we learn

## use
The `use` keyword in Rust is used to bring items into scope from other modules or crates. In our code:

- `use serde::{Deserialize, Serialize};` - Imports serialization traits for converting structs to/from JSON
- `use std::time::{SystemTime, UNIX_EPOCH};` - Imports time-related functionality from standard library
- `use uuid::Uuid;` - Imports UUID generation capability from external crate

This helps us avoid writing full paths every time we need these items.

## struct
A `struct` defines a custom data type that groups related data together. Our `Project` and `Task` structs contain:

- **Fields**: Each field has a name and type (e.g., `id: Uuid`, `name: String`)
- **Derive macros**: `#[derive(Debug, Clone, Serialize, Deserialize)]` automatically implements common traits

## Visibility
The `pub` keyword controls the visibility of struct fields and functions in Rust:

- **Public fields**: `pub` makes fields accessible from outside the current module
- **Private by default**: Without `pub`, fields are only accessible within the same module
- **Encapsulation**: Controls which parts of your code can be accessed by other modules
- **API design**: Use `pub` for fields that should be part of your public interface

## Option<T>
`Option<T>` is Rust's way of handling values that might be present or absent (similar to nullable types in other languages):

- **Some(value)**: Contains a value of type `T`
- **None**: Represents the absence of a value
- **Null safety**: Prevents null pointer errors at compile time
- **Pattern matching**: Works great with `match` statements to handle both cases
- **Examples in our code**: `description: Option<String>`, `assignee_id: Option<Uuid>`

## impl of struct
The `impl` block allows us to define methods associated with a struct. It's where we add behavior to our data:

```rust
impl Project {
    pub fn new(...) -> Self { ... }
}
```

This creates a constructor method that returns a new instance of the struct with initialized values.

## "new" term
If you're familiar with Object-Oriented Programming, then this `new` function has a similar purpose. However, in Rust, `new` is just a **convention** (not a language keyword) for constructor functions that create and return a new instance of a struct.

- **Constructor pattern**: Creates and returns a new instance of the struct
- **Self**: Refers to the current struct type (`Project` in this case)
- **Initialization**: Sets default values and generates required fields like timestamps and UUIDs
- **Encapsulation**: Contains the logic for proper object creation

## enums
Enums define a type that can be one of several variants. Our examples:

- `ProjectStatus`: Can be `Active`, `Archived`, or `Completed`
- `TaskStatus` and `TaskPriority`: Similar concept for different categories

# Reference
- Rust Book: https://doc.rust-lang.org/book



