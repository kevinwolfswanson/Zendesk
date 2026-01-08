# Repository Guidelines

## Project Structure & Module Organization

- `apps/cxone-lookup-app/` — Zendesk private app that polls CXOne and sets the ticket requester.
- `apps/promo-lookup-app/` — Zendesk private app for promo/source offer lookup.
- `lambda/cxone-bridge/` — AWS Lambda bridge used by the CXOne app (`index.js`).
- App assets live under each app’s `assets/` folder; localization strings live in `translations/`.

## Build, Test, and Development Commands

This repo does not include a unified build system. Use app- or Lambda-specific tools:

- Zendesk apps (run locally): `zcli apps:server` from within an app folder.
- Package a Zendesk app: `zcli apps:package` from the app folder (produces a ZIP in `tmp/`).
- Lambda deploy: zip the contents of `lambda/cxone-bridge/` and update the AWS Lambda code (see the AWS console or CLI).

## Coding Style & Naming Conventions

- Use 2-space indentation for JSON and HTML in apps.
- Use 2-space indentation for JavaScript in the Zendesk apps and Lambda.
- Keep file and folder names lowercase with hyphens (e.g., `cxone-lookup-app`).
- Prefer descriptive function names (e.g., `getActiveCall`, `findRequesterByPhone`).

## Testing Guidelines

There is no test harness in this repository. Validate changes via:

- Zendesk app behavior in Agent Workspace (new ticket + active CXOne call).
- Lambda responses with live CXOne calls (expects `200` with phone or `204` when idle).

## Commit & Pull Request Guidelines

- Use short, imperative commit messages (e.g., `Fix requester guard logic`, `Add API key support`).
- PRs should include: summary of changes, deployment impact (Zendesk app/Lambda), and any manual test notes.
- Attach screenshots only if UI changes are visible in the agent workspace.

## Security & Configuration Tips

- Do **not** commit credentials. Secrets are provided via AWS Lambda environment variables.
- Zendesk app settings (bridge URL, API key) are configured in the Zendesk admin UI.
