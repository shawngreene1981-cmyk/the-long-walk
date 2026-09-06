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

## Palaeo-shorelines: built, and switched off

Half the routes here only make sense at low sea level — Beringia was a country,
Doggerland an inhabited landscape, Sundaland continuous land. The layer that
draws those coastlines is complete: shorelines are selected by **depth** rather
than by date, read from the map's own 18-point sea-level curve, so they can
never drift out of step with the sea-level readout. Three drawn stops
(−40 m, −75 m, −120 m) plus modern, which correctly draws nothing.

**It ships disabled, on purpose.** Every polygon carries a source, a basis and a
confidence statement, and the code drops any polygon that cannot — but the
shapes themselves are hand-drawn approximations rather than geometry extracted
from the reconstructions they cite. On a map whose whole argument is that it
never overstates, a coastline that looks surveyed and is not would be the first
thing here to break that. The layer stays off until real sourced geometry
replaces the placeholders; the system is data-driven, so that is a data swap
and not a code change.

When it is on: **solid edge** = published reconstruction, **dashed edge** =
bathymetric approximation, a modern depth contour standing in for a
palaeo-shoreline with no correction for isostatic rebound, sediment or
tectonics — and rebound error is largest at high latitude, which is exactly
Doggerland and Beringia. Before 130,000 years ago the map has no sea-level
curve and deliberately draws no shoreline at all.

## The outstanding GIS job — three targets, one afternoon

Three things on this map are placeholder geometry, and they want the same
tooling, the same sources and the same session. They are listed together because
doing them separately would mean georeferencing the same elevation data three
times.

**1. Palaeo-shorelines.** 16 polygons, hand-drawn, currently disabled.
Sunda and Sahul from Voris 2000 (raster plates — georeference and trace);
Beringia from Manley 2002's bathymetric DEM (`gdal_contour`, no tracing);
Doggerland and the Persian Gulf from GEBCO (`gdal_contour`). Note that
ICE-6G_C's isostatically corrected paleotopography is 1×1°, too coarse for
Doggerland or the Gulf — so those two stay `bathymetric` even done properly.
That is the honest permanent answer for them, not a placeholder.

**2. Ice sheets.** Worse than the coastlines: **26 coordinate pairs across all
four sheets** — Laurentide 8 points, Cordilleran 6, Fennoscandian 6, Patagonian
6. The largest ice sheet in the Northern Hemisphere is an octagon. This is the
*easier* half of the job, because the sources ship as vectors: **Dyke 2004**
(GSC Open File 1574) deglaciation isochrones for the Laurentide and Cordilleran,
**DATED-1** (Hughes et al. 2016) for the Fennoscandian, Davies et al. 2020 for
the Patagonian. No tracing, no contouring — reproject, filter to the LGM
isochrone, simplify, convert. DATED-1 publishes explicit maximum, minimum and
best-estimate margins, which map straight onto the `basis` field the coastlines
already use: the ice could carry a genuine `reconstruction` tier with a real
uncertainty band rather than a dashed approximation.

**3. A self-hosted shaded-relief basemap.** The map currently sits on plain
OpenStreetMap — a road map with prehistoric shapes on it, no topography, and
labels and borders competing with the content. Every hosted alternative was
rejected: Stamen is retired and now needs a key, Esri's shaded relief is a
legacy endpoint under a licence written for licensees rather than a public
grant, and NASA's CC0 Blue Marble is natural-colour imagery that would paint
*modern* vegetation across an Ice Age map and contradict this map's own Green
Sahara mechanic. So render our own, from public-domain elevation data already in
the source list above — GEBCO, SRTM, GTOPO30. Self-hosted: no licence question,
no watermark risk, and it can be tuned to whatever mid-tone the palette actually
needs instead of whatever a vendor chose.

That last point is not cosmetic. Overlay contrast was measured against a
relief-toned ground and three tier colours — contested, hoax and demographic —
lose roughly a third of their contrast on any mid-tone basemap. Those colours
are semantic and are deliberately **not** being changed to chase a basemap that
does not exist yet; they get retuned once there is a real one to tune against,
which makes the palette pass part of this same job.

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

Basemap tiles © OpenStreetMap contributors, © CARTO.
