# CodeBridge — Collaborative Code Editor API

A real-time, two-person collaborative coding backend built with **FastAPI** and **WebSockets**. Two participants share a room, edit code simultaneously, and can execute Python snippets — all in-memory with no database required.

---

## Overview

Code Bridge Hub is a browser-based collaborative coding environment. Two developers can join the same room, write code together in real time, and instantly execute it — no setup, no account required beyond an email address.

It connects to a FastAPI + WebSocket backend ([codebridge API](https://codebridge-6gli.onrender.com)) that handles room management, live code synchronization, and sandboxed code execution.

---

## Features

- **Shared code rooms** — Create a room in one click and share a 5-character room code with your collaborator
- **Real-time sync** — Changes appear instantly on both sides via WebSocket, with cursor and selection tracking
- **Live code execution** — Run Python or C++ directly in the browser; stdout, stderr, exit code, and execution time are shown in the output panel
- **Multi-language support** — Syntax highlighting and language-aware templates for Python and C++
- **Room status checks** — Look up any room code before joining to see language, participant count, and availability
- **Monaco Editor** — Full VS Code-quality editing experience (the same editor that powers VS Code on the web)
- **Responsive UI** — Works on desktop and large tablets

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 18 + TypeScript |
| Build tool | Vite |
| Styling | Tailwind CSS + shadcn/ui |
| Code editor | Monaco Editor (`@monaco-editor/react`) |
| Routing | React Router v6 |
| Real-time sync | WebSocket (native browser API) |
| Backend API | FastAPI (hosted on Render) |
| Icons | Lucide React |

---

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm 9 or later

### Installation

```bash
git clone https://github.com/aryan9867bar/codebridge-web
cd codebridge-web
npm install
```

### Development

```bash
npm run dev
```


### Production build

```bash
npm run build
npm start          # runs the included Node.js static server
```

---

## Usage

### Creating a room

1. Enter your email address
2. Select a language (Python or C++)
3. Click **Create Room**
4. Share the generated room code with your collaborator

### Joining a room

1. Enter your email and the room code you received
2. Click **Check Room** to verify it exists and has space
3. Click **Join Room** to enter the editor

### In the editor

- Both participants see each other's cursor position and selections in real time
- Click **Run** to execute the current code — output appears in the right panel
- The output panel shows stdout, stderr, exit code, and execution time for each run
- Click the trash icon to clear the output history

---

## Project Structure

```
src/
├── components/
│   ├── room/               # Editor-specific components
│   │   ├── RoomHeader.tsx  # Connection status, run button, participant count
│   │   └── OutputPanel.tsx # Execution results panel
│   ├── ui/                 # shadcn/ui primitives
│   ├── CodeTogetherLogo.tsx
│   ├── FormField.tsx
│   ├── LanguageSelect.tsx
│   ├── RoomInfoCard.tsx
│   └── StatusMessage.tsx
├── pages/
│   ├── Index.tsx           # Landing page (create/join room)
│   ├── Room.tsx            # Collaborative editor
│   └── NotFound.tsx
├── hooks/
├── lib/
└── App.tsx
```

---

## Configuration

The backend URL is defined at the top of `src/pages/Index.tsx` and `src/pages/Room.tsx`:

```ts
const API_BASE = "https://codebridge-6gli.onrender.com";
const WS_BASE  = "wss://codebridge-6gli.onrender.com";
```

To point the frontend at a local backend, replace these values with `http://localhost:8000` and `ws://localhost:8000` respectively.

---

## Deployment

The project includes a `render.yaml` for one-click deployment to [Render](https://render.com). The build command is:

```bash
npm ci --include=dev && npm run build
```

---

## License

MIT
