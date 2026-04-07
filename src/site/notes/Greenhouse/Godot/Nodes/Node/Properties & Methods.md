---
{"type":["documentation"],"dg-publish":true,"dg-hide":false,"created":"2026-04-07 16:13","modified":"2026-04-07 16:14","tags":["🌿"],"dg-path":"Godot/Nodes/Node/Properties & Methods.md","permalink":"/Godot/Nodes/Node/Properties & Methods/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"created":"2026-04-07 16:13","modified":"2026-04-07 16:14","tags":["🌿"]}}
---


## Tree Navigation

### Targeting Nodes

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

---

## Tree Lifecycle

### `add_child(node: Node)`

Attaches a node as a child. The most common way to spawn objects at runtime.

```gdscript
# instantiate a scene and add it to the tree
var laser = LaserScene.instantiate()
$Projectiles.add_child(laser)
```
