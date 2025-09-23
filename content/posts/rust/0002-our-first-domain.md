---
title: "Our First Domain: Project and Task"
date: 2025-09-22T21:38:33+07:00
draft: true
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



