# Rally Register

The EP Asset Management team's table tennis ladder. Log matches of any number of games, track Elo ratings and see head-to-head records.

**Use it:** https://tjaartz.github.io/rally-register/ (team password required, once per device and browser)

## How it is built

One static page, `docs/index.html`, served by GitHub Pages. Players and matches live in Google Firebase (Cloud Firestore). Each browser signs in anonymously and becomes a member by entering the team password once. The Firestore security rules check the password on Google's servers, so nobody without it can read or change results.

| Path | What it is |
|---|---|
| `docs/index.html` | The app, served at the address above. |
| `firestore.rules` | Template of the Firestore security rules. The real team password lives only in the Firebase console, never in this repo. |

The Firebase web config in `docs/index.html` is public by design: it identifies the project, and access is controlled by the rules.

## Looking after it

- **Change the team password:** Firebase console → Firestore Database → Rules, edit the password, then Publish. Browsers that already joined keep access.
- **Make everyone enter the password again:** delete the `members` collection in the Firestore console.
- **Fix a result by hand:** edit or delete documents in the `players` and `matches` collections in the Firestore console.

## Rules the app enforces

- Every game goes to 11, with a 2-point lead needed from 10–10 (12–10, 13–11 …).
- A match can have any number of games (1 to 15). Every game counts; most games won takes the match. A level score needs a deciding game.
- Ratings use Elo: everyone starts at 1000, K = 32, and matches are replayed in date order.

## Data shape

- `players/{id}`: `{ name, createdAt }`
- `matches/{id}`: `{ a, b, sets: [{ a, b }, …], winner, playedOn, createdAt }`. `a` and `b` are player ids, `sets` holds one entry per game, `playedOn` is `YYYY-MM-DD`.
- `members/{uid}`: `{ password, joinedAt }`, written once when a browser joins. The page can't read it back.

## Brand

Colours, type and shapes follow the Energy Partners brand: navy `#0C3957` with blue `#2490B8` as the single accent, Montserrat for headings and figures, Source Sans 3 for body copy, sentence-case headings, no shadows or gradients.
