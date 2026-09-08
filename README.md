# Tokyo Gurlies 🎀🇯🇵

A single-file trip page for six days in Tokyo with Yanni, Sol and Susan, **Wed 25 – Mon 30 November 2026**
(5 nights, plus one day out of town). Same shape as the
[USA trip page](https://yannitan11.github.io/usa/): a Notion-style document with
view tabs, a month calendar, day-by-day itineraries, a saved-places list, an
editable budget and a packing checklist.

**Live:** https://yannitan11.github.io/tokyo/

## Status

Nothing is booked. Flights, hotel and the day trip are all shortlists rather
than plans, and every open item is marked `NOT BOOKED` / `TBC` on the page.
Replace them as they firm up — everything editable is `contenteditable`, and
the estimates table drives the summary tiles live.

## What's in it

| Tab | What it holds |
|---|---|
| **Overview** | November calendar (tap a day to jump), weather + daylight, outline flights, and the full itinerary browser |
| **Tokyo** | Six day-by-day plans, plus a curated places list you can add to |
| **Day Trips** | Kamakura, Hakone, Kawaguchiko and Nikkō written up in full — pick one for the Friday |
| **Flights & Stay** | Haneda vs Narita, four neighbourhoods compared, passes, eSIM, what sells out |
| **Tips** | How Japan actually works — money, trains, ordering, onsen, shrines, tax-free |
| **Budget** | Yen with a live SGD rate you can edit, estimates + a daily spending log |
| **Packing** | 45 items, checked off in `localStorage` |

## Technical

Vanilla single `index.html` — inline CSS and JS, no build, no backend, no
account. Auto-deploys via GitHub Pages (main / root).

- **Data:** the places list lives in `localStorage` (`tokyo-wishlist-v1`).
  Optional cross-device sync writes it to one private GitHub gist
  (`tokyo-places-sync.json`) using a gist-scope token held per device; merging
  is per-place with tombstoned deletes (`mergePlaces`, pure and testable).
- **Enrichment:** adding a place looks it up through Nominatim (OpenStreetMap)
  and the Wikipedia REST summary. Both are free, key-less and CORS-enabled,
  which is the honest ceiling for a public static page.
- **The itinerary browser borrows, never copies.** The overview's day panel is
  the same DOM node the city tab owns; `returnItinPanel()` puts it back in its
  original slot on the way out. Nothing is duplicated, so nothing drifts.
- **Colour does navigational work:** crimson is Tokyo, indigo is out of town,
  ginkgo gold is a flying day. Tokens are at the bottom of the `:root` block.

## Run locally

```bash
cd "Tokyo Travel"
python3 -m http.server 8000
```

Or just open `index.html` — there are no modules, so `file://` works too.

## Update and deploy

```bash
cd "Tokyo Travel"
git add -A
git commit -m "your message"
git push
```
