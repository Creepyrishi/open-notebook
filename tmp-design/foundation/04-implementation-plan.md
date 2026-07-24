# Stage 1 — Reskin implementation plan (Direction I "Quiet Green")

> 2026-07-24. Scope: apply the ratified visual identity to the CURRENT app —
> no behavior changes, no new interaction patterns (those are Stage 2, per
> REDESIGN_BRIEF: "new patterns must not be built on the legacy layout" — and
> conversely, the reskin must not smuggle Stage-2 UX in).
> Inputs: `foundation/tokens.css` (canon, validated), `03-design-foundation.md`
> (laws + component inventory), the 9-screen prototype as visual reference.

## Ground rules

- Small PRs, one concern each, screenshot before/after in the PR description.
- Both themes hand-checked on every PR (`theme-store` mechanism unchanged).
- i18n untouched; no copy changes except where a screen pass explicitly says so.
- Each PR keeps `npm run lint` + `npm run test` + `npm run build` green.
- Visual QA: compare against the prototype screen where one exists; where it
  doesn't (Models, Settings, Podcasts), apply tokens + laws, not invention.

## PR sequence

### PR 1 — Design tokens land in `globals.css`
Port `foundation/tokens.css` into `frontend/src/app/globals.css`:
- Replace the stock shadcn values of the semantic vars (`--background`,
  `--foreground`, `--card`, `--primary`, `--border`, `--ring`, `--radius`…)
  with the I equivalents (light `:root` + `.dark`), converting to the file's
  existing oklch convention or keeping hex (decide in-PR; oklch preferred for
  consistency).
- Add the product token layers under `@theme inline` / custom properties:
  content-type hues (`--type-video`…), evidence classes (`--cite-*`) and
  context states (`--ctx-*`) — unused by components yet, but canonized now so
  Stage 2 and community PRs can consume them.
- Fonts: swap Geist → Bricolage Grotesque (display) + Instrument Sans (UI) +
  keep a mono (Spline Sans Mono) via `next/font` with fallbacks; wire
  `--font-sans`/`--font-mono`/new `--font-display`.
- Radius: `--radius` 0.65rem → 6px scale (cards 5–6, controls 4–5).
Acceptance: app boots, every screen renders in both themes with the new
palette; no component code touched. Expect it to look 70% right and reveal
hard-coded colors — inventory them for PR 2/3, don't fix here.

### PR 2 — Primitives + living styleguide
- Restyle the shadcn primitives to the I laws: Button (fern primary, quiet
  secondary, danger only destructive), Card (1px border, no default shadow),
  Dialog (single shadow token, 6px radius, breathing room — fixes the cramped
  modals), Badge/Chip (neutral shell + colored dot idiom), Tabs (underline
  style, kill the pill triple-split), Input/Select (teal focus ring), Tooltip,
  DropdownMenu.
- Add `/dev/design` (dev-only route): renders all tokens + primitives in both
  themes. This is the review tool for every later PR.
- Sweep the hard-coded color inventory from PR 1 into tokens.
Acceptance: `/dev/design` matches the foundation doc; app-wide look ~90%.

### PR 3 — Shell: sidebar + top-level chrome
Current IA stays (Collect/Process/Create/Manage, Ask page stays — Stage 2
kills it). Apply: logo/wordmark (fern/gold/teal mark), nav active state (fern
spine), MANAGE-style quiet grouping, bottom utilities, collapsed-sidebar
behavior unchanged.

### PR 4 — Notebook workspace (visual only)
Spacing/typography/panel treatment per prototype 01 MINUS Stage-2 patterns:
no context chips, no Notes/Creations split, no composer mode switcher. Panel
headers get hue ticks; source cards get the one-line metadata + ⋮ top-right
(pure layout, no new behavior); existing full/insights context dropdown stays
as-is functionally, restyled only. Collapsible panels keep working.

### PR 5 — Notebooks home + Sources page
Home: recently-viewed vs active hierarchy, card treatment per prototype 00
(visual only). Sources: the admin table gets the library card/row treatment
(type pebbles, one-line meta) without changing columns/actions; "Embedded"
pills stop looking like buttons.

### PR 6 — Modals & source viewer (visual pass)
Keep the modal architecture (page/panel conversion is Stage 2). Fix: spacing,
⋮ vs close collision, tab style, nested-card flattening, consistent paddings.

### PR 7 — Remaining screens sweep
Models (visual declutter only: badge diet, clear enabled-vs-available
styling), Settings, Podcasts (real player styling on the raw <audio>),
Transformations, Ask/Search (restyle in place). Empty states get the friendly
copy treatment where copy already exists; new onboarding copy is Stage 2.

### PR 8 — Polish + regression pass
Cross-screen sweep with /dev/design open: stray grays, focus rings, dark-mode
edge cases, 1000px-width sanity, favicon/logo assets.

## Explicitly NOT in Stage 1 (Stage 2 backlog, already designed)
Creations area & artifact system · Notes as menu item · Ask → global chat ·
source page (modal → route) · context chips/spines & ContextSelection Auto ·
citations system · deep research mode · universal Create (⌘J) · Home redesign
(new IA) · search overhaul · onboarding flows.

## Risks / notes
- Fonts change app-wide in PR 1 — biggest single visual jump; ship PR 1+2
  close together so the "half-themed" window is short.
- Community PRs in flight will conflict with globals.css — announce the
  reskin start in the Discussion, merge or close stale UI PRs first.
- Tailwind v4 + tw-animate: verify no plugin assumes the old radius scale.
- After PR 2, consider inviting community screen-pass PRs (PR 5+ are
  parallelizable) with /dev/design as the acceptance reference.
