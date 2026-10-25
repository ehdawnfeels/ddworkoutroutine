# Handoff: Finalized weekly timeblock → Grind Log integration

**Goal:** add this finalized weekly timeblock to the workout schedule artifact (`gym-log.html`, "Grind Log · Forma Flow").

**Sources in this repo**
- `weekly-timeblock.html`: the finalized planner page. The schedule data is the `DAYS` array in its `<script>`.
- `weekly-timeblock-landscape.png`: rendered image of the same plan.
- Published planner: https://claude.ai/artifact/Xy9rcttXEgeqeDxWXYdi5D

## People and fixed facts

- Two profiles, matching the Grind Log: **Don** and **Dars**. They split the morning: one walks Dustin while the other showers, then they swap.
- **Dustin** is the dog. He gets walked twice a day.
- Office days are Mon, Tue, Wed and Thu, 8:00 AM–5:00 PM. The commute is 30 min there and 60 min back.
- **Friday:** work from home, 8:00 AM–5:00 PM.
- **Saturday and Sunday:** no work.
- Gym sessions are capped at **60 min**, the same as the Grind Log's session clock. The gym is 15 min from home each way.

## Rules (keep these consistent)

1. **Lifting days are Mon, Tue, Thu and Sat.** Wednesday is rest. Friday is optional easy cardio for Don and rest plus an optional dance class for Dars. Sunday is off. This matches the existing Grind Log `PROGRAMS`, so don't change the training days.
2. **Lights out is 8 hours before the next alarm.**
   - Before a 5:00 AM alarm, lights out is 9:00 PM, and **9:30 PM at the latest**. Do not use 10:00 PM, which gives only about 6.5 h of sleep.
   - Before a 6:00 AM alarm (Tue and Thu nights), lights out is 10:00 PM.
   - Before a 6:30 AM alarm (Fri and Sat nights), lights out is 10:30 PM.
3. **Weekend wake-up is no later than 7:00 AM.** That keeps it within about 90 min of the weekday 5:00 alarm.
4. **Dinner ends about 2 h before lights out.** Lunch for the next day is packed from a double batch cooked at dinner. No cooking in the morning.
5. **Every day has a protected "Free time" block.**

## Wake / lights-out summary

| Day | Wake | Gym | Lights out that night | Next alarm |
|---|---|---|---|---|
| Mon | 5:00 AM | 5:30–6:30 AM | 9:00 PM (9:30 latest) | Tue 5:00 |
| Tue | 5:00 AM | 5:30–6:30 AM | 10:00 PM | Wed 6:00 |
| Wed | 6:00 AM | Rest | 9:00 PM (9:30 latest) | Thu 5:00 |
| Thu | 5:00 AM | 5:30–6:30 AM | 10:00 PM | Fri 6:00 |
| Fri | 6:00 AM | Optional cardio / dance | 10:30 PM | Sat 6:30 |
| Sat | 6:30 AM | 8:45–9:45 AM | 10:30 PM | Sun 6:30 |
| Sun | by 6:30 AM | Off | 9:00 PM | Mon 5:00 |

## Blocks by day

Categories (used for colors): `move` (move/prep), `commute`, `work`, `home` (home/Dustin), `free`, `sleep` (wind down/sleep).

### Mon / Tue / Thu: gym + office

| Time | Block | Detail | Cat |
|---|---|---|---|
| 5:00–5:15 AM | Wake up | Water, small snack, clothes already laid out | move |
| 5:15–5:30 AM | Transit to gym | | commute |
| 5:30–6:30 AM | Gym session | Full 60 min: warm-up + that day's Grind Log workout | move |
| 6:30–6:45 AM | Transit home | | commute |
| 6:45–7:05 AM | Split: Dustin + shower | One walks Dustin, the other showers | home |
| 7:05–7:25 AM | Swap: shower + breakfast | Walker showers, the other plates breakfast | move |
| 7:25–7:30 AM | Leave buffer | Grab the packed lunch | move |
| 7:30–8:00 AM | Transit to work | | commute |
| 8:00 AM–5:00 PM | At work | Meal + short breaks | work |
| 5:00–6:00 PM | Transit home | Podcast or music. No work messages. | commute |
| 6:00–6:30 PM | Walk Dustin | First thing when you get home | home |
| 6:30–7:15 PM | Cook + eat dinner | Cook double and pack tomorrow's lunch | home |
| 7:15–7:30 PM | 10-min reset | Dishes, gym bag + clothes by the door | home |

**Evening, Monday:**

| Time | Block | Cat |
|---|---|---|
| 7:30–8:30 PM | Free time | free |
| 8:30–9:00 PM | Bedtime routine (screens off, lights low) | sleep |
| 9:00 PM | Lights out (9:30 latest) | sleep |

**Evening, Tuesday and Thursday** (a late night, because the next wake is 6:00):

| Time | Block | Cat |
|---|---|---|
| 7:30–9:30 PM | Free time | free |
| 9:30–10:00 PM | Bedtime routine | sleep |
| 10:00 PM | Lights out | sleep |

### Wednesday: rest + office

| Time | Block | Detail | Cat |
|---|---|---|---|
| 6:00–6:15 AM | Wake up | An extra hour of sleep | move |
| 6:15–6:50 AM | Long walk with Dustin | + 10 min mobility (the Grind Log's Wednesday rest-day items) | home |
| 6:50–7:25 AM | Shower + slow breakfast | | move |
| 7:25–7:30 AM | Leave buffer | | move |
| 7:30 AM–7:30 PM | Same as Mon from "Transit to work" through the "10-min reset" | | |
| 7:30–8:30 PM | Free time | | free |
| 8:30–9:00 PM | Bedtime routine | | sleep |
| 9:00 PM | Lights out (9:30 latest) | | sleep |

### Friday: work from home

| Time | Block | Detail | Cat |
|---|---|---|---|
| 6:00–6:15 AM | Wake up | | move |
| 6:15–6:45 AM | Brisk walk with Dustin | Counts as Don's optional Zone 2 cardio (20–30 min) | move |
| 6:45–7:30 AM | Shower + slow breakfast | | move |
| 7:30–8:00 AM | Free time | Coffee, or start a laundry load | free |
| 8:00 AM–5:00 PM | Work from home | Walk Dustin at lunch | work |
| 5:00–6:00 PM | Weekly reset | Laundry, tidying, grocery list | home |
| 6:00–7:00 PM | Dance class (Dars, optional) | Active rest. Light styles only (see notes). | move |
| 7:15–8:00 PM | Dinner | | home |
| 8:00–10:00 PM | Free time | | free |
| 10:00–10:30 PM | Bedtime routine | | sleep |
| 10:30 PM | Lights out | | sleep |

### Saturday: gym + weekend (no work)

| Time | Block | Detail | Cat |
|---|---|---|---|
| 6:30–7:00 AM | Wake up | Coffee, small snack | move |
| 7:00–7:45 AM | Long walk with Dustin | Together | home |
| 7:45–8:30 AM | Light breakfast | At least 1 h before lifting | home |
| 8:30–8:45 AM | Transit to gym | | commute |
| 8:45–9:45 AM | Gym session | Full 60 min: Don Lower B, Dars Glutes C | move |
| 9:45–10:00 AM | Transit home | | commute |
| 10:00–10:30 AM | Shower + post-gym meal | | move |
| 10:30 AM–5:00 PM | Free time | | free |
| 5:00–5:30 PM | Walk Dustin | | home |
| 5:30–7:30 PM | Dinner | At home or out | home |
| 7:30–10:00 PM | Free time | | free |
| 10:00–10:30 PM | Bedtime routine | | sleep |
| 10:30 PM | Lights out | | sleep |

### Sunday: off

| Time | Block | Detail | Cat |
|---|---|---|---|
| By 6:30 AM | Wake up | Keeps Monday's 5:00 manageable | move |
| Morning | Long walk with Dustin | Slow breakfast after | home |
| Midday | Free time | | free |
| 3:00–5:00 PM | Groceries + meal prep | Proteins and grains for the week | home |
| 5:00–8:30 PM | Free time | Easy dinner | free |
| 8:30–9:00 PM | Bedtime routine | | sleep |
| 9:00 PM | Lights out | | sleep |

## Notes to carry into the Grind Log

- **Friday dance (Dars):** pick light social styles such as salsa, bachata, swing or line dancing. Avoid barre and jump-heavy cardio dance. Saturday's Glutes C is Dars's highest-volume glute day, and the Grind Log already removed Friday HIIT for this reason. Moving the Saturday gym to 8:45 gives about 14 h between class and lifting.
- **If Saturday feels like too much,** cut Glutes C first. The Grind Log already says this.
- **If a 5:00 AM is rough,** skip the gym rather than cut sleep. Do the missed session on Friday instead of the easy cardio.
- **Dustin** is alone from about 7:30 AM to 6:00 PM on office days. Consider a midday walker once or twice a week.

## Integration suggestions

- **Don't duplicate the workout content.** In the timeblock, the gym block should link to or open that day's existing Grind Log session (`PROGRAMS[profile][day]`).
- **Add a "Today" timeline view** keyed off `new Date().getDay()`, using the day tables above. Highlight the current block, and show "Next: …" and time until lights out.
- **The schedule is shared** by both profiles. Only these blocks differ by profile:
  - Saturday's session name: Lower B for Don, Glutes C for Dars.
  - Friday 6:15 AM: Zone 2 for Don, optional for Dars.
  - Friday 6:00 PM: dance class, Dars only.
- **Match the Grind Log's existing themes** (Don dark, Dars light) and its 60-minute clock. Keep the six category colors as theme tokens.
- **Mobile-first layout**, the same as the Grind Log: one day at a time with day tabs, not the 7-column board.
