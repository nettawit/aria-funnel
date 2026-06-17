# UX Spec — Harmony Creation V1.2 + "Add" Features

**Prototype:** [v4.html](https://nettawit.github.io/aria-funnel/v4.html)  
**Status:** Needs update  
**Last updated:** June 2026

---

## Overview

Extends the Harmony Creation composer with an **"+ Add" menu** for attaching context before generating — assets (images/videos), visual references (moodboards/URLs), and info documents. The **Create from URL** flow is also accessible from the same screen.

---

## Entry Point

- Opens directly on the HomeFlow composer (no intro screens, no typewriter animation)  
- The Create from URL modal is pre-opened when the prototype loads

---

## Greeting (static)

> **Hi! I'm Aria, your friendly design assistant.**  
> Tell me your site's name, what kind of business it is, and what makes it unique.

No typewriter animation — text appears immediately.

---

## Composer

**Textarea**  
- Placeholder: `Tell me about your site — or drag in anything that helps Aria: files, images or links…`  
- Drag-and-drop is supported (referenced in placeholder)  
- Min height: fills the card

**Footer row** (left → right)  
| Element | Type | Action |
|---------|------|--------|
| **+ Add** | Ghost button | Opens Add dropdown |
| **Create from URL** | Ghost button | Opens Create from URL modal |
| **Generate site** | Primary button (disabled) | Inert in this prototype version |

---

## "+ Add" Dropdown

Opens as a popover **above** the Add button.  
Header label: `ADD TO YOUR PROMPT`  
Closes on outside click (Escape also closes).

| Row | Icon color | Title | Description | Opens |
|-----|------------|-------|-------------|-------|
| 1 | Orange `#C05B2A` | Add assets | Upload media to use in your site | Assets modal |
| 2 | Purple `#6040D0` | Add visual references | Give Aria a look & feel to start from | Visual references modal |
| 3 | Blue `#1A6CC0` | Add info | Any info that helps Aria build a better site | Info modal |

---

## Add Assets Modal

**Header**  
- Title: `Add assets`  
- Subtitle: `Upload media to use in your site`

**Upload zone**  
- Dashed border, click to open file picker or drop files  
- Label: `Drop files here or browse your computer`  
- Sub-label: `Add as many as you like — images, video, PDF, DOCX`  
- Max file size: **25 MB** per file  
- Over-limit files are rejected with inline error showing filename(s)

**File list** (shown after adding)  
- Each file row: icon (image/video/document) + filename + remove (×)  
- Icon background color: orange `#FFF0E8` / `#C05B2A`  
- **+ Add more** button (secondary) appears below list

**Aria hint box** (blue background)  
- `Anything you'd put on your site — images, logos, videos`  
- `Aria will extract the content and visuals for you`

**Footer**  
- Left: `{N} item(s) ready` (shown when files added)  
- **Cancel** | **Add to Aria** (disabled until ≥1 file added)

**Accepted file types:** images (.png, .jpg, .jpeg, .gif, .svg, .webp), video (.mp4, .mov, .webm), documents (.pdf, .docx)

---

## Add Visual References Modal

**Header**  
- Title: `Add visual references`  
- Subtitle: `Give Aria a look & feel to start from — screenshots, moodboards, designs or links`

**Upload zone** (drag-and-drop)  
- Same dashed-border zone as Assets modal  
- Accepts image files + drag-and-drop

**URL input** (secondary option)  
- Inline URL field for pasting a reference link  
- Validation: must match `(https?://)?domain.tld` format  
- Invalid URL shows inline error

**Footer**  
- **Cancel** | **Add to Aria** (enabled when ≥1 file or valid URL)  
- On confirm: calls `onAdd({ files: [...], url: domain })` and closes modal

---

## Add Info Modal

**Header**  
- Title: `Add info`  
- Subtitle: `Any info that helps Aria build a better site`

**Upload zone** (same as Assets modal)  
- Accepts: PDF, DOCX, and other documents

**Aria hint box** (blue background)  
- `Briefs, docs, brand guides, product lists — anything with context`  
- `Aria will use them to shape a better prompt for your site`

**Footer**  
- **Cancel** | **Add to Aria** (disabled until ≥1 file added)

---

## Create from URL Modal

Same 3-step flow as the V1 Design Feature (see `spec-v1-design.md`):  
1. Enter URL  
2. Scanning (2.2s)  
3. Results with site preview + Content & design / Design only options

Accessible via **"Create from URL"** button in composer footer.

---

## Attached Items (post-add state)

After adding, a chip appears **above the textarea**:

**Asset / info chip**  
- File icon + filename + remove button

**Site chip (Create from URL)**  
- Thumbnail (48×32px) + domain name + mode label (`Content & design` / `Design only`) + platform badge

Multiple chips can be stacked. Each has its own remove button.

---

## Known Issues / Open Items

- **Generate Site** button is inert — prototype ends at the composer  
- Drag-and-drop onto the textarea area is referenced in the placeholder but interaction is not fully prototyped  
- Visual references URL flow needs design review (back button behavior)
