# FiOS — Architecture Updates

Design vault for **FiOS (FRIDAY Integrated Operating System)**: a minimal, security-first, Arch-based distro with a local AI assistant.

**Live site:** https://vishnu7553.github.io/fios-architecture-updates/

The published site is built from the Obsidian notes in [`content/`](content) with [Quartz](https://quartz.jzhao.xyz/). Wikilinks, backlinks, the graph, Mermaid diagrams, and the architecture canvas are rendered there.

## Layout

| Path | What it is |
|---|---|
| `content/` | The Obsidian vault (open this folder as a vault) |
| `quartz.config.yaml` | Site title, base URL, plugins, theme |
| `quartz/` | Quartz source |
| `.github/workflows/deploy-pages.yml` | Builds and deploys to GitHub Pages on push to `main` |

## Local preview

Requires Node.js 22 or newer.

```bash
npm install
npx quartz build --serve
```

Then open http://localhost:8080.

Edit notes in `content/`, push to `main`, and GitHub Pages rebuilds automatically.

## Start here

On the live site, start at the home page, then open **Home** for the mind map. Or read [`content/Home.md`](content/Home.md) directly.
