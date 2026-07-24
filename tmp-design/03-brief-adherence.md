# Adherence check — concepts vs REDESIGN_BRIEF.md (2026-07-21)

Verdict: the fractal thesis is fully compatible with the brief — nothing we
designed contradicts it. But the brief carries a second axis our thesis hasn't
absorbed yet: **progressive agency** (Focused vs Deep Research and everything
it drags in: activity, permissions, interruption, states). That's the main
evolution needed.

## Covered well (no action)

| Brief item | Where |
|---|---|
| 3 scopes, same language | Screens 01/02/04, scope pills everywhere |
| Scope visible before/during/after | Scope pill + selection micro-scope + receipt strip |
| Evidence as part of the answer | 06: chips after claims, popover, bundle accordion |
| Distinct natures (source/note/insight/external/artifact) | 06 chip idiom + ContentTypeBadge ≈ pebble system |
| Provenance survives transformations | Derived-insight breadcrumb popover; honey note idiom |
| External evidence + adoption | Dashed chip, receipt, "Add as source" |
| Supported vs synthesis/inference | ~synthesis chip + dotted underline |
| Open passage from citation | Click-through to Contents panel / source page (02+06) |
| Artifacts searchable, traceable, multi-notebook | 03 Creations + projection badges |
| Notes as authoral, special | Own menu item + reserved surfaces |
| Simple flow stays primary | Calm chat is the center of every screen |
| Citations don't rely on color alone | Number + shape + prefix on every chip class |

## Gaps — thesis must evolve

1. **ModeSwitcher (Focused / Deep Research) — biggest gap.** No screen shows
   the mode choice, its cost/behavior explanation, or per-question promotion
   ("run this one deep") without converting the session. Brief is explicit:
   same citation quality, different effort budget.
2. **Agentic activity via progressive disclosure.** Nothing shows
   AgentActivity ("Searching notebook… 8 candidates · 4 opened"), the
   expandable ResearchPlan/ToolActivity detail, PermissionPrompt (external
   search), ResearchInterruption (stop / refine / answer now), BudgetStatus.
   An entire state family (planning→searching→opening→comparing→done) is
   undesigned.
3. **Composer anatomy.** Our input is a plain field. Brief wants
   ResearchComposer with `@mention` tokens (widen scope without leaving the
   conversation), attachments, and ContextSelection incl. the new `Auto`
   (today's Full/Insights/Excluded + Auto). MentionToken appears nowhere.
4. **Search surface undesigned.** Sidebar has Search but no screen: unified
   SearchResult (source/note/artifact/external in one list, natures intact),
   SearchFilters, ExternalSourceCard preview→adopt flow, "manual search and
   conversation use the same result/evidence components".
5. **Non-happy-path evidence states.** We show the golden path. Missing:
   stale/unavailable evidence (source removed/re-versioned), invalid
   reference, partially-supported and unsupported answers, multiple evidences
   per claim, "evidence opened by the agent" vs merely found.
6. **Conversation lifecycle states.** Empty/onboarding chat, preparing
   context, streaming, recoverable error, capability-unavailable (no
   embeddings / no tool calling / small local model) — the local-first
   promise means fallbacks must look intentional, not broken.
7. **Mobile evidence access.** Popovers need a dialog/sheet alternative;
   evidence must be reachable on narrow viewports (success criterion 3).
   Concepts are desktop-first — one mobile-anatomy plate would close it.
8. **AnswerBlock segmentation.** Brief's contract is segment-based
   (AnswerSegment.grounding per segment, not per sentence). 06 gestures at it;
   the anatomy should acknowledge segments as the unit answers are built from
   (also what "Save answer" and partial-support states hang off).

## Proposed next moves

- **Screen 07 — Deep Research**: notebook chat with ModeSwitcher in the
  composer, a deep run in progress (activity summary + expandable detail),
  PermissionPrompt for external search, interruption controls, and the
  completed deep answer whose citations are identical in kind to focused mode
  (the brief's core promise made visible).
- **Screen 08 — Search**: global search with unified results, nature badges,
  filters, and an ExternalSourceCard with the adopt flow.
- **06 addendum**: a second annotation row with degraded states — stale
  evidence, invalid citation, partially-supported answer banner, multi-evidence
  chip — plus a small mobile plate (evidence as bottom sheet).
- **Composer upgrade across 01/02/04**: @mention token in one of them +
  ContextSelection (Auto default) + capability hint ("local model · focused
  only" as a quiet example).
- Doc: fold "progressive agency" into 02-ux-architecture.md as the second
  axis of the thesis (scopes × agency).
