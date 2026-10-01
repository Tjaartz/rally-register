# Rally Register

The EP Asset Management team's table tennis ladder. Log matches of any number of games, track Elo ratings and see head-to-head records.

- **Start here:** https://tjaartz.github.io/rally-register/
- **Live app:** https://claude.ai/artifact/8998AXCxmqThWcRTNDrZYB (needs a Claude account in the Energy Partners organisation, shared as Contributor to record results)

## How it is built

The live app runs as a Claude artifact. Its shared database (players and matches) lives with the artifact on claude.ai, not in this repo, so the repo holds no names or results.

| Path | What it is |
|---|---|
| `src/rally-register.html` | The app. Published to the Claude artifact above. |
| `docs/index.html` | The landing page served by GitHub Pages (from `/docs` on `main`). |

## Rules the app enforces

- Every game goes to 11, with a 2-point lead needed from 10–10 (12–10, 13–11 …).
- A match can have any number of games (1 to 15). Every game counts; most games won takes the match. A level score needs a deciding game.
- Ratings use Elo: everyone starts at 1000, K = 32, and matches are replayed in date order.

## Updating the app

1. Edit `src/rally-register.html`.
2. Ask Claude Code to republish it to the artifact URL above. It updates in place, so the link and the data stay the same.
3. Commit and push the change here.

## Data shape

Stored in the artifact's database:

- `players/{id}`: `{ name, createdAt }`
- `matches/{id}`: `{ a, b, sets: [{ a, b }, …], winner, playedOn, createdAt }`. `a` and `b` are player ids, `sets` holds one entry per game, `playedOn` is `YYYY-MM-DD`.

## Brand

Colours, type and shapes follow the Energy Partners brand: navy `#0C3957` with blue `#2490B8` as the single accent, Montserrat for headings and figures, Source Sans 3 for body copy, sentence-case headings, no shadows or gradients.
