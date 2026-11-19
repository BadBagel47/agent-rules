> **DRAFT – NOT IN EFFECT.** Will be published as WEB.md together with the next rules version.

# WEB BASICS

Basics the user always wants in web projects (websites and web apps). Read together with the global agent rules (AGENTS.md).

## How to apply
- **New web projects:** include everything below from the start.
- **Existing web projects:** include what is missing as one item in the adaptation plan, so the user approves it once per repo. Record the approval as a decision in HANDOFF.md. These basics change the product, so they are never applied without the user's go-ahead, also when a new point is added here in a minor rules version. Once approved, the normal steps apply: verify, publish and report.
- Keep the project's own look: adapt colours and sizes to the project's design, but do not drop any point below without the user's approval (record it as a decision).
- Verify on a phone-sized screen and with keyboard navigation when the environment allows it. Otherwise say in plain words that it has not been tried.
- A recurring web problem the user points out is proposed as a new point here (via the backlog in agent-rules), not as a project rule in each repo.

## 1. No blue tap highlight or focus ring after a tap or click
On mobile, tapping a button or link must not show a blue highlight, and the focus ring must only show for keyboard users (`:focus-visible`), not after a tap or click. Never remove the focus ring for keyboard users. If the project already has its own focus style, keep it and apply it with `:focus-visible`.
- Text fields are an exception: browsers always show the focus ring there, also after a tap, so the user sees where they are typing. Keep it, in the project's colours instead of the browser's blue.
- Without the tap highlight nothing shows that a tap registered, so buttons and links must have their own pressed state (`:active`), in the project's style.

```css
/* No blue tap highlight on mobile */
* { -webkit-tap-highlight-color: transparent; }

/* Focus ring only for keyboard users */
:focus:not(:focus-visible) { outline: none; }
:focus-visible { outline: 2px solid currentColor; outline-offset: 2px; }
```

## 2. Own arrow in dropdown menus
The browser's own arrow in `<select>` looks different on every device and sits too far to the right. Replace it with an SVG arrow placed a little in from the right edge, with room for the text. Change the arrow colour (`%23888` = #888) to match the project's text colour; with both light and dark themes, set one arrow per theme. Dropdowns built without `<select>` use the same SVG arrow; never text characters such as ▼ or ▾, which look different on every device.

```css
select:not([multiple]):not([size]) {
  appearance: none;
  -webkit-appearance: none;
  padding-right: 2.25rem;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1.5l5 5 5-5' fill='none' stroke='%23888' stroke-width='1.75' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 0.75rem center;
  background-size: 0.75rem auto;
}
```

## 3. Shared look and theme
- The user's Claude artifacts and example pages (e.g. a glass-effect example page) are demos and design references, not the source of a theme. Never copy one into a repo as the project's look without asking.
- When the user asks for a shared look by name (e.g. "glastemat"):
  1. If the shared theme repo exists: use it, connected the way it is meant to be, and only in the project that asked for it.
  2. If it does not exist yet: say so, and ask whether the user wants a one-time copy. If yes: record in HANDOFF.md where the copy came from and when, so it can be replaced by the shared theme later.
