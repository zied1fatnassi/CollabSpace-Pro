# CollabSpace Pro — Frontend Demo

This repository contains a front-end scaffold for CollabSpace Pro: an animated, interactive landing page and a demo real-time board.

What is included
- Vite + React + TypeScript scaffold
- Animated gradient and floating UI elements (Framer Motion)
- Landing page at `/`
- Login page at `/login` with social auth stubs, magic-link form, and biometric (WebAuthn) demo stub
- Demo board component that syncs across browser tabs using BroadcastChannel and optionally via Socket.IO if `COLLABSPACE_SOCKET_URL` is provided at runtime.

Quick start
1. Install dependencies:

```powershell
npm install
```

2. Run the dev server:

```powershell
# CollabSpace Pro — Frontend Demo

This repository contains a front-end scaffold for CollabSpace Pro: an animated, interactive landing page and a demo real-time board.

What is included
- Vite + React + TypeScript scaffold
- Animated gradient and floating UI elements (Framer Motion)
- Landing page at `/`
- Login page at `/login` with social auth stubs, magic-link form, and biometric (WebAuthn) demo stub
- Demo board component that syncs across browser tabs using BroadcastChannel and optionally via Socket.IO if `COLLABSPACE_SOCKET_URL` is provided at runtime.

Quick start
1. Install dependencies:

```powershell
npm install
```

2. Run the dev server:

```powershell
npm run dev
```

Open http://localhost:5173

Quick validation (what to check)
- Landing page: animated background + floating UI elements visible.
- Demo board: in the landing preview, add/edit cards — open a second tab to http://localhost:5173 and you should see changes sync (BroadcastChannel syncs across tabs in the same origin).
- Login page: go to /login — click social buttons (stubs), submit magic-link form (simulated), try biometric sign-in (WebAuthn stub will attempt a credentials.get() — real flow requires a backend challenge).

Deployment (Netlify + Supabase)

1) Prepare repository
- Commit your workspace to a GitHub repository. Include the `.gitignore` present in the project. Use clear commits, for example:
	- `chore: initial frontend scaffold`
	- `feat(ui): landing page and demo board`
	- `feat(auth): login page with auth UI stubs`

2) Configure Supabase
- Create a Supabase project and copy the Project URL and anon public key.
- In Netlify (or your CI), add the following environment variables:
	- `VITE_SUPABASE_URL` — your Supabase project URL
	- `VITE_SUPABASE_ANON_KEY` — your public anon key

3) Deploy on Netlify
- In Netlify, create a new site and link your GitHub repository.
- Build command: `npm run build`
- Publish directory: `dist` (also set in `netlify.toml`).
- Add the above environment variables in Site settings → Build & deploy → Environment.
- Trigger a deploy — Netlify will build the Vite app and publish `dist`.

4) Integrate Supabase for backend features
- Use `src/lib/supabase.ts` as a client wrapper to connect to your Supabase project.
- For auth flows (magic link, OAuth, WebAuthn), implement server-side endpoints as needed, or use Supabase Auth where appropriate.

Notes and next steps
- The social OAuth and magic link flows in the front-end are UI placeholders. For production, implement secure server-side flows or use Supabase Auth.
- WebAuthn requires server-generated challenges and validation; implement these using Supabase Functions or a small server.
- To enable multi-device realtime syncing, run a Socket.IO server and set `window.COLLABSPACE_SOCKET_URL` to its URL, or implement a Supabase Realtime/Table replication strategy.

Git and deployment checklist
- Create a repo on GitHub and push the workspace:

```powershell
git init
git add .
git commit -m "chore: initial frontend scaffold"
git branch -M main
git remote add origin https://github.com/<your-org>/collabspace-pro-frontend.git
git push -u origin main
```

- After pushing, follow Netlify's site creation flow and add environment variables.

Contact and support
- If you want, I can scaffold a minimal local backend (Node + Express) to simulate OAuth, Magic Link and a Socket.IO server for local testing. Tell me if you'd like that and I'll add it to this repo.
