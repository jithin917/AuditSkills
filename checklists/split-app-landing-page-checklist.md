# Split your app and landing page onto separate domains

> **What to check**
>
> Your app lives on `app.yourapp.com`, your landing page on `yourapp.com`. Two separate deployments, connected by a login button.

**Why split it:** you'll change your homepage way more often than your app. Keep them separate and a headline tweak doesn't mean redeploying your whole codebase. Your landing page also stays fast because it doesn't carry your app's JS bundle — plus it's easier to control what Google crawls.

---

## How to check it

1. Open your landing page and your app. Same domain? Then they're probably one deployment.
2. To split: go to your DNS provider, add a new **CNAME** record, type `app` in the name field, and point it to where your app is hosted.
3. Public pages (home, pricing, blog, legal) stay on the main domain. Everything behind login goes on the subdomain.

---

## What bad looks like

Landing page and app in one deployment. You want to fix a typo on the homepage, so you redeploy the app. And when you split them later, every bookmark, shared link, and OAuth redirect URL breaks.

> I mainly like to split them because I can just hire a designer for the marketing pages. Designers use no-code tools like **Framer**. So the landing page can live there on the main domain and the app can live on the subdomain.

---

## Why it matters

Before launch this is one DNS record. After launch it's a migration.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
