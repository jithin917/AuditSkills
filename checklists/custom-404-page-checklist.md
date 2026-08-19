# Add a custom 404 page

> **What to check**
>
> When someone hits a page that doesn't exist, they see something useful instead of a dead end.

---

## How to check it

1. Go to `yourapp.com/asdfasdf`
2. You should see a friendly "page not found" with a link back home
3. **Bonus for later, when you care about SEO:** the page should be a real 404, not a normal page pretending. Test at [httpstatus.io](https://httpstatus.io). Enter the URL, it should say **404**, not 200.

---

## How to fix it

```
Create a custom 404 page for my app: friendly message, a link back to the homepage, and make sure it returns a real 404 status code, not 200.
```

---

## What bad looks like

A blank white screen. A framework error message. Or a "not found" page that reports itself as perfectly fine (200) to Google.

---

## Why it matters

Every launch has broken links from typos in posts and DMs. A good 404 page keeps those visitors on your site.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
