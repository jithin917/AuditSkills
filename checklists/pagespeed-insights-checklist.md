# Run PageSpeed Insights

> **What to check**
>
> Your app loads fast on a normal phone with normal internet, not just on your laptop on wifi.

---

## How to check it

### 1. Run the test
Go to [pagespeed.web.dev](https://pagespeed.web.dev) (free, by Google).

Enter your URL and look at the **Mobile** score:

| Score | Action |
|-------|--------|
| Under 50 | Fix before launch |
| 50 to 89 | Fix your biggest item, launch anyway |
| 90+ | Move on |

### 2. Get a prioritized fix list
Copy the report and paste it into Claude or whatever you're using:

```
Here's my PageSpeed Insights report. Give me a prioritized fix list: biggest speed win first, with the exact code change for each.
```

### 3. Better: install the skill
It's built by **Addy Osmani**, who leads Chrome at Google, from 150+ Lighthouse audits:

```bash
npx skills add addyosmani/web-quality-skills
```

Then just say **"speed up my site"**.

The difference is it gives your AI **real budgets** to hit instead of guessing:
- Under **1.5MB** per page
- Under **300KB** of JavaScript
- Under **500KB** of images above the fold

Then it tells you which specific import blew the budget.

---

## What bad looks like

A mobile score of **34** because of one **4MB hero image**. It's almost always the images or videos (see the next check).

---

## Why it matters

A page that takes 3+ seconds loses half its visitors before they see your headline. On launch day that would be very unfortunate to say the least.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
