# Node.js homework — Express

Module 1 of the GoIT Node.js course. The implementation is on `01-express`; `main` remains the initial repository branch.

## Run locally

```bash
npm ci
cp .env.example .env
npm run dev
```

`npm start` starts the server with Node.js. `npm run dev` uses nodemon to restart it when source files change.

The server reads `PORT` through dotenv, defaulting to `3000`. An existing environment variable takes priority over `.env`.

## Routes

| Method | Path             | Status | JSON response                                       |
| ------ | ---------------- | ------ | --------------------------------------------------- |
| GET    | `/notes`         | 200    | `{ "message": "Retrieved all notes" }`              |
| GET    | `/notes/:noteId` | 200    | `{ "message": "Retrieved note with ID: <noteId>" }` |
| GET    | `/test-error`    | 500    | `{ "message": "Simulated server error" }`           |
| Any    | An unknown route | 404    | `{ "message": "Route not found" }`                  |

This is an API server. The root URL `/` intentionally returns the required 404 response; open `/notes` to check the deployment.

Middleware runs in order: HTTP logging with pino-http, CORS, JSON parsing, routes, the 404 handler, and the four-argument error handler. Notes are placeholder messages for this module; no database or credentials are needed.

## Checks

```bash
npm run lint
npm run format:check
```

## Deploy on Render

Create a **Web Service** connected to this repository:

- Branch: `01-express`
- Runtime: Node
- Build command: `npm ci`
- Start command: `npm start`
- Instance type: Free
- Health check path: `/notes`

Render provides `PORT`; do not upload `.env` or add the old NoteHub token. Check `/notes`, `/notes/example`, `/test-error`, and an unknown route on the deployed service.

Submit the branch URL `https://github.com/marianamasia/nodejs-hw/tree/01-express` together with the Render service URL after deployment. Wait at least five minutes after pushing before submitting for review.
