# CLAUDE.md — hrassmnet.github.io

Personal site for Jack Bates. Astro + Tailwind, static, deployed to GitHub Pages
via GitHub Actions. Read this file at the start of every session and follow it
exactly. When something here conflicts with a general instinct about "good web
design", this file wins.

Always invoke the `frontend-design` skill for any UI work in this project.

---

## 1. What this is

Two pages, one identity.

| Route | Job | Layout |
|---|---|---|
| `/` | Overview. Cinematic, short on text. Makes someone want to click through. | **Vertical** scroll |
| `/projects` | The substance. Six project cards. Where someone actually reads. | **Vertical** scroll |

The contrast between the two is deliberate. The overview performs; the projects
page works. Both use the identical design system so it's obviously one site.

Audience: graduate roles (Palantir, Apple) and MS applications (KAIST GSDS).
Tone: plain, factual, first person, no selling. If a sentence sounds like a
LinkedIn post, delete it.

---

## 2. Design system

These are the only values. Never introduce a colour, size, or font outside them.

### Colour

```css
--bg:          #FAFAF9;  /* page background — near-white, faintly warm */
--surface:     #FFFFFF;  /* cards, raised panels */
--text:        #0A0A0B;  /* primary text */
--text-muted:  #6B6B72;  /* secondary text, captions */
--rule:        #E4E4E7;  /* hairlines, borders, schematic strokes */
--accent:      #0866FF;  /* Meta blue — links, active states, one element per schematic */
--accent-soft: #4A9EFF;  /* gradient endpoint only */
--accent-wash: rgba(8, 102, 255, 0.06); /* subtle fills, hover backgrounds */
```

Bright site. Near-white background everywhere. **No dark mode, no dark sections,
no toggle.** Accent is used sparingly — if more than roughly 5% of a viewport is
blue, it's too much.

### Type

Two families only. Load via Fontsource, self-hosted, not Google's CDN.

```css
--font-display: 'Space Grotesk', system-ui, sans-serif;  /* everything text */
--font-mono:    'JetBrains Mono', ui-monospace, monospace; /* labels, numbers, data */
```

Mono is for: section labels, years, metric values, stack tags, schematic
annotations, card index numbers. Everything else is Space Grotesk.

Scale:

```
display-xl  4.5rem / 1.02 / -0.03em   weight 700   hero name
display-l   3rem   / 1.08 / -0.02em   weight 700   panel headings
h2          2rem   / 1.15 / -0.01em   weight 600
h3          1.375rem / 1.3            weight 600   card titles
body        1.0625rem / 1.6           weight 400
small       0.9375rem / 1.5           weight 400
label       0.75rem / 1 / 0.08em      weight 500   MONO, UPPERCASE
```

Prose never exceeds **68ch**.

### Spacing

4px base. Use only: `4 8 12 16 24 32 48 64 96 128 192`. Panels are generously
spaced — whitespace is the main aesthetic device here, not ornament.

### Structural language

Borrowed from Anduril's discipline, applied on a bright canvas:

- Thin hairline rules (`1px solid var(--rule)`) separating sections
- Mono section labels, uppercase, letter-spaced, small, muted
- Numeric indices on things (`01`, `02`, `03`)
- Tight alignment to a 12-column grid, 24px gutters
- Data presented like readouts, not like marketing copy
- Sharp corners or near-sharp (`border-radius: 2px` max)

---

## 3. Motion

Library: **GSAP + ScrollTrigger**. No other animation library.

### Rules

1. **Never hijack scroll.** No custom scroll velocity, no smooth-scroll libraries
   overriding native behaviour. The scrollbar must stay real.
2. **`prefers-reduced-motion: reduce`** disables entrance animation entirely and
   renders panels static. Non-negotiable.
3. Durations `0.4s`–`0.8s`, easing `power2.out`. Nothing snaps.
4. Entrance animations: opacity + small Y translate (max 16px). Nothing flies in.

---

## 4. Schematics

Every project card and interest panel gets a small hand-built SVG diagram. They
must all look like one family.

- Inline SVG, `viewBox`-based so they scale
- Stroke `1.5px`, colour `var(--rule)`
- Labels: JetBrains Mono, 10px, uppercase, `letter-spacing: 0.08em`, `var(--text-muted)`
- **Exactly one element per schematic uses `var(--accent)`** — the thing the
  diagram is actually about
- No fills except `var(--accent-wash)`
- No icons, no illustrations, no stock graphics. Boxes, lines, arrows, nodes.

---

## 5. Page: `/` (overview, vertical)
## 5a. Creative latitude

Sections 2, 3, 7 and 9 are constraints — palette, type, motion physics,
accessibility, performance. Do not deviate.

Everything about *layout, composition and visual invention* is yours.
Section 5 below specifies what each panel must contain and what it's for.
It does not specify how it should look. Where the two conflict, the brief
wins over my layout suggestion.

Take real risks with composition. This site should not look like a
template. Specifically, you have latitude to:

- Break the grid deliberately where it creates tension
- Use extreme scale contrast (very large type against very small mono)
- Let panels differ structurally from each other rather than repeating
  one layout seven times
- Use negative space aggressively — a panel can be mostly empty
- Invent structural devices I haven't described, as long as they use the
  existing tokens

The failure mode to avoid is not "too weird". It's "safe, centred,
evenly-spaced, looks like every other portfolio". Bias toward the
former.

### Working method

For each panel, propose 2–3 distinct compositional directions in a short
written description before building any of them. I'll pick one. Do not
build a single option and ask for feedback — I'm better at choosing
between things than at describing what I want.
Panels top to bottom:

**01 — Hero**
```
JACK BATES
Business Information Systems — University of Galway
Change is inevitable. Progress isn't.
```
Name, affiliation line, and the site's closing line echoed quietly beneath,
one step up in weight. No metrics, no positioning statement.

**02 — Journey**
Leaving Cert → University of Galway → TBS Education Barcelona → `?`

Rendered as a horizontal timeline within the vertical page — a line the eye
travels left to right across the panel. Year markers in mono. The right-hand
edge terminates in an unlabelled `?` — the future is deliberately open.

**03 — Experience**
EUROCONTROL, Brussels — Power Platform & AI Solutions Engineer (Skyline
Traineeship, 2026). Built AI agents for the Network Management Directorate.
Two or three sentences. Do not repeat Galway/TBS here — they belong to the
Journey panel.

**04 — Projects door**
Full-height panel, large type, single link to `/projects`. This is a designed
moment, not a nav item. Keep the label plain — "Projects".

**05 — Achievements**
Compact. Mono list, hairline-separated, no cards, no badges, no icons:
- ISO 8000 Master Data Quality Manager — ECCMA
- Enhance agents with autonomous capabilities — Microsoft Applied Skills
- First Class Honours — Y1 71% · Y2 75%
- Academic Scholarship — Y1 & Y2
- Leaving Cert — Kearney, Pat Carty & Offaly Historical Society Awards — 601 points
- SAP Design Thinking Challenge — 4-person team, circular-economy platform design

Deliberately understated. The projects carry the weight; this is supporting
evidence.

### 06 — Interests

Three items, presented as a triptych. Word + image only. NO prose,
NO explanatory sentences, NO node strips.

- HISTORY — image, Augustus of Prima Porta
- CYBERNETICS — image or icon, mechanical/systems aesthetic
- PHILOSOPHY — The Creation of Adam, detail of the two hands

Coherence comes from identical treatment, not identical subject matter:
same aspect ratio, same desaturation toward the palette, same 1px rule
frame, same mono label placement. They must read as one set, not three
found images.

This overrides the "no icons/images" rule in section 7 for this panel only.

**07 — Contact / Footer**
- jack.don.bates@gmail.com
- GitHub: github.com/hrassmnet
- CV (PDF download)

Closing line, set quietly, mono or small display:

> Change is inevitable. Progress isn't. What separates them is what we manage to build.

---

## 6. Page: `/projects` (vertical)

Persistent minimal header with a link back to `/`.

Three groups, hairline-separated, each with a mono section label:

**EUROCONTROL** — cards 01, 02, 03
**PERSONAL** — cards 04, 05
**ACADEMIC** — card 06

### Card anatomy

```
01                                    [schematic]
ITSD Email Automation
<body copy>
25,000+ emails in production
Copilot Studio · Power Automate · ServiceNow · SharePoint · Power BI
```

Index in mono. Title in h3. Body copy as written below — **do not rewrite it,
do not "improve" it, do not add adjectives.** Metric chips in mono with
`--accent-wash` background. Stack tags in mono, muted, dot-separated.

### Card content — use verbatim

**01 — ITSD Email Automation**

Continuous pipeline on the ITSD shared mailbox. Every incoming email gets
classified, checked against the ServiceNow knowledge base, and then answered,
ticketed, or handed to a human. Each decision is logged to SharePoint and
surfaced in Power BI.

The design problem was trust: cheap filters run before the agent so the
expensive call only fires when it's needed, and if the KB search wasn't
performed, confidence drops to LOW and a person takes over — regardless of how
certain the model sounded.

`25,000+ emails in production`
Copilot Studio · Power Automate · ServiceNow · SharePoint · Power BI

---

**02 — Microsoft Release Intelligence**

Microsoft ships hundreds of M365 and Azure changes a year and someone has to
work out which ones matter to whom. This ingests them through a public MCP
server, weighs impact against internal knowledge, scores it, and routes by
priority — high-impact items through human approval, mid-tier into a weekly
digest, the rest logged.

The agent classifies but never scores. Judgement is probabilistic, arithmetic is
deterministic, and they don't share a layer.

`800+ updates processed` · `~8 hrs/week saved`
MCP server · Copilot Studio · Power Automate · SharePoint

---

**03 — FF-ICE Flight Plan Converter**

Flight plans are moving from the old ICAO text format to a new XML standard
called FF-ICE. Both are in use during the changeover, so people need to convert
between them. I built an agent in Copilot Studio where you paste the XML in and
get the text format back.

The first version had the LLM reading a written rulebook to parse the XML, plus
a separate flow handling the number formatting. When code execution became
available I replaced all of it with one Python script. The model doesn't touch
the conversion now — it passes the XML to the script and returns what comes back.

Copilot Studio · Python · Agent Sandbox

---

**04 — Personal Knowledge System**

Built an agent that takes my ramblings and notes and puts them into structured
form I can actually check back on — almost an interactive journal. Stored
locally in Obsidian, run through Claude Code.

I throw raw material at it, articles, notes, whatever, and it files it, links it
to what's already there, and flags anything sitting on its own with nothing
pointing at it.

Claude Code · Obsidian · Markdown

---

**05 — Writing Voice Fine-Tune**

Fine-tuned a small open-weight model on 51 examples of my own writing to see
whether a LoRA on that little data could pick up tone, structure and register.
Built the dataset by hand from real emails, technical notes and essays rather
than generating it, then tested against the base model on three prompts held
out of training.

Style transferred, facts didn't. The model took on the register convincingly
but invented biographical details it had no way to hold at this scale — that's
a retrieval problem, not a training one. On a prompt unrelated to anything in
the data it did worse than the base model it started from.

`51 examples · rank-32 LoRA` · `GitHub → writing-voice-lora`
Unsloth · Llama-3.2-1B · LoRA · Google Colab

---

**06 — Healthcare Market Access**

Hackathon case for Bayer. They're launching a therapy across European markets
where pricing rules, reimbursement decisions and approval timelines vary by
country. The question was where to focus to maximise market share and sales.

Worked through 10,000 records across twelve countries — classification on
reimbursement approval, regression on market share and revenue, clustering to
see how the markets grouped. Access conditions decided almost everything; price
barely moved adoption until reimbursement was secured. Markets split cleanly
into access-constrained and access-enabled.

The recommendation was to sequence launches by access rather than market size,
and price after access is won rather than before.

`Full analysis (PDF)` · Python · pandas · scikit-learn · statsmodels

---

## 7. Hard don'ts

- No dark backgrounds or dark mode toggle
- No gradient backgrounds, mesh gradients, or aurora blobs
- No glassmorphism, blur panels, or frosted effects
- No stock icons, icon libraries, or emoji
- No scroll hijacking or custom scroll physics
- No parallax
- No typewriter effects, glitch text, particle fields, or matrix rain
- No Inter, no purple, no generic SaaS landing page patterns
- No adjectives in project copy — no "innovative", "cutting-edge", "passionate"
- No stacked CTAs or marketing language anywhere
- No `localStorage` or `sessionStorage`
- No third-party analytics

---

## 8. Build order

Do these as separate slices. Commit after each. Don't jump ahead.

1. **Design system** — tokens, fonts, a bare page rendering the type scale and
   colour swatches. Nothing else. Get this approved first.
2. **`/projects`** — vertical, static, all six cards, no motion, no schematics
   yet. This page carries the content, so it gets built early.
3. **`/` structure** — all seven panels laid out vertically. Content and
   hierarchy only.
4. **Schematics** — the six card diagrams, the two interest diagrams. One at
   a time, same conventions.
5. **Polish** — favicon, meta tags, OG image, print stylesheet, 375px pass,
   Lighthouse check.

---

## 9. Technical constraints

- Static output only. No SSR, no server functions.
- Target: under 1s load on 4G. Watch bundle size — GSAP is the only heavy
  dependency and should be loaded as a client island on `/` only, not on
  `/projects`.
- All images: WebP, sized, `loading="lazy"` below the fold.
- Contrast must pass WCAG AA.
- Site must be fully readable and navigable with JavaScript disabled.
- PDFs live in `public/` — `cv.pdf`, `bayer-analysis.pdf`.
