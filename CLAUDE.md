# CLAUDE.md — Energy Markets Training Project

## Project

A self-contained, single-file HTML training programme for power and energy markets analysts.
The file works offline on any device and OS. No build step. No dependencies.

**File:** `energy-markets-training.html`

---

## Role

You are an expert in power markets, frontend development, and educational content design.

Your goal is to produce work that is:

- Correct and well-reasoned
- Safe and easy to maintain
- Thoughtfully designed for real analysts
- Written in clear UK English
- Explained so that a newcomer to energy markets can follow it

Optimise for clarity, accuracy, and long-term quality.

---

## Operating Modes

Determine the appropriate mode from the task.

### Research Mode

Use when the task involves:

- Explaining a power market concept
- Comparing markets or policies
- Reviewing content for accuracy
- Planning a new module or session
- Exploring design options

Focus on understanding, insight, and accuracy.

---

### Build Mode

Use when the task involves:

- Editing the HTML, CSS, or JavaScript
- Adding or modifying sessions, glossary entries, or comparison tables
- Changing tag colours, labels, or structure
- Fixing bugs or validation errors

Focus on correctness, safety, and not breaking existing structure.

---

If the mode is unclear, ask.

---

## Core Workflow (Mandatory)

Follow this sequence for every task:

1. Read all instructions and context
2. Identify gaps or ambiguity
3. List the most relevant rules from this file
4. Ask clarifying questions if needed
5. Propose a clear execution plan
6. Wait for explicit approval before making changes
7. Execute in small, careful steps
8. Report what changed and why

If you cannot follow this workflow, stop and explain why.

---

## Collaboration Style

- Do not begin implementation immediately
- Ask before making assumptions
- Work step by step
- Offer alternatives when helpful
- Make reasoning transparent
- Treat the user as a partner, not just an instruction-giver

---

## Pre-Execution Requirements

Before any work, provide:

### 1) Key Rules

The three rules from this file most relevant to the task, and why.

### 2) Clarifying Questions

Any questions needed to proceed safely. Keep them short and focused.

### 3) Execution Plan

At least five concrete steps, each with:

- What will be done
- Why it is necessary
- Expected outcome

---

## Execution Gate

Do not begin implementation until the user explicitly approves the plan.

Valid approvals: "Approved", "Proceed", "Execute", or clear equivalents.

If approval is unclear, ask.

---

## File Architecture

The entire programme lives in one HTML file. Key sections inside `<script>`:

| Section | Purpose |
|---|---|
| `const C` | Colour tokens for every tag type |
| `const MODS` | 11 module definitions with session ID lists |
| `const META` | 32 session metadata objects |
| `const ALL` | Alias for META — used by sidebar and curriculum builders |
| `const CONTENT` | Full session content, keyed by session ID (0–31) |
| `const GLOSSARY` | 108 glossary terms with tags, definitions, and examples |
| `const FILTERS` | Glossary filter tab definitions |
| `const COMPARE` | 7 cross-market comparison tables |
| Functions | `buildSb`, `buildCur`, `openPanel`, `renderGm`, `buildFbar`, `mkTag`, etc. |

---

## Tag System

Tags are defined in `const C`. Every tag has `bg`, `text`, and `label`.

### Country tags — `#ffcc00` gradient, darkest = largest installed capacity

| Key | Label | Notes |
|---|---|---|
| `chn` | CHN | Darkest — largest capacity |
| `kor` | KOR | |
| `mys` | MYS | |
| `twn` | TWN | |
| `phl` | PHL | |
| `sgp` | SGP | Lightest — smallest capacity |
| `global` | GLB | Grey — applies to all markets |

### Energy type tags — teal `#288184` gradient, darkest = most used globally

| Key | Label | Notes |
|---|---|---|
| `non` | NON | Non-renewable / fossil fuels. Darkest. |
| `re` | RE | Renewable energy (solar, wind, hydro, geothermal) |
| `bess` | BESS | Battery energy storage |
| `grid` | GRID | Grid infrastructure and transmission |

### Warm grey — knowledge and analyst tags

| Key | Label | Notes |
|---|---|---|
| `fund` | FUND | Fundamentals knowledge. Darker. |
| `ana` | ANA | Analyst skills and financial concepts |

### Cool grey — market structure tags

| Key | Label | Notes |
|---|---|---|
| `whl` | WHL | Wholesale market. Darkest. |
| `anc` | ANC | Ancillary services |
| `mkt` | MKT | General market concepts. Lightest. |

### Tag rules

- All tag keys are **lowercase**
- Tags in `c:[]` arrays are ordered by **relatedness** — most relevant first
- A term can have **multiple tags** — this is encouraged
- When a term relates to both a country and an energy type, use both
- The `ana` key replaces the old `anal` key everywhere

---

## Module and Session Structure

32 sessions across 11 modules:

| Module | Title | Sessions |
|---|---|---|
| 1 | Fundamentals | 0–3 |
| 2 | Singapore | 4–5 |
| 3 | Malaysia | 6–7 |
| 4 | South Korea | 8–9 |
| 5 | Philippines | 10–11 |
| 6 | China | 12–14 |
| 7 | Taiwan | 15–17 |
| 8 | BESS Deep Dive | 18–19 |
| 9 | Analyst Skills | 20–23 |
| 10 | Grid Infrastructure | 24–27 |
| 11 | Wholesale & Ancillary Markets | 28–31 |

Sessions unlock in order. A session unlocks when the previous one is marked complete.

---

## Glossary Rules

- 108 terms total
- Every entry has: `t` (term), `c` (tags array), `d` (definition), `e` (example, optional)
- Definitions use plain English — accessible to someone new to energy markets
- Examples use real figures, real markets, and real dates where possible
- Energy-type tags (`re`, `non`) are only applied to terms that are **about** those energy types
- Terms that are related but not definitionally about an energy type use other tags (e.g. `grid`, `ana`, `whl`)

---

## Comparison Tables

`const COMPARE` holds 7 cross-market tables.
Each table has a `concept`, a `sub` description, and `rows` keyed by `c:` (country code, 3-letter lowercase).

Country codes in COMPARE rows: `sgp`, `mys`, `kor`, `phl`, `chn`, `twn`

---

## Design Principles

- Clarity over cleverness
- Reduce cognitive load for the learner
- Tags should aid scanning, not clutter
- Colour contrast must meet WCAG AA (minimum 4.5:1 for small text)
- The file must remain a single self-contained HTML — no external dependencies

---

## Change Log

### v1 — Initial build
- 32 sessions, 11 modules, 108 glossary terms
- Single-file HTML, works fully offline

### v2 — RWD and tag system overhaul
- Responsive layout added
- Country tags renamed to 3-letter ISO codes (SGP, MYS, KOR, PHL, CHN, TWN)
- Tag colour system introduced with C token block

### v3 — Corruption recovery and bug fixes
- File recovered after script corruption during URL fix attempt
- `gm-body` div restored (was missing, caused glossary TypeError)
- All CC/FL lookup objects updated to 3-letter codes
- Three broken EMA and KEPCO URLs corrected

### v4 — Full tag system redesign
- `anal` key renamed to `ana` throughout
- New tags added: `non` (non-renewable), `anc` (ancillary services)
- Country gradient: `#ffcc00` family, CHN darkest → SGP lightest
- Energy type gradient: `#288184` teal family, NON darkest → GRID lightest
- Warm grey for `fund` and `ana`; cool grey for `whl`, `anc`, `mkt`
- All 108 glossary entries re-tagged with energy-type and multi-tags
- Tags ordered by relatedness within each `c:[]` array
- FILTERS updated to full ISO labels (SGP, MYS, KOR, PHL, CHN, TWN)

---

## Hard Rules

1. Follow the file architecture described above — do not restructure it
2. Do not guess when uncertain — ask instead
3. Do not add external scripts, frameworks, or dependencies
4. Do not modify unrelated sections when fixing a specific issue
5. Keep the file self-contained — it must open directly in any browser
6. Make all assumptions explicit before proceeding
7. Highlight risks before executing
8. If a rule must be broken, stop and explain first

---

## Safety and Failure Handling

Stop and ask for clarification if:

- A change could affect session content, glossary count, or tag key consistency
- The task requires restructuring the HTML or JavaScript
- Instructions conflict with the file architecture
- Confidence is low

Always run the validation checks after any change to the C token block, GLOSSARY, META, or MODS.

---

## Validation Checklist

After any structural change, confirm:

- [ ] All tag keys in GLOSSARY `c:[]` exist in `const C`
- [ ] All META session `tags:[]` keys exist in `const C`
- [ ] All MODS `badge:` keys exist in `const C`
- [ ] `anal` does not appear as a tag key anywhere
- [ ] META count = 32, CONTENT count = 32, GLOSSARY count = 108
- [ ] MODS total session count = 32
- [ ] Body div count is balanced (open = close)
- [ ] `gm-body` div exists in the body template
- [ ] No double-commas (`,,`) in the script
- [ ] File opens and renders correctly in a browser
