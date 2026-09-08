# Batch-2 spec sites — ground-up redesign

**Date:** 2026-09-08
**Owner:** Michael Omana / GCCofCI Digital
**Scope:** Redesign the five Batch-2 demo sites — `greenery-kitchen`, `kangnam-beauty`,
`resabal-dental`, `ambient-resto`, `little-gee` — from the ground up. Batch-1 sites
(`851-bike-park`, `corex-fitness`, `artina-suites`, `makati-haven`, `mpt-suites`) are **out of
scope** and must not change.

## Why

Client review of Batch 2 raised concrete problems:

1. **Spacing.** Image-to-text gaps in `.split` sections are too tight; `.card` padding is too
   small and heading→body rhythm inside cards is cramped; hero text collides with busy photos;
   container gutters are narrow.
2. **A visible right-edge clip.** Nav links + CTA overflow the viewport at medium widths (nav
   doesn't collapse until 860px), and body text clips at the same right edge — a horizontal
   overflow bug.
3. **Type.** Some pairings hurt legibility (Cormorant Garamond at weight 300) or cause the
   clipping (Oswald's tight all-caps).
4. **Motion.** Only the stat count-up is actually wired up on most pages. The `.reveal` class
   exists but is barely used. The sites feel static.
5. **Sameness.** All five share one skeleton (sticky nav → photo hero → stats band → alternating
   image/text splits → review grid → CTA → footer). They differ only by colour tokens and one
   "signature" component.

## Non-goals

- No change to Batch-1 sites.
- No change to the colour palette of any Batch-2 site (client explicitly likes the colours).
- No build step introduced. Still plain HTML + `base.css` + `theme.css` + `app.js` per site,
  shared files **copied** into each `<site>/assets/`.
- No CMS, no framework, no external JS dependencies.
- Not sending any outreach. That is a separate task.

## Approach

**Approach A (chosen): foundation pass → pilot → roll out.**

1. **Foundation pass** — fix the systemic problems once in `_shared/base.css` and
   `_shared/app.js`, then copy into every Batch-2 site.
2. **Facebook photo pull** — use the operator's logged-in Chrome session to pull real photos
   from each business's Facebook page; art-directed stock remains the fallback at the same
   filenames.
3. **Greenery Kitchen pilot** — rebuild fully as the first site so the quality bar is visible
   on a live page. Client reviews.
4. **Roll out** — rebuild Kangnam, Resabal, Ambient, Little Gee to the same bar.

Rejected: all-five-in-parallel (higher risk of five revisions instead of one); wireframe-first
(slower to a real working page). Layout directions were approved via visual wireframes before
this spec.

## Foundation pass — shared changes

### `_shared/base.css`

- **Container gutter:** `.container` width goes from `min(100% - 2.5rem, …)` to
  `min(100% - 3rem, …)` on mobile scaling up to a wider inline gutter; add a
  `--gutter: clamp(1.25rem, 0.8rem + 2vw, 2.5rem)` token and use it.
- **Spacing scale:** add `--space-2xs … --space-2xl` tokens (clamped) so components stop
  hand-rolling `clamp()` calls and vertical rhythm is consistent.
- **`.card`:** padding floor raised (`clamp(1.6rem, 1.2rem + 1.4vw, 2.4rem)`); add
  `.card > * + *` flow spacing and a dedicated `.card h3 + p`, `.card h4 + p` rhythm so the
  heading is never jammed against its body copy or the top edge.
- **`.split`:** column gap raised to `clamp(2rem, 1rem + 4vw, 5rem)`; add `align-items:start`
  option; ensure the text column has trailing inline padding so it never touches the viewport
  edge on the flush side.
- **Hero:** introduce a reusable `.hero__panel` (max-width, backdrop, padding) and a stronger
  default `--hero-scrim` so hero text always rests on a legible ground regardless of the photo.
  Per-site heroes may opt out (e.g. sites with no photo hero).
- **Nav:** collapse breakpoint raised to **1040px**; between ~1040px and the mobile drawer the
  nav uses a tighter link gap and the CTA becomes a compact pill so it cannot overflow. Audit
  for the horizontal-overflow source (candidate: a `100vw` element, an un-wrapped flex row, or
  the marquee track) and fix it so `body` never needs `overflow-x:hidden` to hide a bug.
- **Reveal:** keep `.reveal`; add `.reveal-group` (staggers direct children via
  `transition-delay` set from `--i`) and a `.reveal--rotate` variant.

### `_shared/app.js`

- **Staggered reveals:** for any `.reveal-group`, set `--i` on each child and add `.is-in` in
  sequence when the group enters the viewport.
- **Parallax:** elements with `[data-parallax]` (value = strength, e.g. `0.15`) get a
  `translate3d(0, …, 0)` on scroll via `requestAnimationFrame`; disabled under
  `prefers-reduced-motion` and on coarse pointers/small screens.
- **Line draw:** `[data-draw]` on an inline SVG `<path>` — set `stroke-dasharray` /
  `stroke-dashoffset` from path length, animate offset to 0 on enter.
- **Keep:** sticky-header state, mobile nav toggle, count-up (`[data-count]`), lightbox,
  footer year, Web3Forms handler with `mailto:` fallback.
- All new behaviour is a no-op under `prefers-reduced-motion: reduce`.

## Per-site architecture

Each site is a distinct page architecture: different nav treatment, different hero archetype,
different body grid, different signature interaction. Colours unchanged. Five pages each
(`index` + 4 inner + `404`), `robots.txt` (`Disallow: /`), `sitemap.xml`, favicon, JSON-LD,
`noindex`, visible `.demo-flag` disclaimer, signed "GCCofCI Digital".

### Greenery Kitchen — "The Daily Board" (editorial broadsheet)

- **Nav:** left wordmark (DM Serif), right-aligned text links, no crammed CTA — a "Order / Call"
  link set.
- **Hero:** no photo. A framed **chalkboard panel** — "Today at Greenery" + the date — as the
  masthead centrepiece on the oat ground, with the serif headline above it.
- **Body:** asymmetric two-column. Sticky **left jump-rail** (Menu / Our Story Since 2000 /
  Delivery / Catering). Right column scrolls: menu as a printed two-column spread with dotted
  leaders and handwritten section heads; "Our Story" as a vertical **timeline** (2000 → today);
  delivery-app link row; catering/bulk enquiry form.
- **Fonts:** Fraunces (headings) + Karla (body) + Caveat (chalk hand); DM Serif Display for the
  wordmark only.
- **Motion:** chalkboard text writes in on load (clip-path); menu rows stagger-fade on scroll;
  date stamp.
- **Pages:** index, menu, meal-plans, story, visit.

### Kangnam Beauty — "Editorial Clinic" (centred, gallery-led)

- **Nav:** centred logo with links split left/right (fashion-house).
- **Hero:** short centred serif statement + a single **hairline-framed portrait** (not
  full-bleed) beneath it. Generous margins.
- **Body:** treatments as a **horizontal snap-scroll gallery** of tall cards, each with a
  before/after. Face-map promoted to a full-width interactive diagram section. Prices as one
  airy single-column list with wide leading. Testimonials as one large rotating pull-quote.
  This site carries the most whitespace of the five — it is the direct answer to "cramped
  boxes".
- **Fonts:** Cormorant Garamond 500 (display only) + Manrope (body/labels).
- **Motion:** hero portrait scale/opacity-in; horizontal gallery drag + scroll-snap;
  before/after slider auto-demos once when scrolled into view; pull-quotes crossfade.
- **Pages:** index, treatments, prices, studio, book.

### Resabal Dental — "Wayfinding" (task dashboard)

- **Nav:** rounded **pill** sticky nav with a prominent "Book" pill.
- **Hero:** compact colour band (no big photo) — headline + three big **action tiles**: Book a
  check-up / New-patient info / Kids' first visit.
- **Body:** first-visit steps as a **horizontal tracker** with a connecting line that draws
  itself on scroll. Services as an icon grid. "Meet the team" as photo cards. **FAQ accordion**
  (new component). Count-up for "years caring" / "little patients".
- **Fonts:** Nunito (headings) + Inter (body); Quicksand kept for the wordmark.
- **Motion:** action tiles lift + slight tilt on hover; tracker line draw; accordion expand;
  count-up.
- **Pages:** index, services, first-visit, clinic, book.

### Ambient Bar & Restaurant — "The Listings Page" (gig-poster broadsheet)

- **Nav:** stripped — wordmark + "Reserve" only; everything else in a slide-down panel.
- **Hero:** a date-led **"What's on this week"** line-up (day · act · time) on the left, with a
  **sticky Reserve / Enquire card** on the right. No mood-photo hero. The marquee strip stays.
- **Body:** menu as a letterpress single sheet; occasion picker's package prints like a **rider**;
  gallery as a tight **contact-sheet strip**; heavy brass rules between sections.
- **Fonts:** Archivo (headings) + Barlow (body) + DM Serif Display italic (accent). Oswald
  removed.
- **Motion:** marquee kept; "what's on" rows stagger in; sticky Reserve card highlights as the
  listings scroll past; gig-list row hover.
- **Pages:** index, food-drinks, events, gallery, reservations.

### Little Gee × Tiny Teapot — "Two Shops, One Door" (literal split)

- **Nav:** two-tone bar — green plant links left, cream cafe links right, wordmark bridging the
  middle.
- **Hero + body spine:** the page is divided down the middle — **Plants | Cafe** — with an
  organic divider; the two halves scroll at slightly different speeds (parallax). A centre
  **"the space"** band where they meet: hours, map, events.
- **Sections:** plant **shelf grid** with hand-drawn price tags; cafe menu as a **bakery case**.
- **Fonts:** Bricolage Grotesque (headings) + Nunito Sans (body); Fredoka for wordmark/labels.
- **Motion:** two halves parallax at different speeds; price tags swing (rotate) on hover;
  plant-of-the-week rotates in; reveals with a small rotation for a hand-placed feel.
- **Pages:** index, plant-shop, cafe, visit-events, contact.

## Facebook photo pull

- Operator is logged into Facebook in the connected Chrome. For each page, open the Photos tab,
  open individual photos, capture the full-resolution image, save into
  `<site>/assets/img/<semantic-name>.jpg` (keep the filenames the templates already expect so a
  later swap is a drop-in).
- Pages: Greenery Kitchen; Kangnam Beauty Makati - Manila; Resabal Dental (@resabaldental);
  Ambient Bar & Restaurant; Little Gee Plants x Tiny Teapot.
- Realistic expectation: Facebook lazy-loads and rewrites image URLs; the haul will be partial.
  Anything not obtained stays art-directed stock. Report the per-site result.
- Menus, prices, reviews, staff names remain client-confirmed placeholders, clearly marked.

## Deployment

- Same repo `cultureoutsiders-spec/makati-web-studio`, GitHub Pages from `main` / root.
- Update the studio `index.html` cards and `README.md` demo table if any structure/URL changes.
- After push: wait for the Pages build, then curl every changed page + asset for `200`, and
  browser-spot-check each rebuilt homepage.

## Acceptance criteria

- [ ] Batch-1 sites byte-for-byte unchanged.
- [ ] No horizontal scrollbar / no right-edge text clip at 320, 375, 768, 1024, 1280, 1440px on
      any Batch-2 page — verified without relying on `overflow-x:hidden` to mask it.
- [ ] Nav never overflows; collapses cleanly before it would.
- [ ] `.split` image and text visibly separated at all breakpoints; `.card` heading never jams
      the top edge or its body copy.
- [ ] Each of the five sites is recognisably a different layout from the other four and from
      Batch 1 — different nav, hero archetype, and body grid.
- [ ] Each site has at least three distinct motion behaviours beyond the count-up, all disabled
      under `prefers-reduced-motion`.
- [ ] New font pairings loaded per site; no weight below 400 used for body copy.
- [ ] Every page: `noindex`, `.demo-flag` disclaimer, JSON-LD, favicon, `robots.txt`,
      `sitemap.xml`.
- [ ] Real Facebook photos integrated where obtainable; per-site haul reported; stock fallback
      otherwise, filenames unchanged.
- [ ] All Batch-2 pages + assets return `200` on GitHub Pages; homepages spot-checked in a
      browser.

## Build order

1. Foundation pass (`base.css`, `app.js`) + copy into all five sites.
2. Facebook photo pull.
3. Greenery Kitchen — full rebuild. Client reviews live.
4. Kangnam Beauty.
5. Resabal Dental.
6. Ambient Bar & Restaurant.
7. Little Gee × Tiny Teapot.
8. Studio `index.html` + `README.md`; deploy; verify.
