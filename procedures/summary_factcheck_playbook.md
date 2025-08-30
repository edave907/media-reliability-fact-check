# Summary & Fact‑Checking Procedure (Team Playbook)

*A crisp, reproducible workflow so anyone on the team can produce the same summaries and fact‑checks without summoning the oracle. Use this with the separate “Clickbaitiness Scoring Procedure (CBI + HTD)”.*

---

## 0) Ground Rules (read these, then tape them to your monitor)
- **No diagnosing from pixels.** If someone “looks unwell,” tag it as *appearance/health speculation* and move on.
- **Dates > vibes.** Always capture both **publish date** and **event date** (and note Alaska Time, if relevant).
- **Primary beats secondary.** Court orders > blogs. Agency memos > hot takes.
- **Opinion ≠ fact.** If it can’t be falsified, don’t “fact‑check” it—label it.
- **Symmetry matters.** Apply the same standard to every author, whether you love them, hate them, or barely tolerate them.

---

## 1) Intake & Metadata
Record these up front (top of your working doc or sheet):
- **Author/Presenter**
- **Affiliation/Platform** (e.g., MidasTouch, Lincoln Project, independent YouTube)
- **Title/Headline** (or first headline‑like line)
- **URL** (video/post)
- **Runtime** (mm:ss); **Transcript source** (auto/human)
- **Publish date/time**; **Event date(s)** mentioned
- **Context tags** (topic: tariffs, CDC, Ukraine, etc.)

---

## 2) Summary Procedure (what to write, and what not to)
1. **Skim once, then segment.** Split the transcript into logical chunks (topic changes, new claim clusters).
2. **Extract the spine.** For each chunk, note the *main claim* in one sentence.
3. **Flag speculation.** Mark lines that are conjecture or opinion (keep them in the summary, but label as such).
4. **Write the summary:**
   - 5–9 bullets, declarative and neutral.
   - Keep numbers and proper nouns; drop adjectives and snark.
   - Add a sub‑section **“What’s new”** (1–3 bullets) if applicable.
   - Add **“Speculation/Opinion”** (1–3 bullets) if the piece leans on it.
5. **Clickbaitiness block.** Insert the **CBI + HTD** snippet (see separate procedure) right after the summary and before the fact‑check.

**Summary Template**
```
## Summary
- [Bullet 1]
- [Bullet 2]
...

### What’s new
- [New item]

### Speculation / Opinion
- [Clearly label]

## Clickbaitiness (CBI)
CBI: NN/100 — Band: [news/mild/clicky/spicy/carnival]
Top drivers: [3 items]
Topic first mentioned: mm:ss (r1%)
First substantive explanation: mm:ss (r2%)
HTD contribution: ±N
Notes: [teasers/cold open if any]
```

---

## 3) Fact‑Checking Procedure (claim → verdict → evidence → citations)
### 3.1 Build a claim list
Classify each into one of:
- **Factual (verifiable)** – dates, numbers, events, rulings, quotes.
- **Attribution** – who said what, where (e.g., “NYT reported X”).
- **Legal/Regulatory** – court actions, statutes, agency memos.
- **Causal inference** – “X caused Y” claims.
- **Opinion/Interpretation** – cannot be falsified; label and skip scoring.

### 3.2 Prioritize
Triage high‑impact claims first: legal rulings, government actions, money figures, polls, foreign‑policy assertions, public‑health claims.

### 3.3 Verify (the loop)
For each **verifiable** claim:
1. **Formulate precise queries** (entity + action + time window). Prefer the subject’s official site first.
2. **Find ≥2 independent sources**; at least one should be **primary** when feasible:
   - **Primary:** statutes, court dockets/orders, agency memos, official press releases, company filings.
   - **Secondary (reputable):** AP, Reuters, WSJ/FT, WaPo/NYT, major local outlets.
   - **Social posts** only as primary statements, then corroborate.
3. **Cross‑check dates** (publish vs event). Note time zones if relevant.
4. **Quote minimally** (short phrases), and **paraphrase** with source links.
5. **Verdict taxonomy**:
   - **True** – supported by multiple reliable sources/primary docs.
   - **Mostly true** – accurate but missing nuance/limited scope.
   - **Mixed** – some parts right, some wrong/unsupported.
   - **Unverified** – claim made, no solid evidence yet.
   - **False** – contradicted by strong evidence.
   - **Opinion/Interpretation** – not subject to fact‑check; label.

### 3.4 Domain‑specific tips
- **Legal/Regulatory:** Pull the **actual order/memo**. Note case number, court, judge, decision date; quote holding/conclusion.
- **Economics/Business:** Use **BLS/BEA/FRED**, company 8‑K/10‑Q, earnings calls; be explicit about units and periods.
- **Public health:** Prefer **CDC/NIH/FDA** docs or physician notes; avoid “looks sick” assertions.
- **Polling:** Use reputable **aggregators**; capture *field dates, sample, LV/RV, MoE*.
- **Foreign affairs:** Check foreign ministry/PMO readouts and top international outlets (Reuters, BBC, AFP, Nikkei, Al Jazeera, etc.).

### 3.5 Write‑up Template
```
## Fact‑Check
**Claim:** [verbatim or tight paraphrase]
**Verdict:** True / Mostly true / Mixed / Unverified / False / Opinion
**Evidence:** [2–4 lines; what supports/refutes]
**Citations:** [1–3 links]

(repeat per claim; prioritize top 5–8)
```

---

## 4) References Section (how to cite)
- List **title, publisher, date (pub + event)**, and **URL**.
- Prefer **diverse outlets**; avoid echoing the same report across clones.
- Cap direct quotes at ~25 words per source.

**References Template**
```
## References
1. [Title] — [Publisher] — [Date]. URL
2. ...
```

---

## 5) Reliability Tracking (post‑check)
After the fact‑check, update the **Author Reliability Tracker**:
- **Reliability level:** High / Medium / Low–Medium / Low
- **Notes:** 2–4 bullets on accuracy patterns (e.g., “solid on legal docs; exaggerates costs”).
- **Running Notes:** append a dated bullet for the author.

---

## 6) QA Checklist (fast pass before you ship)
- [ ] Summary is neutral; speculation labeled.
- [ ] CBI + HTD block included with drivers and times.
- [ ] Top 5–8 claims each have verdict + 1–3 citations.
- [ ] Dates/time zones checked.
- [ ] At least one **primary** source where applicable.
- [ ] References show source diversity.

---

## 7) Optional: Tracker/CSV Fields (for data nerds)
- `author, outlet, headline, url, published_at, runtime_sec`
- `summary_text`
- `cbi_total, cbi_drivers, t1_sec, t2_sec, delay_ratio, htd_score`
- `claims_json` (array of {claim, verdict, sources[]})
- `reliability_level, reliability_notes`

---

## 8) Example (skeleton only)
```
## Summary
- Appeals court narrows authority for new global tariffs; order issued Aug 30, 2025.
- Host claims polling in “mid‑30s” and says CDC is in crisis.

## Clickbaitiness (CBI)
CBI: 46/100 — Clicky
Top drivers: ad‑hom phrase, urgency, concrete court mention (anti‑bait)
Topic first mentioned: 00:45 (7%)
First substantive explanation: 03:20 (28%)
HTD: +8

## Fact‑Check
Claim: Appeals court ruled most new tariffs illegal.
Verdict: Mostly true.
Evidence: Order limits authority under IEEPA; staying effect pending further action.
Citations: [Court order], [Reuters]
...

## References
1. Court order, Case No. XXXX — Aug 30, 2025 — URL
2. Reuters — “Appeals court …” — Aug 30, 2025 — URL
```

---

## 9) Tooling Tips (optional)
- **Transcripts:** YouTube auto‑captions → export; or use any ASR tool; keep timestamps.
- **Time math:** If no timestamps, estimate **~160 wpm** to place T₁/T₂.
- **Search syntax:** site:gov, site:sec.gov, site:courts.gov; use quotes for exact phrases; add date filters.

---

## 10) Last Word
Be boring on process, aggressive on evidence. Your future self (and your lawyer) will thank you.

