# UX Spec — Create from URL V1: Design Feature

**Prototype:** [v1-design.html](https://nettawit.github.io/aria-funnel/v1-design.html)  
**Status:** Needs update  
**Last updated:** June 2026

---

## Overview

This flow adds a **design mode selection** to the Create from URL experience. After scanning a URL, users choose whether to import both content and design, or only the visual style.

---

## Entry Point

The modal opens automatically from the Harmony Creation V1.1 entry screen.  
Trigger: clicking **"Create from URL"** in the composer footer.

---

## Flow Steps

### Step 1 — Enter URL
- Modal title: **"Create from URL"**
- Subtitle: "Use any website as a starting point for your new site."
- Input: URL field with placeholder "Paste any URL addresses"
- CTA: **Scan** (primary, blue)
- Footer note: "Only use URLs where you have rights to the content"

### Step 2 — Scanning
- URL field shows entered domain + **Re-scan** button
- Site screenshot preview renders in the modal
- Progress indicator during scan

### Step 3 — Results (Regular site)
- Domain shown with detected platform badge (Shopify / WooCommerce / none)
- **"All pages — always imported"** row (always selected, with green checkmark)
- Two mode options:

| Option | Label | Description |
|--------|-------|-------------|
| **Content & design** _(default)_ | Keep the layout, style and content | Includes products, categories & prices (Shopify only) |
| **Design only** | Keep the same visual style | No content import |

- Footer: "Only use URLs where you have rights to the content."
- Actions: **Cancel** / **Add to Aria** (primary)

### Step 3b — Shopify detected
- Same as Step 3 but with **Shopify** badge next to domain
- "Content & design" description reads: "Includes products, categories & prices"

---

## Outcome

On **Add to Aria**, the selected site is attached to the prompt as a chip:
- Shows site thumbnail + domain name
- Mode label shown below domain ("Content & design" or "Design only")
- Shopify badge shown if applicable
- User can remove the chip and re-open the modal

---

## Platform Detection Logic

| URL pattern | Badge shown |
|-------------|-------------|
| Contains "shop" (not "woo") | Shopify |
| Contains "woo" | WooCommerce |
| Other | None |

---

## Open Questions / Known Issues

- Prototype is flagged **Needs update** — design options and Shopify copy need review
- "Woohoo" badge label is placeholder — confirm final label with copy
