---
name: "guidelines-reference"
description: "Navigate and use the project's .guidelines/ directory — find the right guideline for any task"
domain: "project-conventions"
confidence: "high"
---

## Context

Every project using this squad has a `.guidelines/` directory at the repo root. This is the single source of truth for all coding conventions, patterns, and rules specific to the project.

Before starting any task, **read `.guidelines/index.md` first** — it maps every available guideline to its domain and file path.

## How to Use Guidelines

1. **Open `.guidelines/index.md`** — this is the master navigation. It tells you what guidelines exist and where they are.
2. **Find the relevant section** for your task domain (frontend, backend, features, deployment, etc. — whatever this project defines).
3. **Read that file** before writing any code.
4. If no guideline exists for your topic → check `.guidelines/index.md` for the closest related one, or ask the coordinator before proceeding.

## Rules

- Never invent a convention without checking `.guidelines/` first.
- If a guideline is missing or outdated → flag it to the coordinator. Do not silently work around it.
- Guidelines take precedence over general best practices when they conflict.
