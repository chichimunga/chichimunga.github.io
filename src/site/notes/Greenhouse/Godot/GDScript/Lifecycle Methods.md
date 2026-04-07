---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-06 12:52","modified":"2026-04-07 16:40","dg-path":"Godot/GDScript/Lifecycle Methods.md","permalink":"/Godot/GDScript/Lifecycle Methods/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-06 12:52","modified":"2026-04-07 16:40"}}
---


Scripts attach to a **Node** and become a class that inherits from it. Add via the green `+` icon in the script panel.

```gdscript
extends Sprite2D  # gives access to all Sprite2D properties and methods

func _ready():
    # Called once when the node is fully loaded
    pass

func _process(delta):
    # Called every frame — use for movement and game logic
    pass
```

## Delta Time

```gdscript
# delta = seconds since last frame → keeps speed consistent across frame rates

# ✅ Use delta for incremental movement
position.x += speed * delta

# ❌ Don't use delta when setting a fixed position
position.x = 100
```

## Vector2

```gdscript
# Represents positions, directions, movement in 2D
# Note: Y axis is flipped — positive Y points DOWN

Vector2(x, y)

Vector2.ZERO   # (0, 0)  — no movement
Vector2.ONE    # (1, 1)
Vector2.UP     # (0, -1)
Vector2.DOWN   # (0, 1)  
Vector2.LEFT   # (-1, 0)
Vector2.RIGHT  # (1, 0)
```

---

## Player Input

Setup: **Project → Project Settings → Input Map** → create actions (e.g. `left`, `right`, `up`, `down`) and assign keys.

```gdscript
# Check if an action is currently held
if Input.is_action_pressed("left"):
    pass

# Top-down movement — returns a normalized Vector2 from 4 directional actions
var direction = Input.get_vector("left", "right", "up", "down")
```

---
