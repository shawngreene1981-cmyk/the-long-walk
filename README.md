# The Long Walk

An interactive map of human migration and knowledge loss across 1.8 million years.

**Live map: https://shawngreene1981-cmyk.github.io/the-long-walk/**

A timeline scrubber drives everything. Nothing on the map exists until the
scrubber reaches its date, so the map is watched as much as read.

## What is on it

| | |
|---|---|
| Anchors | 552 (34 flagged leaders) |
| Migration routes | 111 |
| Leader walk-backs | 15 |
| African corridor connectors | 6 |
| Era checkpoints | 66, across 11 ages |
| Sea-level curve | 18 points |

Plus territories, capabilities, diffusions, pauses, continental shelves, ice
sheets, ghost branches, origin nodes and trade routes. The timeline runs to
1999 CE.

## Every anchor carries an evidence tier

| Tier | Count | |
|---|---|---|
| Well-supported | 407 | |
| Contested / disputed | 111 | |
| Pre-*sapiens* hominin | 26 | a separate category, not a weaker one |
| Tradition | 6 | held and transmitted, not excavated |
| No verified evidence | 2 | |

Roughly 20% of this map is flagged contested — and that is the point, not a
defect. The aim is to show *how well each claim is supported*, not to assert
what happened. A contested anchor is drawn as prominently as a solid one, in a
different colour, so you can see the shape of the disagreement instead of
having it quietly resolved for you.

## Palaeo-shorelines: global, at the source's own resolution, and on by default

Half the routes here only make sense at low sea level — Beringia was a country,
Doggerland an inhabited landscape, Sundaland continuous land.

**The shelf is drawn from the source itself, for the whole world.** The layer shows
**De Groeve et al. 2022**'s coastline-age raster — the only global shoreline
reconstruction with a real glacial-isostatic correction (SELEN4 sea-level solver,
ICE-6G_C ice history, VM5a mantle) — as Web Mercator tiles in `tiles/floodage/`
(668 tiles, 1.46 MB; a view loads only its own), one byte per cell. **Nothing is
simplified, smoothed or removed**, and there are **no region boxes**, so no edge of the
drawing is a box edge. The sea takes the land back **in the source's own 0.5 kyr steps**,
on the source's own dates. Zoomed past level 5 the square 2-arc-minute cells show:
that is the reconstruction's real resolution, and the map does not smooth it into a
precision the source does not have.

The shelf is drawn **as land**, opaque, in the basemap's land colour, under every route
and marker, so at the glacial maximum the continents are simply bigger. Before the
glacial lowstand (~21,000 years ago) the raster records only the most recent coastline,
so ground exposed only at the lowstand shows a little early; the popup says so.

**The HUD follows the drawing.** The five named shelves (Beringia, Doggerland, Sunda,
Sahul, the Persian Gulf) are *walkable* while more than half of their glacial-maximum
shelf is drawn, *drowning* while more than 2% is. Their research dates stay in their
popups; where the source differs — Beringia still 20% exposed at its researched closing
date of 10,500 years ago, Sunda gone by ~8,000 against a researched 7,000 — **the popup
states both and picks neither.** Which named popup opens is chosen by the old region
boxes, which draw nothing.

**The source and this map's global sea-level curve disagree, by tens of metres.** In the
De Groeve raster the shelves flood while the curve still reads the sea lower. Measured
against ETOPO 2022 depths, 8,000–20,000 years ago, the source floods higher by:

| region | |
|---|---|
| Sunda | 18–38 m |
| Sahul | 22–36 m |
| Persian Gulf | 15–33 m |
| Doggerland | 9–19 m |
| Beringia | up to 20 m (and 4–8 m lower before 14,000 ya) |

Every other popup gives the figure measured for its own 10° cell
(`data/floodage/divergence_grid.json`), or says none could be measured there. De Groeve
et al. publish no regional sea-level curve and do not discuss the difference: it is
observed in their raster and not explained in their paper.

**From 26,000 years ago to the present this is a reconstruction** (solid coastline).
**From 26,000 back to 90,000 years ago it is an APPROXIMATION, not a reconstruction**
(dotted coastline): no reconstruction exists there, so the map draws the source's coast
for the date its own sea-level curve last stood at the same depth, with **no
glacial-isostatic correction** — most wrong near the ice, which across the world means
most of the northern shelves. The curve is coarse there: four points between 26,500 and
130,000 years ago, with straight lines across 50,000 and 40,000 years. The switch at
26,000 years ago is instant, the HUD names which side you are on, and a mark on the
timeline shows where it falls. **Before 90,000 years ago nothing is drawn, anywhere** —
the oldest researched shelf window, applied to every shelf at once, because a time limit
draws no edges.

If the shoreline data fails to load, the map says so beside the switch and in the HUD,
and ticking the switch again retries.

The layer is **on by default**. It was switched on after the global layer had been looked at on the live site; untick it to see today's coastline alone.

Shoreline data: De Groeve, J., Kusumoto, B., Koene, E. *et al.* (2022). Global raster
dataset on historical coastline positions and shelf sea extents since the Last Glacial
Maximum. *Global Ecology and Biogeography* 31(11): 2162–2171.
https://doi.org/10.1111/geb.13573 — raster (AGE 2021) via Figshare,
https://doi.org/10.21942/uva.c.5754779.v1, licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Changes were made:** the
coastline-age raster was re-encoded as one byte per cell (its 0.5 kyr coastline step,
modern land, or open sea) and reprojected to Web Mercator tiles at zoom 0–5 by nearest
neighbour. Nothing was simplified, smoothed or removed.

## The GIS job — status

**1. Palaeo-shorelines — global pass built from the source raster itself; looked at, and on by default.** See above.

**2. Border acts — 3000 BCE to 1500 CE, forty-five century acts, drawn for everyone since 2026-09-21** (3000 BCE–1 CE and the 1000–1100 CE trial since 2026-09-18).
Each act is built into `data/borders/` as a timed grid of 0.1° cells (`act_<from>_<to>.bin` with its `.json`
header; built by `geowork/borders/build_act.py`, listed in `data/borders/acts.json`), and the layer loads the act for
the date on screen. Each act is built seeing a century either side, so two acts agree on the year they share, and the
date two powers first met is carried from act to act (`geowork/borders/postpass_pairs.py`), so a frontier lit in one
century does not go dark at the next; `geowork/borders/check_boundaries.py` and `check_seams.py` test both. Where
Cliopatria's own label contradicts its shapes or dates (“Later Zhou” for the Eastern Zhou, “Great Yuan” linked to the
Mongol Yuan, a Macedonian “Empire” from 675 BCE, the “Athenian Coalition”), the popup says so and the map draws it as
the source does (`geowork/borders/source_notes.json`). An insignia is ATTESTED only with a named object, its date
inside the polity's dates and a source, and is drawn only where a source records what the device looked like; the
legend counts them off the table the map draws from, and says how many polities were never examined, so an
ILLUSTRATIVE mark is never read as a polity that had no device. A polity may hold more than one device, each in its own
window of use (England: the long cross, then the three lions). The layer and the tier
change went live together, in one push: the anchor dots are one warm neutral, the evidence tier is in their tooltip and
popup and still in their shape, and colour belongs to the borders. `?borders=0` opens the map without borders, with the
tier colours on the dots. Only two routes on this map carry dated vertices — the Norman routes to Aversa and Pevensey, 1016–1072 — so no other
route seeds a spread: an undated route is not made to carry one. `?borders=next` and `?borders=1` are flags from
before the flip; they change nothing now, and the page says so on screen, as it does for any value it does not know.
Cliopatria includes a polity only where written sources give its location and extent, so it is thin wherever writing
was: the Americas, Oceania and Africa south of the Sahara are under a tenth of their land drawn in every century.
Wherever a region the source barely covers is on screen, a rust line under the HUD says so, with numbers from
`data/borders/coverage.json` (`geowork/borders/coverage.py`); nothing from any other source is drawn to fill it. In that mode, and only in it, the evidence
tier leaves the anchor dots and goes into their tooltip and popup, so colour belongs to the
borders; the dots are one warm neutral and the tier is still carried by shape. Between two
dated Cliopatria shapes the growth and retreat you watch is drawn by the map, not recorded
in the source, and the layer says so. Every insignia is labelled ATTESTED or ILLUSTRATIVE.
The other 55 acts are in
`data/acts/` with a manifest and are not drawn; `?borders=preload` fetches and parses every act in the background,
ahead of the playhead first, so the 25-year acts that are on screen for a tenth of a
second are already in memory when playback reaches them. Cliopatria v0.2.0 (GitHub release tag,
CC BY 4.0; Bennett *et al.* 2025, *Scientific Data* 12, 247,
https://doi.org/10.1038/s41597-025-04516-9) cut into centuries before 1500 CE and
half-centuries after, at 0.25° / 2 dp, with every invalid geometry repaired. The
budget per act is 822,136 bytes — the map's own measured size, read literally — and
**an act that exceeds it is cut finer**: the budget is a density detector, not just a
file-size cap. One act did: 1900–1950 became two 25-year acts.

**3. The Colonial Act, 1500–2024 — ruled 2026-09-28, not built.** Six rulings, against
`SCOPE_Colonial_Act_1500_to_2024.md`. **C1:** a flag is drawn for a polity only where a flag is *attested in use at
that date*, the same bar as the insignia; where none is attested the polity keeps insignia treatment. Measured, that
makes the act an insignia act until about 1800 and a flag act after: under provisional first-flag dates, 0% of the
colonial ground drawn in 1550 has a flagged holder, 2% in 1650, 3% in 1750, and 100% by 1850. **C2 and C3 — measured, then withdrawn (2026-09-28): there is no flag wash.**
The measurement (`geowork/borders/c3_black_contrast.py`, against the forced-route black as actually drawn at Luanda,
RGB 3/9/15 on ground already only 13.1 ΔE away) found black failing in both directions at every weight — 4–15 ΔE from
the route black, inside the palette's own floor of 23, and barely marking the ground — and dark blue, which is in the
Dutch, French and British flags, failing below 0.45. A wash at 0.6 with a lightness floor was ruled and then
**superseded**: a grey German flag is not the German flag. **The ground keeps the palette fill, and the flag is
carried whole — unaltered colours, true black included — in the tooltip and in an insignia-sized badge**, in the
grammar the insignia layer already uses. **The forced routes keep black to themselves.** **C4 — approved as measured:** the thin-source note extends past 1500. A region is
**thin** where under a tenth of its land is drawn (the existing note, unchanged), and **claimed** where more than half
of the land drawn there is held by a power whose home is elsewhere; the two are disjoint by construction. The
possession share is read **from the polygons**, never from the source's `MemberOf` field, which undercounts badly:
it misses **Portugal, Germany, Belgium, Denmark and Spain**, each of which holds colonies inside its own metropolitan
polygon with the field left blank. Corrected shares of the drawn land — the Americas **97% in 1550, 94% in 1650, 96%
in 1750**; South Asia **76% in 1850** and 82% in 1913; Africa south of the Sahara **85% in 1913**, 73% in 1950;
Southeast Asia 75% in 1913; North Africa and the Near East 68% in 1913, 53% in 1950. The `MemberOf` figures in
`SCOPE_Colonial_Act_1500_to_2024.md` are superseded and must not be read as current. **Occupier attribution has no
ground truth in the source and was wrong twice in one pass, so it carries its own fixture
(`geowork/borders/check_attribution.py`) that must fail on a broken rule before it is trusted; nothing is drawn until
it passes.** **C5:** flag research is commissioned at the C1
bar, about twenty occupiers, none drawn until cited. **C6:** a few sourced colonial routes, matched **by route id,
never by proximity** — Point Comfort lands 0.6° from the English first shape, so a proximity match would bind the
arrival of enslaved people to a colonial fill. **The three forced routes are untouched and exempt from every rule in
this act, as before.** The occupier is read from the polygon, not from the source's `MemberOf` field: Portugal's
Angola and Mozambique sit inside "Portuguese Republic" and "Estado Novo" with a blank `MemberOf`, and so do the German
Empire's colonies, Belgium's, Denmark's Greenland and Spain's.

**Corrected 2026-09-28, shipped on its own: the region map.** The regions the thin-source note is measured over
(`geowork/borders/regions.py`, written into `data/borders/coverage.json`) matched the Near East box **before** Europe,
so **every place below 42°N — Iberia, southern Italy, Greece and Turkey-in-Europe — was counted as North Africa and
the Near East**, and Tibet's box reached 73°E and took Delhi into Inner Asia. Both were live in the note and in the
legend. The corrected map carves out Turkey-in-Europe, Crete and Malta first, separates the African coast from Iberia
by longitude (latitude alone cannot: Tangier is 35.8°N and Seville 37.4°N at the same longitude), groups the Sahel
south, and only then matches Europe. It is checked against 44 cities — **44 right, against 29 before**: twelve European cities from Lisbon to Istanbul, Delhi and Amritsar, and Timbuktu — by
`python borders/regions.py`. The change moves Europe's land area **+11%**, the Near East's **−10.5%**, Africa south of
the Sahara's **+5.4%** and South Asia's **+3.9%**; the thin note stops firing in three act-regions it should never
have covered (South Asia at 2300 BCE, Europe at 500 BCE and 100 BCE) and starts firing in none.

**The limits of occupier attribution, recorded so they are findable later.** Whether ground is held by a power whose
home is elsewhere is decided by `geowork/borders/check_attribution.py`, which carries a fixture of known cases and
must fail on a deliberately broken rule before it is trusted. Two things it cannot see, by construction:
**a possession inside the holder's own region** — the rule compares regions, so **Korea under Japan, 1910–1945**, is
invisible to it; and **Russian America (Alaska, 1741–1867)**, because Russia is deliberately left out of the
home-region table so that Siberia is never called a colony, and Alaska goes with it. Both are limits of the rule, not
oversights.

**4. Ice sheets — real margins where the evidence reaches, nothing where it does not.** North America
from **NADI-1** (Dalton *et al.* 2023, CC BY 4.0) from 25,000 years ago, every 500 years; Eurasia,
including the Svalbard–Barents–Kara sheet, from **DATED-1** (Hughes *et al.* 2016, CC BY 3.0) from 38,000
years ago; Patagonia from **PATICE** (Davies *et al.* 2020, **CC BY-NC 3.0 — see the licence table**) from
35,000 years ago. Files in `data/ice/` (`nadi1_0.json`, `nadi1_1.json` cut by time under the budget,
`dated1.json`, `patice.json`), built by `geowork/ice/build_ice.py`. Each is drawn in its own time slices, never
interpolated, with its own uncertainty: minimum, best estimate and maximum. Before those dates no ice is drawn:
the four old boxes were removed on 2026-09-18, the same treatment as the shoreline floor. The blank is where the
mapping stops, not the ice. Batchelor *et al.* 2019 is still unlicensed and no longer needed for the last glacial
maximum: the two clean alternatives were never checked until 2026-09-17.

**3b. The Green Sahara — the land greens, then sand again; the dates are sourced, the shape is drawn.** The
placeholder circle is gone. `data/sahara/` (`field.bin`, `field.json`, `rivers.json`), built by
`geowork/sahara/build_sahara.py`. Sourced: when (Armstrong *et al.* 2023's precession pacing; the Holocene window,
Shanahan *et al.* 2015), how far at full (31°N, Tierney *et al.* 2017), and where the desert is (Natural Earth's
SAHARA polygon, public domain; its river centrelines name the modern perennial rivers, which are not drawn). Drawn by this map and labelled so: the shape of the greening (a front with a soft,
terrain-shaped edge) and the rivers — drainage computed from ETOPO 2022 (CC0) by priority-flood and D8 flow
accumulation, not mapped palaeochannels, none of which are released as licensed data.

**5. A self-hosted shaded-relief basemap — the default.** Looked at on the live map and on a
phone, and switched on; `?relief=0` still gives OpenStreetMap. The map used to sit on plain
OpenStreetMap: a road map with prehistoric shapes on it. Every hosted alternative was
rejected — Stamen retired and keyed, Esri's relief under a licence written for
licensees, NASA's CC0 Blue Marble painting *modern* vegetation across an Ice Age map.
So it is rendered here from **ETOPO 2022** (NOAA, CC0 1.0), which includes bathymetry,
toned to the map's own ground so the palette holds (worst overlay keeps 94.3% of its
contrast), and cut into Web Mercator WebP tiles to zoom 5 in `tiles/relief/`
(1,365 tiles, 12.1 MB).

## Citing a single anchor

Every anchor has its own address, so a specific claim can be linked directly
rather than asking someone to go and find it. Add `?a=<id>` to the URL:

```
https://shawngreene1981-cmyk.github.io/the-long-walk/?a=cn10
```

That opens the map focused on **Yinxu (Yin Ruins) — the oracle bones**, with
the timeline already set to its earliest dated evidence (~3,276 years ago) and
its popup open.

**You do not need to know the id.** Open any anchor on the map and click
*"Copy link to this anchor"* inside its popup — that gives you the full URL,
ready to paste into a video description, a reply, or a footnote.

A moment in time can be cited the same way with `?t=`, in years before present:

```
https://shawngreene1981-cmyk.github.io/the-long-walk/?t=64400
```

Both forms also work as a hash (`#a=cn10`) for tools that strip query strings.
An unrecognised id is ignored rather than treated as an error, so a truncated
link still opens the map.

### Citation

> Greene, Shawn. *The Long Walk: an interactive map of human migration and
> knowledge loss*. https://shawngreene1981-cmyk.github.io/the-long-walk/
> (anchor `cn10`, accessed 2026-08-27).

## Running it locally

A website, not a single file: the URL is the hand-over. No build step, no
framework, no bundler, but the shoreline data, border acts and relief tiles are
separate files fetched by the page, and browsers refuse those fetches on `file://`.
Serve the folder instead, for example:

```
python -m http.server 8000
```

then open http://localhost:8000/. Opened directly as a file, the core map still
works; the shoreline layer and the relief do not.

Leaflet 1.9.4 and the basemap tiles load from a CDN, so the map itself needs a
network connection. If Leaflet cannot load, the page says so explicitly rather
than showing an empty box.

`clipboard.writeText` requires a secure context, so on `file://` the copy
button falls back to a legacy copy; if that is refused too, it prints the URL
in the button itself rather than losing it. Over the live HTTPS URL it copies
directly.

## Licence

Map and dataset © 2026 Shawn Greene, released under
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — share and adapt
freely, including commercially, with credit and a note of any changes. See
[`license`](license).

### Licence obligations, dataset by dataset

Every dataset drawn or shipped here, and what its licence requires of this map. **One entry is a debt, not a
clearance, and it is the only one:**

| Dataset | Licence | Obligation | Commercial use |
|---|---|---|---|
| ETOPO 2022 relief, NOAA NCEI (also the Green Sahara's computed drainage) | CC0 1.0 | none (credited anyway) | yes |
| Natural Earth 10m geography regions and river centrelines (the Sahara polygon; the modern rivers the drawn channels avoid) | public domain | none (credited anyway) | yes |
| OpenStreetMap basemap tiles | ODbL, tiles © OSM contributors | attribution on the map | yes |
| De Groeve *et al.* 2022 shoreline raster | CC BY 4.0 | credit, licence link, state changes | yes |
| Cliopatria v0.2.0 (Bennett *et al.* 2025) | CC BY 4.0 | credit, licence link, state changes | yes |
| NADI-1 ice margins, Dalton *et al.* 2023 | CC BY 4.0 | credit, licence link, state changes | yes |
| DATED-1 ice margins, Hughes *et al.* 2016 | CC BY 3.0 | credit, licence link, state changes | yes |
| **PATICE — Patagonian Ice Sheet, Davies *et al.* 2020** | **CC BY-NC 3.0** | **credit, licence link, state changes** | **NO — NON-COMMERCIAL ONLY** |

**PATICE MUST BE REMOVED OR RELICENSED BEFORE ANY COMMERCIAL USE OF THIS MAP, THE SHOW OR THE GAME.**
It was taken knowingly, as a deliberate exception to the rule that has already excluded three datasets
(Esri's basemap, `historical-basemaps`, CShapes). It is the only non-commercial asset here and it should stay
the only one. It covers the Patagonian ice sheet alone; removing it means dropping that sheet or replacing it
with a differently licensed reconstruction, and nothing else on the map depends on it.
**Where it is:** `data/ice/patice.json` (built by `geowork/ice/build_ice.py` from the Mendeley deposit's
`Shapefiles/Reconstruction/Icesheet*.shp`). To remove it: delete that file and the `patice` entry in the ice
module's source list in `index.html`; Patagonia then has no ice drawn at any date until a differently licensed
reconstruction replaces it.

Basemap tiles © OpenStreetMap contributors. Relief rendered from ETOPO 2022, NOAA
NCEI (CC0 1.0). Border acts from Cliopatria v0.2.0, Bennett *et al.* 2025, CC BY 4.0,
with changes (cut into acts, simplified, invalid geometries repaired; for the drawn act, rasterised to 0.1° cells, composite records not drawn, and the growth between dated shapes computed by this map). Shoreline data © De Groeve et al. 2022, CC BY 4.0, with
changes — see *Palaeo-shorelines* above for the full credit.
