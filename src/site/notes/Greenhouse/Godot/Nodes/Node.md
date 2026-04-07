---
{"type":["documentation"],"tags":["🌿"],"dg-publish":true,"dg-hide":false,"created":"2026-04-04 21:36","modified":"2026-04-07 17:04","dg-path":"Godot/Nodes/Node.md","permalink":"/Godot/Nodes/Node/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌿"],"created":"2026-04-04 21:36","modified":"2026-04-07 17:04"}}
---


**Inheritance Chain** — [[Object\|Object]]

Nodes are the basic building blocks in Godot. There are dozens of different nodes to add images, sounds, timers, and more to your game. They can be nested within another node. This "tree" of nodes is called a **scene**.

**Different types of nodes:**

| Icon | Type          | Use                     |
| ---- | ------------- | ----------------------- |
| 🔵   | 2D nodes      | 2D games                |
| 🟦   | Control nodes | UI / layout             |
| 🟩   | 3D nodes      | 3D games                |
| ⚙️   | General nodes | utility / cross-context |

---

## Tree Navigation

### Targeting Nodes

Several ways to reference a node in script. `$` is the most common in practice.

```gdscript
# $Name — direct child by name
$Logo.rotation_degrees = 90

# path notation — navigate deeper into the tree
$Sprite2D/Arm/Hand
```

### `get_children() -> Array[Node]`

Returns all direct children as an array. Use to loop over children dynamically.

```gdscript
var laser_markers = $LaserStartPositions.get_children()
```

## Tree Lifecycle

### `add_child(node: Node)`

Attaches a node as a child. The most common way to spawn objects at runtime.

```gdscript
var laser = LaserScene.instantiate()
$Projectiles.add_child(laser)
```
