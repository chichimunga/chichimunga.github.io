---
{"type":null,"dg-publish":true,"created":"2026-04-04 22:29","modified":"2026-04-05 07:42","topic":null,"subtopic":null,"tags":["🌳"],"permalink":"/Greenhouse/Godot/Concepts/Global Variables (Autoloads)/","dgPassFrontmatter":true,"dg-note-properties":{"type":null,"created":"2026-04-04 22:29","modified":"2026-04-05 07:42","topic":null,"subtopic":null,"tags":["🌳"]}}
---


You create a script and register it as an Autoload (singleton) — Godot instantiates it once at startup and it persists across all scenes.

**Setting one up:**

1. Create a script, e.g. `Global.gd`
2. Project → Project Settings → Autoload → add your script
3. Give it a name (e.g. `Global`)

**Accessing it from anywhere:**

```gdscript
Global.score += 1
Global.player_health = 100
```

---

In your Godot project, typically at the root level:

```js
res://
├── Global.g
├── Main.tscn
├── Player.gd
└── …
```

Some people organize it into a folder:

```js
res://
└── autoloads/
    └── Global.gd
```

Either works — Godot doesn't enforce a location. The root is most common for small projects, `autoloads/` folder is cleaner as the project grows.

---

## Common Use Cases

- Game state (`score`, `level`, `lives`)
- Player data that persists between scenes
- Settings (volume, difficulty)
- Scene management / transitions

---

## Gotcha

Don't overuse Autoloads — it's tempting to dump everything in there but it makes code hard to follow. Good rule of thumb: only put data or systems that **genuinely need to be accessed from multiple unrelated scenes**.

For data that only one scene or node needs, keep it local to that node.

according to how i have Greenhouse organized, Where should a note titled Global Variables be placed?

Based on your structure, it should go in:

**`Greenhouse/Godot/`**

Since you have `Greenhouse/Godot/Nodes/` for node-specific notes, Global Variables is a Godot concept but not a node — it sits at the Godot level, not inside Nodes.

could it be in a concepts folder? are there enough notes to fill that folder up?

Yes, a `Concepts` folder makes sense. And there are plenty of Godot concepts that aren't nodes:

- Global Variables (Autoloads)
- Signals
- Scene Tree
- Groups
- Resources vs Nodes
- GDScript basics (typing, functions, loops)
- Export variables
- Input handling
- Physics layers & masks
- Game loop (process vs physics_process)
- Tween
- State machines

That's easily 10+ notes without trying hard. `Greenhouse/Godot/Concepts/` works well alongside `Greenhouse/Godot/Nodes/`.
