# OOD Video Matrix Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add the four `demos/OOD` videos to the project website using a 2x2 matrix that separates tasks by columns and disturbance conditions by rows.

**Architecture:** Keep the existing `Real Robot Experiments` section intact and insert one new OOD subsection between the current task demos and pruning visualizations. Build the layout directly in `index.html` with responsive Tailwind utility classes so desktop shows a matrix and mobile still preserves task and condition labels inside each card.

**Tech Stack:** Static HTML, Tailwind CSS via CDN, native HTML5 video

---

### Task 1: Add OOD robustness matrix to the demos section

**Files:**
- Modify: `index.html`
- Test: `index.html`

- [ ] **Step 1: Write the failing test**

Use text assertions that prove the new OOD subsection is not yet present:

```bash
rg -n "OOD Robustness|Assembly Line|Stack Bowls|Hand Occlusion|Laser Distraction|demos/OOD/" index.html
```

- [ ] **Step 2: Run test to verify it fails**

Run:

```bash
rg -n "OOD Robustness|Assembly Line|Stack Bowls|Hand Occlusion|Laser Distraction|demos/OOD/" index.html
```

Expected: exit code `1` with no matches because the OOD matrix has not been added yet.

- [ ] **Step 3: Write minimal implementation**

Insert a new subsection in the `#demos` section with:

```html
<div class="bg-white p-6 rounded-2xl shadow-sm border border-gray-100">
  <div class="flex flex-col md:flex-row md:items-end md:justify-between gap-3 mb-6">
    <div>
      <h3 class="text-xl font-bold text-gray-800 flex items-center gap-2">
        <i data-lucide="shield-check" class="text-emerald-600"></i> OOD Robustness
      </h3>
      <p class="text-sm text-gray-600 mt-2">Columns show tasks and rows show disturbance conditions.</p>
    </div>
  </div>
</div>
```

Then add:
- A desktop header row with `Assembly Line` and `Stack Bowls`
- One row labeled `Hand Occlusion`
- One row labeled `Laser Distraction`
- Four video cards using:
  - `demos/OOD/Assembly_Line_SAG_Hand_Occlusion.mp4`
  - `demos/OOD/Assembly_Line_SAG_Laser_Distraction.mp4`
  - `demos/OOD/Stack_Bowls_SAG_Hand_Occlusion.mp4`
  - `demos/OOD/Stack_Bowls_SAG_Laser_Distraction.mp4`
- Footer chips inside each card so mobile keeps separate task and condition labels

- [ ] **Step 4: Run test to verify it passes**

Run:

```bash
rg -n "OOD Robustness|Assembly Line|Stack Bowls|Hand Occlusion|Laser Distraction|demos/OOD/" index.html
```

Expected: multiple matches showing the new subsection heading, row and column labels, and all four `demos/OOD` sources.

- [ ] **Step 5: Verify surrounding section structure**

Run:

```bash
sed -n '295,470p' index.html
```

Expected: the new OOD subsection appears after `Task Demos` and before `Visualization for Real-time Pruning`.
