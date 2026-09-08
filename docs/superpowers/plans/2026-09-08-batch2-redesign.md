# Batch-2 Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement
> this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild the five Batch-2 demo sites (greenery-kitchen, kangnam-beauty, resabal-dental,
ambient-resto, little-gee) from the ground up — a shared foundation pass then a distinct page
architecture per site — fixing the spacing, nav-overflow, type, motion and sameness problems
from client review.

**Architecture:** Plain static HTML per page + shared `base.css` + per-site `theme.css` +
shared `app.js`, no build step. The foundation pass edits `_shared/base.css` and
`_shared/app.js`; those files are then **copied** into every Batch-2 site's `assets/`. Each
site then gets bespoke `index.html` + 4 inner pages + `404.html` and a rewritten `theme.css`.
Deployed via GitHub Pages from `main`/root of `cultureoutsiders-spec/makati-web-studio`.

**Tech Stack:** HTML5, CSS custom properties + `clamp()` fluid scales, vanilla JS
(IntersectionObserver, rAF scroll), Google Fonts, Web3Forms (contact), GitHub Pages.

## Global Constraints

- No build step, no framework, no external JS dependency. Shared CSS/JS is **copied** into each
  `<site>/assets/`, never imported across folders.
- **Batch-1 sites unchanged:** `851-bike-park`, `corex-fitness`, `artina-suites`, `makati-haven`,
  `mpt-suites` — do not modify any file under these.
- **Colour palettes unchanged** for all five Batch-2 sites. Only layout, type, spacing, motion,
  structure change.
- Every page: `<meta name="robots" content="noindex, nofollow">`, visible `.demo-flag`
  disclaimer reading "Design proposal prepared by GCCofCI Digital — not the official website of
  <business>", JSON-LD `LocalBusiness`-family schema, `<link rel="icon" href="assets/favicon.svg">`,
  OG tags. Per site: `robots.txt` = `Disallow: /`, `sitemap.xml`.
- Signature/footer credit: "GCCofCI Digital", contact `gccofci.digital@gmail.com` /
  `+639455495153` only where a studio credit is shown; business contact details are the
  business's own.
- No body copy set below font-weight 400. No motion without a `prefers-reduced-motion: reduce`
  off-switch.
- Menus, prices, reviews, staff names stay as clearly-marked client-confirmed placeholders.
- Contact forms keep `data-web3key="REPLACE_WITH_WEB3FORMS_KEY"` and the `mailto:` fallback.
- Commit identity: `cultureoutsiders-spec <centralhq01@gmail.com>` (already set local to repo).
- Verification is visual/HTTP, not unit tests: `curl -sI` for `200`, `grep` for required
  markup, browser spot-check, and a manual breakpoint sweep at 320/375/768/1024/1280/1440px.

---

### Task 1: Foundation pass — `_shared/base.css`

**Files:**
- Modify: `_shared/base.css`

**Interfaces:**
- Produces (consumed by every site's HTML + theme.css):
  - Token `--gutter: clamp(1.25rem, 0.8rem + 2vw, 2.5rem)` used by `.container`.
  - Tokens `--space-2xs`, `--space-xs`, `--space-sm`, `--space-md`, `--space-lg`, `--space-xl`,
    `--space-2xl` (clamped).
  - `.container` = `width:min(100% - (var(--gutter) * 2), var(--container)); margin-inline:auto`.
  - `.card` padding = `clamp(1.6rem, 1.2rem + 1.4vw, 2.4rem)`, with `.card > * + * { margin-top:
    var(--space-sm) }` and `.card :is(h2,h3,h4) + :is(p,ul,ol) { margin-top: var(--space-xs) }`.
  - `.split` = `grid-template-columns:1.05fr .95fr; gap:clamp(2rem, 1rem + 4vw, 5rem)`; new
    modifier `.split--top { align-items:start }`; text column gets `padding-inline-end:
    var(--space-xs)` when it is the flush-to-edge side.
  - `.hero__panel` = `max-width:62ch; padding:clamp(1.5rem,1rem+2vw,2.75rem); border-radius:
    var(--radius); background:var(--hero-panel-bg, rgba(0,0,0,.28)); backdrop-filter:blur(3px)`.
  - Default `--hero-scrim: linear-gradient(180deg, rgba(0,0,0,.30), rgba(0,0,0,.62))`.
  - Nav collapses at `max-width:1040px` (was 860px); above the drawer, `.nav__links { gap:1.1rem }`
    and `.nav__links .btn { padding:.6em 1em; font-size:var(--step--1) }`.
  - `.reveal-group > *` staggered via `transition-delay:calc(var(--i,0) * 70ms)`; variant
    `.reveal--rotate` adds `rotate(-1.5deg)` to the hidden state.
  - `body` keeps `overflow-x:clip` ONLY as belt-and-braces; no element may actually exceed the
    viewport (Task verification enforces this).

- [ ] **Step 1: Add the token block**

In `:root` (after `--container`), add:

```css
  --gutter: clamp(1.25rem, .8rem + 2vw, 2.5rem);
  --space-2xs: clamp(.25rem, .2rem + .2vw, .4rem);
  --space-xs:  clamp(.5rem, .4rem + .4vw, .8rem);
  --space-sm:  clamp(.85rem, .7rem + .7vw, 1.25rem);
  --space-md:  clamp(1.25rem, 1rem + 1.2vw, 2rem);
  --space-lg:  clamp(2rem, 1.5rem + 2.4vw, 3.25rem);
  --space-xl:  clamp(3rem, 2.2rem + 4vw, 5rem);
  --space-2xl: clamp(4.5rem, 3.3rem + 6vw, 8rem);
```

- [ ] **Step 2: Widen the container gutter**

Replace `.container{ width:min(100% - 2.5rem, var(--container)); margin-inline:auto; }` with:

```css
.container{ width:min(100% - (var(--gutter) * 2), var(--container)); margin-inline:auto; }
```

- [ ] **Step 3: Loosen `.card`**

Replace the `.card` rule's `padding` line and add flow rhythm:

```css
.card{
  background:var(--paper);
  border:1px solid var(--line);
  border-radius:var(--radius);
  padding:clamp(1.6rem, 1.2rem + 1.4vw, 2.4rem);
}
.card > * + *{ margin-top:var(--space-sm); }
.card :is(h2,h3,h4) + :is(p,ul,ol){ margin-top:var(--space-xs); }
```

- [ ] **Step 4: Open the `.split` gap + edge padding**

Replace the `.split` rule:

```css
.split{ display:grid; grid-template-columns:1.05fr .95fr; gap:clamp(2rem, 1rem + 4vw, 5rem); align-items:center; }
.split--top{ align-items:start; }
.split > .stack{ padding-inline-end:var(--space-xs); }
.split--flip .split__media{ order:-1; }
@media (max-width:840px){ .split{ grid-template-columns:1fr; gap:var(--space-lg); } .split--flip .split__media{ order:0; } .split > .stack{ padding-inline-end:0; } }
```

- [ ] **Step 5: Hero panel + stronger default scrim**

In the `/* ---- Hero ---- */` block, change the `::after` default and add `.hero__panel`:

```css
.hero__bg::after{ content:""; position:absolute; inset:0; background:var(--hero-scrim, linear-gradient(180deg, rgba(0,0,0,.30), rgba(0,0,0,.62))); }
.hero__panel{ max-width:62ch; padding:clamp(1.5rem,1rem+2vw,2.75rem); border-radius:var(--radius); background:var(--hero-panel-bg, transparent); }
```

- [ ] **Step 6: Raise the nav collapse breakpoint and tighten the wide-but-not-mobile band**

Change `@media (max-width:860px)` on the nav block to `@media (max-width:1040px)`. Immediately
before it add:

```css
@media (min-width:1041px) and (max-width:1200px){
  .nav__links{ gap:1.1rem; }
  .nav__links .btn{ padding:.6em 1em; font-size:var(--step--1); }
}
```

Also change the mobile drawer `.nav__links` `inset:64px 0 auto 0;` stays; verify the drawer
still uses `max-width:1040px`.

- [ ] **Step 7: Staggered + rotate reveal variants**

After the existing `.reveal` block:

```css
.reveal-group > *{ opacity:0; transform:translateY(18px); transition:opacity .7s ease, transform .7s ease; transition-delay:calc(var(--i, 0) * 70ms); }
.reveal-group.is-in > *{ opacity:1; transform:none; }
.reveal--rotate{ transform:translateY(18px) rotate(-1.5deg); }
.reveal--rotate.is-in{ transform:none; }
@media (prefers-reduced-motion: reduce){ .reveal-group > *{ opacity:1; transform:none; transition:none; } }
```

- [ ] **Step 8: Swap `overflow-x`**

In `body{}` change `overflow-x:hidden;` to `overflow-x:clip;` (clip can't be scrolled to, so a
real overflow becomes visible as a layout break during testing instead of being silently
scrollable).

- [ ] **Step 9: Verify**

Run: `cd _shared && python -c "import tinycss2,sys" 2>/dev/null || true` (no linter required) —
instead do a brace-balance check:
`node -e "const c=require('fs').readFileSync('_shared/base.css','utf8');const o=(c.match(/{/g)||[]).length,x=(c.match(/}/g)||[]).length;console.log(o===x?'braces OK '+o:'MISMATCH '+o+'/'+x)"`
Expected: `braces OK <n>`

- [ ] **Step 10: Commit**

```bash
git add _shared/base.css
git commit -m "Foundation: base.css spacing tokens, container gutter, card/split rhythm, nav collapse at 1040px, stagger reveals"
```

---

### Task 2: Foundation pass — `_shared/app.js`

**Files:**
- Modify: `_shared/app.js`

**Interfaces:**
- Consumes: `.reveal-group` / `.reveal` / `[data-count]` from Task 1 + existing markup.
- Produces (consumed by site HTML):
  - `.reveal-group` children get `--i` set to their index and `.is-in` added to the group on
    enter.
  - `[data-parallax="<n>"]` (n ~ 0.05–0.3): translated `translate3d(0, calc(scrollDelta * n), 0)`
    on scroll via rAF. Skipped when `matchMedia('(prefers-reduced-motion: reduce)')` matches or
    `matchMedia('(pointer: coarse)')` matches or `innerWidth < 700`.
  - `[data-draw]` on an inline `<path>`: on enter, set `stroke-dasharray` and `stroke-dashoffset`
    to `getTotalLength()`, then transition `stroke-dashoffset` to `0`.
  - Existing behaviours (sticky header `data-scrolled`, nav toggle, count-up, lightbox, footer
    year, Web3Forms) unchanged.

- [ ] **Step 1: Read the current file** to confirm the IIFE structure and the existing
  IntersectionObserver for `.reveal`.

Run: `sed -n '1,40p' _shared/app.js`

- [ ] **Step 2: Extend the reveal observer for groups**

Where `.reveal` elements are observed, also select `.reveal-group`. In the observer callback,
when a `.reveal-group` enters: iterate `entry.target.children`, set
`child.style.setProperty('--i', i)`, then `entry.target.classList.add('is-in')`. Keep the
existing per-element `.reveal` → `.is-in` path. Unobserve after firing.

```js
var revealEls = document.querySelectorAll('.reveal, .reveal-group');
var ro = new IntersectionObserver(function(entries){
  entries.forEach(function(e){
    if(!e.isIntersecting) return;
    var t = e.target;
    if(t.classList.contains('reveal-group')){
      Array.prototype.forEach.call(t.children, function(c,i){ c.style.setProperty('--i', i); });
    }
    t.classList.add('is-in');
    ro.unobserve(t);
  });
}, { rootMargin:'0px 0px -10% 0px', threshold:0.05 });
revealEls.forEach(function(el){ ro.observe(el); });
```

- [ ] **Step 3: Add the parallax module**

Append inside the IIFE:

```js
(function parallax(){
  var reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  if(reduce || matchMedia('(pointer: coarse)').matches || innerWidth < 700) return;
  var nodes = [].slice.call(document.querySelectorAll('[data-parallax]'));
  if(!nodes.length) return;
  var ticking = false;
  function apply(){
    var vh = innerHeight;
    nodes.forEach(function(n){
      var r = n.getBoundingClientRect();
      var mid = r.top + r.height/2;
      var delta = (mid - vh/2) / vh;              // -1..1 through viewport
      var strength = parseFloat(n.getAttribute('data-parallax')) || 0.12;
      n.style.transform = 'translate3d(0,' + (delta * strength * -120).toFixed(1) + 'px,0)';
    });
    ticking = false;
  }
  addEventListener('scroll', function(){ if(!ticking){ requestAnimationFrame(apply); ticking = true; } }, { passive:true });
  addEventListener('resize', apply);
  apply();
})();
```

- [ ] **Step 4: Add the line-draw module**

```js
(function lineDraw(){
  var reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  var paths = [].slice.call(document.querySelectorAll('[data-draw]'));
  if(!paths.length) return;
  paths.forEach(function(p){
    var len = p.getTotalLength();
    p.style.strokeDasharray = len; p.style.strokeDashoffset = reduce ? 0 : len;
  });
  if(reduce) return;
  var io = new IntersectionObserver(function(es){
    es.forEach(function(e){
      if(!e.isIntersecting) return;
      e.target.style.transition = 'stroke-dashoffset 1.4s ease';
      e.target.style.strokeDashoffset = 0;
      io.unobserve(e.target);
    });
  }, { threshold:0.3 });
  paths.forEach(function(p){ io.observe(p); });
})();
```

- [ ] **Step 5: Verify**

Run: `node -c _shared/app.js && echo "syntax OK"`
Expected: `syntax OK`

- [ ] **Step 6: Commit**

```bash
git add _shared/app.js
git commit -m "Foundation: app.js stagger reveals, [data-parallax] scroll module, [data-draw] SVG line draw"
```

---

### Task 3: Propagate shared files + regression-check all five sites still render

**Files:**
- Overwrite: `<site>/assets/base.css`, `<site>/assets/app.js` for each of the five Batch-2 sites.

- [ ] **Step 1: Copy**

```bash
for s in greenery-kitchen kangnam-beauty resabal-dental ambient-resto little-gee; do
  cp _shared/base.css "$s/assets/base.css"
  cp _shared/app.js  "$s/assets/app.js"
done
```

- [ ] **Step 2: Confirm Batch-1 untouched**

Run: `git status --porcelain | grep -E '851-bike-park|corex-fitness|artina-suites|makati-haven|mpt-suites' || echo "batch-1 clean"`
Expected: `batch-1 clean`

- [ ] **Step 3: Local smoke-serve**

```bash
python -m http.server 8765 >/dev/null 2>&1 &  echo $! > /tmp/serve.pid
sleep 1
for s in greenery-kitchen kangnam-beauty resabal-dental ambient-resto little-gee; do
  curl -s -o /dev/null -w "$s %{http_code}\n" "http://localhost:8765/$s/"
done
```
Expected: each line ends ` 200`

- [ ] **Step 4: Commit**

```bash
git add greenery-kitchen/assets/base.css greenery-kitchen/assets/app.js kangnam-beauty/assets/base.css kangnam-beauty/assets/app.js resabal-dental/assets/base.css resabal-dental/assets/app.js ambient-resto/assets/base.css ambient-resto/assets/app.js little-gee/assets/base.css little-gee/assets/app.js
git commit -m "Propagate foundation base.css/app.js into the five Batch-2 sites"
```

(Leave the http.server running for later tasks; kill with `kill $(cat /tmp/serve.pid)` at the end.)

---

### Task 4: Facebook photo pull

**Files:**
- Create/replace: JPEGs under `<site>/assets/img/` (keep the filenames each site's templates
  already reference).

- [ ] **Step 1: Enumerate the target pages**

| Site | Facebook page |
|---|---|
| greenery-kitchen | Greenery Kitchen (facebook.com/greenery.kitchen) |
| kangnam-beauty | Kangnam Beauty Makati - Manila |
| resabal-dental | Resabal Dental (@resabaldental) |
| ambient-resto | Ambient Bar & Restaurant (facebook.com/ambient.makati) |
| little-gee | Little Gee Plants x Tiny Teapot |

- [ ] **Step 2: For each page, in the operator's logged-in Chrome**

Navigate to the page, open the **Photos** / **Photos of** tab, open individual photos at full
size, and capture the rendered image. Save to a working dir
`_fbpull/<site>/NN-<description>.jpg`. Prioritise: interiors / room, food or product, treatment
or service in progress, staff/space, exterior/signage. Aim 4–8 usable per site.

- [ ] **Step 3: Triage + place**

For each site, pick the best shots, downscale to the widths the templates use
(hero ~1600w, cards ~900w, thumbs ~600w) with `python` + PIL, and write them over the existing
`<site>/assets/img/<name>.jpg` filenames. Keep any filename with no good real photo on its
current stock image.

- [ ] **Step 4: Record the haul**

Append to `research/batch-2.md` a short per-site list: which filenames are now real photos vs.
still stock.

- [ ] **Step 5: Commit**

```bash
git add greenery-kitchen/assets/img kangnam-beauty/assets/img resabal-dental/assets/img ambient-resto/assets/img little-gee/assets/img research/batch-2.md
git commit -m "Batch-2: real Facebook photos where obtainable, stock fallback elsewhere"
```

If the pull yields nothing usable for a site, note it in the commit body and move on — the
redesign does not block on photos.

---

### Task 5: Rebuild `greenery-kitchen` — "The Daily Board"

**Files:**
- Rewrite: `greenery-kitchen/assets/theme.css`
- Rewrite: `greenery-kitchen/index.html`, `menu.html`, `meal-plans.html`, `story.html`,
  `visit.html`, `404.html`
- Keep: `robots.txt`, `sitemap.xml`, `assets/favicon.svg` (adjust favicon only if the wordmark
  mark changes)

**Interfaces:**
- Consumes: all Task 1 tokens/classes, Task 2 JS hooks.
- Produces: component classes local to this site — `.masthead`, `.board` (retained, restyled),
  `.rail` (sticky jump-nav), `.spread` (two-column printed menu), `.leader` (dotted leader row),
  `.timeline` / `.tl-item`, `.hand` (Caveat). These are defined only in this `theme.css`.

- [ ] **Step 1: Fonts** — in every page `<head>`, replace the Google Fonts link with:
  `family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600&family=Karla:wght@400;500;700&family=Caveat:wght@600;700&family=DM+Serif+Display&display=swap`

- [ ] **Step 2: `theme.css`** — keep the `:root` colour tokens exactly as they are now
  (`--paper #f4efe3`, `--brand #1f3d2b`, `--accent #c26b3e`, `--leaf #4e7a4e`, etc.). Change
  only:
  - `--font-display: "Fraunces", Georgia, serif;` `--font-body: "Karla", system-ui, sans-serif;`
    keep `--font-hand: "Caveat", cursive;` add `--font-mark: "DM Serif Display", Georgia, serif;`
  - `--radius: 3px;`
  - Add the `.masthead` (grid: wordmark left in `--font-mark`, links right), `.rail`
    (`position:sticky; top:calc(var(--space-md) + 3.5rem)`), `.spread` (`columns:2; column-gap:
    var(--space-lg)` on wide, single column ≤700px), `.leader` (flex row, dotted `flex:1`
    spacer, price in `--font-mono`), `.timeline`/`.tl-item` (left border, node dots),
    `.board` restyled to sit on the oat ground with a dark inset panel.
  - Hero: `.hero--board` = no bg image; the `.board` is the focal element; headline in Fraunces
    `--step-5` with an `<em>` (italic, `--accent`).
- [ ] **Step 3: `index.html`** — structure:
  `header.site-header > nav.masthead` · `main` > `section.hero--board` (headline + dated
  `.board` with 4–6 `.leader` rows, `data-draw` underline on the "Today" hand text) ·
  `section` with `.container` grid `[rail | content]`: `.rail` jump-nav +
  content blocks (short intro `.reveal`, "What we cook" `.spread` teaser `.reveal-group`,
  "Since 2000" `.timeline` teaser, delivery link row, a `.card` catering CTA) ·
  `section.section--brand` reviews (`.reveal-group`, 3 placeholder blocks marked) ·
  footer. Chat FAB + `app.js` + a tiny inline script that types the board heading on load
  (clip-path width 0→100%, skipped under reduced-motion).
- [ ] **Step 4: Inner pages** — `menu.html` (full `.spread`, sections: Mains / Silog / Sides /
  Sweets / Drinks, dishes from the current site, all under an "indicative — confirm with
  Greenery" note); `meal-plans.html` (the 5-Day Bento ₱1,500/week as a `.card` set + enquiry
  form); `story.html` (full `.timeline` 2000→2026 + a values `.reveal-group`); `visit.html`
  (hours table, embedded Google Map iframe for 2078 E. Pascua St. Kasilawan, click-to-call,
  Messenger link, contact form with `data-web3key` + `data-mailto="greenery"`... keep existing
  mailto target). Each inner page carries the full masthead + footer markup (no partials).
- [ ] **Step 5: `404.html`** — masthead + centered "This page took the day off" + link home.
- [ ] **Step 6: Verify markup on every page**

```bash
for p in index menu meal-plans story visit 404; do
  f="greenery-kitchen/$p.html"
  grep -q 'robots" content="noindex' "$f" && grep -q 'demo-flag' "$f" && grep -q 'assets/base.css' "$f" \
    && echo "$p ok" || echo "$p MISSING REQUIRED MARKUP"
done
grep -q 'application/ld+json' greenery-kitchen/index.html && echo "schema ok"
```
Expected: `index ok` … `404 ok`, `schema ok`

- [ ] **Step 7: Serve + eyeball**

`curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8765/greenery-kitchen/` → `200`.
Browser: load it, sweep 320 / 768 / 1024 / 1440px — confirm no horizontal scrollbar, board
readable, rail sticks, menu rows have air, headline doesn't collide with anything.

- [ ] **Step 8: Commit**

```bash
git add greenery-kitchen
git commit -m "Redesign greenery-kitchen: 'The Daily Board' editorial broadsheet layout"
```

---

### Task 6: Rebuild `kangnam-beauty` — "Editorial Clinic"

**Files:**
- Rewrite: `kangnam-beauty/assets/theme.css`
- Rewrite: `kangnam-beauty/index.html`, `treatments.html`, `prices.html`, `studio.html`,
  `book.html`, `404.html`

**Interfaces:**
- Produces (local): `.masthead--center` (logo centred, `.nav__links` split via `order`),
  `.statement` (centred serif hero), `.portrait` (hairline frame, `max-width:520px`,
  `margin-inline:auto`), `.hgallery` (`display:flex; overflow-x:auto; scroll-snap-type:x
  mandatory; gap:var(--space-md)`), `.hgallery__card` (`flex:0 0 min(78vw,420px);
  scroll-snap-align:center`), `.ba` (retained slider, restyled), `.facemap` (retained,
  full-width), `.pmenu` (retained, more leading), `.pullquote` (one large rotating quote).

- [ ] **Step 1: Fonts** — `family=Cormorant+Garamond:ital,wght@0,500;0,600;1,500&family=Manrope:wght@400;500;600;700&display=swap`
- [ ] **Step 2: `theme.css`** — keep colour tokens (`--paper #faf6f4`, `--brand #33262a`,
  `--accent #9c6b73`, `--gold #b89a7e`). Change: `--font-display:"Cormorant Garamond",Georgia,serif;`
  `--font-body:"Manrope",system-ui,sans-serif;` `--font-mono:"Manrope",monospace;` drop the
  `body{font-weight:300}` and `.lead{font-weight:300}` rules → use `400`. `h1,.display{font-weight:500}`.
  Bump `.pmenu__row` padding to `var(--space-sm) 0` and add `line-height:1.5`. Add
  `.masthead--center`, `.statement`, `.portrait`, `.hgallery*`, `.pullquote`.
- [ ] **Step 3: `index.html`** — `nav.masthead--center` · `main` > `section` centred:
  `.statement` (short serif line, `<em>` accent) + `.portrait` (real photo if pulled, else
  stock) with `data-parallax="0.06"` · `section` treatments `.hgallery` `.reveal` (4–5
  `.hgallery__card`, each an image + name + "from ₱" note marked indicative) · `section`
  full-width `.facemap` with an inline script (retain current behaviour) · `section.section--brand`
  a single `.pullquote` with 3 placeholder quotes cycled by inline script (crossfade, paused
  under reduced-motion) · `section` prices teaser `.pmenu` (top 5 rows) + link to prices.html ·
  footer.
- [ ] **Step 4: Inner pages** — `treatments.html` (each treatment a section: description,
  aftercare, a `.ba` slider; retain the drag script); `prices.html` (full `.pmenu`, "indicative,
  confirmed at consultation" banner); `studio.html` (address S-1 Antel Spa Residences 1, G.S.
  Salamanca St., Poblacion; map iframe; "by appointment" hours; hotlines 0906 049 3356 /
  0956 940 1130); `book.html` (consultation-request form, `data-web3key`, `mailto` fallback,
  FB/IG links). Full centred masthead + footer on each.
- [ ] **Step 5: `404.html`**, then **Step 6 verify** (same grep loop as Task 5, path
  `kangnam-beauty`, pages `index treatments prices studio book 404`), **Step 7** serve+eyeball
  (emphasise: generous whitespace, `.ba` auto-demo fires once on scroll, gallery snaps,
  no clip), **Step 8 commit** `-m "Redesign kangnam-beauty: 'Editorial Clinic' centred gallery-led layout"`.

---

### Task 7: Rebuild `resabal-dental` — "Wayfinding"

**Files:**
- Rewrite: `resabal-dental/assets/theme.css`
- Rewrite: `resabal-dental/index.html`, `services.html`, `first-visit.html`, `clinic.html`,
  `book.html`, `404.html`

**Interfaces:**
- Produces (local): `.nav--pill` (rounded sticky bar, `border-radius:999px`, floating with
  `margin-block:var(--space-sm)`), `.hero--band` (flat `--brand` band, no photo), `.tiles`
  (grid of 3 `.tile`, each a big link with icon + label + sub), `.tile:hover`
  (`translateY(-4px) rotate(-.6deg)`), `.tracker` (horizontal flex, SVG connector line with
  `data-draw`), `.tstep`, `.svc-grid`/`.svc` (icon cards), `.team`/`.member`, `.faq`/`.faq__q`
  (`<details>`-based accordion, animated `max-height`).

- [ ] **Step 1: Fonts** — `family=Nunito:wght@400;600;700;800&family=Inter:wght@400;500;600&family=Quicksand:wght@600;700&display=swap`
- [ ] **Step 2: `theme.css`** — keep colours (`--brand #2f6fb0`, `--accent #f2795b`,
  `--mint #8fd4c4`, `--paper #f6fafc`, `--radius 14px`). `--font-display:"Nunito",system-ui,sans-serif;`
  `--font-body:"Inter",system-ui,sans-serif;` `--font-mark:"Quicksand",sans-serif;`. Add
  `.nav--pill`, `.hero--band`, `.tiles`/`.tile`, `.tracker`/`.tstep`, `.svc-grid`/`.svc`,
  `.team`/`.member`, `.faq`. Keep `.steps`/`.step` deleted (replaced by `.tracker`).
- [ ] **Step 3: `index.html`** — `header > nav.nav--pill` (links + bright "Book" pill) ·
  `section.hero--band` (headline + one-line promise + `.tiles`: "Book a check-up" → book.html,
  "New-patient info" → first-visit.html, "Kids' first visit" → first-visit.html#kids) ·
  `section` first-visit `.tracker` (4 `.tstep`, inline SVG line with `data-draw`) `.reveal` ·
  `section` `.svc-grid` (Pediatric / Orthodontics / General & esthetic / Preventive) `.reveal-group` ·
  `section.section--paper2` `.stats` with `data-count` ("years caring", "little patients",
  etc.) · `section` `.faq` (5 Q/A, placeholder answers marked) · `section.section--brand`
  reviews `.reveal-group` (marked placeholder — note "no Google reviews yet") · footer.
- [ ] **Step 4: Inner pages** — `services.html` (each service expanded, `.svc-grid` +
  copy); `first-visit.html` (full `.tracker` + a `#kids` anchor block "Bringing a child",
  what to expect, forms to bring); `clinic.html` (`.team` with Dr. [Name] Resabal placeholder
  cards clearly marked, Unit 1111 Centuria Medical Makati address, map iframe, hours);
  `book.html` (appointment-request form `data-web3key` + `mailto` to resabaldental@gmail.com,
  phone (02) 8567 4115 / 0917 850 0404). Full pill nav + footer each.
- [ ] **Step 5: `404.html`**, **Step 6 verify** (grep loop, pages
  `index services first-visit clinic book 404`), **Step 7** serve+eyeball (tiles lift/tilt on
  hover, tracker line draws on scroll, accordion opens, count-up runs, no clip), **Step 8
  commit** `-m "Redesign resabal-dental: 'Wayfinding' task-dashboard layout"`.

---

### Task 8: Rebuild `ambient-resto` — "The Listings Page"

**Files:**
- Rewrite: `ambient-resto/assets/theme.css`
- Rewrite: `ambient-resto/index.html`, `food-drinks.html`, `events.html`, `gallery.html`,
  `reservations.html`, `404.html`

**Interfaces:**
- Produces (local): `.nav--min` (wordmark + single Reserve link + `.nav__toggle` panel),
  `.listing` (grid `[main | aside]`, aside `position:sticky; top:var(--space-lg)`),
  `.week`/`.gig` (day · act · time rows, hover highlight), `.reserve-card` (the sticky aside,
  gets `.is-lit` toggled by an inline IntersectionObserver as `.week` passes), `.whatson`
  (retained marquee), `.sheet` (letterpress single-sheet menu), `.rider` (occasion package,
  retained picker script), `.contact-sheet` (tight photo strip), brass `.rule--brass`.

- [ ] **Step 1: Fonts** — `family=Archivo:wght@500;600;700;800&family=Barlow:wght@400;500;600&family=DM+Serif+Display:ital@1&display=swap` (remove Oswald)
- [ ] **Step 2: `theme.css`** — keep colours (`--paper #16110d`, `--accent #d29a3e`,
  `--wine #7a2f2a`, `--ink #f0e6d8`, `--radius 0`). `--font-display:"Archivo",system-ui,sans-serif;`
  keep `--font-body:"Barlow"`, `--font-serif:"DM Serif Display"`. Delete all `Oswald` refs and
  the `text-transform:uppercase` on `h1,h2,h3` → keep uppercase only on `.eyebrow`, `.btn`,
  `.foot-h`, `.gig__meta`. Add `.nav--min`, `.listing`, `.week`/`.gig`, `.reserve-card`,
  `.sheet`, `.rider`, `.contact-sheet`, `.rule--brass` (`border-top:2px solid var(--accent)`).
  Keep `.whatson`, `.occasions`, `.pkg` (rename visual to `.rider`).
- [ ] **Step 3: `index.html`** — `header > nav.nav--min` · `.whatson` marquee (retained) ·
  `main` > `section.listing` `.container` grid: main = `<h1>` "What's on this week" + `.week`
  (5–6 `.gig` rows, day/act/time, placeholder line-up marked "sample — this week's acts
  posted on Facebook"), aside = `.reserve-card` (hours, phone, "Reserve a table" + "Book an
  event" buttons; inline IO adds `.is-lit` while `.week` is in view) · `section` `.sheet`
  menu teaser (Kitchen / Bar, dotted `.leader` rows) · `section` `.rider` occasion picker
  (retain the `data` script) · `section` `.contact-sheet` (6 thumbs, lightbox) · `section`
  reviews `.reveal-group` · footer.
- [ ] **Step 4: Inner pages** — `food-drinks.html` (full `.sheet`, "illustrative menu"
  banner); `events.html` (full `.rider` + capacity/packages copy, enquiry form);
  `gallery.html` (`.contact-sheet` full + lightbox); `reservations.html` (`#book` form
  `data-web3key` + `mailto` ambientrestobar@gmail.com, phone 0917 165 6915 /
  (02) 8241 8233, map iframe 3663 Bautista St, Palanan). Full min-nav + footer each.
- [ ] **Step 5: `404.html`**, **Step 6 verify** (grep loop, pages
  `index food-drinks events gallery reservations 404`), **Step 7** serve+eyeball (marquee
  runs, gig rows stagger + hover, reserve card sticks and lights, no clip, headings not
  all-caps-clipped), **Step 8 commit** `-m "Redesign ambient-resto: 'The Listings Page' gig-poster layout; drop Oswald for Archivo"`.

---

### Task 9: Rebuild `little-gee` — "Two Shops, One Door"

**Files:**
- Rewrite: `little-gee/assets/theme.css`
- Rewrite: `little-gee/index.html`, `plant-shop.html`, `cafe.html`, `visit-events.html`,
  `contact.html`, `404.html`

**Interfaces:**
- Produces (local): `.nav--split` (two-tone bar, `.nav__links--plant` left green,
  `.nav__links--cafe` right cream, `.brand` bridging centre), `.duo` (the spine:
  `grid-template-columns:1fr 1fr` with a centre organic divider via SVG/`clip-path`;
  stacks ≤760px), `.duo__side` (each half; `[data-parallax]` at different strengths
  0.05 vs 0.12), `.merge` (centre band across both), `.shelf`/`.pot` (plant grid + swinging
  `.tag` price labels, `transform:rotate` on hover), `.case`/`.bake` (bakery-case menu),
  `.potw` (retained plant-of-the-week, rotates in via `.reveal--rotate`).

- [ ] **Step 1: Fonts** — `family=Bricolage+Grotesque:opsz,wght@12..96,500;12..96,600;12..96,700&family=Nunito+Sans:wght@400;600;700&family=Fredoka:wght@500;600&display=swap`
- [ ] **Step 2: `theme.css`** — keep colours (`--brand #2f6b3f`, `--paper #f8f3e6`,
  `--butter #e9b949`, `--accent #c9694a`, `--radius 18px`). `--font-display:"Bricolage Grotesque",system-ui,sans-serif;`
  `--font-body:"Nunito Sans",system-ui,sans-serif;` `--font-mark:"Fredoka",sans-serif;`. Reduce
  the very-round feel: `--radius 14px` on cards (keep 18px only on `.tag`/pills). Add
  `.nav--split`, `.duo`/`.duo__side`/`.merge`, `.shelf`/`.pot`/`.tag`, `.case`/`.bake`. Keep
  `.potw`, `.care`, `.dish` restyled.
- [ ] **Step 3: `index.html`** — `header > nav.nav--split` · `main` > `section.duo`
  (left `.duo__side` PLANTS: badge, heading, 2–3 lines, image `data-parallax="0.05"`, "Shop
  plants" link; right `.duo__side` CAFE: badge, heading, lines, image `data-parallax="0.12"`,
  "See the menu" link; centre divider) · `section.merge` (hours, map iframe, "small events"
  line — the two businesses meet here) · `section` `.potw` `.reveal--rotate` · `section`
  `.shelf` teaser (6 `.pot` with `.tag`) · `section` `.case` teaser (bakery items) ·
  `section.section--brand` reviews `.reveal-group` · footer.
- [ ] **Step 4: Inner pages** — `plant-shop.html` (full `.shelf`, care `.care` cards,
  "reserve a plant" enquiry, list marked illustrative); `cafe.html` (full `.case` menu,
  illustrative banner); `visit-events.html` (hours, map 3734-D L&M Building, Bautista cor.
  Boyle Sts., Palanan; the garden-events blurb + enquiry form); `contact.html` (form
  `data-web3key` + `mailto` littlegeeplants@gmail.com, phone 0947 869 0514, FB link). Full
  split-nav + footer each.
- [ ] **Step 5: `404.html`**, **Step 6 verify** (grep loop, pages
  `index plant-shop cafe visit-events contact 404`), **Step 7** serve+eyeball (the two halves
  parallax-offset on scroll, tags swing on hover, potw rotates in, stacks cleanly ≤760px, no
  clip), **Step 8 commit** `-m "Redesign little-gee: 'Two Shops, One Door' split-spine layout"`.

---

### Task 10: Studio landing + README + deploy + verify

**Files:**
- Modify: `index.html` (studio landing — the five Batch-2 cards), `README.md` (demo table if
  any URL/label changed — URLs are unchanged, so likely just descriptive text).

- [ ] **Step 1: Refresh the five Batch-2 cards** on the studio `index.html` so each card's blurb
  matches its new direction ("editorial broadsheet", "editorial clinic", "wayfinding
  dashboard", "listings page", "split-identity"). Keep the Batch-1 cards untouched.

- [ ] **Step 2: README** — update the one-line description column for the five Batch-2 rows if
  wording changed; URLs stay.

- [ ] **Step 3: Kill the local server**

```bash
kill $(cat /tmp/serve.pid) 2>/dev/null; rm -f /tmp/serve.pid
```

- [ ] **Step 4: Commit + push**

```bash
git add index.html README.md
git commit -m "Studio landing + README: Batch-2 redesign blurbs"
git push origin main
```

- [ ] **Step 5: Wait for Pages, then verify every changed URL**

```bash
sleep 45
BASE=https://cultureoutsiders-spec.github.io/makati-web-studio
for s in greenery-kitchen kangnam-beauty resabal-dental ambient-resto little-gee; do
  for p in "" 404.html assets/base.css assets/app.js assets/theme.css; do
    curl -s -o /dev/null -w "%{http_code}  $s/$p\n" "$BASE/$s/$p"
  done
done
```
Expected: `200` for every homepage, `assets/*`; `404.html` returns `200` (it's a real file).
Re-run after another `sleep 30` if any `404`/`404`-status appears (Pages build lag).

- [ ] **Step 6: Browser spot-check** each of the five live homepages: no horizontal scroll at
  375 / 1024 / 1440px, fonts loaded (not fallback), at least one non-count-up motion visible on
  scroll, hero text legible.

- [ ] **Step 7: Final commit** if the spot-check needed any fix; otherwise done. Report the five
  live URLs, per-site design direction, per-site FB photo haul, and remaining placeholders to
  the operator.

## Self-Review

- **Spec coverage:** foundation (Task 1–2), propagation (3), FB photos (4), the five
  architectures (5–9 — each maps to a spec section), deploy+verify (10). Acceptance criteria
  map to the Step-6/7 verifies in each site task and Task 10 Steps 5–6. ✔
- **Placeholder scan:** design copy (menus, quotes, staff names, reviews) is deliberately
  placeholder per Global Constraints and marked in-page; no plan step defers work with "TBD". ✔
- **Type consistency:** shared class/token names defined in Task 1–2 Interfaces and reused by
  name in Tasks 5–9; each site's local components are namespaced and defined in that site's
  Interfaces block. ✔
