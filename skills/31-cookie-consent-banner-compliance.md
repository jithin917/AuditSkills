# 🍪 Skill: Cookie Consent Banner & Privacy Compliance

## 🎯 Objective
Implement a non-intrusive, GDPR/ePrivacy-compliant cookie consent banner that blocks tracking cookies until explicit user consent is given. Ensure analytics falls back to a cookieless/anonymous mode if rejected, persist the user's choice, and link to a detailed cookie policy.

## 🧠 Context & "Why It Matters"
- **The Threat:** Many analytics and tracking tools drop cookies and start tracking by default on the very first pageview. Under GDPR and ePrivacy laws, this is illegal without prior, explicit consent.
- **Real-world consequence:** Full cookie tracking from the first pageview with no banner and incoming EU traffic is a direct compliance violation. This is a legal letter and potential fine waiting to happen.
- **The Rule:** Setting this up takes 20 minutes max. It is absolutely worth your time to protect your app and respect user privacy. A banner alone isn't enough; you must also have a cookie policy explaining what is tracked.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** initialize tracking scripts that drop cookies (e.g., standard Google Analytics, Hotjar, Facebook Pixel) before the user explicitly clicks "Accept".
2. **ALWAYS** provide a graceful degradation path: if the user rejects cookies, the analytics tool must operate in a strict "cookieless" or anonymous mode (e.g., PostHog's `on_rejection` mode).
3. **ALWAYS** persist the user's consent choice (via `localStorage` or a minimal, non-tracking cookie) so the banner does not reappear on every single page load.
4. **ALWAYS** include a link in the banner to a dedicated "Cookie Policy" page that explains exactly what is tracked and why.

## 🔍 Audit Protocol
When triggered, scan the codebase and UI to verify consent management:

- [ ] **Banner Presence:** Check if a cookie consent banner component exists and renders on the first visit (simulated via cleared `localStorage`).
- [ ] **Analytics Gating:** Inspect the analytics initialization code (e.g., PostHog, GA4). Verify it is wrapped in a conditional check that waits for the `consent === 'accepted'` state.
- [ ] **Cookieless Fallback:** Verify that if consent is rejected, the analytics provider is configured to not drop cookies (e.g., PostHog `cookieless_mode: 'on_rejection'` or `persistence: 'memory'`).
- [ ] **Persistence:** Ensure the user's choice is saved and the banner component reads this state on mount to prevent re-rendering.
- [ ] **Policy Link:** Confirm the banner contains a link to a `/cookie-policy` page.

## 🛠️ Remediation & Auto-Fix Steps
If consent management is missing or non-compliant, execute the following fixes:

1. **Install a Consent Component:** 
   - Recommend a lightweight, accessible component (e.g., the free shadcn-compatible component: `https://github.com/r2hu1/shadcn-cookie-consent` or a similar minimal library).
2. **Wire Up Analytics:** 
   - Refactor the analytics provider initialization to listen to the consent state.
   - *PostHog Example:* Configure `cookieless_mode: 'on_rejection'` and only call `posthog.init()` after checking the stored consent state.
3. **Generate Cookie Policy:** 
   - Use the specialized legal skill to generate a compliant cookie policy page: `npx skills add kostja94/marketing-skills/skills/pages/legal`
   - Create the route (e.g., `app/cookie-policy/page.tsx`) and link it from the banner and footer.
4. **State Management:** 
   - Ensure the consent state is managed globally (e.g., via React Context or a simple `localStorage` hook) so all tracking scripts can react to it.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Implement Cookie Consent & Analytics Gating**
> "Add a small, non-annoying cookie consent banner to my app. Ensure my analytics (PostHog) only starts tracking with cookies after consent is given. If rejected, use cookieless/anonymous mode. Store the user's choice in localStorage so the banner doesn't reappear on every visit."

**Prompt 2: Generate Cookie Policy Page**
> "I need a Cookie Policy page to link from my consent banner. Use the legal pages skill (`npx skills add kostja94/marketing-skills/skills/pages/legal`) to generate a GDPR-compliant cookie policy that explains what data we collect, why, and how users can manage it. Create the route for it."

**Prompt 3: Audit Current Tracking for GDPR Compliance**
> "Audit my current analytics and tracking setup. Identify any scripts that are dropping cookies or tracking users before they have explicitly consented via a banner. Provide the exact code changes needed to gate these scripts behind a consent state."