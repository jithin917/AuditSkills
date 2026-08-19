# Remove localhost and staging references from your live site

> **What to check**
>
> No references to `localhost`, `127.0.0.1`, `.vercel.app` preview URLs, or staging domains anywhere in your live site: links, preview images, sitemap, metadata.

---

## How to check it

### 1. Manual check
Right-click your homepage, **View source**, press **Ctrl/Cmd + F** and search for: `localhost`, `vercel.app`, `staging`

### 2. Check your sitemap
Open `yourapp.com/sitemap.xml` for the same hardcoded references.

### 3. AI prompt

```
Search my codebase and built output for hardcoded URLs pointing to localhost, 127.0.0.1, preview/staging domains, or my old dev domain. Replace them with the production domain (use an environment variable for the base URL).
```

---

## What bad looks like

Your preview image loads from `localhost:3000`. It works on your machine and is broken for everyone else.

Or a canonical tag pointing to a staging URL, which tells Google to index the wrong site.

---

## Why it matters

Everything looks fine when you test locally. That's exactly why these survive until launch day.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
