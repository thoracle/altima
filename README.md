# ALTIMA

A single-file HTML5 role-playing game — an original homage to the classic
tile-based RPGs of the 1980s (Ultima IV in particular). All art, text, and
code are original. No dependencies, no build step, no server.

## Play

Open `index.html` in a browser, or serve it locally:

```sh
python3 -m http.server 8642
# then visit http://localhost:8642
```

Progress saves to the browser's localStorage (Shift+S to save).

## The quest

Master the Eight Virtues — Honesty, Compassion, Valor, Justice, Sacrifice,
Honor, Spirituality, Humility — through deeds, shrine meditation, and the
mantras taught by the folk of Albion. Each shrine sleeps until its hidden
**rune** is found (ask the folk about RUNE — they hide where their virtues
live). Raise all eight virtues to 80, pass the Trial of the Eight, and
become the **Saint**. The blind Seer of Souls in Castle Lumen will read
thy progress.

## Features

- Procedural overworld (fixed seed) with towns, castle, dungeons, shrines,
  moongates, and ship-only islands
- Keyword-based NPC dialogue (type NAME, JOB, MANTRA, ...)
- Roguelike bump combat everywhere: overworld, 3-level dungeons, and a
  dozen raid scenarios (pirate sieges, undead moongate incursions, shrine
  desecrations, a dragon that burns towns, a deck fight for a ghost ship,
  a whodunit in the castle court, and more)
- Naval play: capturable pirate ships, cannon broadsides, hull damage,
  krakens, a wandering whirlpool
- A bow for ranged attacks, and horses that halve overland travel
- Escalating threat systems, named bosses, two legendary items, and a
  final Trial against eight shadows of yourself

## Controls

| Key | Action |
|-----|--------|
| Arrows / WASD | move & bump-attack |
| T | talk (auto-targets a lone neighbor) |
| F | attack / fire cannons at sea |
| E | enter towns, dungeons, shrines; climb ladders |
| M | meditate at a shrine |
| G | open a chest |
| B / X | board or cross ships / go ashore |
| H | camp |
| Z | stats & proven mantras |
| Shift+S | save |
| ? | help |
