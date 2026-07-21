# jessealexanderbooks.com — site conventions

Author site for the pen name Jesse Alexander (owner: Charissa; explain in plain
English, she approves each change in real time). Live at https://jessealexanderbooks.com
via GitHub Pages (repo WorldsEdgePress/JAwebsite). Workflow: edit → commit → push
immediately; changes are live in ~1 minute; verify live with curl after pushing.
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
index.html (home) · book pages: the-space-between, forbidden-fruit,
the-dukes-christmas-consort · series: hot-lemonade · genres: fantasy, regency,
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
6. **Metadata upkeep**: add the page to sitemap.xml and llms.txt.
7. Commit + push; curl the live URLs to verify; have her refresh and approve.

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
- Never list giveaways that are toggled OFF in StoryOrigin ("Bite Me, It's Halloween"
  is off as of July 2026).

## Voice and facts
- Hooks and blurbs in HER playful voice; salvage her existing wording verbatim
  (blurb docx files in the book folders; jokes are never paraphrased).
- Newsletter is "Heartlines" (MailerLite form 1458978/152857149836363327, double
  opt-in ON — success copy says check your inbox). Freebies for subscribers = the pitch.
- Forbidden Fruit characters: Cain (with a C) and Ash — Cain named first.
- Contact: Jesse@JesseAlexanderBooks.com. Privacy wording lives in the newsletter panel.

## Accessibility (she cares — keep these)
- No faint text on dark or gold backgrounds: bump weight/size/contrast instead.
- Every animation pausable; prefers-reduced-motion respected everywhere.
- Alt text on all covers; aria-labels on icon-only controls.
