# 📧 Skill: Essential Transactional Email Flows

## 🎯 Objective
Guarantee that all critical user journey emails (welcome/signup confirmation, password reset, and payment receipts) are implemented, functional, and correctly routed before launch. Prevent user lockouts and missing purchase confirmations.

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers often focus on the "happy path" (successful login, successful purchase) and forget edge cases or lifecycle emails. 
- **Real-world consequence:** A user forgets their password, but there is no reset flow (or the email never arrives). Their only option is to manually email support, creating friction and lost trust. Alternatively, a user buys a product but gets no receipt, triggering chargebacks or support tickets.
- **The Rule:** Testing the happy path won't catch this. The first locked-out user two weeks after launch will. Do not build authentication from scratch if you can avoid it; use established providers.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch an app with user accounts without a fully functional, tested "Forgot Password" flow (UI link + backend token generation + email delivery).
2. **NEVER** rely on hand-rolled authentication for password resets unless absolutely necessary. Use established providers like Clerk (general) or WorkOS (enterprise/SSO).
3. **ALWAYS** ensure payment processors (Stripe, Polar) are explicitly configured to send customer receipts, or trigger a custom receipt email via your own backend (e.g., Resend) upon successful webhook confirmation.

## 🔍 Audit Protocol
When triggered, simulate or trace the following user journeys in the codebase and UI:

- [ ] **Signup Flow:** Verify that a welcome or email confirmation email is triggered upon successful registration.
- [ ] **Password Reset UI:** Confirm that a "Forgot password?" link exists on the login page.
- [ ] **Password Reset Backend:** Verify the backend generates a secure, time-limited reset token and triggers an email containing the reset link.
- [ ] **Payment Receipts:** Check if Stripe/Polar customer email receipts are enabled in the dashboard, OR if a webhook listener (`checkout.session.completed`) triggers a custom receipt email.
- [ ] **Email Delivery Check:** Remind the user to verify SPF/DKIM/DMARC (referencing Skill #07) to ensure these emails aren't silently going to spam.

## 🛠️ Remediation & Auto-Fix Steps
If any of these flows are missing or broken, execute the following fixes:

1. **Auth Provider Setup (Recommended):** 
   - If using hand-rolled auth, strongly recommend migrating to Clerk or WorkOS. 
   - If already using Clerk, verify the `resetPassword` component and email template are configured in the Clerk Dashboard.
2. **Stripe/Polar Receipts:** 
   - Provide instructions: "Go to Stripe Dashboard > Settings > Emails > Customer emails, and enable 'Payment receipts'."
3. **Custom Receipt Webhook (Alternative):** 
   - Generate a Next.js API route (e.g., `/api/webhooks/stripe`) that listens for `checkout.session.completed`, extracts the customer email, and uses Resend to send a formatted HTML receipt.
4. **Resend MCP Integration (Optional):** 
   - Note: If the user has the Resend MCP server configured in their AI tool, suggest using it to scaffold the email templates automatically (e.g., `https://resend.com/mcp`).

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Full Transactional Email Audit**
> "Run the Transactional Email Audit. Check my codebase and UI to ensure I have: 1) A welcome/signup confirmation email, 2) A fully functional 'Forgot password' flow (UI link + backend token + email trigger), and 3) A payment receipt email (either via Stripe/Polar settings or a custom webhook). Flag anything that is missing or incomplete."

**Prompt 2: Fix Password Reset Flow**
> "My app is missing a proper password reset flow. I am using [Clerk / NextAuth / custom auth]. Generate the necessary backend logic to create a secure reset token, the email template to send the link, and the frontend component to handle the password update. Ensure it handles edge cases like expired tokens."

**Prompt 3: Setup Stripe Receipt Webhook**
> "I want to send a custom receipt email when a user buys my product. Create a Stripe webhook handler for 'checkout.session.completed' that uses Resend to send a clean, professional HTML receipt to the customer's email address."