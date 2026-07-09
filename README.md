# Fernweh

**Live:** https://bswxyz.github.io/fernweh-cabins/ · **Build notes:** https://bswxyz.github.io/fernweh-cabins/guide/

An off-grid cabin & slow-travel booking site for people who need to be unreachable for a while —
part of the [Parable 25 design showcase](https://bswxyz.github.io/fable-hub/).

---

## The concept

Fernweh (*n. — an ache for far-off places*) is a fictional collection of nine architect-built
cabins, hours past the last paved road. The product sells absence: no wifi, no cell signal, no
hurry — so the site treats remoteness as the amenity. Distance tables replace star ratings,
"no wifi" is a feature chip, the dark-sky rating is a Bortle number, and the booking card
promises a human reply "within two days" instead of an instant confirmation. One AI-generated
photograph carries the hero; everything below it is drawn — layered SVG ridgelines, mist,
stars, and three line-illustrated cabins.

## Design system

- **Palette (deep forest):** `--bg:#26302a` · `--panel:#2e3a33` · `--ink:#eae3d5` warm paper ·
  `--dim:#b8ae9b` · `--faint:#77816f` (decorative only) · `--sand:#c8b393` (the single warm
  accent) · `--moss:#7d8a5f` (the anti-amenity green) · one cream interlude `#e7d8c3` for the
  seasons band · `--line:rgba(234,227,213,.10)`.
- **Type:** `Spectral` (literary serif — display and manifesto) · `Inter` (UI/body) ·
  `Space Mono` (everything measured: coordinates, kilometres, Bortle ratings, temperatures,
  prices-per-night). The mono is what makes remoteness read as fact rather than copywriting.
- **Signature motion:** one long, lazy easing — `cubic-bezier(.19,1,.22,1)` — used for
  everything. Reveals take 1.15s, the hero photo settles from `scale(1.07)` over 3.2s, the
  ridge parallax drifts a fixed amplitude across the whole page. Nothing on the site hurries,
  because that is the product.
- **Voice:** quiet longing, anti-hustle. "The signal fades. You won't miss it."

## Stack

- **[Astro 5](https://astro.build), zero client framework.** The page is content-heavy and
  static: cabins, seasons and copy render from typed data arrays at build time. The only
  JavaScript shipped is one small inline script — parallax, scroll reveals, counters, nav
  state, and the booking-card arithmetic.
- **No component hydration.** `<Ridges />` and `<CabinArt kind="ember" />` are server-rendered
  SVG components — reusable like React components, weightless like markup.
- **Google Fonts** (Spectral / Inter / Space Mono), **no other dependencies.**
- Interaction patterns researched on Mobbin: Airbnb's price-first booking card and amenity
  grammar, Booking.com's name→distance tables, Tripadvisor's availability-as-a-calm-fact.

## Running it locally

```bash
git clone https://github.com/bswxyz/fernweh-cabins
cd fernweh-cabins
npm install
npm run dev        # dev server at http://localhost:4321/fernweh-cabins/
npm run build      # static build into ./docs (what GitHub Pages serves)
```

## Structure

```
astro.config.mjs            site/base/outDir — the whole GitHub Pages recipe
src/pages/index.astro       the page: data arrays, markup, and the one client script
src/pages/guide.astro       the "how it was built" write-up → /guide/
src/components/Ridges.astro the fixed parallax ridgefield (5 SVG ridges, mist, stars)
src/components/CabinArt.astro  the three hand-drawn cabin nightscapes
src/styles/global.css       all styling — design tokens live in :root at the top
public/assets/hero.jpg      the single photograph
public/.nojekyll            tells Pages to serve the build as-is
docs/                       committed build output (Pages serves main + /docs)
```

## Demo vs. real — what a production version would need

This is an intentionally-scoped design study. What's **fictional/mocked** today:

- **The cabins don't exist.** The Ember, The Sova and The Lichen — names, coordinates,
  distances, Bortle ratings, prices — are all invented for the design.
- **No booking backend.** The card does real arithmetic (rate × nights, guest capacity
  checks) in client state, but "Request to book" sends nothing and says so. A real version
  needs an availability calendar, a request/hold flow, payments and email.
- **The date "windows" are curated chips,** not a date-range picker. A real product needs a
  full calendar with per-cabin availability and seasonal pricing.
- **The hero photograph is AI-generated.** A real brand would shoot its actual cabins
  (and the other six would need to exist).
- **No accounts, reviews, host tooling, or cancellation logic** — the fine print about
  letters and two-day replies is voice, not infrastructure.

What's **real** and reusable as-is: the layered ridge-parallax system (amplitude-based, seam-
free, reduced-motion safe), the booking-card state model, the amenity/anti-amenity grammar,
the SVG cabin illustrations, and the full responsive/keyboard/reduced-motion layer.

## License

[MIT](LICENSE). Design & build by **Parable** (Anthropic's Claude). The hero image is
AI-generated; the cabins are fictional and no real booking service is implied.
