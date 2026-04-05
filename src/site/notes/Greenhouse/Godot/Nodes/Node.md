---
{"type":["documentation"],"dg-publish":true,"dg-hide":false,"created":"2026-04-04 21:36","modified":"2026-04-05 16:04","tags":["🌿"],"dg-path":"Godot/Nodes/Node.md","permalink":"/Godot/Nodes/Node/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"created":"2026-04-04 21:36","modified":"2026-04-05 16:04","tags":["🌿"]}}
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

### Lifecycle

Lifecycle callbacks to override in script:

```gdscript
# called once when node enters the scene tree
func _ready():

# called every frame
func _process(delta)

# called every physics tick:
func _physics_process(delta):
```

---

## Properties & Methods

### Properties

#### `name: StringName`

The node's name as it appears in the scene tree. Use when you need to identify or find a node by name, or set it dynamically at runtime.

```gdscript
# print this node's name
print(self.name)

# rename a child node
$Enemy.name = "Boss"
```

#### `owner: Node`

The scene root that "owns" this node — typically set automatically when a scene is saved. Useful when instancing scenes and need to know the root.

```gdscript
# print the name of the owning scene root
print(self.owner.name)
```

#### `process_mode: ProcessMode`

Controls whether `_process` and `_physics_process` run when the game is paused. Use this to keep UI or menus running while gameplay is frozen.

```gdscript
# run even when the game is paused
process_mode = Node.PROCESS_MODE_ALWAYS

# never run _process or _physics_process
process_mode = Node.PROCESS_MODE_DISABLED
```

---

### Tree Navigation

#### Targeting Nodes in Code

Several ways to reference a node in script, from simple to flexible. `$` and `%` are the most common in practice.

```gdscript
# $ shorthand — direct child by name
$Logo.rotation_degrees = 90

# path notation — navigate deeper into the tree
$Sprite2D/Arm/Hand

# % prefix — unique name, reachable from anywhere in the scene
# (right-click a node in the editor → "Access as Unique Name" to enable)
%HUDLabel.text = "Score: 0"

# .. goes up one level — access a parent's data from a child script
$"..".health
```

#### `get_node(path: NodePath) -> Node`

Navigates the scene tree by path. `$Sprite2D` is shorthand. Use for accessing known siblings or children.

```gdscript
# get a child by name
var sprite = get_node("Sprite2D")

# shorthand with $
var sprite = $Sprite2D

# go up to parent, then down to a sibling
var hud = get_node("../HUD")
```

#### `find_child(pattern: String) -> Node`

Searches descendants by name pattern (supports wildcards). Use when you don't know the exact path.

```gdscript
# find by exact name
var hp_bar = find_child("HealthBar")

# find by wildcard pattern
var any_label = find_child("*Label*")
```

#### `get_parent() -> Node`

Returns the parent node. Use when a child needs to communicate upward without a direct reference.

```gdscript
# call a method on the parent
var parent = get_parent()
parent.take_damage(10)
```

#### `get_child(idx: int) -> Node`

Returns a child by its index in the tree. Useful when iterating or when you know the order.

```gdscript
# get the first child
var first = get_child(0)
```

#### `get_children() -> Array[Node]`

Returns all direct children as an array. Use to loop over children dynamically.

```gdscript
# hide every direct child
for child in get_children():
    child.hide()
```

---

### Tree Lifecycle

#### `add_child(node: Node)`

Attaches a node as a child. The most common way to spawn objects at runtime.

```gdscript
# instantiate a scene and add it to the tree
var bullet = BulletScene.instantiate()
add_child(bullet)
```

#### `remove_child(node: Node)`

Detaches a child from the tree without freeing it. Use when you want to temporarily hide or reuse a node.

```gdscript
# detach $Sword — it stays in memory but leaves the tree
remove_child($Sword)
```

#### `is_inside_tree() -> bool`

Returns whether the node is currently part of the active scene tree. Use before calling tree-dependent methods on nodes that may have been freed.

```gdscript
# guard against calling tree methods on a detached node
if is_inside_tree():
    get_tree().change_scene_to_file("res://Level2.tscn")
```

#### `queue_free()`

Marks the node for deletion at the end of the current frame. The safe way to destroy nodes — avoids errors from freeing mid-frame.

```gdscript
# destroy this node
queue_free()

# destroy a child node
$Explosion.queue_free()
```

---

### Scene & Groups

#### `get_tree() -> SceneTree`

Returns the active `SceneTree`. Use to change scenes, pause the game, or access groups.

```gdscript
# pause the game
get_tree().paused = true

# switch to a different scene
get_tree().change_scene_to_file("res://Menu.tscn")

# call a method on all nodes in a group
get_tree().call_group("enemies", "disable")
```

#### `add_to_group()` / `is_in_group()`

Groups let you tag nodes and call methods or send signals to all of them at once. Useful for enemies, collectibles, or any category of objects.

```gdscript
# tag this node as an enemy
add_to_group("enemies")

# check group membership before acting
if is_in_group("enemies"):
    take_damage(5)

# call freeze() on every node in the group
get_tree().call_group("enemies", "freeze")
```

---

## Gotchas

edge cases, common mistakes.
