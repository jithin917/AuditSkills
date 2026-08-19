# 📈 Skill: Real User Monitoring (RUM) & Core Web Vitals Tracking

## 🎯 Objective
Enable Real User Monitoring (RUM) to collect field data on Core Web Vitals (LCP, INP, CLS) from actual visitors. Establish a performance baseline from day one and continuously monitor real-world user experience.

## 🧠 Context & "Why It Matters"
- **The Threat:** PageSpeed Insights only tells you how your site runs on Google's fast, wired test machines. It does not tell you how your site runs on a user's three-year-old Android phone connected to spotty hotel Wi-Fi.
- **Real-world consequence:** Users leave because the app feels sluggish in the wild, and you have zero data to prove it or fix it. If you wait until week three to turn on tracking, you have no baseline and lost three weeks of critical performance data.
- **The Rule:** The data only collects while the toggle is on. Turn it on before launch. You must monitor the "Big Three": 
  1. **LCP (Largest Contentful Paint):** < 2.5 seconds (Loading)
  2. **INP (Interaction to Next Paint):** < 200 milliseconds (Responsiveness)
  3. **CLS (Cumulative Layout Shift):** < 0.1 (Visual Stability)

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch a production application without Real User Monitoring (RUM) or Web Vitals tracking enabled.
2. **NEVER** rely solely on lab data (Lighthouse/PageSpeed) to judge production performance. Field data is the ultimate source of truth.
3. **ALWAYS** set up alerts or regular reviews for when LCP, INP, or CLS cross their respective "red" thresholds (2.5s, 200ms, 0.1).

## 🔍 Audit Protocol
When triggered, scan the codebase and hosting configuration to verify RUM is active:

- [ ] **Provider Detection:** Check for the installation of RUM providers:
  - *Vercel:* Look for `@vercel/speed-insights` in `package.json` and `<SpeedInsights />` in the root layout.
  - *PostHog:* Check if Web Vitals tracking is enabled in the PostHog dashboard and if `posthog-js` is configured to capture performance metrics.
  - *Sentry:* Check for `@sentry/browser` performance monitoring configuration.
- [ ] **Root Layout Injection:** Verify the tracking component/script is injected at the root layout level so it fires on every page.
- [ ] **Metric Verification:** Ensure the tool is specifically configured to report LCP, INP, and CLS (not just generic page load times).

## 🛠️ Remediation & Auto-Fix Steps
If RUM is missing or not configured correctly, execute the following fixes:

1. **Vercel Setup (Easiest for Next.js):**
   - Install the package: `npm install @vercel/speed-insights`
   - Add the component to the root `app/layout.tsx` (or `pages/_app.tsx`):
     ```tsx
     import { SpeedInsights } from "@vercel/speed-insights/next"
     // ... inside the return:
     <SpeedInsights />
     ```
2. **PostHog Setup:**
   - Instruct the user: "Go to your PostHog Project Settings > Web Vitals and toggle it ON."
   - Ensure the `posthog-js` initialization in the codebase includes performance tracking (it does by default in recent versions).
3. **Fixing "Red" Metrics (When data comes in):**
   - If the user reports that LCP, INP, or CLS is in the red based on their RUM data, activate the specialized Core Web Vitals skill to fix the specific bottleneck:
     ```bash
     npx skills add addyosmani/web-quality-skills --skill core-web-vitals
     ```
   - Tell the AI: "My real user INP is 450ms. Use the core-web-vitals skill to find the long tasks blocking the main thread and fix them."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Enable Web Vitals (Vercel/Next.js)**
> "Enable Real User Monitoring for my Next.js app hosted on Vercel. Install `@vercel/speed-insights`, add it to my root layout, and ensure it's tracking LCP, INP, and CLS from day one."

**Prompt 2: Enable Web Vitals (PostHog)**
> "I am using PostHog for analytics. Walk me through enabling the Web Vitals toggle in the dashboard, and verify my `posthog-js` setup in the code is correctly configured to capture and send Core Web Vitals data."

**Prompt 3: Fix Red Web Vitals from RUM Data**
> "My Real User Monitoring dashboard shows my INP (Interaction to Next Paint) is in the red at 350ms, and my LCP is 3.2 seconds. Run the core-web-vitals audit on my codebase to identify the long tasks and heavy elements causing this, and give me the exact code fixes."