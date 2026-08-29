# Portfolio — project instructions

Personal portfolio site for **Abhinandan Kumar**, Data Engineer.
Static, single file, no build step. `index.html` is the whole site.

**Current: v1.2.** The visual system below is approved. Add to it; don't
redesign it. If a change would alter the palette, the typefaces, the uppercase
rule or the run-strip signature, ask first.

## Repo shape

```
index.html                  markup + styles + script, all inline
fonts/                      self-hosted woff2 — no external font request
Abhinandan_Kumar_CV.pdf     linked by Download CV and the contact list
README.md                   run + deploy instructions
CLAUDE.md                   this file
```

No package.json, no bundler, no framework, and none should be added. The site
must keep working opened as a `file://` URL with no network — which is why the
fonts are in the repo rather than loaded from Google Fonts.

## Design system (v1.2)

**Concept — lineage.** The page reads as a directed flow, the way a pipeline
does. The sticky left rail is a lineage spine whose nodes fill as sections
pass; it doubles as section nav. Under 900px it collapses to a horizontal
scrolling tab strip with a progress underline.

**Colour — warm white ground, two accents with distinct meanings.**
The ground is a warm white, deliberately *not* the cream (#F4F1EA-ish) that
reads as AI-generated. Dark mode is a warm espresso black, not a blue-black.

| token | light | dark |
|---|---|---|
| `--ground` | `#FBF8F2` | `#15110E` |
| `--surface` | `#FFFFFF` | `#1D1815` |
| `--surface-2` | `#EFEAE0` | `#262019` |
| `--ink` | `#201914` | `#F2EEE9` |
| `--ink-2` | `#4A4139` | `#C9C0B6` |
| `--muted` | `#7C736A` | `#948A7E` |
| `--rule` | `#E5DFD3` | `#2C2520` |
| `--rule-2` | `#CDC5B6` | `#3D342C` |
| `--hot` (tangerine) | `#D9541A` | `#FF8A3D` |
| `--cool` (teal) | `#0B6558` | `#45B3A3` |

**The two accents mean different things. Keep this rule.**

- **Tangerine** = energy and attention. The surname, eyebrows, heading sweeps,
  bullet dashes, the primary button, the active rail node.
- **Teal** = verified, resolved, it worked. Outcome callouts, the "all green"
  indicator, green cells in the run strip, the arrow in `7s → 45ms`, ghost
  button hover.

A third colour is not available. If something needs to stand out and is
neither energy nor outcome, it doesn't need to stand out.

**Theming is three-state.** The palette is defined three times and all three
must stay in sync:

1. bare `:root` — the complete light palette
2. `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }`
3. `:root[data-theme="dark"]` — so the manual toggle wins

Never declare a colour only inside a media query or a `[data-theme]` block.
Most visitors arrive with no `data-theme` stamped at all.

**Type — three faces, fixed roles. Do not add a fourth.**

- `--f-display` **Bricolage Grotesque** — headings, name, company names, metrics
- `--f-body` **Newsreader** — prose and bullet text
- `--f-mono` **JetBrains Mono** — eyebrows, rail labels, chips, schema table,
  labels, dates, buttons, footer

**The uppercase rule.** Uppercase everything that is six words or fewer and
structural: eyebrows, `h2`, `h3`, rail labels, buttons, company names, chips,
field names, credential labels, the footer. **Sentence case for the hero thesis
and all body prose** — uppercase destroys word-shape recognition and makes long
lines measurably harder to read. Do not "fix" the prose by capitalising it.

Uppercase always carries letter-spacing (`.11em`–`.2em` depending on size).

**Signature — the run strip.** A row of uniform-height cells under the hero
thesis, opacity varying, a few teal for green runs, breathing on a staggered
loop. It's the visual language of a task-run history, which is what Abhinandan
actually looks at daily. It is **abstract and decorative** — it must never be
captioned or framed as real data, and no numbers attach to it. It's generated
from a seeded PRNG so it renders identically every load.

**Motion.** A staggered hero reveal on load, the run strip breathing, a
tangerine underline sweeping under each `h2` as it enters the viewport, hover
lifts on buttons, a padding shift on contact rows. All of it disabled under
`prefers-reduced-motion`. Resist adding more — scattered animation is what
makes a page read as generated.

## Content rules

Everything on the page traces to the CV and must stay defensible. Abhinandan
prefers honest, understated claims over inflated metrics — no rounding up, no
invented percentages, no "10x" language. If a number can't be traced to
something he actually did, it doesn't go on the page.

The three hero metrics are `3 yrs`, `10,000+` daily telemetry points, and
`7s → 45ms`. All three trace to specific work.

## Case studies — the pattern for the Work section

The `#projects` section holds a placeholder until project material arrives.
Each case study follows this shape, which comes from IxDF's portfolio guidance
(show thinking, not artifacts; results before detail):

1. **Hook** — what it was, who it was for, Abhinandan's actual role
2. **Problem** — what was broken before
3. **What got built** — architecture and stack
4. **The decision worth defending** — where two options were reasonable and
   why he picked one. This is the highest-value part; give it room.
5. **What went wrong and how he found it** — iteration beats polish
6. **Outcome** — pulled out in a teal `.outcome` callout so a skimming reader
   gets the result without reading the paragraph

Three or four projects maximum. The strongest one goes first.

## Open items

- **Project material** for the Work section — the blocker on finishing v1.2.
- **Location** in `.rail-foot` says "India"; a city was never confirmed.
- GitHub and LinkedIn handles came from the CV and have not been verified to
  resolve.

## Working on this

Edit `index.html` directly. After any change check both themes and a narrow
viewport before committing. The three things that break silently:

1. a colour defined only inside a media or `[data-theme]` block
2. the mobile rail — it's a flex item that needs `width:100%; min-width:0`
   on `.rail > div`, or centred overflow pushes the first tab off-screen
3. selector specificity between `.job`, `.stream` and `section` padding
