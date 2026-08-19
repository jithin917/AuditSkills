# 🔍 Skill: Robots.txt & LLMs.txt Configuration

## 🎯 Objective
Ensure the application has a properly configured `robots.txt` file at the root directory to guide search engine crawlers, explicitly reference the `sitemap.xml`, and optionally include an `llms.txt` file to optimize the site for AI crawlers (like ChatGPT, Claude, and Perplexity).

## 🧠 Context & "Why It Matters"
- **The Threat:** Without a `robots.txt`, crawlers guess where to go, potentially wasting crawl budget on useless paths. Conversely, a misconfigured `robots.txt` (like `Disallow: /`) silently blocks the entire site from being indexed.
- **Real-world consequence:** No `robots.txt` means missed SEO opportunities. `Disallow: /` means zero organic traffic. Furthermore, as AI search grows, lacking an `llms.txt` means AI models have to parse heavy HTML to understand your product, often getting it wrong.
- **The Rule:** It tells the good bots where to go, and it's the first file Google reads on your site. It takes two minutes to set up correctly.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** deploy a production `robots.txt` containing `User-agent: *\nDisallow: /` (unless intentionally blocking a staging environment).
2. **ALWAYS** include a `Sitemap: https://yourapp.com/sitemap.xml` directive at the bottom of the `robots.txt` file.
3. **ALWAYS** allow public, marketing, and documentation routes by default. Only `Disallow` specific paths if they are genuinely public but should not be indexed (though proper authentication is the primary defense for private routes).

## 🔍 Audit Protocol
When triggered, scan the public/root directory of the codebase to verify:

- [ ] **Existence:** Check for a `robots.txt` file in the `public/` or root directory.
- [ ] **No Global Block:** Verify it does *not* contain `Disallow: /` for `User-agent: *`.
- [ ] **Sitemap Reference:** Confirm the file ends with `Sitemap: https://yourapp.com/sitemap.xml` (using the production domain).
- [ ] **LLMs.txt (Optional but Recommended):** Check for an `llms.txt` file in the root/public directory that provides a concise, markdown-formatted summary of the product, key features, and links to important documentation.

## 🛠️ Remediation & Auto-Fix Steps
If the file is missing or misconfigured, execute the following fixes:

1. **Generate Standard `robots.txt`:** Create a clean, permissive `robots.txt` file.
   ```text
   User-agent: *
   Allow: /
   
   # Optional: Disallow specific public but non-indexable paths
   # Disallow: /api/
   # Disallow: /admin/
   
   Sitemap: https://yourapp.com/sitemap.xml