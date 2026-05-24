# 🖼️ Agent Skill: Change or Add Images

This skill sheet instructs the AI agent on how to manage images (site avatars, post covers, post-body inline images) for the Hexo ShokaX blog.

---

## 📁 Image Directory Standards

Always place images in their designated folders inside the `source/` directory to ensure they compile and deploy properly:

| Image Type | Target File/Directory | How to reference in markdown |
|---|---|---|
| **Site Avatar** | `source/avatar.jpg` | Refer to as `avatar.jpg` in `_config.shokax.yml` |
| **Post Covers & Galleries** | `source/images/` | Refer to as `/images/your-image.jpg` |
| **Blog Post Inline Body Images** | `source/images/` | Refer to as `![alt](/images/your-image.jpg)` |

---

## 🛠️ Execution Steps

### 🦄 Scenario A: Replacing the Blog Avatar
If the user asks to change their profile picture/avatar:
1. Receive the new image.
2. Rename and save the image to `source/avatar.jpg` (or another custom filename like `avatar.png`).
3. If a different name is used, update `_config.shokax.yml`:
   ```yaml
   sidebar:
     avatar: avatar.png
   ```

### 🖼️ Scenario B: Adding a Post Cover or Inline Image
If the user asks to add an image to a blog post or set a post cover:
1. Ensure the `source/images/` directory exists.
2. Save the image file inside `source/images/` (recommend using descriptive lowercase names with hyphens, e.g. `source/images/my-trip-cover.jpg`).
3. Link the image:
   * **For post cover**: Set the `cover` field in the markdown's YAML front-matter:
     ```yaml
     cover: /images/my-trip-cover.jpg
     ```
   * **For inline post body**: Use the standard Markdown syntax:
     ```markdown
     ![Short description of the photo](/images/my-trip-cover.jpg)
     ```

---

## 📏 Best Practices & Image Optimization

1. **Formats**: Prefer `.webp` or `.jpg` for photos to ensure fast page loads, and `.png` for screenshots or graphics requiring transparency.
2. **File Size**: Ideal image size should be **under 500KB** for post covers and **under 200KB** for inline body images. If an image is larger than 1MB, recommend compression (using local tools like `sharp` or system utilities) before uploading to avoid slowing down the blog load time.
3. **Accessibility**: Always provide a meaningful alternative text (`alt` tag) for inline images. Do not use generic alt text like "image" or "photo".
