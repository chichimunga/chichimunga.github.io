---
{"type":["documentation"],"dg-publish":true,"dg-hide":false,"created":"2026-04-07 16:13","modified":"2026-04-07 16:24","tags":["🌿"],"dg-path":"Godot/Nodes/Properties & Methods.md","permalink":"/Godot/Nodes/Properties & Methods/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"created":"2026-04-07 16:13","modified":"2026-04-07 16:24","tags":["🌿"]}}
---


## Tree Navigation

### ```

---

## Tree Lifecycle

### `add_child(node: Node)`

Attaches a node as a child. The most common way to spawn objects at runtime.

```gdscript
# instantiate a scene and add it to the tree
var laser = LaserScene.instantiate()
$Projectiles.add_child(laser)
```
