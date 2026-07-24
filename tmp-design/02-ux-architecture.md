# Open Notebook — Fractal UX Architecture (working draft)

> Working document (2026-07-21). Companion to `01-problems-and-vision.md`.
> Anchor visual: Direction D (calm clean). This doc is about structure, not skin.
> Grounded in `.tmp-context/VISION.md` (evidence-centered research vision).

## The diagnosis in one sentence

The domain is already fractal — the same acts (converse, derive, collect) exist
at Source, Notebook and App level — but the UI gives each scope a **different
grammar**, so features feel scattered: transformations don't appear on the
source that produced them, podcasts live in a separate page from the notebooks
they draw on, and Ask is a global chat disguised as a form buried next to
Search.

Notebook LM solves this by **imprisoning everything in one notebook**. We don't
need the prison — we need the grammar.

## The fractal grammar

Every scope offers the same three surfaces, at different zoom levels:

| Surface | Source scope | Notebook scope | App scope |
|---|---|---|---|
| **Contents** (what's in scope) | The content itself (transcript, pages, media) | Sources + notes | Notebooks + library |
| **Conversation** (scoped chat) | Chat with this source (`@` pulls others in) | Chat with notebook | Global chat — the evolution of Ask |
| **Creations** (what was derived) | Insights, notes about it, artifacts that cite it | Artifacts that cite the notebook | The whole Studio, filterable |

Rules that make it fractal rather than three separate features:

1. **One chat, three zooms.** The chat panel is the same component everywhere;
   only the default scope changes (matches VISION's single `Scope` model and
   "one engine, three scopes"). Ask-as-a-page dies; Search remains as the
   retrieval surface.
2. **Artifact is the universal noun.** Note, insight (transformation output),
   podcast episode, mind map, study guide, flashcard deck, video explainer —
   all typed artifacts with provenance (the EvidenceBundle/ContextManifest that
   generated them). "Transformation" becomes the *recipe*; its output is an
   artifact like any other.
3. **Artifacts project into every scope they touch.** An episode citing three
   notebooks appears in the Creations surface of all three — and on any source
   it drew evidence from. Provenance (already preserved per VISION §6) *is* the
   projection index. No duplication: one collection, many filtered views.
4. **Creation is scope-aware, not page-bound.** A universal Create action
   (button + ⌘K + contextual shortcuts) opens the same artifact picker
   anywhere; the invoking scope pre-fills the context. Grammar:
   *Create [type] from [current scope / selection]*. Scope is editable at
   creation time — from a source you can widen to the notebook; from the
   Studio you can compose across notebooks (today's multi-notebook podcast
   flow becomes the general case, not the exception).
5. **Selection is a micro-scope.** Checkboxes on sources (Notebook LM got this
   right) form an ephemeral scope that chat and Create both respect.

## The second axis: progressive agency (added 2026-07-21, from REDESIGN_BRIEF)

The fractal gives us *where* the system looks (scope); the brief adds *how
hard it works* (agency). Two modes, chosen by the user, same citation quality:

- **Focused** — fast, predictable, pre-curated or single-shot retrieved
  context; minimal visible activity; works with small/local models.
- **Deep Research** — adaptive investigation: plans, searches, opens
  evidence, compares; activity summarized with expandable detail
  (never a raw tool-call log); permission prompts for external reach;
  interruptible (stop / refine / answer now).

A single question can be promoted to Deep without converting the session.
Capability gaps (no embeddings, no tool calling, small model) degrade to
Focused gracefully and visibly — a modest install is a first-class citizen,
not a broken one. The thesis is therefore **scopes × agency × evidence**.

## What each surface becomes

### Global Studio (new top-level area)

Consolidates all creations: filter by type (note, insight, podcast, mind map,
study guide, flashcards, video…), by notebook/source, by recency. Also home of
the **recipes** (transformation prompts, podcast profiles — later: mind map
styles, deck templates) and of creation entry points. Replaces the Podcasts
page; absorbs the artifact-management half of Transformations (recipe editing
stays a Manage concern).

### Notebook workspace

Keeps the three-panel shape validated in the style tiles, but the third
concern becomes explicit: Sources | Chat | **Studio strip** (creation
shortcuts + artifacts of this notebook, notes included and pinned first).
Notes stay one tap away — they're the highest-frequency artifact, not a
buried filter.

### Source view

Stops being a modal (per `01`, B4) and becomes the same workspace one zoom
in: content | chat-with-source | its creations (insights it produced, notes
about it, artifacts that cite it — even ones created at broader scope).

### App level

Sidebar simplifies toward: **Notebooks · Sources · Studio · Search** (+ global
chat, reachable everywhere). Ask disappears as a destination; its capability
becomes the App-scope chat. Manage (Models, Settings, recipes…) stays tucked
away.

## Why this answers the community

The many artifact requests (mind maps, study guides, flashcards, video
explainers) stop being N feature requests and become **one extensible
system**: a new artifact type = a recipe + a renderer + `to_retrieval_entries`
(VISION §9). The UI cost of each new type approaches zero because every
surface already knows how to list, filter, project and create artifacts.

## Decisions (2026-07-21, Luis)

- **Naming**: the user-facing area is **"Creations"** (not Studio).
- **Notes**: keep a **reserved area** — unlike other artifacts (create once,
  then consume), notes are continuously edited. Notes gets its **own menu
  item**; inside a notebook it keeps a dedicated surface, not just a filter.
- **Chat sessions**: yes — conversations are scoped objects, and a saved
  answer becomes an artifact carrying its evidence.
- **Projection is forward-only**: applies to content created from now on;
  legacy content won't project as well and that's accepted.

## Visual direction (decision 2026-07-21, Luis)

**Hybrid H — "Quiet Color" (C tamed) is the direction.** Neutral reading
surfaces with honest 1px borders; matured coral/gold/teal owned hues in a
per-panel hierarchy (each surface speaks one hue via tick/chip/action, never
washes); Bricolage Grotesque display + Instrument Sans; friendly copy kept;
flat clarity over gloss; plum-free deep-neutral dark. Signature: the "hue
tick" breaking each panel header's hairline. Community basis: C's
color-as-affordance praised, C's flashiness rejected ("Linux Mint, not Mac"),
chat tint rejected. The 9-screen concept prototype is being re-skinned to H
(`concepts-h/`).

## Direction refinement: Variant I "Quiet Green" (2026-07-23/24)

- Community: red reads as error/alarm → red retired to destructive+degraded
  only; actions move to fern green (#2E6B4F, sibling of the teal AI voice).
  Type hues rebuilt without the traffic-light read (video plum, audio dusty
  mauve, sources-panel sage). Geometry squared to 4–6px.
- The context switch iterated to: single compact chip per card showing only
  the current state (FULL/INSIGHTS/OFF + cycle glyph), same position on every
  card; notes are binary (FULL/OFF); ⋮ overflow top-right; panel-header count
  badges removed.
- Propagated to the 9-screen prototype (concepts-h/, banner "Direction I").
  Open point: checkboxes were replaced by the context chip as the single
  scope mechanism ("4 in context · Auto") — pending Luis's confirmation.

## Source card & workspace refinements (2026-07-23, community designer feedback)

- **The card spine is information, not decoration**: it carries the
  per-source context inclusion state — solid green = full content in context,
  gold = insights-only, no spine + dimmed = excluded. This surfaces a feature
  the current product hides in a dropdown, and pairs with ContextSelection
  (the selector sets the policy, the spine shows each source's state).
- **Card metadata is one line**: type chip + insight count side by side,
  titles get the room. Insight count stays (it signals invested value;
  "No insights yet" is actionable); hover reveals insight titles. Type stays
  (it matters for citations/locators) but smaller.
- **Panels are collapsible** (Sources / Notes / Chat chevrons) — parity with
  the current product, was lost in the concepts.

## Citations & evidence (decisions 2026-07-21)

- Inline numbered chips after claims; one pill skeleton, one distinguishing
  "dress" per evidence class: source (solid) · note (honey, authoral) ·
  derived insight (breadcrumb to original in popover) · external (dashed +
  receipt + "Add as source") · inference (hollow ~synthesis chip — claims
  without a direct span are visually distinct).
- Phase 1 reality: the citation span IS the retrieval chunk (150–300 words,
  verbatim — no LLM trimming). Popovers get pinned header/footer and an
  internal scroll area with fade masks; best-match sentences highlighted by
  cheap term overlap, not AI.
- Chips are minimal (2026-07-22): class dot + sequential number per answer
  (Notebook LM style), color = nature (teal source · gold note · mauve derived
  · slate external). No locators or titles inline — those live in the popover.
- The save affordance is user-named **"Save as Note"** everywhere (internally
  the saved answer is an artifact carrying its evidence bundle).
- The "Transform" verb is retired in the UI: creation entry points all say
  **Create** (recipes remain the internal mechanism).
- **Hover peeks, click goes to the source** — no dedicated Evidence panel
  (rejected: duplicates the Contents surface and adds a concept to learn).
  Click opens the source inside the existing Sources/Contents panel scrolled
  to the highlighted chunk (Notebook LM's pattern); deep-dive is one more
  click to the source page.
- The evidence bundle is a receipt strip at the end of every answer
  ("3 sources · 1 note · 8 passages") expanding as an inline accordion in the
  conversation flow. Saving an answer preserves its bundle (answer → artifact).

## Remaining open questions

- **Transformations page**: survives as "Recipes" under Manage, or moves into
  Creations? Migration story for existing insights → artifacts.
- **How far does phase 1 go**: podcast provenance links are thinner than
  insight/note links today (mitigated by forward-only decision).
