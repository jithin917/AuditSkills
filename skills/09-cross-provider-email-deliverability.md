# 📧 Skill: Cross-Provider Email Deliverability & Link Verification

## 🎯 Objective
Ensure that critical transactional emails (signup confirmations, password resets, receipts) reliably land in the primary inbox (not the spam folder) across major email providers, specifically Gmail and Outlook/Hotmail, and that all embedded links are functional and point to the correct domain.

## 🧠 Context & "Why It Matters"
- **The Threat:** Email providers use vastly different filtering algorithms. An email that perfectly lands in a Gmail inbox might be instantly quarantined by Outlook.
- **Real-world consequence:** You test with Gmail, see the email, and assume it works. Meanwhile, every Outlook/Hotmail user thinks your app is broken because "the confirmation never came," leading to silent user churn on launch day.
- **The Rule:** Password resets and signup confirmations are the most important emails your app sends. If they don't arrive, your app functionally does not work, no matter how good the code is.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** assume inbox placement is successful based on testing with only one email provider (e.g., just Gmail).
2. **NEVER** use raw, unauthenticated SMTP servers (like basic Gmail SMTP or default Node.js `nodemailer` without a dedicated provider) for production transactional emails. Use reputable services (Resend, Postmark, SendGrid).
3. **ALWAYS** ensure the links inside the email templates dynamically use the correct, canonical production domain (not `localhost` or a staging URL).

## 🔍 Audit Protocol
When triggered, the AI should guide the user through a manual verification process and audit the codebase for common deliverability pitfalls:

- [ ] **Provider Diversity Check:** Prompt the user to confirm they have manually tested signup and password reset flows using *both* a `@gmail.com` address and an `@outlook.com` or `@hotmail.com` address.
- [ ] **Link Domain Verification:** Scan email template files (e.g., React Email, MJML, HTML strings) to ensure base URLs are pulled from production environment variables (e.g., `process.env.NEXT_PUBLIC_APP_URL`), not hardcoded to `http://localhost:3000`.
- [ ] **Prerequisite Check:** Verify that the foundational deliverability skills are marked as complete:
  - SPF, DKIM, and DMARC are configured (Skill #07).
  - Emails are being sent from a dedicated subdomain (Skill #10).
- [ ] **Spam Score Check:** Recommend running a sample email through `mail-tester.com` to achieve a score of 9/10 or higher.

## 🛠️ Remediation & Auto-Fix Steps
If deliverability issues or template errors are found, execute the following fixes:

1. **Fix Hardcoded Links:** Replace any `localhost` or staging URLs in email templates with dynamic environment variables pointing to the production domain.
2. **Provider Migration:** If the user is using raw SMTP, provide a code snippet to migrate to a modern API-based provider like Resend or Postmark.
3. **Generate Test Plan:** Output a clear, step-by-step checklist for the user to execute manually (since AI cannot natively check a real Gmail/Outlook inbox without browser automation):
   - "Step 1: Go to incognito mode. Sign up with test@gmail.com. Check Inbox AND Spam."
   - "Step 2: Repeat with test@outlook.com. Check Inbox AND Spam."
   - "Step 3: Click the 'Reset Password' or 'Confirm Email' link in both. Verify it routes to `https://yourapp.com/...`"
4. **Mail-Tester Integration:** Provide instructions on how to send an email to the unique `mail-tester.com` address to get a detailed breakdown of spam triggers.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Email Template & Link Audit**
> "Run the Email Deliverability Audit. Scan my email templates (signup, password reset, receipts) to ensure no links are hardcoded to 'localhost' or staging URLs. Verify they use the correct production environment variable. Then, give me a step-by-step manual testing checklist for Gmail and Outlook."

**Prompt 2: Fix Raw SMTP / Upgrade Provider**
> "I am currently sending emails using raw SMTP / nodemailer. Refactor this to use a reputable transactional email API like Resend or Postmark. Provide the updated backend code and the necessary environment variables."

**Prompt 3: Mail-Tester Preparation**
> "I want to ensure my emails don't go to spam. Give me instructions on how to use mail-tester.com to score my current email setup, and list the top 3 technical reasons (besides content) why my emails might be failing that check."