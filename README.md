# Nothing Is Real

**A race against an RL agent to open the door.**

*A Human vs RL Agent Puzzle Benchmark*

![status](https://img.shields.io/badge/status-in%20development-orange)
![python](https://img.shields.io/badge/python-3.10+-blue)
![phaser](https://img.shields.io/badge/game-Phaser.js-purple)
![license](https://img.shields.io/badge/license-MIT-green)

> 🎮 **Play:** *coming soon* · 🎬 **Demo video:** *coming soon* · 📄 **Report:** *coming soon*

---

## The idea

Every level is the same dark room. There is a door. It is locked.

But the way to open it is **different every time**. Sometimes you press a button. Sometimes you press it five times. Sometimes the button does nothing and the window on the wall was never a window at all.

You don't play alone. An **AI agent trained with reinforcement learning** takes turns with you in the same room. You get 3 tries each. Whoever opens the door first wins the level.

The catch: the agent has **never seen these levels before**. It didn't memorise the answers. It learned *how to figure out* a hidden rule by experimenting, the same thing you are doing.

So the real question is:

> **Can an AI learn new rules as fast as a human can?**

---

## How a round works

```
Level 7 · "Nothing is real..."

You   (try 1)  →  turn the knob ......... ❌
Agent (try 1)  →  press the button ...... ❌
You   (try 2)  →  stone on the button ... ✅  door opens!

Score: You 4 – 3 Agent
```

- Only one player is on screen at a time. The other watches from the side.
- Both players can see each other's failed attempts in the **"Tried" bar**, so you can learn from the agent's mistakes, and it can learn from yours.
- Every level has a one-line hint. It may help. It may lie.

---

## Features

**Game**
- Dark, hand-drawn style 2D puzzle platformer that runs in the browser
- Same room, a new hidden rule every level
- Twists like the **fake window** and **cursor tricks** (sometimes you have to grab the world with your mouse)
- Turn-based **Human vs AI** mode with a live scoreboard
- Agent "thought bubble" and match replays to see what the AI tried and why

**AI**
- Memory-based agent (**Recurrent PPO**) trained with meta-reinforcement learning
- Tested only on **unseen levels**, so it can't rely on memorisation
- Two agent versions for comparison:
  - 👀 **Watcher**: sees the other player's attempts
  - 🙈 **Blind**: sees only its own attempts

---

## Research questions

This project is a game on the outside and an experiment on the inside.

1. **Human vs AI:** How many attempts does a human need to discover a hidden rule, compared to an RL agent?
2. **Learning from others:** Does an agent that watches the other player's mistakes solve levels faster than one that doesn't? *(ablation: Watcher vs Blind)*
3. **Generalisation:** Can the agent handle trick types it only saw in different forms during training?
4. **Where humans win:** Which kinds of twists (language hints, fake objects, cursor tricks) are easy for people but hard for the agent?

Every match played in the browser is logged (anonymously) and used for the analysis.

---

## Door tricks (planned)

| # | Trick | How the door opens |
|---|-------|--------------------|
| 1 | Plain button | Press the button |
| 2 | Again and again | Press the button several times |
| 3 | Press harder | Land on the button from a high jump |
| 4 | Something heavy | Put the stone on the button |
| 5 | Ghost of a try | A previous attempt leaves something behind that helps |
| 6 | Not a window | The window is fake, interact with it |
| 7 | Grab the world | Drag an object with the mouse cursor |
| 8 | Patience | Do nothing and wait |

More tricks, and combinations of tricks, will be added later.

---

## Tech stack

| Part | Tools |
|------|-------|
| Environment & training | Python, Gymnasium, PyTorch, Stable-Baselines3 (`sb3-contrib` RecurrentPPO) |
| Game | Phaser.js (browser) |
| Agent in the browser | ONNX + onnxruntime-web (no server needed) |
| Level rules | Shared JSON files, read by both Python and JavaScript |
| Match data & leaderboard | Supabase / Firebase |
| Hosting | GitHub Pages |

**Design note:** every level's rules live in a single JSON file (for example, *"door opens when `stone` is on `button`"*). The Python training environment and the browser game read the same file, so the agent trains on exactly the game you play.

---

## Project structure (planned)

```
nothing-is-real-rl/
├── levels/          # level rules as JSON (shared by game + training)
├── env/             # Gymnasium environment (Python)
├── agent/           # training scripts, configs, ONNX export
├── game/            # Phaser.js browser game
├── analysis/        # notebooks and plots for human vs AI results
└── docs/            # report, figures, demo media
```

---

## Roadmap

- [ ] Define level rule format (JSON) and the first 8 tricks
- [ ] Build the Python environment (no graphics)
- [ ] Train the first agent and test on unseen levels
- [ ] Build the browser game with placeholder graphics
- [ ] Run the trained agent in the browser (ONNX)
- [ ] Human vs Agent turn system + scoreboard + "Tried" bar
- [ ] Art, animation and sound
- [ ] Watcher vs Blind agent experiment
- [ ] Collect human matches and publish results
- [ ] Demo video and short report

---

## Inspiration

The "same room, new rule" idea is inspired by the mobile puzzle game *That Level Again* by IamTagir. **Nothing Is Real** is an original project: its levels, art, characters and twists are its own, and its focus is the human vs AI learning experiment.

---

## License

[MIT](LICENSE). Feel free to read, learn from and build on this code.

---

## Author

Made by [@Aishwaryasrivastav31](https://github.com/Aishwaryasrivastav31).
Questions, ideas or a level you think the agent can't solve? Open an issue.
