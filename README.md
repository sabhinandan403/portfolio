# Abhinandan Kumar — Portfolio

**Live at <https://abhinandan-kumar.netlify.app>** — pushes to `main` deploy automatically.

A single-file, dependency-free portfolio site. Everything lives in `index.html`:
markup, styles and script. The typefaces are self-hosted in `fonts/`, so the
page makes **no external requests at all** and renders identically offline.

```
index.html                  the whole site
fonts/                      Bricolage Grotesque, Newsreader, JetBrains Mono
Abhinandan_Kumar_CV.pdf     linked by the "Download CV" button
README.md
CLAUDE.md                   the design system and rules for changing it
```

## Run it locally

Opening `index.html` directly in a browser works. To serve it properly
(so the CV download and relative paths behave exactly as they will in
production):

```bash
cd path/to/portfolio
python3 -m http.server 8080
```

Then open <http://localhost:8080>.

Any static server does the same job — `npx serve`, `php -S localhost:8080`,
the VS Code Live Server extension.

## Before deploying publicly

`index.html` carries a `SITE_URL` placeholder in the social-preview meta tags.
Replace it with the live URL — those tags need absolute URLs or LinkedIn,
WhatsApp and Slack won't render the preview card:

```bash
sed -i '' 's|SITE_URL|https://your-site-url|g' index.html
```

(Drop the `''` after `-i` on Linux.)

The CV in this repo is the **public build — no phone number.** It's generated
by `build_cv.js` with `PUBLIC=1`; the private build, which keeps the phone
number, is the one to send directly to recruiters. Don't overwrite the repo
copy with the private one.

## Deploy it

Static folder, no build step: publish directory is this folder, build command
is empty. Every host works the same way.

**The URL is worth thinking about**, because it goes on a LinkedIn profile and
a resume. A GitHub Pages *user site* is always `<github-username>.github.io` —
which only reads well if the username reads like a name. Netlify lets you pick
the subdomain, so `abhinandan-kumar.netlify.app` is available even though the
GitHub handle isn't.

**Netlify** — connect the repo at netlify.com (no build command, publish
directory `.`), then Site settings → Change site name. Or drag this folder onto
<https://app.netlify.com/drop> for a deploy with no git at all. Pushes
redeploy automatically once the repo is connected.

**GitHub Pages**

```bash
git remote add origin git@github.com:<user>/<user>.github.io.git
git push -u origin main
```

Then Settings → Pages → Source: `main` / root. Live at
`https://<user>.github.io`. HTTPS pushes need `gh auth login` or a personal
access token — passwords stopped working years ago, and this is where the
deploy usually stalls.

**After the first deploy**, paste the URL into LinkedIn's
[Post Inspector](https://www.linkedin.com/post-inspector/) once. LinkedIn
caches link previews aggressively, and this forces it to re-read the meta tags
so your first share shows the card rather than a bare link.

## Editing it

- **Colours** are CSS custom properties in the `:root` block near the top.
  There are two accents with distinct meanings — `--hot` (tangerine) for energy
  and attention, `--cool` (teal) for outcomes and anything verified. The dark
  palette is redefined twice below — once for `prefers-color-scheme: dark` and
  once for the manual `[data-theme="dark"]` toggle — so change a colour in all
  three places.
- **Type** is three faces with fixed roles: Bricolage Grotesque for display,
  Newsreader for prose, JetBrains Mono for labels, chips and data. Headings run
  uppercase; prose stays sentence case.
- **The left rail** is generated from the `<a>` tags inside `nav.rail`; the
  script matches each `href` to a section `id`. Add a section, add a link,
  and the scroll tracking picks it up.
- **The projects section** holds four case studies inside
  `<section id="projects">`. Each is a `.case` block with optional `.beat`,
  `.beat.call` (the decision worth defending, tangerine rail) and `.outcome`
  (teal rail) parts. CLAUDE.md documents the pattern and the language rule.

## Theme

The page respects the visitor's OS theme by default. The `theme` button in the
rail overrides it and remembers the choice in `localStorage`, wrapped in
try/catch so private-mode browsers degrade quietly.

## Versions

**v1.8.0** — public release build. Phone number removed from the page and from
the CV committed here (`build_cv.js PUBLIC=1`); the private build that keeps it
is sent to recruiters directly. Open Graph, Twitter card, canonical and
theme-color meta added, plus `og-image.png` (1200x630) for link previews.

**v1.7.0** — case studies rewritten for a non-technical reader: internal
project shorthand replaced with plain description, so the Work section reads
without company context.

**v1.6.0** — recreated sensor heat map added to the third case study (invented
data, no identifiers); location, availability and the three-year figure settled.

**v1.5.0** — case studies deepened: how the cache stays current and where it
breaks, why medallion over reading Cassandra directly, and who the heat map is
actually for.

**v1.4.0** — Work section built out into four case studies; contact links fixed.

**v1.3.1** — the heading underline sweep now replays on every revisit to a
section, rather than animating once per page load.

**v1.3.0** — the hero signature becomes a lineage diagram: sources fan in,
transform layers in the middle, consumers fan out, with packets travelling the
paths. Labels written in plain language for non-technical readers, with the
stack as sub-captions. Replaces the run-activity strip.

**v1.2.0** — warm redesign. Warm-white ground with tangerine and teal accents,
Bricolage Grotesque / Newsreader / JetBrains Mono, uppercase headings, the run
activity strip as signature, self-hosted fonts, copy-email with feedback,
staggered hero reveal and scroll-swept headings. Work section restructured for
case studies, still awaiting project material.

**v1.0.0** — first locked design. Lineage-rail layout, copper-on-graphite
palette, Archivo / Source Serif 4 / JetBrains Mono.

See `CLAUDE.md` for the design system and the rules for changing it.
