# 21 Grams

Agent skills that make AI-built products look and feel considered. Each **scale** covers one purpose, installs on its own, and works through the components and conventions your project already has.

## Website

A guided tour of every scale, with live AI-vs-21 Grams examples you can click: [`docs/index.html`](docs/index.html). Open it in a browser, or serve the `docs/` folder with GitHub Pages.

## Scales

| Scale | What it does | Status | Docs |
|---|---|---|---|
| **ui** | Uplifts UI built by AI so it stops looking AI-generated: house style, icons, charts, toggles, UX and animation principles, design and typography hacks, unslop rules | Available | [README](skills/ui/README.md) · [Changelog](skills/ui/CHANGELOG.md) |
| **ux** | Audits and fixes the flows and usability of AI-built products: navigation, forms, empty/loading/error states, feedback, onboarding, destructive actions, accessibility, task length, choice | Available | [README](skills/ux/README.md) · [Changelog](skills/ux/CHANGELOG.md) |

## Install

**Any agent that supports skills** (Claude Code, Cursor, Codex and others). Pick the scale:

```bash
npx skills add ilbognov/21grams --skill ui
npx skills add ilbognov/21grams --skill ux
```

**Claude Code plugin** (installs every scale; they show up as `21grams:ui`, `21grams:ux`…):

```
/plugin marketplace add ilbognov/21grams
/plugin install 21grams@21grams
```

**Claude.ai:** zip a scale's folder (e.g. `skills/ui`) and upload it under *Settings → Capabilities → Skills*.

## Repo layout

```
.claude-plugin/plugin.json        the 21grams plugin (all scales)
.claude-plugin/marketplace.json   the 21grams marketplace
skills/<scale>/SKILL.md           one folder per scale: ui, ux, …
skills/<scale>/README.md          the scale's docs
skills/<scale>/CHANGELOG.md       the scale's history
docs/index.html                   the website (one self-contained page)
```

Each scale keeps its own changelog. Release tags are named `<scale>@<version>`, e.g. `ui@4.7.0`.

## License

[MIT](LICENSE)
