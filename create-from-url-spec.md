# Create from URL — UX Spec for Developers

> **Figma file:** [Create from URL — Harmony](https://www.figma.com/design/ooyDmc0Qr8sQFSo6A9sWLu/Create-from-URL---Harmony?node-id=15814-40022&m=dev)
> **V1.1 Figma file:** [Funnel Updates](https://www.figma.com/design/GvxmzuhE97Zyl4ekbmZkig/Funnel-Updates?node-id=17147-9105&t=L0dLo4uWAGjeSWgB-1)
> **User research & test overview:** [Research Slides](https://docs.google.com/presentation/d/1BzNxlZvvSOSIlKLMsJ5_bSbOagkuLKaIRjB1dbz8n0M/edit?slide=id.g3eaf126193a_0_38)
> **WDS (Wix Design System):** [Component Storybook](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button)

---

## Overview

"Create from URL" is an entry point inside Harmony Creation that lets a user hand Aria an existing website. Aria scans it and uses the pages, content, and visual style as a starting point for the new Wix site.

The feature surfaces in two product contexts (entry screens), but the scanning modal (`ImportFlow`) is **fully shared** between them. Any change to the modal applies to both.

---

## Entry Points

### V0.5 — "Bring your site" (Figma node `15814-40022`)

**Context:** Harmony Creation entry screen with the "Design your site with Aria" hero + a card-based prompt composer.

**Trigger:** A ghost pill button labeled **"Create from URL"** sits in the action bar at the bottom-left of the composer card.

- WDS component: `Button` / Ghost variant / Medium size (38px height, `0 20px` padding)
- Prefix icon: Globe SVG (WDS `Globe` icon)
- On click → opens `ImportFlow` modal in URL phase

**Attached state:** Once a site is imported, the ghost pill is replaced by an attachment chip (see [Attachment Chip](#attachment-chip)).

---

### V1.1 — Harmony Creation (Figma node `17147-9105`)

**Context:** Aria prompt composer with a text input ("Tell me your site's name…") and example prompt chips.

**Trigger:** A text-style inline button labeled **"Create from URL"** appears below the input or in the toolbar area.

- WDS component: `Button` / Ghost or Text variant
- On click → opens the same `ImportFlow` modal in URL phase

---

## ImportFlow Modal

Shared component. Three sequential phases: `url` → `scanning` → `results`.

### Modal Shell

| Property | Value |
|---|---|
| Width | 530px (max 95vw) |
| Border radius | 12px |
| Shadow | `2px 20px 30px rgba(19,23,32,0.1)` |
| Background | `#fff` |
| Overflow | hidden (clips the footer) |

WDS reference: [Modal](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-modal--modal)

---

### Modal Header

| Element | Detail |
|---|---|
| Title | "Create from URL" — 16px, weight 700, `#151414` |
| Subtitle | "Use any website as a starting point" — 13px, weight 400, `#767574` |
| Info icon | Custom SVG "i" — circle + dot (cy=5.5) + stem (M9 8v5). **Not** WDS `InfoCircle` — intentional to match Figma node |
| Close button | 24×24 circle, bg `#f0efef`, × SVG 8×8 |

---

### Phase 1 — URL Entry

The user pastes or types a URL.

**URL input field**

| Property | Value |
|---|---|
| Height | 38px |
| Background | `#f8f6f6` |
| Border | `1px solid #C1C2C3` (default) → `1px solid #116DFF` + ring (focus) |
| Border radius | 8px |
| Prefix icon | Globe SVG 16×16, color `#767574` |
| Placeholder | "Paste a URL" |
| Clear button | Visible only when input has text and is not busy; × SVG 10×10 |

WDS reference: [Input](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-input--input)

**Continue button** — inline to the right of the input, same row

| Property | Value |
|---|---|
| Height | 38px |
| Padding | `0 18px` |
| Background | `#2F5DFF` |
| Border radius | 8px |
| Font | 14px, weight 600, `#fff` |
| Disabled style | Background `#b0c4ff` |
| Keyboard | `Enter` key in input triggers the same action |

**Footer note**

> "Only use URLs for sites you own or have permission to use"

Background `#f8f6f6`, top border `1px solid #e8e8e8`, 12px text, `#151414`.

---

### Phase 2 — Scanning

Triggered after the user clicks Continue. Runs a simulated async scan (~2s).

**During scan:**
- The Continue button is replaced by a **38×38 blue icon button** (border-radius 8px, `#2F5DFF`) containing a rotating circular arrow SVG. The spin animation is `360deg / 0.9s linear infinite`.
- The input field is disabled (no interaction).
- Below the input row, a **progress bar** appears:
  - Track: full width, 3px height, `#EEEEF6`, border-radius 3px
  - Fill: 65% width, `#2F5DFF`, animated via CSS transition
- Below the progress bar: `Analyzing "{url}"` — 12px, `#767574`

---

### Phase 3 — Results

Displays a preview card of the scanned site.

**Site preview card**

| Property | Value |
|---|---|
| Background | `rgba(255,255,255,0.4)` with `backdrop-filter: blur(7px)` |
| Border radius | 8px |
| Shadow | `3px 3px 12px rgba(0,0,0,0.14)` |
| Padding | `8px 8px 12px` |

Inside the card:

1. **Mac window dots** — three 5×5 circles, color `#cfd1dc`, gap 3.3px
2. **Screenshot** — fetched from `image.thum.io/get/width/560/crop/680/{url}`. Height 238px, `objectFit: cover`, `objectPosition: top`. On error → grey background fallback.
3. **Site name row** — hostname in 12px / weight 500 / `#383838`
4. **Platform badge** (if detected) — on its own line below the hostname

**Platform badges**

| Platform | Detection | Badge label | Background | Text color |
|---|---|---|---|---|
| Shopify | host includes "shop", excludes "woo" | Shopify | `#D5DFFF` | `#383838` |
| WooCommerce | host includes "woo" | Woohoo | `#D5DFFF` | `#383838` |
| *(none)* | regular site | — | — | — |

WDS reference: [Badge / Tag](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-badge--badge)

**Info banner** (below card)

> "Aria will use your site's pages, content and visual style."
> Shopify variant: "…including product data, images and prices."

- Background `#f5f7ff`, border `1px solid #7896ff`, border-radius 12px
- Prefix: info circle SVG 18×18, color `#2F5DFF`
- Font 12px, `#151414`

**Footer actions**

| Button | Style | Action |
|---|---|---|
| Cancel | Outline blue — 30px, border `1px solid #7896ff`, color `#2f5dff` | Closes modal, discards result |
| Add site | Primary blue — 30px, bg `#2f5dff`, color `#fff` | Commits the site, closes modal |

---

### Error States (URL Phase)

Errors appear **below the input row** as inline red text — not a toast, not a banner.

| Trigger | Condition | Message |
|---|---|---|
| Wix site | host includes `wix` | "This is a Wix site — importing from Wix isn't supported yet." |
| Social media | host includes instagram/twitter/facebook/tiktok/linkedin/pinterest | "Social media profiles can't be scanned. Try your website instead." |
| File URL | URL ends in .pdf/.doc/.docx/.xls/.csv | "File URLs aren't supported. Paste a website address instead." |
| Private / localhost | host is localhost or 192.168.x.x / 127.0.0.1 | "This address isn't reachable. Use a publicly accessible URL." |
| Bad format | URL doesn't parse as a valid URL | "That doesn't look like a URL. Try something like example.com." |

Error display:

```
[red ⓘ icon 12×12]  [error message — 12px, #D32F2F]
```

WDS reference: [FormField / Error](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-formfield--form-field)

---

## Attachment Chip (Post-Import)

After a site is successfully added via "Add site", the modal closes and the **attachment chip** appears in the composer action bar (V0.5) or toolbar (V1.1).

**Chip anatomy:**

```
[ favicon 13×13 ]  [ hostname (truncated 160px) ]  [ platform badge? ]  [ × remove ]
```

| Property | Value |
|---|---|
| Height | 30px |
| Padding | `0 10px` |
| Background | `#fff` |
| Border | `1px solid #E8E7E7` |
| Border radius | 24px (pill) |
| Font | 12px, `#151414` |

**Site screenshot thumbnail** (V0.5 only):

- 48×32px container, border-radius 4px, border `1px solid rgba(0,6,36,0.1)`, bg `#ECF0F3` fallback
- Image: `image.thum.io/get/width/96/crop/136/{url}`, `objectFit: cover`
- On error: image opacity → 0 (container keeps its size — no layout collapse)

**Removing the chip:** Clicking × simply removes the attachment — no undo toast.

---

## Hover Popover (V0.5 Entry Point)

When the user hovers over the "Create from URL" ghost pill in V0.5, a popover appears **below** the button.

| Property | Value |
|---|---|
| Position | `top: calc(100% + 8px)`, `left: 0` |
| Width | 220px |
| Background | `#fff` |
| Border radius | 8px |
| Shadow | `0 0 18px rgba(0,6,36,0.1), 0 6px 6px rgba(0,6,36,0.05)` |
| Arrow | 12×12 div rotated 45°, bg `#ECF0F3`, positioned at `top: -6, left: 18` |

**Image grid** — 9 real-site screenshots in a 3×3 CSS grid, rotated 6°, clipped:
- Sites: allbirds.com, notion.so, stripe.com, linear.app, framer.com, figma.com, vercel.com, shopify.com, squarespace.com
- Source: `image.thum.io/get/width/120/crop/80/{site}`
- Grid height: 118px, overflow hidden

**Text below image:**
- Title: "Start with your existing site" — 14px, weight 700, `#000624`
- Body: "Aria brings over your pages, content and brand style, ready to customize." — 12px, `#44485F`

Figma reference: node `15824:3487`

---

## Platform Detection Logic

Detection is done client-side from the URL hostname, in this order:

| Variable | Condition |
|---|---|
| `isShopify` | host contains "shop" AND does NOT contain "woo" |
| `isWoo` | host contains "woo" |
| `isWixSite` | host contains "wix" |
| `isSocial` | host contains instagram / twitter / facebook / tiktok / linkedin / pinterest |
| `isFile` | path ends in .pdf / .doc / .docx / .xls / .csv |
| `isPrivate` | host is localhost, 127.0.0.1, or starts with 192.168 |
| `isBadFormat` | URL fails `new URL()` parse |

Error states (`isWixSite`, `isSocial`, `isFile`, `isPrivate`, `isBadFormat`) block the Continue button and show inline error text. `isShopify` and `isWoo` proceed normally and surface a platform badge in results.

---

## Dev Tweaks Panel (Prototype Only)

A floating **⋮** button (bottom-right, fixed, 36×36, `#1E1E2E`, border-radius 50%) opens a dev-only panel for quickly testing states.

**Valid sites → results**

| Preset | Host |
|---|---|
| Regular site | example.com |
| Shopify store | mystore.myshopify.com |
| WooCommerce | store.woocommerce.com |

**Edge cases → errors**

| Preset | Host |
|---|---|
| Wix site | mysite.wixsite.com |
| Social media | instagram.com/mybrand |
| File URL | example.com/brochure.pdf |
| Private / localhost | localhost:3000 |
| Bad format | not a url!! |

This panel is **not** part of the production spec. It exists to help developers and reviewers quickly demo every state without manual typing.

---

## Navigation — Prototype Lobby Link

Each prototype screen includes a fixed floating nav pill (top-left, `position: fixed`, `z-index: 10000`) with a back arrow and the label **"Lobby"**. Clicking it navigates to `lobby.html`.

This nav layer is on top of all page content and must not interfere with the product UI.

---

## Component Checklist for Dev

| Component | WDS Reference |
|---|---|
| Text input | [Input](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-input--input) |
| Primary button | [Button / Primary](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Ghost button | [Button / Ghost](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Platform badge | [Badge](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-badge--badge) |
| Inline error | [FormField error](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-formfield--form-field) |
| Modal shell | [Modal](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-modal--modal) |
| Loader / spinner | [Loader](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-loader--loader) |
| Info banner | [InfoBanner / SectionHelper](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-sectionhelper--section-helper) |
| Tooltip / popover | [Tooltip](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-tooltip--tooltip) |
