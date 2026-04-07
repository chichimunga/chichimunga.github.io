---
{"type":["documentation"],"dg-publish":true,"dg-hide":false,"created":"2026-04-04 21:36","modified":"2026-04-06 13:12","tags":["🌿"],"dg-path":"Godot/Nodes/Node.md","permalink":"/Godot/Nodes/Node/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"created":"2026-04-04 21:36","modified":"2026-04-06 13:12","tags":["🌿"]}}
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

---

## Usage

The base `Node` has no visual output — use it as a **scene root**, a **script container**, or an **organizational grouping** for other nodes.

**Common uses:**
- Root of a scene that doesn't need a transform or visual
- Attaching a script that manages child nodes (e.g. a `GameManager`)
- Grouping nodes logically without affecting position

---

## Properties & Methods

### Tree Navigation

#### Targeting Nodes

Several ways to reference a node in script. `$` is the most common in practice.

```gdscript
# $ shorthand — direct child by name
$Logo.rotation_degrees = 90

# path notation — navigate deeper into the tree
$Sprite2D/Arm/Hand
```

#### `get_node(path: NodePath) -> Node`

Navigates the scene tree by path. `$Sprite2D` is shorthand. Use for accessing known siblings or children.

```gdscript
# get a child by name
var sprite = get_node("Sprite2D")

# shorthand with $
var sprite = $Sprite2D
```

#### `get_children() -> Array[Node]`

Returns all direct children as an array. Use to loop over children dynamically.

```gdscript
# get all children of a marker container
var laser_markers = $LaserStartPositions.get_children()
```

---

### Tree Lifecycle

#### `add_child(node: Node)`

Attaches a node as a child. The most common way to spawn objects at runtime.

```gdscript
# instantiate a scene and add it to the tree
var laser = LaserScene.instantiate()
$Projectiles.add_child(laser)
```

---

## Gotchas

edge cases, common mistakes.
