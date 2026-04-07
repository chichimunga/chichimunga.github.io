---
{"type":["documentation"],"tags":["🌿"],"dg-publish":true,"created":"2026-04-04 22:29","modified":"2026-04-07","dg-path":"Godot/Concepts/Signals.md","permalink":"/Godot/Concepts/Signals/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌿"],"created":"2026-04-04 22:29","modified":"2026-04-07"}}
---


Signals fire when something happens to a node — a body enters an area, a timer expires, a collision occurs. They're Godot's event system.

## Built-in Signals

1. Create an `Area2D` → nest a `CollisionShape2D` inside → define the shape
2. Select the `Area2D` → click the **Signals** tab (above Inspector) → connect a signal
3. Godot auto-adds the callback function to the attached script

## Custom Signals

Built-in signals only work between nodes in the same scene. Custom signals allow communication across scenes.

**Problem:** A `Gate` node needs to notify its parent `Level` when the player enters. But from inside `Gate`, you can't directly reference `Level` or sibling nodes.

```
Level
├── Player
└── Gate
```

**Solution:** Define a custom signal in `Gate` and emit it. Then connect it from `Level`.

```gdscript
# Gate.gd
extends StaticBody2D

signal player_entered_gate

func _on_area_2d_body_entered(_body):
    player_entered_gate.emit()
```

In the `Level` scene, select `Gate` → Signals tab → double-click `player_entered_gate` to connect it:

```gdscript
# Level.gd
extends Node2D

func _on_gate_player_entered_gate():
    print("Player has entered the gate")
```
