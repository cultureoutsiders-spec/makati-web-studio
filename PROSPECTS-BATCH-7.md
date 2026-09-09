# Prospects — batch 7

Five more Makati businesses with **no website of their own**, researched 2026-09-11. Same offer:
**PHP 25,000 one-time, no retainer (first 5 paying clients), then PHP 35,000.** Client owns the
code; price includes going live on their domain.

Batch 7 theme: **repair, craft and grooming trades** — hands-on shops that live on Facebook posts
and walk-ins.

**STATUS: researched, not built.** Sites not started.

## How the check was done

Each business was Googled by name, then its likely domains were requested directly with `curl`
(`http://<name>.com`, `.ph`, `.com.ph`) to catch three things a plain Google check misses:

- a **real own website** → disqualifies the lead (e.g. Hairshaft Salon `hairshaftsalon.com`,
  Framelogic `framelogic.ph`);
- a **parked / for-sale "lander"** (a ~100-byte page that redirects to `/lander`) → does **not**
  count as a website, the lead still qualifies;
- a **lapsed / suspended** site (cPanel "Account Suspended", default nginx welcome page) → also
  does not count, but is flagged because the owner has shown intent to have one.

A lead qualifies only if every result is a Facebook page, an Instagram account, a directory
listing (Yelp, Booky, Foursquare, Tripadvisor), or a delivery-app page, with no working own
domain.

**Disqualified on checking this round (they have their own live site) —** kept here so we don't
re-research them: Hairshaft Salon (`hairshaftsalon.com`), Framelogic (`framelogic.ph`), Frame
Forte (`frameforte.com`), Makenu bean-to-bar Chocolate (`makenuchocolate.com`), It's Vintage
(`its-vintage.com`), Cop Garden sneaker consignment (`copgarden.com`), Guitar Pusher
(`guitarpusher.com`, and it is a chain), Laro Ceramics (`laro-ceramics.com`, and multi-branch),
Gourmet Corner PH (`gourmetcornerph.com`).

---

## The five

### 1. Shoe Care — shoe, bag & leather-goods repair and restoration (since 1971)
- **Where:** 2120-F Don Chino Roces Avenue, Makati (same avenue as Dan's Bike Shop, different
  business). Open roughly Mon–Sat, shop hours.
- **Presence:** Facebook page (`/Shoe-Care-350071215023823`) + directory listings (Yelp cobbler
  lists, updated 2026). **No website.** No Instagram found.
- **Contact:** 8840-4040 / 8844-6211 / 0918-827-7142 · Facebook Messenger. No public email.
- **Pitch angle:** a 50-year-old repair shop competes with Mr. Quickie on trust, and trust is
  exactly what a Facebook feed can't carry. A site with the service list (resole, recrafting,
  colour restoration, bag spa, luggage), honest turnaround times, a "send us a photo for a quote"
  form, and a since-1971 story does the reassuring that a row of Messenger replies can't.
- **Template:** service menu + spec/turnaround tables + a photo-quote form. Closest to Easyshare's
  "order desk" pattern, in a heritage-workshop register (leather, brass, worn tools).

### 2. Quicker than Quick — shoe & bag repair, key duplication, locksmith, custom leather
- **Where:** Makati (mall-level kiosk-style shop; confirm exact address off the FB page).
- **Presence:** Facebook (`/quickerthanquickph`). `quickerthanquick.com` resolves but is a parked
  "lander", **not a real site**. **No working website.**
- **Contact:** Facebook Messenger. Grab an email/number off the FB About tab.
- **Pitch angle:** four trades under one counter (shoe/bag repair, key cutting, locksmithing,
  bespoke small leather goods) and no single page that lays them out. A site with a tabbed
  "what we do" board, a while-you-wait vs. leave-it list, and a quote form turns a confusing
  kiosk into a booked job.
- **Template:** four-service tabbed board (like SHALA's colour-chip tabs) + a drop-off / quote
  form.

### 3. Jackson Tailors — bespoke tailoring
- **Where:** Makati (confirm street address off FB).
- **Presence:** Facebook (`/jacksontailoring`). `jacksontailors.com` returns an ISP error page,
  `jacksontailoring.com` does not resolve — **no working website.** No Instagram found.
- **Contact:** Facebook Messenger. **Verify the shop is currently operating before pitching** —
  press coverage is a few years old and no 2026 listing was found.
- **Pitch angle:** the shop's story is strong (run by a stylist-menswear designer, son of a Hong
  Kong master cutter) and it is invisible online. A bespoke house sells on cloth, cut and process:
  a site with a "how a suit is made" walk-through, a cloth/lining gallery, a lookbook, and a
  consultation-booking form is the whole pitch.
- **Template:** editorial lookbook + numbered make process + fitting-appointment form. Adapts the
  MOOI "treatment index" typeset feel to menswear, drier and more tailored.

### 4. Studio Matisse — pottery studio + café
- **Where:** Makati (confirm address off IG; appears in 2026 Metro Manila pottery-class guides).
- **Presence:** Instagram only. `studiomatisse.ph` is **registered but serves only the default
  nginx welcome page** — no real site yet, though the registration says one is planned. No
  Facebook found.
- **Contact:** Instagram DM. No public email or phone found — grab off IG.
- **Pitch angle:** a pottery-studio-plus-café runs on class schedules, class types (hand-building,
  wheel, kids, private), a membership/open-studio option, and a booking calendar — none of which
  reads on a grid of IG posts. A real site with a class catalogue and a slot-booking form is a
  straight upgrade, and beats the half-built domain they already own.
- **Template:** class catalogue + schedule grid + booking form (COREX schedule pattern, softened
  for a craft studio — clay, kraft, hand-lettering).

### 5. Another Barbershop — neighbourhood barbershop + retail
- **Where:** Barangay Poblacion, Makati.
- **Presence:** Facebook (`/anotherbarbershop.poblacion`). **No website**, no own domain found.
- **Contact:** Facebook Messenger. Grab a number off the About tab.
- **Pitch angle:** a small Poblacion barbershop that also sells grooming product. Walk-in
  customers want the service list and prices, the barbers, the hours, and increasingly an online
  booking slot; product buyers want to see the shelf. All of it currently lives in the feed.
  (Distinct from the Sanbry attempt in batch 3 — smaller, grittier, retail-forward.)
- **Template:** price list + barber roster + a book-a-chair form + a small product shelf. The
  COREX booking pattern shrunk to a single-chair shop.

---

## Alternates (verify web presence + that they're operating before pitching)

| Business | Type / area | Presence | Note |
|---|---|---|---|
| Slick Barbers Co. | barbershop, Makati | FB `slickbarbersco` | No own domain found. Confirm it's still operating (in batch 8 as a core pick — move here if it doesn't check out). |
| Back Alley Barbershop | traditional barbershop, 1D Bautista St, Salcedo Village | IG `@backalleybarbershop` | `backalleybarbershop.com` shows a cPanel "Account Suspended" page — they had a site and let it lapse. Real opening, strong brief, but the lapsed domain is a flag. |
| Shū Reflexology | Xiamen-style foot reflexology, 58 Jupiter St, Makati | directory listings | No own domain found. Confirm FB/IG + operating. |
| EFREN Watch Repair | watch repair | FB `efrenwatchrepair` | Could **not** confirm a Makati branch (an "Efren's Watch Repair" operates in Ceby/Cebu malls). Do not pitch until the Makati location is confirmed. |

---

## How to work this list

- **Email-first:** none of the five publish an email. All are **DM / call-first**. Grab an email
  off each Facebook About tab first if there is one.
- **Build order that reuses work:** Easyshare "order desk" → Shoe Care; SHALA colour-chip tabs →
  Quicker than Quick; MOOI "treatment index" → Jackson Tailors; COREX schedule → Studio Matisse
  and Another Barbershop.
- **Re-verify before pitching** (the One World Butchers lesson): confirm each is currently
  operating in Makati and still has no site at the moment you send. Jackson Tailors is the
  shakiest on operating status.
