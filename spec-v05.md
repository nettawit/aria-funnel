# UX Spec — Create from URL V0.5

> **Figma:** [Create from URL — Harmony](https://www.figma.com/design/ooyDmc0Qr8sQFSo6A9sWLu/Create-from-URL---Harmony?node-id=15814-40022&m=dev)
> **Prototype:** [harmony-funnel-v1.2.html](https://nettawit.github.io/aria-funnel/harmony-funnel-v1.2.html)
> **WDS Storybook:** [wix-design-system-employees](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button)

---

## Scope

This version covers three capabilities:

1. **New modal experience** — redesigned ImportFlow modal (URL entry → scanning → site preview)
2. **Store integration** — platform detection and tailored behavior for Shopify and WooCommerce sites
3. **Inject images** — site screenshot thumbnail pulled via thum.io into the attachment chip and modal preview

---

## Entry Screen

**Context:** Harmony Creation "Design your site with Aria" — the full-page composer with a text card and template row.

### "Create from URL" ghost pill

- WDS: `Button / Ghost / Medium` (38px height, `0 20px` padding, border-radius 8px)
- Label: "Create from URL"
- Prefix icon: Globe SVG 16×16 (`#767574`)
- Position: left side of the card action bar
- On click: opens `ImportFlow` modal in URL phase

### Hover popover (Figma node `15824:3487`)

Appears **below** the button on hover, `pointer-events: none`.

| Property | Value |
|---|---|
| Position | `top: calc(100% + 8px)`, `left: 0` |
| Width | 220px |
| Shadow | `0 0 18px rgba(0,6,36,0.1), 0 6px 6px rgba(0,6,36,0.05)` |
| Arrow | 12×12 div rotated 45°, bg `#ECF0F3`, at `top: -6, left: 18` |

Image grid: 9 real sites in a 3×3 CSS grid, rotated 6°, clipped at 118px height.
Sites: allbirds.com, notion.so, stripe.com, linear.app, framer.com, figma.com, vercel.com, shopify.com, squarespace.com.
Source: `https://image.thum.io/get/width/120/crop/80/{site}`

Text below grid:
- **"Start with your existing site"** — 14px, weight 700, `#000624`
- "Aria brings over your pages, content and brand style, ready to customize." — 12px, `#44485F`

### Attachment chip (post-import)

Once a site is added, the ghost pill is replaced by a chip in the action bar.

```
[screenshot 48×32]  [favicon 13×13]  [hostname]  [platform badge?]  [× remove]
```

| Property | Value |
|---|---|
| Height | 30px, padding `0 10px`, border-radius 24px |
| Background | `#fff`, border `1px solid #E8E7E7` |
| Screenshot | 48×32px container, `bg #ECF0F3`, thum.io `width/96/crop/136/{url}` |
| On error | Image opacity → 0, container keeps size (no layout collapse) |

Removing the chip: silent — no undo toast.

### Generate Site button

- WDS: `Button / Primary / Medium`, bg `#116DFF`
- Always `marginLeft: auto` so it stays right-aligned whether or not the chip is present

---

## ImportFlow Modal

Shared with V1.1. Three phases: `url` → `scanning` → `results`.

### Modal shell

| Property | Value |
|---|---|
| Width | 530px (max 95vw) |
| Border-radius | 12px |
| Shadow | `2px 20px 30px rgba(19,23,32,0.1)` |

### Header

- Title: "Create from URL" — 16px, weight 700
- Subtitle: "Use any website as a starting point" — 13px, `#767574`
- Info icon: custom SVG "i" (dot `cy=5.5` + stem `M9 8v5`). Not WDS InfoCircle — intentional per Figma.
- Close: 24×24 circle, bg `#f0efef`

### Phase 1 — URL entry

**Input field**

| Property | Value |
|---|---|
| Height | 38px, bg `#f8f6f6`, border `1px solid #C1C2C3`, border-radius 8px |
| Focus | border `#116DFF` + ring `rgba(17,109,255,0.12)` |
| Prefix | Globe icon `#767574` |
| Placeholder | "Paste a URL" |
| `Enter` key | triggers Continue |

**Continue button** — inline right of input, same row

- 38px height, `0 18px` padding, bg `#2F5DFF`, border-radius 8px, 14px/600

**Footer note:** "Only use URLs for sites you own or have permission to use"
bg `#f8f6f6`, top border `1px solid #e8e8e8`

### Phase 2 — Scanning

- Continue button → 38×38 blue icon button with rotating circular arrow SVG (`spin 0.9s linear infinite`)
- Input disabled
- Progress bar: 3px height, track `#EEEEF6`, fill `#2F5DFF` at 65%
- Label: `Analyzing "{host}"` — 12px, `#767574`

### Phase 3 — Results

**Site preview card**

- bg `rgba(255,255,255,0.4)`, `backdrop-filter: blur(7px)`, border-radius 8px
- Mac dots (3× 5px circles, `#cfd1dc`)
- Screenshot: `image.thum.io/get/width/560/crop/680/{url}`, height 238px, cover/top
- Site name + platform badge on separate line below

**Platform badges**

| Platform | Detection | Label | Bg | Color |
|---|---|---|---|---|
| Shopify | host ∋ "shop", ∌ "woo" | Shopify | `#D5DFFF` | `#383838` |
| WooCommerce | host ∋ "woo" | Woohoo | `#D5DFFF` | `#383838` |

WDS: [Badge](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-badge--badge)

**Info banner**

> "Aria will use your site's pages, content and visual style."
> Shopify: adds "…including product data, images and prices."

bg `#f5f7ff`, border `1px solid #7896ff`, prefix info circle `#2F5DFF`

WDS: [SectionHelper](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-sectionhelper--section-helper)

**Footer actions:** Cancel (outline blue) + Add site (primary blue), 30px height

---

## Error States

Inline below input row — red ⓘ icon + text, no toast.

| Error | Condition | Message |
|---|---|---|
| Wix site | host ∋ "wix" | "This is a Wix site — importing from Wix isn't supported yet." |
| Social media | host ∋ instagram/twitter/facebook/tiktok/linkedin/pinterest | "Social media profiles can't be scanned. Try your website instead." |
| File URL | path ends .pdf/.doc/.docx/.xls/.csv | "File URLs aren't supported. Paste a website address instead." |
| Private | localhost / 127.0.0.1 / 192.168.x | "This address isn't reachable. Use a publicly accessible URL." |
| Bad format | fails `new URL()` | "That doesn't look like a URL. Try something like example.com." |

WDS: [FormField error](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-formfield--form-field)

---

## Platform Detection Order

```
isShopify  host ∋ "shop" AND ∌ "woo"
isWoo      host ∋ "woo"
isWixSite  host ∋ "wix"            → error
isSocial   host ∋ instagram|twitter|facebook|tiktok|linkedin|pinterest → error
isFile     path ends .pdf|.doc...  → error
isPrivate  localhost|127.|192.168. → error
isBadUrl   new URL() throws        → error
```

---

## WDS Component Checklist

| Element | WDS |
|---|---|
| Ghost button | [Button / Ghost](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Primary button | [Button / Primary](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-actions--button) |
| Text input | [Input](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-input--input) |
| Platform badge | [Badge](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-badge--badge) |
| Inline error | [FormField](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-formfield--form-field) |
| Modal shell | [Modal](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-modal--modal) |
| Spinner | [Loader](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-loader--loader) |
| Info banner | [SectionHelper](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-sectionhelper--section-helper) |
| Popover | [Tooltip](https://www.wix-pages.com/wix-design-system-employees/?path=/story/components-tooltip--tooltip) |
