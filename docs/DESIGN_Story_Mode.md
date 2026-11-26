# DESIGN — STORY MODE, and the panel as EXPLORE

**Status: DESIGN ONLY. Nothing is built, nothing is on the live page.** Branch
`lanes-story`, cut from `main` at `a06f755`. The live site stays as it is until this is
approved and built.

Founder's verdict on the published panel, 2026-11-26: *"there has to be a better way to
story tell this."* He is right, and the four faults named with it are all the same fault
wearing different clothes — **the instrument is arranged by data structure, not by
argument.** Nine lanes of unlabelled ticks come first because they are the ground;
"width is not duration" gets a paragraph because it is a caveat about the axis; the
period images sit behind the bands because that is where a background goes. Every one of
those is a correct decision about a chart and a wrong decision about a story.

So: **a guided sequence leads, and the chart becomes the place you go afterwards.**

---

## 0. THE ONE THING I COULD NOT READ

The ruling points at `episodes/Episode_Six_Clocks.md`, **updated today**. There is no
`episodes/` directory in this repo, nothing by that name in Drive's `The Reset/episodes/`,
and `_incoming/` holds only the 2026-11-25 copy. The repo's own
`docs/Episode_Six_Clocks.md` says its full version lives *"in the claude.ai project at
episodes/Episode_Six_Clocks.md"* — which is the coordinator's side, not mine.

**So this design is built from the outline I can see**, whose six panel beats match the
six steps of the ruling almost exactly. If today's update changed the beats, send the
file and I will re-cut the sequence against it. Nothing below depends on prose I have not
read; the beats, the dates and the landmarks all come from the repo's own data.

---

## 1. THE SEQUENCE

Six steps. One screen each. Every step is a **single figure with a headline and at most
three lines of copy** — if a step needs a paragraph to work, the figure is wrong.

### Step 1 — TRUE SCALE

**One line, 70,000 BCE to today, drawn to real proportion.** No age-weighting, no
"width is not duration" caveat, because on this screen width *is* duration. That is the
whole point of putting it first: **the caveat the panel needs is a sentence we can skip
entirely if we show the honest line once, at the start.**

Measured, at 1400 px with a 1300 px plot — 72,026 years, **55 years to the pixel**:

| | |
|---|---|
| Ussher's Creation, 4004 BCE | 109 px from the right — **the last 8.4%** |
| the Long Count, 3114 BCE | 93 px — the last 7.1% |
| Egypt's Dynasty 1, 3111 BCE | 93 px |
| the Kali Yuga, 3102 BCE | 93 px |
| the Sumerian Flood, c. 2900 BCE | 89 px |
| the Yellow Emperor, 2698 BCE | 85 px |

**All six clocks fall inside the last 8.4% of the line; five of the six inside the last
7.1%.** Göbekli Tepe sits at 9600 BCE, 210 px from the right — **101 px to the left of
the oldest clock, with nothing of any reckoning between.**

Copy:

> **SEVENTY-TWO THOUSAND YEARS, TO SCALE**
> Every clock in this episode starts inside the last twelfth of this line.
> Göbekli Tepe is the dot five thousand years to their left, and no reckoning on earth
> reaches it.

### Step 2 — THE ZOOM

The window closes to **4000–2500 BCE**: 1,500 years, 1.15 years to the pixel. The same
line, the same colours, the camera moving — **the transition has to be a visible zoom,
not a cut**, or the viewer loses the thread between step 1 and everything after.

Copy:

> **FIFTEEN HUNDRED YEARS, THE SAME LINE**
> This is the sliver the clocks were crowded into. It is wide enough now to hold a
> world.

### Step 3 — THE SIX CLOCKS LIGHT

One at a time, oldest first, each arriving with **a card**: the artifact, its credit, who
set this clock and from what. The image is the size of a playing card at the head of the
step, not wallpaper behind a band.

| order | clock | epoch | card |
|---|---|---|---|
| 1 | Biblical — Ussher | 4004 BCE | Adams' *Synchronological Chart*, 1878 third edition |
| 2 | Maya — Long Count | 3114 BCE | Quiriguá Stela C |
| 3 | Egyptian — king lists | 3111–3045 BCE | the Abydos king list |
| 4 | Hindu — yuga cycle | 3102 BCE | **no card, as ruled** |
| 5 | Sumerian — King List | c. 3000–2900 BCE | the Weld-Blundell Prism |
| 6 | Chinese — traditional | 2698 BCE | an oracle bone, BL Or. 7694/1535v |

**The Hindu blank is a card too, and it says why.** "No yuga-cycle image clears on terms
we accept" is the most honest thing on the screen, and hiding it would be the one
dishonest frame in the sequence.

Copy:

> **SIX CLOCKS, SIX ARTIFACTS**
> Each of these is a thing you can hold, or stand in front of. The date is a claim; the
> object is the evidence that the claim was made.

### Step 4 — THE CLUSTER

The Long Count's zero and the Kali Yuga's epoch are **twelve years apart**, and Egypt's
Dynasty 1 is radiocarbon-dated 3111–3045 in the same window. Three independent clocks,
fixed centuries later by different methods, landing on the same stretch of line.

The step must carry the panel's existing warning (`al02`) on screen, not in a tooltip:
**read as a shared event this is a coincidence of three computed starting points, and
c. 3100 BCE is when writing and states appear** — which is what the three were reaching
back to, not a date they inherited from each other.

Copy:

> **TWELVE YEARS APART**
> 3114 BCE and 3102 BCE, computed in different centuries on different continents.
> What they share is not a memory. It is the moment writing starts.

### Step 5 — THE TWO FLOODS

Ussher's Flood at 2348 BCE against the King List's, which this project places at
c. 3000–2900 BCE: **552–652 years apart**, a range because the anchor is a range. Both
dates fall inside somebody's continuous dated record.

Then Schmidt, in the same frame and not as a footnote: the stratigraphy is his
(*Museum Journal* XXII, 1931), **the date is not**; he put the inundation six hundred
years earlier; the culture break across his layer is **not complete** and there were **no
victims**; and the deposits at Ur, Kish and Shuruppak are **of different dates and cannot
be one event**.

Copy:

> **TWO FLOODS, SIX HUNDRED YEARS APART**
> One flood story, two traditions, and a gap wider than the Old Kingdom.
> The layer under Shuruppak is real. Whose flood it is, and when, is ours to argue.

### Step 6 — BACK OUT

The camera pulls back to step 1's line and **fills in what no clock reaches**: the 84% to
the left of Göbekli, every dated thing on it still drawn. Then the handoff.

Copy:

> **EVERYTHING BEFORE MEMORY**
> Every civilisation counted back to the beginning. None of them could count that far.
> *[ EXPLORE THE WHOLE RECORD ]*

---

## 2. THE LANDMARKS, PER STEP

**Every landmark below is already in the repo's data**, with its own tier and its own
source. Nothing here is typed from memory, and the build must resolve them from the data
rather than hard-coding them — the same rule the panel already follows.

Tier key as on the panel: **S** well-supported, **C** contested, **T** tradition-only.

### Step 1 and step 6 — the true-scale line (from `ANCHORS`, 565 of them)

Eight named, spread across the window so the eye has somewhere to land:

| date | landmark | tier |
|---|---|---|
| 62,974 BCE | Madjedbebe — the oldest date in Australia | C |
| 49,174 BCE | Leang Karampuang — the oldest story | S |
| 33,974 BCE | Chauvet | S |
| 21,974 BCE | Mal'ta — the Ancient North Eurasians | S |
| 19,974 BCE | White Sands — footprints older than the way in | S |
| **9600 BCE** | **Göbekli Tepe** — the anchor of the whole sequence | S |
| 3100 BCE | Stonehenge | S |
| 2600 BCE | Caral-Supe | S |

Each of those is a real row in `ANCHORS` and the dates are the data's own, not rounded
for the slide. **Two I had to drop after checking:** Lascaux and Çatalhöyük are not in
this map's anchor set, and putting them on screen would have meant typing a date — which
is the one thing nothing on this panel does. Mal'ta and White Sands took their places and
are better anyway: they put Siberia and the Americas on a line that otherwise runs
Africa → Australia → Europe.

**On Göbekli's date:** the alignment `al10` spans 9600–8200 BCE, the building period, and
the `ANCHORS` dot sits at 9,500 BCE as a single representative date. The story uses the
alignment's **9600 BCE**, because the claim is about when monumental building starts.
Both numbers are in the data and they do not disagree; the step should not show both.

Behind them, **all 498 in-window anchors as a faint density ribbon** — the same ribbon
Explore will use (§4). The named eight are labelled; the rest are texture, and texture is
honest here because the point of the screen is proportion, not enumeration.

### Step 2 — the zoom, 4000–2500 BCE (37 anchors in window, eight named)

| date | landmark | tier |
|---|---|---|
| 3874 BCE | Sannai-Maruyama — a town with no farming under it | S |
| 3600 BCE | Ġgantija, Malta | S |
| 3474 BCE | Watson Brake — older than the pyramids | S |
| 3200 BCE | Newgrange | S |
| 3100 BCE | Stonehenge | S |
| 2700 BCE | Gilgamesh — Uruk | S |
| 2600 BCE | Caral-Supe | S |
| 2500 BCE | Mohenjo-daro | S |

### Steps 3–5 — from `data/lanes/lanes.json`, unchanged

Step 3 takes the six `reckoningStart` values and the five manifest images. Step 4 is
alignment `al02` and its note. Step 5 is pair `gap-flood` (`gap` 552, `gapTo` 652) and the
`trad-skl` anchor's own `anchorNote`. **No new research, no new sourcing pass.**

---

## 3. (c) HOW THE TRUE-SCALE LINE HANDLES 70,000 YEARS

Four problems, and the answer to each.

**1. 55 years to the pixel, and 206 on a phone.** Anything shorter than that cannot be
drawn to width. Marks on this screen are therefore **points, not bars** — a dot and a
label, never a span, because a span drawn at its minimum width is a lie about duration on
the one screen whose whole argument is duration. Spans return at step 2's zoom, where a
century is 87 px.

**2. The left edge cuts off 67 of the map's 565 anchors**, the oldest being Dmanisi at
1.8 million years — **twenty-five times further back than this screen's left edge.**
Ignoring that would be the same error the panel already fixed once for the yuga cycle.
Use the device the panel already has: **a left-edge off-scale marker**, the same form as
the Hindu lane's *"◄ and 4.32 million years before that, off this map"*. Here it reads
**"◄ and 1.73 million years before this, off this screen — 67 more dated anchors"**.

**3. Why 70,000 BCE and not the full 1.8 million.** Because at 1.8 million the human
story is 4% of the line and the six clocks are a third of a pixel — the screen stops
saying "recorded memory is short" and starts saying "nothing happened", which is false.
70,000 BCE is the right window for an episode about reckonings, and the marker in (2) is
what keeps it honest. **Flagging it as a judgement call: it is a crop, and crops are
arguments.**

**4. What is actually visible at the left.** 115 of the 498 in-window anchors sit left of
Göbekli — Africa, Australia, island Southeast Asia, the first art. At 55 years to the
pixel they are a scatter of dots about 1,000 px wide, dense enough to read as a populated
stretch of line rather than as emptiness. **This matters more than it sounds**: the
failure mode of "everything before memory" is a blank left side, which reads as *nothing
was there* — the exact opposite of the claim. The density ribbon is what stops the screen
arguing against itself.

And one number worth putting on screen: **332 of the 498 anchors — two thirds of the
whole dated record — fall inside that last 8.4% with the clocks.** The record thickens
exactly where the reckonings begin. That is not a coincidence to explain away; it is the
episode's thesis in one measurement.

---

## 4. (d) WHAT CHANGES IN THE PANEL FOR EXPLORE

Six changes. None of them touches the data, the tiers or the sourcing.

1. **Clocks first, ground second.** Group order becomes **Reckonings → Dynasties and
   states → Regions**. Today the six clocks — the point of the panel — sit below nine
   lanes of unlabelled ticks, so the first thing the eye meets is the noise.
2. **The nine region lanes collapse to one density ribbon by default**, labelled
   *"565 dated anchors across nine regions"*, expanding to today's nine lanes on a click.
   The ribbon is the same figure step 1 uses, so Explore opens in the visual language the
   story just taught.
3. **"Width is not duration" shrinks to one line** with the full note behind an
   *(i)* — because step 1 has already shown it, and a viewer arriving from the story does
   not need the paragraph. **Explore must still work cold**, so the one line stays
   permanently visible rather than being removed.
4. **The period images come out from behind the bands and become the lane's card**, at the
   left of each tradition row, where step 3 put them. Invisible wallpaper at 10–26%
   opacity is worth less than a 40 px thumbnail you can actually see — and the five
   credits become legible rather than technically present.
5. **A "back to the story" control**, so Explore is a place you can leave.
6. **Landmarks keep their names at every zoom.** The ticks read as noise partly because
   they are anonymous; at any zoom, the widest-spaced handful in view get labels.

**What does NOT change:** the age-weighted axis, every tooltip, every tier, every source
line, the alignments, the gap connectors, the phone sheet and tap-to-read, and all 114
checks. Explore is the instrument, and the instrument was not the thing that was wrong.

---

## 5. WHAT I AM NOT DOING YET

No code on the page. The frames that come with this doc are **mockups rendered from a
standalone prototype in `geowork/story/`**, not from `index.html`, and the prototype is
not in the build chain. Nothing in `index.html`, `data/` or `img/` is touched on this
branch.

When the frames are approved, the build order is: step 1's true-scale figure first (it is
the only genuinely new drawing primitive), then the sequence shell with keyboard and
swipe, then steps 2–6 on top of the existing lane renderer, then the Explore changes in
§4, each with render-level checks at 1400 px and 390 px, as everything else here has been.
