# Clickbaitiness Scoring Procedure (CBI + HTD)

*A blunt, reproducible way to grade headline screaminess and delay tactics. Use this to get the same numbers I do, without needing my winning personality.*

---

## 1) Purpose
Score how “clickbaity” a headline/clip is using:
- **CBI (Clickbait Index)**: 0–100 scale from language and structure signals.
- **HTD (Headline→Topic Delay)**: penalty/credit based on how long it takes to actually cover the headline’s topic.

Final score = **CBI_base + HTD_adjust**, clamped to **[0, 100]**.

---

## 2) Inputs Required
- **Headline** (or first headline-like line on the video/page)
- **Transcript** (auto or human; note timestamps if available)
- **Optional:** Video length (seconds). If missing, estimate from word count (≈160 wpm).

---

## 3) CBI Feature Set (Signals & Weights)

### A) “Bait” signals (add points)
1. **Hype/Hyperbole words** (shocking, bombshell, destroys, insane, obliterate, meltdown, brutal, savage, humiliating, explosive, devastating)  
   ➜ **+12** per occurrence per **10 words**, cap **3** occurrences.
2. **Doom/Threat framing** (crisis, collapse, catastrophic, doomed, apocalyptic, end of …)  
   ➜ **+8** per **10 words**, cap **2**.
3. **Ad hominem / Value judgment** (loser, sickly, vile, traitor, groomer, pedo, corrupt, evil)  
   ➜ **+8** per **10 words**, cap **2**.
4. **Curiosity gap / Vague promise** (“you won’t believe…”, “this changes everything”, vague *this/these/they* instead of the concrete subject)  
   ➜ **+10** binary + **+1** if vague pronouns replace the noun.
5. **Question headline** (“Is X dead?”, “Did Y just…?”)  
   ➜ **+6** binary.
6. **ALL‑CAPS shouting** (non‑acronyms)  
   ➜ **+6** scaled to % of ALL‑CAPS tokens (cap 10%).
7. **Punctuational drama** (!!!, ??, ?!, multiple emojis)  
   ➜ **+6**, cap **3** marks.
8. **Listicle/numbered promise** (“Top 7…”, “5 reasons…”)  
   ➜ **+4** binary.
9. **Temporal urgency** (breaking, now, today, this morning)  
   ➜ **+4**, cap **2**.
10. **CTA in headline** (must see, watch, subscribe, click, buy)  
   ➜ **+6**, cap **2**.
11. **Culture‑war bait** (woke, deep state, globalist, communist, Soros, etc.)  
   ➜ **+6**, cap **2**.
12. **Body/appearance bait** (frail, sickly, “looks unwell”)  
   ➜ **+3** binary.

### B) “Antidotes” (subtract points)
13. **Concrete sourcing** (names a reputable outlet, docket, case title/number)  
   ➜ **−8** each, cap **2**.
14. **Verifiable specifics** (dates, dollars w/ units, statutes: e.g., “Aug 30, 2025”, “$1.5–1.8B”, “IEEPA/§232”)  
   ➜ **−6** each, cap **2**.
15. **Neutral verbs** (says, reports, files, issues, announces)  
   ➜ **−3** binary.
16. **Cautionary qualifiers** (allegedly, reportedly, according to)  
   ➜ **−3** each, cap **2**.
17. **Non‑sensational terms** (panel, memorandum, ruling, budget estimate, transcript)  
   ➜ **−3** each, cap **2**.

**CBI_base = sum(adders) − sum(subtractors)** → then clamp later after HTD.

---

## 4) HTD: Headline→Topic Delay (adds/credits based on pacing)
**Goal:** Penalize videos that stall before addressing the headline’s topic; credit those that get to it fast.

- **T₁ (first mention):** time when the headline topic is clearly first referenced.
- **T₂ (first substantive explanation):** time when evidence/details appear (numbers, quotes, sources, concrete claim beyond vibes).
- **L:** total video length (seconds). If unknown, estimate L from transcript words / 160 wpm.
- **r₁ = T₁/L**, **r₂ = T₂/L**.

**HTD_adjust (added to CBI_base):**
- If **no T₂**: **+25** and flag as *“headline not supported.”*
- Else based on **r₂**:
  - **≤10% of runtime** or **≤30s** (whichever larger): **−10** (credit)
  - **10–25%:** **0**
  - **25–50%:** **+8**
  - **>50%:** **+15**

**Micro‑signals (optional):**
- ≥2 teaser loops (“after this…”) before T₂ → **+2** each, cap **+4**
- Off‑topic cold open >60s before T₁ → **+3**

**Final:** **CBI_total = clamp(0, CBI_base + HTD_adjust, 100)**

---

## 5) Scoring Bands
- **0–20**: Straight newsy
- **21–40**: Mild heat
- **41–60**: Clicky
- **61–80**: Spicy clickbait
- **81–100**: Caps‑lock carnival

---

## 6) Step‑by‑Step Procedure (Manual)
1. **Capture the headline.** Normalize (lowercase, strip punctuation except !!!/?? and caps tokens noted separately).
2. **Mark “bait” terms.** Count per the weights above (normalize counts per 10 words where noted).
3. **Mark “antidotes.”** Look for concrete sources, dates, statutes, neutral verbs, qualifiers.
4. **Compute CBI_base.** Add/subtract with caps/occurrence limits.
5. **Time the topic.** From the transcript/video, record **T₁** and **T₂**; get **L**.
6. **Compute HTD_adjust** using r₂ (and optional micro‑signals).
7. **Finalize CBI_total** (clamp 0–100). Keep **top 3 drivers** (e.g., “ad hom +8, urgency +4, concrete source −8”).
8. **Document.** Store headline, CBI_total, T₁/T₂/L, drivers, and a one‑liner *why*.

---

## 7) Worked Mini‑Examples
**A.** “BREAKING: Court SMACKS DOWN illegal tariffs!!!”  
- Hype +12, Drama +6, Urgency +4, Ad hom implied +8; Subtract: none → CBI_base ≈ 30.  
- Topic at 4:00 of 8:00 (r₂=0.5) → HTD +8 → **CBI_total ≈ 38** (mild‑clicky) *(real videos often score higher once all features counted).*

**B.** “Appeals court narrows Trump tariff authority in Aug. 30 ruling”  
- Antidotes (date −6, legal term −3, neutral verb −3) → CBI_base ≈ −12 → floor at 0.  
- Topic at 0:20 of 10:00 (≤30s) → HTD −10 → **CBI_total = 0** (news‑y).

---

## 8) Optional Automation (Pseudocode)
```pseudo
function score_cbi(headline, transcript, video_len=None):
  tokens = tokenize(headline)
  scores = 0
  scores += 12 * min(3, count_in_10w(tokens, HYPE))
  scores += 8  * min(2, count_in_10w(tokens, DOOM))
  ...
  scores -= 8  * min(2, has_concrete_sources(headline))
  scores -= 6  * min(2, count_specifics(headline))
  ...
  CBI_base = max(scores, 0)  // don’t clamp high yet

  (T1, T2, L) = locate_topic_times(transcript, video_len)
  r2 = T2/L if T2 else None
  HTD = +25 if not r2 else (-10 if r2<=max(0.1, 30/L) else 0 if r2<=0.25 else 8 if r2<=0.5 else 15)
  HTD += teaser_loops(transcript) * 2  // cap +4
  HTD += 3 if off_topic_cold_open(transcript)>60 else 0

  return clamp(CBI_base + HTD, 0, 100)
```

**Helper lexicons (seed sets):**
- `HYPE = {shocking, bombshell, insane, obliterate, destroy, meltdown, brutal, savage, humiliating, explosive, devastating}`
- `DOOM = {crisis, collapse, catastrophic, doomed, apocalyptic}`
- `CULTURE = {woke, deep state, globalist, communist, groomer, pedo, marxist}`
- `CTA = {must see, watch, subscribe, click, buy, join}`
- `URGENCY = {breaking, now, today, this morning}`

---

## 9) Tracker Schema (add these columns)
- `headline`, `cbi_total`, `cbi_drivers` (comma list), `video_length_sec`, `t1_first_mention_sec`, `t2_first_explained_sec`, `delay_ratio_r2`, `htd_score`

---

## 10) Reporting Snippet (drop into each write‑up)
**Clickbaitiness (CBI):** `NN/100` — *Band:* `…`
- **Top drivers:** `…`
- **Topic first mentioned:** `mm:ss` (`r₁%`)
- **First substantive explanation:** `mm:ss` (`r₂%`)  
- **HTD contribution:** `±N`  
- **Notes:** `teaser loops/off‑topic cold open if any`

---

## 11) QA Tips
- **Two‑pass check:** one person tags features, another verifies T₁/T₂; resolve deltas.
- **Keep examples:** Store 1–2 lines from the transcript where T₁/T₂ occur.
- **Version the lexicons:** If you expand HYPE/DOOM lists, date the change.

---

## 12) Ground Rules (because we’re adults)
- Don’t diagnose health from pixels. Mark as *appearance bait* and move on.
- Opinion ≠ fact. Headlines that assert without sources get dinged.
- Consistency beats dunking. Apply the same weights to everyone.

