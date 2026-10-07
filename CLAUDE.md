# Cube Counters!

A kid-friendly calculator where every number is a friendly robot carrying counting cubes. It has a calculator mode (robots animate +, −, ×, ÷), a **Challenge** mode that earns stars, **Prizes** unlocked by stars (hats, robot colors, birds), and **Build a Robot**. See README.md for the full feature list.

## Audience
The players are young kids. Keep everything simple, friendly and safe: big tap targets, short cheerful words, no scary or negative messages, no ads, links out or data collection. Wrong answers get gentle hints, never a "fail" feel.

## How the project is laid out
- **The app is `index.html`.** All HTML, CSS and JavaScript live there, with no build step and no dependencies.
- `index.html` is about 190 KB, with some assets embedded inline. Don't read or rewrite these lines whole; search around them:
  - lines 19–20: favicon and apple-touch-icon as base64 PNGs
  - lines 22–23: the Fredoka font as base64 woff2
- `voice.json` (about 2.4 MB) is a JSON map of base64 MP3 voice clips (British voice, made with Chatterbox). The page fetches it after it appears. If the page has an inline `<script id="voice-data">` block, that wins, which keeps older offline copies working. Never read `voice.json` whole.
- The `<head>` holds the search and social tags (title, description, canonical, Open Graph, JSON-LD). The `.about` section sits just below the first screen for search engines and grown-ups, and is hidden in the desktop apps (`.is-app` on `<body>`, set from an Electron user-agent check).
- The app code is the large `<script>` near the end of `<body>`.
- `robots.txt` and `sitemap.xml` are for search engines. Update `lastmod` in `sitemap.xml` when the page changes a lot.
- `icon.png` is the app icon used by README.md.
- `CNAME` holds the custom domain.

## Hosting
- Hosted on GitHub Pages at **cubecounters.com**. Pushing to `main` publishes it.
- **Never edit or delete the `CNAME` file.** It's what keeps cubecounters.com pointed at the site.
- The Windows and Mac download apps load the live website, so a broken push breaks them too.
- Push `voice.json` before an `index.html` that depends on it. Any app rebuild must bundle `voice.json` next to `index.html`.

## Saved progress (don't break it)
Progress is saved in `localStorage` through the `store` helper in `index.html` (`store.get` / `store.set`), with every key prefixed `cc.`:

| Key | Holds |
| --- | --- |
| `cc.stars` | star count (number), which unlocks prizes |
| `cc.level` | chosen Challenge level id, such as `add10` |
| `cc.timed` | 5-second timer on or off |
| `cc.design` | Build a Robot design: `{ n, color, hat, colors, brush }` |

Rules:
- Never rename or remove these keys, or change what their values mean. Kids would lose their stars and robots.
- New saved data gets a new `cc.` key. If a value's shape must change, read the old shape too and fill in defaults, like `cc.design` does with `Object.assign`.
- Don't raise the star cost of a prize that already exists, since that would take away prizes kids have earned.

## Work rules
- Track bugs and ideas as GitHub issues (`gh issue create`). Use the templates in `.github/ISSUE_TEMPLATE`.
- Fix one issue at a time.
- Keep commits small, one change per commit.
- End commit messages with `(fixes #N)` for the issue they fix.
- Before committing, tell me how to test the change: what to open, what to tap, and what I should see.
- Update README.md whenever a feature is added, changed or removed.

## Testing
Open `index.html` in a browser; there's nothing to build. Check it on a short laptop or Chromebook screen and a phone-width screen as well, since the layout changes on short screens. To test prizes, set `localStorage['cc.stars']` in the browser console, and restore your real value afterwards.
