# OPEN ITEMS — Synchronoptic Lanes

Companion to `DESIGN_Synchronoptic_Lanes.md` and `RESEARCH_Synchronoptic_Lanes_Sourcing.md`.
Everything here is **unresolved or needs tightening before publication**. Items are struck
out, with what settled them, rather than deleted — a resolved question is worth as much as an
open one when the next person asks why a date on the chart is the date it is.

Last reviewed 2026-11-25.

---

## BLOCKS PUBLICATION

### 1. Tighten the Fara sourcing for the Sumerian Flood anchor
**Founder-ruled 2026-11-25: the anchor stays as built — c. 2900 BCE, labelled approximate and
contested in its tooltip — and this item records what still needs doing.**

The panel hangs the Sumerian King List's Flood on the flood deposit at Shuruppak (Tell Fara),
excavated by Erich Schmidt in 1931: water-laid clay between Jemdet Nasr and Early Dynastic I
levels. Shuruppak was chosen because Ziusudra, the List's own flood hero, is king *of*
Shuruppak — the one place the two records touch.

**What is weak.** The 2900 BCE figure, and the 2900–2750 range, currently rest on secondary
overviews and summaries rather than on the excavation record or a modern review of the Fara
sequence. This is the least well-sourced number on the whole panel.

**What would settle it.** Schmidt's own 1931 publication, or a current treatment of the Fara
stratigraphy. Either would also settle whether the deposit belongs at the Jemdet Nasr / ED I
transition (c. 2900) or at the end of ED I (nearer 2750), which the sources disagree about.

**Also note, and keep in the tooltip whatever the date turns out to be:** several scholars
read the 2900 deposit as *not* being the myth's flood at all, because the List places
Ziusudra's kingship before the flood. That objection survives any refinement of the date.

---

## OPEN, DOES NOT BLOCK v1

These are the eight the sourcing pass listed. Five touch only the dynasty group (v2, to be
built from RESEARCH Part B); three touch tradition lanes and were scoped around rather than
resolved.

| # | item | touches | state |
|---|---|---|---|
| 2 | Erlitou radiocarbon range | Part B, China | open — v2 |
| 3 | 1900 BCE Mature Harappan end | Part B, Indus | open — v2 |
| 4 | Roman Empire 27 BCE / 476 CE | Part B, Rome | open — v2 |
| 5 | Chavín revised phasing | Part B, Andes | open — v2 |
| 6 | Minoan sequence start | Part B, Aegean | open — v2 |
| 7 | Does the Turin King List open with divine rulers? | Egyptian lane | **scoped around** |
| 8 | Three Sovereigns dates | Chinese lane | **scoped around** |
| 9 | A larger free scan of the Weld-Blundell Prism | Sumerian lane image | open — see below |

**7 — Turin.** The Egyptian lane's divine reigns are sourced to Manetho via Eusebius, which is
independent of the Turin question, and §4a offered "the Turin **or** Abydos list" as the
period image. Abydos is used (76 kings from Menes, sourced), so Turin does not block anything.
Still worth resolving before the image goes in, in case Turin is the better plate.

**8 — Three Sovereigns.** The Chinese lane begins at the Yellow Emperor (2698/2697 BCE,
sourced, and flagged in the tooltip as a god later historicised). Anything earlier waits on
this item.

---

### 9. Replace the Weld-Blundell Prism image with a larger free scan
**Founder-ruled 2026-11-26: use the 320 px file for now. This does NOT block
publication.**

The period image behind the Sumerian lane is `File:Sumeriankinglist.jpg` on Wikimedia
Commons — the only photograph of the prism released into the public domain outright.
At **320 × 589** it is the smallest source on the panel: the strip behind that lane is
enlarged from a 212 × 35 crop and is visibly softer than the other four.

**What would settle it.** A larger scan of Ashmolean AN1923.444 under a licence with no
share-alike condition. The better-resolution photographs now on Commons are CC BY-SA 4.0,
which is why they were passed over — see `IMAGE_TERMS_Synchronoptic_Lanes.md`. The
Ashmolean's own collections site is the obvious place to ask.

---
## RESOLVED

- ~~**Kalpa: 1,000 or 2,000 mahāyugas?**~~ **Resolved 2026-11-25, and the two figures were
  never rival claims.** A kalpa is 1,000 mahāyugas, 4.32 billion years, one *day* of Brahma.
  The 2,000 sometimes quoted is a day *and night* together, 8.64 billion. Both are now in the
  Hindu lane's off-scale note.
- ~~**Manetho's 24,900 lunar years in solar.**~~ **Resolved 2026-11-25: 2,206 solar**, which
  is the figure the texts themselves give (Waddell's Loeb; the Armenian Eusebius). An earlier
  working note of "≈2,014" was wrong — that is roughly what dividing by a synodic year gives,
  but it is not what the source says. The lane draws the 24,900 as written and records 2,206
  in the tooltip.

---

## FOUND WHILE BUILDING, NOT IN THE ORIGINAL LIST

- **`data/borders/coverage.json` lists Europe twice and Inner Asia twice**, each with a
  different set of boxes. The region lanes deduplicate by key. Nothing else in the map
  aggregates those entries, so nothing else is affected — but anyone else reading that file
  should know.
- **Cliopatria v0.2.1: 171 of 1,413 Wikidata ids (12%) carry more than one polity name**
  (`Q1068371` is Han Dynasty, Chauhan Dynasty and a Han–Xiongnu alliance at once). This is why
  the dynasty group will be built from RESEARCH Part B and not from the acts. Full list:
  `TLW_FINDING_Cliopatria_QID_collisions_2026-11-25.txt`.
- **The page's tick strip was up to 11.3 px out from its own scrubber thumb.** Fixed
  2026-11-25; the strip and the lanes now share one measurement.
