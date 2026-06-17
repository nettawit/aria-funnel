# UX Spec — Harmony Creation V1.1 with Create from URL

> **Figma:** [Funnel Updates](https://www.figma.com/design/GvxmzuhE97Zyl4ekbmZkig/Funnel-Updates?node-id=17147-9105&t=L0dLo4uWAGjeSWgB-1)
> **Prototype:** [harmony-v1.1.html](https://nettawit.github.io/aria-funnel/harmony-v1.1.html)
> **ImportFlow modal spec:** [spec-v05.md](spec-v05.md) — the modal is shared; all modal behavior is documented there.
> **WDS Storybook:** [wix-design-system-employees](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button)

---

## Scope — UX Fixes

This version addresses UX issues identified in the V0.5 test. Fixes in this build:

- **First screen layout** — rebalanced spacing, hierarchy and prompt area sizing
- **Composer flows** — refined example chip behavior and prompt generation states
- **Modal: dismiss on loading** — closing the modal mid-scan is now handled cleanly
- **Remove line breaks** — truncation and overflow issues in the prompt card removed

---

## Entry Screen

**Context:** Aria prompt composer — "Tell me your site's name, what it does, and who it's for." Full-page card with a text input, example chips, and a character/state indicator.

### Layout

The screen uses a centered card layout with:
- Prompt text input (multi-line, auto-grow)
- Example prompt chips below (horizontally scrollable)
- Action bar at the bottom: "Create from URL" text button left, "Generate" primary button right

### "Create from URL" text button

- WDS: `Button / Ghost / Medium` (38px, `0 20px`, border-radius 8px)
- Label: "Create from URL"
- Prefix icon: Globe SVG 16×16
- Position: **left** of the action bar (Generate stays right)
- On click: opens ImportFlow modal in URL phase

> **Difference from V0.5:** In V0.5 the trigger is a pill inside the composer card action bar. In V1.1 it's a text button in the entry screen toolbar. The modal that opens is identical.

### Attachment chip (post-import)

Once a site is added, the "Create from URL" button is replaced by a chip.

```
[favicon 13×13]  [hostname]  [platform badge?]  [× remove]
```

Note: V1.1 does **not** show the 48×32 screenshot thumbnail in the chip (V0.5-only feature).

| Property | Value |
|---|---|
| Height | 30px, padding `0 10px`, border-radius 24px |
| Background | `#fff`, border `1px solid #E8E7E7` |

Removing the chip: silent — no undo toast.

### Generate button

- WDS: `Button / Primary / Medium`, bg `#2F5DFF`
- Always `marginLeft: auto` — stays right-aligned regardless of chip state

---

## ImportFlow Modal

Identical to V0.5. See **[spec-v05.md → ImportFlow Modal](spec-v05.md)** for full documentation:

- Modal shell dimensions and shadow
- Header (title, subtitle, info icon, close button)
- Phase 1 — URL entry (input field, Continue button, footer note)
- Phase 2 — Scanning (spinner icon button, progress bar, "Analyzing…" label)
- Phase 3 — Results (site preview card, platform badges, info banner, Add site / Cancel)
- Error states (Wix site, social media, file URL, private, bad format)
- Platform detection logic

---

## Composer Flows

### Empty state

Placeholder text: "Tell me your site's name, what it does, and who it's for."
Aria avatar animates to indicate it's listening/ready.

### Typing state

- Border pulses subtly (`rgba(47,93,255,0.22)` → `rgba(47,93,255,0.50)`, 1.8s ease)
- Generate button becomes active once there is input

### Prompt generation (Aria fills the prompt)

Triggered when a site is attached. Aria generates a prompt pre-fill:
- Shows "Aria is generating a prompt based on your site info…" in the card header
- Prompt text fades in with the generated content
- Shopify stores include product data reference in the generated prompt

### Example chips

Horizontally scrollable row of preset prompt suggestions.
- WDS: `Tag / Standard` style
- On click: fills the prompt input with that example text
- "More" overflow chip opens additional suggestions

---

## WDS Component Checklist

| Element | WDS |
|---|---|
| Ghost button | [Button / Ghost](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Primary button | [Button / Primary](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Prompt text input | [Input / Textarea](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-input--input) |
| Example chips | [Tag](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-tag--tag) |
| Platform badge | [Badge](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-badge--badge) |
| Modal (shared) | see [spec-v05.md](spec-v05.md) |
