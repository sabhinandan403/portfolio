# Abhinandan Kumar — Portfolio

A single-file, dependency-free portfolio site. Everything lives in `index.html`:
markup, styles and script. The only external request is the Google Fonts
stylesheet, and there are real fallback stacks behind every face, so the page
also renders correctly with no network at all.

```
index.html                  the whole site
Abhinandan_Kumar_CV.pdf     linked by the "Download CV" button
README.md
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

## Deploy it

Because it's static, every host works the same way: point it at this folder.

**GitHub Pages**

```bash
git init
git add .
git commit -m "portfolio"
git branch -M main
git remote add origin git@github.com:<user>/<user>.github.io.git
git push -u origin main
```

Then Settings → Pages → Source: `main` / root. Live at
`https://<user>.github.io`.

**Netlify / Vercel / Cloudflare Pages** — drag the folder into the dashboard,
or connect the repo. No build command, no output directory; it's already built.

## Editing it

- **Colours** are CSS custom properties in the `:root` block near the top.
  Change `--signal` (the copper accent) and the whole page follows. The dark
  palette is redefined twice below it — once for `prefers-color-scheme: dark`
  and once for the manual `[data-theme="dark"]` toggle — so change a colour in
  all three places.
- **Type** is three faces with fixed roles: Archivo for display, Source Serif 4
  for prose, JetBrains Mono for labels, chips and data.
- **The left rail** is generated from the `<a>` tags inside `nav.rail`; the
  script matches each `href` to a section `id`. Add a section, add a link,
  and the scroll tracking picks it up.
- **The projects section** is a placeholder. The card markup goes inside
  `<section id="projects">`, replacing the `.slot` block.

## Theme

The page respects the visitor's OS theme by default. The `theme` button in the
rail overrides it and remembers the choice in `localStorage`, wrapped in
try/catch so private-mode browsers degrade quietly.

## Versions

**v1.0.0** — design locked. Lineage-rail layout, copper-on-graphite palette,
Archivo / Source Serif 4 / JetBrains Mono, both themes, projects section
scaffolded but not yet populated.

See `CLAUDE.md` for the design system and the rules for changing it.
