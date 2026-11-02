# Handoff: Don & Dars gym tracker ("Grind Log · Forma Flow")

Written 2026-11-02 for whoever continues this work, possibly in an offline environment. The user's latest request takes priority over anything here.

## 1. What this is

A single-file HTML workout tracker for a couple who train together at a commercial gym:

- **Don** (profile key `don`): dark theme (Bebas Neue, acid green). Goal: strength plus an aesthetic upper body during a recomp.
- **Dars** (profile key `dars`): light theme (Fraunces, rose). Goal: glute growth (upper glute, loaded abduction priority) plus overall tone, with upper body as a secondary goal.

They lift at the same time. Every gym session is planned on a shared 60-minute clock so they finish together.

## 2. Files (repo `ehdawnfeels/ddworkoutroutine`, branch `claude/sleepy-volta-57w6tn`)

| File | Status | Notes |
|---|---|---|
| `gym-log-mwfs-v2.html` | **Canonical, edit this one** | Mon/Wed/Fri/Sat schedule. Has everything below. |
| `gym-log-mwfs.html` | Superseded | Same as v2 before the optional extras, research section and calf swap. |
| `gym-log.html` | Superseded | Older Mon/Tue/Thu/Sat schedule. No calorie targets. |
| `HANDOFF.md` | This file | |

Published artifact links (claude.ai, online only):
- **Current:** https://claude.ai/artifact/8X7LHgeiHVo3m6TrvSYBMN (from `gym-log-mwfs-v2.html`)
- Older MWFS: https://claude.ai/artifact/3d3EqtQMFxRGA5wxebfWBp
- Original Mon/Tue/Thu/Sat: https://claude.ai/artifact/YLDAbSgJS8KP1XfUvynCi8

The v2 link was made because the user's phone kept showing a cached old version of the MWFS link. The server copy was current.

## 3. Running it offline

- Open `gym-log-mwfs-v2.html` directly in a browser. There's no build step and no framework.
- **Storage:** the page first renders from `localStorage` (key `ddgym_v3_<profile>`). It then tries `window.claude.use("db")`, the claude.ai shared database. Offline or outside claude.ai that returns nothing, so the page stays on localStorage. The footer then says "Saved on this device only". That's expected.
- **Fonts:** Google Fonts won't load offline. Fallback stacks are set (Impact, Georgia, system-ui, monospace), so the page still works but looks plainer.
- **Links:** Gear-page "How to use it" links (YouTube searches) and Research links need internet.

## 4. Code map (all in one `<script>`)

Grep identifiers rather than line numbers.

- `META`: header brand, subtitle and stat chips per profile.
- `PROGRAMS[profile][Mon..Sun]`: all workout content.
  - A day is `{abbr,name,label,tag,desc,type:"workout"|"rest",share,blocks}`. Rest days use `text` and `items` instead of blocks.
  - A block is `{kind:"straight"|"superset"|"finisher"|"bonus", optional?, label, rest, min, howto, ex:[]}`.
  - `min` is the block's planned minutes including rest. Rule of thumb: heavy set ≈ 3 min, accessory set ≈ 2 min, superset round ≈ 3.5 min, +1 min per station.
  - `optional:true` blocks (dashed "Optional ·" blocks) are excluded from `liftMinutes`, the progress bar and the core weekly-set counts.
  - An exercise is `{n, m:"load"|"reps", s:"3 × 8–12", mus, k, steps[], tip, cue?, main?}`. `main:true` puts it on the Progress tab. Set rows come from the leading number in `s`.
  - **Renaming an exercise orphans its history**, because the id is `exId(day, name)`.
- `WARMUP=5`, `FINISH=55`, `CAP=60`. `liftMinutes`, `optMinutes`, `liftEnd` and `clockHTML` drive the session clock (striped segment = optional extras).
- `CARDIO_OPTS`, `CARDIO_ORDER`, `CARDIO_PICK`, `CARDIO_WHY`, `cardioHTML`: the cardio block at the end of each gym day. `showerHTML` is the optional cold-shower step.
- `FUEL`, `fuelHTML`, `weekAvg`: daily calorie and macro card.
- `GYM_SLOT`, `WEEK`, `renderWeek`: the Week tab (shared daily timeblock, live Now/Next strip). `byProfile` overrides per-profile blocks.
- `GEAR`, `EX_GEAR`, `renderGear`: the Gear tab. **Every exercise name must map in `EX_GEAR`.**
- `REFS`, `refsHTML`: the "What the research says" section on the Plan tab.
- `TIERS`, `BW_KG`, `e1rm`: Progress tab estimated 1RM (Epley) and bodyweight-based strength levels for Don's squat and deadlift.
- Persistence: `load`, `persist`, `persistHistory`, `queueWrite` (one db write in flight per document). Current week's inputs reset each Monday (`weekOf`); history is kept.
- Tabs: Train, Progress, Plan, Gear, Week.

## 5. Validation (run before every handoff)

```bash
sed -n '/<script>/,/<\/script>/p' gym-log-mwfs-v2.html | sed '1d;$d' > /tmp/app.js && node --check /tmp/app.js && echo "JS OK"
```

Then click through, or use Playwright at 400 px width: switch profiles; open every day; log a set and tick it; check cardio; open Progress, Plan, Gear and Week. Check that there are no console errors and no horizontal scroll (`scrollWidth` = 400). Also check that every exercise maps to gear: `gearOf(ex)` should be truthy for all.

## 6. People and fixed facts

- **Don:** 64.5 kg, 163 cm, 30, male. About 8k steps a day. Deadlift PR 86 kg (190 lb). Does easy near-daily pull-up "greasing" sets.
- **Dars:** 50 kg, 155 cm, 31, female. About 8k steps a day. Some fat concentrated around her midsection.
- **Work:** office Mon–Thu 8–5 (commute 30 min there, 60 back). Work from home Friday. No work on weekends.
- **Gym:** 15 min from home. **No seated calf raise machine.** Gets crowded on Saturdays.
- **Home equipment:** one 25 lb kettlebell and resistance bands.
- **Dustin** is the dog, walked twice a day.
- **Units:** kg everywhere.
- **Shoes:** Converse (flat) for the whole session. The Pegasus running shoes are fine for machines and cardio, but not ideal for deadlifts.

## 7. Current program (MWFS)

Gym days are Mon, Wed, Fri, Sat; rest days are Tue, Thu, Sun.
- Mon and Wed: 5:00 wake, gym 5:30–6:30.
- Fri: gym 6:30–7:30 (work from home, no shower needed after).
- Sat: gym 8:45–9:45.

Each session runs: 5 min warm-up together → lifting → optional extras (7–8 min, taken from cardio first; going up to 15 min past the hour is OK) → easy cardio together until 0:55 → optional short cold rinse (30–90 s, never ice baths).

### Don (upper/lower)
- **Mon Upper A:** incline DB press 3×6–10; SS lat pulldown 3×8–12 + DB lateral raise 3×12–20; SS seated cable row 3×8–12 + hanging knee raise 3×10–15. *Optional:* cable fly 2×12–15 + overhead cable triceps extension 2×10–15.
- **Wed Lower A:** leg extension 2×12–15 (pre-exhaust, deliberately first); back squat 3×6–8; barbell RDL 3×6–10; tri-set leg curl 3×10–15 + standing calf raise 3×10–15 + cable Pallof press 3×10/side. *Optional:* cable lateral raise 2×12–15/side + incline DB curl 2×10–15.
- **Fri Upper B:** SS incline DB press 3×8–12 + pull-up (assisted) 3×6–10; SS pec deck 2×12–15 + chest-supported row 2×10–12; SS DB lateral raise 3×12–20 + cable face pull 2×12–15; SS triceps pressdown 2×10–15 + DB curl 2×10–15. *Optional:* reverse pec deck 2×15–20 + assisted dip 2×8–12.
- **Sat Lower B:** conventional deadlift 3×5 (~72–75 kg); SS seated leg curl 3×10–15 + cable crunch 3×10–15; leg press 3×10–12 (after Dars, from ~0:28); SS seated DB calf raise 3×12–15 + DB lateral raise 2×15–20. *Optional:* leg extension 2×12–15 + standing calf raise 2×10–15.
- **Rest days:** Tue rest and mobility; Thu optional Zone 2 (brisk 6:15 walk with Dustin); Sun easy movement.
- **Weekly effective sets** (indirect sets count half), core → with extras: chest 8→11, back ~11, side delts 8→10, rear delts ~4.5→6.5, triceps ~5→9, biceps ~7.5→9.5, quads 8→10, hamstrings ~10.5, calves 6→8, core 9.

### Dars (glute focus)
- **Mon Glutes A:** hip thrust 4×8–12; Bulgarian split squat 3×8–12/leg; hip abduction machine 3×12–20 (lean forward); cable kickback 2×12–15/side. *Optional:* cable lateral raise 2×12–15/side + face pull 2×12–15.
- **Wed Glutes B:** hip abduction 4×10–20 (first, as the main lift); barbell RDL 3×8–10; lying leg curl 3×10–15 (before Don's tri-set at ~0:34); 45° back extension (glute focus) 3×12–15. *Optional:* lat pulldown 2×10–12 + push-up 2×as many as possible.
- **Fri Upper:** SS lat pulldown 2×8–12 + machine chest press 2×8–12; SS seated row 2×10–12 + DB lateral raise 2×12–15; standing cable abduction 2×12–15/side + dead bug 2×8–10/side. *Optional:* triceps pressdown 2×12–15 + DB curl 2×12–15.
- **Sat Glutes C:** hip thrust 3×10–15; leg press feet high & wide 3×10–15 (~0:16–0:25); hip abduction 3×15–25; DB step-up 2×10–12/leg (cut first if Saturday is too much). *Optional:* cable crunch 2×12–15 + Pallof press 2×10/side.
- **Rest days:** Tue rest (dance fits better Thursday); Thu rest, with the optional dance class here (light social styles only, no barre or jump-heavy dance); Sun easy.
- **Weekly volume:** glutes are heavily covered (~24 direct sets plus secondary work). With extras, her upper body and core get 4–6 sets per muscle across two days.

## 8. Nutrition (in `FUEL`)

| | Gym days | Rest days | Weekly avg | Estimated burn |
|---|---|---|---|---|
| Don | 2,100 kcal · P115 C275 F60 | 1,875 · P115 C220 F60 | ~2,000 | ~2,145 (≈7% deficit) |
| Dars | 1,550 · P90 C195 F45 | 1,375 · P90 C150 F45 | ~1,475 | ~1,625 (≈9% deficit) |

- Burn estimates use Mifflin-St Jeor × 1.2, plus 8k steps, plus about 150–220 kcal per session.
- Protein is 0.8 g/lb for both (the user's rule; cost matters to them).
- Gym-day extra calories come from carbs.
- **Adjusting:** use weigh-ins (weekly averages) and Dars's waist at the navel every 2 weeks.
  - Don: aim to lose 0.1–0.25 kg a week.
  - Dars: aim to lose 0.1–0.2 kg a week. If hip thrust or abduction stalls for 2+ weeks, add 100–150 kcal.
  - Move Dars to maintenance (~1,625) once her midsection goal is reached.
- If she knows her current stable intake, it beats the formula. This was asked but not answered.

## 9. House rules

- Lights out 8 h before the next alarm (9:00 PM before a 5:00 alarm, 9:30 at the latest).
- **Missed session:** skip it and carry on with the next one. No Sunday make-ups. A one-day shift is OK: e.g. Wednesday's session done Thursday at 5:00, with Saturday trimmed and that day's calories swapped.
- Log a shifted session on its original day tab.
- Weeks 1–2: one set fewer per exercise with 3+ sets. Deload around week 7.
- Progression: most sets end 1–3 reps from failure. Add weight when all sets reach the top of the rep range.

## 10. Evidence notes (keep claims at this level)

- **Strong:** weekly volume dose-response (Schoenfeld 2017; Pelland 2024 is a preprint); similar growth from ~5–30 reps when sets are hard (Schoenfeld 2017 JSCR); protein plateau around 1.6 g/kg (Morton 2018; the cutoff is uncertain).
- **Moderate:** fractional set counting (Pelland 2024); closer to failure builds more muscle (Robinson 2024); overhead triceps beats pushdowns (Maeo, EJSS); incline curls favor the upper biceps vs preacher curls favor the lower (IJSM 2025); recomp is possible (Barakat 2020).
- **Limited:** leaning forward on abduction targets the upper glute (EMG only); cold water after lifting (Roberts 2015: ice baths only, not short showers).
- Never claim spot reduction, or that an exercise guarantees a "shelf" shape.

## 11. Open items (proposed, not applied; confirm with the user first)

1. **Day-balance audit** (the user's latest question; proposals made, awaiting a yes):
   - Move a chest fly from Friday to Monday as a core exercise, so both upper days are 17 sets. Monday's optional becomes overhead triceps + machine chest press.
   - Wednesday RDL to 3×8–10 with 2–3 reps left.
   - Make Saturday's quad exercise flexible (leg press, hack squat, Smith squat or goblet squat) for both, because the gym gets crowded.
2. **Abduction rep ranges** (proposed): Mon 3×12–20 (keep), Wed 4×10–15, Sat 3×15–20. The user agreed 4 sets is fine but never confirmed the ranges.
3. **Offline-write data loss:** if someone logs while "Saved on this device only" and the shared db already has data, the next synced load overwrites the local edits. Proposed fix: compare timestamps and keep the newer copy. Offered, not built.
4. Header weight and protein in the old `gym-log.html` are stale (65 kg / 110 g). Leave as is unless asked.

## 12. User preferences

- Wants things evidence-based, and wants weak evidence labelled as weak.
- Didn't want identical programs for the two of them. Shared equipment is fine; the programming differs.
- Prefers optional extras over making sessions longer. Up to 15 min over or less cardio is acceptable.
- Cost-conscious (protein).
- Make changes in the canonical file, verify (syntax plus a render check), then commit and push to the branch above.
