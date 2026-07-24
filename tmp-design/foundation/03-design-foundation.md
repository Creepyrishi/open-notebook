# 03 · Design Foundation — Variant I "Quiet Green"

Canonical token system distilled from `style-tiles/i-quiet-green.html` (canon)
and the nine `concepts-h/` screens, tie-broken by `02-ux-architecture.md`.
Single source of truth: [`tokens.css`](tokens.css) — written to seed the app's
`globals.css`. Validation: [Appendix B](#appendix-b--re-application-test).

Precedence used throughout: **decisions log > canon tile > concept-screen
plurality (newest screens win among concepts)**.

---

## The Laws

1. **Fern acts.** `--primary` (#2E6B4F) is THE action color — New, Add Source,
   Write Note, Send, active states. Nothing else gets to look clickable-green.
2. **Teal speaks.** `--teal` (#0E7268) is the AI/system voice — chat, insights,
   AI badges, source-evidence citations, the focus ring, text selection.
3. **Red destroys.** `--danger` (#B0432D) appears only on destructive actions
   and errors. It is never an accent, never a highlight, never a badge.
4. **Warn is clay, never the action hues.** Degraded states (stale citation,
   broken link, degraded provenance) wear `--clay` (#B0451F) — an orange clay
   deliberately distinct from danger red. Warn never borrows fern/teal/gold.
5. **Color never washes a reading surface.** Panels and cards stay neutral
   (`--surface`); hues live in dots, ticks, chips, and spines. The single
   sanctioned exception: the teal evidence washes (`--excerpt-wash`,
   `--best-match`) on cited passages.
6. **One shadow token, and popovers own it.** `--shadow-pop` is the only true
   shadow in the system; only popovers may use it. Overlay sheets use
   `--shadow-overlay`; everything else is hairline borders plus at most
   `--shadow-soft`/`--shadow-lift`. Hairlines separate, shadows don't.
7. **Geometry is 4–6px.** Squared instrument, not toy: panels 6px, cards and
   controls 5px, chips 4px. Floor is 4px — nothing sharper, nothing rounder.
   "Pills" are squared too (`--r-pill: 4px`).
8. **Mono is for data.** `--font-mono` renders locators, chunk markers, counts,
   URLs, receipts, kbd — never prose. Display face is for identity moments
   (hero, wordmark); body face does everything else.
9. **Dark overrides raws only.** `.dark` on `<html>` redefines the palette,
   semantic raws, and shadows; every `var()` alias re-resolves by itself.
   Never duplicate aliases into the dark block.

---

## Token Reference

### 1 · Core palette

| Token | Light | Dark | Owns |
|---|---|---|---|
| `--fern` / `-deep` / `-tint` | #2E6B4F / #245740 / #DFEAE2 | #55B285 / #6CC298 / #1B2F25 | action |
| `--sage` / `-deep` / `-tint` | #5E7A54 / #47603F / #E5EBDC | #93B084 / #A8C299 / #232B1D | web / gathering |
| `--gold` / `-deep` / `-tint` | #A97B12 / #7C5A05 / #F3EAD3 | #CFA13E / #DDB55F / #322B1B | notes / pdf (honey) |
| `--teal` / `-deep` / `-tint` | #0E7268 / #095A51 / #DDECE8 | #3FB3A5 / #64C5B9 / #16302C | AI / system voice |
| `--plum` / `-tint` | #5D4991 / #EAE6F3 | #A290D3 / #29253A | video; seasoning (model chip, kbd) |
| `--mauve` / `-deep` / `-tint` | #8D5B80 / #714566 / #F1E5EE | #C892BA / #D6A8CB / #322230 | audio |
| `--slate` / `-deep` / `-tint` | #4E6B84 / #3A5468 / #E1E8EE | #8FAFC8 / #A5C1D6 / #212B34 | paper / external |
| `--violet` / `-deep` / `-tint` | #6E51A6 / #57408A / #EBE5F5 | #A995DB / #BCAAE6 / #2B2540 | derived insight (≠ audio mauve) |
| `--clay` / `-deep` / `-tint` | #B0451F / #93330F / #F5E4DB | #F08A5C / #F5A07A / #35211A | warn / degraded |

### 2 · Semantic

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bg` | #F5F5F2 | #17181B | app canvas |
| `--bg-deep` | #EEEEE9 | #121316 | recessed canvas (rails, wells) |
| `--surface` | #FEFEFC | #1E2024 | panels, cards — reading surface |
| `--surface-raised` | #FFFFFF | #24262B | hovers, popovers, inputs |
| `--surface-recessed` | #F4F4F0 | #24262B | recessed area within a panel |
| `--surface-sunken` | #ECECE7 | #2B2D33 | deepest step (kbd, inner wells) |
| `--ink` | #23252A | #ECEDEA | primary text |
| `--ink-soft` | #565A61 | #A9ACB1 | secondary text |
| `--ink-faint` | #878B92 | #74777D | metadata, placeholders |
| `--ink-faintest` | #A8ABB1 | #63666C | disabled, ghost glyphs |
| `--line` | #E0E0DA | #2E3036 | hairline borders |
| `--line-soft` | #E8E8E2 | #26282D | sub-separators |
| `--line-strong` | #23252A | #ECEDEA | emphasis border = ink |
| `--primary` / `-hover` | #2E6B4F / #245740 | #3D8E67 / #479E74 | THE action color |
| `--on-primary` | #F1F8F3 | #ECF7F0 | text on primary |
| `--danger` / `-deep` / `-tint` | #B0432D / #93341F / #F5E4DF | #DF7C63 / #E9937D / #37231D | destructive/error only |
| `--warn` / `-deep` / `-tint` | → clay | → clay | degraded, never destructive |
| `--focus-ring` | `0 0 0 3px var(--teal-tint)` | (auto) | keyboard focus |

### 3 · Content-type hues (dots, ticks, chips only — never washes)

| Token | Alias of | | Token | Alias of |
|---|---|---|---|---|
| `--type-video` | plum | | `--type-paper` | slate |
| `--type-pdf` | gold | | `--type-note` | gold |
| `--type-web` | sage | | `--type-ai` / `--type-insight` | teal |
| `--type-audio` | mauve | | *each with* `-soft` | matching `-tint` |

### 4 · Evidence classes (citations)

One pill skeleton, one distinguishing dress per class (06-citations):

| Token | Alias / value | Chip dress |
|---|---|---|
| `--cite-source` | teal | solid dot + number |
| `--cite-note` | gold | solid gold dot — authoral |
| `--cite-derived` | violet | violet dot; popover carries breadcrumb to original |
| `--cite-external` | slate | dashed border, hollow ring dot, receipt + "Add as source" |
| `--cite-synthesis` | ink-faint | hollow dot — claims without a direct span |
| `--cite-warn` | clay | stale/degraded dress |
| `--excerpt-wash` | #ECF3F0 / #1C2A28 | cited-passage background (sanctioned wash) |
| `--best-match` / `--best-match-ring` | rgba(teal .16 / .20) | best-match sentence highlight |

### 5 · Context states (per-source inclusion)

| Token | Alias | Meaning |
|---|---|---|
| `--ctx-full` / `-tint` | fern | full content in context (solid green spine) |
| `--ctx-insights` / `-tint` | gold | insights-only |
| `--ctx-off-ink` / `--ctx-off-bg` | ink-soft / surface-raised | excluded — no spine, dimmed |

### 6–8 · Shape, type, space

- **Radii**: `--r-xl` 6px (panels/overlays) · `--r-lg` 5px · `--r-md` 5px
  (cards/controls) · `--r-sm` 4px (chips) · `--r-pill` 4px.
- **Faces**: display "Bricolage Grotesque" · body "Instrument Sans" · mono
  `ui-monospace, "SF Mono", "Cascadia Mono", Menlo`.
- **Scale**: hero 24 · title 15.5 · body 13.5 · small 12 · micro 10.5 (px).
- **Space**: `--sp-1..7` = 4 / 8 / 10 / 14 / 18 / 22 / 28 px.

### 9–10 · Depth & motion

| Token | Light | Dark |
|---|---|---|
| `--shadow-soft` | 0 1px 2px rgba(35,37,42,.06) | 0 1px 2px rgba(0,0,0,.35) |
| `--shadow-lift` | 0 1px 3px rgba(35,37,42,.10) | 0 1px 3px rgba(0,0,0,.45) |
| `--shadow-pop` *(popovers only)* | 0 1px 2px …,08 + 0 8px 26px …,13 | …,45 + 0 10px 30px …,5 |
| `--shadow-overlay` *(modal sheets)* | 0 2px 6px …,10 + 0 16px 44px …,18 | 0 2px 6px …,4 + 0 20px 52px …,55 |

Motion: `--motion-fast` .12s (small hovers) · `--motion-base` .15s (controls) ·
`--motion-slow` .25s (theme cross-fade, large surfaces) · `--ease: ease`.

---

## Component Inventory (implied by the mockups)

| Component | Anatomy (one line) | Specced by |
|---|---|---|
| **AppShell / NavRail** | fixed left rail: wordmark, Create button, nav items, Manage disclosure, footer utilities (theme, language, sign out) | 00, 01 |
| **CreateButton** | the one solid-fern button (`--primary` + `--on-primary`), kbd hint chip | 00–08 |
| **SourceCard + spine** | 5px card, left 3px spine = context state (fern full / gold insights / none+dimmed off); title, one metadata line (TypeBadge + insight count), ⋮ overflow | 01, 02 |
| **ContextChip (ctx-state)** | compact chip showing only current state FULL/INSIGHTS/OFF + cycle glyph, same position on every card; notes binary | 01 |
| **ContextSelection bar** | "4 in context · Auto" scope strip over the conversation: Auto/Full/Insights/Excluded | 01, 04 |
| **TypeBadge** | micro chip: type glyph + label in the type hue on its `-soft` tint | 01, 02, 08 |
| **HueTick** | tiny square/dot of a type or evidence hue — the only color a neutral surface carries | 00, 03, 08 |
| **PanelHeader** | small-caps title + hue tick, collapse chevron, tinted panel action | 01 |
| **CitationChip (cite)** | inline pill: class dot + sequential number; dresses: solid (source), gold (note), violet (derived), dashed+hollow (external), hollow (synthesis), clay (stale), line-through (broken), stacked (multi) | 06 |
| **EvidencePopover** | the only `--shadow-pop` surface; chunky variant: pinned header (source, locator) + scrolling excerpt with fade masks + pinned footer ("Open source →") | 06 |
| **CitedChunk** | reading passage on `--excerpt-wash` with gutter marker; `--best-match` sentence highlight | 06 |
| **ChunkMarker** | mono micro label "chunk 7/12 · cited in 2 answers" with teal dot | 06 |
| **EvidenceBundle (receipt strip)** | end-of-answer strip "3 sources · 1 note · 8 passages", expands as inline accordion | 06, 04 |
| **AnswerCard + SaveAsNote** | notebook-voiced answer block; actions: Save as Note (fern ghost), Copy | 01, 04, 06 |
| **ChatComposer** | input on `--surface-raised`, scope chips, fern send button | 01, 04 |
| **NoteCard** | gold-ticked card, "AI generated" teal badge variant, edited-ago metadata, FULL/OFF chip | 01 |
| **CaptureBar** | one-line "Capture a thought…" input with fern submit | 01 |
| **CreationCard / RecipeTile** | creation type tile (podcast, mind map, study guide…) with hue tick + mono metadata | 03, 05 |
| **CreateOverlay** | modal sheet on `--shadow-overlay`, `--r-xl`, recipe grid | 05 |
| **ModelChip / Kbd** | plum-seasoned mono chips (gpt-…, ⌘J) | 00, 01 |
| **SearchResult row** | type tick + title + mono locator + notebook breadcrumb | 08 |
| **ResearchTimeline** | deep-research stepper: numbered mono phases, per-question promotion rows | 07 |
| **ThemeToggle / banner** | concept-only chrome (tile banner, screen switcher) — not product | all |

---

## Appendix A — Drift Report (Task 1)

Three token generations exist across the ten files:
**Gen A** = 00-home, 01-notebook (older names: `--canvas/--raised/--hairline/
--ink-2/-3/--r-panel/--font-sans/--fs-meta/--c-*`; larger spacing) ·
**Gen B** = 02, 03, 05 · **Gen C** = 04, 08 · **Gen D** = 06, 07 (newest;
adds violet, shadow-pop, evidence washes).

Disagreements and rulings (canonical value in **bold**):

| # | Token | Values seen | Ruling |
|---|---|---|---|
| 1 | `--fs-hero` | 26px (canon tile, 04, 08) vs **24px** (02, 03, 05, 06, 07) | **RATIFIED 2026-07-24: 24px.** Application screens win over the style tile. tokens.css, 04, 08 and the canon tile updated to 24px. |
| 2 | spacing `--sp-3..7` | **10/14/18/22/28** (canon + 7) vs 12/16/20/24/32 (Gen A) | Canon wins; 00/01 must re-adopt. |
| 3 | `--ink-faint` | **#878B92** (canon + 7) vs #A8ABB1 (Gen A) | Canon wins. Gen A's value is a genuine 4th ramp step → admitted as new token `--ink-faintest` (#A8ABB1 / #63666C). |
| 4 | dark metadata ink | canon dark `--ink-faint` **#74777D** vs Gen A dark `--ink-3` #84878D | Canon wins (light values matched exactly); fix 00/01 dark. |
| 5 | `--slate` (paper/external) | #54718D (A) / #54708B (B) / #5A6B7E (C) / **#4E6B84** (D) | Canon silent, decisions log names slate but no hex → judgment call: the evidence-spec screens (06/07, newest) win. |
| 6 | `--clay` (warn) | #B0432D =danger (B, C) vs **#B0451F** (D) | Law 4: warn must be clay, distinct from danger red. B/C drifted by aliasing clay to danger. Danger stays **#B0432D** per canon. |
| 7 | `--violet` (derived) | only in 06/07: **#6E51A6** | Decisions log ruling — canonical; distinct from audio mauve #8D5B80. |
| 8 | pdf hue | c-honey #B08420 (A) / honey #9C6B1B (C) vs **gold #A97B12** | **RATIFIED 2026-07-24: pdf and notes share gold #A97B12.** Screens A/C corrected. Revisit only if the pdf/note distinction ever matters at tick size — then mint a deliberate `--honey` token instead of ad-hoc values. |
| 9 | `--focus-ring` | teal rgba (A) / fern tint+ring (B) / **`0 0 0 3px var(--teal-tint)`** (C, D) | **RATIFIED 2026-07-24: focus ring is teal** (`0 0 0 3px var(--teal-tint)`) — teal-as-system-voice reading confirmed over "fern acts". Screens A/B corrected. |
| 10 | `--font-mono` | 3 orderings | **`ui-monospace, "SF Mono", "Cascadia Mono", Menlo, monospace`** (A + D). |
| 11 | `--shadow-overlay` | 3 variants (A / B / 05) | **05-create-overlay's** — the screen that specs overlays. |
| 12 | `--shadow-card` | .05 alpha (A) vs `--shadow-soft` .06 | Collapsed into **`--shadow-soft`**. |
| 13 | `--slate-tint`, `--clay-tint`, `--shadow-lift` | ±1-digit / whitespace variants | Canonical formatting; values from the winning file per rows 5–6. |
| 14 | `--fs-md` 14.5px (Gen A) | defined, never used | Dropped from canon. |
| 15 | Gen A naming | canvas/raised/hairline/ink-2/ink-3/r-panel/r-card/r-ctl/font-sans/fs-meta/fs-title(=hero)/c-\* | Pure name drift → canonical names; see validate/ adapter for the full mapping. |

Deliberate per-file extras kept out of canon: none — everything recurring was
promoted (evidence washes, violet, shadow-pop) or dropped as unused (fs-md,
`--offset-*: none` in the tile).

---

## Appendix B — Re-application Test (Task 3)

Method: `validate/01-notebook.tokenized.html` and
`validate/06-citations.tokenized.html` are byte-copies of the originals whose
local `:root`/`.dark` blocks are replaced by `<link …/tokens.css>` plus a
names-only adapter (01) / empty adapter (06). Screenshotted headless Chromium,
1440px, full-page, both themes, over a local HTTP server; pixel-compared with
PIL (visible = channel delta > 8).

**Re-run 2026-07-24 — post-ratification, corrections applied to the screens.**
The drift corrections of Appendix A (rows 1–2, 4–6, 8–9, 12, 15) were applied
to the concepts-h screens and the canon tile, the tokenized copies were
regenerated from the corrected screens, and the diff re-run. No "classified
drift" allowances remain — the screens now ARE the canon:

| Screen | Theme | any-delta px | visible px |
|---|---|---|---|
| 01-notebook | light | 0.009 % | 0.000 % |
| 01-notebook | dark | 0.000 % | 0.000 % |
| 06-citations | light | 0.000 % | 0.000 % |
| 06-citations | dark | 0.000 % | 0.000 % |

Residue: 01-light's 0.009 % is 134 sub-visible pixels (channel delta ≤ 8) plus
exactly one pixel at delta 14, deterministic across runs, localized to two
anti-aliased edges (a rounded control corner and a dashed gold border's dash
phase). It is a Chromium rasterization artifact of applying identical tokens
via `<link>` vs inline `<style>` — not token drift; a self-vs-self reshoot of
the same file diffs at 0.000 %.

<details>
<summary>Historical: first run (2026, pre-correction) — resolved</summary>

Raw diff then: 01-notebook 19.29/15.36 % (light), 19.83/14.85 % (dark);
06-citations 15.89/12.11 % (light), 15.83/11.79 % (dark) — dominated by
text-reflow ghosting from hero-size and spacing drift. A diagnostic run with
each screen's classified drifts pinned back reached 0.000–0.006 % any-delta,
proving every differing pixel was accounted for by Appendix A rows 1
(hero — since ratified at 24px), 2 (spacing), 4 (dark metadata ink), 5 (slate),
6 (warn/clay), 8 (pdf gold), 12 (card shadow) plus the token gaps
(`--ink-faintest`, `--surface-recessed/-sunken`, `--line-soft`) that were
admitted into tokens.css before that run. All of these are now fixed in the
screens themselves.
</details>
