# 🎥 Skill: Session Recordings & Consent Management

## 🎯 Objective
Implement user session recording (e.g., via PostHog, Hotjar, or Microsoft Clarity) to observe qualitative user behavior, identify UX friction points, and understand exactly what users do before they convert or churn. This must be strictly gated behind user consent and feature robust sensitive data masking.

## 🧠 Context & "Why It Matters"
- **The Threat:** Quantitative data (funnels, analytics) tells you *where* users drop off, but not *why*. Without session recordings, you are guessing if a form is confusing, a button is broken, or a layout is misleading.
- **Real-world consequence:** Launch week passes, users churn, and you have zero visibility into what they actually experienced. Conversely, recording users without consent (especially in the EU) can lead to severe GDPR/privacy violations and legal trouble.
- **The Rule:** Recordings are a "nice to have" but a massive advantage. However, they must **never** start before the user explicitly opts in via a cookie banner, and **never** capture sensitive inputs like passwords or credit card numbers.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** initialize or start a session recording script before the user has given explicit consent via a cookie/privacy banner. (Crucial for GDPR/ePrivacy compliance).
2. **NEVER** record sensitive form inputs. Ensure the recording SDK is configured to mask password fields, payment/credit card fields, and any other sensitive data by default.
3. **ALWAYS** integrate the recording tool's initialization with your cookie consent manager (e.g., CookieYes, Osano, OneTrust, or a custom banner).

## 🔍 Audit Protocol
When triggered, scan the codebase to verify the session recording setup and privacy guardrails:

- [ ] **SDK Detection:** Check for the installation of a session recording provider (e.g., `posthog-js` with recordings enabled, `@hotjar/browser`, `@microsoft/clarity`).
- [ ] **Consent Gating:** Inspect the initialization code. Verify that the recording script is **not** loaded or started on initial page load. It must only be triggered after a "consent granted" event from your cookie banner.
- [ ] **Input Masking Check:** Verify the SDK configuration. Ensure `maskAllInputs: true` (or the provider's equivalent) is set, and explicitly check that password and payment fields have strict masking applied.
- [ ] **Manual Verification:** Instruct the user to open the live site in an incognito tab, accept the cookie banner, perform a few actions, and then watch their own session in the provider's dashboard to confirm it captures correctly and masks sensitive fields.

## 🛠️ Remediation & Auto-Fix Steps
If session recordings are missing, un-gated, or lack masking, execute the following fixes:

1. **Gate Behind Consent:** 
   - Refactor the analytics/recording initialization. 
   - *Example:* Move the `posthog.init()` or `hotjar.init()` call into a callback that only fires when the user clicks "Accept" on the cookie banner.
2. **Enforce Masking:** 
   - Update the SDK configuration to ensure sensitive fields are masked.
   - *PostHog Example:* Ensure `mask_all_inputs: true` is set in the config. Add `ph-no-capture` class to any specific DOM elements that should never be recorded.
3. **Provide Consent Integration Code:** 
   - Generate the boilerplate code to listen for the cookie banner's consent event and dynamically load the recording script only at that moment.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Setup PostHog Recordings with Consent**
> "Set up PostHog session recordings in my app. Crucially, do NOT load the script on initial page load. Gate the initialization behind my cookie consent banner so it only starts after the user accepts. Ensure all sensitive inputs (passwords, payments) are masked by default."

**Prompt 2: Fix Un-gated Session Recording**
> "My session recording tool (PostHog/Hotjar) is currently loading immediately on page load, violating privacy rules. Refactor the code to pause or delay the recording initialization until the user explicitly grants consent via the cookie banner. Provide the exact event listener code needed."

**Prompt 3: Verify and Enforce Input Masking**
> "Check my session recording configuration. Ensure that password fields, credit card inputs, and any other sensitive forms are strictly masked and will not be captured in the session replay. Add the appropriate CSS classes (like 'ph-no-capture') or SDK config flags to guarantee this."