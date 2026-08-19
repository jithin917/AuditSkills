# Make sure your emails land in the inbox, not spam

> **What to check**
>
> The emails your app sends (signup confirmation, password reset, receipts) land in the inbox, not in spam. On launch day, a signup email in spam is a user you lose without noticing.

---

## How to check it

1. Sign up for your own app with a **Gmail** address. Did the email arrive? Inbox or spam?
2. Repeat with an **Outlook/Hotmail** address. They filter very differently.
3. Click the links inside the email. Do they work? Right domain?

---

## How to fix it

Spam placement is almost never about your email text. Fix the next two checks first (SPF/DKIM/DMARC and the sending subdomain), send through a service like **Resend** instead of raw SMTP, then confirm with the mail-tester check at the end of this section.

---

## What bad looks like

**Gmail:** inbox. **Outlook:** spam folder.

You'd never notice, but every Outlook user thinks your app is broken because "the confirmation never came."

---

## Why it matters

Password resets and signup confirmations are the most important emails your app will ever send. If they don't arrive, your app doesn't work, no matter how good the code is.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
