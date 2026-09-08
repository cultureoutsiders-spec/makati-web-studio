# Makati Web Studio — what to do next

A step-by-step reference. Work top to bottom. You can do Phase 0 once, then repeat
Phase 1 → Phase 2 for one business at a time (you don't have to send all five at once).

**Related docs:** `PRICING.md` (what to charge + market research) · `HANDOVER-AND-HOSTING.md`
(what you vs. the client each need for hosting, and the client FAQ).

- **Local folder:** `C:\Users\centr\Documents\Online-Business\Makati-Web-Studio`
- **Code repo:** https://github.com/cultureoutsiders-spec/makati-web-studio
- **Studio index (all five demos):** https://cultureoutsiders-spec.github.io/makati-web-studio/

| Business | Folder | Live demo | Outreach draft | Send to |
|---|---|---|---|---|
| 851 Bike Park | `851-bike-park/` | https://cultureoutsiders-spec.github.io/makati-web-studio/851-bike-park/ | `emails/851-bike-park.md` | chuakatherine@yahoo.com (email) |
| COREX Fitness | `corex-fitness/` | https://cultureoutsiders-spec.github.io/makati-web-studio/corex-fitness/ | `emails/corex-fitness.md` | @corex.fitnessgym (Instagram DM) |
| Artina Zobel Residences | `artina-suites/` | https://cultureoutsiders-spec.github.io/makati-web-studio/artina-suites/ | `emails/artina-suites.md` | info@artinasuites.com (email) |
| The Makati Haven | `makati-haven/` | https://cultureoutsiders-spec.github.io/makati-web-studio/makati-haven/ | `emails/makati-haven.md` | themakatihaven@gmail.com (email) |
| MPT Suites | `mpt-suites/` | https://cultureoutsiders-spec.github.io/makati-web-studio/mpt-suites/ | `emails/mpt-suites.md` | reservations@makatiprimetowersuites.com (email) |

---

## Phase 0 — one-time setup (do once, ~5 minutes)

### 0.1 Get a Web3Forms key so the contact forms actually deliver

Right now every contact/booking form has a placeholder key. Until it's replaced, submitting
a form just opens the visitor's email app instead of sending you a message.

- [ ] Go to https://web3forms.com
- [ ] Enter the email address where you want form submissions to land, click "Create Access Key"
- [ ] Copy the key it shows you (looks like `a1b2c3d4-....`). One key works for all five sites.
- [ ] Keep it handy for Phase 1.

### 0.2 Decide your studio identity

The emails have blanks you need to fill every time:

| Placeholder | What to put |
|---|---|
| `[STUDIO NAME]` | Your business name (e.g. "Makati Web Studio", or whatever you trade as) |
| `[YOUR NAME]` | Your name |
| `[REPLY EMAIL]` | The email address replies should go to |
| `[PHONE]` | Your contact number |
| `[CALENDAR LINK]` | A booking link (Calendly / Cal.com / Google Calendar appointment page), or delete that sentence if you don't use one |

- [ ] Write these five values down somewhere you can copy-paste from.

---

## Phase 1 — prepare ONE business's site before you email it

Do this for whichever business you're about to contact. Repeat per business.
Replace `<slug>` below with that business's folder name from the table above.

### 1.1 Put your Web3Forms key in the forms

The key appears in the pages that have a form:

- `851-bike-park/` → `service.html`, `contact.html`
- `corex-fitness/` → `contact.html`
- `artina-suites/` → `contact.html`
- `makati-haven/` → `rates.html`, `contact.html`
- `mpt-suites/` → `booking.html`

In each of those files:

- [ ] Find `REPLACE_WITH_WEB3FORMS_KEY` and replace it with your real key from Phase 0.1.
  (In VS Code: open the folder, press `Ctrl+Shift+H`, search `REPLACE_WITH_WEB3FORMS_KEY`,
  replace all.)

### 1.2 Point the "message us" button and chat links at the real account

Some buttons currently link to generic placeholders:

- `https://m.me/` → change to the business's real Facebook Messenger link
  (`https://m.me/<their-page-username>`)
- `https://instagram.com/...` → confirm it's the business's real handle
- `https://facebook.com/` → change to the business's real Facebook page URL

- [ ] Search each site's HTML for `m.me/` and `facebook.com/` and `instagram.com/` and fix any
  that aren't the real account. If you don't know the real Messenger link yet, leave it — it's
  not critical for the pitch, just don't claim it works.

### 1.3 Swap in real photos (optional for the pitch, required before it goes live)

Every image is placeholder stock. The layout is built so real photos drop in with **no code
changes** as long as you keep the same filenames.

- [ ] Look in `<slug>/assets/img/` — note the filenames (e.g. `hero-showroom.jpg`,
  `bike-honda.jpg`).
- [ ] Get the business's real photos (from their Facebook/Instagram, or ask them for a folder).
- [ ] Rename each real photo to match an existing filename and drop it in `<slug>/assets/img/`,
  overwriting the placeholder. Keep them roughly landscape and under ~500 KB each.

**Known placeholder mismatches to prioritise:**
- `artina-suites` → the "bunk room" card shows a double bed, not bunks.
- `makati-haven` → the hero is a generic bright studio.
- All coach photos in `corex-fitness/coaches.html` are stock and the names say `[Name]`.

You can send the pitch email with placeholder photos (the emails already say the photos are
placeholders). Just make sure real photos are in before a paying client's site goes public.

### 1.4 Replace placeholder testimonials with real reviews

Search the site's HTML for `PLACEHOLDER`. Where you find testimonial blocks marked placeholder,
paste in 2–3 real reviews:

- **851 Bike Park, COREX, Makati Haven, MPT Suites** → have placeholder testimonial cards.
  Copy real quotes from the business's Google reviews / ClassPass / Airbnb, keep them short,
  and update the `<cite>` line with the reviewer's first name or "Google review".
- **Artina** → already uses real attributed quotes, nothing to do.

### 1.5 Check the coaches page (COREX only)

`corex-fitness/coaches.html` has six cards with `Coach [Name]` and generic bios.

- [ ] Either fill in real coach names/bios, or if you don't have them yet, that's fine for the
  pitch — the gym provides them if they buy.

### 1.6 Test the site yourself

- [ ] Open the live URL on your phone and on a laptop. Click through every page in the nav.
- [ ] Submit the contact form with your own details. Confirm the message arrives at the inbox
  you set in Phase 0.1 (check spam too).
- [ ] Check the "Call" links open your dialer and the map loads.

### 1.7 Push your changes so the live site updates

After editing files, from a terminal:

```bash
cd "/c/Users/centr/Documents/Online-Business/Makati-Web-Studio"
"/c/Program Files/GitHub CLI/gh.exe" auth status   # should say logged in as cultureoutsiders-spec
git add -A
git commit -m "Prep <business name> site: forms, photos, testimonials"
git push
```

Wait 1–2 minutes, then reload the live URL. GitHub Pages rebuilds automatically on every push.

---

## Phase 2 — send the outreach

### 2.1 Finish the draft

- [ ] Open `emails/<slug>.md`.
- [ ] Pick one of the three subject lines.
- [ ] Copy the body. Replace `[STUDIO NAME]`, `[YOUR NAME]`, `[REPLY EMAIL]`, `[PHONE]`,
  `[CALENDAR LINK]` with your Phase 0.2 values.
- [ ] Re-read it once out loud. Cut anything that feels off for your voice.

### 2.2 Send it

- **Email businesses (851, Artina, Makati Haven, MPT):** send from your own email to the address
  in the table. Plain text is fine.
- **COREX:** it's a two-message Instagram DM. Send message 1, then message 2 right after. Send
  from the studio's own IG account if you have one (looks less like spam than a personal account).

### 2.3 Log it

Keep a simple list: business, date sent, channel, and a reminder to follow up in ~4–5 days if
no reply. One polite follow-up is fine; after that, leave it.

---

## Phase 3 — when someone replies

### Pricing — current drafts vs. recommended

Full breakdown and the market research behind it: **`PRICING.md`**.

| | One-time | Monthly |
|---|---|---|
| What the email drafts currently say | ₱30,000–₱50,000 | ₱3,000–₱5,000/mo |
| **Recommended — introductory (no retainer, lead with this)** | **₱24,000** | none |
| Recommended — introductory (with retainer) | ₱12,000 setup | ₱1,800/mo |
| Recommended — competitive / market rate (no retainer) | **₱40,000** (₱35k for 851 & COREX, ₱45k for the 3 accommodation sites) | none |
| Recommended — competitive / market rate (with retainer) | ₱25,000–₱30,000 | ₱2,500–₱3,500/mo |

Every one-time price bundles: the build, responsive design, form setup, domain connection,
**12 months hosting**, **2 revision rounds**, and a handover call. Then the client owns it.
The email drafts were **not** edited — set your real figure from `PRICING.md`, then either lower
the numbers in each `emails/*.md` or just quote your figure on the call.

### If they're interested

- [ ] Offer the 15-minute call, or just answer their questions by message.
- [ ] Walk them through the live demo screen-by-screen.
- [ ] Confirm the deal: state one one-time figure (see the table above / `PRICING.md`), and
  mention the care plan as **optional** (hosting + unlimited small edits + backups + a monthly
  refresh), month-to-month, cancel anytime.
- [ ] Ask for: their real photos, their real Google/other reviews, confirmation of phone numbers
  and opening hours, and whether they have a domain or want you to register one.
- [ ] Send an invoice for the one-time fee (50% to start is normal; balance on handover).

### If they say no / no reply

Move on. The demo already did its job as a portfolio piece — keep the live URL, you can show it
to the next similar business.

---

## Phase 4 — when a client pays (going live for real)

Work in that business's folder only.

### 4.1 Finish the content

- [ ] All real photos in `<slug>/assets/img/` (same filenames).
- [ ] All real testimonials in place, no `PLACEHOLDER` left.
- [ ] Real phone numbers, hours, socials, Messenger link everywhere in the site.
- [ ] Web3Forms key set to an inbox the **client** checks (or one you forward to them).

### 4.2 Remove the "demo" markers

In every `.html` file of that site:

- [ ] Delete the line that starts `<div class="demo-flag">` (the "design proposal — not the
  official website" note in the footer).
- [ ] Change `<meta name="robots" content="noindex, nofollow">` to
  `<meta name="robots" content="index, follow">` so Google can find it.
- [ ] In `<slug>/robots.txt`, change `Disallow: /` to `Allow: /` (or delete the Disallow line).
- [ ] In the footer, decide whether to keep or remove "Built by Makati Web Studio".

### 4.3 Put it on the client's domain

Cheapest reliable option that matches how it's built now:

**Option A — Cloudflare Pages (recommended, free, custom domains, private repos allowed):**
1. Create a Cloudflare account, go to Workers & Pages → Create → Pages → Connect to Git.
2. Connect the `makati-web-studio` repo (or a copy of just that client's folder in its own repo).
3. Build settings: framework = None, build command = empty, output directory = `<slug>`
   (or `/` if it's a single-site repo).
4. Add the client's domain under the Pages project's "Custom domains" and follow the DNS steps.

**Option B — Netlify:** same idea. Drag-and-drop the `<slug>` folder at app.netlify.com/drop
for an instant test URL, or connect the repo, then add the custom domain.

**Option C — keep it on GitHub Pages** with a custom domain: add a file named `CNAME` containing
the client's domain to that site's folder, then set the domain in the repo's Settings → Pages,
and point the domain's DNS at GitHub. Works, but the repo has to stay public on the free plan.

For **Artina** and **MPT Suites**, the client already owns a domain (`artinasuites.com` /
`makatiprimetowersuites.com`) — use that.

### 4.4 Ongoing (if they took the care plan)

- Keep hosting running.
- Make small edits when they ask (text, prices, a new photo) — edit the file, `git commit`,
  `git push`, done in minutes.
- Once a month: check every page still loads, refresh a photo or a promo line, send them a
  one-line "site's healthy" note. That's what the monthly fee buys.

---

## Quick reference — strings to find and replace

| Find | Where | Replace with |
|---|---|---|
| `REPLACE_WITH_WEB3FORMS_KEY` | form pages (see 1.1) | your Web3Forms key |
| `[STUDIO NAME]` `[YOUR NAME]` `[REPLY EMAIL]` `[PHONE]` `[CALENDAR LINK]` | `emails/*.md` | your details |
| `PLACEHOLDER` | site HTML | real testimonials / coach info |
| `https://m.me/` | site HTML | client's real Messenger link |
| `<div class="demo-flag">…</div>` | site HTML (Phase 4 only) | delete the line |
| `content="noindex, nofollow"` | site HTML (Phase 4 only) | `content="index, follow"` |
| `Disallow: /` | `<slug>/robots.txt` (Phase 4 only) | `Allow: /` |

## Troubleshooting

- **Form says "something went wrong":** the Web3Forms key is missing or wrong. Re-check 1.1.
- **Live site didn't update after a push:** wait 2 minutes and hard-refresh (`Ctrl+Shift+R`).
  Check the repo's Actions tab for a failed "pages build".
- **`gh` command not found:** run `export PATH="$PATH:/c/Program Files/GitHub CLI"` first, or
  use the full path `"/c/Program Files/GitHub CLI/gh.exe"`.
- **An image looks stretched:** it's fine to use any landscape photo; the site crops it to fit.
  Very tall/narrow images will crop hard — use landscape where you can.
- **Want to take a site down:** in the repo Settings → Pages, or just delete that site's folder
  and push.
