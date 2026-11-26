# DESIGN — Synchronoptic Lanes ("What Was Happening at the Same Time")

*Design note for the interactive map (The Long Walk). Drafted 2026-11-25 by Fathom at Shawn's request. Status: DESIGN ONLY, nothing built. **FOUNDER RULINGS 2026-11-25:** six tradition lanes (§4a); a panel under the map (§4); big-dynasty lanes added (§4b); the Adams style for tradition lanes only, a period image behind every tradition lane, and an episode outlined now (§7). Sourcing pass done: RESEARCH_Synchronoptic_Lanes_Sourcing.md. Episode outline: Episode_Six_Clocks.md.*

---

## 1. The idea in one paragraph

A **lane panel under the migration map**: time runs left to right, and each region, dynasty or tradition gets its own horizontal lane, so a single vertical slice shows what every part of the world was doing at the same moment. **Six lanes are traditions' own chronologies**, each drawn as *what the tradition reckons*, next to the dated history and archaeology lanes. Where they disagree with the ground, or with each other, the gap is drawn on purpose. **The Divergence Test, drawn as a picture.**

## 2. Where it comes from

**Adams' Synchronological Chart** (Sebastian C. Adams, Presbyterian minister and educator, first published 1871; editions through 1881). It's a 23-foot fold-out timechart that runs each civilization in its own coloured band and merges secular history with a Biblical chronology starting from Adam in 4004 BC (Ussher's date). Full digital copies are in the David Rumsey Map Collection.

What it does brilliantly, and what we take: **bands in parallel, read down a column for simultaneity.** Its own rules worth borrowing: a stream ends at conquest, splits at independence, merges at absorption; question marks flag disputed dates.
What it can't do, and why that is our hook: **it starts at 4004 BC, so everything older has nowhere to go.** Göbekli Tepe (~9600 BCE), the Tas Tepeler sites, and the whole deep-time story of the Long Walk sit off the left edge of Adams's paper. Our version puts them on the page *and* keeps his lane, so the reader can see exactly where a tradition's clock starts and what lies before it.

## 3. Rules it must keep (existing standing rules)

- **"Let the map be a map."** Opacity means time only. Evidence tiers live in tooltips, not the visual layer.
- **Evidence tiers unchanged:** the map's existing tiers (well-supported, contested, pre-sapiens, tradition, no verified evidence). Every item on a lane carries its tier in its tooltip.
- **The Divergence Test** is the methodology; this view is a display of it, not a new standard.
- **A CHANGE TO AN APPROVED SET COMES BACK BEFORE IT IS USED (ruled 2026-11-26).** Once Shawn has approved a specific set — these files, these sources, these licences — swapping any member of it for a different file, source or licence is a decision for him and not for whoever is building. **Write the case and wait for his word, EVEN WHEN THE REPLACEMENT IS PLAINLY BETTER.** The rule comes from a case where it was: the approved oracle-bone photograph turned out on download to show the uninscribed face of the bone through museum glass, and was replaced mid-build with a British Library scan of the inscribed face under the same licence. The swap was kept, and it should still have been asked. “Obviously better” is exactly the reasoning that makes an approval stop meaning anything.
- **Tradition lanes are labelled as tradition**, never as history and never mocked. The tone is "here is what this tradition reckons, here is what the ground shows". **No lane is privileged**: all six get the same treatment.

## 4. Layout (RULED 2026-11-25: a panel under the map)

| | |
|---|---|
| **Where** | **A panel under the existing Long Walk map**, sharing its scrubber, so map and lanes are seen simultaneously. Scrubbing moves a vertical "now" line across the lanes; clicking a lane item moves the map. |
| **Axis** | One shared time axis with the scrubber, using the **same non-linear era checkpoints**, so deep prehistory and recent centuries both get readable space. |
| **Three groups of lanes, top to bottom** | (1) **Regions**: archaeology, one lane per region the map uses, from existing anchor data. (2) **Dynasties and states** (§4b). (3) **Traditions** (§4a): six reckonings. |
| **Style (RULED)** | The map's house style for regions and dynasties; **the Adams look (inked bands, period lettering) for the six tradition lanes only**. |
| **The divergence gap** | Before a tradition's reckoning begins, its lane shows a **hatched "before this reckoning" zone**, with a tooltip saying so plainly. Where a tradition lane and a history/archaeology lane name the same thing with different dates, a thin connector links the two, labelled with the size of the gap. |
| **Simultaneity column** | Hovering any point in time highlights everything on every lane within that window, Adams-style. |
| **Collapsing** | With ~20+ lanes, each group must collapse/expand, and lanes can be pinned. |

### 4a. THE SIX TRADITION LANES (ruled 2026-11-25)

Dates and labels: see RESEARCH_Synchronoptic_Lanes_Sourcing.md Part A.

| lane | reckoning | where its clock starts | period image behind the lane (RULED: one per lane) |
|---|---|---|---|
| **Biblical** | Ussher (1650), as drawn by Adams (1871) | Creation, 4004 BC (other Biblical reckonings 3761–5509 BC) | a strip of the 1871 Adams chart |
| **Hindu** | the yuga cycle | Kali Yuga epoch 3102 BCE; the deep cycle reaches far older | a manuscript page |
| **Maya** | the Long Count | 13.0.0.0.0 = 11 Aug 3114 BCE (GMT) | a Long Count stela |
| **Chinese** | traditional chronology | Yellow Emperor (trad. 2698/2697 BCE), Xia, Shang, Zhou; year-precise from 841 BCE | an oracle bone |
| **Egyptian** | Manetho; Turin, Abydos, Palermo lists | reigns of gods and demigods, then Menes / Dynasty 1 | the Turin or Abydos list |
| **Sumerian** | the Sumerian King List | kingship descends from heaven; 8 kings, 241,200 years; the Flood; Kish | the Weld-Blundell Prism |

Every image's reuse terms get checked first; a lane whose image can't be cleared runs without one rather than borrowing another tradition's.

**Alignments, handled carefully:** several reckonings begin near 3100 BCE (Kali Yuga 3102, Long Count 3114; Egypt's Dynasty 1 radiocarbon-dated 3111–3045), and two traditions carry a Flood. By the Divergence Test these are coincidences or shared inheritances to be explained, not evidence of a common event. Each alignment tooltip says so, with its honest tier.

### 4b. DYNASTIES AND STATES

Egypt; Mesopotamia; Indus; China; Persia; Greece and Rome; Mesoamerica; Andes. Dates and conventions: RESEARCH Part B. Each band carries its scholarly convention and uncertainty in the tooltip.

## 5. Data shape

Each lane item: `lane`, `group` (region / dynasty / tradition), `label`, `start`, `end` (or a point), `tier`, `source`, `note`, optional `pairs_with`. Tradition items also carry `tradition` and `reckoning`. Dynasty items carry `convention` (e.g. "middle chronology").

## 6. Why

The show's central question made visible: how much happened before the stories begin. Six traditions side by side make it about how humans reckon time. It debuts in the episode "Six Clocks".

## 7. Rulings (all 2026-11-25)

Six tradition lanes; a panel under the map; the Adams look for tradition lanes only; one period image behind every tradition lane, reuse terms checked; episode outlined.

## 8. Next steps

1. Resolve the sourcing pass's eight open items (listed in RESEARCH) — note which block v1.
2. Build v1 against the existing map data plus the sourced lanes.
