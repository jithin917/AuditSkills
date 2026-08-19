# ⚡ Skill: PageSpeed Insights & Performance Budget Enforcement

## 🎯 Objective
Ensure the application achieves a high Google PageSpeed Insights Mobile score (ideally 90+) by enforcing strict performance budgets, identifying specific bottlenecks from real Lighthouse reports, and providing prioritized, exact code changes to fix them.

## 🧠 Context & "Why It Matters"
- **The Threat:** Apps often load instantly on a developer's powerful laptop on fast Wi-Fi, but crawl on a normal mobile phone on a standard cellular connection.
- **Real-world consequence:** A page that takes 3+ seconds to load loses half its visitors before they even see the headline. On launch day, this directly translates to massive, silent user drop-off.
- **The Rule:** A mobile score under 50 must be fixed before launch. 50-89 means fix the biggest item and launch. 90+ is the goal. Never guess performance; use real budgets.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** ignore the **Mobile** PageSpeed Insights score in favor of the Desktop score. Mobile is the baseline.
2. **ALWAYS** enforce strict performance budgets: 
   - Under 1.5MB total per page.
   - Under 300KB of JavaScript.
   - Under 500KB of images above the fold.
3. **NEVER** deploy a massive, unoptimized hero image or video without lazy loading or modern compression (WebP/AVIF).

## 🔍 Audit Protocol
When triggered, analyze the provided PageSpeed Insights report or scan the codebase for common performance anti-patterns:

- [ ] **Report Analysis:** If a PSI/Lighthouse JSON or text report is provided, parse it to identify the top 3 "Opportunities" with the highest potential time savings.
- [ ] **Budget Check:** Flag any route or component that imports heavy libraries (e.g., full `lodash`, heavy charting libraries, large UI component sets) without code-splitting or lazy loading.
- [ ] **Image/Video Audit:** Identify large, unoptimized image assets (especially hero images) or auto-playing videos that block the main thread or Largest Contentful Paint (LCP).
- [ ] **Render-Blocking Resources:** Check for CSS or JS files loaded in the `<head>` without `async` or `defer` attributes.

## 🛠️ Remediation & Auto-Fix Steps
If performance issues or budget blowouts are identified, execute the following fixes in priority order (biggest speed win first):

1. **Image Optimization:** 
   - Convert large images to WebP/AVIF.
   - Add `loading="lazy"` and `decoding="async"` to below-the-fold images.
   - Use framework-specific optimized image components (e.g., Next.js `<Image>`).
2. **JavaScript Code Splitting:** 
   - Wrap heavy, non-critical components (e.g., rich text editors, complex charts, modals) in dynamic imports (e.g., `next/dynamic` or `React.lazy`).
3. **Font Optimization:** 
   - Ensure web fonts use `font-display: swap` and are preloaded if critical.
4. **Provide Exact Code Changes:** Output the precise before/after code snippets for the identified bottlenecks, explaining exactly how much bundle size or load time this will save.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: PageSpeed Report Analysis**
> "Here is my PageSpeed Insights report: [paste report text or JSON]. Give me a prioritized fix list: biggest speed win first, with the exact code change for each. Focus on Mobile performance."

**Prompt 2: Enforce Performance Budgets (Addy Osmani Skill)**
> "Speed up my site. Enforce strict performance budgets: under 1.5MB per page, under 300KB of JavaScript, and under 500KB of images above the fold. Scan my codebase, tell me which specific imports or assets blew the budget, and refactor them to be lazy-loaded or optimized."

**Prompt 3: Fix Specific LCP/CLS Issues**
> "My Largest Contentful Paint (LCP) is too slow, likely due to my hero image. Refactor my homepage to use an optimized, properly sized image component with priority loading, and ensure no layout shift (CLS) occurs while it loads."