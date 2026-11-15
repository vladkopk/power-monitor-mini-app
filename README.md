# Power Monitor Telegram Mini App

Static Telegram Mini App frontend for GitHub Pages. Google Apps Script remains the backend and validates Telegram `initData` for every RPC call.

## Files
- `index.html` — Telegram Mini App interface.
- `config.js` — public Apps Script `/exec` endpoint (not a secret).
- `.github/workflows/pages.yml` — GitHub Pages deployment.

## Apps Script installation
1. In the current Apps Script project, replace the main `.gs` source with the supplied updated `TOMZN_Telegram_Bot_PHASE3_MINI_APP_GITHUB_PAGES_BRIDGE_POST.gs`.
2. Create or replace the HTML file named exactly `MiniAppBridge` with the supplied `MiniAppBridge.html`.
3. Keep all existing Script Properties. Confirm these values:
   - `TELEGRAM_WEB_APP_URL` = the existing production `/exec` URL.
   - `TELEGRAM_MINI_APP_PUBLIC_URL` = `https://vladkopk.github.io/power-monitor-mini-app/`
   - `MINI_APP_FRONTEND_ORIGIN` = `https://vladkopk.github.io`
4. Deploy a new version of the existing `TG Hook` Web App. Do not create a new deployment.
5. Run `configurePowerMonitorMiniApp()` only if the Telegram menu button needs to be set again. The verified button should point to GitHub Pages.

## Bridge design
The frontend submits each RPC request through a hidden HTML form to the Apps Script Web App. Apps Script handles `pmBridge=1` before the normal Telegram webhook secret check, then validates Telegram's signed `initData` in `miniAppApi()`. The response HTML runs `google.script.run` and posts the result to the GitHub Pages top-level window. Normal Telegram webhook POSTs keep their original hook-secret path.

Never put Telegram Bot Token, Tuya secrets, Script Properties, or Scriptable keys in this public repository.
