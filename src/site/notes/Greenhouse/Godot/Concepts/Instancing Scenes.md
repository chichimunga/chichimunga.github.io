---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-07 17:00","modified":"2026-04-07 17:04","dg-path":"Godot/Concepts/Instancing Scenes.md","permalink":"/Godot/Concepts/Instancing Scenes/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-07 17:00","modified":"2026-04-07 17:04"}}
---


To spawn objects at runtime (e.g. a laser when the player shoots), create a reusable scene then instantiate it in code.

## Setup

1. Create a new scene — add a root node, `Sprite2D`, and `CollisionShape2D`
2. Save it as a `.tscn` file

## Instancing in Code

```gdscript
# Preload the scene (runs once at startup)
var laser_scene: PackedScene = preload("res://scenes/Laser.tscn")

func _on_player_laser():
    var laser = laser_scene.instantiate()
    add_child(laser)  # adds it to the scene tree
```

`preload()` loads the scene at startup. `instantiate()` creates a new copy each time it's called.
