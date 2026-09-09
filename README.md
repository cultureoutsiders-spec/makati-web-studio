# Makati Web Studio — spec sites

Static, no-build marketing websites built as design proposals for real Makati businesses that
currently have no website. Each site is a self-contained folder that can be handed to a buyer
and hosted anywhere.

## Live demos (GitHub Pages)

| Business | Folder | URL |
|---|---|---|
| 851 Bike Park (motorcycle dealer) | `851-bike-park/` | https://cultureoutsiders-spec.github.io/makati-web-studio/851-bike-park/ |
| COREX Fitness (boxing / Muay Thai / HYROX) | `corex-fitness/` | https://cultureoutsiders-spec.github.io/makati-web-studio/corex-fitness/ |
| Artina Zobel Residences (budget hotel) | `artina-suites/` | https://cultureoutsiders-spec.github.io/makati-web-studio/artina-suites/ |
| The Makati Haven (serviced studios) | `makati-haven/` | https://cultureoutsiders-spec.github.io/makati-web-studio/makati-haven/ |
| MPT Suites (aparthotel) | `mpt-suites/` | https://cultureoutsiders-spec.github.io/makati-web-studio/mpt-suites/ |
| Greenery Kitchen (vegan restaurant — "editorial broadsheet") | `greenery-kitchen/` | https://cultureoutsiders-spec.github.io/makati-web-studio/greenery-kitchen/ |
| Kangnam Beauty Makati (PMU studio — "editorial clinic") | `kangnam-beauty/` | https://cultureoutsiders-spec.github.io/makati-web-studio/kangnam-beauty/ |
| Resabal Dental Clinic (family dentistry — "wayfinding dashboard") | `resabal-dental/` | https://cultureoutsiders-spec.github.io/makati-web-studio/resabal-dental/ |
| Ambient Bar &amp; Restaurant (bar + events — "gig-listings page") | `ambient-resto/` | https://cultureoutsiders-spec.github.io/makati-web-studio/ambient-resto/ |
| Little Gee Plants × Tiny Teapot (plant shop + cafe — "two shops, one door" split) | `little-gee/` | https://cultureoutsiders-spec.github.io/makati-web-studio/little-gee/ |
| Yan yan soo (florist / gift delivery — "flower table" shop grid) | `yan-yan-soo/` | https://cultureoutsiders-spec.github.io/makati-web-studio/yan-yan-soo/ |
| HELP Therapy Center (children's speech / OT / PT / SPED — "help desk" knowledge base) | `help-therapy/` | https://cultureoutsiders-spec.github.io/makati-web-studio/help-therapy/ |
| PhysioSpace Poblacion (holistic physical therapy — calm "breathing" column) | `physiospace/` | https://cultureoutsiders-spec.github.io/makati-web-studio/physiospace/ |
| Koffle (coffee &amp; waffle cafe — storybook hidden-cafe) | `koffle/` | https://cultureoutsiders-spec.github.io/makati-web-studio/koffle/ |
| All Stars Cafe and Sports Bar (sports bar — fixtures scoreboard) | `all-stars/` | https://cultureoutsiders-spec.github.io/makati-web-studio/all-stars/ |
| Rapide Salon San Antonio Makati (car detailing / ceramic coating — "the bay sheet" work order) | `rapide-salon/` | https://cultureoutsiders-spec.github.io/makati-web-studio/rapide-salon/ |
| MOOI Makati (aesthetic &amp; wellness spa — "the treatment index") | `mooi-makati/` | https://cultureoutsiders-spec.github.io/makati-web-studio/mooi-makati/ |
| Easyshare Printing Services Makati (plan &amp; digital printing — "the order desk" press sheet) | `easyshare-printing/` | https://cultureoutsiders-spec.github.io/makati-web-studio/easyshare-printing/ |
| SHALA Beauty Lounge (nails / lashes / brows — "the colour wall" chip menu) | `shala-beauty/` | https://cultureoutsiders-spec.github.io/makati-web-studio/shala-beauty/ |
| Fortune Bakeshop (neighbourhood bakeshop since 1974 — "the bread board" receipt) | `fortune-bakeshop/` | https://cultureoutsiders-spec.github.io/makati-web-studio/fortune-bakeshop/ |
| Blue Door 304 (hidden speakeasy bar — "the door" you knock to enter) | `blue-door-304/` | https://cultureoutsiders-spec.github.io/makati-web-studio/blue-door-304/ |
| MSM Wells Photo (analog film lab — "the contact sheet" of film frames) | `msm-wells-photo/` | https://cultureoutsiders-spec.github.io/makati-web-studio/msm-wells-photo/ |
| Spindle Hole Records (new & used vinyl / turntables — "the crate" divider-tab browser) | `spindle-hole/` | https://cultureoutsiders-spec.github.io/makati-web-studio/spindle-hole/ |
| Gray Matter Showroom (archive / grail fashion — "the archive index" object-label grid) | `gray-matter/` | https://cultureoutsiders-spec.github.io/makati-web-studio/gray-matter/ |
| Kombat Sports Kalayaan (martial-arts academy — "the round timer" + fight card) | `kombat-sports/` | https://cultureoutsiders-spec.github.io/makati-web-studio/kombat-sports/ |
| Bibio (natural wine bar — "the list" of hand-annotated wine labels) | `bibio/` | https://cultureoutsiders-spec.github.io/makati-web-studio/bibio/ |
| Dan's Bike Shop (road &amp; MTB shop + workshop — "the build sheet" + service board) | `dans-bike-shop/` | https://cultureoutsiders-spec.github.io/makati-web-studio/dans-bike-shop/ |
| The Golden Fur Makati (pet grooming / vet / boarding — "the report card" pet passport) | `golden-fur/` | https://cultureoutsiders-spec.github.io/makati-web-studio/golden-fur/ |
| The GoodFellas Cafe (weekday office cafe — "the order ticket") | `goodfellas-cafe/` | https://cultureoutsiders-spec.github.io/makati-web-studio/goodfellas-cafe/ |
| Hoshi House (matcha slow-bar — "the slow vertical" with a sumi brushstroke) | `hoshi-house/` | https://cultureoutsiders-spec.github.io/makati-web-studio/hoshi-house/ |

Studio landing page: repo root `index.html`.

## Stack

- Plain HTML + one CSS file + one JS file per site. **No build step, no dependencies.**
- Fonts from Google Fonts; images are local JPEGs in each site's `assets/img/`.
- `_shared/base.css` and `_shared/app.js` are the source of truth; they are **copied** into each
  `<site>/assets/`. Edit the shared copy, then `cp` into the sites.

## Per-site structure

```
<site>/
  index.html + 4 inner pages + 404.html
  robots.txt        (Disallow: / — these are demos)
  sitemap.xml
  assets/
    base.css   (copy of _shared/base.css)
    app.js     (copy of _shared/app.js)
    theme.css  (site-specific tokens + signature components)
    favicon.svg
    img/       (placeholder stock — swap for the client's photos)
```

## Handing a site to a client

1. Zip the single `<site>/` folder. It has no external dependency beyond Google Fonts.
2. Swap `assets/img/*` for the client's real photos (keep the same filenames — nothing else changes).
3. Contact forms use [Web3Forms](https://web3forms.com): create a free access key and replace
   `REPLACE_WITH_WEB3FORMS_KEY` in each form's `data-web3key`. Until then the form falls back to
   opening the visitor's email client.
4. Replace the placeholder testimonial blocks (marked `PLACEHOLDER` in the HTML) with the client's
   real Google / ClassPass reviews.
5. Point the client's domain at the host and remove the `noindex` meta + the `.demo-flag` footer line.

## Notes

- Every page carries `<meta name="robots" content="noindex">` and a visible "design proposal"
  disclaimer while it lives on the studio domain.
- Research dossiers for each business are in `research/`.
- Draft outreach messages are in `emails/`.
