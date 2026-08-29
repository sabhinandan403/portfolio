# Portfolio — project instructions

Personal portfolio site for **Abhinandan Kumar**, Data Engineer.
Static, single file, no build step. `index.html` is the whole site.

**v1 design is locked.** The visual system below was approved and should not be
redesigned. Add to it; don't replace it. If a change would alter the palette,
the typefaces, or the lineage-rail concept, ask first.

## Repo shape

```
index.html                  markup + styles + script, all inline
Abhinandan_Kumar_CV.pdf     linked by the Download CV button and the contact list
README.md                   run + deploy instructions
CLAUDE.md                   this file
```

There is no package.json, no bundler, no framework, and none should be added.
The site must keep working when opened as a `file://` URL with no network.

## Design system (locked at v1)

**Concept — lineage.** The page reads as a directed flow, the way a data
pipeline does. The sticky left rail is a lineage spine: nodes fill as sections
pass. It doubles as section nav. On screens under 900px it collapses to a
horizontal scrolling tab strip with a progress underline.

**Colour.** Cool graphite neutrals with a single warm copper signal. Every
colour is a CSS custom property in `:root`. There is no second accent — copper
is the only saturated colour on the page, and that restraint is deliberate.

| token | light | dark |
|---|---|---|
| `--ground` | `#FCFCFA` | `#0F1216` |
| `--surface` | `#F1F2EE` | `#161A1F` |
| `--ink` | `#15181C` | `#E9EAE5` |
| `--muted` | `#666E78` | `#8F98A2` |
| `--rule` | `#DCDED8` | `#252B32` |
| `--signal` | `#A8481A` | `#E07A33` |

**Theming is three-state.** The palette is defined three times and all three
must stay in sync:

1. bare `:root` — the complete light palette
2. `@media (prefers-color-scheme: dark) { :root:not([data-theme="light"]) }`
3. `:root[data-theme="dark"]` — so the manual toggle wins

Never declare a colour only inside a media query or a `[data-theme]` block.
Most visitors arrive with no `data-theme` attribute stamped at all, and a
colour defined only in those blocks will not apply to them.

**Type — three faces, fixed roles.** Do not introduce a fourth.

- `--f-display` **Archivo** — headings, name, company names, metric numbers
- `--f-body` **Source Serif 4** — prose and bullet text
- `--f-mono` **JetBrains Mono** — eyebrows, rail labels, stack chips, the
  schema table, metric captions, dates, footer

Google Fonts is the only external request. Every stack has a real fallback so
the page holds up offline.

**Structure.** Section eyebrows are lowercase mono identifiers (`profile`,
`experience`, …) — they read as schema names, matching the rail. Skills are set
as a **schema table** (`dl.schema`), mono field names against mono values, not
as a tag cloud or progress bars. No skill-percentage bars, ever.

## Content rules

Everything on the page is drawn from the CV and must stay defensible. Abhinandan
prefers honest, understated claims over inflated metrics — no rounding up, no
invented percentages, no "10x" language. If a number can't be traced to
something he actually did, it doesn't go on the page.

The three hero metrics are `3 yrs`, `10,000+` daily telemetry points, and
`7s → 45ms`. All three trace to specific work in the CV.

## Open items

- **Projects section** is a deliberate placeholder (`.slot` inside
  `<section id="projects">`). Case-study cards replace it when the project
  list arrives. Match the existing type scale and the copper accent; no new
  colours.
- **Location** in `.rail-foot` currently reads "Bengaluru · India" and needs
  confirming.
- GitHub and LinkedIn handles came from the CV and have not been verified to
  resolve.

## Working on this

Edit `index.html` directly. After any change, check both themes and a narrow
viewport before committing — the three-state theming and the rail's mobile
collapse are the two things that break silently.
