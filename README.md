# Tokyo Gurlies 🎀🇯🇵

A single-file trip page for six days in Tokyo with Yanni, Sol and Susan — fly
**Tue 24 Nov 2026**, in the city **Wed 25 – Mon 30 Nov**, home Tue 1 Dec (plus
one day out of town). Same shape as the
[USA trip page](https://yannitan11.github.io/usa/): a Notion-style document with
view tabs, a month calendar, day-by-day itineraries, a saved-places list, an
editable budget and a packing checklist.

**Live:** https://yannitan11.github.io/tokyo/

## Status

Flights and the flat are booked — JAL **JL36** out of Changi 22:25 on Tue 24
Nov, landing **Haneda 05:55** on the 25th, and **JL711** home from **Narita**
18:10 on Mon 30 Nov. An entire apartment in **Asakusabashi** (Taito City) from
the 24th, which means the dawn arrival has somewhere to put its bags. The only
open decision is which day trip to take on the Friday. A handful of shops carry
a `verify` badge because I could not confirm their address — those are unknowns,
not decisions.
Replace them as they firm up — everything editable is `contenteditable`, and
the estimates table drives the summary tiles live.

## What's in it

| Tab | What it holds |
|---|---|
| **Overview** | November calendar (tap a day to jump), weather + daylight, outline flights, and the full itinerary browser |
| **Tokyo** | Six day-by-day plans, plus a curated places list you can add to |
| **Day Trips** | Kamakura, Hakone, Kawaguchiko and Nikkō written up in full — pick one for the Friday |
| **Vintage** | Secondhand luxury bags: the condition grading scale, the four shopping districts mapped onto the days, what Tokyo is actually cheap for, and what to check before buying |
| **Flights & Stay** | Both airport runs, what the Asakusabashi flat is plugged into, living there, passes, eSIM, what sells out |
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

## Itinerary rewrite (2026-11-12)

- **Friday 27 Nov is Mount Fuji, decided** — by train: Fuji Excursion 3 from Kinshichō 07:07 → Shimoyoshida 09:13
  (Chūreitō Pagoda) → Kawaguchiko (hōtō, Ōishi Park) → Fuji Excursion 44 at 16:48 → Shinjuku 18:48 → Negishi.
  The full plan is `#tokyo-day-3`; the Day Trips tab is now the bad-weather bench and points back at it.
- **Yanni's eight named places each have a day**, marked with a `.must` "on your list" badge: Moheji (Wed),
  Café Heckeln + Maisen + OH KAMA BAR (Thu), Negishi (Fri), Kinboshi Pasta (Sat), Onibus Coffee (Sun),
  Shiraishi (Mon). Kinboshi and Shiraishi are best guesses and carry `.tbc` verify badges.
- **Overview gained a booking board (`.bk-board`) and an eat list (`.eat-grid`)**; rows call `goDay(n)`.
- **Every day has a `.route` strip** under the day head. Day 2 no longer includes Meiji Jingū or Takeshita.
