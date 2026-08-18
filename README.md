# JetPack Joyrider

An endless runner built in Unity as a self-imposed challenge: recreate the core loop of a classic mobile game from scratch, without a tutorial to follow.

The scope was intentionally limited to the base mechanics. Visually it diverges from the original — the source sprites were not available, so the art was replaced rather than copied.

---

## The core problem: difficulty as a system

The interesting part of this project isn't the player controller — it's `MapManager`, which acts as a **hazard director**. Instead of hardcoding a level, it decides at runtime what to spawn, when, and how punishing it should be.

Each hazard carries its own timing contract so that randomness stays fair:

- **Horizontal laser** — spawns and holds for a beat before activating, giving the player a window to escape.
- **Missile** — displays an incoming-missile warning, then fires after a short delay.
- **Bombs** — placed randomly, with a chance of spawning in clusters.
- **Vertical laser** — multiple variants with different behaviours.

The design rule throughout: every hazard telegraphs itself before it can kill. Randomness generates the challenge; the telegraph keeps a death feeling like the player's fault.

---

## Stack

| | |
|---|---|
| Engine | Unity 6000.0.48f1 |
| Language | C# |
| Rendering | Universal Render Pipeline (URP) |
| Input | Unity Input System |
| Persistence | PlayerPrefs |

---

## Architecture

```
Assets/Script/
├── MapManager.cs         # Hazard director: spawn timing, randomness, difficulty
├── PlayerScript.cs       # Player movement, stats and weapon handling
├── HUDManager.cs         # In-game HUD
├── Menu.cs               # Menu navigation
├── SaveManager.cs        # High-score persistence
└── Misc/
    ├── BackGroundScroller.cs   # Continuous background scroll
    ├── MissiileScript.cs       # Missile warning + launch
    └── SimpleLaserScript.cs    # Laser hazard behaviour
```

`SaveManager` is a singleton kept alive across scene loads via `DontDestroyOnLoad`, persisting the high score through `PlayerPrefs`.

Single scene: `Assets/Scenes/Game.unity`.

---

## Running locally

```bash
git clone https://github.com/EnzoGiacomini/JetPack-Joyrider-Clone.git
```

Open the folder through **Unity Hub** with editor version `6000.0.48f1`, then load `Assets/Scenes/Game.unity` and press Play.

---

## Roadmap

Planned but not implemented:

- [ ] Sound and music
- [ ] Boss encounters
- [ ] Separate endless and story modes

---

## Credits

Visual effects from the **JMO Assets** package.
