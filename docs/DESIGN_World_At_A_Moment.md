# DESIGN — THE WORLD AT A MOMENT

**Status: DESIGN ONLY. Nothing is built.** Branch `world-at-a-moment`, cut from `main`
at `b489adc`. The live site is untouched.

Founder's verdict, verbatim:

> *"if I wanted to look at the crucifixion of jesus christ between 0-32ad, I want to see
> whats happening in these other cultures around the world. I want to do the same as i
> have done with gobekli tepe seeing how far humans had spread by the younger dryas
> event. map shows that. This is where the education takes place. Also map says 2000
> years ago. good also needs an actual date"*

The lanes answer *when*. This answers **what else, where, at the same time** — and it
answers it on the map, which is where the reader already is.

---

## 1. A REAL DATE IN THE HEADER

The header reads **`~2,000 YEARS AGO`** and nothing else. It would read:

> **~2,000 YEARS AGO · c. 30 CE**     *the scrubber steps about 5 years here*

Three things decide the form, and all three are measured rather than assumed.

**a. The axis cannot address a single year, and the readout must not pretend it can.**
One step of the scrubber is **4.6 years at 30 CE, 6.4 at the Younger Dryas, 2.5 at the
Bronze Age collapse and 11.1 at Long Count zero** — measured off
`yearsAgoFromSlider` at each position. So the date is `c.` wherever a step is wider
than a year, which is everywhere before about 1700 CE. **The axis itself is not touched:
that needs its own ruling, and this design does not ask for one.**

**b. No year zero.** 1 BCE is followed by 1 CE. The conversion is the one
`build_lanes.py` already uses, and the readout must never print "0 CE".

**c. The small print earns its place.** "The scrubber steps about 5 years here" is what
makes `c.` honest instead of coy: it says *why* the date is approximate, and it changes
as you scrub.

## 2. GO TO A DATE

A box that accepts what a reader would type: **`30 CE`**, **`9600 BCE`**,
**`2000 years ago`**, **`30AD`**, **`-9600`**. It resolves to a year, then moves the
scrubber to the nearest step it can reach — and **if that lands more than a step away it
says so** rather than silently showing a different year.

### The featured moments — the proposed final list

Five are the founder's. **The sixth is a recommendation, and the gap table is why.**

| # | moment | date | tier | why it is on the list |
|---|---|---|---|---|
| 1 | The crucifixion | c. 30–33 CE | **contested** | The founder's own example. An execution almost every scholar accepts happened, on a year nobody can fix: 30 and 33 CE both fit Pilate's prefecture and the gospels' calendar notes. The tier is about the *date*, not the event. |
| 2 | The Younger Dryas begins | c. 10,900 BCE | solid | Göbekli Tepe's world, dated in the Greenland ice cores. The frame that shows how far people had already spread. |
| 3 | The Great Pyramid | c. 2560 BCE | solid | The one date most readers already own. |
| 4 | The Bronze Age collapse | c. 1177 BCE | contested | A date made famous by one book; the collapse is a process, and the panel should say so. |
| 5 | Long Count zero / the Kali Yuga | 3114 / 3102 BCE | tradition | Ties straight to story mode's step 4. |
| **6** | **The Lapita reach the open Pacific** | **c. 1000 BCE** | solid | **Recommended addition.** At all five of the moments above, **Oceania and Southeast Asia are empty** — see §5. This is the moment where Oceania is not a blank row but the lead: Bismarck Archipelago 1500 BCE, Mwanihuki 1401, Tonga/Samoa 1000, Teouma 950, Nukuleka 888. Without it the feature teaches, five times over, that nothing happened in the Pacific. |

## 3. "MEANWHILE, AROUND THE WORLD"

One entry per region, **all nine, in the map's own region order**, for the chosen moment.

Each filled entry carries: **what was happening**, its **date**, its **tier** as a chip,
its **site line**, and a **fly there** control that moves the map to it. Each empty
entry says, in the words the Persia lane already uses:

> *no source checked for this window* — An empty row means this project has not looked,
> not that nothing was happening.

**The window is part of the claim and is printed.** At 30 CE the panel uses ±150 years
and says so; the Younger Dryas uses ±1,000, because a climate onset dated in ice cores
and a scatter of radiocarbon sites are not the same kind of date. A footer states the
count: *"7 of 9 regions have a dated anchor inside ±150 years of this moment. The rest
say so."*

**Why a window at all, rather than the year itself:** at ±25 years around 30 CE the map
holds **4 anchors across 3 regions**. At ±50, six across five. At ±150, twenty-two
across seven. A feature that shows four rows and six blanks would teach the opposite of
what it is for — and the answer is both to widen the window honestly and to source more,
not to hide the blanks.

## 4. THE MAP AT THAT MOMENT

Unchanged from what the map already does, with one addition: the entries in the panel
are **pinned**, and clicking one flies there. Active sites lit, the rest dimmed,
Cliopatria borders as now. The mockups' map pane is a **photograph of the live map**
scrubbed to each date, not a drawing, because the question is what the map already shows.

## 5. THE SOURCING PLAN, AND THE GAP TABLE

### What the map holds now, per region per moment

Counted with the page's own `regionOf()` — file order, first matching box — against all
565 anchors.

| region | 30 CE ±150 | YD ±1000 | Pyramid ±150 | Collapse ±125 | LC zero ±150 |
|---|---|---|---|---|---|
| Oceania | **0** | **0** | **0** | **0** | **0** |
| the Americas | 3 | 7 | 1 | 1 | 1 |
| Europe | 5 | 2 | 3 | 2 | 3 |
| Africa south of the Sahara | 2 | 1 | **0** | **0** | 2 |
| North Africa and the Near East | 3 | 1 | 3 | 9 | 2 |
| Inner Asia | 1 | 1 | 1 | 2 | 1 |
| Southeast Asia | **0** | **0** | **0** | **0** | **0** |
| South Asia | 4 | **0** | 5 | 1 | **0** |
| East Asia | 4 | **0** | **0** | 2 | 1 |
| **filled** | **7/9** | **5/9** | **5/9** | **6/9** | **6/9** |

**The structural gap is Oceania and Southeast Asia: empty at every one of the five.**
Not because the Pacific was empty — because this map's sourcing passes have not gone
there for these windows. Oceania's 24 anchors cluster at 1500–888 BCE and after 900 CE;
Southeast Asia's 33 jump from 23,974 BCE to 3,674 BCE and again from 1,774 BCE to
500 BCE.

### The plan, on RESEARCH Part B's rules

Same rules as Part B: real sources, stated chronology conventions, a tier on every
claim, **nothing typed without a source**, and *contested* recorded as a result rather
than a failure. One pass per moment, each producing a row per region.

**Priority 1 — the two structural blanks, at 30 CE** (the founder's own example):

- **Southeast Asia** — Óc Eo and the Funan ports, the Dong Son bronze horizon, Sa Huỳnh
  jar burials. All have excavation literature and radiocarbon.
- **Oceania** — the end of the Lapita sequence and the long pause before East Polynesia;
  the honest answer here may be *"the settled record resumes c. 900 CE"*, which is a
  finding, not a blank.

**Priority 2 — the holes in the other four moments:** Africa south of the Sahara at the
Pyramid and the Collapse; South Asia and East Asia at the Younger Dryas; East Asia at
the Pyramid (Liangzhu and Longshan are both well dated and are an obvious miss).

**Priority 3 — the moments themselves.** Each featured moment needs its own sourced
entry with a tier, especially the crucifixion, where the honest statement is *the event
is accepted, the year is argued*, and the panel should name the two candidates and what
each rests on.

**And one dependency, found while measuring this.** The region boxes in
`data/borders/coverage.json` are **ordered and overlapping**, and the page returns the
first box that contains a point. Karahan Tepe (37.09 N, 39.30 E) therefore files under
*North Africa and the Near East*, not Europe; Luoyang files under East Asia only because
Inner Asia's first box stops at 98° E. The assignment is defensible but it is **an
artifact of box order**, and a feature that promises "one entry per region" inherits it.
This is worth an eyes-on pass before the sourcing starts, and it is already half-known:
`OPEN_ITEMS` records that the same file lists Europe twice and Inner Asia twice.

## 6. HOW THIS SITS WITH STORY MODE AND EXPLORE

**One page, three doors, and the story still leads.**

| | what it answers | how you get there |
|---|---|---|
| **Story mode** | *How did six civilisations count back, and how short is recorded memory?* | leads the page, as now |
| **The world at a moment** | *What else was happening, and where?* | the header date box and the featured moments — reachable from any step, and from the map |
| **Explore** | *Show me everything and let me read it* | the handoff at step 6, as now |

The moment panel is **the third door and not a fourth page**: it opens beside the map,
in the page the reader is already on, and closes back to it. Story mode's step 4 and
step 5 each name a moment — the ~3100 cluster and the two floods — and both should
offer *"see the world at this moment"*, which is the point where the sequence hands the
reader the controls.

**Explore does not change.** It is the instrument; this is a reading of it at one date.

## 7. WHAT I AM NOT DOING YET

No code on the page. The frames are **mockups rendered from a standalone prototype in
`geowork/moment/`**, with the map pane photographed from the live page. Nothing in
`index.html`, `data/` or `img/` is touched on this branch. No sourcing has been done yet
— §5 is the plan and the measured gaps, which is what was asked for before code.
