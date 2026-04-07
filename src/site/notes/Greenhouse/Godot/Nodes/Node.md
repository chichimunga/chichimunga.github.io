---
{"type":["documentation"],"dg-publish":true,"dg-hide":false,"created":"2026-04-04 21:36","modified":"2026-04-07 16:23","tags":["🌿"],"dg-path":"Godot/Nodes/Node.md","permalink":"/Godot/Nodes/Node/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"created":"2026-04-04 21:36","modified":"2026-04-07 16:23","tags":["🌿"]}}
---


**Inherits** — [[Object\|Object]]

Nodes are the basic building blocks in Godot. There are dozens of different nodes to add images, sounds, timers, and more to your game. They can be nested within another node. This "tree" of nodes is called a **scene**.

**Different types of nodes:**

| Icon | Type          | Use                     |
| ---- | ------------- | ----------------------- |
| 🔵   | 2D nodes      | 2D games                |
| 🟦   | Control nodes | UI / layout             |
| 🟩   | 3D nodes      | 3D games                |
| ⚙️   | General nodes | utility / cross-context |

## Targeting Nodes

Several ways to reference a node in script. `$` is the most common in practice.

```gdscript
# $ shorthand — direct child by name
$Logo.rotation_degrees = 90

# path notation — navigate deeper into the tree
$Sprite2D/Arm/Hand
```

### `get_node(path: NodePath) -> Node`

Navigates the scene tree by path. `$Sprite2D` is shorthand. Use for accessing known siblings or children.

```gdscript
# get a child by name
var sprite = get_node("Sprite2D")

# shorthand with $
var sprite = $Sprite2D
```

### `get_children() -> Array[Node]`

Returns all direct children as an array. Use to loop over children dynamically.

```gdscript
# get all children of a marker container
var laser_markers = $LaserStartPositions.get_children()

```
