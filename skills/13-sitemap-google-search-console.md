# 🔍 Skill: Sitemap Generation & Google Search Console Setup

## 🎯 Objective
Ensure the application has a valid, production-ready `sitemap.xml` that is correctly referenced in `robots.txt`, and guide the user to submit it to Google Search Console for fast, monitored indexing and crawl error detection.

## 🧠 Context & "Why It Matters"
- **The Threat:** Without a sitemap, search engine crawlers must discover your pages organically through external links, which can take weeks for a new site. 
- **Real-world consequence:** You launch your app, but for three weeks, Google has no idea you exist. Furthermore, without Google Search Console, you are flying blind regarding crawl errors, indexing failures, or broken pages.
- **The Rule:** A sitemap provides faster indexing and a free dashboard showing exactly what Google sees. Always verify the sitemap contains your real production domain, never a staging or localhost URL.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** include login-protected, private, or staging URLs in the `sitemap.xml`. Only list public, indexable pages (e.g., landing, pricing, blog, public profiles).
2. **NEVER** use relative paths or `localhost`/`staging` domains in the `<loc>` tags of the sitemap. All URLs must be absolute and point to the production domain.
3. **ALWAYS** ensure the `sitemap.xml` is explicitly referenced in the `robots.txt` file (`Sitemap: https://yourapp.com/sitemap.xml`).

## 🔍 Audit Protocol
When triggered, scan the codebase and project structure to verify:

- [ ] **Sitemap Existence:** Check if a `sitemap.xml` (or framework-specific sitemap generator, like Next.js `app/sitemap.ts`) exists.
- [ ] **Content Validation:** If it exists, verify it only contains absolute URLs matching the production domain and excludes private/authenticated routes.
- [ ] **Robots.txt Reference:** Check the `public/robots.txt` (or equivalent) to ensure it contains the `Sitemap: https://yourapp.com/sitemap.xml` directive.
- [ ] **Localhost/Staging Check:** Grep the sitemap and robots files for `localhost`, `127.0.0.1`, or `.vercel.app` / `.netlify.app` URLs to prevent accidental staging indexing.

## 🛠️ Remediation & Auto-Fix Steps
If the sitemap is missing, incomplete, or misconfigured, execute the following fixes:

1. **Generate Sitemap:** 
   - *Next.js (App Router):* Generate an `app/sitemap.ts` file that dynamically or statically exports an array of public URLs with `lastModified` dates.
   - *Vite/React/Static:* Generate a static `public/sitemap.xml` file listing the core public routes.
2. **Update Robots.txt:** 
   - Generate or update `public/robots.txt` to include:
     ```text
     User-agent: *
     Allow: /
     Sitemap: https://yourapp.com/sitemap.xml
     ```
3. **Provide GSC Instructions:** Output clear, step-by-step instructions for the user to manually verify their domain in Google Search Console and submit the sitemap URL in the "Sitemaps" tab.
4. **Framework-Specific Plugins:** If applicable, suggest plugins like `next-sitemap` for older Next.js pages router setups.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Sitemap Audit & Creation**
> "Run the Sitemap Audit. Check if my app has a valid sitemap.xml listing all public pages (landing, pricing, blog) with absolute production URLs. If missing, create one and ensure it is referenced in my robots.txt. Exclude any login-protected or private routes."

**Prompt 2: Next.js App Router Sitemap**
> "Create a Next.js App Router sitemap.ts file for my app. Include my main public routes (/, /pricing, /about) and provide a placeholder for dynamic routes (like /blog/[slug]). Also, update my robots.txt to point to this sitemap."

**Prompt 3: Google Search Console Prep**
> "My sitemap is ready at https://myapp.com/sitemap.xml. Give me a step-by-step checklist on how to verify my domain in Google Search Console and submit this sitemap so Google can start indexing my pages immediately."