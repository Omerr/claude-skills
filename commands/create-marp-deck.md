# Create Marp Slide Deck

Create a presentation slide deck using the Marp markdown format, following the established conventions in this repo.

## Arguments
- `$ARGUMENTS` - Optional topic hint for the deck

## Phase 1: Interview

Before generating anything, interview the user by asking these questions **one at a time**, waiting for each answer before proceeding to the next. Use `AskUserQuestion` for each question.

**Question 1 — Goal & Topic:**
Ask: "What's this presentation about? What should the audience walk away knowing or being able to do?"

**Question 2 — Audience:**
Ask: "Who's the audience? (e.g., engineering team, executives, external clients, conference attendees)"

**Question 3 — Key Points:**
Ask: "What are the key points or sections you want to cover? List the main ideas, even if rough."
- If the user provides files, URLs, or references, read/fetch them thoroughly before continuing.

**Question 4 — Data & Demos:**
Ask: "Any specific data, code examples, diagrams, or demos to include? Do you have these ready, or should I create them?"

**Question 5 — Format:**
Ask: "Is this a **briefing deck** (read as much as presented — data, decisions, internal review) or a **narrative talk** (live on stage, one argument carried end to end)?" This decides the structure in Phase 2.

**Question 6 — Constraints:**
Ask: "Any constraints? Think: target number of slides, time limit for the talk, things to avoid, or specific branding requirements."

After collecting all answers, briefly summarize what you understood and ask for confirmation before proceeding.

## Phase 2: Generate the Deck

You are creating a Marp slide deck in the `presentations/` directory. Pick the structure that matches the format from Question 5, then follow the conventions below.

### Reference decks (read one before you start)
- **Narrative talk** (hook, progressive reveals, journey maps, sourced speaker notes): `presentations/embarrassing-ai.md`
- **Briefing deck** (parts, tables, takeaways): pick a current deck in `presentations/` (e.g. `disfluency-founders.md`). Do not reference decks that no longer exist.

A narrative talk leans on four things a briefing deck doesn't need: **progressive reveal**, **one running example threaded throughout**, a **recurring visual callback**, and **rich speaker notes**. All four are described below.

---

## FRONTMATTER

Every deck starts with this frontmatter:

```yaml
---
marp: true
theme: default
paginate: true
size: 16:9
html: true
---
```

`html: true` is **required** — every custom component below uses raw HTML (`<div>`, `<img class>`, `<audio>`). Without it Marp silently strips the HTML and those slides render blank. The export command must also pass `--html` (see EXPORTING).

---

## CSS STYLE BLOCK

Immediately after the frontmatter, include a `<style>` block. Start from the base below, then paste in only the components the talk actually uses (COMPONENT CATALOG). Treat the catalog as a parts bin — copy what you need from the reference deck rather than regenerating styling from scratch.

The base block:

1. **Base font sizes** for section, table, blockquote, pre
2. **Header styles** for breadcrumb navigation (gray text, blue for active section)
3. **Section classes** for the title slide and each part/section divider - gradient backgrounds, white text

### Color palette for section dividers (pick 2-4 based on number of parts):
- Blue: `linear-gradient(135deg, #1e3a5f 0%, #2d5a8e 100%)`
- Green: `linear-gradient(135deg, #064e3b 0%, #047857 100%)`
- Amber: `linear-gradient(135deg, #7a4a1a 0%, #a66b2e 100%)`
- Purple: `linear-gradient(135deg, #3d1e5c 0%, #5a2d8e 100%)`
- Title slide (always dark navy): `linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #0f172a 100%)`

### Base template:

```html
<style>
section { font-size: 24px; }
table { font-size: 18px; }
blockquote { font-size: 26px; }
pre { font-size: 16px; }
header { font-size: 14px; color: #999; }
header strong { color: #2563eb; }
section.title-slide {
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #0f172a 100%);
}
section.part-FIRST,
section.part-SECOND,
section.part-THIRD,
section.title-slide {
  --h1-color: #fff;
  --heading-strong-color: #fff;
  --fgColor-default: rgba(255, 255, 255, 0.95);
  --fgColor-muted: rgba(255, 255, 255, 0.7);
  color: white;
}
section.part-FIRST  { background: linear-gradient(135deg, #1e3a5f 0%, #2d5a8e 100%); }
section.part-SECOND { background: linear-gradient(135deg, #064e3b 0%, #047857 100%); }
section.part-THIRD  { background: linear-gradient(135deg, #3d1e5c 0%, #5a2d8e 100%); }
</style>
```

Replace `FIRST`, `SECOND`, `THIRD` with short descriptive names for each part (e.g., `part-context`, `part-results`, `part-summary`).

---

## SLIDE STRUCTURE

### Briefing deck — linear, read-as-much-as-presented

1. **Title Slide**
```markdown
<!-- _class: lead title-slide -->

# Main Title
## Subtitle

**Key detail 1**: value
**Key detail 2**: value
**Date**: Month Year
```

2. **Questions / Goals slide** — 3-5 questions the deck answers, numbered list with bold lead-ins.

3. **Agenda slide**
```markdown
<!-- _class: lead title-slide -->

# Agenda

### Part 1: Name
Short description

### Part 2: Name
Short description
```

4. **Per part**: section divider + content slides (see below).
5. **Final slides** — summary/takeaways within the last section.

### Narrative talk — one argument, carried live

1. **Cold-open hook** (before the title) — `<!-- _class: lead hook-slide -->`, `<!-- _paginate: false -->`. An audio clip, a provocative quote, a live demo. No "today I'll talk about…".
2. **Title slide** (same as above).
3. **Roadmap** — a `reveal-stack` (or plain fragments) that builds the map of the talk in 2-3 clicks, instead of a bullet agenda.
4. **Per section**: a `progress-map` interstitial → colored divider → content slides → another `progress-map` with the state advanced.
5. **Takeaways** → final `progress-map` (all done) → **thank-you / resources** slide with a QR to a sources page.

### Section divider (both modes)
```markdown
<!-- _header: "" -->
<!-- _class: lead part-NAME -->

# Part N: Section title

**One-line description**
```

### Content slide with breadcrumb (both modes)
```markdown
<!-- header: "Part 1: **Chatbots** · Agents&nbsp;&nbsp;-&nbsp;&nbsp;Part 2: Why · Takeaways" -->

# Slide title

Content here
```
The breadcrumb shows where you are. The active section is wrapped in `**bold**`. The `header` directive persists until changed — set it once on the first content slide of a section. Reset with `<!-- _header: "" -->` before each divider, hook, or progress-map.

---

## COMPONENT CATALOG

Each is a `section` class. Paste its CSS into the style block and use the markup pattern. The full, current CSS for all of these lives in `presentations/embarrassing-ai.md` — copy from there rather than retyping.

### `progress-map` — the journey slide (signature device for narrative talks)
A full slide between sections showing the whole arc with done ✓ / active / next / takeaway ★ states. Appears once up front as the roadmap, then again at every section boundary with states advanced. This is what gives the audience a felt sense of place — the single most valuable narrative component.

```html
<!-- _header: "" -->
<!-- _paginate: false -->
<!-- _class: progress-map -->

<div class="parts">
  <div class="part p1 active">Part 1 · The tales</div>
  <div class="part p2">Part 2 · Why &amp; fixes</div>
</div>
<div class="track">
  <div class="step done c1"><div class="badge">✓</div><div class="label">Chatbots</div></div>
  <div class="arrow done">→</div>
  <div class="step next"><div class="badge">2</div><div class="label">Agents</div></div>
  <div class="arrow">→</div>
  <div class="step"><div class="badge">?</div><div class="label">Why</div></div>
  <div class="arrow">→</div>
  <div class="step takeaway"><div class="badge">★</div><div class="label">Takeaways</div></div>
</div>
```
State classes: `done` (✓ filled), `active`/`next` (highlighted, dashed), `takeaway` (★). Copy the `section.progress-map …` CSS block from the reference deck verbatim.

### `reveal-stack` — cumulative diagram built one click per layer
Absolutely-stacked images centered on a dark slide; each `* ![…]` fragment lays the next frame over the last. For building a diagram or kill-chain step by step. Pair with multi-frame SVGs (`thing_1.svg`, `thing_2.svg`, …) where frame N contains frame N-1 plus one new element.
```markdown
<!-- _class: reveal-stack -->

* ![Frame 1 description, doubles as narration cue](images/thing_1.svg)
* ![Frame 2 adds the next layer](images/thing_2.svg)
* ![Frame 3, the payoff](images/thing_3.svg)
```

### `big-number` / `big-quote` — single-statement impact slides
`# 1,522` rendered huge, or one italic quote on near-black. Reveal cold, let it land, then advance.

### `chat` — chat-bubble transcript
`* ` list items alternate user (odd, left, light) / AI (even, right, blue). Lead each bubble with a bold speaker label. A trailing list item carrying only `<img class="stamp">` renders as a bare callback stamp, not a bubble.

### `shot` — framed screenshot on dark background
`# Title` + one shadowed image + optional caption bullets. For product screenshots and tool dashboards.

### `diagram` — full-bleed single image on dark.

### `hook-slide` — cold-open (audio / big quote, centered, purple-dark).

### `interstitial` ("MEANWHILE…") / `somber` — tonal-shift slides.

### `image-swap` / `image-stack` / `islreveal` — positioned image reveals where a later frame pops over an earlier one (query → answer → image). Tune per-image `w:`/`h:` directives.

### Recurring callback motif (narrative)
A small image reused across slides as a running punchline — e.g. `<img class="stamp" src="images/…png">` pinned bottom-right, with escalating variants (`stamp s2`, `s3`, `s4`) piled on via separate fragments. Pick one motif and let it recur; it ties the talk together.

### Corner metadata badge
A persistent `<div class="story-date">Apr 2026</div>` top-right on story slides — a running device the audience learns to read ("watch the date").

---

## PROGRESSIVE REVEAL

Use plain `* ` bullet lists for click-by-click reveal — in marp-cli 4.4.x each top-level `* ` item auto-fragments. **Do not** use `<div data-marpit-fragment>`; it gets stripped. Numbered `1.` lists do not fragment — use `* `. This drives most of a narrative talk. Order fragments so each click is one beat: setup → turn → payoff.

---

## SPEAKER NOTES (required for narrative talks, encouraged for all)

Every content slide gets an HTML comment after it with:
- **DELIVERY**: how to pace it — what to reveal, where to hold, the keeper line.
- **CITATIONS**: for any factual claim, the primary source (URL, incident-DB ID, paper). Fact-heavy talks live or die on this; keep the receipts in the notes so they're at hand for Q&A.
- **Q&A prep**: anticipated questions and the facts that answer them.

```markdown
<!--
DELIVERY: Reveal the number cold. Hold. Then click to the curve.
CITATIONS:
- The Register, "...": https://...
- AI Incident Database #1039: https://incidentdatabase.ai/cite/1039/
-->
```

Notes are part of the deliverable, not an afterthought — they're what lets a human present the deck under stage pressure.

---

## FORMATTING RULES

1. **Sentence case for all headings** — only capitalize the first letter and proper nouns (e.g., "Get started in 5 minutes", not "Get Started in 5 Minutes"). Breadcrumb headers follow the same rule
2. **No trailing periods** on bullets, text lines, or table cells
3. **Single dash** (`-`) for parenthetical separators, never em-dashes — anywhere, deck or SVG
4. **Backticks** for program names, file names, and technical identifiers (not bold)
5. **Bold** for emphasis on key phrases and findings
6. **Tables** for data comparisons - keep them concise
7. **Blockquotes** (`>`) for key callouts or distinctions
8. **One idea per slide** - if a slide is getting dense, split it into two
9. Keep bullet lists to 3-5 items max per slide
10. No parenthetical notes in the slide body unless absolutely necessary
11. **Descriptive alt text** on every image — write it as a full sentence so it doubles as the presenter's narration cue and serves accessibility
12. **Per-slide pagination**: add `<!-- _paginate: false -->` on hooks, progress-maps, and interstitials

---

## ASSETS

- Images/SVGs go in `presentations/images/`. For `reveal-stack`, author multi-frame SVGs that are visually cumulative.
- Audio for a live demo: `<audio controls src="clip.mp3"></audio>`, file next to the deck. Renders a play button in the HTML.

---

## EXPORTING

HTML is the real deliverable for any component-heavy deck:

```bash
npx @marp-team/marp-cli@latest --no-stdin --html FILENAME.md -o FILENAME.html
```

- `--html` is **mandatory** — without it raw HTML components are stripped.
- `--no-stdin` prevents marp from hanging on stdin.

**Plain (non-editable) PPTX** is a lossy fallback — custom CSS, audio, `progress-map`, and animated reveals do **not** survive it. Only produce it for a plain briefing deck, and warn the user that components won't render:

```bash
npx @marp-team/marp-cli@latest --no-stdin --pptx FILENAME.md -o FILENAME.pptx
```

### Publishing (optional)
A talk deck can ship with a companion **resources page** — a standalone `…-resources.html` listing every source and tool, linked from a QR on the thank-you slide. If the project has a deploy script for the deck (e.g. `scripts/deploy-<name>.sh`), run it after edits to publish HTML + resources to GitHub Pages.

---

## EDITABLE PPTX EXPORT (OPTIONAL)

If the user asks for editable PPTX (text that can be edited in PowerPoint or Google Slides), run these additional steps. This requires LibreOffice and python-pptx to be installed. Note: this still does not preserve custom-component styling — it is meant for plain text-and-bullet decks.

```bash
# PPTX - editable text (experimental, requires LibreOffice)
npx @marp-team/marp-cli@latest --no-stdin --pptx --pptx-editable --allow-local-files FILENAME.md -o FILENAME-editable.pptx
python3 -c "
from pptx import Presentation
from pptx.util import Emu
prs = Presentation('FILENAME-editable.pptx')
margin = Emu(747720)
for slide in prs.slides:
    for shape in slide.shapes:
        if shape.has_text_frame and shape.shape_type == 17:
            tf = shape.text_frame
            if not tf.text.strip() or tf.text.strip().isdigit():
                continue
            font_size = None
            if tf.paragraphs and tf.paragraphs[0].runs:
                font_size = tf.paragraphs[0].runs[0].font.size
            if not font_size:
                continue
            new_width = prs.slide_width - margin - shape.left
            if new_width > shape.width:
                shape.width = new_width
            min_height = int(font_size * 1.4) * 2
            if shape.height < min_height:
                shape.height = min_height
            tf.word_wrap = True
prs.save('FILENAME-editable.pptx')
"
```

Notes:
- `--allow-local-files` needed for local images
- `--pptx-editable` requires LibreOffice installed
- The python-pptx post-processing fixes text box sizing issues from LibreOffice conversion
- Always use `--no-stdin` to prevent marp from hanging on stdin
