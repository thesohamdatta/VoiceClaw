# VoiceClaw — Project Context & Architecture

VoiceClaw is a voice-first interactive development environment. It leverages **Gemini 3.1 Flash Live** for low-latency voice orchestration and **Claude Code CLI** for high-fidelity codebase manipulation.

## 🏗️ Architecture

The system operates as a distributed bridge between local execution and cloud-based AI:

- **Frontend (React/TS/Vite):** Handles audio capture and playback. It establishes a **direct WebSocket connection to Gemini Live API** for minimal voice latency.
- **Backend (FastAPI):** Acts as a thin relay and orchestrator. It spawns `claude -p` as a subprocess to execute tasks.
- **Dual Gemini Sessions:**
    - **Main Session (Jarvis):** Handles user conversation, intent recognition, and tool calls.
    - **Narration Session:** A separate, parallel Gemini session that provides real-time spoken commentary ("sports commentary") while Claude is working.
- **Claude CLI Subprocess:** Instead of using an API, VoiceClaw runs the `claude` CLI with `--output-format stream-json`. This provides Claude's full tool suite (LSP, shell, file I/O) out-of-the-box.
- **Function Routing:** Gemini calls high-level functions (e.g., `code_task`, `investigate_and_advise`) which are mapped to specific `claude` CLI invocations with varying permissions and tool constraints.

## 🚀 Key Commands

### Backend (Python)
- **Install Dependencies:** `pip install -r requirements.txt`
- **Run Server:** `python server.py`
- **Run with Pre-selected Project:** `python server.py --project /path/to/project`
- **Set Port:** `python server.py --port 3333`

### Frontend (Node.js)
- **Install Dependencies:** `cd frontend && npm install`
- **Development Mode (Hot Reload):** `npm run dev` (proxies API to `:3333`)
- **Build:** `npm run build`

## 🛠️ Development Conventions

### Python Backend
- Uses **FastAPI** for REST and WebSockets.
- Orchestrates `claude` CLI via `subprocess.Popen` in `claude_runner.py`.
- Employs **Git Checkpoints** for safety: Every `code_task` or `run_command` triggers a git commit (`[VoiceClaw checkpoint]`) to allow for voice-controlled `rewind`.
- Session persistence for Gemini handles and Claude session IDs is managed in `.voicecode/session.json` within the project directory.

### Frontend
- **React 19** with **Vite** and **Tailwind CSS**.
- **WebSocket Orchestration:** Managed across `gemini-connection.ts`, `narration-connection.ts`, and `backend-connection.ts`.
- **Audio Processing:** `audio-manager.ts` handles PCM worklets for low-level audio streaming.
- **Debugging:** `Ctrl+Shift+D` downloads a detailed event log for troubleshooting.

### AI Personas (Prompts)
- **Jarvis (Main):** Senior engineer, concise, direct, witty, and "ruthless" (roasts the user/Claude). Responds in English regardless of input language.
- **Narrator:** Commentary-style, brief (1-2 sentences), focuses on "what and why" of Claude's activity. Also roasts everything.

## 📁 Key File Map

| File | Purpose |
|---|---|
| `server.py` | FastAPI entry point, WebSocket relay for Claude events. |
| `claude_runner.py` | Spawns and manages the `claude` CLI subprocess. |
| `function_router.py` | Maps Gemini tool calls to `claude` instructions. |
| `checkpoint.py` | Git-based checkpointing and session management. |
| `frontend/src/main.ts` | Frontend entry point and module glue. |
| `prompts/gemini_system.md` | System instructions for the main conversation Gemini. |
| `prompts/narration_system.md` | System instructions for the live narrator Gemini. |

## Agent skills

### Issue tracker

GitHub — issues live in the repo's GitHub Issues. See `docs/agents/issue-tracker.md`.

### Triage labels

Default canonical labels. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context — one `CONTEXT.md` + `docs/adr/` at the repo root. See `docs/agents/domain.md`.
