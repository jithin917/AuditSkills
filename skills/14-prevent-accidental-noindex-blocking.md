# 🔍 Skill: Prevent Accidental Search Engine Blocking (Noindex)

## 🎯 Objective
Ensure that the application is not accidentally blocking search engine crawlers via `robots.txt` rules, `noindex` meta tags, `X-Robots-Tag` headers, or hosting provider preview deployment settings. Guarantee the site is discoverable and indexable on launch day.

## 🧠 Context & "Why It Matters"
- **The Threat:** Development environments often use `noindex` tags or `Disallow: /` in `robots.txt` to prevent staging sites from appearing in Google. These settings are frequently forgotten and pushed to production.
- **Real-world consequence:** There is no error and no warning. You launch your app, but it never shows up in search results. You only find out weeks later when organic traffic is zero. 
- **The Rule:** Hosting platforms like Vercel automatically add an invisible `X-Robots-Tag: noindex` header to Preview Deployments. If your custom domain is accidentally pointing to a preview instead of production, Google will be blocked.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** deploy a production `robots.txt` containing `Disallow: /` under `User-agent: *`.
2. **NEVER** leave `<meta name="robots" content="noindex">` or framework-specific `noindex` metadata on public-facing production pages.
3. **ALWAYS** verify that custom domains in hosting platforms (Vercel, Netlify) are explicitly routed to the **Production** deployment, not a Preview or Branch deployment.

## 🔍 Audit Protocol
When triggered, scan the codebase, configuration files, and hosting setup to verify:

- [ ] **Robots.txt Check:** Inspect `public/robots.txt` (or equivalent). Flag if `Disallow: /` is present for `User-agent: *`.
- [ ] **Metadata Check:** Search the codebase (especially layout files, head components, or SEO configs) for `noindex`, `noindex, nofollow`, or `X-Robots-Tag`.
- [ ] **Hosting Routing Check (Vercel/Netlify):** Remind the user to verify in their hosting dashboard that their custom domain is assigned to the "Production" environment, not a preview branch.
- [ ] **Google Search Check:** Instruct the user to run a `site:yourapp.com` search in Google. If nothing appears and the site is new, proceed with the technical checks above.

## 🛠️ Remediation & Auto-Fix Steps
If blocking mechanisms are found, execute the following fixes:

1. **Clean Robots.txt:** Remove any `Disallow: /` rules intended for staging. Ensure it allows crawling (e.g., `User-agent: *\nAllow: /`).
2. **Remove Noindex Tags:** Delete `noindex` from metadata objects (e.g., Next.js `metadata` export) or HTML `<head>` tags.
3. **Fix Hosting Routing:** Provide step-by-step instructions: "Go to Vercel/Netlify Dashboard → Settings → Domains. Ensure your custom domain is pointing to the Production deployment. If it's on a preview, reassign it."
4. **Force Re-indexing:** Instruct the user to go to Google Search Console, use the "URL Inspection" tool on their homepage, and click "Request Indexing" to prompt Google to crawl the newly unblocked site immediately.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Indexing Audit**
> "Check my site for anything that blocks search engines: robots.txt disallow rules, noindex meta tags, and X-Robots-Tag response headers. My domain is [yourapp.com]. Tell me exactly what to remove or change to ensure Google can index my production site."

**Prompt 2: Fix Robots.txt and Metadata**
> "I suspect my site might be blocking Google. Scan my codebase for any 'noindex' tags in my metadata or layout files, and check my robots.txt for 'Disallow: /'. Remove them and prepare the files for a production deployment."

**Prompt 3: Vercel Preview Noindex Check**
> "I am using Vercel. Check if my custom domain might be accidentally pointing to a Preview deployment (which adds a noindex header). Give me the exact steps to verify and fix this in the Vercel dashboard, and tell me how to request indexing in Google Search Console afterward."