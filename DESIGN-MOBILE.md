# ALTIMA Mobile — UI Design

Target: playable one-handed on iPhone/Android portrait, no keyboard ever
required. Desktop keys keep working (one codebase, responsive).

## Guiding principles

1. **Touch is the native input, not a shim.** Ultima VI/VII were
   mouse-driven; tap-to-act is the modern heir. No memorizing keys.
2. **One smart button beats ten dumb ones.** The game already knows what
   E/G/M/B would do on any tile ("press E to enter") — surface that as a
   single context-labeled action button.
3. **Chips already won.** The dialogue chip system is fully touch-ready;
   the mobile design extends its philosophy to movement and commands.

## Layout (portrait)

```
┌─────────────────────────┐
│ HP ███████░ 178   ⛁146  │  ← mini-HUD strip (tap = stats drawer)
│ 🍞 42   MASTER OF VALOR │
├─────────────────────────┤
│                         │
│                         │
│      game canvas        │  ← 100vw, square, pixelated,
│      (13×13 view)       │     integer-scaled
│                         │
│                         │
├─────────────────────────┤
│ log (3-4 lines, larger  │
│ font, scrollable)       │
│ [JOB] [BUY] [RATS] [BYE]│  ← chips as-is
├─────────────────────────┤
│ [🗺]  [ ENTER MOONHAVEN ]  [⚔] │  ← bottom bar, thumb zone
└─────────────────────────┘
```

- **Mini-HUD**: HP bar, gold, food, title. Tapping it (or swiping from
  the right edge) opens the full stats/virtues panel as a slide-over
  drawer. Critical alerts (⚠ starving, shrine defiled) inline.
- **Canvas**: `width:100vw; max-width:100vh` with
  `image-rendering:pixelated`; scale to integer multiples when possible
  to keep pixels crisp. `touch-action:none` to kill browser gestures.
- **Bottom bar** (thumb zone, respects `env(safe-area-inset-bottom)`):
  - **Map** button (P) — left.
  - **Context action** button — center, wide, label changes live:
    "Enter Gloom" / "Climb down" / "Meditate" / "Open chest" /
    "Board ship" / "Go ashore" / "Camp" / "Talk to Wren". Resolves the
    same logic the hint messages already use. Disabled label ("…") when
    nothing applies.
  - **Attack/targeting** button — right (see combat).
- Landscape: two-column (canvas left, log+stats right) via media query —
  approximately the desktop layout.

## Movement: virtual joystick (the d-pad vibe)

- **Fixed joystick, bottom-left**: a semi-transparent ring with a knob.
  Touch and drag; direction resolves to the dominant axis (the game is
  4-way). Dead zone ~16 px so resting a thumb does nothing.
- **Hold to walk**: first step fires on engage, then repeats every
  ~170 ms while held — exactly the cadence of holding an arrow key.
  Release stops instantly.
- Implemented by dispatching the real Arrow key events, so the entire
  existing input stack (bump-attack, direction prompts after T/F,
  overlay dismissal) works untouched — aiming a cannon is "tap ⚔, flick
  the stick."
- Tap-to-move shelved (kept here for the record); swipe-step dropped.

## Context actions by tap (the U7 rule: tap the thing)

| Tap target                  | Action                              |
|-----------------------------|-------------------------------------|
| adjacent monster            | melee attack (bump)                 |
| distant monster (bow/ship)  | ranged shot / cannon if in range+LoS|
| adjacent NPC                | talk (portrait + chips)             |
| self                        | pass turn (space)                   |
| tile underfoot w/ feature   | same as context button (E/G/M)      |
| distant walkable tile       | auto-walk                           |

Long-press any tile = "look" (identify sprite: "a wraith", "a moongate").

## Combat

- Melee: tap the adjacent enemy. Auto-walk toward a tapped distant enemy
  stops at melee range, never swings without a tap.
- Ranged (bow, cannons): tap enemy within range — the game validates
  range/line like `shootArrow`/`fireCannon` already do. The ⚔ button
  toggles "aim mode" highlighting valid targets when ambiguous.
- Direction prompts (old F+arrow flow) disappear on touch: the tap IS
  the direction.

## Dialogue & typing

- Chips unchanged (they're already ideal).
- A **⌨ chip** at the end of the chip row summons the OS keyboard for
  typed secrets/mantras; input stays pinned above the keyboard using
  `visualViewport` so the layout never jumps.
- Shrine mantra entry: show the keyboard automatically (it's the one
  place typing is the point).

## System / platform

- **Autosave** on `visibilitychange` (hidden) — mobile browsers evict
  tabs; nobody loses a run to a phone call.
- **Audio unlock** on first `touchstart` (extend `ensureMusic`).
- **PWA**: manifest + icon + `display:standalone` so it installs to the
  home screen; the single-file game is already offline-capable — add a
  tiny service worker for cache.
- Safe areas: pad bottom bar and HUD with `env(safe-area-inset-*)`.
- Prevent double-tap zoom (`touch-action`), pinch reserved for future
  map zoom.
- Haptics: `navigator.vibrate(15)` on hit taken / level-up (Android;
  iOS ignores it gracefully).

## Keyboard parity

Every key keeps working. The mobile chrome (HUD, bottom bar) appears at
`max-width: 720px` or `pointer:coarse`; desktop layout is untouched
above that. One `index.html`, one save format, both worlds.

## Build phases

1. **Core** — responsive layout + mini-HUD + stats drawer + tap-to-move
   + context action button + chips keyboard summon + autosave-on-hide.
2. **Combat & polish** — tap targeting for bow/cannon, aim mode,
   long-press look, swipe steps, landscape layout.
3. **Platform** — PWA manifest/service worker, haptics, D-pad option,
   install prompt.
