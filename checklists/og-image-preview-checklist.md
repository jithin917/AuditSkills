# Add a preview image for your links (OG image)

> **What to check**
>
> When someone shares your app in WhatsApp, iMessage, X, or LinkedIn, it shows a proper preview image and title, like Notion, Anthropic, or Stripe links do. On launch day your link gets shared more than ever. The preview is the first thing everyone sees.

---

## How to check it

1. Send your link to yourself in **WhatsApp**. Image, title, and description showing?
2. Double-check at [opengraph.xyz](https://www.opengraph.xyz). It shows how every platform renders your link.
3. No image? Two-minute fix: add an `og.png` (1200 by 630 pixels) to your public folder and reference it in your metadata.

Let your AI tool generate the image from your logo:

```
Add an Open Graph preview image to my app: create the metadata tags (og:title, og:description, og:image, twitter:card summary_large_image) and tell me exactly where to put the og.png file. Also add a favicon if missing.
```

---

## What bad looks like

A bare grey link with no image. Or worse, a preview pointing to `localhost:3000`.

Social platforms cache previews, so a broken one can stick around after you fix it. Get it right before the first share.

---

## Why it matters

The preview image gets more attention and more clicks, and it takes less than two minutes to set up.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
