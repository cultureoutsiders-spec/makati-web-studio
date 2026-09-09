# Batches 7-9 spec sites — design

Date: 2026-09-11. Builds on `PROSPECTS-BATCH-7.md` / `-8.md` / `-9.md` (commit `65319d4`) after an
extensive second-pass verification of every prospect's contact info and website status.

## Goal

Build finished multi-page spec/demo websites for the Makati businesses in batches 7-9 that
survived the second pass, at a quality bar above batches 5-6. Same commercial offer: PHP 25,000
one-time (first 5 clients), then PHP 35,000, no retainer, client owns the code, price includes
going live on their domain.

## Second-pass results

**Cut on verification (5):**
- Jackson Tailors — has a site, `jacksonstailors.com` (first pass checked `jacksontailors.com` /
  `jacksontailoring.com`, missed the "s").
- Ludo: Boardgame Store — the business closed both branches (Sept 2026 FB announcement); also had
  `ludogames.ph`.
- soma reformer — cannot be pinned to one confirmed, currently-operating Salcedo studio; too many
  near-identical names.
- Studio Matisse — actually in San Juan, not Makati; has `studiomatisseph.com`.
- Fez Spa — it is the spa inside 1898 Hotel, on `1898hotel.com/fez-spa/`; not an independent shop.

**Replacements sourced + verified (4):** Salon A, Shu Reflexology, Dream Hair Makati, Dive Buddies.
**(Dive Buddies later disqualified 2026-09-11** — it is the dive-school arm of Aquamundo Sports,
whose site `aquamundosports.com` is a live Shopify store; the emails found for it were
`@aquamundosports.com`. Removed. **13 planned sites → 12.)**
A fifth replacement (a plant shop) was attempted and abandoned: Wild Plants Studio has no
verifiable address / hours / operating evidence; Archipelago Plants the same; Nest Plant Studio is
in Mandaluyong and has a site. **Slot 15 is left unfilled this run — build 14.**

**Verification method:** name search + `curl` on every plausible domain (`.com` / `.ph` /
`.com.ph` / hyphenated / with and without trailing brand words), reading the response body to
distinguish a real site from a parked "lander" (~100-byte redirect to `/lander`), a bare nginx
welcome page, a suspended cPanel page, or an unrelated foreign site. Plus an operating-status
check (a 2025-2026 directory listing, a recent review, or a dated social post).

## The 14 confirmed businesses

### Batch 7 — repair & grooming trades

| # | Business | Address | Contact | Direction |
|---|---|---|---|---|
| 1 | Shoe Care | 2120-F Don Chino Roces Ave, Makati | call `840-4040` / `0918 827 7142`; FB DM | "the repair ticket" — heritage leather/shoe/bag repair since 1971. Service menu with real price bands (glue P120, stitch P280, resole from P680 women / P1700 men), turnaround table, a "send a photo for a quote" form. Register: leather, brass, worn tools. |
| ~~2~~ | ~~Quicker than Quick~~ — **REMOVED 2026-09-11**: the found email `quickerthanquickph@gmail.com` bounced (`550 NoSuchUser`), no other reliable contact. Site folder, draft, Gmail draft and listings all deleted. Batch 7 is now 4 sites. | | | |
| 3 | Another Barbershop | 5880 Enriquez Ave, Poblacion, Makati | call `0917 123 5880`; FB DM `/anotherbarbershop.poblacion` | "the chair card" — neighbourhood barbershop + retail. Price list (Cut & Wash P320, Shave P450, Colour P1,300 confirmed), barber roster, book-a-chair form, a small product shelf. Tue-Sun 11am-8pm. |
| 4 | Slick Barbers Co. | 3919 Yague St cor. South Ave, Brgy Sta Cruz, Makati | FB DM `/slickbarbersco`; Setmore | "the standing appointment" — "glory days of the neighbourhood barbershop." Price list, barbers, a weekly-availability grid, book-a-chair form. Open 10am-10pm daily. Grittier, mid-century-shop identity. |
| 5 | Salon A | 106 San Agustin St, Makati | IG DM `@salon_a_manila`; call `0954 380 3129` | "the Korean chair" — Korean-owned salon, staff trained by a Korean creative director, Korean products. Cut / colour / treatment menu, a stylist page, a K-styling "how it works", booking form. Clean, bright, Seoul-salon register. 10am-8pm. |

### Batch 8 — studios & body

| # | Business | Address | Contact | Direction |
|---|---|---|---|---|
| 6 | Arte Tattoo & Piercing | General Luna Bldg, Don Pedro St, Poblacion, Makati | IG DM `@artetattooph`; call `0918 919 8611` | "the wall of work" — busy walk-in studio + piercing. Artist roster (each a portfolio + style tag), a deposit-and-book flow, an aftercare page, a piercing price list. Sun-Wed 1-9pm, Thu-Sat 3pm-12am. Vegan ink. |
| 7 | Ymahe Tattoo Studio | GF Coro Hotel, 8436 Kalayaan Ave, Poblacion, Makati | IG DM `@ymahetattoostudio`; call `0977 722 9368` | "the quiet sheet" — one fine-line artist inside a boutique hotel. Restrained portfolio, a consultation form (reference images, placement, size, budget), a healing/aftercare page. Calm, precise. Sun-Thu 1-10pm, Fri-Sat 1pm-12am. |
| 8 | Shu Reflexology | 3/F 58 Jupiter Bldg, Jupiter St, Bgy Bel-Air, Makati | **email `shu.makati.jupiter@gmail.com`**; call `0927 966 8188` | "the pressure map" — Xiamen-style Chinese foot reflexology + full body. Treatment menu with durations & prices, a foot-reflex-point diagram as the signature, a booking form. Open 1pm-1am daily. |
| 9 | Dream Hair Makati | 303 JP Rizal St, Brgy Tejeros, Makati (GF CMC Bldg) | FB DM `/dreamhairmakati` | "the colour swatch" — fashion-colour / balayage specialist. Colour-service catalogue (basic / ombre / French / fashion balayage), a before/after-style shade wall, a consultation form. Daily 10am-9pm. Bold, colour-led. |
| ~~10~~ | ~~Dive Buddies~~ — **REMOVED 2026-09-11**: it is the dive-school arm of Aquamundo Sports; `aquamundosports.com` is a live Shopify store, so it has a website. B8 is now 4 sites. | | | |

### Batch 9 — food, drink & indulgence

| # | Business | Address | Contact | Direction |
|---|---|---|---|---|
| 11 | Coco Gelato PH | 197 Salcedo St, Salamin Bldg, Legazpi Village, Makati (outside Minnano Supermarket) | FB DM; call `0966 166 9616` | "the flavour board" — artisan gelato by a Japan-trained, Italian-style chef, ~15 flavours. Rotating "scooping today" board, an allergen key, cups/cones/pints, party-tub pre-order form. Daily 10am-9pm. |
| 12 | Patisserie BEBE Rouge | 7602 Sacred Heart St cor. Metropolitan Ave, Brgy San Antonio, Makati | **email `beberougenhtc@gmail.com`**; call `0917 851 9636` | "the cake case" — French-Japanese patisserie, Japanese-community favourite (strawberry shortcake). Case grid, whole-cake catalogue with size/price/lead-time tables, seasonal reservation cakes, reservation form. Daily 8am-7pm. |
| 13 | Cartel Deli | GF Picasso Boutique Serviced Residences, 119 L.P. Leviste St, Salcedo Village, Makati | **email `contact@carteldeli.com`**; call `0917 625 2249` | "the three menus" — Spanish cafe-deli-bar (Pablo Bistro group). Cafe menu, deli counter, a wine list of 40+, plus grazing boards and events. Board / catering order form. Daily 7am-10pm. |
| 14 | Mandalay Whisky & Cigars | OPL Building, 100 Don Carlos Palanca, Legazpi Village, Makati (entered through The Belle & Dragon) | call `0917 625 8818` | "the humidor list" — bourbon & whisky cigar bar, a hidden room. Moody single-scroll, humidor list, pour list, house rules (walk-in / membership / private bookings), a table / private-room request form. ~6pm-3am Mon-Sat. |

## Build model (unchanged from batches 5-6)

Plain static HTML, zero build step. Per site under `<slug>/`:

- `index.html` + 4 inner pages + `404.html`
- `robots.txt` (`User-agent: *` / `Disallow: /`), `sitemap.xml`
- `assets/base.css` and `assets/app.js` — **copied** verbatim from `_shared/`
- `assets/theme.css` — per-site: overrides the CSS custom properties
  (`--paper --paper-2 --ink --ink-soft --line --accent --accent-ink --brand --brand-ink`, fonts,
  `--radius`, `--container`), adds one signature component, appends
  `.nav__links a.btn{ color:var(--_fg); }` (nav-CTA specificity fix).
- `assets/favicon.svg` — a small per-site mark
- `assets/img/*.jpg` — `picsum.photos/seed/<slug>-<name>/<w>/<h>` (reliable, unique per seed);
  same as batches 5-6.

Every page carries: `<meta name="robots" content="noindex, nofollow">`, a visible `.demo-flag`
footer line ("Design proposal prepared by GCCofCI Digital — not the official website of X …"),
JSON-LD, OG tags. Contact forms:
`<form data-contact data-web3key="REPLACE_WITH_WEB3FORMS_KEY" data-mailto="REPLACE_WITH_EMAIL">`
(mailto fallback until a real key is added).

**CSS gotcha to respect:** `clamp()` needs whitespace around `+` / `-`
(`clamp(1rem, 1rem + 3vw, 3rem)`), or the whole declaration is silently dropped.

**Typography:** each of the 14 gets a fresh Google-Fonts pairing (display / body / mono where
needed) not used in batches 1-6. The ~60 already-used families are listed in the theme.css files;
avoid them.

## What "better quality than before" means here

Per the user's answers this session: keep batch-5/6-level content (picsum images, plausible
placeholder copy written fresh per business, JSON-LD/OG on every page) and the batch-5/6 level of
design craft (one signature component per site, everything else quiet). **The upgrade is a real
engineering / QA pass**, run once across all 14 after they are built:

1. **Responsive sweep 320-1440.** Every page: no horizontal body scroll at 320; wide content
   (tables, diagrams, code) scrolls inside its own `overflow-x:auto` container; nav collapses
   cleanly; hero and signature components hold up at 360, 768, 1024, 1440.
2. **Accessibility.** Visible keyboard focus on every interactive element; `prefers-reduced-motion`
   respected by every animation/transition; text contrast AA against its background (check the
   accent-on-dark and muted-body cases specifically); every `<img>` has meaningful `alt`; one
   `<h1>` per page and a sane heading order; form fields have associated `<label>`s.
3. **Performance / correctness.** Every `<img>` has explicit `width`/`height` (or an aspect-ratio
   box) to stop layout shift, and `loading="lazy"` below the fold; no oversized images; favicon
   and OG image resolve.
4. **Cross-page QA.** Every internal link and in-page anchor resolves; nav "current page" state is
   right on all 6 pages; the contact form markup is identical and correct on the page that hosts
   it; `sitemap.xml` lists the real filenames; JSON-LD validates shape.

Fixes from the QA pass are committed as one "QA pass" commit per batch (or one across all three).

## Sequence

1. Copy `_shared/{base.css,app.js}` into each new `<slug>/assets/`.
2. Build **Batch 7** (5 sites) -> commit -> push -> `curl` every page for `200` on Pages.
3. Build **Batch 8** (5 sites) -> commit -> push -> verify.
4. Build **Batch 9** (4 sites) -> commit -> push -> verify.
5. **QA pass** across all 14 (checklist above) -> fix -> commit -> push -> re-verify.
6. Studio landing `index.html`: add 14 `<a class="demo">` cards. `README.md`: add 14 rows.
7. Outreach: `emails/<slug>.md` for all 14 (`humanizer` applied — no em/en dashes in the sent
   text; each carries the **set-up-costs paragraph**: domain ~PHP 1,000/yr in the client's name;
   hosting free for a static site, paid host ~PHP 300-500/mo optional; Michael registers the
   domain + points it + puts it live at no extra charge). 3 are emails (Shu Reflexology,
   Patisserie BEBE Rouge, Cartel Deli); 11 are DM scripts. Stage all 14 as Gmail drafts in
   `gccofci.digital@gmail.com` (emails addressed; DM scripts subject-flagged `[DM SCRIPT …]`,
   no recipient). **Not sent — Michael reviews + sends.**
8. Update Claude memory (`project_makati_web_studio.md`, `MEMORY.md`) and the Obsidian vault note.
9. Report: live URLs, the unfilled slot 15, anything that needs Michael's input before a sale
   (placeholder photos, real menus/prices/staff, addresses, Web3Forms keys).

## Out of scope

- Real photography, real menus/prices/staff names (placeholders, same as batches 1-6).
- Sending any outreach (drafts only).
- A 15th site (slot left unfilled; revisit with proper verification later).
- Any change to the 30 existing sites beyond the landing page + README.
