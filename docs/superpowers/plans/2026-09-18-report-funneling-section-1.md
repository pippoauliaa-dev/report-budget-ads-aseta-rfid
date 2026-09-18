# Report Funneling Section 1 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans (recommended) or superpowers:subagent-driven-development to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the existing multi-section report with a clean Section 1 funnel report for Aseta and RFID WMS Total Solution.

**Architecture:** Keep the report as a self-contained static `index.html` with inline CSS and no new dependencies. Use responsive HTML cards and CSS trapezoid layers for the two funnels; expose the supplied funnel metrics, deal attribution, revenue, ad spend, spend/revenue ratio, and ROAS directly in the page.

**Tech Stack:** HTML5, CSS3, vanilla JavaScript-free static presentation.

**Spec:** Section 1 requirements approved in conversation on 2026-09-18.

## Global Constraints

- Keep only the funnel report section in the published page; do not retain the old budget trend, before-after, learning phase, or recommendation sections yet.
- Use Indonesian copy and Indonesian Rupiah formatting.
- Do not add dependencies or external assets.
- Aseta funnel stages are `Leads → Meeting → Trial / Quotation → Deal Contract`.
- RFID funnel stages are `Leads → Meeting → Quotation → Deal Contract`.
- Aseta spend is Rp7.829.027 and revenue is Rp46.155.104; ROAS is 5,90x and spend/revenue is 16,96%.
- RFID spend is Rp4.848.486 and revenue is Rp125.500.000; ROAS is 25,88x and spend/revenue is 3,86%.
- Aseta deals are RS Dewi Sri Karawang (Rp693.750, lead Agustus Week 2), SiCepat (Rp20.214.404, lead Agustus Week 2), and PT Gregah Sukses Mandiri (Rp25.246.950, lead Juli Week 4).
- RFID revenue is First Luxury Singapore, developed from First Luxury Indonesia, and must appear as a footnote.

---

### Task 1: Replace the report with the approved funnel section

**Files:**
- Modify: `index.html`
- Modify: `README.md`

**Interfaces:**
- Produces a responsive, standalone page at the existing GitHub Pages URL.
- Uses semantic `.funnel-panel`, `.funnel`, `.funnel-stage`, `.deal-list`, and `.efficiency-grid` structures for the final section.

- [ ] **Step 1: Replace the old document with the section-only layout**

Create a compact page containing:
- Hero title and period context.
- A two-column responsive grid.
- An Aseta panel with four funnel layers, its three deal details, and efficiency metrics.
- An RFID panel with four funnel layers, its efficiency metrics, and the First Luxury footnote.
- A short methodology note clarifying that revenue is based on recorded contracts and may originate from earlier leads.
- CSS media queries for mobile stacking and accessible contrast.

Use CSS `clip-path: polygon(...)` on each stage to create the widening/narrowing funnel appearance without an image dependency. Keep the stage text in normal HTML inside each shape.

- [ ] **Step 2: Update repository documentation**

Update `README.md` so its scope describes the current Section 1 funnel report and the displayed period rather than the removed sections.

- [ ] **Step 3: Verify the static report**

Run:
```bash
git diff --check
git status --short
```

Expected: no whitespace errors; only the intended report and documentation files changed. Search the generated HTML to confirm the old section headings do not remain:
```bash
python -c "from pathlib import Path; s=Path('index.html').read_text(encoding='utf-8'); assert 'Budget & delivery trend' not in s; assert 'Report Funneling' in s; print('static checks passed')"
```

- [ ] **Step 4: Commit the completed section**

```bash
git add index.html README.md docs/superpowers/plans/2026-09-18-report-funneling-section-1.md
git commit -m "feat: rebuild report as funnel section"
```

- [ ] **Step 5: Push the approved change**

```bash
git push origin main
```
