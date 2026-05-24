# 🤖 AI Agent Guidelines for Hexo ShokaX Workspace

Welcome, Agent! This repository is a Monorepo Workspace containing a Hexo blog and a customized ShokaX theme. This guide outlines the project layout, development commands, and how to execute specific automated tasks.

---

## 📁 Directory Map

* `/` (Root): The Hexo blog site workspace. Contains global config `_config.yml` and theme config `_config.shokax.yml`.
* `/source/_posts/`: Your main folder for writing blog posts (in Markdown format).
* `/source/images/`: Images and static assets for blog posts.
* `/themes/shokax/`: A Git Submodule containing the TypeScript/esbuild source code for the **hexo-theme-shokaX** theme.
* `/AGENTS.md`: This file (guidelines and landing page).
* `/.agents/skills/`: Step-by-step skill instruction sheets for executing common automated tasks.

---

## ⚙️ Core Development Commands

As an agent, you can execute the following commands in the root directory:

| Command | Action |
|---|---|
| `pnpm install` | Install all workspace dependencies and link the local theme. |
| `pnpm --filter hexo-theme-shokax build` | Compile the ShokaX theme (TypeScript & esbuild compilation). |
| `npx hexo s` | Start local Hexo preview server (default: `http://localhost:4000`). |
| `pnpm run clean` | Clean compiled static pages cache. |
| `pnpm run build` | Generate compiled static website output to `/public/`. |

---

## 🧠 Agent Automation Skills

We have defined specialized skill cards inside `/.agents/skills/` for common maintenance tasks. Always read these files before performing the corresponding task:

1. **[Add Blog Post Skill](file:///.agents/skills/add_post.md)** (`/.agents/skills/add_post.md`): How to create, write, and format blog posts using ShokaX's recommended markdown front-matter (covers, local audio players, tags, categories).
2. **[Change Image Skill](file:///.agents/skills/change_image.md)** (`/.agents/skills/change_image.md`): How to receive a new image, save it to the correct assets directory, optimize it, and embed it correctly.
3. **[Deploy Skill](file:///.agents/skills/deploy.md)** (`/.agents/skills/deploy.md`): How to compile the theme, generate the static site, verify the build, and push to GitHub to trigger GitHub Pages CI/CD.

---

## 🚦 Important Guidelines for Agents

* **Submodule Care**: The theme in `/themes/shokax` is a Git submodule. Do not commit theme changes inside the root blog repository. If you make modifications inside `themes/shokax`, they must be committed and pushed to its own origin (`lyricnjlovelove-png/hexo-theme-shokaX`).
* **Theme Build Requirement**: Whenever you edit CSS, Pug, or TypeScript files inside the theme, you **MUST** run `pnpm --filter hexo-theme-shokax build` to compile the changes, otherwise the Hexo server won't reflect them.
* **Keep Site Config Independent**: Customize global parameters in `_config.yml` and ShokaX specific settings in `_config.shokax.yml` (located in the root). Do not hardcode configurations inside the theme's core code.
