# Fylo — Landing Site

Scroll-driven marketing site for Fylo. Single static `index.html` (all CSS + JS inline)
served by a tiny Node server that supports HTTP range requests (needed so the hero
video can be scrubbed as you scroll).

## Run it locally

Requires [Node.js](https://nodejs.org) (any recent version — no dependencies to install).

```bash
node server.js
```

Then open **http://localhost:8000**.

> Use this server, not Python's `http.server` or VS Code Live Server — the hero video
> scrubbing needs byte-range support, which `server.js` provides and most simple static
> servers don't.

## Editing

Everything lives in **`index.html`** — markup, styles (in one `<style>` block), and
scripts (in one `<script>` block at the bottom). No build step, no framework. Edit and
refresh the browser.

Rough structure of the page, top to bottom:

| Section            | What it is                                              |
|--------------------|---------------------------------------------------------|
| `nav`              | Fixed top bar with the `fylo.` wordmark                 |
| `.stage`           | Pinned hero — text cross-fades beside the spinning hexagon as you scroll |
| `.employees`       | The 2×2 grid of AI-employee cards (pop-in on scroll)    |
| `.demo`            | The mock product dashboard (animated sparklines + count-up stats) |

### Common tweaks

- **Hero video** — `assets/hexpoo-teal5.mp4`, scrubbed by scroll. Swap the file (keep the
  name, or update the `<video src>`).
- **Card pop animation** — `@keyframes ecardPop` and the `.emp-cards .ecard:nth-child(n).in`
  `animation-delay` rules.
- **Hero text cross-fade timing** — the `heroFade` / `empFade` windows in the `onScroll()` function.
- **Dashboard numbers / sparklines** — the `.stat` blocks in the `.demo` section; numbers
  count up from `data-target`, sparkline shapes are the SVG `d="..."` paths.

## Files

```
index.html        the whole site
server.js         dev server with range support (run this)
assets/
  hexpoo-teal5.mp4  hero hexagon video (scrubbed on scroll)
  hexagon.png       favicon
```

## Notes / honesty constraints

- The dashboard is a **visual mockup** — the toggles, dropdown, and "Live" pill are
  decorative, and the numbers are illustrative, not real data.
- Google Reviews is the only live employee; keep claims consistent with what actually ships.
