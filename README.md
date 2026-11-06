# Newfoundland Rails

A browser game for 2 to 5 players: claim rail routes across Newfoundland, connect the towns on your destination tickets, and score the most points.

Play it at **https://lumoconnor.github.io/ttrnl/**

## How to play online

1. One player opens the page, enters a name, and chooses **Create game**. They get a five-letter code.
2. They send the others the invite link (the **Copy invite link** button in the lobby) or the code.
3. Everyone else opens the link, enters a name, and joins. The host starts the game.

The host's browser runs the game, so the host keeps the page open. If the host reloads or closes the tab, play pauses; reopening the page and choosing **Return to the game** picks it up where it left off. Other players who reload can choose **Rejoin game**.

You can also play on one device: **pass and play** takes turns on one screen, and **Quick test** starts a three-player game with test tools.

## How it works

Everything is one static page (`index.html`), so it runs on GitHub Pages with no server of our own.

- **Online play** uses [PeerJS](https://peerjs.com/) (vendored in `vendor/`, MIT licence) to open direct WebRTC connections between browsers. The free PeerJS cloud service only introduces the browsers to each other (and relays traffic through its TURN servers when a direct connection is blocked). The host's browser holds the game state, applies every move with the rules engine, and sends the new state to everyone. The host also saves the game in `localStorage`, which is how a reload resumes.
- **The board** is data: `boards/newfoundland.json` (40 towns, 107 routes, 36 destination tickets, rules) is a readable copy of the board embedded in `index.html`. The map is drawn from that data over a coastline from [Natural Earth](https://www.naturalearthdata.com/) (public domain).

### Testing online play locally

Run a PeerJS server (`npx peer --port 9000`) and a static server in this folder, then open `index.html?peerhost=127.0.0.1&peerport=9000` in two browser profiles.
