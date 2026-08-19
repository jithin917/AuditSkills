# 🛡️ Skill: Remove Localhost & Staging URL Leakage

## 🎯 Objective
Eradicate all references to development, staging, or preview environments (e.g., `localhost`, `127.0.0.1`, `.vercel.app`, `staging.domain.com`) from the production codebase and built output. Ensure all absolute URLs dynamically resolve to the correct production domain.

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers frequently hardcode URLs during local development for convenience. Because everything works perfectly on their local machine, these hardcoded values slip through code review and into the production build.
- **Real-world consequence:** An Open Graph preview image loads from `localhost:3000` (working for the dev, but broken for every real user). A canonical tag points to a staging URL, telling Google to index the wrong site and wasting SEO authority. API callbacks fail because they point to a dead preview deployment.
- **The Rule:** Everything looks fine when you test locally. That's exactly why these survive until launch day. Never trust hardcoded URLs.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** hardcode `localhost`, `127.0.0.1`, `.vercel.app`, `.netlify.app`, or any staging domain in production code, metadata, sitemaps, or email templates.
2. **ALWAYS** use a dedicated environment variable (e.g., `NEXT_PUBLIC_APP_URL`, `VITE_APP_URL`, `process.env.BASE_URL`) for constructing absolute URLs.
3. **ALWAYS** verify that canonical tags, sitemap `<loc>` entries, and Open Graph `og:image` URLs use the production environment variable.

## 🔍 Audit Protocol
When triggered, perform a comprehensive search across the codebase and configuration files:

- [ ] **Codebase Grep:** Search all files for `localhost`, `127.0.0.1`, `staging`, `.vercel.app`, `.netlify.app`, or any known old dev domains.
- [ ] **Metadata & Head Check:** Specifically inspect `<link rel="canonical">`, `<meta property="og:image">`, and `<meta property="og:url">` for hardcoded development URLs.
- [ ] **Sitemap Check:** Verify `sitemap.xml` (or generator) uses the production base URL, not a local or preview URL.
- [ ] **Callback/Webhook Check:** Ensure OAuth callbacks (e.g., Google, GitHub) and Stripe webhook URLs are configured to use the production environment variable, not a hardcoded local tunnel (like `ngrok`) or preview URL.

## 🛠️ Remediation & Auto-Fix Steps
If hardcoded development URLs are found, execute the following fixes:

1. **Define Environment Variable:** Ensure a `NEXT_PUBLIC_APP_URL` (or framework equivalent) is defined in `.env.example` with a placeholder like `https://yourapp.com`.
2. **Search and Replace:** 
   - Identify all instances of hardcoded local/staging URLs.
   - Replace them with template literals using the environment variable (e.g., `` `${process.env.NEXT_PUBLIC_APP_URL}/image.png` ``).
3. **Framework-Specific Helpers:** If using Next.js, suggest using `new URL(path, process.env.NEXT_PUBLIC_APP_URL)` or a dedicated `lib/utils.ts` helper to safely construct absolute URLs.
4. **Clean Up:** Remove any leftover development-only redirect rules or middleware that might be forcing staging behavior in production.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive URL Leakage Audit**
> "Search my codebase and built output for hardcoded URLs pointing to localhost, 127.0.0.1, preview/staging domains (like .vercel.app), or old dev domains. Flag every instance, especially in metadata, canonical tags, sitemaps, and image sources. Tell me exactly what to replace with my production environment variable."

**Prompt 2: Auto-Fix Hardcoded URLs**
> "I want to eliminate all localhost and staging URLs from my production build. Find every hardcoded development URL in my code and replace it with a dynamic reference using process.env.NEXT_PUBLIC_APP_URL (or the correct env var for my framework). Add NEXT_PUBLIC_APP_URL to my .env.example file."

**Prompt 3: Webhook & Callback Verification**
> "Check my OAuth callbacks (e.g., Clerk, NextAuth) and Stripe webhook configurations. Ensure they are not hardcoded to localhost or ngrok URLs, and update them to use the production environment variable so they work correctly when deployed."