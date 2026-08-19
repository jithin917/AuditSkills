# ⚖️ Skill: Legal Pages (Terms of Service & Privacy Policy)

## 🎯 Objective
Ensure the application has legally compliant Terms of Service (ToS) and Privacy Policy pages, properly linked in the footer and signup flows. These pages must contain all necessary clauses for payment processor approval (e.g., Stripe) and regional compliance (GDPR, CCPA).

## 🧠 Context & "Why It Matters"
- **The Threat:** Launching without legal pages or with incomplete templates. Payment processors like Stripe will reject your application if these pages are missing or lack specific clauses. Furthermore, failing to comply with GDPR (EU) or CCPA (California) can result in severe fines.
- **Real-world consequence:** Your Stripe application stalls for weeks because the required pages aren't on your site. Or, an EU user emails you demanding their data be deleted, and you have no legal framework or process to handle it.
- **The Rule:** The ToS protects *you* (limitation of liability, warranty disclaimer). The Privacy Policy protects the *user* and keeps you compliant (data collection, deletion rights). Get them in place before you accept money or personal data.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch or apply for a payment processor (Stripe, PayPal) without both a Terms of Service and a Privacy Policy published and publicly accessible.
2. **NEVER** omit the **"Limitation of Liability"** and **"Warranty Disclaimer"** (usually in all-caps) from the Terms of Service. These are your primary legal shields when something breaks.
3. **NEVER** use a generic Privacy Policy that doesn't explicitly name the *actual* third-party tools you are using (e.g., specific analytics, cookie trackers, payment providers).
4. **ALWAYS** include a clear, actionable mechanism in the Privacy Policy for users to request the deletion of their data.

## 🔍 Audit Protocol
When triggered, scan the UI, routing, and page content to verify legal compliance:

- [ ] **Footer Links:** Verify that both `/terms` (or `/tos`) and `/privacy` exist and are linked in the site's footer.
- [ ] **Signup Flow Check:** Inspect the signup/registration forms. Ensure there is text stating "By signing up, you agree to our Terms of Service and Privacy Policy" with clickable links.
- [ ] **ToS Content Verification:** Read the generated ToS to ensure it contains:
  1. Fulfillment policy (how services/products are delivered).
  2. Refund/Cancellation policy.
  3. Limitation of liability.
  4. Warranty disclaimer.
- [ ] **Privacy Policy Content Verification:** Read the Privacy Policy to ensure it explicitly lists:
  1. What data is collected.
  2. Why it is collected.
  3. Specific third-party processors (e.g., Stripe for payments, PostHog for analytics).
  4. How long data is kept.
  5. How users can request data deletion (GDPR/CCPA requirement).

## 🛠️ Remediation & Auto-Fix Steps
If legal pages are missing, incomplete, or unlinked, execute the following fixes:

1. **Generate the Content:** 
   - Use the specialized AI skill if available: `npx skills add kostja94/marketing-skills/skills/pages/legal`
   - Alternatively, use the comprehensive prompt (see below) to generate tailored, compliant drafts based on your app's actual features.
2. **Create Routes/Pages:** 
   - Create the public pages (e.g., `app/terms/page.tsx` and `app/privacy/page.tsx`) and render the generated markdown/content.
3. **Update Footer & Signup UI:** 
   - Add the links to your global Footer component.
   - Add the "By signing up..." consent text and links to your authentication/signup forms.
4. **Legal Review Warning:** 
   - Always append a disclaimer to the generated text: "This is an AI-generated draft. It is highly recommended to have a qualified lawyer review these documents, especially if you are handling sensitive user data or operating in multiple jurisdictions."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Legal Pages Generation**
> "Create a Terms of Service and Privacy Policy for my app. The ToS needs a fulfillment policy, refund policy, limitation of liability, and warranty disclaimer. The Privacy Policy must be GDPR and CCPA compliant: list what data we collect (including analytics and cookies), why, how long we keep it, and how users request deletion. Add both as public pages linked in the footer."

**Prompt 2: Automated Setup via Legal Skill**
> "I want to generate my legal pages using the specialized skill. I am running: `npx skills add kostja94/marketing-skills/skills/pages/legal`. Generate the Terms of Service and Privacy Policy tailored to my app, and create the routes for them."

**Prompt 3: Fix Signup Consent & Footer Links**
> "I have my Terms and Privacy pages, but they aren't linked properly. Add links to both pages in my global footer component. Also, update my signup form to include a checkbox or text saying 'By signing up you agree to our Terms and Privacy Policy' with clickable links to those pages."