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
by 124 polygons extracted from **De Groeve et al. 2022**, the only global shoreline
reconstruction with a real glacial-isostatic correction (SELEN4 sea-level solver,
ICE-6G_C ice history, VM5a mantle). Three stops, each the reconstructed coast at the
date this map's curve first reaches that depth, walking back from the present:

| sea level | date | |
|---|---|---|
| −120 m | ~19,000 ya | Last Glacial Maximum |
| −75 m | ~12,900 ya | after meltwater pulse 1A |
| −40 m | ~9,550 ya | early Holocene drowning |

Drawn for the five researched shelves only — Beringia, Doggerland, Sunda, Sahul and
the Persian Gulf — so each coastline keeps its region's research note and dating. It
is a model, not a survey: good to roughly 10 km, with small islands missing. Every
polygon carries source, basis and confidence, and the code drops any polygon that
cannot.

**Before 26,000 years ago the map deliberately draws no shoreline at all.** That is
the reach of the best available source, not of our effort: no GIA-corrected global
shoreline product exists before 26 ka. An unsourceable coastline should be absent
rather than approximate.

The layer is **off by default** pending a ruling on switching it on.

Shoreline data: De Groeve, J., Kusumoto, B., Koene, E. *et al.* (2022). Global raster
dataset on historical coastline positions and shelf sea extents since the Last Glacial
Maximum. *Global Ecology and Biogeography* 31(11): 2162–2171.
https://doi.org/10.1111/geb.13573 — raster (AGE 2021) via Figshare,
https://doi.org/10.21942/uva.c.5754779.v1, licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Changes were made:** the
coastline-age raster was thresholded at three dates, read at about 0.1°, polygonised,
simplified at 0.08°, rounded to 2 decimal places, clipped to five regions, and
fragments under 0.35 square degrees removed.

## The GIS job — status

**1. Palaeo-shorelines — done.** See above.

**2. Border acts — cut, not yet on the map.** Cliopatria v0.2.0 (GitHub release tag,
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

**4. A self-hosted shaded-relief basemap — in progress.** The map sits on plain
OpenStreetMap: a road map with prehistoric shapes on it. Every hosted alternative was
rejected — Stamen retired and keyed, Esri's relief under a licence written for
licensees, NASA's CC0 Blue Marble painting *modern* vegetation across an Ice Age map.
So it is rendered here from **ETOPO 2022** (NOAA, CC0 1.0), which includes bathymetry.
Whether the existing palette holds against it is being settled by measurement.

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

One self-contained HTML file. No build step, no framework, no bundler — clone
the repo and open `index.html` directly in a browser.

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

Basemap tiles © OpenStreetMap contributors. Shoreline data © De Groeve et al. 2022, CC BY 4.0, with
changes — see *Palaeo-shorelines* above for the full credit.
