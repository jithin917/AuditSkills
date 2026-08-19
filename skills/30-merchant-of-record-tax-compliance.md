# ⚖️ Skill: Merchant of Record (MoR) & Global Tax Compliance

## 🎯 Objective
Ensure the application has a designated Merchant of Record (MoR) or automated tax compliance solution (e.g., Polar, Lemon Squeezy, Stripe Tax) to handle international VAT and sales tax collection and remittance. Prevent the developer from becoming personally liable for complex global tax filings.

## 🧠 Context & "Why It Matters"
- **The Threat:** Using a basic, plain Stripe integration makes *you* (your legal entity) the Merchant of Record. This means you are legally responsible for calculating, collecting, and remitting VAT and sales tax in *every single country or state* where you have a customer.
- **Real-world consequence:** A year of international sales through plain Stripe, followed by the realization that you owed VAT registrations in a dozen countries the whole time. This results in massive back-payments, penalties, and expensive tax advisor fees.
- **The Rule:** Picking a MoR on day one costs a slightly higher transaction fee. Unreported VAT later costs a fortune in back payments and legal trouble. Shift the burden before you scale.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** assume a basic Stripe or PayPal integration automatically handles global tax compliance and remittance for you. It does not.
2. **ALWAYS** designate a clear Merchant of Record (either your own registered entity with automated tax tools, or a third-party MoR like Polar or Lemon Squeezy) before accepting international payments.
3. **ALWAYS** display the correct legal entity name and tax information on receipts and checkout pages, as required by the chosen MoR.

## 🔍 Audit Protocol
When triggered, scan the codebase and payment configuration to verify tax compliance:

- [ ] **Payment Provider Check:** Identify the current payment provider (e.g., raw Stripe API, Stripe Checkout, Polar, Lemon Squeezy, Paddle).
- [ ] **MoR Status Verification:** 
  - If using *Polar, Lemon Squeezy, or Paddle*: Verify they are set as the MoR (they handle tax remittance by default).
  - If using *plain Stripe*: Check if "Stripe Tax" is explicitly enabled and configured with the correct product tax codes. If not, flag this as a critical risk.
- [ ] **Checkout Flow Check:** Ensure the checkout page or payment link is configured to automatically calculate and add tax based on the customer's billing address/location.
- [ ] **Receipt Compliance:** Verify that generated receipts or webhook data include the MoR's legal name and tax registration details, not just the developer's personal name.

## 🛠️ Remediation & Auto-Fix Steps
If the app is using plain Stripe without tax handling, execute the following fixes:

1. **Recommend a MoR Migration (Highly Recommended for Indie/SaaS):** 
   - Suggest migrating to a developer-friendly MoR like **Polar** or **Lemon Squeezy**. They are built on top of Stripe but handle all global VAT/sales tax remittance, tiered subscriptions, and compliance out of the box.
2. **Alternative: Enable Stripe Tax:** 
   - If the user must stay with raw Stripe, provide instructions to enable Stripe Tax in the Stripe Dashboard, register for tax in relevant jurisdictions, and update the checkout session code to include `automatic_tax: { enabled: true }`.
3. **Update Checkout Code:** 
   - Generate the updated API route or Server Action code to integrate the new MoR's checkout session or payment link.
4. **Legal Disclaimer:** 
   - Remind the user: "I am an AI, not a CPA or tax attorney. This setup provides technical guidance for common MoR solutions, but you should consult a tax professional regarding your specific business structure and obligations."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Audit Current Payment & Tax Setup**
> "Run a Merchant of Record audit on my app. I am currently using [Stripe / Polar / other]. Am I legally the Merchant of Record, and am I handling international VAT/sales tax correctly? Flag any compliance risks and recommend the safest path forward."

**Prompt 2: Migrate to a MoR (e.g., Polar or Lemon Squeezy)**
> "I want to stop being the Merchant of Record and avoid handling global VAT myself. Help me migrate my payment flow from plain Stripe to [Polar / Lemon Squeezy]. Provide the backend code to create a checkout session and the frontend code to redirect the user."

**Prompt 3: Enable Stripe Tax (If staying with Stripe)**
> "I am keeping plain Stripe but need to handle taxes. Update my Stripe Checkout session code to enable `automatic_tax: { enabled: true }`, and give me a checklist of what I need to configure in the Stripe Dashboard to make this legally compliant."