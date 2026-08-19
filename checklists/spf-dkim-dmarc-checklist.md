# Configure SPF, DKIM and DMARC

> **What to check**
>
> The three DNS records that prove your emails really come from you: SPF, DKIM, DMARC. Without them, spam filters distrust you by default, and anyone on the internet can send fake emails that look like they're from your domain.

---

## How to check it

No terminal needed:

### 1. Check your email provider dashboard
If you use **Resend** (or Postmark, Loops, SendGrid): open your dashboard, go to **Domains**, and all three records should show as verified.

Resend walks you through adding them at your DNS provider — their guide is at [resend.com/docs/add-a-domain](https://resend.com/docs/add-a-domain).

### 2. Independent check
Enter your domain at [dmarcian.com/domain-checker](https://dmarcian.com/domain-checker). You want SPF, DKIM, and DMARC all green.

### 3. DMARC policy
For DMARC, `p=quarantine` is the minimum that actually protects. `p=none` is only monitoring.

---

## What bad looks like

- **Missing DMARC:** scammers can spoof `support@yourapp.com` and your users can't tell the difference.
- **Missing SPF or DKIM:** emails go straight to spam.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
