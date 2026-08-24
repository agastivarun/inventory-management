---
name: saas-sidebar-redesign
description: Redesigns the app shell from a top nav bar into a modern SaaS-style left vertical sidebar with consistent spacing and a polished, professional look. Use when asked to redesign, modernize, or restyle the UI, move navigation to a sidebar, or give the app a "SaaS-style" or "dashboard-style" look.
---

# SaaS Sidebar Redesign

Converts the app shell in `client/src/App.vue` from a full-width top nav bar into a fixed left vertical sidebar, matching the layout convention of modern SaaS dashboards (e.g. Linear, Stripe, Vercel). This changes only the app shell and navigation chrome — routes, API calls, and page-level view logic are untouched.

**MANDATORY: Delegate all implementation to the `vue-expert` subagent.** Per this repo's `CLAUDE.md`, any creation or significant modification of a `.vue` file must go through `vue-expert`. This skill defines the design spec and plan; do not edit `.vue` files directly from the main thread.

## Current State (before)

`client/src/App.vue` renders:
```
<div class="app">
  <header class="top-nav">          <!-- full-width, sticky, 70px tall -->
    <div class="nav-container">     <!-- logo, horizontal nav-tabs, LanguageSwitcher, ProfileMenu -->
  </header>
  <FilterBar />                      <!-- full-width bar below the header -->
  <main class="main-content">        <!-- max-width 1600px, centered -->
    <router-view />
  </main>
</div>
```
Nav items are `router-link`s inside `.nav-tabs`, active state via `$route.path` comparison. Global styles (`.card`, `.stat-card`, `table`, `.badge`, etc.) live in `App.vue`'s unscoped `<style>` block and are shared by every view — **do not touch these**, only the shell/nav-related rules.

## Target State (after)

Two-column shell: fixed-width sidebar on the left (full viewport height) + a content column on the right that scrolls independently.

```
<div class="app-shell">
  <aside class="sidebar">
    <div class="sidebar-brand">…logo + company name…</div>
    <nav class="sidebar-nav">
      <router-link> icon + label, one per route, vertical stack </router-link>
    </nav>
    <div class="sidebar-footer">…LanguageSwitcher, ProfileMenu…</div>
  </aside>

  <div class="content-area">
    <header class="content-topbar">
      <FilterBar />
    </header>
    <main class="main-content">
      <router-view />
    </main>
  </div>
</div>
```

### Sidebar spec
- Width: `240px` fixed (`260px` is also acceptable — pick one and use it consistently in any width/margin calc).
- Full height (`100vh`), `position: sticky; top: 0`, own scroll if nav list ever overflows.
- Background: white or very light slate (`#ffffff` or `#f8fafc`), `border-right: 1px solid #e2e8f0` (reuse existing `--line`/`#e2e8f0` token already used across the app — do not invent a new border color).
- Brand block at top: company name + subtitle, same content currently in `.logo`, just stacked vertically instead of inline with the nav.
- Nav items stacked vertically, one per line:
  - Icon (inline SVG, 18–20px, stroke-based line icon — **no emoji**, per the project's "No emojis in UI" rule) + label, `gap: 0.75rem`.
  - Default state: `color: #64748b`.
  - Hover: `background: #f1f5f9`, `color: #0f172a`.
  - Active (`$route.path` match): `background: #eff6ff`, `color: #2563eb`, plus a `3px` left accent bar (replaces the old bottom-border active indicator, which doesn't read correctly in a vertical layout).
  - Consistent row height/padding across items — pick one `padding` value (e.g. `0.75rem 1rem`) and apply it uniformly, don't let icon vs. no-icon rows differ in height.
- Footer area (bottom of sidebar): `LanguageSwitcher` and `ProfileMenu`, stacked or inline depending on how they render standalone — check both components' own root styles before deciding, since they were built for a horizontal header context and may need minor spacing adjustments (not logic changes) to sit well vertically.

### Content area spec
- `flex: 1`, own vertical scroll, `min-width: 0` (so tables/charts can shrink instead of pushing the sidebar off-screen).
- `content-topbar` replaces the old full-width `FilterBar` placement: same component, just now scoped to the content column's width instead of the full viewport.
- `main-content`: drop the old `max-width: 1600px; margin: 0 auto` centering — in a sidebar layout the content column IS the available width. Keep the existing `padding: 1.5rem 2rem`.

### Spacing consistency
Reuse the app's existing 4px/8px rhythm — don't introduce a new scale. Concretely:
- Sidebar internal padding, nav item padding, and content-area padding should all resolve to multiples of `0.25rem` (4px), matching values already used elsewhere in `App.vue` (`0.625rem`, `0.75rem`, `1.25rem`, `1.5rem`, `2rem`, etc.).
- Keep the existing `border-radius` values (`6px` for interactive elements like nav items/buttons, `8–10px` for cards) — a sidebar redesign should feel like a layout change, not a new design language.
- Keep the existing color tokens (`#0f172a`, `#64748b`, `#e2e8f0`, `#2563eb`, `#f8fafc`, `#eff6ff`) already used in `App.vue` — do not introduce a new palette.

## Icons

The project has no icon library. Use small inline SVG (stroke-based, ~1.5px stroke, 20x20 viewBox) for each nav item — one simple icon per route (e.g. grid/home for Dashboard, boxes for Inventory, clipboard/list for Orders, dollar/chart for Finance, trending-up for Demand, bar-chart for Reports). Keep them as inline `<svg>` in the template (consistent with the project's existing custom-SVG-chart convention) rather than adding an icon package dependency — don't add a new npm dependency for this.

## Implementation steps (for vue-expert)

1. Read `client/src/App.vue`, `client/src/components/FilterBar.vue`, `client/src/components/LanguageSwitcher.vue`, and `client/src/components/ProfileMenu.vue` in full before editing, to see their current root-level styles/assumptions (e.g. `FilterBar`'s `.filters-bar` is currently styled full-width).
2. Restructure `App.vue`'s template per the "Target State" markup above. Keep every existing route (`/`, `/inventory`, `/orders`, `/spending`, `/demand`, `/reports`), every `t('nav.…')` i18n key, and the same modals (`ProfileDetailsModal`, `TasksModal`) wired the same way — this is a layout change, not a feature change.
3. Replace `.top-nav` / `.nav-container` / `.logo` / `.nav-tabs` CSS rules with `.app-shell` / `.sidebar` / `.sidebar-brand` / `.sidebar-nav` / `.sidebar-footer` / `.content-area` / `.content-topbar` rules, following the spec above. Leave every other rule in `App.vue`'s `<style>` block (`.card`, `.stat-card`, `table`, `.badge`, `.loading`, `.error`, etc.) untouched.
4. If `FilterBar.vue`'s own scoped styles assume full viewport width (e.g. a centered max-width container), adjust only what's needed for it to sit well in the narrower content column — don't rewrite its filter logic.
5. Check each view under `client/src/views/*.vue` for hardcoded width assumptions (rare, but some charts/tables might reference viewport-relative sizing) — adjust only if something visibly breaks, don't preemptively touch views that already work with `flex: 1` content.
6. Add a `mobile`/narrow-viewport fallback: below some breakpoint (e.g. `900px`), collapse the sidebar to icons-only or behind a toggle rather than letting it crowd out content — keep this simple (icon-only collapse is enough; a full slide-out drawer is optional polish, not required).

## Verification

After vue-expert finishes:
1. Confirm both dev servers are running (`http://localhost:3000`, `http://localhost:8001`) — start them if not (see the `start` skill).
2. Use Playwright MCP tools to navigate to each route (`/`, `/inventory`, `/orders`, `/spending`, `/demand`, `/reports`) and screenshot:
   - Sidebar renders full-height, correct item is highlighted as active per route.
   - Filters still work (change a filter, confirm data updates — same underlying `useFilters` composable, only its visual position changed).
   - ProfileMenu and LanguageSwitcher still open/function from their new position.
   - No layout overflow/clipping at common widths (1440px, 1024px, and the narrow breakpoint from step 6 above).
3. Check the browser console for errors via `mcp__playwright__browser_console_messages`.
4. Confirm no emojis were introduced and no new npm dependency was added (`git diff client/package.json` should be empty unless explicitly discussed).
