# TrnX

A single-file progressive web app for tracking a structured 2-year body transformation. Built on the Nothing OS design language — dot matrix texture, monospace type, black background, red accent. No backend, no account, no cloud. Everything lives on your device.

---

## What it is

TrnX is a personal fitness OS, not a generic tracker. It's built around a fixed 8-phase, 24-month plan — from building a base at ~92 kg to hitting a lean, athletic peak. Each phase has its own calorie targets, macros, cardio goals, and expected body composition milestones. The app tracks your daily compliance across workouts, food, hydration, and body stats, and ties it all back to where you are in the plan.

---

## Pages

### Home
Your daily dashboard. Shows today's weight, streak, and calories eaten at a glance. Below that is a live energy balance card showing your TDEE (BMR + NEAT + workout burn) versus what you've eaten, so you always know if you're in deficit. A gym schedule section lets you set your gym time and counts down to it, with a pre-workout reminder that fires 45 minutes before (configurable). Hydration tracker at the bottom — 7 cups = 3.5L target, tap to fill.

### Workout
Six structured sessions across the week. Each session has a defined exercise list with planned sets, reps, and starting weights. Tap an exercise to expand it and log sets inline — enter weight, reps, and optional RIR (reps in reserve). The app estimates calories burned per set in real time. A progress bar tracks completion across the session. Tap "Start Session" to launch the active session overlay with a live timer, rest countdown between sets, and a session complete summary at the end showing total volume, sets, and kcal burned.

### Calories
A calorie ring showing today's intake vs. your phase target, with macro breakdown (protein, carbs, fat). Quick-add buttons for common foods (rice, eggs, chicken, dal, protein shake, banana, roti, yoghurt). Full food log below with per-item delete. TDEE breakdown card shows the components of your daily burn. Target is set per phase and updates automatically when you advance.

### Reports
Four time windows: Week, Month, Quarter, Year. Shows net calorie deficit for the period, key metrics (sessions completed, average daily calories, current weight, streak), a weight trend chart, per-exercise strength progress cards showing starting weight vs. current PR, and a body trends chart for waist measurements. Charts render with grid lines and a structured empty state when no data has been logged yet — they grow dynamically as you add entries.

### Profile
Log daily body stats (weight, waist, resting heart rate, sleep). Body metrics grid at the top updates with each log. Push-up tracker for daily reps. Settings for dark/light theme, notifications, and calorie targets. Plan phase management with the full phase selector sheet. 2-year roadmap showing all 8 phases with current phase highlighted. Year 1 progress bars for weight and waist. Current phase targets card. Milestone cards showing expected physique checkpoints.

---

## The 8-Phase Plan

| Phase | Period | Name | Weight Target | Calories |
|-------|--------|------|--------------|----------|
| 1 | Y1 M1–3 | Foundation | 84–88 kg | 2,200 kcal |
| 2 | Y1 M4–6 | Fat Loss | 79–83 kg | 2,000 kcal |
| 3 | Y1 M7–9 | Conditioning | 74–78 kg | 1,900 kcal |
| 4 | Y1 M10–12 | Peak Year 1 | 72–74 kg | 1,850 kcal |
| 5 | Y2 M13–15 | Recomp | 70–73 kg | 1,950 kcal |
| 6 | Y2 M16–18 | Strength | 69–71 kg | 2,050 kcal |
| 7 | Y2 M19–21 | Elite Lean | 68–70 kg | 1,950 kcal |
| 8 | Y2 M22–24 | Mastery | 68–70 kg | 2,000 kcal |

Phases are **not automatic** — you advance them manually. When you set a phase, the app records the date. After 90 days on any phase, a "Phase Up Available" banner appears on the Profile page with a one-tap advance button. You can dismiss it and stay on the current phase as long as you want. Calorie targets and macros update automatically when you advance.

---

## Tracked Exercises

The workout plan is built around Smith machine compound lifts, dumbbell accessories, and Zone 2 cardio:

**Monday / Push — Upper** — Smith Machine Bench Press, Smith Bent-Over Row, Incline DB Press, DB Shoulder Press (seated), Lateral Raises (DB), Tricep Pushdowns (Cable/DB)

**Wednesday / Pull — Lower** — Smith Machine Squat, Smith Machine RDL, Leg Press, Leg Curl, Calf Raise, Seated Cable Row

**Thursday / Cardio** — Brisk Walk / Jog (Zone 2, HR 119–139)

**Friday / Push — Hypertrophy** — Incline DB Press, Pec Deck Fly, Cable Lateral Raise, Face Pull, Smith Machine OHP, Skull Crushers

**Saturday / Pull — Strength** — Smith Machine RDL (Heavy), Bulgarian Split Squat, Leg Press (wide), Hip Thrust, Seated Leg Curl, optional cardio finisher

**Sunday / Arms + Shoulders** — DB Shoulder Press, Lateral Raises, Rear Delt Fly, DB Curl, Hammer Curl, Incline DB Curl, Smith Machine OHP, Tricep Bench Dips

**Tuesday** — Active Recovery (Light Home Walk, optional)

Strength progress for key lifts (Smith Machine Bench Press, Squat, RDL, DB Shoulder Press, Lateral Raises) is tracked in the Reports page with starting weight vs. current PR.

---

## Data & Storage

All data is stored in `localStorage` under the key `trnx2` as a single JSON object. Nothing is sent anywhere. The state object includes:

- `bodyLogs` — daily weight, waist, resting HR, sleep entries
- `calLog` — food entries per date
- `workoutLog` — logged sets per exercise per date
- `burnLog` — kcal burned per date
- `waterLog` — cups logged per date
- `exercisePR` — personal records per exercise (best weight × reps)
- `streak` / `streakLast` — daily consistency tracking
- `calTarget` — active calorie and macro targets
- `planPhase` — current phase ID (1–8)
- `phaseStartDate` — date the current phase was started (used for phase-up banner)
- `phaseBannerDismissed` — which phase's banner has been dismissed
- `gymTime` — set gym time for countdown and pre-workout alert
- `pushups` — daily push-up counter
- `theme` — light or dark

Clearing site data in your browser will reset the app completely.

---

## PWA Installation

TrnX is a PWA. It requires two companion files alongside `index.html`:

- `manifest.json` — app name, icons, display mode, theme colour
- `sw.js` — service worker for offline caching

With those in place, you can install it to your home screen from Chrome or Safari and it will run fullscreen with no browser chrome, behaving like a native app.

---

## Design System

Built on the Nothing OS aesthetic:

- **Fonts** — DM Mono (body), Space Mono (headings, labels, numbers)
- **Dot matrix background** — 12px radial gradient grid at 5.5% opacity
- **Colours** — `#0a0a0a` background, `#f0f0f0` text, `#ff0000` accent
- **Border radius** — 2px throughout (sharp, not rounded)
- **Dark/light** — full theme support via CSS custom properties, toggled in settings
- **Animations** — subtle: fadeUp on cards, burnPulse on live burn indicator, timerBeat on active sets

---

## File Structure

```
index.html      ← entire app (HTML + CSS + JS, self-contained)
manifest.json   ← PWA manifest (required for install)
sw.js           ← service worker (required for offline)
apple-touch-icon.png  ← home screen icon
```

The app is intentionally a single file. There are no build steps, no npm, no frameworks. Open it in a browser and it works.
