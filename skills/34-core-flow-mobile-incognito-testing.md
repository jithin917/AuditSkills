# 📱 Skill: Core Flow Mobile & Incognito Testing (First-Time User Experience)

## 🎯 Objective
Guarantee that the application's primary user journey (landing → sign up → core value delivery → payment) works flawlessly on a mobile device in an incognito, logged-out state. Simulate and validate the exact First-Time User Experience (FTUE) before launch.

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers test their apps logged in, on large desktop monitors, every single day. They become blind to the friction a new user faces.
- **Real-world consequence:** A signup button that is unclickable on mobile. A confirmation email that gets caught in spam. A payment form that throws an error on step 2 because of a mobile keyboard overlay. You lose the user instantly, and they never come back.
- **The Rule:** Your users get the version you never test. You must manually walk the core flow on a phone, in incognito mode, as a stranger, before anyone else does.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** assume a flow that works on a desktop browser will work identically on a mobile device or in strict incognito mode.
2. **NEVER** rely on `localStorage` or `sessionStorage` for critical auth state without a fallback, as strict mobile incognito modes (like Safari's Advanced Data Protection) may block or clear them aggressively.
3. **ALWAYS** test the *entire* path to value, not just the signup. If the app's value is "creating a project," the test isn't complete until a project is created.
4. **ALWAYS** use a real, fresh email address and a real test payment (if applicable) during this validation.

## 🔍 Audit Protocol
When triggered, the AI cannot physically hold a phone, so it must act as a strict QA director, generating a targeted checklist and scanning the codebase for known mobile/incognito pitfalls in the core flow:

- [ ] **Viewport & Mobile Layout:** Verify the core signup and onboarding components have proper mobile breakpoints and do not overflow horizontally.
- [ ] **Touch Targets:** Ensure primary CTAs (Signup, Continue, Pay) are at least 44x44px and have adequate spacing to prevent mis-taps on mobile.
- [ ] **Keyboard Interference:** Check if fixed bottom elements (like a "Continue" button) might be obscured by the mobile virtual keyboard.
- [ ] **Incognito Storage:** Verify that critical session tokens are stored in secure, `SameSite=None; Secure` cookies rather than relying solely on `localStorage`, which can be blocked in strict mobile privacy modes.
- [ ] **Email Deliverability:** Remind the user to check the spam folder of the fresh email account used during the test.

## 🛠️ Remediation & Auto-Fix Steps
If the codebase shows vulnerabilities for mobile or incognito users, execute the following fixes:

1. **Fix Mobile Overlays/Keyboards:** 
   - Add CSS to ensure fixed bottom buttons account for the mobile viewport height (`dvh`) or add padding to the bottom of forms to prevent keyboard overlap.
2. **Secure Auth Storage:** 
   - Refactor auth state to use HTTP-only, Secure cookies instead of `localStorage` to ensure it works reliably in strict mobile browser environments.
3. **Generate the Ultimate QA Checklist:** 
   - Output a highly specific, step-by-step manual testing script for the developer to execute on their physical phone.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Generate Mobile Core Flow QA Checklist**
> "I am about to launch. Generate a strict, step-by-step manual testing checklist for me to execute on my physical phone in an incognito tab. Cover the entire core flow: landing, signup with a fresh email, reaching the core value feature, and completing a test payment. Highlight specific mobile pitfalls to watch for."

**Prompt 2: Audit Core Flow for Mobile & Incognito Readiness**
> "Audit my signup, onboarding, and payment components for mobile and incognito compatibility. Check for touch target sizes, mobile keyboard overlap issues, and any reliance on localStorage that might break in strict mobile privacy modes. Provide exact CSS or code fixes."

**Prompt 3: Simulate First-Time User Friction**
> "Act as a strict QA tester. Review my core user journey from the landing page to the 'Aha!' moment. Identify any unnecessary friction, confusing copy, or potential points of failure for a completely new, non-technical user on a mobile device."