# Marrakech Tourist App (iOS + Android) — Expo React Native Plan (Offline-First + Convex Phase 2)

## 1) Product thesis

This is a **paid, offline-first "confidence companion"** for first-time tourists in Marrakech (Morocco).
It replaces the need for multiple apps (maps, blogs, phrasebooks, pricing guesses) with one trusted guide.

- Know **what to do today** (curated, not overwhelming) — plus a 1-tap **My Day plan** that fits your time/budget.
- Know **what things should cost** (MAD ranges + negotiation scripts)
- Avoid **common tourist traps**
- Act with **cultural confidence** (etiquette + do/don't)
- Reduce **language friction** (Darija glossary + optional audio)
- Works **offline** as the default mode

- Instantly sanity-check any quoted price in the moment (**Quote → Action**)
- Set a **Home Base** (riad/hotel) and get an offline compass back to it
- Follow itineraries with **Route Cards** (next stop, distance, time, offline-friendly)

### Target users & moments (personas)

- **First-time visitors (1–4 days)** who want a clear plan without endless research.
- **Families / groups** who need "safe defaults" (hours, fees, etiquette, kid-friendly).
- **Budget travelers** who care most about fair prices + negotiation confidence.
- **Anxiety-prone travelers** who want reassurance, scripts, and "what to do if…" flows.

### Jobs-to-be-done (JTBD)

- "I'm here today—give me a realistic plan for the next 6–10 hours."
- "I'm being quoted a price—help me respond confidently and fairly."
- "I have no internet—help me navigate, communicate, and avoid common traps."

### Product principles (keep decisions consistent)

- **Curation over completeness** (small set, high confidence).
- **Offline-first UX** (no dead-ends offline; online is additive).
- **Short, actionable writing** (checklists, scripts, ranges, red flags).
- **Trust cues everywhere** (review dates + clear "staleness" messaging).

### Success metrics (so you can evaluate v1)

- Activation: % of new users who view ≥1 Price Card + save ≥1 item in first session
- Activation: % who complete "offline ready" setup (downloaded recommended packs OR explicitly choose "download later")
- Reliability: % who pass **Offline Readiness Check** in onboarding (integrity OK + core flows usable offline)
- Support load: # of users who open Diagnostics/Offline Readiness (proxy for "something feels broken")
- Trust: % who view Privacy/Permissions explainer (and do not churn immediately after)
- Retention: % returning on day 2 / day 7 (tourists are short-lived—optimize for day 2)
- Helpfulness: "Was this useful?" ≥80% positive on Price Cards

**Not** a reviews app (TripAdvisor/Yelp).
**Not** a generic directory (Google Maps).
It's the "locals' practical guide" you can trust.

---

## 2) Monetization

**Recommended model: Option B — Free download + one-time unlock (with a meaningful offline preview)**

- Free offline preview pack that is genuinely useful (not a "toy demo"):
  - A small set of **high-impact Price Cards** (e.g., airport taxi + short taxi + 1–2 souk categories)
  - Quote → Action enabled for those categories
  - Arrival checklist + core "say no" phrases
  - A handful of curated places + 1 itinerary
- One-time purchase unlocks full Marrakech content + all offline features.
- Still: **no subscriptions, no ads, no accounts**.
- Target price: **$4.99–$9.99** (regional pricing enabled).
- Implementation cost is higher (IAP + restore), but conversion is typically stronger.

**Alternative (Option A — Paid up-front):**
- Keep as a launch fallback if you strongly prioritize implementation simplicity.
- Note: paid-up-front can reduce installs (especially for influencer-driven campaigns).

**Why these models work for this app:**
- Acquisition is influencer/IG/FB-driven (value is pre-sold before install).
- First-time tourists want reliability, not experiments.
- Competitive research shows backlash against subscriptions and restrictive free tiers.
- Free preview lets users experience the app's quality before committing; paywall appears only after they've tasted core value.

**What the app guarantees to the user:**
- Everything essential works offline after install/unlock.
- No surprise paywalls beyond the one-time unlock.
- No account required.
- No ads. No data selling.

**Optional add-ons (only if clearly optional, not required):**
- Audio Pack (spoken Darija phrases, mini guides)
- Extra regions / day trips pack

**Important rule:**
- The unlocked core Marrakech experience must feel complete without any add-ons.
- The preview pack must still deliver real offline value so users trust the unlock.

**Downloads screen:**
- Clear messaging on what's included vs optional packs (sizes, Wi‑Fi-only toggle).
- A simple **Downloads** screen (treat packs like a product surface):
  - Determinate progress (bytes + %) + per-pack state: queued → downloading → verifying → installing → ready (or failed)
  - Pause/resume/cancel + retry with clear error reasons (no ambiguous failures)
  - "Free space required" preflight + Wi‑Fi-only toggle + cellular confirmation for large packs
  - State persists across app restarts/process death so downloads reliably resume

---

## 3) Core features (what must ship)

### A) Explore places (landmarks, monuments, neighborhoods, shopping)

Curated entities with:

- Short description (skimmable)
- Neighborhood context (Medina, Gueliz, etc.)
- "Best time to go", time needed, entry fees (if applicable)
- Hours + **Open now** indicator (offline, when structured hours are available)
- **Expected cost range in MAD** + "last reviewed" date
- "Local tips" and "watch outs"
- **Not-a-tourist-trap cues (transparent):**
  - Badge: "Local pick" / "Mixed" / "Tourist-heavy"
  - Short explanation: "Why we recommend this" (1–3 bullets)
- Directions (open in Apple Maps / Google Maps)
- **Navigate (Medina-aware):**
  - If Offline Map Pack is installed: show offline walking route guidance
  - If not installed: explain and link to Downloads (never a blank map)
- Save / share (including a clean, screenshot-friendly "share card")
- **Related** (small, curated cross-links):
  - Relevant Price Cards (e.g., fees, taxi, nearby bargaining categories)
  - Useful Darija phrases (large-text driver mode when relevant)
  - Tips & safety items tied to this place (scams, etiquette, "watch outs")

### B) Eat (restaurants & cafés + what to order)

Curated list—not giant database.
For each place:

- Why it's worth it
- What to order / what to avoid
- Typical spend range (MAD) + last reviewed
- Hours + **Open now** indicator (offline, when structured hours are available)
- Tags: budget, rooftop, family-friendly, veg-friendly, etc.

### C) Prices & negotiation (the killer differentiator)

This is where the app earns its price.
Structured "Price Cards" for common tourist spend categories:

- Taxi fares (airport, short ride, night)
- Hammam (local vs tourist)
- Souk items (lanterns, spices, rugs, babouches, argan oil, etc.)
- Food & drinks (mint tea, tagine, fresh juice, pastries)
- Guides/tours/day trips
- SIM cards / eSIM guidance (high-level)

Each price card includes:

- **Expected MAD range** (with unit like *per ride / per person / per item*) + last reviewed
- **Related "Do this safely" links** (optional): curated places or safer alternatives when relevant
- **Provenance note** (how this range was derived) + optional seasonality tags
- **Confidence + volatility** indicator (helps users interpret how strict the range is, and triggers staleness warnings sooner for volatile categories)
- "What influences price"
- Negotiation scripts (simple phrases)
- "Red flags" + "what to do instead"
- Notes for different contexts (night / peak season)

#### Quote → Action (instant quote fairness check + what to say)

A fast tool for the exact high-stress moment tourists face: *"I was quoted X MAD—am I being overcharged, and what should I say?"*

**UX flow (works offline):**

1. User selects a category (Taxi / Hammam / Souk item / Guide / Food & drink / etc.)
2. The app suggests the most relevant **Price Card** (or user picks one)
3. User enters the quoted amount (MAD) (+ quantity if relevant, e.g., per person, per item, per km)
   - The UI always shows the unit to avoid apples-to-oranges comparisons.
4. Optional context toggles adjust the expected range (e.g., night, peak season, group size, distance tier)
5. Results screen shows:
   - **Fairness meter**: Low (confirm details) / Fair / High / Very High (with a confidence note)
   - **Expected range (adjusted)** + last reviewed + provenance
   - **Suggested counter-offer range** (polite + firm)
   - **Best 1–3 scripts** (Darija + English, + optional French for taxi/restaurant contexts)
   - If **Low**: "Confirm what's included" checklist + 1–2 clarification scripts
   - **If they won't budge**: "what to do instead" alternatives
   - **Compare quotes** (optional): keep 2–3 recent quotes for the same Price Card and show a quick comparison view

**Implementation details:**

- All logic is deterministic and on-device; no AI required.
- Add a small `pricingEngine` module:
- Inputs: `priceCard.expectedCostMAD`, `priceCard.unit`, `quoteMAD` (or `homeCurrencyAmount` + stored rate), optional `quantity`, selected `contextModifiers`
- Output: `{ adjustedRange, fairnessLevel, suggestedCounterRange, scripts, explanation, confidence }`
- Fairness heuristic (simple + explainable, tunable per card):
  - `Low` if `quoteMAD < adjustedMin * lowMultiplier` (default 0.75; override per card)
  - `Fair` if `quoteMAD <= adjustedMax`
  - `High` if `quoteMAD <= adjustedMax * highMultiplier`
  - `Very High` if `quoteMAD > adjustedMax * highMultiplier`
  - Where `highMultiplier` defaults to `1.25`, `lowMultiplier` defaults to `0.75`, but can be overridden per Price Card/category.
- Suggested counter range:
  - `counterMin = adjustedMin` (or slightly above in high-friction categories)
  - `counterMax = adjustedMax` (or `adjustedMax * 0.95`)
- Store the user's last 10 Quote → Action checks locally (recents) so they can quickly re-open.
- Extend PriceCard to include optional `lowMultiplier` and `inclusionsChecklist` (short bullets shown only when helpful)

**Data requirements:**

- Extend `PriceCard` to include optional `contextModifiers` (so you can adjust ranges without changing code), for example:
  - `id`: `"night"`, `"peak_season"`, `"group_3plus"`, `"airport_fixed_fare"`, etc.
  - `label`: shown in the UI
  - `factorMin/factorMax` or `addMin/addMax`: how the expected range changes
  - `notes`: optional explanation shown to the user

Implementation note: keep modifiers *small and explainable*—the goal is confidence, not false precision.

### D) Culture & etiquette (practical, short)

Skimmable, useful:

- Dress code suggestions (contexts)
- Tipping norms
- Photography etiquette
- Ramadan etiquette basics
- Mosques / religious spaces etiquette
- Friday customs
- Respectful behavior in souks

### E) Darija survival glossary (searchable; audio optional)

- Categories: greetings, taxi, directions, bargaining, food, emergencies
- Each phrase:
  - Darija in Arabic
  - Latin transliteration
  - English meaning
  - RTL display support (Arabic shown right-to-left; "show large text" mode for taxi drivers)
  - Optional audio playback
  - Optional: **"Used in" shortcuts** (links to relevant Price Cards / Tips / Arrival flows)
- Include **numbers** and bargaining essentials (very high utility)

### F) Itineraries (opinionated, day-by-day)

Examples:

- 1-day "first timer"
- 3-day "best of"
- Shopping day
- Food day
- Relaxed / family-friendly day

#### My Day (offline daily plan builder)

A lightweight planner that fulfills the core JTBD ("give me a realistic plan for the next 6–10 hours") without needing internet or AI.

**UX flow (offline):**
1. Pick your constraints: time available (2–10h), pace (relaxed/standard), budget (budget/mid/splurge), and interests (food, shopping, museums, gardens, hammam, etc.).
2. Choose a starting point:
   - Current location (optional, if permission granted)
   - Home Base (if set)
   - A neighborhood (manual selection)
3. The app builds a plan with 3–7 stops + suggested meal/drink breaks.
   - Avoids closed stops when structured hours are available
   - Prefers geographically coherent clusters (minimize backtracking)
   - Respects "best time to go" windows when provided (morning/afternoon/evening)
4. Tap "Start" to follow it via **Route Cards**. You can skip a stop and the plan reflows.

**Implementation approach:** deterministic `planEngine` using your curated content.
- Inputs: `availableMinutes`, `startPoint`, `interests[]`, `pace`, `budgetTier`
- Data: per-place `visitMinMinutes`/`visitMaxMinutes`, `bestTimeWindows`, structured hours (if present), tags, and optional `crowdLevel`/`kidFriendly` tags
- Travel-time model (offline): prefer a **precomputed travel-time matrix** (distance + ETA) between curated POIs (generated at build time)
  - Fallback: region clustering + tuned heuristics only when no matrix entry exists
- Output: ordered `Plan` (a list of place ids + time blocks) suitable for Route Cards

This keeps the promise of "what should I do today?" even for users who never open the itineraries list.

#### My Trip (offline 1/2/3-day builder)

- Choose 1, 2, or 3 days
- Auto-group by area (Medina/Gueliz/etc.) to keep days walkable
- Drag-reorder stops (manual override)
- Export/share a clean itinerary card (image)

Each step links to places already in the app.

#### Route Cards (execute itineraries without getting lost)

For each itinerary (and any generated plan later), provide a **Route Card** view that helps users *do the plan* with minimal friction.

**Route Card UX:**

- "Route overview" screen:
  - list of stops in order
  - estimated total time (sum of stop times + walking estimates)
  - "Start route" button
- "Next stop" screen (the core):
  - big stop name + quick facts
  - **compass arrow + distance** to the next stop (offline)
  - rough "walk time" estimate (offline heuristic)
  - **Navigate** (offline within pack areas; online handoff optional)
  - "Recenter" button (explicit; helps with GPS drift)
  - "GPS is weak here" hint state (calm guidance: keep walking 20m then re-check)
  - optional "Open in maps" button (online-only)
  - "Mark as done" → advances to next stop
- Optional: "route hints" for tricky legs (short text written by you)

**Medina Mode (fallback UX):**
- If GPS accuracy is poor or heading is unstable:
  - simplify UI (direction + distance + landmark hint text)
  - one-tap "Ask for directions" phrase card (large text)

**Implementation details:**

- Define **Routing Capability Levels** (to avoid "half-working" UX):
  - Level 0: compass + distance + landmark hint (always available)
  - Level 1: offline map display + user dot + bearing line (no routing)
  - Level 2: offline route polyline from precomputed legs (no turn-by-turn)
  - Level 3: optional future turn-by-turn via on-device routing graph (only if reliability is proven)
- Prefer **precomputed route legs** (polyline + distance + ETA) for:
  - itinerary steps
  - My Day generated steps
  - a curated set of "common legs" within the Medina
- On-device routing graph becomes optional (Phase 3/Level 3), not required for a reliable v1
- Cache per-leg results locally (routeId + stepIndex → polyline + distance + ETA) for stability and performance
- Fallback when routing is unavailable: Level 0 + short "Medina Mode" hint text + one-tap "Ask for directions" phrase card
- For each leg, compute straight-line distance with Haversine and estimate walk time with tuned speeds:
  - default: ~4.5 km/h (outside medina)
  - medina multiplier: slower (dense paths)
- Use the same heading/bearing helpers as Home Base compass to render the arrow.
- Persist route progress locally so the user can leave the app and come back:
  - `{ routeId, itineraryId, currentStepIndex, startedAt }`

**Data requirements:**

- Add optional fields to `Itinerary.steps`:
  - `estimatedStopMinutes?: number`
  - `routeHint?: string` (shown only in Route mode)

### G) Tips & safety (confidence builder)

- Common scams (henna, faux guides, "helpful" strangers, etc.)
- How to say "no" politely
- Cash/ATM basics
- Emergency numbers and what to do (high-level)
- "What to do if…" quick guides (lost phone, taxi issues, etc.)

### H) Arrival mode + quick tools (high perceived value)

An opinionated "first hours in Marrakech" flow that works fully offline:

- **Airport arrival checklist:** taxi expectations, typical fare ranges, polite refusal scripts
- **SIM / eSIM checklist:** what to ask for, what to avoid (high-level)
- **Cash / ATM checklist:** what to do if an ATM fails, small-bills reminder
- **Medina orientation tips:** "how to handle 'helpful' strangers", staying calm in crowds

Offline utility tools (simple, not gimmicky):

- **MAD ↔ home currency converter** (manual rate + last-updated timestamp)
- **Tipping quick guide** (common situations + ranges)
- **Bargaining calculator** (start price → target range; show "good deal / okay / too high")
- **Home Base compass** (set your riad/hotel; offline arrow + distance + taxi-driver card)

#### Home Base compass (offline "get me back")

Users set a single "Home Base" once (their riad/hotel). Then the app can always show:

- **Compass arrow** pointing to Home Base + distance (meters/km)
- Quick actions:
  - "Copy address / name"
  - "Show taxi driver" (large Arabic/Latin destination + simple phrase)
  - "Open directions" (online-only, optional)

**Implementation details (Expo React Native):**

- Store `homeBase` locally in `user.db` as `{ name, lat, lng, notes? }`.

**Location (expo-location):**
- Use `Location.getCurrentPositionAsync()` for initial fix when screen opens (shows "last updated" time)
- Use `Location.watchPositionAsync()` **only while compass screen is visible** (start in `useEffect`, remove subscription on unmount)
- Configure `accuracy: Location.Accuracy.High` for navigation; use `Location.Accuracy.Balanced` for general location
- Set appropriate `timeInterval` and `distanceInterval` values for offline-first behavior
- Add a safety timeout so location updates stop automatically after X minutes if the screen is left open (prevents silent battery drain)
- Provide a manual "Refresh location" button

**Compass heading (prefer fused heading):**
- Prefer `expo-location` heading updates (`watchHeadingAsync`) when available (more stable than raw magnetometer in dense urban environments like the Medina)
- Fallback to `expo-sensors` Magnetometer only if heading APIs are unavailable
- Subscribe **only while the compass/route screen is visible**; always clean up subscriptions on unmount
- Smooth heading with a simple low-pass filter to reduce jitter (don't "snap")
- Expose a "Heading confidence" + "Calibration needed" state with friendly guidance (e.g., "move your phone in a figure‑8")

**Compute (shared TypeScript logic):**
- `distanceMeters = haversine(current, homeBase)`
- `bearingDegrees = bearing(current, homeBase)`
- `relativeAngle = bearingDegrees - headingDegrees` (for rotating the arrow)

- Privacy: no backend, no background tracking; location used only on-device when the compass/route screens are open.

---

## 4) UX & navigation (simple, premium)

### First-run onboarding (60–90 seconds, skippable, re-runnable)

Goal: prevent offline dead-ends and build trust immediately.

1. Language + home currency
2. "Offline promise" screen:
   - What works offline (almost everything)
   - What needs internet (optional updates, optional downloads)
3. Pick offline downloads (district-based packs; sizes shown; Wi‑Fi-only toggle)
3b. **Offline Readiness Check** (fast local validation + "Test in Airplane Mode" checklist)
4. Quick demo entry: Quote → Action (Taxi example)
5. Privacy + Permissions explainer:
   - No accounts required
   - No ads / no data selling
   - Location is optional and only used on-device
   - Request location only when user taps Near Me / Go Home / Navigate
   - Request **foreground/"When in Use"** location only (never background location in v1)
   - Show a short pre-permission explanation so the system prompt is never surprising; denial path must keep the app usable

### Bottom tabs (recommended)

1. **Home**
2. **Explore**
3. **Eat**
4. **Prices**
5. **More** (Darija, Itineraries, Tips, Culture, Settings)

### Platform-native navigation rules (non-negotiable)

These rules prevent "it feels off" moments that undermine trust in a paid utility app.

**React Native (both platforms)**
- Use React Navigation with a bottom tab navigator (`@react-navigation/bottom-tabs`) for top-level navigation
- Use native stack navigator (`@react-navigation/native-stack`) for drill-down flows to get native push/pop animations
- Preserve interactive swipe-back gesture on iOS (enabled by default with native-stack)
- Use modals only for focused, temporary tasks (filters, pickers), not primary navigation
- Follow Back/Up principles: hardware back button on Android pops history; never exits the app unexpectedly
- Use `react-native-screens` for native screen management and better performance
- Test gesture navigation compatibility on both platforms

### Visual design language (Marrakech identity)

The app should feel unmistakably rooted in Marrakech while staying modern and readable. This design system is adapted from the web reference implementation at [marrakech-compass](https://github.com/osekkat/marrakech-compass).

#### Design Philosophy

- **Warm & Culturally Inspired:** The palette draws from Marrakech's iconic colors — terracotta walls, Majorelle blue gardens, and golden souks
- **Modern Minimalism with Moroccan Accents:** Clean UI patterns with cultural color cues
- **Professional yet Approachable:** Tourist app with local authenticity
- **Pattern as Texture:** Use Islamic geometric patterns as subtle background texture, never overwhelming content

---

#### Color System

**Primary Palette (Moroccan-inspired)**

| Token | HSL Value | Hex | Usage |
|-------|-----------|-----|-------|
| `terracotta` (Primary) | `hsl(14, 65%, 45%)` | `#BD5D3A` | Primary actions, active states, brand identity |
| `terracotta-light` | `hsl(14, 60%, 60%)` | `#D88066` | Hover states, lighter accents |
| `terracotta-dark` | `hsl(14, 70%, 35%)` | `#983D24` | Pressed states, emphasis |
| `majorelle` (Secondary) | `hsl(220, 75%, 45%)` | `#1D4ED8` | Secondary actions, informational elements |
| `majorelle-light` | `hsl(220, 70%, 60%)` | `#5B8DEF` | Hover states |
| `majorelle-dark` | `hsl(220, 80%, 35%)` | `#1E3A8A` | Pressed states |
| `gold` (Accent) | `hsl(40, 85%, 55%)` | `#E5A833` | Highlights, special callouts, icons |
| `gold-light` | `hsl(40, 80%, 70%)` | `#F0C56E` | Light accents |
| `gold-dark` | `hsl(40, 90%, 40%)` | `#C77D0A` | Strong accents |

**Semantic Colors**

| Token | HSL Value | Usage |
|-------|-----------|-------|
| `success` (Mint Green) | `hsl(158, 55%, 40%)` | Success states, "Great price" indicator |
| `warning` (Warm Amber) | `hsl(35, 90%, 50%)` | Warnings, "High price" indicator |
| `destructive` (Red) | `hsl(0, 70%, 50%)` | Errors, "Very high price" indicator |

**Background & Surface Colors (Light Mode)**

| Token | HSL Value | Usage |
|-------|-----------|-------|
| `background` | `hsl(35, 30%, 97%)` | Main app background (warm cream) |
| `card` | `hsl(35, 25%, 99%)` | Card surfaces (slightly warmer) |
| `muted` | `hsl(35, 20%, 92%)` | Muted backgrounds (warm sand) |
| `border` | `hsl(30, 20%, 88%)` | Subtle warm borders |
| `sand` | `hsl(35, 30%, 85%)` | Decorative sand tones |

**Dark Mode Colors**

| Token | HSL Value | Usage |
|-------|-----------|-------|
| `background` | `hsl(20, 25%, 8%)` | Dark background (warm, not cold) |
| `foreground` | `hsl(35, 20%, 95%)` | Light text on dark |
| `card` | `hsl(20, 25%, 12%)` | Dark card surfaces |
| `primary` | `hsl(14, 60%, 55%)` | Terracotta (slightly lighter) |
| `border` | `hsl(20, 20%, 20%)` | Subtle dark borders |

**Price Fairness Indicator Colors**

| Level | Background | Text | Border |
|-------|------------|------|--------|
| Low (Great Price) | `success/15%` | `success` | `success/30%` |
| Fair | `accent/15%` | `accent-foreground` | `accent/30%` |
| High | `warning/15%` | `warning-foreground` | `warning/30%` |
| Very High | `destructive/15%` | `destructive` | `destructive/30%` |

**Gradients**

```typescript
// src/shared/theme/gradients.ts
export const gradients = {
  sunset: ['hsl(14, 65%, 45%)', 'hsl(40, 85%, 55%)'], // Terracotta → Gold
  morocco: ['hsl(35, 30%, 97%)', 'hsl(35, 25%, 92%)'], // Cream → Sand
  blue: ['hsl(220, 75%, 45%)', 'hsl(220, 70%, 60%)'],  // Majorelle gradient
};
```

---

#### Typography

**Font Families**

| Purpose | Font | Weights | Usage |
|---------|------|---------|-------|
| Display/Headings | `Playfair Display` (serif) | 400, 500, 600, 700 | H1-H4, hero text, place names |
| Body/UI | `Inter` (sans-serif) | 300, 400, 500, 600, 700 | Body text, buttons, labels |

**Typography Scale (React Native)**

```typescript
// src/shared/theme/typography.ts
export const typography = {
  // Display (Playfair Display)
  displayLarge: { fontFamily: 'PlayfairDisplay-Bold', fontSize: 32, lineHeight: 40, letterSpacing: -0.5 },
  displayMedium: { fontFamily: 'PlayfairDisplay-SemiBold', fontSize: 28, lineHeight: 36, letterSpacing: -0.3 },
  displaySmall: { fontFamily: 'PlayfairDisplay-SemiBold', fontSize: 24, lineHeight: 32, letterSpacing: -0.2 },
  
  // Headings (Playfair Display)
  headlineLarge: { fontFamily: 'PlayfairDisplay-SemiBold', fontSize: 22, lineHeight: 28 },
  headlineMedium: { fontFamily: 'PlayfairDisplay-Medium', fontSize: 18, lineHeight: 24 },
  headlineSmall: { fontFamily: 'PlayfairDisplay-Medium', fontSize: 16, lineHeight: 22 },
  
  // Body (Inter)
  bodyLarge: { fontFamily: 'Inter-Regular', fontSize: 16, lineHeight: 24 },
  bodyMedium: { fontFamily: 'Inter-Regular', fontSize: 14, lineHeight: 20 },
  bodySmall: { fontFamily: 'Inter-Regular', fontSize: 12, lineHeight: 16 },
  
  // Labels (Inter)
  labelLarge: { fontFamily: 'Inter-Medium', fontSize: 14, lineHeight: 20 },
  labelMedium: { fontFamily: 'Inter-Medium', fontSize: 12, lineHeight: 16 },
  labelSmall: { fontFamily: 'Inter-Medium', fontSize: 11, lineHeight: 14 },
  
  // Buttons (Inter)
  button: { fontFamily: 'Inter-SemiBold', fontSize: 14, lineHeight: 20, letterSpacing: 0.1 },
  buttonSmall: { fontFamily: 'Inter-SemiBold', fontSize: 12, lineHeight: 16 },
};
```

---

#### Spacing & Layout

**Spacing Scale**

```typescript
// src/shared/theme/spacing.ts
export const spacing = {
  xs: 4,
  sm: 8,
  md: 12,
  lg: 16,
  xl: 24,
  '2xl': 32,
  '3xl': 48,
  '4xl': 64,
};

export const layout = {
  containerPadding: 16,          // Standard screen padding
  cardPadding: 16,               // Card internal padding
  sectionGap: 24,                // Gap between major sections
  itemGap: 12,                   // Gap between list items
  touchTarget: 44,               // Minimum touch target (iOS standard)
  touchTargetAndroid: 48,        // Minimum touch target (Android standard)
  borderRadius: 12,              // Standard corner radius (0.75rem)
  borderRadiusSmall: 8,          // Smaller elements
  borderRadiusFull: 9999,        // Pills/chips
  tabBarHeight: 80,              // Bottom tab bar height (with safe area)
};
```

**Shadows**

```typescript
// src/shared/theme/shadows.ts (React Native)
import { Platform } from 'react-native';

export const shadows = {
  soft: Platform.select({
    ios: {
      shadowColor: 'hsl(20, 25%, 15%)',
      shadowOffset: { width: 0, height: 2 },
      shadowOpacity: 0.08,
      shadowRadius: 4,
    },
    android: { elevation: 2 },
  }),
  
  card: Platform.select({
    ios: {
      shadowColor: 'hsl(20, 25%, 15%)',
      shadowOffset: { width: 0, height: 4 },
      shadowOpacity: 0.1,
      shadowRadius: 8,
    },
    android: { elevation: 4 },
  }),
  
  elevated: Platform.select({
    ios: {
      shadowColor: 'hsl(20, 25%, 15%)',
      shadowOffset: { width: 0, height: 8 },
      shadowOpacity: 0.15,
      shadowRadius: 16,
    },
    android: { elevation: 8 },
  }),
  
  tabBar: Platform.select({
    ios: {
      shadowColor: 'hsl(20, 25%, 15%)',
      shadowOffset: { width: 0, height: -4 },
      shadowOpacity: 0.08,
      shadowRadius: 10,
    },
    android: { elevation: 8 },
  }),
};
```

---

#### Component Styling Patterns

**Buttons**

| Variant | Background | Text | Border | Usage |
|---------|------------|------|--------|-------|
| `default` | `terracotta` | white | none | Primary CTAs |
| `secondary` | `majorelle` | white | none | Secondary actions |
| `outline` | transparent | `terracotta` | `terracotta` | Tertiary actions |
| `ghost` | transparent | foreground | none | Subtle actions |
| `destructive` | `destructive` | white | none | Delete/cancel |

| Size | Height | Padding | Font |
|------|--------|---------|------|
| `sm` | 36 | 12h × 8v | buttonSmall |
| `default` | 44 | 16h × 10v | button |
| `lg` | 52 | 24h × 14v | button |
| `icon` | 44 × 44 | centered | — |

```typescript
// Button style example
const buttonStyles = {
  default: {
    backgroundColor: colors.terracotta,
    borderRadius: layout.borderRadius,
    paddingHorizontal: 16,
    paddingVertical: 10,
    minHeight: layout.touchTarget,
  },
  pressed: {
    opacity: 0.9,
    transform: [{ scale: 0.98 }],
  },
};
```

**Cards**

```typescript
// Card variants
const cardStyles = {
  // Standard card
  base: {
    backgroundColor: colors.card,
    borderRadius: layout.borderRadius,
    borderWidth: 1,
    borderColor: colors.border,
    ...shadows.card,
  },
  
  // Interactive card (places, prices)
  action: {
    // On press: add border highlight
    pressedBorderColor: `${colors.terracotta}33`, // 20% opacity
    pressedScale: 0.98,
  },
  
  // Glass effect card
  glass: {
    backgroundColor: `${colors.card}CC`, // 80% opacity
    // Note: backdrop blur requires react-native-blur or similar
    borderWidth: 1,
    borderColor: `${colors.border}80`, // 50% opacity
  },
  
  // Elevated card
  elevated: {
    ...shadows.elevated,
  },
};
```

**Badges/Chips**

```typescript
const chipStyles = {
  base: {
    borderRadius: layout.borderRadiusFull,
    paddingHorizontal: 10,
    paddingVertical: 4,
  },
  
  variants: {
    primary: { backgroundColor: `${colors.terracotta}1A`, color: colors.terracotta }, // 10% bg
    secondary: { backgroundColor: `${colors.majorelle}1A`, color: colors.majorelle },
    success: { backgroundColor: `${colors.success}1A`, color: colors.success },
    muted: { backgroundColor: colors.muted, color: colors.mutedForeground },
  },
  
  // "Open now" chip
  openNow: { backgroundColor: `${colors.success}1A`, color: colors.success },
  
  // Price range chip
  priceRange: { backgroundColor: `${colors.gold}1A`, color: colors.goldDark },
};
```

**Bottom Tab Bar**

```typescript
const tabBarStyles = {
  container: {
    backgroundColor: colors.card,
    borderTopWidth: 1,
    borderTopColor: colors.border,
    ...shadows.tabBar,
    // Add safe area padding at bottom
  },
  
  tab: {
    active: { color: colors.terracotta },
    inactive: { color: colors.mutedForeground },
  },
  
  indicator: {
    backgroundColor: colors.terracotta,
    height: 3,
    borderRadius: 1.5,
  },
};
```

---

#### Moroccan Pattern Overlay

Use a subtle Moroccan geometric pattern as background texture for:
- Onboarding screens
- Empty states
- Section headers
- Share cards

```typescript
// Pattern usage (as SVG background or image)
const moroccanPattern = {
  // SVG pattern at 5% opacity over terracotta
  opacity: 0.05,
  color: colors.terracotta,
  
  // Apply to:
  // - Full-screen backgrounds (onboarding)
  // - Card headers (decorative)
  // - Loading skeletons
  // - Share card backgrounds
};
```

---

#### Animations & Transitions

**Keyframe Animations**

```typescript
// Using react-native-reanimated
const animations = {
  fadeIn: {
    from: { opacity: 0, translateY: 8 },
    to: { opacity: 1, translateY: 0 },
    duration: 300,
    easing: Easing.out(Easing.ease),
  },
  
  slideUp: {
    from: { translateY: '100%' },
    to: { translateY: 0 },
    duration: 300,
    easing: Easing.out(Easing.ease),
  },
  
  scaleIn: {
    from: { scale: 0.95, opacity: 0 },
    to: { scale: 1, opacity: 1 },
    duration: 200,
    easing: Easing.out(Easing.ease),
  },
  
  pulseSoft: {
    // For loading states
    keyframes: [1, 0.7, 1],
    duration: 2000,
    loop: true,
  },
};
```

**Transition Defaults**

```typescript
const transitions = {
  fast: 150,      // Button press, hover
  normal: 200,    // Color changes, small movements
  slow: 300,      // Page transitions, modals
  spring: { damping: 15, stiffness: 150 }, // Bouncy interactions
};
```

---

#### Accessibility

- **Touch Targets:** Minimum 44×44pt (iOS) / 48×48dp (Android)
- **Contrast:** All text meets WCAG AA contrast requirements
- **Pattern Usage:** Never place patterns behind body text; patterns are decorative only
- **Dark Mode:** Maintains warm tones (not cold blue/purple themes)
- **Dynamic Type:** Support iOS Dynamic Type and Android font scaling
- **Focus Order:** Logical focus order for VoiceOver/TalkBack

---

#### Design Tokens Summary (Theme File)

```typescript
// src/shared/theme/index.ts
export const theme = {
  colors: {
    // Primary
    primary: 'hsl(14, 65%, 45%)',
    primaryLight: 'hsl(14, 60%, 60%)',
    primaryDark: 'hsl(14, 70%, 35%)',
    
    // Secondary
    secondary: 'hsl(220, 75%, 45%)',
    secondaryLight: 'hsl(220, 70%, 60%)',
    secondaryDark: 'hsl(220, 80%, 35%)',
    
    // Accent
    accent: 'hsl(40, 85%, 55%)',
    accentLight: 'hsl(40, 80%, 70%)',
    accentDark: 'hsl(40, 90%, 40%)',
    
    // Semantic
    success: 'hsl(158, 55%, 40%)',
    warning: 'hsl(35, 90%, 50%)',
    destructive: 'hsl(0, 70%, 50%)',
    
    // Surfaces
    background: 'hsl(35, 30%, 97%)',
    card: 'hsl(35, 25%, 99%)',
    muted: 'hsl(35, 20%, 92%)',
    border: 'hsl(30, 20%, 88%)',
    
    // Text
    foreground: 'hsl(20, 25%, 10%)',
    mutedForeground: 'hsl(20, 15%, 45%)',
  },
  
  // ... spacing, typography, shadows from above
};

// Dark mode overrides
export const darkTheme = {
  colors: {
    ...theme.colors,
    background: 'hsl(20, 25%, 8%)',
    foreground: 'hsl(35, 20%, 95%)',
    card: 'hsl(20, 25%, 12%)',
    primary: 'hsl(14, 60%, 55%)',
    border: 'hsl(20, 20%, 20%)',
    muted: 'hsl(20, 20%, 15%)',
    mutedForeground: 'hsl(35, 15%, 60%)',
  },
};
```

---

#### Implementation Notes

- Use **Islamic geometric patterns** as a recurring motif in surfaces and separators (cards, section headers, onboarding backgrounds, loading/skeleton states, share cards).
- Keep patterns subtle and low-contrast behind content so legibility always wins over decoration.
- Build a color system anchored in **Marrakech terracotta tones** (warm clay/earth palette), supported by neutrals and a small number of accent colors for status/action states.
- Prefer warm terracotta gradients/tints for empty states, onboarding atmosphere, and hero surfaces; avoid cold/default generic palettes.
- Define these choices as design tokens on both platforms (color, spacing, corner radius, pattern opacity) so iOS and Android remain visually consistent.
- Respect accessibility with this style: maintain contrast targets, avoid pattern noise behind body text, and ensure dark mode keeps the same identity (warm earthy base, not generic blue/purple dark themes).

### Home (paid-app feel)

- "What do you need right now?" quick actions:
  - Taxi prices
  - **My Day** (build a realistic plan for the next 6–10 hours)
  - **Quote → Action** (check a quoted price)
  - Souk bargaining
  - Arrival mode
  - **Go Home** (Home Base compass)
  - Currency converter
  - Must-see landmarks
  - Phrasebook
  - Continue route (shown only if an active Route Card is running)
- **My Day** plan builder (constraints → generated plan → Route Cards)
- **Today's Tip** (rotating)
- **Phrase of the Day**
- Optional: Weather (online-only, cached; hide gracefully offline)
- "Saved" + "Recently viewed"

### Key UX mechanics (small but high impact)

- Map/List toggle in Explore
- Fast global search across places + prices + phrases + tips
- Map screen includes a clear search bar + "Navigate to…" entrypoint (avoid "I can't find directions" confusion)
- Deep links: shared items open directly to the correct Place/PriceCard screen
- One-tap entrypoints for high-stress moments (Quote → Action, Go Home)
- "Active route" banner when following a Route Card
- Favorites + recents
- "Quick fact chips" on detail screens (hours, fee, time needed, neighborhood)
- "Open now" chips + filter (uses structured hours; falls back gracefully)
- Clear offline state UX ("No internet? Core guide still works.")
- Language support: **localized UI** (EN/FR/ES/DE/IT/NL first; Arabic UI later) + locale-aware dates/numbers/currency formatting
- RTL readiness: ensure Arabic text renders correctly (alignment, numerals, shaping) in phrasebook + taxi-driver cards
- Dark mode
- Accessibility: dynamic type, contrast, touch targets (iOS hit targets ≥44×44 pt; Android hit targets ≥48×48 dp) + correct focus order for VoiceOver/TalkBack

#### Loading, progress, and error UX (standardized)

Every screen must follow the same state model so the app never feels "stuck" or inconsistent:

- `loading` → show skeleton/placeholder content (no blank screens)
- `content` → normal state
- `refreshing` → keep content visible; show subtle progress
- `offline` → show cached content + clear "what still works" message
- `error` → explain what failed + provide a next action (Retry / Downloads / Work offline)

Progress indicator rules:
- Prefer **determinate** progress for downloads/imports (bytes + % + pause/resume/cancel).
- Use **indeterminate** spinners only for short unknown-duration work; if >10s, show recovery actions.

---

## 5) Content strategy (this is the product)

Your advantage is **trusted curation + pricing confidence**.
You are not competing on "more listings". You are competing on:

- clearer advice
- more practical info
- better structure
- offline usability
- pricing + scripts + "watch outs"

### Content scope for a strong v1

- 20–40 places (high-quality, well-written)
- 15–25 price cards (high-impact categories)
- 50–150 Darija phrases
- 5–10 itineraries
- Culture/tips: concise but complete essentials

### Localization strategy (keep it manageable)

- v1 recommendation: ship **English content** + **localized UI** (EN/FR/ES/DE/IT/NL).
- Add French/Spanish/German/Italian/Dutch content as v1.x content updates once the editorial pipeline is stable.
- Always keep a safe fallback: if a translation is missing, show English rather than blanks.

### Content operations (treat content like releases)

Minimum pipeline (even if manual at first):

- Single source of truth (repo or lightweight CMS export)
- `shared/content/` is the canonical source for most product data (places, prices, phrases, itineraries, culture, tips)
- Schema validation (TypeScript + runtime validation via Zod/JSON Schema) before shipping bundles
  - enforce invariants: unique ids, valid coordinates, price min<=max, required `updatedAt`, no missing referenced ids
- Reference validation:
  - itinerary steps reference valid place/price ids
  - internal links are not broken
- Integration requirement (must pass every content release):
  - build `content.db` from `shared/content/`
  - bundle that DB into both apps (`ios/.../Resources/SeedData/content.db` and `android/.../assets/seed/content.db`)
  - verify repositories/screens on iOS + Android render the updated content correctly
- Editorial checks:
  - every price card has updatedAt + provenance note
  - every place has `reviewedAt` (and `hours.verifiedAt` if hours are present)
  - places with hours include `hours.verifiedAt` (so you can show "hours last checked" and staleness messaging)
  - staleness warnings appear when appropriate
- Generate a small **content changelog** per release (used for "What's new" in-app + store update notes)
- Asset budgeting:
  - image compression + size caps
  - audio pack size displayed before download

### Trust UI for prices + places

- Every price range shows:
  - "Last reviewed: YYYY-MM-DD"
  - Optional warning if old (e.g., > 6 months):
    - "Prices may have changed"

- Standardize staleness + confidence rules via a single **TrustEngine**:
  - Inputs: `verifiedAt/updatedAt`, `fieldType` (hours/fees/price), `volatility`, `confidence`, optional `staleAfterDays`
  - Output: `{ freshnessLevel, badgeLabel, warningCopy, showCTA }`
  - Unit-test these rules (avoids regressions that undermine trust)
  - Single source of truth for staleness thresholds across Places, Prices, Quote→Action, Tips

- Every place detail shows (field-level trust):
  - "Verified: YYYY-MM-DD" (editor check)
  - Hours verified date (if structured hours)
  - Fees verified date (if fees shown)
  - Staleness warnings based on per-field TTL (hours usually stricter than descriptions)
  - Place status: Open / Temporarily closed / Permanently closed (with note if applicable)

Add 2 lightweight credibility boosters:

- **Provenance note** (1 short line): "based on recent quotes in 2026-01" / "posted fare" / "local hammam vs tourist hammam"
- **Report outdated info**: simple button ("Was this accurate?" yes/no) with optional note.
  - v1: store locally in an offline "feedback outbox"
    - quick reasons: closed/moved/hours wrong/price wrong/tourist-trap/other
  - phase 2: upload outbox when online (no account required)

---

## 6) Technical stack (mobile)

### Why Expo React Native?

This app is built with **Expo React Native** (using `expo-dev-client` for development builds) for these reasons:

1. **Single codebase** — One TypeScript codebase for both iOS and Android. Faster iteration, consistent behavior, and lower maintenance burden for a small team.

2. **Expo ecosystem** — Expo provides well-maintained, consistent APIs for all app needs: location, sensors, file system, SQLite, and more. Libraries are tested together and versioned for compatibility.

3. **Development builds with native access** — Using `expo-dev-client` gives full native module access while retaining Expo's developer experience (fast refresh, easy debugging, EAS Build).

4. **Premium feel is achievable** — With `react-native-screens`, native stack navigators, and careful attention to performance, Expo apps can feel as polished as native apps. Many successful paid apps use Expo.

5. **Shared business logic** — All engines (pricing, planning, routing, geo) are written once in TypeScript and work identically on both platforms.

6. **Faster development** — Hot reload, single codebase, and Expo's tooling mean faster feature development and bug fixes.

7. **Simplified builds** — EAS Build handles iOS and Android builds in the cloud, reducing local toolchain complexity.

**Tradeoffs acknowledged:**
- Development builds required for native modules (can't use Expo Go for full feature set)
- Some third-party libraries may need config plugins
- Performance-critical views may need optimization (compass animation, map rendering)

### Expo platform requirements

**Expo SDK:** 52+ (latest stable)

**iOS**
- Minimum deployment: iOS 14.0 (Expo SDK 52 default)
- **Build toolchain:** Xcode 15+ (handled by EAS Build for cloud builds)

**Android**
- Minimum SDK: 26 (Android 8.0)
- **Target SDK:** align with Google Play policy deadlines (e.g., API 34+ for submissions as required)

### Core architecture

**Architecture pattern:**
- **Feature-based folder structure** with clean separation
- **Repository pattern** for data access
- **React Context + hooks** for dependency injection (DB/services only)
- Use a small global state store with selectors for high-churn UI state (downloads, active route, offline readiness)
- **Unidirectional data flow** (state flows down, actions flow up)

**Architecture enforcement (paid-app reliability):**
- Add lint rules to prevent cross-feature imports (enforce boundaries)
- Keep engines pure (no Expo imports) so they are unit-testable

### Expo React Native stack

**Navigation:**
- `@react-navigation/native` + `@react-navigation/native-stack` for native-feeling navigation
- `@react-navigation/bottom-tabs` for tab navigator
- `react-native-screens` for native screen management
- `react-native-safe-area-context` for safe area handling

**Localization:**
- `react-i18next` + `i18next` for UI localization (EN/FR)
- `expo-localization` for device locale detection

**Maps:**
- `react-native-maps` for online map display (works with expo-dev-client)
- Offline map packs: `@maplibre/maplibre-react-native` with MBTiles/vector tiles (requires expo-dev-client)
- Offline routing (Medina core): on-device routing using a bundled walking graph inside the pack

**Location & Sensors:**
- `expo-location` for GPS (foreground location only)
- `expo-sensors` for magnetometer/compass heading

**Sharing:**
- `expo-sharing` for native share sheets

**Image rendering:**
- `react-native-view-shot` for share card screenshots (compatible with Expo)
- `expo-image` for optimized image loading and caching

**Database:**
- `expo-sqlite` for SQLite with FTS5 support (Expo SDK 50+ has full FTS5)
- Same two-DB architecture: `content.db` (read-only) + `user.db` (user state)

**Networking:**
- Native `fetch` for HTTP requests
- `expo-file-system` `createDownloadResumable()` for resumable background downloads

**Storage:**
- `expo-file-system` for file system access and atomic operations
- `@react-native-async-storage/async-storage` for small settings only
- `expo-asset` for bundling seed content

**Network State:**
- Use `@react-native-community/netinfo` for reliable network state + subscriptions (Wi‑Fi-only gating)
- Optionally keep `expo-network` for one-off "what's my current state" checks

**IAP:**
- Required if Option B (one-time unlock):
  - Use `react-native-iap` or `expo-in-app-purchases` for iOS/Android IAP
  - Implement **restore purchases** and resilient local "unlocked" state
  - Keep gating logic content-driven (preview pack vs unlocked packs) so it's easy to tune
- Not required if Option A (paid up-front)

**UI Components:**
- Custom components following platform conventions
- `react-native-reanimated` for smooth animations (compass arrow, transitions)
- `react-native-gesture-handler` for gesture support
- `@shopify/flash-list` for high-performance lists (Explore/Eat/Prices)

### Expo library mapping

| Vanilla React Native | Expo Equivalent | Notes |
|---------------------|-----------------|-------|
| `react-native-geolocation-service` | `expo-location` | Better Expo integration |
| `react-native-sensors` | `expo-sensors` | Magnetometer for compass |
| `react-native-sqlite-storage` | `expo-sqlite` | Full FTS5 support in SDK 50+ |
| `react-native-fs` | `expo-file-system` | File operations, atomic moves |
| `react-native-background-downloader` | `expo-file-system` | `createDownloadResumable()` |
| `@react-native-community/netinfo` | `@react-native-community/netinfo` (preferred) or `expo-network` | Network state detection |
| `react-native-localize` | `expo-localization` | Device locale detection |
| `react-native-share` | `expo-sharing` | Native share sheets |
| `react-native-fast-image` | `expo-image` | Better caching, modern API |
| `react-native-iap` | `react-native-iap` or `expo-in-app-purchases` | Required for Option B (one-time unlock) |

### State & data

Expo React Native uses the same data architecture on both platforms:

- **Two SQLite database files:**
  - `content.db` (mostly read-only): places, price cards, phrases, tips/articles, FTS tables
  - `user.db` (write-heavy): favorites, recents, Home Base, active route progress, downloads metadata
- Why two DBs: content updates become a fast **file swap** (less risk of corrupting user state, and no long migration).
- Preferences storage for tiny settings only:
  - `@react-native-async-storage/async-storage` for both platforms
  - Settings: language, exchange rate, Wi‑Fi-only downloads

**Offline content store:**
- Ship bundled seed content using `expo-asset` (in `assets/seed/content.db`)
- On first run, copy seed `content.db` to writable location using `expo-file-system` (**FTS tables must ship prebuilt**; if a rebuild is ever required, do it in the background and keep core search usable)
- Cache updated bundles; verify; then:
  - (Preferred) replace `content.db` with a prebuilt, verified DB file for that version
  - Atomic swap with rollback support

- Activation must be exclusive and crash-safe:
  - Close all SQLite connections via the db wrapper
  - Ensure no `-wal` / `-shm` sidecar files remain for `content.db` (delete or swap them together)
  - Open `content.db` in read-only / query-only mode (prevent accidental writes that create WAL)
  - Use `FileSystem.moveAsync()` for atomic rename (temp file + rollback)
  - Post-activation verification:
    - `PRAGMA quick_check;` (mandatory)
    - rollback to last-known-good if verification fails
  - Reopen connections after swap

**Non-blocking startup rule:**
- Never block app startup on downloads/indexing/import
- If an update/pack is incomplete, fall back to last-known-good content and show a small banner
- Avoid infinite spinners: every download/import state must have timeout + retry + cancel

### Downloads & storage (offline packs)

Treat downloads like a mini product: predictable, resumable, and easy to manage.

**Expo (both platforms):**
- Use `expo-file-system` `createDownloadResumable()` for resumable downloads
- Treat "background downloading while the app is killed" as **best-effort** (platform-dependent); the hard requirement is **process-death-resilient resume on next launch** with clear user messaging
- Resume data stored for pause/resume (library handles Range headers via `savable()` and `resumeAsync()`)
- Preflight: check available disk space via `expo-file-system` (`FileSystem.getFreeDiskStorageAsync()`)
- Use `@react-native-community/netinfo` for network state and Wi-Fi-only toggle

**Packs are a product surface:**
- Pack manifest supports **dependencies** (e.g., routing_graph depends on medina_map_tiles)
- "Recommended downloads" (based on selected itinerary / trip length / Home Base region)
- Verify downloads (sha256 from manifest) before importing/using assets
  - Use `expo-crypto` for sha256 verification
- **Signed manifest (recommended even in v1 if any packs are hosted remotely):** Ed25519 signature with pinned public key
- Safe install pipeline: download → verify → unpack to temp → validate → atomic move → register
- Make installs **idempotent** and crash-safe via a Pack Registry (single source of truth):
  - `packs` table in `user.db`: `{ packId, version, state, installedAt, sizeBytes, sha256, lastVerifiedAt }`
  - on app start: reconcile filesystem ↔ registry; repair or rollback if mismatched
- Rollback: keep last-known-good pack version; auto-revert on validation failure
- Cache eviction policy:
  - Show total space used by packs
  - Allow uninstall per pack
  - Keep the last 1–2 content versions for rollback, then auto-clean older ones
- Backup policy (critical for large offline packs):
  - **iOS:** Use `FileSystem.documentDirectory` with appropriate backup exclusion via Expo config plugin or native configuration
  - **Android:** configure backup rules via Expo config plugin to exclude large packs
  - Backup only user intent/state (`user.db` + small settings)

**Pack types (district-based + utility-based):**
- Base Pack (ships in-app)
- Medina Pack (offline map + routing graph + core POIs)
  - Declare explicit subcomponents: tiles + routing graph + POIs (lets you diagnose failures clearly)
  - Add: `travel_matrix` + `route_legs` (precomputed; powers fast offline Route Cards + My Day)
- Gueliz Pack (offline POIs + map)
- Day Trips Pack (offline guides; optional map)
- Audio Pack (phrases + mini guides)
- Images Pack (hi-res)

**Data saver UX:**
- Show pack sizes up front + "Wi‑Fi only" toggle
- Allow cellular download with explicit confirmation for large packs

### Search

- **SQLite full-text search** for fast, consistent on-device search (FTS5 preferred):
  - FTS across places, price cards, phrases, tips/articles
  - Add a shared **normalization spec** (Arabic/Latin/digits) applied at index + query time
  - Normalize Arabic-Indic digits (٠١٢٣٤٥٦٧٨٩) → (0123456789) at index + query time
  - Index `aliases` aggressively (high leverage for tourists)
  - Add lightweight ranking boosts: exact match > alias match > prefix match > contains
  - Add "Did you mean?" suggestions using aliases + prefix candidates (offline, deterministic)
  - Prefer per-locale indexing strategy:
    - show results in UI language when available
    - fallback to English content when missing (never blank)
  - `expo-sqlite` supports FTS5 on both platforms (Expo SDK 50+)
  - FTS tables must be prebuilt in `content.db` (no runtime index creation)

---

## 7) Architecture (offline-first, no backend required for v1)

### v1 (no backend)

**Expo React Native Architecture (TypeScript)**
```
marrakechCompass/
├─ app.json                      # Expo app configuration
├─ app.config.js                 # Dynamic Expo config (optional)
├─ eas.json                      # EAS Build configuration
├─ package.json
├─ tsconfig.json
├─ babel.config.js
├─ metro.config.js
├─ index.js                      # Entry point (registers App)
│
├─ src/
│   ├─ App.tsx                   # Root component, providers, navigation setup
│   ├─ core/
│   │   ├─ database/
│   │   │   ├─ ContentDatabase.ts    # expo-sqlite wrapper, read-only content
│   │   │   ├─ UserDatabase.ts       # expo-sqlite wrapper, user state
│   │   │   ├─ DatabaseManager.ts    # connection management, atomic swap
│   │   │   └─ migrations/
│   │   ├─ repositories/
│   │   │   ├─ PlaceRepository.ts
│   │   │   ├─ PriceCardRepository.ts
│   │   │   ├─ PhraseRepository.ts
│   │   │   ├─ ItineraryRepository.ts
│   │   │   ├─ FavoritesRepository.ts
│   │   │   └─ RecentsRepository.ts
│   │   ├─ services/
│   │   │   ├─ LocationService.ts    # expo-location wrapper
│   │   │   ├─ HeadingService.ts     # expo-location heading (preferred) + magnetometer fallback
│   │   │   ├─ DownloadService.ts    # expo-file-system downloads
│   │   │   ├─ ContentSyncService.ts # bundle verification + swap
│   │   │   └─ SearchService.ts      # FTS5 queries
│   │   └─ engines/
│   │       ├─ PricingEngine.ts      # Quote → Action logic
│   │       ├─ PlanEngine.ts         # My Day offline builder
│   │       ├─ RouteEngine.ts        # leg estimates + progress
│   │       ├─ GeoEngine.ts          # haversine, bearing
│   │       └─ TrustEngine.ts        # staleness/confidence/volatility → UI badges + warnings
│   ├─ features/
│   │   ├─ home/
│   │   │   ├─ HomeScreen.tsx
│   │   │   ├─ useHome.ts
│   │   │   └─ components/
│   │   ├─ explore/
│   │   │   ├─ ExploreScreen.tsx
│   │   │   ├─ PlaceListScreen.tsx
│   │   │   ├─ PlaceMapScreen.tsx
│   │   │   ├─ PlaceDetailScreen.tsx
│   │   │   └─ useExplore.ts
│   │   ├─ eat/
│   │   │   ├─ EatScreen.tsx
│   │   │   └─ useEat.ts
│   │   ├─ prices/
│   │   │   ├─ PricesScreen.tsx
│   │   │   ├─ PriceCardDetailScreen.tsx
│   │   │   └─ usePrices.ts
│   │   ├─ quoteAction/
│   │   │   ├─ QuoteActionScreen.tsx
│   │   │   ├─ FairnessMeter.tsx
│   │   │   └─ useQuoteAction.ts
│   │   ├─ homeBase/
│   │   │   ├─ HomeBaseSetupScreen.tsx
│   │   │   ├─ GoHomeScreen.tsx
│   │   │   ├─ CompassArrow.tsx
│   │   │   └─ useHomeBase.ts
│   │   ├─ myDay/
│   │   │   ├─ MyDayScreen.tsx
│   │   │   ├─ ConstraintPicker.tsx
│   │   │   └─ useMyDay.ts
│   │   ├─ routeCards/
│   │   │   ├─ RouteOverviewScreen.tsx
│   │   │   ├─ NextStopScreen.tsx
│   │   │   └─ useRoute.ts
│   │   ├─ phrasebook/
│   │   │   ├─ PhrasebookScreen.tsx
│   │   │   ├─ PhraseDetailScreen.tsx
│   │   │   └─ usePhrasebook.ts
│   │   ├─ search/
│   │   │   ├─ SearchScreen.tsx
│   │   │   └─ useSearch.ts
│   │   ├─ more/
│   │   │   ├─ MoreScreen.tsx
│   │   │   ├─ CultureScreen.tsx
│   │   │   ├─ TipsScreen.tsx
│   │   │   └─ ItinerariesScreen.tsx
│   │   └─ settings/
│   │       ├─ SettingsScreen.tsx
│   │       ├─ DownloadsScreen.tsx
│   │       └─ DiagnosticsScreen.tsx
│   ├─ shared/
│   │   ├─ components/
│   │   │   ├─ Card.tsx
│   │   │   ├─ Chip.tsx
│   │   │   ├─ PriceTag.tsx
│   │   │   ├─ MapPreview.tsx
│   │   │   ├─ SearchBar.tsx
│   │   │   ├─ SectionHeader.tsx
│   │   │   ├─ ShareCardRenderer.tsx
│   │   │   └─ OfflineBanner.tsx
│   │   ├─ hooks/
│   │   │   ├─ useDatabase.ts
│   │   │   ├─ useLocation.ts        # wraps expo-location
│   │   │   ├─ useNetworkState.ts    # wraps expo-network
│   │   │   └─ useStorage.ts
│   │   ├─ models/
│   │   │   ├─ Place.ts
│   │   │   ├─ PriceCard.ts
│   │   │   ├─ GlossaryPhrase.ts
│   │   │   ├─ Itinerary.ts
│   │   │   ├─ Plan.ts
│   │   │   └─ UserSettings.ts
│   │   ├─ context/
│   │   │   ├─ DatabaseContext.tsx
│   │   │   ├─ SettingsContext.tsx
│   │   │   └─ LocationContext.tsx
│   │   ├─ theme/
│   │   │   ├─ colors.ts
│   │   │   ├─ typography.ts
│   │   │   └─ spacing.ts
│   │   └─ utils/
│   │       ├─ formatters.ts
│   │       ├─ constants.ts
│   │       └─ i18n.ts
│   ├─ navigation/
│   │   ├─ RootNavigator.tsx
│   │   ├─ TabNavigator.tsx
│   │   └─ types.ts
│   └─ locales/
│       ├─ en.json
│       └─ fr.json
│
├─ assets/
│   ├─ seed/
│   │   └─ content.db               # Bundled SQLite database
│   ├─ images/
│   │   ├─ icon.png
│   │   ├─ splash.png
│   │   └─ adaptive-icon.png
│   └─ fonts/                       # Custom fonts if needed
│
├─ shared/                          # Content pipeline (Node.js scripts)
│   ├─ content/
│   │   ├─ places.json
│   │   ├─ price_cards.json
│   │   ├─ glossary.json
│   │   ├─ culture.json
│   │   ├─ tips.json
│   │   ├─ activities.json
│   │   ├─ itineraries.json
│   │   └─ events.json
│   ├─ scripts/
│   │   ├─ validate-content.ts
│   │   ├─ build-bundle.ts          # JSON → SQLite content.db
│   │   ├─ build-routing-matrix.ts  # curated POIs → travel-time matrix + route legs (offline)
│   │   ├─ check-links.ts
│   │   └─ copy-db-to-assets.ts     # Copy content.db to assets/seed/
│   └─ schema/
│       └─ content-schema.json
│
├─ ios/                             # Generated by expo prebuild (managed by Expo)
│   └─ ...
│
├─ android/                         # Generated by expo prebuild (managed by Expo)
│   └─ ...
│
├─ __tests__/
│   ├─ engines/
│   │   ├─ PricingEngine.test.ts
│   │   ├─ PlanEngine.test.ts
│   │   ├─ GeoEngine.test.ts
│   │   ├─ RouteEngine.test.ts
│   │   ├─ TrustEngine.test.ts
│   │   └─ TrustEngine.golden.test.ts
│   ├─ repositories/
│   │   ├─ PlaceRepository.test.ts
│   │   ├─ PriceCardRepository.test.ts
│   │   └─ FavoritesRepository.test.ts
│   ├─ services/
│   │   ├─ SearchService.test.ts
│   │   └─ ContentSyncService.test.ts
│   ├─ database/
│   │   └─ DatabaseManager.test.ts
│   ├─ components/
│   │   ├─ FairnessMeter.test.tsx
│   │   ├─ CompassArrow.test.tsx
│   │   └─ ShareCardRenderer.test.tsx
│   ├─ hooks/
│   │   ├─ useQuoteAction.test.ts
│   │   └─ useHomeBase.test.ts
│   ├─ offline/
│   │   └─ gracefulDegradation.test.ts
│   ├─ localization/
│   │   └─ translations.test.ts
│   ├─ performance/
│   │   └─ startup.perf.test.ts
│   └─ fixtures/
│       └─ trust-engine-golden.json
│
├─ maestro/                         # E2E tests
│   └─ flows/
│       ├─ 01-fresh-install-offline.yaml
│       ├─ 03-quote-action-flow.yaml
│       └─ 07-route-cards-execution.yaml
│
└─ convex/                          # Phase 2 only
    ├─ schema.ts
    ├─ content.ts
    └─ versions.ts
```

**Rule:** The app remains fully useful without internet.

**Expo-specific notes:**
- `ios/` and `android/` directories are generated by `expo prebuild` and should be in `.gitignore` for managed workflow, or committed if using continuous native generation
- Use `eas.json` to configure build profiles (development, preview, production)
- `app.json` contains Expo-specific configuration (bundle identifiers, permissions, plugins)
- Seed content bundled via `expo-asset` from `assets/seed/content.db`

---

## 8) Phase 2 backend: Convex (for updates + sync, not dependency)

Phase 2 goal: enable updates without app releases while keeping offline reliability.

You can do this with either:
- **Signed manifests + static hosting (recommended baseline)** for `content.db` + pack files on a CDN/object store
- **Convex (optional)** for admin workflows, feedback intake, and an events feed

The simpler baseline (static hosting + signed manifests) reduces operational complexity and makes Phase 2 less "all-or-nothing."

Convex is added to:

- update content without app releases
- optionally sync favorites/bookmarks across devices (if you add auth)
- manage content with a lightweight admin workflow
- optionally ship a small curated "What's on this week" events feed (online-first + cached; never required)

### What Convex should store

**Content tables (curated):**

- `places`
- `priceCards`
- `glossaryPhrases`
- `cultureArticles`
- `itineraries`
- `tips`
- `events` (phase 2): small curated weekly list with timestamps + expiration

**Versioning:**

- `contentVersions` (latest version + release notes + rollout rules)
  - include: `latest`, `releasedAt`, `releaseNotesByLocale`, `minSupportedAppVersion`, `rolloutPercent`

**Optional user state (if you do auth):**

- `userState` (favorites, bookmarks, downloads metadata)

**Feedback (high leverage for trust):**

- `feedback` (contentId, type, note, createdAt, appVersion, locale; no account required)

### Content sync approach (keep it robust + simple)

Two good approaches:

**Option A — Bundle-based (simplest)**

- Convex stores a `contentBundle` JSON for each version (or latest only)
- App checks `contentVersions.latest`
- If newer, downloads bundle and replaces cached content
- Rebuild local search index

Pros: easiest, least code, safest.
Cons: bigger downloads (still fine if curated).

**Option B — Incremental diffs (more complex)**

- App pulls updated docs since last version
- Writes updates to local cache
- Rebuild index

Pros: smaller updates.
Cons: more edge cases.

**Recommendation:** Start with **bundle-based**.

**Events approach (phase 2, optional):**
- Small JSON feed with `expiresAt` so stale events disappear automatically
- Cache last successful fetch so it's usable briefly offline (with "Last updated" label)

### Hardening (strongly recommended once *any* remote downloads ship — packs or updates)

- Add a **signed content manifest**:
  - manifest contains: `version`, `locale`, `bundleUrl`/`dbUrl`, `sizeBytes`, `sha256`, `releasedAt`, `minSupportedAppVersion`, `expiresAt`, `signature`
  - signature: Ed25519 (app ships with pinned public key; reject unsigned/expired manifests)
  - replay protection: store the highest accepted `releasedAt` and do not accept older manifests unless explicitly allowed (prevents downgrade attacks)
  - app verifies signature **before** download/import, then verifies sha256 **after** download and **before** activation
- **Atomic import + rollback**:
  - download → verify → **swap in a new content DB file** → keep previous version for rollback (fallback: import+swap tables)
- **Staged rollout**:
  - allow a rollout percentage / "beta channel" to catch bad releases early

### Assets (images/audio)

- v1: ship a small set in-app (best offline experience)
- phase 2:
  - host assets on a CDN/object store (S3/Cloudflare R2/etc.)
  - store URLs in Convex
  - download audio packs on demand and cache locally

Important: ensure asset URLs are versioned and match the content bundle version to avoid "missing audio/image" issues.

---

## 9) Data model (shared schema, TypeScript implementations)

### Shared JSON schema (content authoring)

Content is authored in JSON with a shared schema, then bundled into SQLite.
React Native uses the same database schema and content bundles on both platforms.

### Unify "place-like" entities

Landmarks, restaurants, shops, markets can share a base shape.

**Place** (SQLite table: `places`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | TEXT PK | |
| `name` | TEXT | |
| `aliases` | TEXT | JSON array of alternate spellings/names (optional but high leverage) |
| `region_id` | TEXT | pack/district id (e.g., "medina_core", "gueliz") |
| `category` | TEXT | "landmark", "museum", "garden", "neighborhood", "restaurant", "cafe", "shopping", etc. |
| `short_description` | TEXT | |
| `long_description` | TEXT | nullable |
| `reviewed_at` | TEXT | YYYY-MM-DD, nullable |
| `status` | TEXT | "open" / "temporarily_closed" / "permanently_closed" |
| `status_note` | TEXT | nullable (e.g., renovation, moved) |
| `confidence` | TEXT | "high", "medium", "low", nullable |
| `tourist_trap_level` | TEXT | "low" / "mixed" / "high" |
| `why_recommended` | TEXT | JSON array; short bullets |
| `neighborhood` | TEXT | nullable |
| `address` | TEXT | nullable |
| `lat` | REAL | nullable |
| `lng` | REAL | nullable |
| `hours_text` | TEXT | always shown |
| `hours_timezone` | TEXT | nullable |
| `hours_weekly` | TEXT | JSON array, nullable; enables "Open now" |
| `hours_exceptions` | TEXT | JSON array, nullable (Ramadan/holidays/one-off closures) |
| `hours_verified_at` | TEXT | nullable |
| `hours_stale_after_days` | INTEGER | nullable; default by category |
| `fees_min_mad` | INTEGER | nullable |
| `fees_max_mad` | INTEGER | nullable |
| `fees_notes` | TEXT | nullable |
| `expected_cost_min_mad` | INTEGER | nullable |
| `expected_cost_max_mad` | INTEGER | nullable |
| `expected_cost_notes` | TEXT | nullable |
| `expected_cost_updated_at` | TEXT | nullable |
| `expected_cost_stale_after_days` | INTEGER | nullable; default by category |
| `visit_min_minutes` | INTEGER | nullable |
| `visit_max_minutes` | INTEGER | nullable |
| `best_time_to_go` | TEXT | nullable (human-readable) |
| `best_time_windows` | TEXT | JSON array, nullable (machine: "morning"/"afternoon"/"evening") |
| `tags` | TEXT | JSON array |
| `local_tips` | TEXT | JSON array |
| `scam_warnings` | TEXT | JSON array |
| `do_and_dont` | TEXT | JSON array |
| `images` | TEXT | JSON array of asset refs or URLs |
| `related_links` | TEXT | JSON array (optional, authoring-time convenience; compiled to content_links) |

**TypeScript Model (React Native)**
```typescript
// src/shared/models/Place.ts

export type PlaceCategory =
  | 'landmark'
  | 'museum'
  | 'garden'
  | 'neighborhood'
  | 'restaurant'
  | 'cafe'
  | 'shopping';

export type Confidence = 'high' | 'medium' | 'low';

export type PlaceStatus = 'open' | 'temporarily_closed' | 'permanently_closed';

export interface Coordinate {
  lat: number;
  lng: number;
}

export interface WeeklyHours {
  day: number; // 0-6 (Sunday-Saturday)
  open: string; // "09:00"
  close: string; // "18:00"
}

export interface Place {
  id: string;
  name: string;
  aliases: string[];
  regionId: string;
  category: PlaceCategory;
  shortDescription: string;
  longDescription: string | null;
  reviewedAt: string | null; // ISO date
  status: PlaceStatus;
  statusNote: string | null;
  confidence: Confidence | null;
  touristTrapLevel: 'low' | 'mixed' | 'high';
  whyRecommended: string[];
  neighborhood: string | null;
  address: string | null;
  location: Coordinate | null;
  hoursText: string | null;
  hoursTimezone: string | null;
  hoursWeekly: WeeklyHours[] | null;
  hoursExceptions: object[] | null;
  hoursVerifiedAt: string | null;
  hoursStaleAfterDays: number | null;
  feesMinMad: number | null;
  feesMaxMad: number | null;
  feesNotes: string | null;
  expectedCostMinMad: number | null;
  expectedCostMaxMad: number | null;
  expectedCostNotes: string | null;
  expectedCostUpdatedAt: string | null;
  visitMinMinutes: number | null;
  visitMaxMinutes: number | null;
  bestTimeToGo: string | null;
  bestTimeWindows: string[] | null;
  tags: string[];
  localTips: string[];
  scamWarnings: string[];
  doAndDont: string[];
  images: string[];
}

// Helper to map SQLite row to Place object
export function mapRowToPlace(row: any): Place {
  return {
    id: row.id,
    name: row.name,
    aliases: JSON.parse(row.aliases || '[]'),
    regionId: row.region_id,
    category: row.category as PlaceCategory,
    shortDescription: row.short_description,
    longDescription: row.long_description,
    reviewedAt: row.reviewed_at,
    status: row.status as PlaceStatus,
    statusNote: row.status_note,
    confidence: row.confidence as Confidence | null,
    touristTrapLevel: row.tourist_trap_level,
    whyRecommended: JSON.parse(row.why_recommended || '[]'),
    neighborhood: row.neighborhood,
    address: row.address,
    location: row.lat && row.lng ? { lat: row.lat, lng: row.lng } : null,
    hoursText: row.hours_text,
    hoursTimezone: row.hours_timezone,
    hoursWeekly: row.hours_weekly ? JSON.parse(row.hours_weekly) : null,
    hoursExceptions: row.hours_exceptions ? JSON.parse(row.hours_exceptions) : null,
    hoursVerifiedAt: row.hours_verified_at,
    hoursStaleAfterDays: row.hours_stale_after_days,
    feesMinMad: row.fees_min_mad,
    feesMaxMad: row.fees_max_mad,
    feesNotes: row.fees_notes,
    expectedCostMinMad: row.expected_cost_min_mad,
    expectedCostMaxMad: row.expected_cost_max_mad,
    expectedCostNotes: row.expected_cost_notes,
    expectedCostUpdatedAt: row.expected_cost_updated_at,
    visitMinMinutes: row.visit_min_minutes,
    visitMaxMinutes: row.visit_max_minutes,
    bestTimeToGo: row.best_time_to_go,
    bestTimeWindows: row.best_time_windows ? JSON.parse(row.best_time_windows) : null,
    tags: JSON.parse(row.tags || '[]'),
    localTips: JSON.parse(row.local_tips || '[]'),
    scamWarnings: JSON.parse(row.scam_warnings || '[]'),
    doAndDont: JSON.parse(row.do_and_dont || '[]'),
    images: JSON.parse(row.images || '[]'),
  };
}
```

**PriceCard** (SQLite table: `price_cards`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | TEXT PK | |
| `title` | TEXT | e.g., "Taxi: Medina short ride" |
| `category` | TEXT | "taxi", "hammam", "souks", "food", "guides", etc. |
| `unit` | TEXT | "per ride", "per person", "per item", nullable |
| `volatility` | TEXT | "low", "medium", "high", nullable |
| `confidence` | TEXT | nullable |
| `expected_cost_min_mad` | INTEGER | |
| `expected_cost_max_mad` | INTEGER | |
| `expected_cost_notes` | TEXT | nullable |
| `expected_cost_updated_at` | TEXT | |
| `what_influences_price` | TEXT | JSON array |
| `negotiation_scripts` | TEXT | JSON array of {darijaLatin, arabic?, french?, english} |
| `red_flags` | TEXT | JSON array |
| `what_to_do_instead` | TEXT | JSON array |
| `context_modifiers` | TEXT | JSON array of modifier objects |
| `fairness_high_multiplier` | REAL | nullable, default 1.25 |
| `quantity_label` | TEXT | nullable |
| `quantity_default` | INTEGER | nullable |
| `quantity_min` | INTEGER | nullable |
| `quantity_step` | INTEGER | nullable |

**GlossaryPhrase** (SQLite table: `phrases`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | TEXT PK | |
| `category` | TEXT | |
| `arabic` | TEXT | RTL text |
| `latin` | TEXT | transliteration |
| `english` | TEXT | |
| `audio` | TEXT | asset ref or URL, nullable |

**Itinerary** (SQLite table: `itineraries`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | TEXT PK | |
| `title` | TEXT | |
| `duration` | TEXT | "1 day", "3 days", etc. |
| `steps` | TEXT | JSON array of step objects |

**UserSettings** (SQLite table in `user.db`: `user_settings`)

| Column | Type | Notes |
|--------|------|-------|
| `key` | TEXT PK | |
| `value` | TEXT | JSON-encoded value |

Keys: `homeBase`, `activeRoute`, `travelProfile`, `exchangeRate`

**Favorites** (SQLite table in `user.db`: `favorites`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | INTEGER PK | autoincrement |
| `content_type` | TEXT | "place", "price_card", "phrase", "itinerary" |
| `content_id` | TEXT | |
| `created_at` | TEXT | ISO8601 |

**Recents** (SQLite table in `user.db`: `recents`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | INTEGER PK | autoincrement |
| `content_type` | TEXT | |
| `content_id` | TEXT | |
| `viewed_at` | TEXT | ISO8601 |

**Plan** (SQLite table in `user.db`: `plans` — generated My Day plans)

| Column | Type | Notes |
|--------|------|-------|
| `id` | TEXT PK | |
| `created_at` | TEXT | ISO8601 |
| `inputs` | TEXT | JSON object |
| `steps` | TEXT | JSON array |

### Content link graph (recommended)

Add a SQLite table `content_links` in `content.db` (generated at build time):

| Column | Type | Notes |
|--------|------|-------|
| `id` | INTEGER PK | autoincrement |
| `from_type` | TEXT | "place", "price_card", "tip", "phrase" |
| `from_id` | TEXT | |
| `to_type` | TEXT | "place", "price_card", "tip", "phrase" |
| `to_id` | TEXT | |
| `link_kind` | TEXT | "related_price", "useful_phrase", "avoid_scam", "safe_alternative" |

This powers cross-links without hardcoding per-feature logic.

### Imported dataset notes (current workspace)

The current `shared/content/*.json` files (including the newly added Lonely Planet extraction) follow this envelope:

```json
{
  "meta": { "generated_at": "...", "source_document": "...", "notes": [] },
  "items": [ ... ]
}
```

- `items[].id` is the stable primary key used for joins and user state references.
- `source_refs` is used as editorial provenance (for the imported guide content, values map to guide page numbers).
- Current populated domains are `places`, `price_cards`, `activities`, `itineraries`, `tips`, `culture`, `glossary`, and `events`.
- Relationship conventions in current data:
- `itineraries.items[].steps[]` references `place_id` (for `type: "place"` or `type: "meal"`) and `activity_id` (for `type: "activity"`).
- `tips` can include `related_place_ids` and/or `related_price_card_ids`.
- `favorites`/`recents` (in `user.db`) reference content by `content_type` + `content_id`.

**Image linkage in current imported data**

- Place records now use an `images` array (for example in `shared/content/places.json`) and currently point to local extraction paths.
- Use `docs/lonely_planet_extracted/images_rgb_canonical/` as the preferred upload source (RGB-safe + deduplicated).
- Do not use `docs/lonely_planet_extracted/images/` as the primary upload source for production; it includes raw extraction outputs that may contain CMYK color artifacts.
- Image manifests and mapping files:
- `docs/lonely_planet_extracted/images_rgb/manifest_rgb.json` (RGB extraction inventory + hashes)
- `docs/lonely_planet_extracted/images_rgb/canonical_upload_list.json` (deduplicated upload list)
- `docs/lonely_planet_extracted/images/place_image_candidates.json` (place-to-image mapping, including `suggested_relative_path_rgb`; fallback mappings are flagged with `suggested_match_type: "nearest_page_fallback"`)

**Implementation guidance (when wiring the app)**

- During asset upload, replace local `images` paths with stable remote URLs, but keep the same place IDs so app/database joins remain unchanged.
- Treat `images[0]` as hero image and additional entries as optional gallery images.
- If mapping is marked as fallback (`nearest_page_fallback`), treat it as provisional and queue it for editorial review.
- Never block rendering on missing images; always fall back to text-first cards/placeholders.
- Keep imports deterministic: same input JSON + same asset map should produce the same `content.db`.

**How to use each `shared/content` file in app implementation**

- `shared/content/places.json`
- Primary source for Explore/Eat place cards and detail screens.
- Also used by Route Cards, My Day planner inputs, map markers, and related-item chips.
- `shared/content/price_cards.json`
- Source for Prices list/detail and Quote → Action engine inputs (`expected_cost_*`, scripts, modifiers, fairness multipliers).
- Should be joinable from place/tip UI via related IDs or `content_links`.
- `shared/content/activities.json`
- Source for day-trip/experience cards and itinerary `activity` steps.
- Use for optional “book later” and planning modules; keep offline summaries first.
- `shared/content/itineraries.json`
- Source for itinerary list/detail and Route Card execution flows.
- Parse `steps[]` by `type` and resolve referenced `place_id` / `activity_id` before render.
- `shared/content/tips.json`
- Source for safety, scam awareness, arrival, accessibility, family, and practical decision cards.
- Use `related_place_ids` / `related_price_card_ids` to surface contextual tips in detail pages.
- `shared/content/culture.json`
- Source for concise etiquette/culture do-don’t modules in More/Culture screens.
- Keep these lightweight and skimmable; they are not long-form articles.
- `shared/content/glossary.json`
- Source for phrasebook categories + phrase detail cards.
- Respect RTL behavior when Arabic is present and preserve `verification_status` for QA workflows.
- `shared/content/events.json`
- Optional online-first module; if stale/unavailable, hide gracefully without impacting core offline value.
- `shared/content` `meta` blocks
- Use for diagnostics (“content generated at”, source provenance) and internal QA visibility.
- Do not block runtime UX on `meta` parse failures; treat missing meta as non-fatal.

---

## 10) Screen list (everything that needs to be built)

### Navigation + shell

- Tab navigator layout
- Onboarding flow (first-run + re-runnable from Settings)
- Global search modal/screen
- Shared "detail" screens (place detail, price card detail)
- Settings screen (offline downloads/**Downloads manager**, exchange rate, **language**, privacy, Privacy Center, diagnostics, "What's new")
- Diagnostics screen (content version, last sync/import status, storage usage, **Offline Readiness**, **Repair Packs**, export debug report)

### Home

- Quick actions
- **Offline Ready** chip (shows: Ready / Missing recommended pack / Integrity issue → one-tap fix path)
- **My Day** plan builder (constraints → generated plan → Route Cards)
- Today's tip
- Phrase of the day
- Saved + recents

### Arrival + tools

- Arrival mode (first 2 hours + first day)
- Currency converter (manual rate + timestamp)
- Tipping guide
- Bargaining calculator
- **Home Base setup** (set riad/hotel)
- **Go Home** (compass screen)

### Explore

- List view with filters
- Map view with markers + list preview
- Place detail screen
- Neighborhood section (optional but valuable)

### Eat

- Curated list view + filters
- Place detail (reuse)
- "What to eat" guide page (optional)

### Prices

- Price card categories
- Price card detail pages
- **Quote → Action** tool (modal/screen)
- Negotiation playbook page (optional)

### More

- Culture & etiquette pages
- Darija phrasebook: categories + search + phrase detail
- Itineraries list + itinerary detail
- **My Trip builder** (1/2/3 day planner + drag reorder)
- **Route Card** (route overview + next stop + Medina Mode)
- Tips & safety pages

### Cross-cutting features

- Favorites
- Recently viewed
- Share
- Offline content loader + caching
- Search indexing

---

## 11) Project structure (recommended)

### Expo React Native project structure

```
marrakechCompass/
├── app.json                     # Expo app configuration
├── app.config.js                # Dynamic Expo config (for env vars, plugins)
├── eas.json                     # EAS Build configuration
├── package.json                 # Dependencies, scripts
├── tsconfig.json                # TypeScript configuration (strict mode)
├── babel.config.js              # Babel configuration
├── metro.config.js              # Metro bundler configuration
├── index.js                     # Entry point
├── .eslintrc.js                 # ESLint configuration
├── jest.config.js               # Jest test configuration
│
├── src/                         # React Native TypeScript source
│   ├── App.tsx                  # Root component with providers
│   ├── core/
│   │   ├── database/            # expo-sqlite wrappers
│   │   ├── repositories/        # Data access layer
│   │   ├── services/            # expo-location, expo-sensors, etc.
│   │   └── engines/             # Business logic (pricing, planning, geo)
│   ├── features/
│   │   ├── home/
│   │   ├── explore/
│   │   ├── eat/
│   │   ├── prices/
│   │   ├── quoteAction/
│   │   ├── homeBase/
│   │   ├── myDay/
│   │   ├── routeCards/
│   │   ├── phrasebook/
│   │   ├── search/
│   │   ├── more/
│   │   └── settings/
│   ├── shared/
│   │   ├── components/          # Reusable UI components
│   │   ├── hooks/               # Custom React hooks
│   │   ├── models/              # TypeScript types + Zod schemas
│   │   ├── context/             # React Context providers
│   │   ├── theme/               # Design tokens (colors, typography)
│   │   └── utils/               # Formatters, constants, i18n
│   ├── navigation/
│   │   ├── RootNavigator.tsx
│   │   ├── TabNavigator.tsx
│   │   └── types.ts
│   └── locales/
│       ├── en.json
│       ├── fr.json
│       ├── es.json
│       ├── de.json
│       ├── it.json
│       └── nl.json
│
├── assets/                      # Expo asset directory
│   ├── seed/
│   │   └── content.db           # Bundled SQLite database
│   ├── images/
│   │   ├── icon.png             # App icon (1024x1024)
│   │   ├── splash.png           # Splash screen
│   │   └── adaptive-icon.png    # Android adaptive icon
│   ├── fonts/                   # Custom fonts
│   └── audio/                   # Bundled audio files
│
├── shared/                      # Content pipeline (Node.js scripts)
│   ├── content/
│   │   ├── places.json
│   │   ├── price_cards.json
│   │   ├── glossary.json
│   │   ├── culture.json
│   │   ├── tips.json
│   │   ├── activities.json
│   │   ├── itineraries.json
│   │   └── events.json
│   ├── scripts/
│   │   ├── validate-content.ts  # Zod validation
│   │   ├── build-bundle.ts      # JSON → SQLite content.db
│   │   ├── build-routing-matrix.ts  # curated POIs → travel-time matrix + route legs
│   │   ├── check-links.ts       # Reference validation
│   │   └── copy-db-to-assets.ts # Copy to assets/seed/
│   └── schema/
│       └── content-schema.json  # JSON Schema for validation
│
├── ios/                         # Generated by `expo prebuild`
│   └── ...                      # (managed by Expo, regenerated on prebuild)
│
├── android/                     # Generated by `expo prebuild`
│   └── ...                      # (managed by Expo, regenerated on prebuild)
│
├── __tests__/                   # Jest tests
│   ├── engines/
│   │   ├── PricingEngine.test.ts
│   │   ├── PlanEngine.test.ts
│   │   ├── GeoEngine.test.ts
│   │   ├── RouteEngine.test.ts
│   │   ├── TrustEngine.test.ts
│   │   └── TrustEngine.golden.test.ts
│   ├── repositories/
│   │   ├── PlaceRepository.test.ts
│   │   ├── PriceCardRepository.test.ts
│   │   ├── PhraseRepository.test.ts
│   │   ├── FavoritesRepository.test.ts
│   │   └── RecentsRepository.test.ts
│   ├── services/
│   │   ├── SearchService.test.ts
│   │   ├── ContentSyncService.test.ts
│   │   └── PackRegistry.test.ts
│   ├── database/
│   │   └── DatabaseManager.test.ts
│   ├── components/
│   │   ├── FairnessMeter.test.tsx
│   │   ├── CompassArrow.test.tsx
│   │   ├── PriceTag.test.tsx
│   │   ├── OfflineBanner.test.tsx
│   │   ├── OpenNowChip.test.tsx
│   │   └── ShareCardRenderer.test.tsx
│   ├── hooks/
│   │   ├── useQuoteAction.test.ts
│   │   ├── useHomeBase.test.ts
│   │   ├── useRoute.test.ts
│   │   └── useNetworkState.test.ts
│   ├── utils/
│   │   └── formatters.test.ts
│   ├── offline/
│   │   └── gracefulDegradation.test.ts
│   ├── localization/
│   │   ├── translations.test.ts
│   │   ├── rtl.test.ts
│   │   └── fallback.test.ts
│   ├── performance/
│   │   ├── startup.perf.test.ts
│   │   ├── search.perf.test.ts
│   │   └── memory.perf.test.ts
│   └── fixtures/
│       ├── trust-engine-golden.json
│       ├── test-places.json
│       └── test-price-cards.json
│
├── maestro/                     # E2E tests (Maestro)
│   ├── flows/
│   │   ├── 01-fresh-install-offline.yaml
│   │   ├── 02-explore-and-price-check.yaml
│   │   ├── 03-quote-action-flow.yaml
│   │   ├── 04-home-base-setup.yaml
│   │   ├── 05-go-home-compass.yaml
│   │   ├── 06-my-day-builder.yaml
│   │   ├── 07-route-cards-execution.yaml
│   │   ├── 08-phrasebook-search.yaml
│   │   ├── 09-download-pack-flow.yaml
│   │   ├── 10-content-update-flow.yaml
│   │   ├── 11-low-storage-recovery.yaml
│   │   └── 12-permission-denial-paths.yaml
│   ├── utils/
│   │   └── common-assertions.yaml
│   └── config.yaml
│
├── convex/                      # Phase 2 only
│   ├── schema.ts
│   ├── content.ts
│   └── versions.ts
│
└── docs/
    └── api.md
```

### Key files explained

**Root configuration files (Expo-specific):**
- `app.json` - Expo app configuration (name, slug, version, iOS/Android bundle IDs, permissions, plugins)
- `app.config.js` - Dynamic configuration (environment variables, conditional plugins)
- `eas.json` - EAS Build profiles (development, preview, production)
- `package.json` - dependencies, scripts for build/test/lint
- `tsconfig.json` - TypeScript configuration with path aliases
- `metro.config.js` - Metro bundler configuration

**Native directories (managed by Expo):**
- `ios/` - Generated by `expo prebuild`, contains Xcode project
- `android/` - Generated by `expo prebuild`, contains Gradle project
- These directories are regenerated when you run `expo prebuild --clean`
- For development builds, commit these or regenerate in CI

**Assets (Expo asset system):**
- `assets/seed/content.db` - Bundled SQLite database (loaded via expo-asset)
- `assets/images/` - App icons, splash screens
- `assets/fonts/` - Custom fonts (loaded via expo-font)
- `assets/audio/` - Bundled audio files

**Content pipeline:**
- `shared/content/` - JSON source files (single source of truth)
- `shared/scripts/build-bundle.ts` - generates `content.db` from JSON
- `shared/scripts/copy-db-to-assets.ts` - copies DB to `assets/seed/`

---

## 12) Non-functional requirements (make it "paid quality")

### Performance

- Fast startup (avoid heavy network calls on launch)
- Responsiveness is non-negotiable: never do disk IO / network / JSON decoding on the JS thread; use async patterns and consider moving heavy work to native modules if needed
- Lazy-load images using `expo-image` (built-in caching and performance optimization)
- Build search index once and reuse
- Measure and enforce startup performance:
  - Profile launch time on both iOS and Android using Flipper or Expo Dev Tools
  - Hermes engine is enabled by default in Expo SDK 50+
  - Use EAS Build for optimized production builds
- Set performance budgets:
  - cold start target (mid-tier device)
  - search response time target (p95)
  - memory ceiling in Explore + Map views
  - offline map render performance (fps target on mid-tier device)
  - **marker budget** (max markers rendered at once; enforce clustering/progressive disclosure)
  - offline route computation budget (time-to-route for Medina core)

### Offline behavior

- Entire guide works without internet
- Online features are additive only
- Clear messaging when offline, not scary

**Paid-app guarantee:**
- Core value works immediately after install, offline.
- No blocking "downloading resources…" screen on first launch.
- If optional packs are not downloaded, the app still remains fully usable.

### Privacy

- Trust + privacy are product pillars:
  - "Near me" is optional
  - Location used only on-device (sorting, Go Home, Navigate) and only while those screens are open
  - No contacts/photos permissions (ever)
  - No ads, no selling data, no shady SDKs
  - If crash reporting exists, make it privacy-forward and explain it in-app (opt-in preferred)

### Privacy / Trust / Attribution Center (in Settings)

A user-facing screen that builds confidence and reduces "why should I trust this?" friction:

- **"Works offline" explanation**: clear, friendly summary of what works without internet
- **"How prices are sourced"**: what "confidence" and "last reviewed" mean; how ranges are derived
- **"How to report outdated info"**: link to feedback flow
- **Data & privacy**:
  - what data is stored on-device
  - what leaves the device (ideally nothing in v1)
  - why permissions are requested (location only, on-demand)
- **Attributions**: map data licenses, media credits, open-source licenses
- **Crash reporting toggle**: opt-in preferred, off by default, with clear explanation

### Store policy resilience
- CI check: fail release builds if iOS build SDK / Android target SDK are below current store requirements
- Re-evaluate minimum deployment targets yearly based on device share + QA budget

### QA checklist (minimum)

**Both platforms:**
- Works in airplane mode
- Works on low-memory devices
- Map view doesn't crash with many markers (keep curated marker count reasonable; enforce a marker budget via clustering/progressive disclosure)
- Search works fast across content
- Optional-pack-missing flows degrade gracefully (no dead-end screens)
- Upgrade from previous store version preserves user state + pack registry
- All external links open correctly
- Dark mode works correctly
- RTL text (Arabic) renders correctly in phrasebook

**iOS-specific:**
- VoiceOver smoke test on core flows (Quote → Action, Go Home, Route Cards, Search)
- Dynamic Type sizes (accessibility)
- Works on oldest supported iOS version (14.0)
- Background download resume after app termination

**Android-specific:**
- TalkBack smoke test on core flows
- Font scaling (accessibility)
- Works on oldest supported API level (26)
- Background download resume after process death
- Battery optimization handling (Doze mode)

**Expo-specific:**
- JS bundle loads and runs on both platforms without errors
- No yellow box warnings in release builds
- Hermes engine enabled (default in Expo SDK 50+)
- Expo modules (expo-sqlite, expo-sensors, expo-location) work on both platforms
- React Navigation transitions are smooth (no jank)
- Development build runs correctly on physical devices
- EAS Build produces valid App Store / Play Store binaries

**Location flows tested (both platforms):**
- Deny permission (app still usable)
- Grant permission (Go Home + Route Cards work)
- Heading unavailable (fallback UI still works)
- Low power mode / battery optimizations (manual refresh still works)
- Location accuracy degraded (graceful handling)
- Offline navigation running for 10 minutes (battery + stability)

Add "paid app" reliability basics:

- **App must be fully usable in airplane mode immediately after fresh install**
- Interruption tests:
  - app launch while downloads are in progress (must still be usable)
  - content update download interrupted (resume works)
  - low storage during download (clear error message)
  - app killed mid-import (must recover safely on next launch)
  - app updated from N-1/N-2 with existing data (no data loss)
  - IAP restore after reinstall (Option B) keeps entitlement offline
- Permission contract:
  - no location prompt until explicit user action (Near Me / Go Home / Navigate)
- Observability:
  - Crash reporting: **opt-in preferred**, privacy-forward messaging in Privacy Center
  - On-device ring-buffer logs (redacted; no precise location; no user-entered notes)
  - Export debug report includes pack/version state + recent redacted events (helps support without screenshots)
  - Operational quality gates: monitor **Android vitals** (crash + ANR rates) and iOS crash/hang metrics (Xcode Organizer/MetricKit) as release blockers, not "nice to haves"

---

## 12b) Test strategy (paid-app reliability)

For a paid, offline-first app where reliability is the core product promise, testing must be comprehensive and automated. This section defines the complete test strategy.

### Test pyramid overview

| Layer | Scope | Coverage Target | When Run |
|-------|-------|-----------------|----------|
| Unit tests | Engines, utilities, formatters, hooks | >90% | Every commit |
| Integration tests | Repositories + SQLite, services | >80% | CI on every PR |
| Component tests | Critical UI components | Key components | CI on every PR |
| E2E tests (Maestro) | Critical user journeys | 12+ scenarios | PR smoke + nightly full + pre-release |
| Performance tests | Startup, search, rendering | Pass budgets | Nightly + pre-release on real devices |
| Manual QA | Platform-specific, edge cases | Checklist | Before store submission |

### Release blocker thresholds (explicit)

Ship is blocked unless all of these are true for the release candidate:

- P0/P1 open defects: **0**
- Critical E2E pass rate: **100%** (one infra retry allowed)
- Crash-free sessions during staged rollout: **>=99.7%**
- Android vitals: **user-perceived ANR < 0.47%**, overall ANR < 0.70%
- iOS crash/hang metrics: no regression versus previous production release
- Performance budgets: pass on reference physical devices
- Data integrity suites (upgrade matrix + chaos + rollback): no data-loss findings

### Unit tests

**Engines (pure TypeScript, no Expo imports):**

All engines must be thoroughly unit tested since they contain core business logic.

```typescript
// __tests__/engines/PricingEngine.test.ts
describe('PricingEngine', () => {
  describe('calculateFairness', () => {
    it('returns "fair" when quote is within expected range', () => {});
    it('returns "low" when quote is below lowMultiplier threshold', () => {});
    it('returns "high" when quote exceeds max but within highMultiplier', () => {});
    it('returns "very_high" when quote exceeds highMultiplier', () => {});
    it('applies context modifiers correctly (night, peak_season)', () => {});
    it('uses per-card multiplier overrides when provided', () => {});
    it('handles quantity correctly (per person, per item)', () => {});
    it('generates correct counter-offer range', () => {});
    it('selects appropriate negotiation scripts', () => {});
  });
});

// __tests__/engines/PlanEngine.test.ts
describe('PlanEngine', () => {
  describe('generatePlan', () => {
    it('respects availableMinutes constraint', () => {});
    it('filters places by selected interests', () => {});
    it('avoids closed places when hours are known', () => {});
    it('clusters geographically to minimize backtracking', () => {});
    it('respects bestTimeWindows (morning/afternoon/evening)', () => {});
    it('adjusts stop count based on pace setting', () => {});
    it('includes meal breaks at appropriate times', () => {});
    it('handles empty interest selection gracefully', () => {});
    it('returns empty plan when no places match constraints', () => {});
  });
});

// __tests__/engines/GeoEngine.test.ts
describe('GeoEngine', () => {
  describe('haversine', () => {
    it('calculates distance between two points correctly', () => {});
    it('returns 0 for identical points', () => {});
    it('handles antipodal points', () => {});
  });
  describe('bearing', () => {
    it('calculates bearing correctly (north = 0)', () => {});
    it('handles edge cases (same point, poles)', () => {});
  });
  describe('relativeAngle', () => {
    it('computes arrow rotation correctly', () => {});
    it('normalizes angles to 0-360 range', () => {});
  });
});

// __tests__/engines/TrustEngine.test.ts
describe('TrustEngine', () => {
  describe('calculateFreshness', () => {
    it('returns "fresh" when within staleAfterDays', () => {});
    it('returns "stale" when beyond staleAfterDays', () => {});
    it('returns "very_stale" when beyond 2x staleAfterDays', () => {});
    it('uses field-specific TTLs (hours stricter than descriptions)', () => {});
    it('factors in volatility (high volatility = stricter TTL)', () => {});
    it('generates correct warning copy for each level', () => {});
    it('returns showCTA=true when update action is available', () => {});
  });
});

// __tests__/engines/RouteEngine.test.ts
describe('RouteEngine', () => {
  describe('estimateWalkTime', () => {
    it('uses default speed for non-medina routes', () => {});
    it('applies medina multiplier for medina routes', () => {});
    it('uses precomputed matrix when available', () => {});
    it('falls back to haversine estimate when matrix missing', () => {});
  });
  describe('advanceRoute', () => {
    it('advances to next step correctly', () => {});
    it('handles skip and reflows remaining route', () => {});
    it('persists progress for resume after app kill', () => {});
  });
});
```

**TrustEngine golden file tests:**

```typescript
// __tests__/engines/TrustEngine.golden.test.ts
import goldenCases from './fixtures/trust-engine-golden.json';

describe('TrustEngine golden file tests', () => {
  goldenCases.forEach((testCase) => {
    it(`${testCase.name}`, () => {
      const result = TrustEngine.calculateFreshness(testCase.input);
      expect(result).toEqual(testCase.expected);
    });
  });
});
```

**Utilities and formatters:**

```typescript
// __tests__/utils/formatters.test.ts
describe('formatters', () => {
  describe('formatMAD', () => {
    it('formats currency correctly with thousands separator', () => {});
    it('handles zero and negative values', () => {});
  });
  describe('formatDistance', () => {
    it('shows meters for distances under 1km', () => {});
    it('shows km with 1 decimal for distances over 1km', () => {});
  });
  describe('formatDuration', () => {
    it('formats minutes correctly', () => {});
    it('formats hours and minutes correctly', () => {});
  });
  describe('normalizeSearchQuery', () => {
    it('normalizes Arabic-Indic digits to ASCII', () => {});
    it('lowercases and trims input', () => {});
    it('handles mixed Arabic/Latin text', () => {});
  });
});
```

### Integration tests (repositories + SQLite)

Test the data layer with real SQLite databases (in-memory or temp files).

```typescript
// __tests__/repositories/PlaceRepository.test.ts
describe('PlaceRepository', () => {
  let db: SQLiteDatabase;
  let repo: PlaceRepository;

  beforeEach(async () => {
    db = await openTestDatabase(); // in-memory SQLite
    await seedTestData(db);
    repo = new PlaceRepository(db);
  });

  afterEach(async () => {
    await db.closeAsync();
  });

  describe('getAll', () => {
    it('returns all places', async () => {});
    it('maps database rows to Place objects correctly', async () => {});
    it('parses JSON fields (aliases, tags, hours) correctly', async () => {});
  });

  describe('getById', () => {
    it('returns place by id', async () => {});
    it('returns null for non-existent id', async () => {});
  });

  describe('getByRegion', () => {
    it('filters by region_id', async () => {});
  });

  describe('getByCategory', () => {
    it('filters by category', async () => {});
  });

  describe('search', () => {
    it('finds places by name', async () => {});
    it('finds places by alias', async () => {});
    it('ranks exact matches higher than partial matches', async () => {});
    it('handles Arabic text correctly', async () => {});
    it('normalizes Arabic-Indic digits in query', async () => {});
  });
});

// __tests__/repositories/PriceCardRepository.test.ts
describe('PriceCardRepository', () => {
  // Similar structure to PlaceRepository
  describe('getByCategory', () => {});
  describe('search', () => {});
  describe('getWithModifiers', () => {
    it('parses context_modifiers JSON correctly', () => {});
  });
});

// __tests__/repositories/FavoritesRepository.test.ts
describe('FavoritesRepository', () => {
  describe('add', () => {
    it('adds favorite correctly', async () => {});
    it('prevents duplicate favorites', async () => {});
  });
  describe('remove', () => {
    it('removes favorite by content_type and content_id', async () => {});
  });
  describe('getAll', () => {
    it('returns favorites ordered by created_at desc', async () => {});
  });
  describe('isFavorite', () => {
    it('returns true for favorited items', async () => {});
    it('returns false for non-favorited items', async () => {});
  });
});
```

**FTS5 search tests:**

```typescript
// __tests__/services/SearchService.test.ts
describe('SearchService', () => {
  describe('FTS5 search', () => {
    it('finds results across places, prices, phrases', async () => {});
    it('applies normalization at query time', async () => {});
    it('handles prefix search correctly', async () => {});
    it('returns results ranked by relevance', async () => {});
    it('handles empty query gracefully', async () => {});
    it('handles special characters without crashing', async () => {});
  });

  describe('Arabic-Indic digit normalization', () => {
    it('normalizes ٠١٢٣٤٥٦٧٨٩ to 0123456789 at index time', async () => {});
    it('normalizes query with Arabic-Indic digits', async () => {});
    it('finds "50 MAD" when searching "٥٠"', async () => {});
  });

  describe('suggestions', () => {
    it('returns "Did you mean?" suggestions for typos', async () => {});
    it('suggests from aliases when no direct match', async () => {});
  });
});
```

**Database operations tests:**

```typescript
// __tests__/database/DatabaseManager.test.ts
describe('DatabaseManager', () => {
  describe('atomic swap', () => {
    it('swaps content.db atomically', async () => {});
    it('cleans up WAL/SHM files before swap', async () => {});
    it('rolls back on verification failure', async () => {});
    it('closes all connections before swap', async () => {});
    it('reopens connections after swap', async () => {});
  });

  describe('integrity verification', () => {
    it('passes PRAGMA quick_check on valid DB', async () => {});
    it('detects corrupted database', async () => {});
  });

  describe('migration', () => {
    it('applies user.db migrations in order', async () => {});
    it('handles migration failure gracefully', async () => {});
    it('does not run already-applied migrations', async () => {});
    it('migrates safely from N-1 to N with existing user state', async () => {});
    it('migrates safely from N-2 to N with chained migrations', async () => {});
  });
});
```

### Upgrade-path and migration matrix tests

Every release candidate must test real upgrade paths, not just fresh installs.

```typescript
// __tests__/upgrade/upgradeMatrix.test.ts
describe('Upgrade matrix', () => {
  it('upgrades N-1 -> N and preserves favorites/recents/homeBase/activeRoute', async () => {});
  it('upgrades N-2 -> N and applies chained migrations safely', async () => {});
  it('keeps installed packs and registry state consistent after upgrade', async () => {});
  it('rolls back safely to last-known-good state if migration fails', async () => {});
});
```

### Component tests (React Native Testing Library)

Test critical UI components in isolation.

```typescript
// __tests__/components/FairnessMeter.test.tsx
import { render, screen } from '@testing-library/react-native';

describe('FairnessMeter', () => {
  it('renders "Great Price" for low fairness level', () => {
    render(<FairnessMeter level="low" />);
    expect(screen.getByText(/great price/i)).toBeTruthy();
  });

  it('renders "Fair" with correct color for fair level', () => {});
  it('renders "High" with warning color for high level', () => {});
  it('renders "Very High" with destructive color for very_high level', () => {});
  it('shows confidence note when provided', () => {});
});

// __tests__/components/CompassArrow.test.tsx
describe('CompassArrow', () => {
  it('rotates arrow based on relative angle', () => {});
  it('shows distance in meters when < 1km', () => {});
  it('shows distance in km when >= 1km', () => {});
  it('shows calibration needed state', () => {});
  it('shows heading confidence indicator', () => {});
});

// __tests__/components/PriceTag.test.tsx
describe('PriceTag', () => {
  it('renders price range correctly', () => {});
  it('shows "Last reviewed" date', () => {});
  it('shows staleness warning when old', () => {});
  it('formats MAD correctly with locale', () => {});
});

// __tests__/components/OfflineBanner.test.tsx
describe('OfflineBanner', () => {
  it('renders when offline', () => {});
  it('hides when online', () => {});
  it('shows "Core guide still works" message', () => {});
});

// __tests__/components/OpenNowChip.test.tsx
describe('OpenNowChip', () => {
  it('shows "Open now" when currently open', () => {});
  it('shows "Closed" when currently closed', () => {});
  it('hides when no hours data available', () => {});
  it('handles timezone correctly', () => {});
});
```

**Share card snapshot tests:**

```typescript
// __tests__/components/ShareCardRenderer.test.tsx
describe('ShareCardRenderer', () => {
  it('renders place share card correctly', () => {
    const tree = render(<ShareCardRenderer type="place" data={mockPlace} />);
    expect(tree.toJSON()).toMatchSnapshot();
  });

  it('renders price card share card correctly', () => {
    const tree = render(<ShareCardRenderer type="price_card" data={mockPriceCard} />);
    expect(tree.toJSON()).toMatchSnapshot();
  });

  it('renders quote result share card correctly', () => {
    const tree = render(<ShareCardRenderer type="quote_result" data={mockQuoteResult} />);
    expect(tree.toJSON()).toMatchSnapshot();
  });
});
```

### Hook tests

```typescript
// __tests__/hooks/useQuoteAction.test.ts
import { renderHook, act } from '@testing-library/react-hooks';

describe('useQuoteAction', () => {
  it('calculates fairness when quote is entered', () => {});
  it('updates result when context modifiers change', () => {});
  it('saves quote to recents', () => {});
  it('handles quantity changes correctly', () => {});
});

// __tests__/hooks/useHomeBase.test.ts
describe('useHomeBase', () => {
  it('loads saved home base on mount', () => {});
  it('saves home base to user.db', () => {});
  it('calculates distance and bearing when location available', () => {});
  it('handles missing location gracefully', () => {});
});

// __tests__/hooks/useRoute.test.ts
describe('useRoute', () => {
  it('loads active route on mount', () => {});
  it('advances to next stop', () => {});
  it('handles skip correctly', () => {});
  it('persists progress across app restarts', () => {});
  it('calculates next stop distance and bearing', () => {});
});

// __tests__/hooks/useNetworkState.test.ts
describe('useNetworkState', () => {
  it('returns online when connected', () => {});
  it('returns offline when disconnected', () => {});
  it('detects Wi-Fi vs cellular', () => {});
  it('updates when network state changes', () => {});
});
```

### E2E tests (Maestro)

Define critical user journeys that must pass before any release.

**Directory structure:**

```
maestro/
├── flows/
│   ├── 01-fresh-install-offline.yaml
│   ├── 02-explore-and-price-check.yaml
│   ├── 03-quote-action-flow.yaml
│   ├── 04-home-base-setup.yaml
│   ├── 05-go-home-compass.yaml
│   ├── 06-my-day-builder.yaml
│   ├── 07-route-cards-execution.yaml
│   ├── 08-phrasebook-search.yaml
│   ├── 09-download-pack-flow.yaml
│   ├── 10-content-update-flow.yaml
│   ├── 11-low-storage-recovery.yaml
│   ├── 12-permission-denial-paths.yaml
│   ├── 13-iap-unlock-and-restore.yaml
│   └── 14-missing-optional-pack-fallback.yaml
├── utils/
│   └── common-assertions.yaml
└── config.yaml
```

**Critical E2E scenarios:**

```yaml
# maestro/flows/01-fresh-install-offline.yaml
# Scenario: App works offline immediately after fresh install
appId: com.marrakechcompass.app
---
- launchApp:
    clearState: true
- toggleAirplaneMode: true  # Enable airplane mode
- assertVisible: "Home"
- tapOn: "Explore"
- assertVisible: "Places"  # Content loads from bundled DB
- tapOn:
    index: 0  # First place
- assertVisible: "Details"
- tapOn: "Prices"
- assertVisible: "Price Cards"
- tapOn:
    index: 0  # First price card
- assertVisible: "Expected range"
- tapOn: "Quote → Action"
- assertVisible: "Enter quoted price"
- inputText: "50"
- tapOn: "Check"
- assertVisible: "Fairness"  # Result shows
- toggleAirplaneMode: false  # Disable airplane mode

# maestro/flows/03-quote-action-flow.yaml
# Scenario: Quote → Action provides correct guidance
appId: com.marrakechcompass.app
---
- launchApp
- tapOn: "Quote → Action"
- tapOn: "Taxi"
- assertVisible: "Short ride"
- tapOn: "Short ride"
- inputText: "30"
- tapOn: "Check"
- assertVisible: "Fair"
- assertVisible: "Expected range"
- assertVisible: "Negotiation scripts"
- inputText: "150"  # Change to high quote
- tapOn: "Check"
- assertVisible: "Very High"
- assertVisible: "Counter-offer"

# maestro/flows/04-home-base-setup.yaml
# Scenario: User can set and use Home Base
appId: com.marrakechcompass.app
---
- launchApp
- tapOn: "Go Home"
- assertVisible: "Set your Home Base"
- tapOn: "Set Home Base"
- inputText: "Riad Fes"
- tapOn: "Search"
- tapOn:
    index: 0  # First result
- tapOn: "Confirm"
- assertVisible: "Home Base saved"
- tapOn: "Go Home"
- assertVisible: "Compass"
- assertVisible: "Distance"

# maestro/flows/07-route-cards-execution.yaml
# Scenario: User can follow an itinerary with Route Cards
appId: com.marrakechcompass.app
---
- launchApp
- tapOn: "More"
- tapOn: "Itineraries"
- tapOn: "1-day first timer"
- assertVisible: "Route overview"
- tapOn: "Start route"
- assertVisible: "Next stop"
- assertVisible: "Distance"
- tapOn: "Mark as done"
- assertVisible: "Next stop"  # Advances to step 2
- tapOn: "Skip"
- assertVisible: "Next stop"  # Advances to step 3
- runFlow: "kill-and-relaunch"  # Simulate app kill
- assertVisible: "Continue route"  # Progress persisted
- tapOn: "Continue route"
- assertVisible: "Next stop"  # Still on step 3

# maestro/flows/09-download-pack-flow.yaml
# Scenario: Download pack with interruption and resume
appId: com.marrakechcompass.app
---
- launchApp
- tapOn: "Settings"
- tapOn: "Downloads"
- tapOn: "Medina Pack"
- assertVisible: "Download"
- tapOn: "Download"
- assertVisible: "Downloading"
- waitForAnimationEnd
- delay: 2000  # Let download start
- tapOn: "Pause"
- assertVisible: "Paused"
- tapOn: "Resume"
- assertVisible: "Downloading"
- runFlow: "kill-and-relaunch"  # Simulate app kill
- tapOn: "Settings"
- tapOn: "Downloads"
- assertVisible: "Resume"  # Download state persisted
- tapOn: "Resume"
- waitForAnimationEnd: { timeout: 60000 }
- assertVisible: "Installed"

# maestro/flows/12-permission-denial-paths.yaml
# Scenario: App remains usable when permissions denied
appId: com.marrakechcompass.app
---
- launchApp:
    clearState: true
- tapOn: "Go Home"
- tapOn: "Set Home Base"
- inputText: "Riad"
- tapOn: "Search"
- tapOn:
    index: 0
- tapOn: "Confirm"
- tapOn: "Go Home"
# System permission dialog appears
- tapOn: "Don't Allow"  # Deny location
- assertVisible: "Location not available"
- assertVisible: "Copy address"  # Fallback still works
- assertVisible: "Show taxi driver"  # Fallback still works
- assertNotVisible: "Compass"  # Compass hidden without permission

# maestro/flows/13-iap-unlock-and-restore.yaml
# Scenario: One-time unlock + restore behaves correctly
appId: com.marrakechcompass.app
---
- launchApp:
    clearState: true
- assertVisible: "Preview"
- tapOn: "Unlock full Marrakech"
- runFlow: "iap-sandbox-purchase-success"  # helper flow
- assertVisible: "Unlocked"
- runFlow: "kill-and-relaunch"
- assertVisible: "Unlocked"  # entitlement persisted
- tapOn: "Restore purchases"
- assertVisible: "Purchase restored"
- toggleAirplaneMode: true
- assertVisible: "Unlocked"  # offline relaunch still unlocked
- toggleAirplaneMode: false

# maestro/flows/14-missing-optional-pack-fallback.yaml
# Scenario: Missing optional pack never creates a dead-end
appId: com.marrakechcompass.app
---
- launchApp:
    clearState: true
- tapOn: "More"
- tapOn: "Itineraries"
- tapOn: "1-day first timer"
- tapOn: "Start route"
- assertVisible: "Offline map pack not installed"
- assertVisible: "Continue with compass guidance"  # Level 0 fallback
- assertVisible: "Download pack"
```

### Security and integrity tests

```typescript
// __tests__/services/ContentSyncService.test.ts
describe('ContentSyncService', () => {
  describe('manifest verification', () => {
    it('accepts valid Ed25519 signature', async () => {});
    it('rejects invalid signature', async () => {});
    it('rejects expired manifest', async () => {});
    it('rejects manifest with releasedAt older than stored', async () => {});
    it('rejects manifest without signature', async () => {});
  });

  describe('content verification', () => {
    it('accepts file with matching sha256', async () => {});
    it('rejects file with mismatched sha256', async () => {});
    it('rejects corrupted download', async () => {});
  });

  describe('atomic update', () => {
    it('activates new content after verification', async () => {});
    it('rolls back on verification failure', async () => {});
    it('keeps previous version for rollback', async () => {});
  });
});

// __tests__/services/PackRegistry.test.ts
describe('PackRegistry', () => {
  describe('install', () => {
    it('registers pack in user.db after install', async () => {});
    it('is idempotent (same pack can be reinstalled)', async () => {});
    it('updates version when pack is upgraded', async () => {});
  });

  describe('reconcile', () => {
    it('detects missing pack files and marks for repair', async () => {});
    it('detects orphan files and cleans up', async () => {});
    it('auto-rolls back corrupted pack to previous version', async () => {});
  });

  describe('uninstall', () => {
    it('removes pack files and registry entry', async () => {});
    it('keeps dependencies if other packs need them', async () => {});
  });
});
```

### IAP and entitlement tests (Option B required)

If monetization is Option B, purchase and restore flows are release-critical.

```typescript
// __tests__/services/IAPService.test.ts
describe('IAPService', () => {
  it('unlocks full content after successful purchase', async () => {});
  it('restores entitlement after reinstall on same store account', async () => {});
  it('persists unlocked entitlement for offline relaunch', async () => {});
  it('handles pending/deferred transactions without duplicate unlocks', async () => {});
  it('keeps preview content usable when store APIs are unavailable', async () => {});
});
```

### Fault-injection (chaos) tests for offline reliability

```typescript
// __tests__/chaos/contentActivation.chaos.test.ts
describe('Content activation chaos', () => {
  it('survives process kill during download, verify, and swap', async () => {});
  it('handles ENOSPC during unpack with clear recovery UX', async () => {});
  it('recovers when WAL/SHM files are unexpectedly present', async () => {});
  it('repairs filesystem/registry mismatch on next launch', async () => {});
});
```

### Performance tests

Define performance budgets and enforce them.

Use two layers:
- CI smoke performance tests (quick regression signals)
- Device-level release profiling (authoritative gate on real hardware)

For release gates, measure on **physical release builds** and store p50/p95 across >=30 cold launches per reference device.

**Budgets:**

| Metric | Target | Device Reference |
|--------|--------|------------------|
| Cold start | < 2000ms | iPhone 11 / Pixel 4a |
| Search response (p95) | < 100ms | iPhone 11 / Pixel 4a |
| Quote → Action calculation | < 50ms | iPhone 11 / Pixel 4a |
| Compass animation FPS | ≥ 55 fps | iPhone 11 / Pixel 4a |
| Memory (Explore list) | < 150 MB | Any |
| Memory (Map view) | < 200 MB | Any |

**Performance test implementation:**

```typescript
// __tests__/performance/startup.perf.test.ts
describe('Startup performance', () => {
  it('cold start completes within budget', async () => {
    const startTime = performance.now();
    await launchApp({ clearState: true });
    await waitForElement('Home');
    const duration = performance.now() - startTime;
    expect(duration).toBeLessThan(2000);
  });
});

// __tests__/performance/search.perf.test.ts
describe('Search performance', () => {
  it('search returns results within budget', async () => {
    const results = [];
    for (let i = 0; i < 100; i++) {
      const start = performance.now();
      await searchService.search('tajine');
      results.push(performance.now() - start);
    }
    const p95 = percentile(results, 95);
    expect(p95).toBeLessThan(100);
  });
});

// __tests__/performance/memory.perf.test.ts
describe('Memory usage', () => {
  it('Explore list stays within memory budget', async () => {
    await navigateTo('Explore');
    await scrollToEnd();
    const memory = await getMemoryUsage();
    expect(memory.usedJSHeapSize).toBeLessThan(150 * 1024 * 1024);
  });
});
```

**Authoritative device instrumentation (release gates):**
- iOS: Xcode Instruments + MetricKit (startup, hangs, memory)
- Android: Macrobenchmark/Perfetto (startup, jank/FPS, memory)
- Persist reports as CI artifacts and compare against previous release

### Offline simulation tests

Test offline behavior in CI without real network.

```typescript
// __tests__/offline/gracefulDegradation.test.ts
describe('Offline graceful degradation', () => {
  beforeEach(() => {
    jest.spyOn(NetInfo, 'fetch').mockResolvedValue({
      isConnected: false,
      isInternetReachable: false,
    });
  });

  it('Explore screen renders with cached data', async () => {
    render(<ExploreScreen />);
    expect(await screen.findByText('Places')).toBeTruthy();
    expect(screen.queryByText('Loading...')).toBeNull();
  });

  it('shows offline banner', async () => {
    render(<ExploreScreen />);
    expect(await screen.findByText(/offline/i)).toBeTruthy();
  });

  it('Quote → Action works without network', async () => {
    render(<QuoteActionScreen />);
    // ... full flow test
  });

  it('hides weather widget when offline', async () => {
    render(<HomeScreen />);
    expect(screen.queryByTestId('weather-widget')).toBeNull();
  });

  it('shows cached events with "Last updated" label', async () => {
    render(<EventsScreen />);
    expect(await screen.findByText(/last updated/i)).toBeTruthy();
  });
});
```

### Privacy and permission contract tests

```typescript
// __tests__/privacy/permissionsContract.test.ts
describe('Permission contract', () => {
  it('does not prompt location until user taps Near Me/Go Home/Navigate', async () => {});
  it('keeps core flows usable when location permission is denied', async () => {});
  it('redacts precise coordinates from debug report export', async () => {});
  it('fails CI if contacts/photos permissions are introduced', async () => {});
});
```

### Localization tests

```typescript
// __tests__/localization/translations.test.ts
import en from '../src/locales/en.json';
import fr from '../src/locales/fr.json';
import es from '../src/locales/es.json';
import de from '../src/locales/de.json';
import it from '../src/locales/it.json';
import nl from '../src/locales/nl.json';

const locales = { en, fr, es, de, it, nl };

describe('Translations', () => {
  const enKeys = getAllKeys(en);

  Object.entries(locales).forEach(([locale, translations]) => {
    if (locale === 'en') return;

    describe(`${locale} locale`, () => {
      it('has all keys from English', () => {
        const localeKeys = getAllKeys(translations);
        const missingKeys = enKeys.filter(k => !localeKeys.includes(k));
        expect(missingKeys).toEqual([]);
      });

      it('has no extra keys not in English', () => {
        const localeKeys = getAllKeys(translations);
        const extraKeys = localeKeys.filter(k => !enKeys.includes(k));
        expect(extraKeys).toEqual([]);
      });

      it('has no empty string values', () => {
        const emptyKeys = getKeysWithEmptyValues(translations);
        expect(emptyKeys).toEqual([]);
      });
    });
  });
});

// __tests__/localization/rtl.test.ts
describe('RTL layout', () => {
  it('Arabic text renders right-to-left', () => {
    render(<PhraseDetail phrase={arabicPhrase} />);
    const arabicText = screen.getByTestId('arabic-text');
    expect(arabicText.props.style).toContainEqual({ textAlign: 'right' });
  });

  it('Large text mode shows Arabic correctly', () => {
    render(<LargeTextCard phrase={arabicPhrase} />);
    // Snapshot to catch layout regressions
    expect(screen.toJSON()).toMatchSnapshot();
  });
});

// __tests__/localization/fallback.test.ts
describe('Translation fallback', () => {
  it('falls back to English when translation missing', () => {
    i18n.changeLanguage('fr');
    // Assume 'rare_key' exists in en but not fr
    const result = i18n.t('rare_key');
    expect(result).toBe(en.rare_key);
  });

  it('never shows empty string or key name', () => {
    i18n.changeLanguage('fr');
    const result = i18n.t('common.save');
    expect(result).not.toBe('');
    expect(result).not.toBe('common.save');
  });
});
```

### Time, timezone, and calendar edge tests

```typescript
// __tests__/time/openNowAndFreshness.test.ts
describe('Open-now and freshness edge cases', () => {
  it('handles DST transitions in Africa/Casablanca correctly', () => {});
  it('handles timezone changes while app is running', () => {});
  it('applies Ramadan/holiday exceptions over weekly hours', () => {});
  it('keeps staleness labels correct across local date boundaries', () => {});
});
```

### Content validation tests (CI)

```typescript
// shared/scripts/validate-content.test.ts
import { validatePlaces, validatePriceCards, validateItineraries } from './validate-content';
import places from '../content/places.json';
import priceCards from '../content/price_cards.json';
import itineraries from '../content/itineraries.json';

describe('Content validation', () => {
  describe('Places', () => {
    it('all places pass schema validation', () => {
      const result = validatePlaces(places);
      expect(result.success).toBe(true);
    });

    it('all places have required fields', () => {
      places.items.forEach(place => {
        expect(place.id).toBeDefined();
        expect(place.name).toBeDefined();
        expect(place.short_description).toBeDefined();
        expect(place.category).toBeDefined();
      });
    });

    it('all places have reviewedAt date', () => {
      places.items.forEach(place => {
        expect(place.reviewed_at).toMatch(/^\d{4}-\d{2}-\d{2}$/);
      });
    });

    it('coordinates are valid (when present)', () => {
      places.items.forEach(place => {
        if (place.lat !== null) {
          expect(place.lat).toBeGreaterThanOrEqual(-90);
          expect(place.lat).toBeLessThanOrEqual(90);
        }
        if (place.lng !== null) {
          expect(place.lng).toBeGreaterThanOrEqual(-180);
          expect(place.lng).toBeLessThanOrEqual(180);
        }
      });
    });

    it('price ranges are valid (min <= max)', () => {
      places.items.forEach(place => {
        if (place.expected_cost_min_mad !== null && place.expected_cost_max_mad !== null) {
          expect(place.expected_cost_min_mad).toBeLessThanOrEqual(place.expected_cost_max_mad);
        }
      });
    });
  });

  describe('Price Cards', () => {
    it('all price cards pass schema validation', () => {
      const result = validatePriceCards(priceCards);
      expect(result.success).toBe(true);
    });

    it('all price cards have updatedAt', () => {
      priceCards.items.forEach(card => {
        expect(card.expected_cost_updated_at).toBeDefined();
      });
    });

    it('price ranges are valid', () => {
      priceCards.items.forEach(card => {
        expect(card.expected_cost_min_mad).toBeLessThanOrEqual(card.expected_cost_max_mad);
      });
    });
  });

  describe('Reference integrity', () => {
    it('itinerary steps reference valid place IDs', () => {
      const placeIds = new Set(places.items.map(p => p.id));
      itineraries.items.forEach(itinerary => {
        itinerary.steps.forEach(step => {
          if (step.place_id) {
            expect(placeIds.has(step.place_id)).toBe(true);
          }
        });
      });
    });

    it('related_price_card_ids in tips are valid', () => {
      const priceCardIds = new Set(priceCards.items.map(p => p.id));
      // Similar validation for tips
    });

    it('all internal links are valid', () => {
      // Validate content_links references
    });
  });
});
```

### CI configuration

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: TypeScript type-check
        run: npm run typecheck
      
      - name: ESLint
        run: npm run lint
      
      - name: Validate content schema
        run: npm run validate:content
      
      - name: Check reference integrity
        run: npm run check:links
      
      - name: Build content.db
        run: npm run build:content
      
      - name: Verify content.db matches shared/content
        run: npm run verify:content-db

  test:
    runs-on: ubuntu-latest
    needs: validate
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Unit tests
        run: npm run test:unit -- --coverage
      
      - name: Integration tests
        run: npm run test:integration
      
      - name: Component tests
        run: npm run test:components
      
      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          file: ./coverage/lcov.info

  build:
    runs-on: ubuntu-latest
    needs: test
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Check forbidden permissions
        run: npm run check:permissions
      
      - name: EAS Build (preview)
        run: eas build --profile preview --platform all --non-interactive
        env:
          EXPO_TOKEN: ${{ secrets.EXPO_TOKEN }}

  e2e:
    runs-on: macos-latest
    needs: build
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4
      
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
      
      - name: Install Maestro
        run: curl -Ls "https://get.maestro.mobile.dev" | bash
      
      - name: Download preview build
        run: eas build:download --latest --platform ios --output ./app.tar.gz
        env:
          EXPO_TOKEN: ${{ secrets.EXPO_TOKEN }}
      
      - name: Extract app
        run: tar -xzf app.tar.gz
      
      - name: Run E2E tests
        run: maestro test maestro/flows/
```

### CI lane strategy (fast feedback + full confidence)

- **PR fast lane (<15 min):** typecheck, lint, unit/integration/component tests, content validation, permission checks, and critical Maestro smoke flows (`01`, `03`, `12`, `14`)
- **Nightly full lane:** full Maestro suite + upgrade matrix + IAP sandbox + chaos tests + device-level performance profiling
- **Release candidate lane:** run nightly suite against the exact release build artifact before submit
- Publish failure artifacts: videos/screenshots, app logs, test reports, perf traces

### Test flake policy

- Auto-retry failing E2E/perf tests once (infra noise guard)
- Track flaky tests by owner and flake rate
- If flake rate >2% over 7 days: quarantine test + create fix ticket
- Quarantined tests run nightly but do not gate PRs; critical-flow tests cannot remain quarantined at release time

### Test commands (package.json)

```json
{
  "scripts": {
    "test": "jest",
    "test:unit": "jest --testPathPattern='__tests__/(engines|utils|hooks)'",
    "test:integration": "jest --testPathPattern='__tests__/(repositories|database|services)'",
    "test:components": "jest --testPathPattern='__tests__/components'",
    "test:upgrade": "jest --testPathPattern='__tests__/upgrade|__tests__/database/.*migration'",
    "test:iap": "jest --testPathPattern='__tests__/iap|__tests__/services/IAPService'",
    "test:chaos": "jest --testPathPattern='__tests__/chaos'",
    "test:performance": "jest --testPathPattern='__tests__/performance'",
    "test:offline": "jest --testPathPattern='__tests__/offline'",
    "test:privacy": "jest --testPathPattern='__tests__/privacy'",
    "test:localization": "jest --testPathPattern='__tests__/localization'",
    "test:time": "jest --testPathPattern='__tests__/time'",
    "test:e2e": "npm run test:e2e:full",
    "test:e2e:critical": "maestro test maestro/flows/01-fresh-install-offline.yaml maestro/flows/03-quote-action-flow.yaml maestro/flows/12-permission-denial-paths.yaml maestro/flows/14-missing-optional-pack-fallback.yaml",
    "test:e2e:smoke": "maestro test maestro/flows/01-fresh-install-offline.yaml",
    "test:e2e:full": "maestro test maestro/flows/",
    "test:nightly": "npm run test && npm run test:upgrade && npm run test:iap && npm run test:chaos && npm run test:e2e:full",
    "validate:content": "ts-node shared/scripts/validate-content.ts",
    "check:links": "ts-node shared/scripts/check-links.ts",
    "check:permissions": "ts-node shared/scripts/check-permissions.ts",
    "build:content": "ts-node shared/scripts/build-bundle.ts",
    "verify:content-db": "ts-node shared/scripts/verify-content-db.ts"
  }
}
```

### Pre-release checklist (manual QA)

In addition to automated tests, complete this checklist before every store submission:

**Offline behavior:**
- [ ] Fresh install works in airplane mode
- [ ] All tabs render with content
- [ ] Search works offline
- [ ] Quote → Action works offline
- [ ] Go Home compass works offline
- [ ] Route Cards work offline
- [ ] Core screens remain usable when optional packs are missing (clear fallback + Downloads CTA)
- [ ] Downloads resume after app kill

**Platform-specific:**
- [ ] iOS: VoiceOver reads all interactive elements
- [ ] iOS: Dynamic Type scales correctly (all sizes)
- [ ] iOS: Swipe-back gesture works
- [ ] Android: TalkBack reads all interactive elements
- [ ] Android: Font scaling works correctly
- [ ] Android: Back button behavior is correct
- [ ] Android: Doze mode doesn't break downloads

**Edge cases:**
- [ ] Low storage: clear error message, no crash
- [ ] Permission denied: app still usable
- [ ] No location prompt appears before explicit user intent (Near Me / Go Home / Navigate)
- [ ] Content update interrupted: safe recovery
- [ ] App killed during route: progress persists
- [ ] Upgrade path N-1 -> N preserves user state + pack registry
- [ ] Upgrade path N-2 -> N applies chained migrations safely
- [ ] DST/timezone changes do not break Open now and freshness labels
- [ ] Very long place names: text doesn't overflow
- [ ] Empty search results: helpful message

**Monetization (Option B):**
- [ ] Unlock purchase succeeds in sandbox on iOS and Android
- [ ] Restore purchases works after reinstall
- [ ] Unlocked entitlement is honored offline after relaunch
- [ ] Preview-only path still delivers useful offline value

**Visual:**
- [ ] Dark mode: all screens look correct
- [ ] RTL Arabic text: renders correctly
- [ ] Large text mode: readable on taxi driver card
- [ ] Share cards: look good when shared

---

## 13) Store listing strategy (so paid installs convert)

Your App Store / Play Store copy must **prove value before purchase**:

**Positioning line:**
"The offline Marrakech guide you can trust — prices, navigation, and cultural confidence."

- "Fair prices in MAD + negotiation scripts"
- "Offline-first: works without internet"
- "Avoid common scams"
- "Darija phrases + etiquette"
- "Curated must-sees + itineraries"

Screenshots should highlight:

- Works offline (airplane mode screenshot)
- Offline Medina navigation (not just pins)
- Fair prices in MAD + negotiation scripts
- No subscriptions / no ads / no data selling
- Quote → Action + Go Home + Route Cards (shows "confidence in the moment")
- Shareable Price Card "snapshot" (helps marketing + word-of-mouth)
- Arrival mode + converter (shows "paid utility" immediately)

---

## 14) What to build first (order of implementation, not milestones)

### Phase 0: Foundation

1. **Expo project setup**
   - Initialize Expo project with TypeScript template: `npx create-expo-app marrakechCompass --template expo-template-blank-typescript`
   - Install `expo-dev-client` for development builds with native module access
   - Configure EAS Build (`eas.json`) with development, preview, and production profiles
   - Set up ESLint, Prettier, and TypeScript strict mode with path aliases
   - Configure Metro bundler and Jest for testing

2. **Shared content pipeline**
   - JSON schema + Zod validation scripts
   - `build-bundle.ts` script (JSON → SQLite `content.db`)
   - Treat `shared/content/` as the source of truth for most app data
   - `copy-db-to-assets.ts` to copy content.db to `assets/seed/`
   - Seed content for development (5 places, 5 price cards, 20 phrases)

3. **App foundation**
   - Install and configure core Expo dependencies:
     - Navigation: `@react-navigation/native`, `@react-navigation/native-stack`, `@react-navigation/bottom-tabs`
     - Database: `expo-sqlite`
     - Storage: `expo-file-system`, `@react-native-async-storage/async-storage`
     - Location: `expo-location`, `expo-sensors`
     - UI: `react-native-reanimated`, `react-native-gesture-handler`, `react-native-screens`
   - Set up DatabaseManager with `expo-sqlite` wrapper
   - Create basic theme + design system components (Marrakech terracotta palette)
   - Implement bottom tab navigation structure
   - Create first development build and test on iOS Simulator and Android Emulator

### Phase 1: Core features

4. Integrate generated `content.db` (from `shared/content/`) via `expo-asset`, then implement content loading + favorites/recents
5. Explore list + place detail
6. Prices list + price card detail (this is the money-maker)
7. **Quote → Action** (reuses Price Cards; high value)
8. Darija phrasebook + search (FTS5 via `expo-sqlite`)
9. Itineraries + tips/culture pages

### Phase 2: Location features

10. **Home Base compass** (`expo-location` + `expo-sensors` magnetometer for heading; big confidence win)
11. **My Day** plan builder (offline daily plan)
12. **Route Cards** (execute itineraries with next-stop guidance)
13. Map integration + external directions (`react-native-maps` with expo-dev-client + `expo-linking` for external maps)

### Phase 3: Polish & store readiness

14. Store-ready polish (screenshots, App Store video, copy)
15. Downloads manager (audio packs, content updates via `expo-file-system`)
16. Offline UX polish, error states, empty states
17. Accessibility audit (VoiceOver / TalkBack)
18. Localization (EN/FR/ES/DE/IT/NL UI with `react-i18next` + `expo-localization`)
19. EAS Submit configuration for App Store / Play Store

### Phase 4: Backend (optional)

20. Phase 2 Convex: content versioning + bundle downloads + optional user sync

---


## 15) Phase 2 Convex: exact "needs to be built"

- Convex schema: content tables + `contentVersions`
- Upload pipeline for curated content (could be manual at first)

**Expo sync module (TypeScript):**
- `ContentSyncService.ts` using native `fetch` for manifest + bundle downloads
- Resumable download support via `expo-file-system` `createDownloadResumable()`
- Verify sha256 using `expo-crypto`
- Atomic DB swap using `expo-file-system` (`FileSystem.moveAsync()`)
- FTS tables must be prebuilt in downloaded content.db (no runtime index creation)

**Sync flow:**
- Read latest version from Convex via HTTP/Convex client
- Compare with cached version (stored in AsyncStorage)
- Download manifest + bundle using `expo-file-system`
- Verify hash/signature before import using `expo-crypto`
- Close all SQLite connections via `expo-sqlite`
- Perform atomic file swap (keep previous version for rollback)
- Reopen SQLite connections

- Optional auth + user state sync (favorites/bookmarks) via Convex

---

## 16) Shared code & development workflow

### What's shared (everything!)

With Expo React Native, almost all code is shared between iOS and Android:

**Shared TypeScript code (in `src/` directory):**
- All UI code (React Native components)
- All business logic (hooks, context, engines)
- Database access layer (`expo-sqlite` wrapper)
- Services (`expo-location`, `expo-file-system`, sync)
- Engines (pricing, planning, routing, geo)
- Navigation
- Theme and styling

**Shared content (in `shared/` directory):**
- Content JSON files (places, prices, phrases, itineraries, tips, culture)
- Content validation scripts (TypeScript/Node with Zod)
- SQLite database build scripts (JSON → content.db)
- JSON Schema definitions
- Content changelog generation
- Asset pipeline (image compression, audio encoding)

**Platform-specific (minimal, managed by Expo):**
- `ios/` - Generated by `expo prebuild`, Xcode project
- `android/` - Generated by `expo prebuild`, Gradle project
- Platform-specific configuration in `app.json` / `app.config.js`
- Config plugins for native customization (permissions, splash screens)

### Development workflow

1. **Content updates:** Edit JSON in `shared/content/`, run validation, build `content.db`, copy to `assets/seed/`
2. **Development:** Run `npx expo start` to start Metro bundler with Expo Dev Tools
3. **Development build:** Create with `eas build --profile development --platform ios` (or android)
4. **iOS testing:** Run development build on iOS Simulator or physical device
5. **Android testing:** Run development build on Android Emulator or physical device
6. **Unit testing:** Run `npm test` for Jest tests (engines, hooks, utilities)
7. **E2E testing:** Use Maestro for end-to-end tests on both platforms
8. **Release:** Build with EAS and submit via EAS Submit

### Development commands

```bash
# Start Expo development server
npx expo start

# Start with dev client (for native modules)
npx expo start --dev-client

# Create development build (iOS)
eas build --profile development --platform ios

# Create development build (Android)
eas build --profile development --platform android

# Run on iOS simulator (after installing dev build)
npx expo start --ios

# Run on Android emulator (after installing dev build)
npx expo start --android

# Run tests
npm test

# Build content.db from JSON
npm run build:content

# Lint and type-check
npm run lint
npm run typecheck

# Generate native projects (for debugging native code)
npx expo prebuild

# Build production release (iOS)
eas build --profile production --platform ios

# Build production release (Android)
eas build --profile production --platform android

# Submit to App Store
eas submit --platform ios

# Submit to Play Store
eas submit --platform android
```

### Code quality checklist

Maintain quality across the single codebase:
- [ ] TypeScript strict mode with no `any` types in production code
- [ ] All engines have unit tests with >90% coverage
- [ ] All screens tested on both iOS and Android
- [ ] No platform-specific code without `Platform.OS` checks
- [ ] Accessibility labels on all interactive elements
- [ ] No console warnings in release builds

### CI gates (required for "paid quality")

See **Section 12b (Test Strategy)** for complete test definitions and CI configuration.

**On every commit:**
- TypeScript type-check passes (`tsc --noEmit`)
- ESLint passes with no errors

**On every PR:**
- Unit tests pass with >90% coverage on engines (Jest)
- Integration tests pass (repositories + SQLite)
- Component tests pass (React Native Testing Library)
- Critical E2E smoke flows pass (`01`, `03`, `12`, `14`)
- Validate content schema + references (`npm run validate:content`)
- Build `content.db` and ensure it includes required tables + FTS tables
- Verify `assets/seed/content.db` is the latest version generated from `shared/content/`
- Forbidden-permissions check: fail if contacts/photos permissions appear in `app.json`
- EAS Build succeeds on both iOS and Android (use `eas build --profile preview`)

**On merge to main:**
- Full E2E suite passes (Maestro all flows)
- Upgrade matrix + IAP + chaos suites pass
- Device-level performance tests pass budgets on reference devices
- Generate changelog artifact for in-app "What's new" + store notes

### Trust & reliability gates (additions)

- Pack integrity test: verify manifests + sha256 + install/uninstall flows (simulated)
- Offline smoke test: core flows must work in airplane mode (Maestro `01-fresh-install-offline.yaml`)
- Security tests: signature verification, hash validation, replay prevention
- Automated E2E scenarios (Maestro) on CI:
  - `01-fresh-install-offline.yaml`: airplane mode install → explore → price card → quote → phrasebook
  - `04-home-base-setup.yaml` + `12-permission-denial-paths.yaml`: home base with permission denied path
  - `09-download-pack-flow.yaml`: pack install interrupted → resume → verify → activate
  - `13-iap-unlock-and-restore.yaml`: purchase unlock + restore + offline entitlement check
  - `14-missing-optional-pack-fallback.yaml`: missing optional pack still allows fallback guidance
  - `07-route-cards-execution.yaml`: route progress persists after app kill
- Localization tests: all translations complete, RTL rendering correct, fallback works

### Release-blocker policy (explicit)

Do not ship if any of the following fail:
- Any P0/P1 bug remains open
- Critical E2E flows fail after one retry
- Crash-free/ANR thresholds regress past targets
- Upgrade, rollback, or chaos tests show possible data loss
- Device-level performance budgets fail on reference hardware

### Schema-driven codegen (recommended)

- Generate TypeScript types + Zod validators from shared JSON schema
- CI gate: fail if generated types are out of date vs schema changes

---

## 17) Definition of "done"

The app is "ready to sell" when:

- It works great offline on both iOS and Android
- Pricing + negotiation content feels trustworthy (ranges + reviewed date)
- It's curated enough to feel premium (not empty, not bloated)
- Tourists can plan a day, move around, eat well, negotiate, and avoid traps
- Quote → Action, Go Home, My Day, and Route Cards work reliably offline (core "confidence" moments)
- Store pages (App Store + Play Store) clearly communicate the value in 5 seconds
- Offline promise is validated via a repeatable test checklist (airplane mode + interrupted update + low storage)
- Both platforms pass accessibility audits (VoiceOver + TalkBack)
- Option B (free preview + one-time unlock) implemented: IAP + restore works; preview pack delivers real value; paywall appears after user experiences core features
- Expo app performs smoothly on mid-tier devices (no jank, fast startup)
- No JS errors or yellow boxes in release builds
- Same user experience on iOS and Android (single codebase advantage)
- EAS Build produces valid App Store / Play Store binaries
- EAS Submit successfully uploads to both stores
