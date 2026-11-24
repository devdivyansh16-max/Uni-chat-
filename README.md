# CampusChat

A responsive real-time chat application built with **Node.js, Express, Socket.IO, HTML, CSS, and JavaScript**. It includes public community rooms and personal invite-code rooms for study groups.

## Features

- Real-time messaging with multiple users
- Personal private rooms with 6-character invite codes
- Public rooms that everyone can discover
- Online member list and live member counts
- Typing indicators
- Room search and “My rooms” filter
- Four color themes: Violet, Ocean, Sunset, and Forest
- Animated welcome screen, messages, buttons, and status indicators
- Responsive desktop and mobile layouts
- Profile name and avatar color saved in the browser
- Message history and private-room access restored after reconnecting
- Input validation and safe rendering of message text
- No database or external API keys required

## Screenshots

### Welcome screen

![CampusChat welcome screen](screenshots/welcome.png)

### Desktop chat

![CampusChat desktop chat](screenshots/desktop.png)

### Mobile chat

![CampusChat mobile chat](screenshots/mobile.png)

## Run in VS Code

### Requirements

- Node.js 18 or newer
- VS Code with its built-in terminal

### Steps

1. Open the `chatapp` project folder in VS Code.
2. Open a terminal using **Terminal → New Terminal**.
3. Install the dependencies:

   ```bash
   npm install
   ```

4. Start the application:

   ```bash
   npm start
   ```

5. Open this address in a browser:

   ```text
   http://localhost:3000
   ```

Keep the terminal running while using the application. Press `Ctrl + C` in the terminal to stop the server.

> Use `npm start`, not VS Code Live Server. The Node server provides both the frontend files and the real-time Socket.IO connection.

## Test with multiple users

1. In the first browser, enter a display name and select **Enter CampusChat**.
2. Select **Create a room**, enter a room name, and keep **Private room** selected.
3. Copy the generated invite code.
4. Open a second browser or an incognito/private window.
5. Open `http://localhost:3000`, enter a different display name, and select **Join room**.
6. Enter the invite code.
7. Send messages from both browsers and check the live member list and typing indicator.

Using two incognito windows or two different browsers creates separate local profiles, which makes multi-user testing straightforward.

## Available commands

| Command | Purpose |
| --- | --- |
| `npm start` | Start CampusChat on port 3000 |
| `npm run dev` | Start CampusChat with automatic server restart |
| `npm test` | Run the automated integration tests |
| `npm run check` | Check server and frontend JavaScript syntax |
| `npm run start:all` | Start CampusChat and the original classroom Socket.IO server |
| `npm run start:classroom` | Start only the original classroom server on port 8080 |

If port 3000 is already in use, set another port before starting:

**Windows PowerShell**

```powershell
$env:PORT=3001
npm start
```

**macOS / Linux**

```bash
PORT=3001 npm start
```

Then open `http://localhost:3001`.

## Project structure

```text
chatapp/
├── public/
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── screenshots/
│   ├── welcome.png
│   ├── desktop.png
│   └── mobile.png
├── tests/
│   └── server.test.js
├── chat-server.js
├── client.html
├── package.json
├── package-lock.json
├── server.js
└── start.js
```

## Backend note

The original classroom files, `server.js` and `client.html`, are preserved unchanged. `chat-server.js` is the additional application server used by the new frontend. It provides room management, membership checks, message validation, presence, and typing events.

Rooms and message history are stored in server memory, so they reset when the server restarts. This keeps the assignment dependency-free and easy to run locally.

## Verification

`npm test` checks:

- Frontend and health endpoints
- Private-room access control
- Invite-code validation
- Multi-user presence
- Real-time message delivery
- Duplicate, empty, and oversized message handling
- Private-room access after reconnecting
- Message history restoration
- Leaving rooms
- Public-room discovery
- Room isolation
- Typing events
