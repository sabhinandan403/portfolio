# Roadmap — planned, not built

Ideas agreed but deliberately not implemented yet. Nothing here is approved for
building without checking with Abhinandan first. `CLAUDE.md` remains the record
of what *is* built.

---

## 1. A figure per problem — "understand it in seconds, without reading"

**Goal.** A recruiter scanning `#projects` should grasp what each problem *was*
before deciding to read the prose. Same instinct as the hero lineage diagram,
applied one level down.

**The scope is narrower than it sounds.** The figure explains **the problem and
its resolution** — not the architecture. Architecture is what the prose is for.
If a sketch needs a legend to explain the boxes, it has stopped doing this job.

### The constraint that matters most

These must **not** read as four more hero diagrams. The hero is the page's
signature; four rivals would flatten it and turn the page into a diagram
gallery. Deliberately a quieter register:

| | hero lineage diagram | problem figures |
|---|---|---|
| height | 184px | ~90–110px |
| labels | boxes + sub-captions + 3 group captions | 2–4 words, no sub-captions |
| motion | packets loop continuously | one transition, plays once on entry |
| job | narrates a career | narrates one before/after |

**The colour system already encodes this.** Tangerine = the problem state,
teal = resolved. No new colours, no new meanings — before/after maps exactly
onto the two accents the site already has.

### Honest assessment of the four

Not all four earn one, and this is the part worth agreeing before any building.

**1. "The page that took seven seconds" — strongest. Build this first.**
Two horizontal bars on a shared time axis: 7s in tangerine, 45ms in teal.
At true scale the second bar is ~0.6% of the first — roughly 4px against 600px.
That near-invisible sliver *is* the argument; no annotation needed beyond two
mono labels. Optionally, above it: one browser box with several arrows to a
database, collapsing to one arrow into memory. Nothing else on the page makes
its point this fast.

**2. "Telemetry into tables" — build only with a different angle.**
The obvious drawing (sources → raw → cleaned → curated → consumers) is a
smaller re-run of the hero diagram. Redundant, and it dilutes the signature.
The angle that *is* distinct: three reports each computing the same KPI
separately and showing three different numbers, versus one cleaned layer
feeding all three the same number. That draws the actual problem — numbers
drifting apart — rather than the pipeline shape.

**3. "A day of sensor data" — already has a figure. Do not add a second.**
Cheaper and better: extend the existing heat map with a thin "before" strip
above it — scattered raw event ticks — so the figure carries the transformation
instead of only the result. Reuses the SVG that exists.

**4. "Ten KPIs" — probably skip.** Definitions are the least visual thing on
the page, and the honest drawing of it lands very close to #2's. Two figures
making the same argument is worse than one. If something is wanted here, it
should not be a diagram — a single definition line rendered as a card would do
more.

**So the realistic outcome is two new figures and one extension, not four.**

### Placement

Figure goes **immediately after the `<h3>`, before "The problem" prose.** The
whole point is that it is read *instead of* the paragraph, so it cannot sit
below it. This pairs with the separate idea of lifting each `.outcome` callout
to the top of its block — together they give a skimmer title → picture →
result in about ten seconds per problem.

### Motion

One transition, triggered on scroll-in, played **once** — the before state
holding briefly, then becoming the after state. Not a loop. Four looping
figures plus the hero means a page that never settles, which reads cheap and
fights the hero for attention.

Reuse the existing `IntersectionObserver`, and re-arm on re-entry the way the
heading sweep does, since Abhinandan asked for that behaviour explicitly.
Everything must be inert and show the resolved state under
`prefers-reduced-motion`.

### Mechanics and traps

- Inline SVG, no library. Wrap in the existing `.flow` / `.flow-wrap`
  horizontal-scroll pattern so narrow viewports do not squash them.
- Every figure needs a real `aria-label` describing the finding in a sentence,
  as the heat map's does — not "diagram".
- Test both themes and a narrow viewport before committing; strokes that read
  on warm white can disappear on the graphite ground.
- Watch page weight. Three more inline SVGs plus their animation is the largest
  single addition since the case studies. If `index.html` gets unwieldy, that
  is the moment to reconsider, not after.
- No confidentiality drift: these are schematics, invented like the heat map.
  No real device IDs, module names, or internal source lists — the standing
  rule in `CLAUDE.md`.

### Sequencing

1. Build **#1 only**, as a prototype for the register.
2. Look at it in both themes and on mobile, in context, next to the hero.
3. **Decide then** whether the quieter register actually holds — and only then
   whether #2 and #3 are worth it. If #1 makes the page feel busier rather than
   faster, the honest answer is to stop at one.

### The risk worth naming

This can make the page worse. The current version is restrained, and restraint
is why it does not read as generated. Four figures is the point where a
considered page becomes a busy one. The sequencing above exists to catch that
before it is four figures deep.
