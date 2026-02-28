# AGENTS.md

## Cursor Cloud specific instructions

### Project overview

bolt.diy is a Remix-based AI-powered web development platform. It is a single web application with no external database or backend services — all persistence is client-side (IndexedDB) and code execution runs in-browser via StackBlitz WebContainers.

### Required tooling

- **Node.js 20.15.1** (per `.tool-versions`)
- **pnpm 9.4.0** (per `packageManager` field in `package.json`)

### Running the dev server

```bash
pnpm run dev
```

Starts the Remix/Vite dev server on **port 5173**. The `dev` script first runs `pre-start.cjs` (prints version info) then launches `remix vite:dev`.

### Key commands

See `package.json` `scripts` section. Summary:

| Command | Purpose |
|---------|---------|
| `pnpm run dev` | Start development server (port 5173) |
| `pnpm test` | Run Vitest test suite |
| `pnpm lint` | Run ESLint on `app/` |
| `pnpm lint:fix` | Auto-fix lint + Prettier |
| `pnpm typecheck` | Run `tsc` type checking |
| `pnpm run build` | Production build |

### Non-obvious notes

- The Vitest process hangs briefly after tests pass (known upstream issue with Vite server cleanup). Tests still report correctly — wait for the exit code.
- The pre-commit hook (`.husky/pre-commit`) runs both `pnpm typecheck` and `pnpm lint`. Both must pass before any commit.
- API keys for LLM providers are **not required** for the dev server to start or for tests/lint/typecheck to pass. They are only needed for actual AI chat functionality and can be entered via the UI at runtime or set in `.env.local`.
- Chrome 129 has a known issue with Vite dev mode; the app includes middleware that blocks it. Use Chrome Canary or any other modern browser for local testing.
- `.env.example` documents all supported environment variables. Copy to `.env.local` and fill in keys as needed. Never commit `.env.local`.
