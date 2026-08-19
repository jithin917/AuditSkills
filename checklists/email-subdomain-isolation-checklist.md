# Send automated emails from a subdomain, not your main domain

> **What to check**
>
> Automated emails (signups, billing, resets) are sent from a **subdomain** like `mail.yourapp.com`, not from your main domain.

The reason: email reputation sticks to the sending domain. If your automated emails ever get flagged as spam, only the subdomain's reputation burns. Your main domain, and your personal `you@yourapp.com`, stays clean.

> **IMPORTANT:** This does NOT mean you can just start spamming people with subdomains. Google will flag your main domain. It's just an isolation layer. Don't do cold email outreach with subdomains.

---

## How to check it

1. Look at the sender address of your app's emails. `something@mail.yourapp.com` is right. `something@yourapp.com` is risky.
2. To set it up: in **Resend**, add `mail.yourapp.com` as the sending domain and configure the records it gives you.
3. Planning a newsletter later? Give marketing email its own subdomain too (like `news.yourapp.com`), same logic.

---

## What bad looks like

App emails, marketing blasts, and your personal replies all from one domain. One spam complaint wave poisons all of it at once.

---

## Why it matters

Set it up before you have volume. A burned domain reputation takes months to repair.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
