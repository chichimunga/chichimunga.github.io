---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-02 13:31","modified":"2026-04-07 19:31","dg-path":"Godot/Nodes/RigidBody2D.md","permalink":"/Godot/Nodes/RigidBody2D/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-02 13:31","modified":"2026-04-07 19:31"}}
---


**Inheritance Chain** — [[Greenhouse/Godot/Nodes/Node\|Node]] → [[CanvasItem\|CanvasItem]] → [[Greenhouse/Godot/Nodes/Node2D\|Node2D]] → [[CollisionObject2D\|CollisionObject2D]] → [[PhysicsBody2D\|PhysicsBody2D]]

Moves via the physics engine: gravity, bouncing, friction, etc. Give it a starting velocity or force and Godot handles the rest. Use for grenades, falling objects, debris.

---

## Usage

Needs a [[Sprite2D\|Sprite2D]] child (visuals) and a [[CollisionShape2D\|CollisionShape2D]] child (collision).

Gravity defaults to `1`. You only need to provide an initial velocity. Physics takes over from there.

## Signals

### `body_entered(body: Node)`

Emits when a collision with another PhysicsBody2D or TileMap occurs.

### `body_exited(body: Node)`

Emits when the collision with another PhysicsBody2D or TileMap ends.
