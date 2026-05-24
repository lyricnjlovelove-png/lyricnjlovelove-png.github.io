# 🌸 lyricnjlovelove-png.github.io

欢迎来到你的个人博客工作区！这是一个基于 **Hexo** 与 **ShokaX** 主题的高性能、极速响应的个人博客系统。

Welcome to your personal blog workspace! This is a high-performance, fast-loading personal blog system powered by **Hexo** and the **ShokaX** theme.

本项目的特色是采用了 **Monorepo** (单体仓库) 配合 **Git Submodule** (子模块) 的现代前端开发架构，使你能完美进行本地主题定制与文章内容管理，并实现完全自动化的 **CI/CD** 部署。

This project features a modern frontend development architecture utilizing **Monorepo** and **Git Submodule**, enabling seamless local theme customization, content management, and fully automated **CI/CD** deployment.

---

## 📁 Project Layout / 项目结构

```text
lyric/ (Blog Root - lyricnjlovelove-png.github.io)
├── package.json                # Main project dependencies & scripts / 主项目依赖与脚本
├── pnpm-workspace.yaml         # pnpm workspace configurations / pnpm 工作区定义
├── _config.yml                 # Hexo global configurations / Hexo 全局配置文件
├── _config.shokax.yml          # ShokaX theme custom settings / ShokaX 主题自定义设置
├── source/
│   ├── _data/
│   │   └── images.yml          # Custom post covers list (Min 6 images) / 随机封面图列表 (最少6张)
│   └── _posts/                 # Blog posts (Markdown format) / 博客文章 (Markdown 格式)
├── themes/
│   └── shokax/                 # [Git Submodule] Custom ShokaX theme source / ShokaX 主题源码子模块
├── .github/
│   └── workflows/
│       └── pages.yml           # GitHub Actions CI/CD pipeline / GitHub Actions 部署流水线
├── AGENTS.md                   # AI Agent landing instructions / 智能体运维指引总纲
└── .agents/
    └── skills/                 # AI Agent skill cards / 智能体技能卡目录
```

---

## ⚙️ Development Commands / 核心指令

你和你的 AI Agents 可以通过终端执行以下核心指令来打理博客：

You and your AI Agents can manage the blog by running the following core commands in your terminal:

| Command / 命令 | Description / 说明 |
|---|---|
| `pnpm install` | Install all dependencies and link the workspace theme / 安装项目依赖并自动软链接本地主题 |
| `pnpm --filter hexo-theme-shokax build` | Compile the ShokaX theme using `esbuild` / 编译 `themes/shokax` 中的主题源码 |
| `pnpm run clean` | Clean Hexo compiled cache and files / 清除旧的编译缓存与静态文件 |
| `pnpm run build` | Generate static website files to `public/` / 执行 Hexo 编译并生成静态页面到 `public/` 目录 |
| `npx hexo s` | Start local `development server` at `http://localhost:4000` / 启动本地开发预览服务器 |

---

## 🖥️ Local Preview & Verification / 本地开发与效果预览

要在本地预览你的修改（无论是改了文章还是定制了主题样式）：

To preview your modifications locally (whether you edited blog content or customized the theme styles):

### 1. 编译主题 (Compile Theme)
如果你修改了 `themes/shokax/` 目录下的 TypeScript, Pug, 或者是 CSS 源码，必须先执行编译：

If you edited TS, Pug, or CSS source code inside `themes/shokax/`, you must compile it first:
```bash
pnpm --filter hexo-theme-shokax build
```

### 2. 生成静态页面 (Generate Static Pages)
每次更新博客文章、图片或修改配置后，清理缓存并重新生成 HTML/CSS 静态资源：

After updating posts, images, or configurations, clean the cache and rebuild static resources:
```bash
pnpm run clean && pnpm run build
```

### 3. 运行本地开发服务器 (Run Local Server)
在项目根目录启动本地调试服务器：

Start the local server at your blog root directory:
```bash
npx hexo s
```
打开浏览器访问 **`http://localhost:4000`** 即可完美预览你的博客页面效果与交互！

Open your browser and navigate to **`http://localhost:4000`** to fully preview the blog pages and interactions!

---

## 🔧 Blog & Pages Customization / 博客与页面个性化配置

ShokaX 支持极其丰富的个性化定制。主要的配置文件说明如下：

ShokaX supports extensive custom features. The primary configuration files are:

### 1. 全局配置 (Global Configuration) -> `_config.yml`
位于项目根目录下。在这个文件中你可以修改博客的基本信息（Essential Information）：
* **`title`**: 你的博客大标题。
* **`author`**: 博客作者名字。
* **`language`**: 语言（推荐设为 `zh-CN`）。
* **`url`**: 你的博客正式上线网址，填 `https://lyricnjlovelove-png.github.io`。

Located at the root. You can modify essential site information here such as **`title`**, **`author`**, **`language`** (recommended as `zh-CN`), and **`url`** (`https://lyricnjlovelove-png.github.io`).

### 2. 主题细节配置 (Theme Custom Configuration) -> `_config.shokax.yml`
位于项目根目录下，用来定制 ShokaX 主题的外观和交互：
* **`alternate`**: 站点头部大字 Logo 标语。
* **`sidebar.avatar`**: 你的头像图片名，可以将图片放入 `source/` 下并在配置中引用它。
* **`darkmode`**: 是否开启夜间模式。
* **`modules`**: 音乐播放器 (`player`)、鼠标烟花特效 (`fireworks`)、AI 摘要 (`summary`) 等功能模块的开关。

Located at the root, used to customize ShokaX layout and UI options such as **`alternate`** (logo banner text), **`sidebar.avatar`** (profile image), **`darkmode`** (night mode toggler), and functional **`modules`** (music player, mouse fireworks, AI summary).

### 3. 随机背景图配置 (Random Background Covers) -> `source/_data/images.yml`
由于 ShokaX 包含防止页面卡死的保护逻辑，**此列表必须包含至少 6 张图片**。当你新建文章且没有手动指定封面时，系统会从这里随机挑选精美的背景大图渲染在页面顶部。

Due to thread-blocking prevention safeguards in ShokaX, **this list must contain at least 6 images**. If you write a new post without a cover, the theme randomly selects a curated background from here to render at the top banner.

---

## 🖋️ Writing Guide / 撰写与管理博客

你可以使用 AI Agents 或自己手动创建文章：

You can use AI Agents or manually manage your blog posts:

### 1. 创建新文章 (Create New Post)
在根目录下执行：
```bash
npx hexo new post "你的文章标题"
```
系统会在 `source/_posts/你的文章标题.md` 自动生成一个带有初始 **`front-matter`** 结构的文章模板。

This generates an empty markdown post template with initial **`front-matter`** at `source/_posts/your-title.md`.

### 2. 文章 Front-Matter 配置规范
打开你的文章 Markdown 文件，在顶部的 YAML 头信息中填入以下属性以发挥 ShokaX 的极致外观：

Open your markdown post and fill in the YAML block at the top with these attributes to activate ShokaX graphics:

```yaml
---
title: "你的文章标题"
date: 2026-05-24 21:16:00
tags:
  - 标签1
  - 标签2
categories:
  - 父分类
  - 子分类
cover: /images/post-cover.jpg   # 指定文章特有头图，不填则使用 images.yml 随机背景
# 指定本页面特有的 Nyx 音乐播放列表
audio:
  - title: "歌曲名"
    list:
      - https://music.163.com/#/song?id=XXXXXX
---
```

---

## 🚀 Push & Automatic Deploy / 提交与自动部署

由于我们完美配置了 **CI/CD**，你每次发布文章的部署流程都极其简单：

Since our **CI/CD** is fully configured, publishing your blog content online is extremely simple:

### 1. 仅修改了文章、图片或配置 (Content Only)
如果你只改动了文章、根目录配置或图片：
```bash
git add .
git commit -m "content: publish new post"
git push origin main
```
**GitHub Actions** 会立即自动捕获推送，构建你的整个 Monorepo 项目，并在 2 分钟内将编译好的网页自动部署到你的 Pages 域名中！

**GitHub Actions** will instantly trigger, compile the entire Monorepo project, and publish your site to your Pages domain within 2 minutes!

### 2. 修改了 `themes/shokax` 主题源码 (Theme Code Edits)
由于主题属于独立管理的 **Git Submodule**，如果你改动了主题内部代码，需要两步推送以保证云端 Actions 能获取到最新的提交：

Since the theme is maintained as a **Git Submodule**, if you edited the theme codebase, follow these steps to update the reference on GitHub:

```bash
# A. 进入子模块并推送主题代码 / Go to submodule and push theme edits
cd themes/shokax
git add .
git commit -m "custom: tweak layouts"
git push origin main

# B. 返回根目录，提交最新的子模块指针 / Return to root and commit the new pointer
cd ../..
git add themes/shokax
git commit -m "build: update theme submodule pointer"
git push origin main
```

---

## 🤖 AI Agent Integration / 智能体集成

本工作区附带了全套的 **AI Agent 规范**，任何本地智能体在连接此项目后都会查阅 **`AGENTS.md`**。你可以放心委托智能体自动执行上述所有的“写文章、更换配图、预览、子模块关联推送与 CI/CD 触发部署”的工作！

This workspace is fully optimized for AI Agent operations. Any local agent will read **`AGENTS.md`** first. You can fully delegate tasks like "adding posts, uploading images, previewing, and committing submodules" to your AI companion hands-free!
