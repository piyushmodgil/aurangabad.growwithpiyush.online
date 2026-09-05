# GWP Aurangabad Landing Page — Build Notes

## Latest: single-keyword SEO focus (header vs. body)
The hero/header now targets **one** primary keyword — "Best Digital Marketing Services in
Aurangabad, Bihar" — instead of naming all four towns in the H1. This is deliberate SEO
practice, not a content cut:

- **Google ranks focused pages better than diluted ones.** An H1/title trying to rank for
  "Aurangabad," "Daudnagar," "Haspura," AND "Obra" simultaneously competes with itself and
  usually ranks weaker for all four than a page that commits to one primary target and lets
  secondary terms live in the body.
- **What changed in the header specifically:** the eyebrow, `<h1>`, hero photo alt text, and
  the photo caption overlay now say only "Aurangabad, Bihar." Title tag, meta description,
  and Open Graph tags follow the same single-keyword rule.
- **Where Daudnagar/Haspura/Obra still live (on purpose):** the "Areas We Serve" section
  (each town gets its own heading + paragraph — this is what tells Google those pages are
  relevant to those searches too), two of the six service card descriptions, the FAQ (two
  questions name them directly), the footer, and the lead form's area dropdown. Nothing
  was removed — it moved from the header into the body, which is where it actually helps
  rather than dilutes.
- **"Best" was added** to the title, meta description, H1, and hero image alt text — a
  common, high-intent modifier for local searches ("best digital marketing agency near
  me"-style queries). It's backed immediately by the stat ticker and trust line beneath it,
  so it reads as substantiated rather than a bare claim.
- **Title/meta length:** title is 71 characters (Google's soft cutoff is ~60–65, but this
  isn't a ranking penalty, only a display-truncation risk on some result widths); meta
  description is 148 characters, comfortably inside Google's ~155–160 char display limit.
- If you later want a **second page ranking Daudnagar** (or Haspura/Obra) as its own
  primary keyword, the standard approach is a *separate* page per town rather than trying
  to rank one page for all of them — happy to build that if it's worth it for your traffic
  volume in those towns specifically.

## Design system
Matches the visual language of your main site (`growwithpiyushlanding.html`):
Sora + Inter + IBM Plex Mono type system, navy/orange palette, animated stat ticker,
numbered service cards, dark/light section rhythm, a real inline lead-capture form, and a
floating WhatsApp button. Still a single self-contained `index.html` — no build step —
deployed alongside its `assets/` folder.

**Deploy as a unit:** `index.html` and `assets/` must stay in the same folder.

## What changed from the previous version
- **Typography & palette** now match your main site exactly: Sora for headings, Inter for
  body copy, IBM Plex Mono for labels/numbers/stats — loaded from Google Fonts with
  `preconnect` + `display=swap` so it doesn't block the first paint.
- **Sticky header** with a text-based wordmark (`GROW WITH PIYUSH` — swap in your real
  `logo.png` under `assets/` and I'll wire it into the header/footer `<img>` tags if you
  send it over) and a WhatsApp CTA.
- **Animated stat ticker** below the hero — the credentials that were a static strip before
  now scroll continuously (pauses on hover), matching your main site's signature element.
- **Numbered service cards** (01–06) in a seamless grid instead of individually bordered
  boxes — same visual system as your Ranchi page's services section.
- **Credibility cards** (①②③) for "Why Choose GWP," dark/light alternating sections for
  rhythm, and a proper multi-step "Our Process" row.
- **Real inline lead form** at the final CTA (name, business, WhatsApp number, area,
  service, goal) that builds a structured WhatsApp message on submit — same pattern as your
  main site's audit form, and more useful than a plain WhatsApp button since it captures
  intent before the chat even starts. The Hero's primary CTA scrolls down to this form; a
  ghost "Chat on WhatsApp" button next to it, the mid-page CTA, and a floating WhatsApp
  button in the corner all still fire an instant WhatsApp chat for anyone who doesn't want
  to fill a form.
- **Recognition/photo grid** kept from the previous version — your six real photos
  (Governor's Award, newspaper coverage, Mumbai billboard, workshops), still WebP+JPEG with
  lazy loading.

## Still true from before
- All SEO copy, section order, and keyword placement from the original handoff spec —
  nothing was cut, only re-skinned.
- `LocalBusiness`, `FAQPage`, and `BreadcrumbList` JSON-LD schema in `<head>` (validated).
- Meta title/description and Open Graph tags as specified.
- GA4 (`whatsapp_click` with a `location` param — now: `nav`, `hero`, `mid-page`,
  `final-band`, `floating-button`) and Meta Pixel (`Contact`) events on every WhatsApp
  touchpoint; `faq_expand` per accordion open. Both scripts load only after `window.load`.

## Before you launch
1. **Swap the two placeholder IDs** near the top of the `<script>` block:
   `GA4_MEASUREMENT_ID` and `META_PIXEL_ID`.
2. **Send me your logo file** (or drop `logo.png`/`logo.svg` into `assets/`) if you want
   the real GWP mark in the header/footer instead of the text wordmark — five-minute swap.
3. **Point "Learn more" links** at your real service page URLs — currently assume
   `growwithpiyush.online/services/<slug>`.
4. **Confirm the address block** in the `LocalBusiness` schema — only `addressRegion: Bihar`
   is filled in.
5. **Verify the breadcrumb** JSON-LD matches your actual site nav (assumes an "Areas We
   Serve" parent page at `/areas-we-serve`).
6. **Re-check the Open Graph image URL** once hosted — assumes the page lives at
   `growwithpiyush.online/digital-marketing-services-aurangabad-bihar/` with `assets/`
   alongside it.
7. **Still missing:** an actual client results/analytics screenshot for the Recognition
   section — left out rather than faked, per the spec's "real, verifiable images only" rule.

## Matching the main site's stack
Still plain HTML/CSS/JS rather than React + Vite — zero build tooling, deploy today the same
way the Orientation 2026 site went out. The sections here map cleanly to components if you
later want this as a route inside the main React app.

## Performance
No render-blocking scripts above the fold; CSS is inlined; analytics defers until after
load; every photo is compressed WebP with JPEG fallback (hero eager, rest lazy). Google
Fonts adds one network hop for type — traded deliberately for the more premium look you
asked for, mitigated with `preconnect` and `font-display: swap`.
