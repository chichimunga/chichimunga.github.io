---
{"type":["documentation"],"tags":["🌱"],"dg-publish":true,"created":"2026-04-07 16:59","modified":"2026-04-07 17:04","dg-path":"Godot/Concepts/Timers.md","permalink":"/Godot/Concepts/Timers/","dgPassFrontmatter":true,"dg-note-properties":{"type":["documentation"],"tags":["🌱"],"created":"2026-04-07 16:59","modified":"2026-04-07 17:04"}}
---


`Timer` is a node. Add it as a child, configure its duration in the Inspector, then start it in code. When it runs out it emits a `timeout` signal — connect that signal to a callback.

Common use: action cooldowns.

```gdscript
var can_laser: bool = true

func _process(delta):
    if Input.is_action_pressed("primary_action") and can_laser:
        can_laser = false
        shoot_laser()
        $PrimaryActionCooldown.start()  # Timer node set to 0.5s in Inspector

# Connected via Signals tab — fires when timer expires
func _on_primary_action_cooldown_timeout() -> void:
    can_laser = true
```
