# Every version of your URL should end up at the secure one

> **What to check**
>
> Every version of your URL ends up at the secure one.

---

## How to check it

Type these into your browser. All four should land on the same `https://` page:

1. `http://yourapp.com` (no s)
2. `https://yourapp.com`
3. `http://www.yourapp.com`
4. `https://www.yourapp.com`

### Bonus
Check your certificate grade at [ssllabs.com/ssltest](https://www.ssllabs.com/ssltest). You want an **A**.

If you host on **Vercel**, **Netlify**, or **Cloudflare**, the certificate is usually handled for you, but the www redirect often isn't.

---

## How to fix it

### Vercel or Netlify
Add both `yourapp.com` and `www.yourapp.com` under **Domains** and set one to redirect to the other.

### Anywhere else
Add the redirect at your DNS provider or in your host config.

---

## What bad looks like

`www.` shows an error while the bare domain works. Half the links people share will be the broken version.

---

## Why it matters

- Browser security warnings destroy trust
- Google treats `www` and non-`www` as two different sites if you don't redirect

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
