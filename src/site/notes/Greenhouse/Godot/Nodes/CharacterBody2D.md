---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-07","dg-path":"Godot/Nodes/CharacterBody2D.md","permalink":"/Godot/Nodes/CharacterBody2D/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-07"}}
---


**Inheritance Chain** — [[Greenhouse/Godot/Nodes/Node\|Node]] → [[CanvasItem\|CanvasItem]] → [[Greenhouse/Godot/Nodes/Node2D\|Node2D]] → [[CollisionObject2D\|CollisionObject2D]] → [[PhysicsBody2D\|PhysicsBody2D]]

The standard node for player-controlled characters.

--- Gives you full control over movement — unlike [[Greenhouse/Godot/Nodes/RigidBody2D\|RigidBody2D]], physics are not applied automatically.

## Usage

Needs a **Sprite2D** child (visuals) and a **CollisionShape2D** child (collision).

Uses `_physics_process` instead of `_process` to stay in sync with the physics engine.

```gdscript
extends CharacterBody2D

const SPEED = 200.0

func _physics_process(delta):
    var direction = Input.get_vector("left", "right", "up", "down")
    velocity = direction * SPEED
    move_and_slide()  # handles delta automatically
```

`move_and_slide()` moves the body and handles collisions — it adjusts velocity along slopes and walls automatically.

## Properties & Methods

key props with types, useful methods with signatures.

## Gotchas

edge cases, common mistakes.
