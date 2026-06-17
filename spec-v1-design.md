# UX Spec — Create from URL V1: Design Feature

**Prototype:** [v1-design.html](https://nettawit.github.io/aria-funnel/v1-design.html)  
**Status:** Needs update  
**Last updated:** June 2026

---

## Overview

Adds a **design import mode** to the Create from URL flow. After scanning a URL the user chooses whether Aria should import both content + design, or the visual style only.

---

## Entry Point

- Opens from the **"Create from URL"** button in the Harmony V1.1 composer footer  
- The modal is pre-opened when the prototype loads

---

## Modal — Step 1: Enter URL

**Header**  
- Title: `Create from URL`  
- Subtitle: `Use any website as a starting point`  
- Top-right: info icon (ⓘ) + close button (×)

**Body**  
- URL input field (autofocused)  
  - Left icon: globe  
  - Placeholder: `Paste a URL`  
  - Clear button (×) appears when field has value  
  - Supports Enter key to submit  
- CTA: **Continue** (primary blue, 38px height)

**Footer**  
- `Only use URLs for sites you own or have permission to use`

---

## Modal — Step 1b: Scanning

- URL input is **disabled** during scan  
- Continue button replaced by a **spinning loader** (blue 38×38px square)  
- Progress bar appears below input: `Analyzing "{domain}"`  
- Scan duration: ~2.2 seconds → transitions to results

---

## Validation & Error States

Errors appear inline below the input with a red icon.

| Trigger | Error message |
|---------|--------------|
| Empty field or invalid format | `Enter a full website URL, like www.example.com` |
| Wix domain (wix.com, .wixsite.com, .wixstudio.com) | `This is already a Wix site — Aria works best with sites from other platforms.` |
| Social media URL (Instagram, Facebook, TikTok, Twitter/X, LinkedIn, Pinterest, Snapchat, YouTube) | `Social media profiles can't be imported. Try a business website instead.` |
| Direct file link (.pdf, .jpg, .png, .zip, .mp4, etc.) | `This link points to a file, not a webpage. Paste the main site URL instead.` |
| Private / local URL (localhost, 127.x, 192.168.x, 10.x, 172.16–31.x) | `This URL isn't publicly accessible. Use a live website URL.` |
| Unreachable site | `Couldn't reach this site. Check the URL and try again.` |
| Timeout | `This is taking longer than expected. Try again or use a different URL.` |

Typing in the field after an error clears the error immediately.  
If user edits the URL after results are shown, modal resets to Step 1.

---

## Modal — Step 2: Results

**URL field** remains editable (editing resets to Step 1).

**Site preview card** (glassmorphism style)  
- macOS-style 3 dot row (decorative)  
- Screenshot of the scanned site via thum.io (560px wide)  
- Domain name below screenshot  
- Platform badge if detected (see detection logic below)

**Info banner** (blue, below preview card)  
- Regular site: `Aria will use your site's pages, content and visual style.`  
- Shopify: `Aria will use your site's pages, content and visual style, including product data, images and prices.`

**Design mode selection** (two options)

| Option | Label | Description | Default |
|--------|-------|-------------|---------|
| Content & design | Keep the layout, style and content | Includes products, categories & prices (Shopify only) | ✓ Selected |
| Design only | Keep the same visual style | No content imported | — |

**"All pages — always imported"** row with green checkmark (always on, not toggleable)

**Footer actions**  
- **Cancel** (outlined blue)  
- **Add to Aria** (primary blue) → attaches site chip to the composer

---

## Platform Detection Logic

| URL pattern | Badge shown | Badge color |
|-------------|-------------|-------------|
| Host contains "shop" (and not "woo") | Shopify | Blue (#D5DFFF) |
| Host contains "woo" | WooCommerce | Blue (#D5DFFF) |
| wix.com / .wixsite.com / .wixstudio.com | Error (see validation) | — |
| Other | No badge | — |

---

## Post-Add State (composer)

After clicking **Add to Aria** a chip appears above the textarea:

- Thumbnail (thum.io screenshot, 48×32px)  
- Domain name  
- Mode label: `Content & design` or `Design only`  
- Shopify badge (if applicable)  
- Remove button (×) in top-right corner of chip  

Removing the chip allows re-opening the modal.

---

## Known Issues / Open Items

- Prototype flagged as **Needs update** — design mode selection UI needs visual refresh  
- "Woohoo" badge label is a placeholder — confirm final WooCommerce label  
- Re-scan button shown in prototype header is decorative (does not re-trigger scan)
