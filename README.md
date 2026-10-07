# AetherState

A real-time collaborative platform that synchronizes state between human users and AI agents using Yjs CRDTs over a WebRTC mesh, with Redis + PostgreSQL persistence and JWT access control.

## Features

- **Yjs CRDT engine** — shared-document state with conflict-free merging (`bridge-server.ts`, `crdt-callback.ts`).
- **WebRTC mesh networking** — peer-to-peer document sync via a signaling server (`webrtc-signaling.ts`).
- **WebSocket connection pooling** — managed client connections (`websocket-pool.ts`).
- **Dual-tier persistence** — Redis as hot cache, PostgreSQL as durable store for snapshots and operation history.
- **JWT-based access control** — document-level authorization with asymmetric RS256 signing.
- **MCP server** (`mcp-server.ts`) — MCP gateway exposing the platform to AI agents, with rate limiting, Zod input validation, Winston audit logging, and Helmet/CORS headers.
- **Docs** — `ARCHITECTURE.md`, `IMPLEMENTATION_SUMMARY.md`, `CHANGELOG.md`, `CONTRIBUTING.md`, MIT license.

## Tech stack

Node.js ≥ 18, TypeScript 5.3, Express 4, `ws`, Yjs 13, `jsonwebtoken`, Redis 4, `pg`, Zod, Winston, Helmet, LangChain.

## Getting started

```bash
npm install
cp .env.example .env   # fill in JWT_PUBLIC_KEY, DATABASE_URL, Redis settings
npm run build
npm start              # or start:mcp / start:bridge / start:signaling
```

`docker-compose.yml` provisions Redis 7, PostgreSQL 16, and the MCP/bridge/signaling services. RSA keys for RS256 are generated with `openssl genrsa -out private.pem 2048` (see `.env.example`).

## Project structure

```
├── bridge-server.ts      # Yjs CRDT document state + persistence + broadcasting
├── mcp-server.ts         # MCP gateway (auth, rate limiting, audit logging)
├── webrtc-signaling.ts   # WebRTC peer signaling
├── websocket-pool.ts     # WebSocket connection management
├── crdt-callback.ts      # CRDT change callbacks
├── index.ts              # entry point
├── docker-compose.yml    # Redis, Postgres, service containers
└── .env.example          # required environment configuration
```

## Status

Functional codebase with real npm scripts and containerized services. The package.json repository URLs still point at placeholder `github.com/yourusername/aetherstate` addresses, and the README header links a YouTube short that is not described anywhere in the repo.
