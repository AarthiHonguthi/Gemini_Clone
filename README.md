## Gemini-clone (React) — Frontend README

A lightweight Vite + React frontend that demonstrates a small app structure integrating with Google's generative AI client. This README gives a frontend developer a focused, practical guide to run, develop, and extend the project.

## Quick summary

- Frameworks: React (v19), Vite
- Purpose: Frontend demo / clone integrating with a generative AI model through `@google/generative-ai`.

## Requirements

- Node.js (recommended >= 18 LTS)
- npm (or yarn/pnpm) — instructions below use npm
- A Gemini / Google generative API key if you want to call the model from the browser (see config below)

## Install

Open PowerShell and run:

```powershell
# install dependencies
npm install
```

## Available scripts

The project ships with common Vite scripts. From the project root run:

```powershell
# start dev server (hot reloading)
npm run dev

# build production bundle
npm run build

# preview production build locally
npm run preview

# run ESLint check
npm run lint
```

These are defined in `package.json`:

- `dev` -> `vite`
- `build` -> `vite build`
- `preview` -> `vite preview`
- `lint` -> `eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0`

## Environment / Configuration

- The app expects a runtime environment variable for the generative API key: `VITE_GEMINI_API_KEY`.
- This is accessed in the frontend via `import.meta.env.VITE_GEMINI_API_KEY` inside `src/config/gemini.js`.

Example local env (create a `.env` in the project root):

```powershell
# .env
VITE_GEMINI_API_KEY=your_real_api_key_here
```

Security note: Never commit your real API keys to the repository. Use `.gitignore` to omit `.env` files.

## Important files & structure

Top-level layout (relevant files/folders):

```
index.html
package.json
vite.config.js
src/
  App.jsx
  main.jsx
  index.css
  assets/
    assets.js
  components/
    Main/
      Main.jsx
      Main.css
    Sidebar/
      Sidebar.jsx
      Sidebar.css
  config/
    gemini.js        # wrapper around @google/generative-ai usage
  context/
    Context.jsx      # React Context used app-wide
public/
  (static assets)
```

Short descriptions:

- `src/main.jsx` — app entry, ReactDOM.render / createRoot and Context provider wiring.
- `src/App.jsx` — top-level app layout; composes `Main` and `Sidebar` components.
- `src/config/gemini.js` — client helper that reads `import.meta.env.VITE_GEMINI_API_KEY`, initializes `@google/generative-ai`, and exposes `runChat(prompt)`; see it before adding production API logic.
- `src/context/Context.jsx` — shared React context for app state and injection points.
- `src/components/*` — UI components and CSS modules.

## How the Gemini config works (quick)

- `src/config/gemini.js` constructs a `GoogleGenerativeAI` client with the key read from `VITE_GEMINI_API_KEY` and exports an async `runChat(prompt)` helper.
- Keep heavy or sensitive server-side logic on a backend when possible. Calling large-language-model APIs directly from client-side code exposes the key to users unless you use a secure token-exchange / proxy server.

## Development notes & recommended workflow

1. Install and run the dev server (`npm run dev`).
2. Implement components under `src/components`. Use `Main` and `Sidebar` as examples.
3. Keep presentational concerns in `.css` files next to components.
4. If adding calls to `runChat`, consider adding a simple wrapper that rate-limits or delegates to a server endpoint.

## Linting & formatting

- ESLint is already configured in `package.json` scripts.
- To run lint checks:

```powershell
npm run lint
```

If you want Prettier or additional tooling, add it as a devDependency and wire it into your editor.

## Troubleshooting

- Dev server fails to start: make sure Node >= 18, run `npm install` again, then `npm run dev`.
- Missing `VITE_GEMINI_API_KEY` — you will get runtime errors from `src/config/gemini.js` where the API key is read. Add `.env` with the variable and restart dev server.
- React or Vite version conflicts: remove `node_modules` and reinstall (`rm -r node_modules; npm i` in PowerShell use `Remove-Item -Recurse node_modules; npm i`).

## Suggested next steps / improvements

- Move sensitive API calls to a small backend/proxy to hide the API key.
- Add unit tests for utility modules and basic component tests (React Testing Library + vitest).
- Add CI (GitHub Actions) to run lint & build on PRs.

## Contributing

- Fork -> branch -> PR. Keep changes focused and add a short description of what you changed.

## License

This repo currently doesn't include a license file. Add one (for example MIT) if you plan to publish or accept contributions.

---

If you want, I can also:

- add a `.env.example` file and update `.gitignore` to exclude `.env` (recommended),
- add a short CONTRIBUTING.md or GitHub Actions workflow to run lint/build on PRs,
- or add unit test scaffolding with vitest + React Testing Library.

If you'd like any of those, tell me which and I'll implement it next.

# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh
