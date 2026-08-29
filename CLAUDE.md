# Portfolio — project instructions

Personal portfolio site for **Abhinandan Kumar**, Data Engineer.
Static, single file, no build step. `index.html` is the whole site.

**Current: v1.8.** The visual system below is approved. Add to it; don't
redesign it. If a change would alter the palette, the typefaces, the uppercase
rule or the lineage-diagram signature, ask first.

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

## Design system (v1.8)

**Concept — lineage.** The page reads as a directed flow, the way a pipeline
does. The sticky left rail is a lineage spine whose nodes fill as sections
pass; it doubles as section nav. Under 900px it collapses to a horizontal
scrolling tab strip with a progress underline.

**Colour — warm white ground, two accents with distinct meanings.**
The light ground is a warm white, deliberately *not* the cream (#F4F1EA-ish)
that reads as AI-generated. The dark ground is the cool graphite carried over
from v1 — Abhinandan chose it over a warm espresso black. Warm accents on a
cool dark ground is the intended tension; don't "correct" it to match the
light theme's warmth.

| token | light | dark |
|---|---|---|
| `--ground` | `#FBF8F2` | `#0F1216` |
| `--surface` | `#FFFFFF` | `#161A1F` |
| `--surface-2` | `#EFEAE0` | `#1E242A` |
| `--ink` | `#201914` | `#E8E9E6` |
| `--ink-2` | `#4A4139` | `#BFC5CC` |
| `--muted` | `#7C736A` | `#949CA6` |
| `--rule` | `#E5DFD3` | `#252B32` |
| `--rule-2` | `#CDC5B6` | `#39414A` |
| `--hot` (tangerine) | `#D9541A` | `#FF8A3D` |
| `--cool` (teal) | `#0B6558` | `#45B3A3` |

**The two accents mean different things. Keep this rule.**

- **Tangerine** = energy and attention. The surname, eyebrows, heading sweeps,
  bullet dashes, the primary button, the active rail node.
- **Teal** = verified, resolved, it worked. Outcome callouts, the consumer
  boxes and outbound packets in the hero diagram, the arrow in `7s → 45ms`,
  ghost button hover.

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

**Two exceptions, both deliberate:** the hero `h1` — his name — stays title
case, because a name is a name and not a label. And the eyebrow directly above
it is the only uppercase element allowed to sit against it.

Uppercase always carries letter-spacing (`.11em`–`.2em` depending on size).

**Signature — the lineage diagram.** An inline SVG under the hero thesis:
three sources fan in, the middle narrows to COLLECT → TRANSFORM → TRUSTED DATA,
and it fans back out to dashboards, reports and applications. Packets travel
the actual curved paths via `animateMotion` — tangerine going in, teal coming
out, so the colour system carries the story.

**Its labels are written for a non-technical reader.** Abhinandan asked for
this specifically: recruiters and HR see the site too. So the box labels are
plain language (DEVICE DATA, BUSINESS DATA, COLLECT, TRANSFORM, TRUSTED DATA,
DASHBOARDS, REPORTS, APPLICATIONS) with the stack in smaller muted type
underneath (IOT TELEMETRY, SQL SERVER, COPY INTO, DBT MODELS, FACTS + DIMS,
POWER BI…). Three group captions narrate it: DATA COMES FROM / WHAT I BUILD /
SO PEOPLE CAN DECIDE. **Do not swap the plain labels for jargon** — the
sub-captions exist so engineers still get the detail.

Mechanics worth knowing: packets carry `visibility="hidden"` plus a `<set>` at
their own `begin`, or SVG parks them at 0,0 until they start. The diagram is
600px minimum width inside a horizontally scrolling `.flow`; `.flow-wrap` fades
its right edge while more can be scrolled, toggled from JS on scroll, resize
and `document.fonts.ready`.

**Motion.** A staggered hero reveal on load, packets travelling the diagram, a
tangerine underline sweeping under each `h2`, hover lifts on buttons, a padding
shift on contact rows. All of it disabled under `prefers-reduced-motion`.
Resist adding more — scattered animation is what makes a page read as
generated.

**The heading sweep re-arms.** The observer toggles `.swept` on entry *and*
off on exit rather than unobserving, so the sweep replays every time a section
is revisited — Abhinandan asked for this explicitly. It depends on the
transition living on `.swept::after` and **not** on the base `h2::after` rule:
removing the class takes the transition with it, so the bar snaps back to zero
off-screen instead of un-sweeping in view. If you ever move that `transition`
declaration up to the base rule, the reset becomes visible and looks broken.

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

## Open items — pick up here

The Work section is **built** — four case studies, written only from material
Abhinandan supplied, each with a defensible call and an outcome.

- **Confidentiality — the standing rule.** He sent a real product screenshot
  (device IDs, room names) and a screenshot of his own code-analysis session
  naming internal modules and cache sources. **None of that is on the site and
  none of it goes on it.** The cache case study describes the mechanism — Kafka
  CDC, event-driven, no scheduled refresh — without naming files, libraries or
  subscribed sources. The heat map is a recreation with invented data, labelled
  as such on the page. Keep both that way.
- **The phone number is gone and stays gone.** As of v1.8 this repo is a
  public artefact: the URL goes on his LinkedIn and his resume. No phone number
  on the page, and none in the CV committed here. `build_cv.js` takes
  `PUBLIC=1` to drop it; the private build that keeps it is emailed to
  recruiters directly and **must never be committed**. After any change to the
  contact list or the CV, grep the repo (excluding `.git`) for his phone number
  and expect no matches. Only `index.html`, `fonts/`, the CV and `og-image.png`
  are published; the markdown files stay out of the deploy.

Settled: **DE resume is the canonical framing.** **3 years** experience — career
started July 2023, so the hero metric is right and the full-stack CV's "2+" is
the stale one. **Bangalore**, open to relocating, prefers remote or hybrid.
Contact links display shortened text but point at the real profiles
(`linkedin.com/in/abhinandan-kumar-611a64192`, `github.com/sabhinandan403`) —
deliberate, don't "fix" the display strings to match.

## The heat map figure

Inside case study three. A recreated day: 24 hours × four 15-minute cells, the
shading a **sequential ramp of the accent** — one hue, light to dark — because
it encodes magnitude (motion count against thresholds), not category. That's
why it doesn't need a third colour and mustn't get one.

The data is invented and hardcoded as a 96-character string in the renderer;
`x` marks a no-data gap, drawn with a hatch pattern. The legend is required —
it's a magnitude encoding — and the caption on the page says it is a recreation
and not the product UI. **Do not replace it with the real screenshot.**

## Deploying — live

**Live at https://abhinandan-kumar.netlify.app** — repo
`github.com/sabhinandan403/portfolio` (public, branch `main`), linked to
Netlify with auto-publishing on. **A push to `main` redeploys the site.** No
manual upload step; `netlify.toml` sets publish `.` and an empty build command.

Netlify was chosen over GitHub Pages because a Pages user site would be
`sabhinandan403.github.io` — his handle, not his name, and this URL goes on a
resume. If he buys a domain later, point it at the same project.

`SITE_URL` is already replaced throughout `index.html` with the live origin.
**If the site ever moves, those five meta tags must be updated** (canonical,
`og:url`, `og:image`, and the two theme-colors are origin-independent), or link
previews break. `og-image.png` (1200x630) is the preview card.

Also configured, and worth not undoing: visitor access is public (Netlify now
creates projects with SSO team login required, which would put a login wall in
front of recruiters), and the "Powered by Netlify" badge is switched off.

After the first share, run the URL through LinkedIn's Post Inspector once —
LinkedIn caches previews hard.

## Working on this

Edit `index.html` directly. After any change check both themes and a narrow
viewport before committing. The three things that break silently:

1. a colour defined only inside a media or `[data-theme]` block
2. the mobile rail — it's a flex item that needs `width:100%; min-width:0`
   on `.rail > div`, or centred overflow pushes the first tab off-screen
3. selector specificity between `.job`, `.stream` and `section` padding
