# UX Spec — Harmony Creation V1.2 + "Add" Features

**Prototype:** [v4.html](https://nettawit.github.io/aria-funnel/v4.html)  
**Status:** Needs update  
**Last updated:** June 2026

---

## Overview

Harmony Creation V1.2 expands the prompt composer with an **"Add" menu** — letting users attach assets, visual references, or info documents before generating their site. The **Create from URL** modal is also accessible from the same composer.

---

## Entry Point

Opens on the HomeFlow composer screen directly (no intro screens).  
Static greeting — no typewriter animation.

---

## Greeting

> **"Hi! I'm Aria, your friendly design assistant."**  
> Tell me your site's name, what kind of business it is, and what makes it unique.

---

## Composer

- Large textarea: placeholder "Tell me about your site — or drag in anything that helps Aria: files, images or links…"
- Footer row (left to right):
  - **+ Add** button (ghost)
  - **Create from URL** button (ghost)
  - **Generate site** button (primary, right-aligned) — disabled in prototype

---

## "+ Add" Dropdown

Opens as a popover above the Add button, titled **"ADD TO YOUR PROMPT"**.

| Option | Icon color | Title | Description |
|--------|------------|-------|-------------|
| **Add assets** | Orange | Add assets | Upload media to use in your site |
| **Add visual references** | Purple | Add visual references | Give Aria a look & feel to start from |
| **Add info** | Blue | Add info | Any info that helps Aria build a better site |

### Add Assets modal
- Title: "Add assets"
- Subtitle: "Upload media to use in your site"
- Hints: "Anything you'd put on your site — images, logos, videos" / "Aria will extract the content and visuals for you"
- Upload zone + file list
- CTA: **Add to Aria** (disabled until file added)

### Add Visual References modal
- Title: "Add visual references"
- Subtitle: "Give Aria a look & feel to start from — screenshots, moodboards, designs or links"
- Accepts: image files + URLs
- CTA: **Extract** → **Add to Aria**

### Add Info modal
- Title: "Add info"
- Subtitle: "Any info that helps Aria build a better site"
- Hints: "Briefs, docs, brand guides, product lists — anything with context" / "Aria will use them to shape a better prompt for your site"
- CTA: **Add to Aria**

---

## Create from URL

Same 3-step modal as the V1 Design Feature flow (see `spec-v1-design.md`).  
Accessible via the **"Create from URL"** button in the composer footer.

---

## Attached Items (post-add state)

After adding any item, a chip appears above the textarea:
- Asset chip: file name + remove button
- Site chip: thumbnail + domain + mode label + platform badge

---

## Open Questions / Known Issues

- Generate Site button is inert in this prototype version
- "Add visual references" URL input flow needs design review
- Drag-and-drop onto the textarea is referenced in the placeholder copy — confirm if in scope
