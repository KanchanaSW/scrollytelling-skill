# scrollytelling-data

A [Cursor](https://cursor.com) and [Claude Code](https://claude.com/claude-code) skill that builds a **data scrollytelling article**: one sticky/pinned chart, steps that scroll past it, numbers that morph — and a chart that is a **pure function of the current step index**.

Same camera philosophy as [scroll-portfolio](https://github.com/KanchanaSW/scroll-portfolio): one scroll authority, one `requestAnimationFrame` family, visual state derived from a single number. Different product: a vertical data story, not a horizontal résumé camera.

Not enter/leave choreography. Not a transition queue. Not `position: sticky` inside a transformed Lenis/GSAP parent.

## Install

Claude Code:

```bash
git clone https://github.com/KanchanaSW/scrollytelling-skill ~/.claude/skills/scrollytelling-data
```

Cursor:

```bash
git clone https://github.com/KanchanaSW/scrollytelling-skill ~/.cursor/skills/scrollytelling-data
```

Or, from a local checkout, symlink into both runtimes:

```bash
chmod +x scripts/install.sh
./scripts/install.sh
```

That links:

- `~/.cursor/skills/scrollytelling-data` — Cursor
- `~/.claude/skills/scrollytelling-data` — Claude Code

## What's in the box

```
SKILL.md                         laws + ordered workflow
references/camera.md             step-index owner, pin, ticker
references/content.md            story.ts — full snapshots, never diffs
references/gotchas.md            fast-scroll, resize, sticky-inside-transform
references/stack.md              Vite 7, Tailwind v4, GSAP register
references/structure.md          src/ tree
references/a11y.md               matchMedia, reduced motion, print
templates/                       copy-paste owner, chart, number morph, story
scripts/install.sh               dual-runtime symlink
```

## The format in one paragraph

The graphic stays on screen (ScrollTrigger pin, not sticky-inside-transform). Steps scroll beside it. Lenis owns scroll; GSAP's ticker is the only RAF; on each tick the owner measures step tops against a trigger line and writes **one** `stepIndex`. The chart renders `states[index]` — a full snapshot, never `addSeries` / `reset`. Fast-scroll to the last step shows the last snapshot, not a queued film of the beats in between. Scrolling up to step N looks like scrolling down to step N.

## After install

Restart Cursor / start a new Claude Code session so the skill description is in the catalog. Then, in any project, paste a prompt like this:

```
Use the scrollytelling-data skill. Scaffold a data scrollytelling article:
one pinned chart, scrolling steps, morphing headline numbers.
Claim: [one sentence]. Dataset: [URL or file]. Beats: [ordered list of full chart views].
```

The agent should read `SKILL.md` then `references/camera.md` before writing scroll or chart code.

### Sample command

```
Use scrollytelling-data. Build a data scrolly: pinned stacked-bar of US electricity generation, 6 steps from the 2000 mix → coal peak → gas rise → wind/solar, headline morphing on renewables share. Data from EIA. Vite + React + Lenis + GSAP pin.
```

Cursor: `@scrollytelling-data` then the same prompt. Claude Code: `/scrollytelling-data` or just the prompt after install.

### Sample ideas

Any of these work if you keep **one graphic on screen** and let scroll pick the snapshot:

| Idea | Chart | What the steps do |
|---|---|---|
| What actually grew | stacked bars, energy mix | whole mix → emphasize coal → land on solar |
| Who owns streaming | stacked area, subscriber share | 2015 pile → Netflix peak → Disney/YouTube split |
| The rent gap | dual line, median rent vs wage | both rise → wage stalls → gap at latest year |
| Cars that aren't cars | line, EV vs ICE sales | ICE plateau → EV takeoff → one market's crossover |
| Where the tax dollar goes | stacked bar, city budget | total → public safety slice → leftover for housing |
| Heat, not weather | bars, decade temperature anomaly | 1970s baseline → each decade → last decade highlighted |

A beat is a **full chart view** (marks, highlight, domain, headline number), not `{ add: 'coal' }`. If the story needs filters, a dashboard, or a horizontal résumé camera, this is the wrong skill.
