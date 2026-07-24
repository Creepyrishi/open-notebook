# Open Notebook UI Redesign — Problems & Vision

> Working document (2026-07-21). Lives in `tmp-design/` until the direction is settled;
> then graduates to `docs/` or a GitHub Discussion.

## Why now

Open Notebook succeeded on substance: multi-provider AI, self-hosting, privacy, a
large and engaged community. The UI never got the same investment — it still runs
the stock shadcn/ui theme (default zinc palette, default blue primary, Geist,
default radius) with layouts that grew organically. The product has no visual
identity of its own, and several core screens are hard or unpleasant to use.

A redesign is likely the highest-leverage investment available: it is what stands
between "impressive open-source project" and "product people prefer over
Notebook LM".

## Scope (agreed)

- **Full**: new visual identity (tokens, typography, color, surfaces) **and**
  restructuring of problematic screens **and** rethinking information
  architecture / navigation (menu grouping, entry flows, onboarding).
- First-class priorities, all four:
  1. **Impeccable dark mode** — designed alongside light from the first style
     tile, not derived from it.
  2. **Responsive/mobile** — workspace and media designed for small screens from
     the prototype stage.
  3. **Density/productivity** — less dead space, more visible content, fast
     navigation; optimize for intense daily use.
  4. **Empty states & onboarding** — first-run experience and empty screens that
     teach; key for community adoption.

## Problem inventory

### A. Identity (affects every screen)

- **A1. No brand layer.** Stock shadcn tokens: pure white background, generic
  zinc grays, generator-default blue primary (`oklch(0.623 0.214 259.815)`),
  Geist font. The sidebar logo sparkle is the only personality in the app.
- **A2. Everything is a bordered card on white, with equal visual weight.** No
  hierarchy; the eye has nowhere to land. Screens feel pale and lifeless.
- **A3. Placeholder-looking text everywhere.** "Add description...",
  "No description", "Using Default Models" — the product reads as unfinished.
- **A4. Dark mode is a mechanical inversion** of the light theme, not a designed
  theme.

### B. Structure / layout

- **B1. Notebook workspace (the core screen): three rigid columns.** Fixed
  widths, dead space, cards inside cards, chat squeezed into a fixed column.
  Should be a real workspace: adjustable/collapsible panels, chat focus mode,
  controlled density.
- **B2. Sources list is an admin table.** A knowledge library rendered as a
  database grid: no favicons/thumbnails, no media-type visual language, no
  grouping; "Embedded: Yes" pills look like clickable buttons. Should be a
  library experience — browsing it should be pleasant.
- **B3. Models screen is the worst offender.** Config dump with information
  duplicated at three levels (provider badges, config badges, per-model badges),
  hard scrolling, "enabled" indistinguishable from "available", no reordering.
  Needs progressive disclosure: defaults on top (already right), compact
  provider list with clear state, detail only on expand.
- **B4. Source viewer is a full page crammed into a modal.** Content, insights
  and details tabs inside a dialog; the ⋮ menu collides with the close X.
  Should be a wide side panel or a real route.
- **B5. Modals in general:** cramped spacing, nested cards, dated pill-style
  triple tab switcher.
- **B6. Ask/Search, Podcasts, Settings: forms floating in a white void.** No
  guidance, no visual interest; podcast player is the browser's raw
  `<audio>` element. Media area is too simple and not responsive.
- **B7. Notebooks home:** "Recently Viewed" and "Active Notebooks" cards are
  visually identical; source/note counts are tiny badges that look like buttons.

### C. Information architecture / navigation (to rethink)

- **C1. Menu grouping** (Collect / Process / Create / Manage) — revisit whether
  these categories match how users actually think.
- **C2. Entry flows** — how users get content in, and how the app guides them
  from "empty install" to "first insight".
- **C3. Onboarding** — nothing guides a fresh install today (configure models →
  create notebook → add source → chat).

## Vision

Open Notebook should feel like **a calm, confident research studio you own** —
not a generic SaaS dashboard, and not a Google product clone.

Qualities to design for:

1. **Identity** — someone seeing a screenshot should recognize Open Notebook.
2. **Hierarchy** — each screen has one obvious primary thing; surfaces, type
   scale and color carry the structure instead of borders-on-white.
3. **A workspace, not pages of cards** — the notebook screen feels like a place
   where work happens; panels flex, chat can take over, content is dense but
   never cramped.
4. **The library feels like a library** — sources are browsable, visual,
   inviting; media type is a first-class visual signal.
5. **Progressive disclosure for configuration** — Models/Settings show the
   simple path first and expert depth on demand.
6. **Both themes are first-class**, mobile is respected, and empty screens
   teach.

## Process (agreed)

1. ✅ This document.
2. **Style tiles**: the same screen (notebook workspace) executed in **three
   aesthetic directions**, light + dark each, as static HTML — no app code:
   - **Warm library/editorial** — paper-and-ink warm neutrals, serif display
     type, calm research-studio feel; a true "notebook" identity.
   - **Refined technical tool** — dark-friendly, controlled density, mono
     accents, Linear/Raycast-grade precision; embraces the dev/self-host base.
   - **Alive & colorful** — color as protagonist: strong accents per content
     type (source/note/podcast), tinted surfaces, more playful.
   - **Calm clean / soft neutral** — the low-risk candidate: Notebook LM-grade
     restraint (soft elevation instead of borders, functional pastels, calm
     density) but with its own identity — distinctive type, deliberate canvas
     temperature, non-Google accent.
   Note: visual direction is being decided first; UX/layout restructuring is a
   separate, later conversation — all tiles share the same screen structure on
   purpose.
3. Pick a direction (possibly a hybrid), then apply it to the 5–6 key screens
   as clickable static prototypes.
4. Phased implementation plan: tokens/theme → shell (sidebar/nav) → screen by
   screen, in small PRs.

## Open questions

- Where does this doc graduate to — `docs/7-DEVELOPMENT/design/` via PR, or a
  GitHub Discussion to involve the community early?
- Typography licensing constraint: self-hosted app → fonts must be open
  (Google Fonts / OFL) and bundled, no external CDN at runtime.
- How far can we deviate from shadcn/Radix components? (Recommendation: keep
  Radix primitives and the component architecture; retheme deeply and replace
  layout patterns — not the a11y layer.)
