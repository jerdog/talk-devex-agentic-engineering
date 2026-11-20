# Developer Experience in the Age of Agentic Development

Conference talk by Jeremy Meiss, built with [Slidev](https://sli.dev) and the WWT theme (`slidev-theme-wwt`).

## Decks

| File | Length | Notes |
| --- | --- | --- |
| [slides.md](slides.md) | 45 min | The full talk. |
| [slides-25min.md](slides-25min.md) | 25 min | The short cut. Shares most slides and notes with the 45-minute deck. |
| `slides-old.md`, `slides-25min-old.md` | | Superseded versions, kept for reference. |
| `old_content/` | | Source material from the earlier DevEx talk. |

[global-top.vue](global-top.vue) holds the deck-wide styles shared by both decks (footer, logos, click reveal).

## Run

```sh
pnpm install
pnpm dev                              # slides.md (45 min)
pnpm exec slidev slides-25min.md      # the 25-minute deck
pnpm build                            # static build
pnpm export                           # PDF/PNG export
```

## Speaker notes

- A note gives the overview of the slide (what it means and why it matters). It does not read the cards or steps out one by one, except for a quote or a point that needs making.
- `[click]` in a note marks where the presenter clicks. Each cue is the start of the part of the note that goes with the next click.

## Custom frontmatter

Slidev and the WWT theme provide their own frontmatter (`layout`, `title`, `clicks`, `reveal`, `hideBadge` and so on). This section covers the options this talk adds or uses in a specific way.

### Deck-wide (first slide's frontmatter)

| Key | Value | What it does |
| --- | --- | --- |
| `htmlAttrs: data-click-reveal` | `"off"` | Content that a layout or `v-click` would hide until clicked is always visible. Clicks still advance, so the `[click]` cues in the notes step as usual. Remove the line (or set `"on"`) to reveal content on click again, deck-wide. |

The rule behind it is in [global-top.vue](global-top.vue):
`html[data-click-reveal="off"] .slidev-layout:not(.reveal-on-click) .slidev-vclick-hidden`.

### Per slide

| Key | Value | What it does |
| --- | --- | --- |
| `clicks` | number | Total click steps for the slide. **Set it to the number of `[click]` cues in the slide's notes.** Without it, a slide with no click-revealed content has no steps, so the cues have nothing to advance. Use `0` when the slide has layout reveals (stats, process, timeline) but no cues. |
| `class: reveal-on-click` | | Opts this slide out of `data-click-reveal: "off"`, so its content is revealed on click. Set `clicks` to the number of reveal steps, and keep the slide's own CSS from forcing the content visible. |
| `class: show-top-logo` | | Brings back the top-left WWT logo on this slide. It is hidden on every slide by default (the footer logo stays). |

### Click combinations

| You want | `data-click-reveal` | Slide frontmatter |
| --- | --- | --- |
| Content always visible, clicks step the notes | `"off"` | `clicks: N` (N = cues in notes) |
| Content always visible, no clicks needed | `"off"` | `clicks: 0` |
| Content revealed on click | `"off"` | `class: reveal-on-click` and `clicks: N` |
| Content revealed on click everywhere | removed | `clicks: N` |

To check a slide, count the `[click]` cues in its note and compare with `clicks`. They should match.

### Deck-wide behaviour set in global-top.vue

- The slide title is hidden in the footer (the page number stays).
- The top-left WWT logo is hidden on every slide (see `show-top-logo` above).
- The corner badge reads `public/images/badge.png`. That file does not exist yet, so set `hideBadge: true` (as the first slide does) or add the image.

## Slide conventions

- **Source lines:** where a layout has no source slot, a `Source:` line goes in the slide body, or a `.wwt-stats::after` rule pins one above the footer on stats slides.
- **Charts:** image-feature slides with charts use `background-size: contain` so the whole chart shows.
- **Single statement:** one-line statements use `layout: section` with a `title`.
