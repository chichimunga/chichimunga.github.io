---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-04 22:29","modified":"2026-04-07 16:57","dg-path":"Godot/Concepts/GDScript Basics.md","permalink":"/Godot/Concepts/GDScript Basics/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-04 22:29","modified":"2026-04-07 16:57"}}
---


GDScript is Python-like and uses indentation for structure. It's built into Godot — no imports needed for engine types.

## Variables

```gdscript
var speed = 200          # inferred type
var speed: float = 200   # explicit type
const MAX_SPEED = 500    # constant — cannot be reassigned
```

### Exported Variables

`@export` exposes a variable to the Godot Inspector, letting you set values without editing code.

```gdscript
@export var speed: float = 200
@export var jump_height: int = 300
```

## Functions

```gdscript
func move(direction: Vector2) -> void:
    position += direction * speed

func get_health() -> int:
    return health
```

- `->` declares return type, `void` means no return value
- All functions are public by default

## If / Else

```gdscript
if health <= 0:
    die()
elif health < 20:
    play_low_health_sound()
else:
    pass
```

## Loops

```gdscript
# for loop over a range
for i in range(5):       # 0, 1, 2, 3, 4
    print(i)

# for loop over an array
for item in inventory:
    print(item)

# while loop
while health > 0:
    take_damage()
```

## Arrays

```gdscript
var inventory = ["sword", "shield", "potion"]

inventory.append("arrow")       # add to end
inventory.erase("potion")       # remove by value
inventory.size()                # length
inventory[0]                    # access by index
```

## Dictionaries

```gdscript
var stats = {
    "health": 100,
    "speed": 200
}

stats["health"]          # access
stats["mana"] = 50       # add or update
stats.has("speed")       # check key existence
```

## Common Built-in Types

| Type | Example | Notes |
| ---- | ------- | ----- |
| `int` | `42` | whole numbers |
| `float` | `3.14` | decimal numbers |
| `bool` | `true` / `false` | |
| `String` | `"hello"` | double quotes |
| `Vector2` | `Vector2(x, y)` | 2D position/direction |
| `Array` | `[1, 2, 3]` | ordered list |
| `Dictionary` | `{"key": value}` | key-value pairs |

## Gotchas

**Indentation is syntax** — mixing tabs and spaces causes errors. Godot uses tabs by default.

**Integer division truncates** — `5 / 2` returns `2`, not `2.5`. Use `5.0 / 2` to get a float.

**`null` comparisons** — use `== null` not `is null`. `is` checks type, not value.

**Strings are not implicitly cast** — `"Score: " + score` errors if `score` is an int. Use `str(score)` or string formatting:

```gdscript
"Score: %d" % score
"Score: " + str(score)
```

**`@export` requires a type hint** to show the correct widget in the Inspector. Without it, Godot falls back to a generic field.
