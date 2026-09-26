# Board Game Matcher (QVAC)

Describe your game night, like "relaxed co-op for me and my partner" or "silly party game for a big group", set how many players and how long you have, and find **board and card games that fit by meaning** from a list of 40, from UNO and Codenames to Wingspan and Pandemic. Build a **game night list** to copy and share.

It runs **on your own computer** using [QVAC](https://github.com/tetherto/qvac), Tether's open-source AI SDK.
No API key, no cloud service, and what you type never leaves your machine.

![screenshot](screenshot.png)

## SDK version

`@qvac/sdk` **0.19.0** (declared in `package.json`)

Functions used: `loadModel` and `embed`, with the `EMBEDDINGGEMMA_300M_Q4_0` model.

## Install

You need [Node.js](https://nodejs.org) 22 or newer and some free disk space for the model.

```bash
git clone https://github.com/misaki-codex/qvac-board-game-matcher.git
cd qvac-board-game-matcher
npm install
```

## Run

```bash
npm start
```

Then open **http://localhost:3071** (the address, not the HTML file). The first start downloads the model.
While it loads, keyword matching is used instead, so it always works.

## How it works

- `games.js` holds 40 popular games with player count, play time, age and a description of how each feels. Add your own.
- Only games that fit your player count and time are compared. Then `server.js` ranks them with QVAC's `embed` by cosine similarity.
- Player counts, times and ages are approximate, so check the box for your edition.
- The server listens on `127.0.0.1`, so only your own computer can reach it.

## Troubleshooting

If you see `RPC_INIT_TIMEOUT`, the QVAC worker was slow to start. `server.js` already waits 3 minutes.
Set `QVAC_RPC_INIT_TIMEOUT_MS` (milliseconds) before `npm start` to wait longer, and make sure no other
QVAC app is running at the same time. If you see `ERR_MODULE_NOT_FOUND`, delete the `node_modules` folder
and run `npm install` again (this usually means an install was interrupted, for example by a full disk).

## License

MIT
