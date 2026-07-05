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

- Procedural overworld (fixed seed) with six towns, a castle, dungeons,
  shrines, and ship-only islands
- Eight moongates ruled by two moons: silver Argent's phase opens a
  gate, dark Umbra's phase chooses where it leads
- Original chiptune score — eight themes: overworld, town, castle,
  dungeon, sea, shrine hymn, battle, and a death dirge
  (V toggles music)
- Living towns: every villager keeps a daily agenda — working by day,
  drinking in the tavern by evening, asleep in a real bed at night
  (shops keep hours; guards, healers, and pirates never rest)
- IM-style dialogue: topics, shop wares, and yes/no questions appear
  as clickable reply chips (numbers and free typing still work) —
  secrets still hide behind unlisted words, and the folk greet a
  Paragon differently than a Stranger
- Roguelike bump combat everywhere: overworld, 5-level dungeons (each
  with a scripted vault on the third floor, where a named warden and
  its retinue guard the only ladder down), and a
  dozen raid scenarios (pirate sieges, undead moongate incursions, shrine
  desecrations, a dragon that burns towns, a deck fight for a ghost ship,
  a whodunit in the castle court, and more)
- Nine magic relics with passive powers (regeneration, poison immunity,
  a death-cheating ankh...) hidden at the bottoms of the dungeons and in
  the spoils of the hardest raids — guarded by wraiths, basilisks, and
  demons in the deep dark
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
| P | peer at the world map (fog of war) |
| Z | stats & proven mantras |
| V | toggle music |
| Shift+S | save |
| ? | help |
