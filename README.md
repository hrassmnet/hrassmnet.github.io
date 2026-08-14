# hrassmnet.github.io

Personal site — [hrassmnet.github.io](https://hrassmnet.github.io)

Two pages. `/` is an overview: education, experience, achievements, contact.
`/projects` is the work itself — six cards across three groups, each with the
design decision that shaped it and the stack it runs on.

## Projects covered

| # | Project | Note |
|---|---|---|
| 01 | ITSD Email Automation | Layered triage pipeline over a shared service-desk mailbox |
| 02 | Microsoft Release Intelligence | Model judges, deterministic code scores |
| 03 | FF-ICE Flight Plan Converter | XML → ICAO text, conversion logic in sandboxed Python |
| 04 | Personal Knowledge System | Agent-maintained Obsidian corpus |
| 05 | Writing Voice Fine-Tune | Rank-32 LoRA on 51 examples — [repo](https://github.com/hrassmnet/writing-voice-lora) |
| 06 | Healthcare Market Access | Classification, regression and clustering across twelve markets |

Each card carries a hand-drawn SVG schematic (`src/components/schematics/`)
rather than a screenshot, so the architecture is legible without the reader
needing access to any of the systems.

## Stack

Astro 7 · Tailwind 4 · no client framework. Motion is dependency-free and gated
behind `prefers-reduced-motion`; every page renders fully without JavaScript.

## Running it

```sh
npm install
npm run dev      # localhost:4321
npm run build    # → ./dist
```

Requires Node ≥ 22.12. Deploys to GitHub Pages on push to `main`
(`.github/workflows/deploy.yml`).

## Structure

```
public/          static assets — CV, favicons, images, og image
src/
  pages/         index.astro · projects.astro · 404.astro
  components/    Seo.astro, schematics/
  styles/        global.css — design tokens live here
```

---

Jack Bates · [jack.don.bates@gmail.com](mailto:jack.don.bates@gmail.com)
