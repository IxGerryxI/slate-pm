# Slate PM — Database Schema

## Notes

- SQLite is used as the database engine
- Foreign keys must be enabled on every connection:
  PRAGMA foreign_keys = ON;

## Schema Intent

- Projects are top-level containers
- Tasks form a recursive tree structure under projects
- All task types (epic, task, subtask) share one unified table
- Backend is responsible for enforcing data consistency rules

## 1. Settings Table

A key-value store for user preferences (single-user system).

CREATE TABLE IF NOT EXISTS settings (
    key TEXT PRIMARY KEY,
    value TEXT NOT NULL
);

## 2. Projects Table

Top-level containers with specific workspace metadata.

CREATE TABLE IF NOT EXISTS projects (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    description TEXT,
    status TEXT DEFAULT 'active',
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

## 3. Tasks Table (Unified Node Hierarchy)

Supports epics, tasks, and subtasks in a single recursive structure.

CREATE TABLE IF NOT EXISTS tasks (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    project_id INTEGER NOT NULL,
    parent_id INTEGER DEFAULT NULL,
    type TEXT NOT NULL DEFAULT 'task',
    title TEXT NOT NULL,
    description TEXT,
    priority TEXT DEFAULT 'medium',
    status TEXT DEFAULT 'todo',
    sort_order INTEGER DEFAULT 0,
    due_date DATETIME DEFAULT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (project_id) REFERENCES projects(id) ON DELETE CASCADE,
    FOREIGN KEY (parent_id) REFERENCES tasks(id) ON DELETE CASCADE
);

## 4. Indexes

CREATE INDEX IF NOT EXISTS idx_tasks_project ON tasks(project_id);
CREATE INDEX IF NOT EXISTS idx_tasks_parent ON tasks(parent_id);

## Notes on Design

- Tasks use a recursive adjacency list model (parent_id)
- Deleting a project cascades all related tasks
- Deleting a task cascades all subtasks
- Sorting is handled via sort_order

## Timestamps

- created_at is set automatically on insert
- updated_at must be manually updated by the backend on every write operation