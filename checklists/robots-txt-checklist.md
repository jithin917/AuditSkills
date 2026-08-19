# Add a robots.txt file

> **What to check**
>
> A `robots.txt` file in your root folder telling crawlers what to crawl.

---

## How to check it

1. Open `yourapp.com/robots.txt`
2. Rule of thumb: allow everything, except pages that shouldn't show up on Google. Authenticated pages don't get indexed anyway. (Make sure it points to your sitemap.)
3. Prompt:

```
Create a robots.txt for my app: allow all crawlers by default, disallow admin/private routes if they're not protected by authentication anyway, and reference my sitemap.xml.
```

### Optional: llms.txt
A short summary file of your most important pages so AI tools like ChatGPT and Claude understand your site without parsing all the HTML. It's still very new, so it doesn't guarantee anything. But it takes two minutes with AI, so why not.

---

## What bad looks like

No robots.txt at all. Or the opposite: `Disallow: /` blocking everything (see the Google indexing check).

---

## Why it matters

It tells the good bots where to go, and it's the first file Google reads on your site.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
