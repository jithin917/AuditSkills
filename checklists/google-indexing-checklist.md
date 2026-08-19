# Make sure Google can index your site

> **What to check**
>
> Your site can tell Google "don't index me" without you noticing. There's no error and no warning. You just never show up in search, and you find out weeks later.

---

## How to check it

### 1. Check if you're indexed
Google `site:yourapp.com`. If your pages show up, you're indexed. Tick the box.

If you launched in the last few days, Google may just not have visited yet, so run the next two checks.

### 2. Check robots.txt
Open `yourapp.com/robots.txt`. If you see `Disallow: /` under `User-agent: *`, everything is blocked.

### 3. Vercel users: check your deployment type
Preview deployments are noindexed by default through an invisible header, so you won't find it in your code.

Go to **Settings → Domains** and make sure your domain sits on the **Production** deployment, not a preview.

### 4. AI prompt

```
Check my site for anything that blocks search engines: robots.txt disallow rules, noindex meta tags, and X-Robots-Tag response headers. My domain is yourapp.com. Tell me exactly what to remove.
```

---

## How to fix it

1. Delete the `Disallow: /` line from `robots.txt` and remove `noindex` from your metadata. Redeploy.
2. **Vercel:** Settings → Domains, point your domain at the **Production** deployment.
3. Go to **Google Search Console**, inspect your homepage URL, and hit **"Request indexing"** so Google comes back right away.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
