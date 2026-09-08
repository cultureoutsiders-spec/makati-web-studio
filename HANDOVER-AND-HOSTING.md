# Handover & hosting — what you and the client each need

Covers the two ways a sale ends:

- **Path A — you host and manage it** (client pays the one-time fee + a monthly care plan).
- **Path B — client buys the code outright** and runs it themselves (one-time fee only).

Companion to `NEXT-STEPS.md` (workflow) and `PRICING.md` (numbers).

All prices are 2026 Philippine figures. Check current rates before quoting — they move.

---

## Path A — you host and manage the site

### Accounts you need (mostly free)

| Thing | Recommended | Cost | Notes |
|---|---|---|---|
| **Static host** | Cloudflare Pages | Free | Unmetered bandwidth, 500 builds/month, free SSL, free custom domains. One studio account holds many client sites as separate "projects". Netlify or GitHub Pages also work. |
| **Code storage** | One private GitHub repo per client | Free | Private repos are free on GitHub. Cloudflare/Netlify deploy from private repos for free (only *GitHub Pages itself* needs a paid plan for private repos — Cloudflare doesn't). One repo per client makes handover clean later. |
| **Domain** | Client buys it in their own account; you get access | ~₱600–₱1,200/yr for .com | See the ownership note below. If you hold it, use Cloudflare Registrar (at-cost, no markup) or Namecheap/Porkbun. |
| **DNS** | Whatever the registrar or Cloudflare provides | Free | Point the domain at the host with the records the host gives you (usually one CNAME + one TXT, or Cloudflare nameservers). |
| **SSL / HTTPS** | Automatic on Cloudflare Pages / Netlify / GitHub Pages | Free | Never pay for an SSL certificate for one of these sites. |
| **Contact-form backend** | Web3Forms | Free: 250 submissions/month, unlimited forms | If a busy hotel exceeds 250/mo, upgrade Web3Forms (~$8/mo) or switch to Formspree. |
| **Form destination email** | The client's existing inbox, or one you provision | See email table below | The form has to send *somewhere*. |
| **Analytics** (optional) | Cloudflare Web Analytics or Google Analytics 4 | Free | Add this so you can show the client visitor numbers. Cloudflare's version needs no cookie banner. |
| **Uptime monitoring** (optional) | UptimeRobot free tier | Free | Get an alert if the site goes down before the client notices. |

### Email options (the form needs a destination; the client may also want `info@theirbrand.com`)

| Option | Cost | Good for |
|---|---|---|
| Forward form mail to their existing Gmail / Yahoo | Free | Simplest. Most clients already have this. |
| Zoho Mail free plan | Free | 5 users, 1 custom domain, webmail only (no Outlook/phone IMAP on free). Fine for `info@brand.com`. |
| Google Workspace Business Starter | ~₱500–₱600/user/month (VAT-incl., via a PH reseller) | Client wants Gmail on their own domain, on phone and desktop. |

### Your recurring cost to run one managed site

| Item | Your cost |
|---|---|
| Hosting | ₱0 |
| Domain (only if you hold it) | ~₱1,000 / year |
| Form backend | ₱0 (under 250 submissions/month) |
| Analytics, monitoring | ₱0 |
| Email | ₱0 if forwarding; ₱500–₱600/user/month if you provision Workspace |
| **Your time** | a few minutes per edit: change file → `git commit` → `git push` → live in ~1 min |

So the monthly care fee (from `PRICING.md`: ₱1,800 intro / ₱2,500–₱3,500 market) is almost pure
margin. You're selling availability, backups and "someone who answers", not covering real costs.

### Your monthly workflow per managed client

1. Make any edits they asked for (text, prices, photos), push, confirm live.
2. Once a month: open every page, check it loads and looks right, refresh one thing (a promo, a
   seasonal line, a photo), check the year in the footer.
3. Check the analytics; send them a one-line "site's healthy, X visitors this month" note.
4. Watch the domain expiry date. Renew or remind them ~30 days out.

### Keep a record

A simple spreadsheet: client, repo URL, host project, domain, domain expiry date, form key,
email setup, monthly fee, who pays for the domain. This is the thing that saves you when you
have eight clients.

---

## Path B — client buys the code and runs it themselves

### What they now have to arrange and pay for

| Item | What it is | Cost | Frequency |
|---|---|---|---|
| **Domain registration** | The `theirbrand.com` name | ~₱600–₱1,200/yr for .com; some local TLDs cheaper | **Every year, or the site and email go dark.** Turn on auto-renew. |
| **Web hosting** | Where the files live | **₱0** on Cloudflare Pages / Netlify / GitHub Pages | Free forever for a static site this size. |
| **SSL certificate** | The padlock / HTTPS | **₱0**, automatic on the hosts above | — |
| **Form backend** | Web3Forms key (already in the site) | Free up to 250 submissions/month | Only pay if they outgrow it. |
| **Business email** | Destination for the contact form + their "email us" | Free (forward to existing) / Free (Zoho) / ~₱500–600/user/mo (Workspace) | Their choice. |
| **Someone to make edits** | A person who can open an HTML file, change words between the tags, save, and re-upload / `git push` | Their staff's time | Not "coding", but not nothing. If no one will, that's the care plan. |

**Tell them plainly:** these sites do **not** need a "web server", cPanel, or a ₱300–₱1,000/month
shared-hosting plan. A hosting salesperson will try to sell them one. They don't need it. If their
in-house IT insists on traditional hosting (Hostinger, GoDaddy, a local host), it still works —
just upload the site folder through the host's file manager or FTP — but it's an unnecessary cost.

### What they should understand about what they bought

- **It's a static site.** Fast, cheap-to-free to host, and very hard to hack (no database, no
  logins). The trade-off: **no admin dashboard / CMS.** Edits are made in the files. Great for
  cost and security, not great if they want to publish a blog post every week themselves.
- **No monthly platform fee to anyone.** Unlike Wix, Squarespace or Shopify, there is no rent.
  The domain is the only unavoidable cost.
- **It will not update itself.** Prices, promos, room rates, opening hours, the footer year —
  someone has to change them.
- **SEO is set up, not "done".** Page titles, descriptions, link-preview tags, `LocalBusiness` /
  `Hotel` structured data and a sitemap are all in place. Actually ranking on Google still needs
  their Google Business Profile, customer reviews, and time.
- **The photos are placeholders.** They're free-to-use stock. Real photos should replace them at
  the same filenames — especially anything showing a room or the actual shopfront.
- **Fonts** load free from Google Fonts. **The map** is a free Google embed, no API key, no cost.
- **Analytics is not installed** by default. They add Google Analytics 4 or Cloudflare Analytics
  if they want visitor stats.
- **Keep the zip.** If an edit breaks something, the folder you handed over is the restore point.
  (If it's in Git, every past version is recoverable.)

### The handover pack (give this with every Path B sale)

- [ ] The site folder(s), zipped — or access to a repo that's now theirs.
- [ ] A one-page "how to edit your text and swap your photos" guide.
- [ ] The list of what still needs doing: real photos, real reviews in the testimonial blocks,
      Web3Forms key pointed at their inbox, real Messenger/Instagram links, `noindex` removed,
      the "design proposal" footer line removed. (This is section 4.1–4.2 of `NEXT-STEPS.md`.)
- [ ] Where it's hosted and how to log in (host account, domain registrar, Web3Forms).
- [ ] A 30-minute handover call.
- [ ] A one-line written statement that they own the code, content and design outright.

---

## Selling a one-time "set it up for me" service (no retainer)

The client took the code-only deal, then asks you to put it live. This is a **one-off launch
fee**, not a retainer. Charge it separately, or bundle it into the intro price (see note below).

### What "setup / launch" includes

- Deploy the site to free hosting (Cloudflare Pages / Netlify / GitHub Pages)
- Connect their domain, confirm HTTPS is working
- Point the contact form at their inbox (Web3Forms key) and send a test
- Add Google Analytics 4 or Cloudflare Analytics
- Submit the sitemap to Google Search Console; link the site to their Google Business Profile
- Set up `info@theirbrand.com` — forwarding, or a Zoho / Workspace mailbox — if they want it
- Final QA on the live URL: every page, mobile, forms, links
- Hand over every login + a one-page "where everything is"

### What to charge (one-time, PHP)

| Scope | Price |
|---|---|
| Just deploy + connect a domain they already own | ₱1,500–₱2,500 |
| **Standard launch** (deploy, domain, form, analytics, Search Console, GBP link, QA, handover) | **₱3,500–₱5,000** |
| Full launch **incl. registering the domain for them** + email setup (MX / Zoho / Workspace) | ₱5,000–₱7,500 |

**Better option:** fold "standard launch" into the introductory price so you never actually sell
"just the code". A non-technical owner handed a zip with nothing live is an unhappy client and a
support headache. Make the ₱24,000 mean "built, live, and yours." Only quote a lower code-only
number (~₱16,000–₱20,000) when the client genuinely has their own web person.

### Is it hard?

Not for these static sites, once you've done it once.

- **Deploy:** Cloudflare Pages / Netlify — connect the repo (or drag-and-drop the folder), pick
  the output folder, deploy. Live on a temporary URL in about a minute.
- **Custom domain:** add it in the host's dashboard; it shows you one DNS record; paste that at
  the domain registrar. Wait 5 minutes to a few hours for it to propagate. HTTPS turns itself on.
- **Form:** create a Web3Forms key with the client's email, paste it into the form pages, push,
  send a test message.
- **Fiddly bits:** waiting on DNS, the odd confusing registrar panel, and email MX records if
  they want `info@`. None of it is hard, it just needs care and patience.
- **Time:** first client, give yourself a few hours plus some googling. After that, 30–60 minutes.

### Can this be done for you / automated?

- **Yes, for the deploy + config part:** connecting a repo, deploying, enabling Pages, wiring the
  Web3Forms key into the files, and writing out the exact DNS record for a given domain can all
  be handed off. (The five demo sites in this repo were deployed this way.)
- **No, for the parts that need an account holder:** buying the domain (it's a purchase),
  creating the Cloudflare / Netlify / registrar accounts, and typing passwords into dashboards.
  Those stay with you.
- **Practical split:** you spend ~10 minutes buying the domain and making the host account, then
  the repo setup, deploy, DNS instructions, form wiring and live QA can be done for you or from a
  click-by-click you follow once.

---

## FAQ — what a client will probably ask

**"Can I edit it myself?"**
Text and prices, yes — you change the words between the tags in an HTML file and re-upload.
Layout or new sections, ask me (or take the care plan).

**"Who owns it?"**
You do, outright, once the final payment clears — the code, the content and the design. It's in
the agreement.

**"What if you disappear or stop doing this?"**
You have the files and a how-to guide, and it's plain HTML, so any web person can pick it up.
That's a real advantage over a site locked inside Wix or a proprietary builder.

**"Is it secure? Can it be hacked?"**
It's a static site — no database, no login page, nothing to break into. About as safe as a
website gets. Just keep the domain and hosting passwords safe.

**"Will it show up on Google?"**
It's built to be found — proper titles, a sitemap, structured data. Ranking also needs your
Google Business Profile, reviews and a bit of time. I can link the site to your Google listing.

**"Does it work on phones?"**
Yes — built mobile-first. The menu becomes a tap-to-open drawer, columns stack, text resizes.
No sideways scrolling.

**"How fast is it?"**
Fast. No heavy framework; the images are the only real weight.

**"What are the ongoing costs if I run it myself?"**
Just the domain, about ₱1,000 a year, if you host on a free static host. Optionally a business
email and analytics. No monthly website fee.

**"Can you connect my existing domain and email?"**
Yes. Email is separate from the website and keeps working through any change.

**"How many revisions do I get?"**
Two rounds included in the build. After that it's the monthly care plan or a small per-change
fee.

**"How long does a change take after I've paid it off?"**
Minutes to a day, depending on the change and whether you're on the care plan.

**"Can I add a blog / online booking / a shop later?"**
Possible, quoted as new work. The site can grow. A real booking engine or online store is a
bigger project than a content page.

**"Can I see how many visitors I get?"**
Yes, once Google Analytics or Cloudflare Analytics is added — free, takes a few minutes.

**"Can you give me an official receipt / OR?"**
[Decide this before you start selling. If you're BIR-registered, yes. If not, say so upfront.]

**"Is there a contract?"**
Yes — one page: scope, price, payment schedule, ownership transfers on final payment, what's not
included, revision count. Protects both of us.

**"Refund if I don't like it?"**
[Your policy — `PRICING.md` suggests "not happy within 7 days of going live, full refund".]

**"Can you also do our social media / Google Ads / logo?"**
Separate services, priced separately.

---

## Things the client should take into consideration even if they don't ask

- **Put the domain in your own registrar account**, paid with your own card, in your business
  name — not your web person's. If it's in someone else's account you depend on them forever, and
  domain-ownership fights are how these relationships go bad.
- **Turn on domain auto-renew.** A lapsed domain takes the website *and the email* down, and
  someone else can grab the name.
- **Save every login** (registrar, host, Web3Forms, email) in a password manager. Don't keep them
  only in your web person's head.
- **Back up before you edit.** Keep the handover zip somewhere safe.
- **Whoever edits must check the result on a phone**, not just a laptop.
- **Don't buy hosting you don't need.** For this site, free static hosting is correct; a paid
  cPanel plan is money wasted.
- **Actually reply to the form submissions.** A contact form nobody checks is worse than no form.
- **Keep it current** — the footer year, this season's promo, current rates. A stale site reads
  as "closed".
