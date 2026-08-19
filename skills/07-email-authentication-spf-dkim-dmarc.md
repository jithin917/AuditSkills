# 🛡️ Skill: Email Authentication (SPF, DKIM, DMARC)

## 🎯 Objective
Ensure that the application's domain has properly configured SPF, DKIM, and DMARC DNS records. This guarantees email deliverability (preventing spam folder placement) and prevents malicious actors from spoofing the domain to send fake emails.

## 🧠 Context & "Why It Matters"
- **The Threat:** Without these three DNS records, email providers (Gmail, Outlook, etc.) distrust your emails by default. Furthermore, anyone on the internet can send emails that appear to legitimately come from `@yourapp.com`.
- **Real-world consequence:** Missing SPF/DKIM means your transactional emails (password resets, receipts) go straight to spam. Missing DMARC means scammers can spoof `support@yourapp.com` to phish your users, and your users have no way to tell the difference.
- **The Rule:** `p=quarantine` is the minimum DMARC policy that actually provides protection. `p=none` is only for monitoring and does not stop spoofing.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** send production transactional or marketing emails from a domain without verified SPF and DKIM records.
2. **NEVER** leave DMARC set to `p=none` in production. It must be upgraded to `p=quarantine` (or `p=reject`) to actively block or quarantine spoofed emails.
3. **ALWAYS** use a dedicated subdomain for sending app emails (e.g., `mail.yourapp.com` or `notifications.yourapp.com`) to isolate your primary domain's reputation.

## 🔍 Audit Protocol
When triggered, verify the email authentication setup:

- [ ] **Provider Dashboard Check:** If using Resend, Postmark, Loops, or SendGrid, verify that the domain status shows "Verified" for all three records (SPF, DKIM, DMARC) in the provider's dashboard.
- [ ] **DNS Record Check:** Query the domain's DNS TXT records to confirm the presence of:
  - `v=spf1 include:... ~all` (or `-all`)
  - `v=DKIM1; k=rsa; p=...`
  - `v=DMARC1; p=quarantine; ...`
- [ ] **Independent Verification:** Recommend the user run the domain through `dmarcian.com/domain-checker` or `mail-tester.com` to ensure all three show as "green" or passing.
- [ ] **Policy Strictness:** Explicitly flag if the DMARC record is set to `p=none` and recommend upgrading to `p=quarantine`.

## 🛠️ Remediation & Auto-Fix Steps
If records are missing or misconfigured, execute the following fixes:

1. **Identify Provider:** Determine which transactional email provider is being used (e.g., Resend, SendGrid).
2. **Generate DNS Records:** Output the exact TXT records required by that specific provider.
   - *Example for Resend:* Provide the specific `v=spf1 include:spf.resend.com ~all` and the DKIM `v=DKIM1; k=rsa; p=...` values from their dashboard.
3. **Generate DMARC Record:** Provide a safe, protective DMARC record template:
   - `v=DMARC1; p=quarantine; rua=mailto:dmarc-reports@yourapp.com; pct=100`
4. **Subdomain Recommendation:** If the user is sending from the root domain, suggest moving to a subdomain (e.g., `mail.yourapp.com`) and provide the DNS records for that subdomain instead.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Email Auth Audit**
> "Run the Email Authentication Audit. Check if my domain has SPF, DKIM, and DMARC records configured correctly. Verify that my DMARC policy is at least 'p=quarantine' and not just 'p=none'. Tell me exactly which records are missing or failing."

**Prompt 2: Provider-Specific Setup (e.g., Resend)**
> "I am setting up Resend for my transactional emails. Generate the exact SPF, DKIM, and DMARC TXT records I need to add to my DNS provider (e.g., Cloudflare, Namecheap) to get my domain fully verified. Also, recommend if I should use a subdomain."

**Prompt 3: DMARC Policy Upgrade**
> "My DMARC record is currently set to 'p=none'. Generate the updated DNS TXT record to change it to 'p=quarantine' to actively protect my domain from spoofing, and include a 'rua' tag for aggregate reporting."