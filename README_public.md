# Memory Game

A real-time multiplayer memory card game built as a single self-contained HTML file. Players match pairs of cards across themed categories, and each match reveals a detail panel with a title, subtitle, body text, and a key metric. All content is supplied at runtime through a CSV file, so the game can be themed for any topic without touching the code.

**Current version:** 1.3.0

## Live demo

Once published via GitHub Pages or Netlify, open the hosted URL and you are taken to the lobby. A game data CSV must be loaded before a room can be created.

## How to play

1. **Load the game data.** On the lobby screen, paste a Google Drive CSV link into the *Load game data* field and click *Load*. This step is required: the game ships with no built-in cards.
2. **Create or join a room.** One player enters a name and clicks *Create room* to get a 4-letter room code. Everyone else enters their name plus that code and clicks *Join room*.
3. **Host starts the game.** Once 2 to 4 players are in the room, the host presses *Start game*.
4. **Take turns.** Players are highlighted automatically when it is their turn. Each turn has a 15-second timer.
5. **Match pairs.** Flip two cards. If they match, the detail panel at the bottom reveals the full card content and the player earns the point.

### Turn rules

- A match grants a **bonus turn**. A second consecutive match scores the point but does **not** grant a third turn.
- A missed match passes the turn to the next player.
- If the 15-second timer runs out with no completed move, the turn is forfeited and passes on.
- The turn timer can be **paused** by any player using the pause button; the freeze is synchronized across all devices.

### Scoreboard

The side panel shows, at all times:

- Each player's name, with the active player highlighted.
- A performance indicator per player: matches divided by turns, shown as a percentage.
- Per-category progress: how many pairs have been found, and which players found them.

## Supplying content with a CSV

The game has no bundled cards. All content, categories, titles, labels, and metrics come from a CSV file hosted on Google Drive.

### Steps

1. Build a CSV using the schema below. Each row is one card. Define each card **once**; the engine automatically creates its matching pair.
2. Keep the total number of card rows **even** (10 rows is recommended for a 5x4 board).
3. Save as `.csv` and upload to Google Drive.
4. Right-click the file, choose *Share*, and set access to **Anyone with the link can view**.
5. Copy the shareable link.
6. Open the game, paste the link into the *Load game data* field on the lobby screen, and click *Load*.

### CSV columns

| Column | Description |
| --- | --- |
| `game_title` | Title shown on the lobby and browser tab (first row only). |
| `game_subtitle` | Subtitle below the title. |
| `category_id` | Short key grouping cards (for example `a`, `b`, `c`). |
| `category_name` | Display name in the sidebar. |
| `category_color` | Hex accent color for the category. |
| `category_bg` | Light hex background for the result-panel tag badge. |
| `category_text_color` | Dark hex text color for the tag badge. |
| `card_title` | Short title on the card face and result panel heading. |
| `card_subtitle` | One-line subtitle in the result panel. |
| `card_body` | 2 to 3 sentence description in the result panel. |
| `card_icon` | Font Awesome 6 Free icon handle (for example `fa-trophy`). |
| `metric1_label` | Label for the headline metric. |
| `metric1_value` | Value for the headline metric. |
| `metric2_label` | Label for the supporting context line. |
| `metric2_value` | Value for the supporting context line. |

Browse icon handles at https://fontawesome.com/search?o=r&m=free&s=solid

## Setup: real-time sync (Firebase)

Multiplayer sync uses Firebase Realtime Database. The included build is wired to a Firebase project. To point it at your own:

1. Create a project at https://console.firebase.google.com
2. Add a Realtime Database (start in test mode for quick setup).
3. Register a web app and copy the `firebaseConfig` block.
4. Replace the `firebaseConfig` object near the bottom of the HTML file.

> Note: test-mode database rules expire after 30 days. To keep the game running, set the rules to allow read and write access.

## Publishing

### GitHub Pages

1. Push `pm_memory_game_public_v1.3.0.html` to a public repo.
2. In the repo, go to *Settings > Pages*, select the `main` branch, and save.
3. Your game will be live at `https://<username>.github.io/<repo>/pm_memory_game_public_v1.3.0.html`.

### Netlify

Connect the repo in Netlify with no build command and the root as the publish directory, or drag the HTML file onto https://drop.netlify.com for an instant public URL.

## Files

| File | Purpose |
| --- | --- |
| `pm_memory_game_public_v1.3.0.html` | The complete game engine (single file, no bundled content). |
| `README.md` | This file. |

The game data CSV is **not** included in this repository. It is hosted privately on Google Drive and loaded at runtime, so card content stays separate from the public code.

## Tech notes

- Single HTML file: no build step, no dependencies to install.
- No content is bundled in the code; a CSV must be loaded to play.
- Firebase Realtime Database for cross-device state sync.
- Font Awesome 6 Free (loaded via CDN) for card icons.
- The board grid sizes itself automatically based on the number of cards.

## Changelog

### v1.3.0
- Public build: removed all bundled card data. A CSV is now required to create a room.
- Taller, more readable result panel that shows the full card body without scrolling.
- Larger result icon and headline metric, with the metric value colored to match the category accent.
- Board cards shrink slightly to give the detail panel more room.

### v1.2.0
- Version stamped in the title and lobby screen.
- CSV-driven customization and Font Awesome icons.
