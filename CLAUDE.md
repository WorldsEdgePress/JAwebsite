# jessealexanderbooks.com — site conventions

Author site for the pen name Jesse Alexander (owner: Charissa; explain in plain
English, she approves each change in real time). Live at https://jessealexanderbooks.com
via GitHub Pages (repo WorldsEdgePress/JAwebsite). Workflow: edit → commit → push
immediately; changes are live in ~1 minute; verify live with curl after pushing.
If a change doesn't appear, check `gh api repos/WorldsEdgePress/JAwebsite/pages/builds/latest`
— builds can fail/queue. The `.nojekyll` file in the root disables Jekyll processing
(builds were failing without it) — NEVER delete it.
NEVER put this folder inside Dropbox (Dropbox corrupts git).

## Design tokens
- Colors: navy #2f2e40 (bg), indigo #343451 (cards), gold #f3cd5d (accents/buttons),
  gold-soft #f6eaae, tan #a18f63, dusty green #7D8F69 (newsletter), cream #fefefe.
- Fonts: Playfair Display (headings), Cormorant Garamond (everything else). Google Fonts.
- Background patterns (inline SVG data-URIs in css/style.css): `celestial` (stars) for
  paranormal/sci-fi/fantasy moods, `damask` (flourishes) for regency moods.
- Reviews band: cream-gold #e8dcb8 bg, quotes bold (600) 18px near-black navy #1d1c2e.
  Text on any gold/tan background must be bold and dark — she flagged readability twice.
- After ANY css/style.css change, bump the cache stamp on every page:
  `sed -i 's|style.css?v=N|style.css?v=N+1|g' *.html`

## Page inventory
index.html (home) · bookshelf.html (every cover in a tablet frame on CSS shelf
planks, newest first, NO ribbons/badges/text — hover shows the title) · book pages: the-space-between, forbidden-fruit,
the-dukes-christmas-consort, wolfsbane, bite-me-its-halloween (standalone, paranormal shelf) · series: hot-lemonade · genres: fantasy, regency,
paranormal-romance, futuristic (PURE shelves — the Duke lives on regency only; his
"Fantasy regency" badge is a flavor label) · freebies.html · redirect stubs:
fantasy-regency, sci-fi-fantasy, jessealexanderbooks/ (old QR codes — keep).

## Adding a new book (the checklist)
1. **Web cover**: from the original PNG (lives in her Kindle Vella folders — never
   modify originals), make a 640px-wide JPG q86 → `assets/covers/<slug>.jpg`.
2. **Book page** `<slug>.html` — copy an existing book page. Must have:
   - head: canonical + OG/Twitter tags (og:type book, og:image = cover, absolute
     https://jessealexanderbooks.com/ URLs) + JSON-LD Book (+BookSeries with position).
   - cover in `.cover-stage > .device-frame.float-anim` (tablet frame, gold glow, float).
   - series-tag, h1, gold italic `.hook` line, full back-cover blurb (hunt her docx in
     the book's Kindle Vella folder — use HER wording; offer 2 hook options, she picks).
   - badges: genre badge linking to the genre page + `.badge.ku` "Free on Kindle
     Unlimited" span; gold "Read on Amazon" button; formats-note if paperback/audio.
   - "Readers are saying…" `.reviews-band` ONLY when written reviews exist (quote
     verbatim, trimmed; ★★★★★ stars).
   - freebies section with that book's freebies; "More from this world" `.world-teaser`
     (add her video when she provides one — see Videos below).
   - `.fade-up` on lower sections + the IntersectionObserver script block.
3. **Home page**: add a `.book-card` to the grid — cover links to book page,
   `data-tags` for series/genre/standalone filters, hook + one-line blurb, badges,
   Amazon button AND "More about this book →" link (home keeps buy buttons).
4. **Series + genre pages**: add a fully clickable `<a class="book-row" href=...>` —
   cover, tag, title, hook, one-liner, KU badge span, `<span class="more-link">More
   about this book →</span>`. NO Amazon button on these compact rows (the book page
   sells; the whole card is the click). Remove the book from coming-soon spots.
5. **New series/genre?** Add a filter chip on home; a new genre gets its own page
   (shelves stay pure). Remaining brand genres when needed: erotic, contemporary.
6. **Bookshelf**: add a `.shelf-item` to bookshelf.html at the FRONT of the grid
   (newest first). Plain cover in a `.device-frame`, no ribbon.
7. **Metadata upkeep**: add the page to sitemap.xml and llms.txt.
8. Commit + push; curl the live URLs to verify; have her refresh and approve.

## Preorder lifecycle (template: Wolfsbane, July 2026)
1. **Announced, not yet buyable**: coming-soon card (release-date tag, "Preorder is
   coming soon", More-about link) + full book page with `.preorder-callout` (gold
   bordered box: "Preorder opens soon — special price until release day <date>" +
   Heartlines link). Badge slot shows "Releases <date>" instead of KU. Trope star
   bullets (`.trope-list`) welcome on book pages.
2. **ASIN exists (preorder open)**: add gold "Preorder on Amazon" button above the
   callout; move the book INTO the home "Books available now" grid with a
   "Preorder · releases <date>" badge; remove from coming-soon spots. Add sameAs
   (Amazon URL) to the page's JSON-LD. Add the series filter chip on home if new
   series. Slap the PREORDER ribbon on its covers: wrap the cover img in
   `<span class="ribbon-wrap">` + `<span class="ribbon">Preorder</span>` (remove
   ribbon on release day).
3. **Release day**: badge → "Free on Kindle Unlimited", button → "Read on Amazon"
   (keep the StoryOrigin universal link as href), delete the callout, update the
   page's meta/og descriptions from "Releases <date>" to "Out now", move the llms.txt
   entry from Preorder to Books. Ribbon text flips Preorder → **New**.
4. **The New ribbon** (her convention, Aug 2026; current holder: Bite Me, It's Halloween, Sept 2026): the newest released book wears the
   gold "New" ribbon on its covers sitewide. When the next book releases (or goes to
   preorder), it takes the ribbon and the previous holder's ribbon-wrap/ribbon markup
   is removed. Exactly one ribbon-wearer at a time.
5. **The "Working on / coming soon" section** (home, renamed Aug 2026): each
   soon-card carries a status `.next-tag` — "Coming in <month>" when a release window
   exists, "Working on" for WIPs; the nearest release gets the `featured` card style.

## Videos / animations
- One animation per page, max. Placement: the book page's "More from this world".
- Pattern: `.video-wrap > video.world-video` (muted loop playsinline preload="none",
  data-src, no src) + `.video-toggle` pause/play button + the lazy-load
  IntersectionObserver script (loads only when scrolled near; reduced-motion visitors
  get it paused). Copy source mp4 → `assets/video/<slug>-world.mp4` (keep ≤ ~25 MB).

## Freebies
- All StoryOrigin links. Cards are compact: mini-tablet-framed cover (automatic via
  `.freebie-cover` CSS), `.next-tag` label, title, ONE line, gold "Get it free".
- A new freebie goes on freebies.html under its book-world section AND on the related
  book page AND series page. Freebie covers: 300px-wide JPG → `assets/covers/freebies/`.
- Never list giveaways that are toggled OFF in StoryOrigin. (The old "Bite Me, It's
  Halloween" GIVEAWAY stays off — it grew into a full paid release, standalone, no
  series, coming September 2026. Don't confuse the two.)

## Voice and facts
- Hooks and blurbs in HER playful voice; salvage her existing wording verbatim
  (blurb docx files in the book folders; jokes are never paraphrased).
- Newsletter is "Heartlines" (MailerLite form 1458978/152857149836363327, double
  opt-in ON — success copy says check your inbox). Freebies for subscribers = the pitch.
- Forbidden Fruit characters: Cain (with a C) and Ash — Cain named first.
- Contact: Jesse@JesseAlexanderBooks.com. Privacy wording lives in the newsletter panel.

## Accessibility (she cares — keep these)
- No faint text on dark or gold backgrounds: bump weight/size/contrast instead.
- Text on GOLD surfaces (buttons, ku badges, active chips, ribbon) is near-black
  #14131d at weight 700 — never plain navy, she flagged it as hard to read.
- Every animation pausable; prefers-reduced-motion respected everywhere.
- Alt text on all covers; aria-labels on icon-only controls.
