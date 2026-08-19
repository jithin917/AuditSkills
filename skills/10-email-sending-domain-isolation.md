# 📧 Skill: Email Sending Domain Isolation (Subdomains)

## 🎯 Objective
Isolate automated and transactional email sending to a dedicated subdomain (e.g., `mail.yourapp.com` or `app.yourapp.com`) to protect the primary domain's email reputation, ensuring personal and marketing communications remain unaffected by automated email spam flags.

## 🧠 Context & "Why It Matters"
- **The Threat:** Email reputation is tied directly to the sending domain. If your automated app emails (password resets, receipts, notifications) trigger spam filters, the *entire* domain's reputation is penalized.
- **Real-world consequence:** If app emails, marketing blasts, and your personal `you@yourapp.com` replies all share the root domain, a single wave of spam complaints poisons all of them at once. A burned domain reputation takes months to repair.
- **The Rule:** Set this up *before* you have volume. It is an isolation layer, not a loophole. (Note: Google still connects the dots, so this does not permit cold email outreach or spamming).

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** configure your primary root domain (e.g., `yourapp.com`) as the default sender for automated, high-volume transactional emails.
2. **ALWAYS** use a dedicated subdomain for transactional emails (e.g., `mail.yourapp.com`, `notifications.yourapp.com`).
3. **ALWAYS** use a *separate* subdomain for marketing/newsletter blasts (e.g., `news.yourapp.com`) to further isolate reputation risks.
4. **NEVER** use these subdomains for cold email outreach or unsolicited bulk emailing. 

## 🔍 Audit Protocol
When triggered, scan the codebase and email provider configuration to verify domain isolation:

- [ ] **Identify Current Sender:** Check the `EMAIL_FROM_ADDRESS` or equivalent environment variable. Flag if it uses the root domain (e.g., `noreply@yourapp.com`).
- [ ] **Verify Subdomain Setup:** Check if a dedicated subdomain (e.g., `mail.yourapp.com`) is added and verified in the transactional email provider's dashboard (e.g., Resend, SendGrid, Postmark).
- [ ] **DNS Record Check:** Ensure that the SPF, DKIM, and DMARC records (from Skill #07) are configured specifically for the *subdomain*, not just the root domain.
- [ ] **Marketing Separation:** If a newsletter or marketing email service is detected (e.g., Loops, Mailchimp), verify it is using a distinct subdomain (e.g., `news.yourapp.com`).

## 🛠️ Remediation & Auto-Fix Steps
If the root domain is being used for automated emails, execute the following fixes:

1. **Update Environment Variables:** 
   - Change the sender address in `.env` to use the subdomain: `EMAIL_FROM_ADDRESS="Your App <noreply@mail.yourapp.com>"`.
2. **Provider Configuration Steps:** 
   - Provide exact instructions for the user's email provider (e.g., Resend): 
     1. Go to Domains.
     2. Add `mail.yourapp.com` as a new sending domain.
     3. Copy the provided SPF, DKIM, and DMARC TXT records.
3. **DNS Update Guidance:** 
   - Instruct the user to add these new records to their DNS provider (Cloudflare, Namecheap, etc.) specifically for the `mail` subdomain.
4. **Codebase Search:** 
   - Grep the codebase for any hardcoded `@yourapp.com` email addresses in email templates or backend logic and replace them with the new subdomain variable.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Email Domain Audit**
> "Run the Email Domain Isolation audit. Check my environment variables and email sending logic. Am I currently sending automated transactional emails from my root domain? If so, flag it and provide the steps to migrate to a 'mail.yourapp.com' subdomain."

**Prompt 2: Resend Subdomain Setup**
> "I want to set up a dedicated subdomain for my transactional emails using Resend. Give me the exact step-by-step instructions on what to click in the Resend dashboard, and list the DNS records I will need to add to Cloudflare for 'mail.yourapp.com'."

**Prompt 3: Update Hardcoded Sender Addresses**
> "Search my entire codebase for any hardcoded email addresses ending in '@yourapp.com' used in email templates or backend mailers. Replace them with a new environment variable: process.env.EMAIL_FROM_ADDRESS, and add that variable to my .env.example file as 'Your App <noreply@mail.yourapp.com>'."