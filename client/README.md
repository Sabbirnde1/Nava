# Client (React)

This folder contains the React frontend for `DEX_Nova_MVP` (Create React App).

Quick summary:
- Development port: `3006` (see `client/package.json`)
- The `proxy` field in `client/package.json` forwards API requests to `http://localhost:4000` in development

## Prerequisites

- Node.js (>=14) and npm

## Install

From the project root:

```bash
npm install --prefix client
# or
cd client && npm install
```

## Available scripts

From project root:

```bash
npm run client         # start the client dev server (runs `npm start` inside client/)
```

From inside `client/`:

```bash
npm start              # start dev server (Windows: port set via package.json)
npm run build          # build production bundle
npm test               # run tests
npm run analyze        # analyze build bundles (optional)
```

## Environment & proxy

- Development uses the `proxy` in `client/package.json` to forward API calls to the backend at `http://localhost:4000`.
- For production, prefer using an explicit `REACT_APP_API_URL` env var at build time rather than relying on `proxy`.

Example (build-time env):

```bash
REACT_APP_API_URL=https://api.example.com npm run build
```

## Build & serve for production

```bash
# build the frontend
npm run build --prefix client

# serve the build folder with a static server (example: serve)

serve -s client/build -l 3006
```

## Troubleshooting

- If the client can't reach the API, confirm backend is running on `http://localhost:4000` or update `proxy` in `client/package.json`.
- On non-Windows shells (WSL/macOS), set `PORT=3006` before starting the dev server.

## Next steps I can do for you

- Add `client/.env.example` with `REACT_APP_*` variables.
- Replace `proxy` usage with `REACT_APP_API_URL` in the frontend code and add docs.

---

If you'd like a `client/.env.example` generated, tell me the variables you'd like included (e.g. `REACT_APP_API_URL`, `REACT_APP_MAP_KEY`).
