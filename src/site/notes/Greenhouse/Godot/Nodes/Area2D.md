---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-02 13:31","modified":"2026-04-07 16:52","dg-path":"Godot/Nodes/Area2D.md","permalink":"/Godot/Nodes/Area2D/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-02 13:31","modified":"2026-04-07 16:52"}}
---


**Inheritance Chain** — [[Greenhouse/Godot/Nodes/Node\|Node]] → [[CanvasItem\|CanvasItem]] → [[Greenhouse/Godot/Nodes/Node2D\|Node2D]]

Invisible zone that detects when bodies enter or exit. Use for doorways, pickups, hazard zones, and triggers.

---

## Usage

1. Add `Area2D` → nest a `CollisionShape2D` inside it → define the shape
2. Select the `Area2D` → click the **Signals** tab → connect a signal
3. Godot auto-generates the callback in the attached script

```gdscript
func _on_area_entered(area):
    print("Something entered the area!")
```

## Properties & Methods

key props with types, useful methods with signatures.

## Gotchas

edge cases, common mistakes.
