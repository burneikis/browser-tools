# browser-tools

Minimal Chrome DevTools Protocol (CDP) scripts for agent-assisted web automation, packaged as a [pi](https://github.com/badlogic/pi-mono) agent skill. Each tool is a small standalone Node script that connects to Chrome on `localhost:9222`.

Based on the browser tools by [Mario Zechner](https://github.com/badlogic), adapted for Linux.

## Requirements

- Linux
- Google Chrome (default: `/usr/bin/google-chrome-stable`)
- Node.js 22.12+
- `rsync` (only for `--profile`)

## Install

As a pi skill:

```bash
git clone https://github.com/burneikis/browser-tools ~/.pi/agent/skills/browser-tools
cd ~/.pi/agent/skills/browser-tools
npm install
```

The agent picks it up from `SKILL.md`. The scripts also work standalone.

## Tools

| Script | Purpose |
|---|---|
| `browser-start.js [--profile]` | Start Chrome with remote debugging on `:9222`. `--profile` copies your Chrome profile (cookies, logins). |
| `browser-nav.js <url> [--new] [--reload]` | Navigate the current tab, or open a new one. |
| `browser-eval.js '<js>'` | Evaluate JavaScript in the active tab (async context). |
| `browser-screenshot.js` | Screenshot the viewport, prints the temp file path. |
| `browser-pick.js '<message>'` | Interactive element picker; returns element info for the clicked elements. |
| `browser-cookies.js` | Print cookies for the active tab. |
| `browser-content.js <url>` | Navigate and extract readable content as markdown (Readability + Turndown). |

## Configuration

| Env var | Default |
|---|---|
| `CHROME_PATH` | `/usr/bin/google-chrome-stable` |
| `CHROME_PROFILE` | `~/.config/google-chrome` |

The automation profile lives in `~/.cache/browser-tools`.

## Security notes

- `--profile` copies your real browser session into `~/.cache/browser-tools`. Anything with access to port 9222 can control that browser and its logged-in sessions.
- `browser-cookies.js` prints cookie values in plain text.

## License

MIT, see [LICENSE](LICENSE).
