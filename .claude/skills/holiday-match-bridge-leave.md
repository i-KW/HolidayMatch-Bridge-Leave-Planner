---
name: holiday-match-bridge-leave
description: Generate multi-country holiday comparison calendars with AI-powered bridge leave plans. Fetches official holiday data, parallel multi-source verification, generates color-coded HTML calendars, and calculates optimal annual leave strategies.
metadata:
  tags: calendar, holiday, travel, multi-country, bridge-leave
---

# HolidayMatch · Holiday Comparison & Bridge Leave Planner

## Trigger

When a user asks to create a holiday calendar for two countries, or to add a new country pair to the HolidayMatch project.

---

## Workflow

### 0. Time Awareness — Dynamic Year Detection

Identify time clues in the user's request — avoid hardcoding a fixed year:

- **Vague expressions**: Recognize phrases like "next week", "next month", "soon". Use WebSearch to confirm the current date, then calculate the target month.
- **Distance judgment**:
  - Target is **≤1 month away** → default to this year, proceed directly
  - Target is **≥2 months away** → proactively ask "this year or next year?"
- **December cross-year prompt**: If current month is December, prompt "Would you like to include early next year as well?"
- If user says "next year", auto-increment year by +1.

> **Goal**: Align with real planning scenarios (last-minute vs. advance planning), reduce irrelevant output.

### 1. Parallel Research — Multi-Source Concurrent Retrieval + Cross-Validation

> Each country and each source fetched independently in parallel — no serial waiting.

**Parallel dimensions** (simultaneous):
- **By country**: Agent A → Country 1 holidays / Agent B → Country 2 holidays
- **By source**: For the same country, concurrently search government sites + calendar sites + timeanddate.com
- **By year**: If multiple years needed (e.g. this year + next year), search years in parallel

**Cross-validation mechanism**:
- Same date appears in multiple sources → ✅ High confidence
- Single source only → ⚠️ Medium confidence, note the source
- Conflicting sources → ❓ Flag as needs verification, run additional search

> **Note**: Islamic/lunar holidays (Eid al-Fitr, Chinese New Year, etc.) shift annually on the Gregorian calendar. WebSearch with the specific year is required — do not rely on model memory.

> **Benefits**: 2× speed, reduced context interference, improved accuracy

### 2. Determine the Standard Yearly Calendar

Generate the 12-month calendar grid based on the **Gregorian Calendar + ISO 8601 week standard**. Fill in holidays only after the day-of-week alignment is correct.

| Item | Standard |
|------|----------|
| Calendar system | Gregorian Calendar |
| Week starts | **Monday → Sunday** (consistent with existing templates) |
| Days per month | Jan 31 / Feb 28(29 leap) / Mar 31 / Apr 30 / May 31 / Jun 30 / Jul 31 / Aug 31 / Sep 30 / Oct 31 / Nov 30 / Dec 31 |
| Leap year rule | Divisible by 4 and not by 100, OR divisible by 400 |
| Day-of-week calculation | Use WebSearch for "{year} calendar" to get full year grid, or use algorithms (Zeller / Tomohiko Sakamoto) |
| Verification | WebSearch "{year} calendar printable" and spot-check Jan 1 and a few key dates |

**Important**: Generate the empty monthly grid with correct day-of-week alignment first, then populate holidays and labels.

### 3. Generate Calendar HTML

Follow the exact structure of the existing templates:

- **Single-file HTML** — zero dependencies
- **Color coding**:
  - Country A = green (`class="uk"` or `class="cn"`)
  - Country B = orange/blue (`class="es"` or `class="ie"`)
  - Both = purple (`class="both"`)
  - Regional = red (`class="regional"`)
  - Make-up workdays = red background (`class="work"`)
  - Weekend = light blue tint (`class="weekend"`)
- **Month-by-month table** with day-of-week alignment
- **Cell labels**: emoji + short holiday name
- **Month header**: summary of holidays + shared holiday indicator (➡ M/D 🟣 Both)
- **English primary**, add local language as secondary where appropriate

### 4. Special Rules & Regional Variations

The following rules must be considered when generating calendars and bridge leave plans:

| Rule | Countries | Description |
|------|-----------|-------------|
| **Make-up workdays (调休)** | 🇨🇳 China | Weekend work to compensate for long holidays — mark as "补班/调班" |
| **Substitute Bank Holiday** | 🇬🇧 UK | Holiday on weekend → moved to following Monday |
| **Regional Holidays** | 🇪🇸 Spain | Jueves Santo / Lunes de Pascua vary by autonomous community |
| **Puente (Bridge)** | 🇪🇸 Spain | Holiday on Tue/Thu → locals take Mon/Fri off to bridge |
| **振替休日 (Furikae Kyujitsu)** | 🇯🇵 Japan | Holiday on Sunday → moved to Monday |
| **国民の休日 (Kokumin no Kyujitsu)** | 🇯🇵 Japan | Mid-week day becomes a holiday if sandwiched between two holidays |
| **대체공휴일 (Substitute Holiday)** | 🇰🇷 Korea | Holiday on weekend → moved to next weekday |
| **Pont (Bridge)** | 🇫🇷 France | Holiday on Thursday → take Friday off, similar to Spanish puente |
| **Feiertage (Federal system)** | 🇩🇪 Germany | Each state has different holidays — no single national list |
| **Floating holidays** | Multiple | Islamic (Eid) and Lunar (CNY, Mid-Autumn) dates shift yearly. Must WebSearch with specific year. Do not rely on model recall. |
| **Federal vs State** | 🇺🇸 US | Federal holidays vs state-observed holidays differ |

### 5. Verification Safety Net — Confidence Markers & Source Transparency

> Don't fake certainty — honestly expose the boundaries.

- **Confidence levels**:
  - ✅ High: multiple sources agree + government site confirmed
  - ⚠️ Medium: third-party sources agree but no official doc found
  - ❓ Needs verification: conflicting sources or single source only
- **Source transparency**: Note source link or type (gov / media / calendar site) beside each date
- **AI-generated marker**: Clearly label bridge leave tips as "AI-generated suggestions, for reference only"
- **Disclaimer**: Floating holiday dates (Islamic/lunar) may vary ±1 day due to moon sighting or official announcement

> **Goal**: Let users know the reliability level of each piece of information, rather than pretending all information is equally certain. An honest "uncertain" is more valuable than a fake "certain".

### 6. Summary Section
- Annual holiday summary table per country (including make-up workday counts)
- **Overlapping holidays table** (mark 🟣)
- Regional variation notes

### 7. Bridge Leave Guide
Calculate optimal annual leave strategies:
- For each holiday cluster: days of leave needed → total consecutive days off
- **Highlight the best deal**: `style="background:#fff8e1;"` on the row with the longest continuous break
- Format: "Take X days leave → Y days off"
- Consider cross-country suggestions (e.g. when Country A is on holiday but B isn't, A can visit B)

### 8. Sources & Footer
- Link to official sources (gov.uk, BOE, etc.)
- Last updated timestamp (use WebSearch for current date)
- Regional variation / floating holiday disclaimers

---

## Output Spec
- Filename: `{Country1}＆{Country2}_HolidayMatch_Calendar.html`
- Saved in project root
- Confirm with user before pushing to GitHub

## Reference Templates
- `China＆Ireland_HolidayMatch_Calendar.html` — Chinese work-swap (调休) pattern
- `UK＆Spain_HolidayMatch_Calendar.html` — English/Spanish, regional holiday notes

## Product Principles
- **Side-by-side comparison** — see both countries' holidays at a glance
- **Practical value first** — bridge leave tips are the killer feature, not just a calendar
- **Zero friction** — single HTML, no install, print-friendly
- **Shareable** — can be dropped into a group chat or family shared document
