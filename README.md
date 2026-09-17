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

**2. Border acts — cut, shipped as data, preloaded; ONE act drawn, behind `?borders=1`, waiting to be looked at.**
The first act, 1000–1100 CE, is built into `data/borders/` as a timed grid of 0.1° cells
(`act_1000_1100.bin` with its `.json` header; built by `geowork/borders/build_act.py`) and drawn
only when the page is opened with `?borders=1`. In that mode, and only in it, the evidence
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

**3. Ice sheets — blocked, and staying blocked.** The four sheets are **26 coordinate
pairs** between them — bounding boxes, and the legend says so. The identified
replacement, Batchelor *et al.* 2019, carries **no licence on the deposit itself**,
only on the paper describing it. This project does not ship data whose rights cannot
be traced to the artefact, so the boxes stay, labelled as boxes, until that is
resolved rather than assumed.

**4. A self-hosted shaded-relief basemap — the default.** Looked at on the live map and on a
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
| ETOPO 2022 relief, NOAA NCEI | CC0 1.0 | none (credited anyway) | yes |
| OpenStreetMap basemap tiles | ODbL, tiles © OSM contributors | attribution on the map | yes |
| De Groeve *et al.* 2022 shoreline raster | CC BY 4.0 | credit, licence link, state changes | yes |
| Cliopatria v0.2.0 (Bennett *et al.* 2025) | CC BY 4.0 | credit, licence link, state changes | yes |
| **PATICE — Patagonian Ice Sheet, Davies *et al.* 2020** | **CC BY-NC 3.0** | **credit, licence link, state changes** | **NO — NON-COMMERCIAL ONLY** |

**PATICE MUST BE REMOVED OR RELICENSED BEFORE ANY COMMERCIAL USE OF THIS MAP, THE SHOW OR THE GAME.**
It was taken knowingly, as a deliberate exception to the rule that has already excluded three datasets
(Esri's basemap, `historical-basemaps`, CShapes). It is the only non-commercial asset here and it should stay
the only one. It covers the Patagonian ice sheet alone; removing it means dropping that sheet or replacing it
with a differently licensed reconstruction, and nothing else on the map depends on it.
**Not yet in the map:** the ice-margin rebuild that uses it is queued behind the stop rule, and this row will
name the files it arrives in when it does.

Basemap tiles © OpenStreetMap contributors. Relief rendered from ETOPO 2022, NOAA
NCEI (CC0 1.0). Border acts from Cliopatria v0.2.0, Bennett *et al.* 2025, CC BY 4.0,
with changes (cut into acts, simplified, invalid geometries repaired; for the drawn act, rasterised to 0.1° cells, composite records not drawn, and the growth between dated shapes computed by this map). Shoreline data © De Groeve et al. 2022, CC BY 4.0, with
changes — see *Palaeo-shorelines* above for the full credit.
