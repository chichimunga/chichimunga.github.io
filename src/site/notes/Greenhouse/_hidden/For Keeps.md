---
{"type":null,"tags":[],"dg-publish":true,"created":"2026-05-17 15:56","modified":"2026-05-17 16:09","dg-path":"_hidden/For Keeps.md","permalink":"/_hidden/For Keeps/","dgPassFrontmatter":true,"dg-note-properties":{"type":null,"tags":[],"created":"2026-05-17 15:56","modified":"2026-05-17 16:09"}}
---


## Marble Roguelite

### Concept

Marble roguelite/like game. Rings on the player's finger represent **static (passive) abilities** that persist through a run.

### Core Rules

- **Shooter rule:** the shooter marble may bounce off walls as many times as it wants, but once it hits another marble it cannot hit any more.
- **Overflick penalty:** flicking a marble too hard so that it flies off the board incurs a penalty.
- **Turn order:** each player rolls a d6 to determine who goes first. If tied, re-roll only enough to break the tie (force a non-tie). Leave the dice on the table once play starts so they become physical obstacles players must navigate around.

### Marble Properties / Variants

Each marble has a **fixed property** that determines how it reacts to collisions, scoring, etc.

#### Baseline Traits

- Weighted, lightweight, bouncy, hollow, magnetic
- Sizes: small, medium, large
- "Lopsided" property (rolls erratically)

#### Physics / Collision Marbles

- **Lead Core (Non-Elastic):** very high mass, near-zero restitution. Doesn't bounce — thuds and stops dead, transferring all energy to the victim.
- **Geode:** high mass, but brittle.
- **Moss Ball (Marimo):** absorbs momentum. When struck, barely moves and the striker stops dead.
- **Kinetic Adder:** adds kinetic energy to another marble it hits.
- **Energy Stealer:** steals kinetic energy from a marble it hits, then releases it after X *(define X — turns? hits? time?)*.
- **Pusher:** pushes other marbles away from it.
- **Time Bomb:** explodes after X turns.

#### Trail / Area Marbles

- **Slug (Trail Blazer):** leaves a "slime" trail (temporary 2D sprite / `Decal` on the board). Any marble entering the trail has its friction reduced to zero and slides uncontrollably.

#### Behavior / AI Marbles

- **Gyro (Auto-Correction):** constantly applies a tiny `CentralForce` toward the center of the ring. Cheat-y — fights momentum to stay in bounds.
- **Turbo:** apply a `ConstantForce` in the direction of movement.
- **Ghost:** passes through the first ball it hits.
- **Singularity Core:** doesn't need to hit other marbles — as it rolls past, it yanks them out of their path toward itself.
- **Ionized Striker (EMP):** on contact, applies a "Disable" state to the victim.
- **Cursed:** chaotic, moves unexpectedly.
- **D20 (Chaotic):** "spherical-ish," tumbles and stops on a face. Whichever face lands up gives a temporary buff to the next shot.
- **Jawbreaker:** every time it hits the ring boundary, it sheds a layer — changing color, becoming slightly smaller and faster.
- **Godot Robot Marble** *(concept — define behavior)*.

#### Trigger-condition Marbles

- **Four-Wall marble:** "If this marble hits all four walls in one throw…" *(finish the trigger — bonus damage? score multiplier? unlock?)*.

### Board / Spatial Mechanics

- **"Up your butt" safe pocket:** a designated safe pocket where a marble can be tucked away (presumably a recessed area on the board where the marble is protected from collisions).
- **Dice as obstacles:** the d6s rolled for turn order stay on the board as live obstacles.

### Roguelite / Meta-Progression

- **Between-run store:** spend in-game currency between runs to purchase items. Only a select number of marbles are available at a time; the inventory refreshes after every run.
- **Rings (passive abilities):** see Concept — rings worn on the finger function as static/passive ability slots that carry through a run.

### Godot / Dev Notes

- **Visual cues:** attach a `GPUParticles3D` node to special marbles to telegraph their power — e.g., faint blue glow for Magnetic, frosty mist for Chilled, etc.
- **Physics primitives referenced:** `restitution`, `CentralForce`, `ConstantForce`, `Decal`.
- **Tutorial:** [Create a 3D Marble Game in Godot 4 — Part 1: Getting Started (Beginner Tutorial)](https://www.youtube.com/watch?v=SdJplQOYXrs)

### Inspirations / References

- r/Marbles thread: <https://www.reddit.com/r/Marbles/s/eOS3dEgaHA>

### Open Questions / To Define

- Four-Wall marble: what's the payoff for hitting all four walls in one throw?
- Energy Stealer: what's the release condition — X turns, X hits, time-based?
- Time Bomb marble: how many turns is X, and is the timer visible to opponents?
- Godot Robot Marble: what is its behavior / property?
- How do rings (passive abilities) interact with marble properties? Stack? Override?
- Pocket mechanic: how does a marble get into / out of the "safe pocket"? Is it a one-time use?
