# 📊 Skill: Analytics Installation & Firing Verification

## 🎯 Objective
Ensure that a web analytics tool (e.g., PostHog, Plausible, Google Analytics) is correctly installed, configured, and—critically—actually firing on the production domain before launch. Guarantee that launch-day visitor data is captured and cannot be lost.

## 🧠 Context & "Why It Matters"
- **The Threat:** "Installed" is not the same as "working." Analytics snippets are frequently wrapped in environment checks that only run in development, or reference keys that aren't set in production.
- **Real-world consequence:** Launch day brings 2,000 visitors, but your analytics dashboard shows 0 because the tracking snippet only fired in development. That valuable launch traffic data is gone forever—there is no way to measure yesterday's visitors.
- **The Rule:** Your launch traffic only happens once. Without analytics, you'll never know which post drove the traffic, or why nobody signed up. Verify it fires on the live domain, not just localhost.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch without confirming analytics is actively recording on the production domain. Installation alone is insufficient.
2. **NEVER** gate the analytics snippet behind a `NODE_ENV === 'development'` check by accident. Ensure it runs in production.
3. **ALWAYS** verify tracking via the analytics dashboard's real-time view after deploying to the live domain.
4. **ALWAYS** ensure analytics respects user consent if a cookie/consent banner is in place (referencing Skill #Legal/Cookie Banner).

## 🔍 Audit Protocol
When triggered, scan the codebase and configuration to verify the analytics setup:

- [ ] **Provider Detection:** Identify which analytics tool is installed (PostHog, Plausible, GA4, Vercel Analytics, etc.) by checking `package.json`, layout files, and `<head>`/`<body>` scripts.
- [ ] **Environment Gate Check:** Inspect the analytics initialization code. Flag if it is incorrectly wrapped in a development-only condition, or if it requires an environment variable (e.g., `NEXT_PUBLIC_POSTHOG_KEY`) that may be missing in production.
- [ ] **Production Presence:** Verify the tracking snippet or provider component is rendered on the live production domain, not just localhost.
- [ ] **Event Firing Check:** Confirm that at least the default `pageview`/`$pageview` event is being captured, plus any custom conversion events (e.g., `signup_completed`).
- [ ] **Real-Time Verification (Manual Step):** Instruct the user to open the live site in an incognito tab and confirm their visit appears in the analytics dashboard's real-time/live view.

## 🛠️ Remediation & Auto-Fix Steps
If analytics is missing or not firing in production, execute the following fixes:

1. **Install PostHog (Recommended for early stage):** 
   - PostHog's free tier is exceptionally generous and open source. 
   - *Next.js:* Install `posthog-js` and wrap the app in a `PostHogProvider` in the root layout, using `NEXT_PUBLIC_POSTHOG_KEY` and `NEXT_PUBLIC_POSTHOG_HOST`.
2. **Fix Environment Gating:** 
   - Remove any accidental development-only conditions around the analytics initialization.
   - Ensure the required public environment variable is added to the production hosting environment (e.g., Vercel Project Settings > Environment Variables).
3. **Add Provider to Root Layout:** 
   - Generate the provider wrapper code so analytics loads globally across all pages.
4. **Add Conversion Events:** 
   - Instrument at least one meaningful conversion event (e.g., capture `signup_completed` in the auth success callback) so you can measure funnel drop-off.
5. **Provide Verification Checklist:** Output a manual checklist for the user to confirm it works on the live domain:
   - "Step 1: Deploy to production."
   - "Step 2: Open the live site in an incognito tab."
   - "Step 3: Open the PostHog dashboard > Activity/Real-time view."
   - "Step 4: Confirm your incognito visit appears. If not, check the browser console and network tab for blocked requests (ad blockers)."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Install Analytics (PostHog)**
> "Install PostHog analytics in my Next.js app. Set up the PostHogProvider in my root layout using NEXT_PUBLIC_POSTHOG_KEY and NEXT_PUBLIC_POSTHOG_HOST environment variables. Ensure it runs in production, and add it to my .env.example file. Also capture a 'signup_completed' event when a user successfully signs up."

**Prompt 2: Verify Analytics Is Firing**
> "Check my analytics setup. Identify which analytics tool is installed, verify it isn't accidentally gated behind a development-only environment check, and confirm the required environment variables are being used correctly. Give me a step-by-step checklist to verify it's actually firing on my live production domain using the real-time dashboard view."

**Prompt 3: Fix Dev-Only Analytics Snippet**
> "My analytics snippet only seems to run in development, not in production. Inspect my analytics initialization code, remove any incorrect development-only conditions, and ensure the tracking fires on the live domain. Also tell me where to add the analytics API key in my hosting provider's environment variables."