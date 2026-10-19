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
century does not go dark at the next; `geowork/borders/check_boundaries.py` and `check_seams.py` test both.

**Ruled 2026-10-11: the bar those two checks are held to is "no worse than the set already live", not zero.** A
boundary is a join between two independently built acts, and some disagreement is inherent: they are cut from the
same release but converge separately, and a cell can change hands in the year they share. The live set has never
scored zero — when the check was first run across it on 2026-10-09 it returned 44 boundaries, 9 of them clean,
2,041 cells absent at a start, 1,993 absent at an end and 53 date-disagreements. Demanding zero of a rebuild would
hold it to a standard the thing it replaces has never met, and would stop the map moving forever. So the question
asked of any staged set is the comparative one, boundary by boundary, and a rebuild ships when no boundary is worse
than the live set's equivalent.

**What "worse" means is a count of what a visitor could see, not of cells that differ.** The disagreements that
matter are the ones that change a line's weight: a pair of owners dated to an act's own floor when the previous act
knows they met centuries earlier is drawn at full brightness instead of at the fade floor, and because the fade's
live window is wider than a single century, it stays wrong for the whole act. The useful figure is therefore the
share of the full-brightness seam cells in an act's opening frame that are wrong — at boundary 1700 of the
first v0.2.1 rebuild that was 265 of 269, against at most 1 anywhere in the live set. Where

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

**Ruled 2026-09-29: an openly labelled convention is honest; a conflict in the record is not.** Flags are drawn
from their blazons, and a blazon fixes the arrangement and leaves the widths to the artist — that is what heraldry
is. Of the objects this map draws, **only the Dannebrog has its geometry stated by its own source**: the Danish
Forordning of 11 July 1748 gives the cross as a seventh of the hoist and the quarters as 3:1:3 by 3:1:4.5. The cross
of St George, Sweden's yellow cross and Genoa's cross are drawn at **conventional widths**, and each of those popups
says so in its own words — *"the widths drawn here are the conventional ones and are this map's, not the source's"*.

That is **not** the same as the cases this map leaves blank, and the difference is the whole rule. Portugal's
blue-and-white monarchy flag is not drawn because two decrees of **18 October 1830 give two different proportions**,
blue a third and blue a half; the 1606 Union Flag is not drawn because Perrin reports the heralds' own pattern
**lost** and the width of the white about the red **disputed**. In both, the record contains a contradiction, and
choosing between them on the map would be this map settling a question its sources leave open. Where a source is
merely silent on a width, a stated convention leaves the reader able to see what is the map's and what is the
source's. Where a source disagrees with itself, nothing is drawn.

**Cliopatria v0.2.1, released 3 October 2026 — reviewed, and the map does not draw it yet.** The release
addresses all six faults this project reported on 23 September, and the fixes were checked against the file
rather than against the release notes: the Northern Song now runs to 1138 with its SeshatID restored and the
Southern Song begins in 1139; *Dutch Cape Coast* is split into **Dutch Cape Colony** (Q4807130, the Cape) and
**Dutch Gold Coast** (Q770776, the forts), each verified by coordinate; the British Cape and Freetown records,
which were drawn on each other's ground, are now each on their own; *French Equatorial Africa* is renamed French
Algeria and carries Q218272 throughout; *Danish India* on the Gold Coast becomes **Danish Gold Coast** (Q770833);
and Portugal's overseas possessions regain their `MemberOf` while the Portuguese Republic's identifier is
corrected from Q45 to Q167360. **Two faults this project found IN v0.2.1 went back upstream and were filed on
2026-10-12 as [#22](https://github.com/Seshat-Global-History-Databank/cliopatria/issues/22)** — Freetown Colony
still carrying Q3780, the city, after its geometry was fixed — **and [#23](https://github.com/Seshat-Global-History-Databank/cliopatria/issues/23)** — Danish India
ending in 1808 when the settlements were sold in 1845, a date this project checked before suggesting it, and which
v0.2.0's own 1848 also got wrong. Both were open with no replies when last checked on 2026-10-16. The drafting
rule stands: this project writes the issue, the founder files it. **This map drew v0.2.0 until 2026-10-11 and now draws v0.2.1.** Adopting the new release was not a
file swap: 130 records straddle the 1500 act boundary and five of them — including the Habsburg Monarchy
— are removed or retimed in v0.2.1, so an act built on the new release beside an act built on the old one
would draw different shapes for the same polity on either side of the join. So adoption meant re-cutting
the slices and rebuilding all fifty acts on the new release, which ran from 6 to 9 October 2026, and
shipping them in one push rather than act by act.

**Withdrawn 2026-10-05: the “822,136 B budget ceiling”.** The scope for the colonial acts named that
figure as the per-act size limit. It is **below `act_1200_1300`, which is 899,788 bytes raw and has been live
for weeks**, so it was never a ceiling anything was held to. The measured envelope is the largest act already
shipping; the 1500–1600 act, at 840,319 bytes raw and about 345,000 gzipped, sits inside it.

**A frontier that re-lit at a century boundary, 2026-10-11.** Investigating boundary 1700 before the v0.2.1
set shipped turned up a real fault, not an artefact of the check. `postpass_pairs.py` carries "when did these two
powers first meet" from act to act by the polity's name after renames, and it was building that rename map **as it
walked the acts in order**, so an act could never see a rename that happens in a later one. Each act loads a
century either side, so act 1700–1800 sees `Bessarabia → Principality of Moldavia at 1814` and roots that
polity to *Bessarabia*, while act 1600–1700 does not and roots it to *Principality of Moldavia*. The two acts
then keyed the same pair of owners under different names, the carry missed, and the pair was dated to the next
act's floor — drawn at full brightness, which on this map means "these two have just met", for the whole of
the following century. At boundary 1700 that was **265 of the 269 full-brightness seam cells in the act's opening
frame**, on the Spain–Portugal, Spain–France, Moldavia–Poland and Moldavia–Ottoman frontiers.
Opened at 1699 and 1704 on the Moldavia frontier, the line visibly went from half strength to full and stayed
there.

**Collecting the renames up front was not enough, and the first attempt moved the fault rather than fixing it.**
A name can be the target of more than one rename: `Angevin Empire → Kingdom of England` at 1210 and
`Commonwealth of England → Kingdom of England` at 1662 are both real, so a name-to-name map keeps whichever it
read last, and the acts either side of 1400 resolved England to opposite ends of the chain — boundary 1400
gained exactly the 36 cells boundary 1500 lost. The renames are now **unioned**: every name a rename ever links is
one component and the component's representative is the carry name, so every act agrees whatever part of a chain
its own window happens to show. Across the 49 boundaries the cells that light wrongly at a join fell from **304 to
3**, and on every one of the 44 boundaries the live set also has, the rebuilt set is now identical to it or better.

**The male-line bottleneck, 2026-10-15 — and the first layer whose shape is a map of its own evidence.**
Across the mid-Holocene the number of men leaving male-line descendants collapsed while the number of women doing
so did not. The bottleneck is well supported; **the cause is not**, and the two are drawn apart: Karmin et al.
2015 report it from 456 whole Y chromosomes and date it to “the last 10 ky”, with “a reduction at
around 8–4 kya” in the Results, which is the window the layer runs on. Zeng, Aw & Feldman 2018 propose
competing patrilineal kin groups, and that paper is **a mathematical model, not new genetic data**; it addresses
“5000–7000 years ago”, a narrower window than the evidence paper it sets out to explain. The
popular “17 women for every man” figure is **not drawn on this map**: it could not be traced past a
blog summary to anything Karmin et al. actually write.

**The shading is a sampling footprint, not a territory, and it is computed rather than drawn.** It is one halo
around each of the 128 population coordinates published in the paper's own Supplemental Table S1, for the 320
samples in its nine geographically explicit regions; the parser refuses to emit anything unless it reproduces
that table exactly. There is deliberately **no outline joining the halos**, because an outline asserts that the
ground between two samples was sampled. The first build did hull them, and the hulls lied — nine
populations strung from Nigeria to Tanzania produced a shape that swallowed the Sahara, and eighteen Siberian
populations produced a wedge across the Arctic Ocean. So the whole of the Americas is three villages in
north-western Argentina, Oceania is two in highland New Guinea, and Australia is absent, its two samples having
been excluded from the paper's own geographically explicit analyses. **Where the layer is blank the finding has
not been tested there, which is not the same as the finding being false there.**

Four markers carry the same thread at human scale: Shum Laka, where an adolescent boy buried about 7,900 years
ago carried A00, the oldest known branch of the Y tree; Bronze Age Iberia, where close to 100% of Y chromosomes
were replaced against about 40% of overall ancestry; Iceland, settled by Norse men and largely Gaelic women; and
Leicester, where Richard III's mitochondrial DNA matched his sister's descendants and his Y chromosome matched
none of five male-line relatives. Every date was checked against the paper making the claim before it was
placed, and three of the dates first proposed for this layer moved as a result.

**The trigger fired on 2026-10-16, and the borrowed grammar is retired.** This entry used to say that the
bottleneck borrowed `TERRITORIES` — the only timed polygon the map had, meaning “a population held
this ground” — and that a **second** genetic event would earn the two of them a layer of their own.
Bell Beaker is the second. `t_y_bottleneck` is cut out of `TERRITORIES` entirely, 30,401 characters of it, and
the geometry now lives in `data/genetics/events.json` (built by `geowork/genetics/build_genetics.py`), which
makes `index.html` 24 KB smaller into the bargain. The bottleneck's popup no longer has to spend a paragraph
denying its own grammar.

**Every event declares what its own shape means, and the popup prints that before anything else**, because the
two shapes are opposite kinds of claim and nothing else on screen tells them apart. The bottleneck's is a
**sampling footprint** — one halo per sampled population, so the blanks are visible. The Beaker event's is
**the ground the finding is about** — the island of Great Britain, from Natural Earth, because the 90% is
Britain's gene pool. Ireland is deliberately not shaded: the abstract has the complex reaching Britain *and*
Ireland, but the figure belongs to Britain.

**The Beaker turnover, 2450–2000 BCE, WELL-SUPPORTED; its mechanism CONTESTED.** Olalde *et al.* 2018,
*Nature* 555:190–196. The abstract's “replacement of approximately 90% of Britain's gene pool within a
few hundred years”, and the body's more precise and longer-horizon **“a minimum of 90±2% local
population turnover by the Middle Bronze Age (~1500–1000 BCE)”**, with the authors' own caveat kept:
“the exact turnover rate and its geographic pattern will be refined with more ancient samples.” The
drawn window is the paper's own for the first centuries after contact; **there is no single arrival year in
the paper and the map does not invent one.** Its erratum (*Nature* 555:543) corrects one author's surname and
touches no figure — checked, because an erratum on a paper you are about to quote has to be read.

**The half that makes it worth a layer: it travelled as an idea, then as people.** Between Iberia and central
Europe the authors found “limited genetic affinity” and “exclude migration as an important
mechanism of spread between these two regions”. From central Europe onward “migration had a key
role”, carrying steppe-related ancestry into Britain. The same archaeological culture spread one way in
one place and the other way in another, which is why pots have never been a safe proxy for people.

**And the mechanism is contested because the paper names none.** Olalde *et al.* write that the results
“motivate further archaeological research” and list pathogen exposure among the things to examine.
Violence, disease and social advantage are all live and none of them is this paper's finding. The popup says
so: do not read the 90% as a massacre, read it as an unexplained replacement.

**Stonehenge is cited separately, as two dated facts side by side.** Olalde does not mention Stonehenge once.
The `a27` anchor now carries Parker Pearson *et al.* 2007, *Antiquity* 81:617–639, which dates the
**sarsen circle and trilithons to 2620–2480 BC** and the first phase to **3015–2935 cal BC**, and
which notes independently “the presence of Beaker pottery in Britain before 2500 BC”. The great
stones went up and within a few generations the people who raised them were largely replaced. **The map puts
the two dates next to each other and leaves the inference to the reader**, rather than attributing a
connection to a paper that does not make one. `yb02` points the other way: close to 100% of Iberia's Y
chromosomes and about 90% of Britain's whole gene pool, contemporary, both steppe-related, reported by the
same lead author a year apart.

**An arithmetic error of mine, caught before it shipped.** The window was first written 4,400–3,950 years
ago. This map counts years-ago from 2026, so 2450 BCE is **4,476** and 2000 BCE is **4,026** — out by 76
years. Corrected, and the build now prints the BCE conversion beside the years-ago figure so the next one is
caught by reading the output rather than by noticing.

**A note-rendering fault, found by building on top of it and fixed map-wide the same day.** Notes on this map
have been written with blank lines between paragraphs since the first anchors, and **not one of them ever
drew**: the text ran together into a single block. 208 objects were affected, 189 of them anchors. The fault was
invisible in the data, which looked correct, and only ever showed on screen. It is fixed at the single
chokepoint every popup and tooltip already passes through — the patched `L.DivOverlay.prototype.setContent`
— so no call site can miss it, and single newlines are left alone because the popup templates themselves
wrap across lines. Two existing notes were photographed before and after, and two unaffected popups came back
byte-for-byte identical.

**Neighbouring powers you could not tell apart, 2026-10-17 — and the fix was already written.**
The map has had adjacency-aware colouring since the ancient acts: `geowork/borders/palette_assign.py` runs
DSATUR over the polity graph with a hard rule (records overlapping in time and within 0.1° never share a
colour) and a soft one at 1°. **It was only ever run on the acts before 1500.** One line —
`if a['from'] >= 1500: continue` — and everything after it fell through to `PALETTE[0]`, so **607 of the
743 polities appearing from 1500 onward were drawn in the same olive.** Measured by the source's own
adjacency rule: **0% of bordering pairs shared a colour at 1500, 60% at 1750, 88% at 1850, 94% at 1950.** At
1850 France, Austria, Russia, Prussia and Britain were one green separated only by frontier lines.

**Eight colours were tried first, and eight does not fit.** The hard-adjacency graph contains an **8-clique**
— Rome, Parthia, the Seleucids, the Ptolemies, Pontus, Cappadocia, Armenia and the Greek city-states all
bordering one another at once — so eight is the floor. Four methods failed to reach it: DSATUR, a
depth-1 Kempe swap, real Kempe-chain interchange, and tabu search keeping its best state, all stalling at the
same two pairs. **Nine fits, but only by recolouring 557 pre-1500 polities.** Founder-ruled: take **ten**,
because screenshots and show footage of the ancient map already exist and stability of what is published
beats one fewer colour. **Ten fits with zero conflicts and moves 23 of the 929 pre-1500 polities.** Soft
(1°) same-colour pairs fell from 244 to 72. After: **0% at 1500, 1750, 1850 and 1950.**

**And the palette had never been checked for colour vision deficiency.** It was comfortable for normal
vision — worst pair 23.3 ΔE composited at the map's own 0.6 fill opacity, nothing under 12 — and
it failed badly otherwise: the olive and the orange were **4.8 ΔE apart under deuteranopia**, one colour
to roughly one man in twelve, and the tan against the green was 5.4 under protanopia. Retuned the same
surgical way as the September “reads as water” fix: **five of the eight shipped colours are
untouched**, three are retuned and two are new.

| | before | after |
|---|---|---|
| normal vision, worst pair | 23.3 | 18.1 |
| deuteranopia, worst pair | **4.8** | **14.2** |
| protanopia, worst pair | **5.4** | **13.8** |
| pairs under ΔE 12, any vision | 6 | **0** |

Two things the optimiser had to be stopped from doing. Left free it went to the corners of the gamut and
returned electric yellow and bright cyan — maximal separation, nothing like this map — so the reward
is **capped** once every vision clears 18 and the search is held inside a sepia style band. And it picked
straight back the **water-blues** the September fix removed for reading as sea, so that hue band is excluded
outright. **No act was rebuilt**: the table is applied as each act loads, through the same hook that already
swapped two slots.

**The Southeastern nations, and a Louisiana with no outline, 2026-10-19.**
Two things went on together, and one of them is mostly an argument about what may be drawn.

**LOUISIANA IS FOUR DATED MOMENTS AND NO SHAPE, because the shape does not exist.** The plan was a
hatched “claimed, not controlled” outline over the National Atlas territorial-acquisitions
layer. That layer is gone: `nationalatlas.gov` no longer resolves, the USGS `dds.cr.usgs.gov` and
`prd-tnm` endpoints return 404, ScienceBase returns no such item, and the Wayback Machine holds no
snapshot of the file. Cliopatria is not a substitute — its *French Louisiana* is a narrow
corridor along the Mississippi of about three square degrees, because it maps where France was
rather than what France claimed. So the sequence is drawn as **1682, 1762, 1800, 1803** and nothing
else, and **the absence is the history rather than a hole in the research**: not one of those four
transfers had an agreed boundary, and two of them were secret. The only mapped extent ever
published for this ground is the United States’ own 1803 Purchase boundary, drawn afterwards;
putting it around La Salle’s 1682 ceremony would have given the reader a line none of the
signatories had.

**A DEFECT IN THE BORDER DATA, STATED AND NOT CORRECTED.** Cliopatria v0.2.1 keeps a French strip
along the Mississippi from **1763 to 1779**, sixteen years after France left the continental
interior, and carries *New France* on as a vanishing sliver to **1791**. The handoff recorded this
as a 1779 end-date typo; measured against the shipped data it is not that — the 1763 collapse
is already modelled (area 19.4 in 1757–61, 5.6 in 1762, 3.0 in 1763–79), and what is wrong
is the sixteen-year tail. Ruled 2026-10-18: **draft the issue, say so on the map, touch nothing.**
An issue is drafted for the maintainers to file; no act is rebuilt and no upstream record is edited
to make this map’s picture tidier.

**THE NATIONS LAYER: CESSION, REMOVAL, AND WHAT IS STILL THERE.** The Southeastern five
— Cherokee, Chickasaw, Choctaw, Muscogee (Creek), Seminole — in three parts and one toggle.
**Seventy-six of Charles C. Royce’s numbered cessions**, each appearing in the year the treaty,
statute or executive order took the ground and each staying, because the ground stayed taken; every
popup names the instrument and links to Royce’s own Schedule entry and the treaty text.
**Five of the seventy-six are named and not drawn** — Royce 65, 128, 129, 130 and 543 —
because the Forest Service records them as having no shape in the dataset, and a gap is drawn as a
gap. The **1838–39 Cherokee removal** is in the forced-route grammar as ruled: black, dotted, no
arrowhead, and it never fades. **The Roundup and Disbandment routes are drawn thinner and labelled
as what they are** — the roads to the stockades, and where the detachments broke up on arrival
— because neither is a removal route and the source names them separately.

**The present-day lands appear in the timeline’s final act, and nowhere before it.** They are
labelled **present-day (Census TIGER 2025)** in the tooltip, the popup and the legend, and drawn as
a **thin dashed outline and never a fill** so they cannot read as territory. The first version drew
them at every date, on the argument that they were a reference to now like the basemap underneath;
the argument was available, but it made this one layer exempt from the rule the whole map runs on
— that nothing exists until the scrubber reaches its date. **Founder-ruled 2026-10-19: the final
act only.** Ruling 7 is honoured by their arriving at all: scrub to the end and the ground the
cessions took is still taken, and these nations are still there. These are 2025 boundaries and this
timeline stops in 1999; the twenty-six-year gap is stated rather than hidden.
Each shape also carries **the Census Bureau’s own word for what it is**, because a reservation
and an Oklahoma tribal statistical area are not the same kind of thing and one shape must not imply
the other.

**Three measurements that changed the build rather than decorating it.**
**One.** Matching tribe names by substring inflated the cession count from 36 to 112: “Creek”
catches Crow Creek Sioux, Cow Creek Umpqua, Berry Creek Rancheria, Dry Creek Pomo, Grave Creek, Hog
Creek Shawnee and the Swan Creek and Black River Chippewa. It is the same fault as matching a route
by proximity instead of by id and it got the same answer: **the names are named**, the real figure is
**76**, and the builder aborts on any name its allow-list has not ruled on. The Eastern Band was
missed entirely by the same kind of error in the other direction — its land is filed as
**Qualla Boundary**, which contains no string a Cherokee-keyed search would find.
**Two.** **One colour per nation does not fit.** Fourteen hill-climbs from fourteen random starts all
stopped at a worst pair of **10.1 ΔE** against the border palette under protanopia, against the
bar of 12 that the palette ruling set. Six colour families do not fit this gamut with the water-blues
excluded. The five barely overlap on the ground, so **geography separates them and the tooltip names
them**; the layer uses two colours, ceded and today, worst pair **13.8**.
**Three.** A first pass labelled two off-reservation trust lands as **Hawaiian home land**, from a
hand-written class table. The source already knew — its own `NAMELSAD` field spells out what each
area is — and had not been asked. The table is gone; the labels are the Census Bureau’s words.

**The licence question that gated all of this, answered by opening the records.** Works of the US
federal government are not subject to copyright (17 U.S.C. §105), and an agency attribution line
names the author rather than imposing a restriction. **Trail of Tears** (NPS DataStore **2238914**):
the FGDC originator is “National Park Service, National Trails Intermountain Region, GIS”,
additional use constraints are blank, access is Open/Public, and **every one of the 2,006 features
carries ORIGINATOR = National Park Service**. The Trail of Tears Association appears on 74 segments
in the `MAPSOURCE` field, as material the Park Service digitised from — a credit, not an
authorship, and credited here as one. The source does set a real bound that is **not** a licence term:
*“This data set should not be displayed or used at scales that exceed 1:100,000”*, which the
map honours and states in the popup. **Royce cessions** (USFS `S_USA.TRIBALCEDEDLANDS`, 2018): access
constraints “None”, and the 2018 revision was a collaboration of the USFS Office of Tribal
Relations, the NPS National NAGPRA Program, the EPA American Indian Environmental Office and
Dr. Claudio Saunt of the University of Georgia — who, the lineage says, **digitised the Royce maps
independently of the Forest Service**. The polygons drawn here are the Forest Service’s own; the
collaboration is credited. **Native Land Digital is not used**, as ruled.

**Ruled 2026-10-06: nothing built is deleted, even when it can be rebuilt.** Outputs go to
`G:\My Drive\The Reset\_Archive` as `ARCHIVE_YYYY-MM-DD_description`. "It is reproducible" is not a reason to
throw something away: reproducing it costs hours, and the thing being compared against is gone while you do.

**This rule exists because it was broken on 2026-10-06.** The 1500–1600 act had been built twice on
Cliopatria v0.2.0 — once with the whole-field convergence criterion, at 840,319 bytes, and once with a
faster target-only criterion, at 840,341 — to test whether the two agreed. They did not, so the act was
held; and when the v0.2.1 review then showed its source window had changed, **both builds were deleted from the
working tree** on the reasoning that an act nobody would ship was clutter. That was wrong twice over: the
whole-field build was the reference the convergence question would be re-argued from, and the pair together
were the only existing measurement of what that criterion is worth. They survived only because copies had been
made earlier for the byte comparison, and they are now in `_Archive` as
`ARCHIVE_2026-10-06_act_1500_1600_v020_wholefield.bin` and `..._targetonly.bin`. The next one might not survive.

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
| Cliopatria v0.2.1, 3 October 2026 (Bennett *et al.* 2025) — **the version this map draws**, since 2026-10-11 | CC BY 4.0 | credit, licence link, state changes | yes |
| Cliopatria v0.2.0 — drawn until 2026-10-11, superseded | CC BY 4.0 | same | yes |
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
