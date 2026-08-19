# Add a cookie consent banner

> **What to check**
>
> If your analytics uses cookies, you ask for consent first, especially with EU visitors. Some tools track without consent by default, which puts the problem on your side.

---

## How to check it

### 1. Check if tracking starts before consent
Open your site in **incognito**. Does a consent banner appear before tracking starts?

### 2. PostHog users
Set the cookieless mode to `on_rejection`, so tracking respects the banner. Then let AI wire it up:

```
Add a small, non-annoying cookie consent banner to my app. Analytics only starts after consent; on reject, use cookieless/anonymous mode. Store the choice so the banner doesn't reappear on every visit.
```

### 3. Component option
A free **shadcn** component: [github.com/r2hu1/shadcn-cookie-consent](https://github.com/r2hu1/shadcn-cookie-consent)

### 4. Cookie policy page
A banner on its own isn't enough. You also need a **cookie policy page** explaining what each cookie does. That skill comes in the same folder as the terms and privacy ones:

```bash
npx skills add kostja94/marketing-skills/skills/pages/legal
```

---

## What bad looks like

Full cookie tracking from the first pageview, no banner, EU traffic incoming. That's a legal letter waiting to happen.

---

## Why it matters

Setting this up takes 20 minutes max… It's worth your time.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
