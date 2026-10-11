# Ruy López Chess Trainer

A polished, offline-first chess opening studio for learning the Ruy López (Spanish Opening) as White, with optional practice from Black’s perspective.

## Features

- **Learn:** interactive lessons covering the opening moves, development, center, bishop pair, pawn structure, space, king safety, and initiative.
- **History & style:** sourced historical timeline and a variation-sensitive account of the opening’s attacking and positional trade-offs.
- **Variation explorer:** navigate a curated tree of more than 20 principal and commonly encountered defenses, including Berlin, Morphy, Open, Exchange, Closed/Breyer, Marshall/Anti-Marshall, Schliemann–Jaenisch, Classical, Steinitz and Bird. Coverage is selective, not exhaustive.
- **Historical games:** replay complete game scores sourced from PGN Mentor; navigate by SAN or jump to teaching moments. Original instructional commentary is identified as interpretation, not as an attributed annotation or engine analysis.
- **Practice & review:** legal move entry and board interaction, White and Black exercises, progressive hints, distinction between trained moves, legal alternatives and off-plan moves, spaced review, glossary, quizzes and a printable reference sheet.
- **Local-first:** bundled lesson and game data; progress is stored locally, with no account, paid API or network connection required for the learning experience.
- **Windows desktop:** packaged in Electron with an offline local interface.

## Run the web app

Requires Node.js 22.12 or newer and npm.

```sh
npm ci
npm run dev
```

Vite prints the local development URL. To build the browser app:

```sh
npm run build
```

## Build the Windows desktop app

On Windows x64:

```powershell
npm ci
npm run package
```

The packaged directory is `release/win-unpacked`. Start **Ruy López Chess Trainer.exe** from that directory. The build bundles Electron and the site assets; users running the application do not need Node.js or a development server. To install the app in your per-user Local AppData Programs folder and create/update its shortcut on the resolved Windows Desktop, run `python scripts/install.py`. Learning progress is stored separately in `%LOCALAPPDATA%\RuyLopezTrainerData`, so updating the application does not overwrite it.

The published repository contains source and build inputs, not `node_modules`, generated bundles, or the large platform-specific Electron distribution. GitHub is not used as an application backend.

## Tests

```sh
npm test
npm run dev -- --host 127.0.0.1 --port 5173
```

In another terminal:

```sh
npm run test:ui
```

The browser test exercises section navigation; representative opening branches; board geometry and legal/illegal moves; all historical scores; replay controls; both practice perspectives; quiz and progress persistence; and a narrow mobile viewport. `tests/ui.mjs` also supports `APP_EXE` mode for testing a packaged Windows application, including loading bundled sections after blocking HTTP(S) requests. For a fresh independent check of the game records, install `python-chess` and run:

```sh
python tests/verify_sources.py
```

The record-check script re-fetches the identified PGNs and checks that each expected full SAN score and its metadata still match the source. This *verification script* needs an Internet connection; the chess trainer itself does not.

## Sources and scope

Historical outline and repertoire explanations are summarized in original wording from the [Wikibooks Ruy López opening chapter](https://en.wikibooks.org/wiki/Chess_Opening_Theory/1._e4/1...e5/2._Nf3/2...Nc6/3._Bb5) and cross-checked against [Wikipedia’s Ruy López reference](https://en.wikipedia.org/wiki/Ruy_Lopez). Event and player records are cited in `research.json` and the app, linked to the exact [PGN Mentor Capablanca archive](https://www.pgnmentor.com/players/Capablanca.zip), [Fischer archive](https://www.pgnmentor.com/players/Fischer.zip), and [2000 World Championship event score](https://www.pgnmentor.com/events/WorldChamp2000.pgn); the [PGN Mentor index](https://www.pgnmentor.com/files.html) identifies those collections. Re-fetched records are independently checked in `tests/source-results.json`. Full reference downloads are not needed to build or run the application and are deliberately not tracked.

Chess move legality is enforced by [`chess.js`](https://github.com/jhlywa/chess.js). Strategic commentary is educational interpretation, not engine-verified evaluation. The historical games reproduce the supplied database scores through their recorded final moves; a resignation or agreed draw need not be checkmate or stalemate. Refer to `research.json` for exact PGN headers, score-verification details, the date limitations and the historical-source notes.

## Privacy

In the installed desktop app, preferences and learning progress remain in the current Windows user’s Local AppData. The desktop shell denies web access in the application window; external references open in the user’s normal browser. No telemetry, remote fonts, login or cloud synchronization are used.
