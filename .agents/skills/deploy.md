# 🚀 Agent Skill: Preview, Build, and Deploy

This skill sheet instructs the AI agent on how to preview changes locally, build the Hexo site, and deploy updates to GitHub Pages using the monorepo submodule setup.

---

## 🛠️ Step 1: Local Preview and Verification

Always verify changes locally before pushing them to production:

1. **Clean and Generate the Website**:
   Run this in the root folder to clean old cache and build static pages:
   ```bash
   pnpm run clean && pnpm run build
   ```
2. **Compile the Theme (If theme source code was modified)**:
   If any files in `themes/shokax/` (CSS, Pug, JS, TS) were modified, you **must** compile the theme:
   ```bash
   pnpm --filter hexo-theme-shokax build
   ```
3. **Generate Pagefind Search Index (Optional)**:
   If `pagefind` search is enabled in `_config.shokax.yml`, run this after generating pages:
   ```bash
   pnpm dlx pagefind --site public
   ```
4. **Start the Local Server**:
   Start the local preview server:
   ```bash
   npx hexo s
   ```
5. **Inspect the Site**: Open `http://localhost:4000` in the browser. Check that:
   * Newly added posts render perfectly.
   * Images display correctly with valid paths.
   * No console errors or layout breakage are present.

---

## 📦 Step 2: Committing and Deploying (CI/CD)

Because this project is structured as a **Monorepo with Git Submodules**, you must follow specific Git workflows depending on what you changed.

### Case A: You only changed blog posts, configurations, or images (No theme edits)
If you only added/edited markdown posts in `source/_posts/` or changed configurations in the root folder:
1. Stage, commit, and push in the root folder:
   ```bash
   git add .
   git commit -m "content: publish new post"
   git push origin main
   ```
2. **What happens next?** GitHub Actions will automatically catch the push, build the site using the workspace configuration, and publish the HTML pages to your `github.io` page within 2 minutes.

---

### Case B: You modified the ShokaX Theme source code in `themes/shokax`
If you edited files inside `themes/shokax/`:
1. **First, commit and push changes inside the Submodule**:
   ```bash
   cd themes/shokax
   git add .
   git commit -m "custom: tweak theme layouts/styles"
   git push origin main
   cd ../.. # Return to the root folder
   ```
2. **Next, update the submodule pointer in the Root Repository**:
   In the root directory, Git will detect that `themes/shokax` has a new commit hash. You must stage and commit this updated pointer:
   ```bash
   git add themes/shokax
   git commit -m "build: update theme submodule pointer"
   git push origin main
   ```
3. **Why is this necessary?** If you don't push inside the submodule and update the pointer in the root, the GitHub Actions CI/CD runner won't see your theme modifications, and your published online blog will continue to render using the old theme code.
