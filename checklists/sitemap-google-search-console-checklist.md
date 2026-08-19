# Submit your sitemap to Google Search Console

> **What to check**
>
> Google knows your pages exist. Without a sitemap, indexing a new site can take weeks. With one, you also get a free dashboard showing exactly what Google sees.

---

## How to check it

### 1. Check your sitemap exists
Open `yourapp.com/sitemap.xml`. It should list your public pages (landing, pricing, blog).

### 2. If it's missing, let Claude build one

```
Create a sitemap.xml for my app listing all public pages, and reference it from robots.txt. Only include pages that should show up on Google, no login-protected pages.
```

### 3. Submit to Google Search Console
Go to [Google Search Console](https://search.google.com/search-console), verify your domain, open the **Sitemaps** tab, and submit your sitemap URL.

---

## What bad looks like

No sitemap and no Search Console. You launch, and for three weeks Google has no idea you exist.

Also check: the sitemap contains your **real domain**, not a staging URL.

---

## Why it matters

Two reasons:
1. **Faster indexing** — Google discovers your pages immediately
2. **Search Console** shows you crawl errors and missing pages. You see exactly what Google sees.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
