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

## Palaeo-shorelines: sourced, and off by default

Half the routes here only make sense at low sea level — Beringia was a country,
Doggerland an inhabited landscape, Sundaland continuous land. The layer that
draws those coastlines selects shorelines by **depth** rather than by date, read
from the map's own 18-point sea-level curve, so they can never drift out of step
with the sea-level readout.

**The geometry is now sourced.** The 16 hand-drawn placeholders have been replaced
by 3,305 polygons extracted at full resolution from **De Groeve et al. 2022**, the only global shoreline
reconstruction with a real glacial-isostatic correction (SELEN4 sea-level solver,
ICE-6G_C ice history, VM5a mantle). Three stops, each the reconstructed coast at the
date this map's curve first reaches that depth, walking back from the present:

| sea level | date | |
|---|---|---|
| −120 m | ~19,000 ya | Last Glacial Maximum |
| −75 m | ~12,900 ya | after meltwater pulse 1A |
| −40 m | ~9,550 ya | early Holocene drowning |

Drawn for the five researched shelves only — Beringia, Doggerland, Sunda, Sahul and
the Persian Gulf — so each coastline keeps its region's research note and dating. Each
region shows only the shelf inside its own box; where the box cuts the shelf the land
stops in a straight line, which is the limit of the regional extraction and not a coast,
and no coastline is drawn along it.

**The shelf is drawn as land**, opaque, in the land colour of whichever basemap is
active, under every route and marker, so at the glacial maximum the continents are
simply bigger and the modern coastline is hidden beneath them. The stops are nested:
each is solid while the sea is below it, and as the sea rises through an interval only
that outer ring fades — the sea taking it back. With `?sea=blue` the water on either
basemap is toned to a clear blue (only water pixels move), so there is something for
the sea to take; that stays behind its parameter until it has been looked at. It is a model, not a survey, and **how
much of each region's shelf survives simplification is measured and stated, region by
region and stop by stop**, in every shoreline popup and here:

| kept | −120 m | −75 m | −40 m |
|---|---|---|---|
| Beringia | 99.7% | 99.3% | 94.6% |
| Doggerland | 99.5% | 98.6% | 92.2% |
| Sunda | 99.5% | 97.0% | 73.3% |
| Sahul | 98.4% | 95.5% | 77.5% |
| Persian Gulf | 99.9% | 99.2% | 91.5% |

97.9% overall. The loss concentrates at −40 m, where the shelf is fragmented into
small islands. Every polygon carries source, basis and confidence, and the code drops
any polygon that cannot. The geometry lives in `data/coasts.json` and is fetched only
when the layer is switched on.

**Before 26,000 years ago the shorelines are an APPROXIMATION, not a reconstruction,
and the map says so in words.** 26 ka is the reach of the best available source: no
GIA-corrected global shoreline product exists before it. Below it the map draws the same
De Groeve shapes, selected by its own sea-level curve rather than reconstructed for that
date, with **no glacial-isostatic correction** — so they are most wrong at high latitude,
which here means Beringia. The popup, the legend and the HUD all name it an
approximation; its coastline is dashed where the reconstruction's is solid; the switch at
26,000 years ago is instant, and a mark on the timeline shows where it falls. The curve
is coarse there: four points between 26,500 and 130,000 years ago, with straight lines
across 50,000 and 40,000 years. Each shelf is still drawn only within its researched
window, so the approximation reaches back to 36 ka (Beringia), 65 ka (Sahul), 70 ka
(Persian Gulf) and 90 ka (Sunda); Doggerland, held by ice, is never approximated.

The HUD reports a shelf as walkable only while the layer is on and drawn. If the
shoreline data fails to load, the map says so beside the switch and in the HUD, and
ticking the switch again retries.

The layer is **off by default** until the full-resolution extraction has been looked at.

Shoreline data: De Groeve, J., Kusumoto, B., Koene, E. *et al.* (2022). Global raster
dataset on historical coastline positions and shelf sea extents since the Last Glacial
Maximum. *Global Ecology and Biogeography* 31(11): 2162–2171.
https://doi.org/10.1111/geb.13573 — raster (AGE 2021) via Figshare,
https://doi.org/10.21942/uva.c.5754779.v1, licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Changes were made:** the
coastline-age raster was thresholded at three dates at full resolution (2 arc-minutes)
within five regional boxes, polygonised, simplified at 0.05°, rounded to 2 decimal
places, and pieces under 0.003 square degrees removed.

## The GIS job — status

**1. Palaeo-shorelines — re-extracted at full resolution, layer off until looked at.** See above.

**2. Border acts — cut, shipped as data, preloaded, not yet drawn.** The 56 acts are in
`data/acts/` with a manifest. The borders layer's visual grammar is still unruled, so
nothing is rendered; `?borders=preload` fetches and parses every act in the background,
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

**4. A self-hosted shaded-relief basemap — built, behind `?relief=1` until looked at.** The map sits on plain
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

Basemap tiles © OpenStreetMap contributors. Relief rendered from ETOPO 2022, NOAA
NCEI (CC0 1.0). Border acts from Cliopatria v0.2.0, Bennett *et al.* 2025, CC BY 4.0,
with changes (cut into acts, simplified, invalid geometries repaired). Shoreline data © De Groeve et al. 2022, CC BY 4.0, with
changes — see *Palaeo-shorelines* above for the full credit.
