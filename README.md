# Power Monitor Telegram Mini App

Static Telegram Mini App frontend for GitHub Pages. Google Apps Script remains the backend and validates Telegram `initData` for every RPC call.

## Files
- `index.html` — responsive Telegram Mini App interface.
- `config.js` — public Apps Script `/exec` endpoint. This URL is not a secret.
- `.github/workflows/pages.yml` — deploys the site to GitHub Pages after pushes to `main`.

## Setup
1. Replace `PASTE_YOUR_APPS_SCRIPT_EXEC_URL_HERE` in `config.js` with the existing production Apps Script Web App URL ending in `/exec`.
2. Do not put Telegram bot tokens, Tuya secrets, API keys, or Script Properties in this repository.
3. In Apps Script, add the supplied `MiniAppBridge.html` file and deploy a new version of the existing `TG Hook` Web App.
4. Set Apps Script Script Properties:
   - `TELEGRAM_WEB_APP_URL` = the existing Apps Script `/exec` URL.
   - `TELEGRAM_MINI_APP_PUBLIC_URL` = `https://vladkopk.github.io/power-monitor-mini-app/`
   - `MINI_APP_FRONTEND_ORIGIN` = `https://vladkopk.github.io`
5. Run `configurePowerMonitorMiniApp()` once from Apps Script.
6. In repository Settings → Pages, select **GitHub Actions** as the build and deployment source if it is not already selected.

The hidden Apps Script iframe provides the server-side bridge. The browser sends Telegram `initData` to Apps Script; the server validates the signature and user allowlist before returning data or changing notification settings.
