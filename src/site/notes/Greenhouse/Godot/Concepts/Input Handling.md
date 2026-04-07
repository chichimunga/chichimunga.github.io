---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-04 22:30","modified":"2026-04-07 16:55","dg-path":"Godot/Concepts/Input Handling.md","permalink":"/Godot/Concepts/Input Handling/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-04 22:30","modified":"2026-04-07 16:55"}}
---


Setup: **Project → Project Settings → Input Map** → create actions (e.g. `left`, `right`, `up`, `down`) and assign keys.

## Actions

```gdscript
# Check if an action is currently held
if Input.is_action_pressed("left"):
    pass

# Top-down movement — returns a normalized Vector2 from 4 directional actions
var direction = Input.get_vector("left", "right", "up", "down")
```

## Mouse

```gdscript
# Rotate the node to face the mouse cursor
look_at(get_global_mouse_position())
```
