# Chris Tarot Web

A browser-based tarot/oracle card reading app (`index.html`, `sage.css`, `sage.js`) with a custom deck builder and selectable background scenes.

## Color Palette

Colors are used directly as hex/rgba values in `sage.css` (no CSS custom properties/variables are defined). Grouped by role below.

### Sage / seafoam green — primary UI surfaces
The dominant palette family, used for panels, modals, buttons, and headers.

| Swatch | Hex | Usage |
|---|---|---|
| 🟩 | `#bcd8c8` | Modal headers/backgrounds (custom layout, guidebook, deck modal), card preview area |
| 🟩 | `#94ac9f` | Modal body backgrounds, custom cell tiles, "Next"/"Confirm" buttons |
| 🟩 | `#aab6a0` | Deck-type toggle default state, arrow toggle button |
| 🟩 | `#919e86` | Deck-type toggle active state |
| 🟩 | `#557367` | Deck-type toggle hover state |
| 🟩 | `#5d8272` | Layout grid buttons |
| 🟩 | `#3d6b58` | Layout grid button hover |
| 🟩 | `#587362` | Audio "playing" button state |
| 🟩 | `#709284` / `rgba(112,146,132,0.5)` | Semi-transparent panel backgrounds (custom count, position list) |
| 🟩 | `#ebefe9` | Custom cell hover background |

### Gold / bronze — accents & highlights
| Swatch | Hex | Usage |
|---|---|---|
| 🟨 | `#c9a84c` | Active/hover accents — icon borders, preview card labels, active cell borders |
| 🟨 | `#8a7a60` | Secondary icon/button text and borders |

### Terracotta / rust — secondary accent
| Swatch | Hex | Usage |
|---|---|---|
| 🟧 | `#c97a4c` | Rotated preview card border/text |
| 🟧 | `#e3d5c8` | Rotated preview card background |

### Purple — deep accents
| Swatch | Hex | Usage |
|---|---|---|
| 🟪 | `#2e2548` | Header text border, custom footer button borders |
| 🟪 | `#44446a` | Card-back placeholder background |
| 🟪 | `#9b6dcc` | Background-thumbnail hover border |
| 🟪 | `#7b5ea7` | Custom cell hover border |

### Neutrals — text & backgrounds
| Swatch | Hex | Usage |
|---|---|---|
| ⬜ | `#fff` / `#ffffff` / `#fefefe` / `#fcfcfc` | Body text (white), light backgrounds/borders |
| ⬜ | `#f1e7e3` | Active custom-cell background |
| ⬜ | `#333` / `#222` | Dark text |

### Transparency layers
Most interactive surfaces (buttons, overlays, hover states) use `rgba(255,255,255, 0.1–0.9)` white overlays for glass-like translucency, and `rgba(0,0,0, 0.5–0.75)` black overlays for shadows/scrims — rather than flat opaque fills.

### Light/dark text theming
`sage.css` has a `THEME — LIGHT / DARK TEXT SWITCHING` block (body.theme-dark / body.theme-light) that swaps UI text between `rgba(255,255,255,0.9)` (white, for dark background images) and `rgba(0,0,0,0.75)` (dark, for light background images). Each background entry in `BG_CATEGORIES` (`sage.js`) can carry a `theme: "dark" | "light"` field so text stays legible against whichever background is selected; entries without one default to `"dark"`.

### Base
The page background (`body`) is white text (`color: white`) over a full-bleed fixed background image (see Background Categories below), giving the app its default look before a user picks a custom background.

---

## Background Categories

Backgrounds are selectable via a picker modal, defined in `sage.js` (`BG_CATEGORIES`). Files live in [img/background/](img/background/).

| Category | Label | Images |
|---|---|---|
| `animals` | **Animals** | `background74.png` – Default · `background1.jpeg` – Ladybug · `background2.jpeg` – Mouse · `background3.jpeg` – Fox |
| `mystical` | **Mystical** | `background4.jpeg` – Dragon · `background18.jpeg` – Dragon 2 · `background5.jpeg` – Castle · `background6.jpeg` – Winter Cave · `background7.jpeg` – Lanterns |
| `marble` | **Marble** | `background8.jpeg` – Blue waves · `background9.jpeg` – Black |
| `stone` | **Stones** | `background10.jpeg` – Blue Stones · `background11.jpeg` – Mossy Rock · `background12.jpeg` – Glowing Stones |
| `forest` | **Forest** | `background16.jpeg` – Acorns |
| `ocean` | **Ocean & Sand** | `background13.jpeg` – Ocean · `background14.jpeg` – Ocean 2 · `background15.jpeg` – Ocean 3 |

`background74.png` doubles as both the "Default" picker option and the app's default `body` background (set directly in `sage.css`). Note there is no `background17.jpeg` — the picker's file numbering skips it.

> **Note:** this list was restored to match the files actually present in `img/background/`. The `sage.js`/`sage.css` code was originally copied over from another project ("White Sage") and briefly referenced that project's own background set (`caves`, `floral`, `forestandleaves`, `lakesandrivers` categories, files like `background23.jpeg`, `dragon2.jpg`, etc.) — none of which exist in this project, so the picker and the default page background were both broken (404s) until fixed.

---

## Custom Decks

This app no longer ships pre-built decks. `deckConfig` in `sage.js` starts empty (`const deckConfig = {}`) — every deck is created by the user through the in-app **custom deck builder** (tarot or oracle layout, uploaded card images), then persisted locally:

- **Primary storage:** IndexedDB, database `white-sage-custom-decks` (object store `decks`).
- **Fallback / legacy storage:** localStorage key `chris-tarot-customDecks` (used only if IndexedDB is unavailable, and for one-time migration of any pre-existing data saved under the old, unnamespaced `customDecks` key).

Both storage mechanisms are scoped to this app's own browser origin and cannot be read by or shared with any other website.

### Leftover, unused deck images
[img/deck1/](img/deck1/) (Sheep, partial), [img/deck2/](img/deck2/) (Mouse), [img/deck3/](img/deck3/) (Pirate), and [img/deck4/](img/deck4/) (Medieval) contain full/partial 78-card tarot artwork from an earlier version of the app that used a hardcoded `deckConfig` registry. **Nothing in `sage.js`, `sage.css`, or `index.html` currently references these folders** — they're dead assets left over from before the switch to fully custom/user-uploaded decks. Safe to delete if the earlier hardcoded-deck approach won't be revisited, or worth wiring back in as selectable presets if it will.

Additional standalone image: [img/chris-logo.png](img/chris-logo.png) — site logo (also currently unreferenced in the code — check before removing).
