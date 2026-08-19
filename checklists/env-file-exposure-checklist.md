# Check that yourapp.com/.env shows nothing

> **What to check**
>
> Your config files aren't downloadable from the internet. AI tools generate `.env` files with all your passwords, and sometimes they end up deployed.

---

## How to check it

Open these URLs in your browser. Every single one should show an error page, never file contents:

- `yourapp.com/.env`
- `yourapp.com/.env.local`
- `yourapp.com/.env.production`
- `yourapp.com/.git/config`

---

## How to fix it

### 1. If any file showed contents: rotate every key in it today.

Bots scan new domains for these paths within hours, so treat them as stolen.

### 2. Then stop it from happening again:

```
My .env file is reachable on my live domain. Make sure .env* files are excluded from the build and public output, blocked in my host config, and listed in .gitignore.
```

---

## What bad looks like

The browser shows a file with `DATABASE_URL=...` and `OPENAI_API_KEY=...` in it. That's every secret you have, public.

Bots scan every new domain for exactly these paths, so it gets found within hours.

---

## Why it matters

The check takes 60 seconds. Skipping it can cost you every account your app touches.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
