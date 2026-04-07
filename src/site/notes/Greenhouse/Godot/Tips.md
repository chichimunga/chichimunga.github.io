---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-07","dg-path":"Godot/Tips.md","permalink":"/Godot/Tips/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-07"}}
---


## Editor

- **Change a node's type** after creation: right-click it in the Scene panel → "Change Type"
- **View built-in docs:** `Cmd`/`Ctrl` + click any class or method in the script editor
- **Remote tab** (Scene panel) — only visible while the game is running. Shows all active nodes in the scene tree. Useful for debugging live state.

## Project Settings

- **Window size:** Project → Project Settings → Displays → Window → set Viewport Width and Height

## Scene Structure

Standard 2D physics node layout:

```
PhysicsBody (e.g. CharacterBody2D)
├── Sprite2D        ← visuals
└── CollisionShape2D ← collision
```
