# OPEN ITEMS — Synchronoptic Lanes

Companion to `DESIGN_Synchronoptic_Lanes.md` and `RESEARCH_Synchronoptic_Lanes_Sourcing.md`.
Everything here is **unresolved or needs tightening before publication**. Items are struck
out, with what settled them, rather than deleted — a resolved question is worth as much as an
open one when the next person asks why a date on the chart is the date it is.

Last reviewed 2026-11-26.

---

## PUBLISHED AGAIN — 2026-11-27, STORY MODE

**Founder-ruled.** The guided sequence leads and the panel is Explore. Live at
https://shawngreene1981-cmyk.github.io/the-long-walk/

| | |
|---|---|
| merge commit | **`5ee117e`** — `--no-ff`, parents `a06f755` and `75e0887` |
| rollback point | **`a06f755`**, the tip of `main` before this merge |
| published `index.html` | sha256 `de05cbbe3c54d7c5…`, 1,343,185 bytes |
| checks at the gate | 155 — 96 desktop, 19 phone, 40 story |

**The branch rule returned with that push.** `lanes-story` is the working branch and
nothing is pushed without a new ruling. The checklist below was run in full again, with
its corrected hash line, and the live checks (`geowork/lanes/shot_live.py`) now cover
story mode as well as the panel.

---

## PUBLISHED — 2026-11-26

**Founder-ruled, and done.** The panel is live at https://shawngreene1981-cmyk.github.io/the-long-walk/

| | |
|---|---|
| merge commit | **`a06f755`** — `--no-ff`, parents `19875a4` and `6f604ce` |
| rollback point | **`19875a4`**, the tip of `main` before the merge |
| published `index.html` | sha256 `38ff426a3a2b6c78…`, 1,300,506 bytes |
| deploy | `git push origin main`; GitHub Pages served the new page about 20 seconds later |

**The branch rule returned with that push.** `synchronoptic-lanes` is the working
branch again and **nothing is pushed without a new ruling.** The checklist below was
run in full before the merge and is kept, not struck out: it is the procedure for the
next publication as much as the record of this one.

The one item that had blocked — the Fara sourcing behind the Sumerian Flood anchor
— was researched, the anchor was widened to a range, and the item was released
before any of this.

---

## THE PUBLICATION CHECKLIST

**Written 2026-11-26, and RUN IN FULL the same day** on the founder’s publication
ruling. It is kept here as the procedure for the next one. **`19875a4` is the
pre-publication tip of `main`** — the number to quote in any rollback.

**What the run produced**, for the next person who follows it:

- pre-flight §A: a full rebuild left the tree clean at `index.html` **1,300,506
  bytes**; 95 desktop and 19 phone checks passed; `origin/main..main` was empty;
- §B: merge `a06f755`, pushed `19875a4..a06f755`;
- §C: the live page was still the old one on the first look and the new one about
  **20 seconds** later. It was not re-pushed;
- **one line of §C was wrong and is corrected below.** See the note on `autocrlf`.

The live site is classic GitHub Pages off `main`’s root: there is no workflow in
`.github/`, so pushing `main` IS the deploy. It usually rebuilds in under a minute.

### A. Before the merge — pre-flight, on `synchronoptic-lanes`

1. **Prove the page is reproducible and was not hand-edited.** Rebuild it from the two
   base commits and the patch chain, then look at the tree:

   ```sh
   cd /c/Users/shawn/geowork && sh build_page.sh
   cd /c/Users/shawn/Before-Us/tlw-repo && git --no-optional-locks status --short
   ```

   **The status must come back EMPTY.** A dirty tree after a rebuild means the committed
   page is not the page the build produces, and the rule that the page is built and never
   hand-edited has already been broken somewhere. *Run at `189422b` on 2026-11-26: clean,
   `index.html` 1,300,506 bytes.*

2. **Both check suites, against the rebuilt page**, from `/c/Users/shawn/geowork/lanes`
   with the venv Python (`/c/Users/shawn/geowork/.venv/Scripts/python.exe -I`):

   ```sh
   python -I check_lanes.py     # expect: all lanes checks passed   (95 desktop)
   python -I check_phone.py     # expect: all phone checks passed   (19 at 390 px)
   ```

   Both end with a clean-console check. Neither can test the LIVE page: each serves this
   working copy over a local port. They prove what is about to be published, not what is.

3. **Read what publication would actually put on the site**, rather than assuming:

   ```sh
   git --no-optional-locks log --oneline main..synchronoptic-lanes
   git fetch origin && git --no-optional-locks log --oneline origin/main..main
   ```

   The second must be empty. If `main` has anything of its own, that lands on the live
   page too, and it has not been looked at as part of this work.

### B. The merge and the push — only on the founder’s publication ruling

```sh
cd /c/Users/shawn/Before-Us/tlw-repo
git checkout main
git merge --no-ff synchronoptic-lanes -m "Publish the synchronoptic lanes panel"
git push origin main
git checkout synchronoptic-lanes        # so later work cannot land on main by accident
```

**`--no-ff` is not cosmetic.** It makes ONE merge commit, and that single commit is what
makes the rollback in §D a single revert. A fast-forward leaves no one thing to undo,
and the only way back is rewriting published history.

**Push `main` only.** Pushing `synchronoptic-lanes` itself is a separate decision and is
not needed to publish. Do not delete the branch: §D needs it.

### C. What to check on the live page afterwards

Live URL: `https://shawngreene1981-cmyk.github.io/the-long-walk/`

**First, that the deploy landed at all** — the one part of this a command settles:

```sh
git show main:index.html | sha256sum                      # NOT sha256sum index.html
curl -s https://shawngreene1981-cmyk.github.io/the-long-walk/ | sha256sum
curl -sI https://shawngreene1981-cmyk.github.io/the-long-walk/data/lanes/lanes.json
curl -sI https://shawngreene1981-cmyk.github.io/the-long-walk/img/lanes/adams-panorama.webp
```

**Hash the COMMITTED BLOB, not the working file.** This repo is checked out with
`core.autocrlf=true`, so the `index.html` on disk is CRLF and **1,309,001 bytes** while
the blob git stores — and GitHub serves — is LF and **1,300,506 bytes**. Their
hashes can never match, and `sha256sum index.html` therefore reports a failed deploy on
a deploy that worked perfectly. The first version of this checklist said exactly that,
and running it is what found the mistake.

The two hashes must match, and both `curl -sI` must give **200**. If the live hash is
still the old one, Pages has not finished rebuilding — **wait and look again; do not
re-push.** A second push does not make a build go faster and it muddies §D.

**Then run the live checks:** `python -I geowork/lanes/shot_live.py` (written
2026-11-26). Thirteen render-level checks against the published URL in headless Edge,
and the frames to go with them. Every other check in this project serves a local copy,
so none of them can say anything about the live site: byte-identity proves the HTML is
the same, not that it renders when the assets come over https from Pages. It measures
the anchor band, the beat-5 chip and its three caps, the Roman Republic bar, the five
images arriving from the live origin, the phone sheet and tap-to-read. The human list
below is still worth doing — but it is no longer the only thing standing between a
broken deploy and nobody noticing.

**Desktop, in a real browser** (the checks only ever used headless Edge):

- the panel is under the map, the six clocks open, the dynasty and state group collapsed;
- scrub the slider end to end: the reveal follows it, the now line tracks, the tick strip
  stays aligned to the thumb;
- **BEAT 5** — the dashed bracket in the gutter joining the Biblical clock to the
  Sumerian one. The chip must read **552–652 YEARS**. Hover the run: the tooltip
  names Ussher’s **2348 BCE** and the anchor as **3000 BCE to 2900 BCE**;
- **the Sumerian Flood anchor is a BRACKETED BAND** with an upright at each limit and the
  ≈ mark — not a rule with a diamond. Hover it: this project’s placement,
  Schmidt’s own mid-fourth-millennium date, the incomplete culture break, the absent
  victims, the different-dated deposits, and the tier **contested**;
- spans have real width. **The Roman Republic bar in the dynasty group is the one that
  exposed the 1.3 px bug** — look at it specifically;
- each tradition lane’s inked band carries its period image, and the Hindu lane has
  none, as ruled;
- the browser console is clean.

**390 px phone.** Device emulation is fine, but **load AT 390 px — do not resize a
desktop page down into it.** The page reads the breakpoint while it builds, and resizing
afterwards is not the same thing.

- the panel is a bottom sheet; its head is sticky and paints ABOVE the chart, not under
  it; the hint is visible;
- **the tap-to-read box**: tap a span, an anchor and a connector. Each opens the box with
  the same text the desktop tooltip gives. The ✕ closes it, and **the hint comes back
  when it does** — both have been bugs here;
- no alignment label is sliced at the panel edge (“…BESIDE AUGUSTUS AND TH”
  was the one that got through);
- widen back past 760 px: the page unlocks, the body scrolls again, the desktop layout
  returns and the track refits to the thumb.

**The image credits**, which are the part with a licence behind it:

- every inked band’s tooltip carries its own image credit — five rights holders on
  four different bases, and a reader checking one should not have to unpick a paragraph;
- the credits roll (presentation mode, `?present=1`) lists the lanes data entry and all
  five image entries;
- **the Adams entry must say third edition, 1878, and that the file was downscaled and
  re-encoded.** Faithful reproduction is the basis on which that one is free to use at
  all, so a credit that omits the re-encoding is the credit that matters most here.

### D. How to roll back

**Route 1, preferred — one commit, no rewritten history:**

```sh
cd /c/Users/shawn/Before-Us/tlw-repo
git checkout main
git revert -m 1 <the merge sha from §B>
git push origin main
```

That undoes the whole merge and Pages rebuilds to the previous page. The work stays on
`synchronoptic-lanes` untouched, so it can be fixed and re-merged.

**If only the page is wrong and the merge should stand**, restore the one file the site
actually serves:

```sh
git checkout main
git checkout 19875a4 -- index.html
git commit -m "Restore the pre-publication page while the panel is fixed"
git push origin main
```

The panel lives entirely inside `index.html`. `data/lanes/lanes.json` and `img/lanes/`
left behind are then unreferenced and harmless.

**Route 2, only on an explicit ruling:** `git reset --hard 19875a4` and
`git push --force-with-lease origin main`. It rewrites published history, and it restores
the live page **no faster than route 1**, so there is no reason to reach for it in a
hurry.

Whichever route: **do not delete the branch**, and **do not rerun `build_page.sh` while
the live page is broken.** A rebuild changes this working copy, never what is already
deployed, and it costs the one clean comparison — committed against live — that
tells you what actually went out.

---

### 1. ~~Tighten the Fara sourcing for the Sumerian Flood anchor~~ — RESOLVED,
no longer blocking

**Resolved 2026-11-26.** The anchor is now **c. 3000–2900 BCE, a range and not a
date**: the Jemdet Nasr / Early Dynastic I boundary, where the flood deposit at Shuruppak
(Tell Fara) lies. Its tier stays **contested**.

#### What the sourcing pass found

**Schmidt 1931 was found and read in full.** Erich F. Schmidt, “Excavations at Fara,
1931”, *The Museum Journal* XXII.3–4 (September 1931), 193–217, University of
Pennsylvania — free HTML at `penn.museum/sites/journal/9356/`. The Journal prints its
own warning at the head that it is a **preliminary field report**.

In plots DE 38/39, at **4–5 m below the mound surface**, the soil turns nearly sterile
— yellow clay and sand. Beneath it: charcoal, ash, dark culture refuse and the first
complete polychrome vessel, the Jemdet Nasr stratum. Above it: Early Sumerian. He calls it
alluvial soil and an inundation layer. **The stratigraphy our tooltip described was
accurate.** Four other things were not:

1. **Schmidt did not date it to 2900 BCE.** On the chronology of 1931 he put the Jemdet
   Nasr period in the first half of the fourth millennium and the inundation at about its
   **middle** — some six hundred years earlier than our figure.
2. **The figure came from elsewhere**: the modern radiocarbon dating of Jemdet Nasr
   (c. 3100–2900 BCE), which places the JN / ED I boundary where his deposit sits, and
   **Mallowan, “Noah’s Flood Reconsidered”, *Iraq* 26 (1964)**. A legitimate
   inference, **but ours**, and now labelled as ours in the tooltip.
3. **The old tooltip’s range, which ran on to the end of ED I, did not survive.**
   Nothing in the pass supported it. It has been removed everywhere it appeared.
4. **Two caveats in Schmidt’s own report were missing from our tooltip**, and both
   weaken the anchor. The culture break across the layer is **not complete** — Early
   Sumerian bowls at the same level as the Jemdet Nasr vessels beneath it, and sherds
   below it he could not tell apart from those above. And there were **no victims**, from
   which he concluded that either the people were warned and fled, or the end of the
   Jemdet Nasr settlement merely *coincided* with the inundation. He declined to call it
   one event at all.

And the objection that survives all of it: **the deposits are of different dates and
cannot be one flood** — Ur c. 3500 BCE, Kish three (two c. 2900, one c. 2600),
Shuruppak at this boundary. That is on top of the King List putting Ziusudra’s
kingship *before* the flood.

**All five points are now in the anchor’s own tooltip**, and a check asserts each of
them by name, so none can quietly fall out again.

#### Follow-up reading — does NOT block

- **Harriet P. Martin, *Fara: A Reconstruction of the Ancient Mesopotamian City of
  Shuruppak* (Birmingham, 1988)**, the standard synthesis, freely downloadable from Stony
  Brook’s Archive of Mesopotamian Archaeological Reports (`hdl.handle.net/11401/89085`,
  309 pp., a 560 MB scan).
- **The German–Iraqi excavations**, Otto (LMU Munich) with al-Hussainy (Al-Qadisiyah):
  Otto, Fink, Herbst, Seabrook & Einwag, *MDOG* **156** (2024) and **157** (2025),
  “Neue Feldforschungen in Fāra / Šuruppak”, covering the 2022 and 2024
  seasons. Their published summary makes no flood-deposit claim and dates the Fara period
  proper to c. 2600–2475 BCE. They also record that the main hill is **massively
  damaged by illegal excavation**, so Schmidt’s section is now much harder to
  re-check in the field.

---
## OPEN, DOES NOT BLOCK v1

These are the eight the sourcing pass listed. Five touch only the dynasty group (v2, to be
built from RESEARCH Part B); three touch tradition lanes and were scoped around rather than
resolved.

| # | item | touches | state |
|---|---|---|---|
| 2 | Erlitou radiocarbon range | Part B, China | **resolved as contested** |
| 3 | 1900 BCE Mature Harappan end | Part B, Indus | **resolved — against Part B** |
| 4 | Roman Empire 27 BCE / 476 CE | Part B, Rome | **resolved** |
| 5 | Chavín revised phasing | Part B, Andes | **resolved as contested** |
| 6 | Minoan sequence start | Part B, Aegean | **resolved** |
| 7 | Does the Turin King List open with divine rulers? | Egyptian lane | **scoped around** |
| 8 | Three Sovereigns dates | Chinese lane | **scoped around** |
| 9 | A larger free scan of the Weld-Blundell Prism | Sumerian lane image | open — see below |
| 10 | Persia lane: one bar, Achaemenid only | Part B, Persia | open — see below |

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

### 10. Persia lane: one bar. Achaemenid, Parthian and Sasanian unsourced
**Founder-ruled 2026-11-26: not now. This does NOT block publication, and the lane’s own “no source checked” note stays exactly as it is.**

RESEARCH Part B sources the Achaemenid empire (550–330 BCE) and nothing else for Persia, so the lane draws one bar across a span the rest of the panel fills with four or more. The Seleucid, Parthian and Sasanian states are absent **because they were not in the sourcing pass, not because they were judged unimportant**.

**The lane says this itself**, in its own tooltip, and that wording is the point of the item: *an empty stretch of lane here means no source was checked, which is a different thing from an empty stretch meaning nothing was happening.* Any panel that draws some regions densely and others thinly owes the reader that distinction.

**What would settle it.** A sourcing pass for post-Achaemenid Iran on the same footing as Part B: Seleucid, Parthian/Arsacid and Sasanian, with the chronology convention stated, as the other lanes do.

---


## RESOLVED IN v2 — the five Part B items

All five were closed on 2026-11-26 while the dynasty group was typed. **Three of them
resolve to “contested”, which is a result and not a failure**: the literature does
not agree, the lane says so in its own tooltip, and the mark carries the contested tier.

- ~~**2. Erlitou radiocarbon range.**~~ **Resolved as CONTESTED.** The
  Xia–Shang–Zhou Chronology Project’s 2000 chart begins the Xia at 2070 BCE;
  a larger series of radiocarbon samples from Erlitou’s lower layers moved the
  site’s own start to about **1750 BCE** (Wu Xiaohong, Peking University, reported in
  *Science*), and Erlitou’s excavation director has publicly called the project
  political. The lane draws **1750–1520** and **does not label Erlitou “Xia”**,
  because whether the site is the dynasty the texts describe IS the dispute. The
  traditional Xia date stays on the Chinese tradition lane, where it belongs.
- ~~**3. 1900 BCE Mature Harappan end.**~~ **Resolved AGAINST Part B.** Part B gave
  Mature c. 2600–2000 and Late to c. 1700. Kenoyer’s table (2008), and
  Shaffer’s Integration / Localisation eras behind it, give **2600–1900** and
  **1900–1300**, and the 1900 boundary is common to nearly every published scheme.
  Part B’s figures are superseded on the lane and the lane note says so. What is
  still disputed is the Mature start (2600 or 2800) and the Late end (1300 or 1500).
- ~~**4. Roman Empire 27 BCE / 476 CE.**~~ **Resolved.** 27 BCE is a constitutional
  moment; **476 CE is a modern convention**, the deposition of Romulus Augustulus, and
  it ends only the WESTERN empire. The eastern empire ran to 1453, **which this
  map’s axis reaches**, so it is drawn rather than left off. The two bars overlap
  from the division of 395, and that overlap is declared in `build_lanes.py`.
- ~~**5. Chavín revised phasing.**~~ **Resolved as CONTESTED.** Part B’s
  c. 900–200 BCE is Burger’s OLD chronology. His own later AMS sequence has the
  site founded **c. 950 cal BC** and abandoned **by c. 400 cal BC**; Kembel’s
  architectural sequence instead puts five construction phases at **1100–550 BC**,
  moving the Janabarriu phase some four centuries earlier than the old scheme. The bar
  follows the radiocarbon sequence and the architectural one is in its tooltip.
- ~~**6. Minoan sequence start.**~~ **Resolved.** Part B’s “palaces from c.
  1900” is the date of the FIRST PALACES, not of the Minoan sequence, which begins
  at Early Minoan I, **c. 3100 BCE**. The lane draws 3100–1100 with the
  Protopalatial palaces (c. 1900–1700) named in the note. **The Late Minoan end
  moves by about a century** depending on the Aegean chronology — radiocarbon puts
  the Thera eruption near 1600 BCE, Egyptian synchronism about a hundred years later
  — and that argument is not settled, so the bar is contested.

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
- **EVERY SPAN ON THE PANEL WAS DRAWN 1.3 px WIDE, from step 5 to 2026-11-26.** The
  drawing code took a span’s left edge from the RIGHT of its pair and its width from
  a subtraction that is negative for every span there is, so the minimum-width floor
  fired every time. It survived five steps and ninety checks because every span on the
  panel was short — Abram’s seventy-five years, Solomon’s eight — and at
  this zoom 1.3 px is roughly what a correct one would look like. The state lanes, where
  the Roman Republic is 482 years, showed it in one frame. **No check had asserted that
  a span’s width matched its own dates**; one does now.
- **The page's tick strip was up to 11.3 px out from its own scrubber thumb.** Fixed
  2026-11-25; the strip and the lanes now share one measurement.
