## Repo snapshot

- Framework: Vue 3 (single-file components). Entry: `src/main.js` -> mounts `App.vue` to `#app`.
- Dev tooling: Vue CLI (see `package.json` scripts). Run `npm install` then `npm run serve` for dev or `npm run build` for production.

## Where to look first (fast orientation)

- App entry: `src/main.js`
- Top-level layout: `src/App.vue` (imports `./components/HomePage.vue`)
- Main UI pieces: `src/components/HomePage.vue` and `src/components/SearchBox.vue` — these show the project's component patterns.
- Static / HTML template: `public/index.html` (htmlWebpackPlugin title and favicon location)
- Build/dev server customization: `vue.config.js` (devServer host/ws settings and a custom file-loader rule for `.ico` files)
- Service worker: `registerServiceWorker.js` (PWA integration via `@vue/cli-plugin-pwa`)

## Build / dev / debug commands (explicit)

- Install deps: `npm install`
- Start dev server (hot reload): `npm run serve` (runs `vue-cli-service serve`)
- Build for production: `npm run build` (runs `vue-cli-service build`)

Notes about dev server: `vue.config.js` sets `devServer.host` to `0.0.0.0`, `port: 8080`, and a custom websocket URL (`ws://0.0.0.0:8080/ws`). The project uses `allowedHosts: 'all'` which allows remote/LAN access.

## Project-specific patterns & conventions

- Single-file components: SFCs live in `src/components/`. Follow the existing structure: template -> style -> script, and prefer `scoped` styles where components isolate layout (see `SearchBox.vue`).
- CSS assets: component styles sometimes import `@/assets/HomePage.css` (uses the `@` alias to `src/`). Use `@/assets/...` for in-repo assets.
- Icons & file loader: `vue.config.js` defines a `file-loader` rule for `.ico` that outputs to `assets/`. When adding `.ico` files, place them under `src/assets/` and reference via `@/assets/name.ico` or update the public folder if they must remain static.
- Service worker / PWA: `registerServiceWorker.js` is present and `@vue/cli-plugin-pwa` is in devDependencies. Be mindful when modifying index.html or the service worker registration.

## Integration points & external dependencies

- External deps (from `package.json`): `vue` (3.x), `core-js`, `register-service-worker`. Dev deps include Vue CLI plugins.
- Network / runtime: components open external URLs (e.g., `SearchBox.vue` opens search engine URLs with `window.open`). Treat outbound navigation as a side-effect and avoid changing it without explicit tests.

## Examples from the codebase (copyable patterns)

- Dev server start: `npm run serve`
- Example component pattern (SearchBox): uses `v-model` for inputs, `mounted()` to set defaults (`selectedEngine = engines[0]`), and a `search()` method which `encodeURIComponent()` the query before `window.open()`.

## Known code smells / things an agent should notice

- `src/components/HomePage.vue` currently includes `head`/`body` tags and an absolute Windows path in an `<img src="C:\\Users\\...">`. These are discoverable issues; do not replace or move the asset without asking the human owner. Prefer using `@/assets/...` or `public/` for shared images.

## What NOT to change without confirmation

- `vue.config.js` devServer host/ws settings (used for remote development). Changing them can break the developer's local access flow.
- Service worker registration (`registerServiceWorker.js`) and PWA plugin configuration.
- Any hard-coded absolute filesystem paths — these are likely user-specific.

## Quick checklist for PRs from an agent

1. Preserve `package.json` scripts unless adding equivalent ones and include doc updates in `README.md`.
2. Run `npm run serve` locally to validate dev behavior if making UI/asset changes.
3. When adding static assets: prefer `src/assets/` with `@/assets/...` or `public/`; update `vue.config.js` only if absolutely required.
4. Avoid modifying service worker or PWA manifest without tests and an explanation in the PR.

## If you need more context

- Open `src/components/SearchBox.vue` to see input binding and navigation examples.
- Open `vue.config.js` for bundler and dev-server specifics.
- If you plan to change build or CI behavior, ask for the preferred Node/npm versions (not present in repo).

---

If any section is unclear or you want the file to contain more examples (for example: common refactors or unit test hooks), tell me which area to expand and I will iterate.
