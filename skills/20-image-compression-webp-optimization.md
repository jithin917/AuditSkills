# 🖼️ Skill: Image Compression & WebP Optimization

## 🎯 Objective
Ensure all images in the application are compressed, resized to their actual display dimensions, and converted to modern, highly efficient formats like WebP or AVIF. Guarantee that no single image exceeds 1MB to maximize page load speed and minimize mobile data usage.

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers often export or download high-resolution images (e.g., 4K screenshots, uncompressed PNGs) and drop them directly into the project folder without optimization.
- **Real-world consequence:** A 3.8MB `hero.png` forces every mobile visitor to download megabytes of data before they can even read the headline. This is the #1 reason new apps feel sluggish and suffer from high bounce rates.
- **The Rule:** Ideally, no image on the site is over 1MB. Page speed is one of the biggest reasons people leave a website. Optimize before you commit.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** commit or deploy an image file larger than 1MB without explicit, justified exception (and even then, heavily scrutinize it).
2. **ALWAYS** prefer modern image formats like WebP or AVIF over legacy PNG or JPEG for photographs, screenshots, and complex graphics.
3. **ALWAYS** resize images to the *maximum dimensions they are actually displayed at* in the UI. Do not serve a 4000px wide image to be displayed at 400px wide.

## 🔍 Audit Protocol
When triggered, scan the codebase (especially `public/`, `assets/`, or `static/` directories) to identify optimization opportunities:

- [ ] **File Size Check:** Identify all `.png`, `.jpg`, and `.jpeg` files larger than 500KB (flag >1MB as critical).
- [ ] **Format Check:** Flag opportunities to convert large PNGs/JPEGs to WebP or AVIF.
- [ ] **Component Usage:** Check if the framework's optimized image component is being used (e.g., Next.js `<Image>`, Astro `<Image>`, Nuxt `<NuxtImg>`) instead of raw `<img>` tags, which handle responsive sizing and lazy loading automatically.
- [ ] **Display vs. Actual Size:** If possible, estimate if an image's intrinsic resolution vastly exceeds its CSS/rendered dimensions.

## 🛠️ Remediation & Auto-Fix Steps
If oversized or unoptimized images are found, execute the following fixes:

1. **Automated Compression (CLI):** 
   - If the environment supports it, use `cwebp` (the same engine as Squoosh) to compress images. 
   - *Example command:* `cwebp -q 80 input.png -o output.webp`
2. **Update Code References:** 
   - Search the codebase for the old image filenames (e.g., `hero.png`).
   - Replace them with the new optimized filenames (e.g., `hero.webp`).
3. **Implement Optimized Components:** 
   - Replace standard `<img src="..." />` tags with framework-specific optimized components (e.g., Next.js `<Image src="/hero.webp" width={800} height={400} priority />` for above-the-fold content).
4. **Manual Squoosh Fallback:** 
   - If CLI tools are unavailable, instruct the user: "Go to squoosh.app, drag and drop your large images, select WebP, adjust the quality slider until the file is under 500KB, download, and replace the file in your `public/` folder."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Image Audit & Fix**
> "Find all images in my app's public or assets folder. Identify any that are over 500KB. Provide the exact CLI commands (using cwebp or similar) to convert them to WebP at 80% quality, and then update all code references in my codebase to point to the new .webp files."

**Prompt 2: Next.js Image Optimization**
> "Scan my codebase for standard <img> tags. Replace them with Next.js <Image> components, ensuring I am using the correct width, height, and 'priority' attributes for above-the-fold images to prevent layout shift and improve loading."

**Prompt 3: Manual Squoosh Workflow Guide**
> "I have a few large hero images and screenshots. Give me a step-by-step guide on how to use squoosh.app to compress them to WebP format under 500KB each, and tell me exactly where to place them in my Next.js project structure."