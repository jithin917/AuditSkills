# Compress your images with Squoosh

> **What to check**
>
> Ideally no image on your site is over 1 MB. Oversized images are the #1 reason new apps feel slow.

---

## How to check it

### 1. Manual compression
Go to [squoosh.app](https://squoosh.app). It's free, made by Google, and your images never leave your browser.

Convert your big images (hero, screenshots, logos) to **WebP**.

### 2. CLI option
Claude can also do this with the CLI using `cwebp` (it's the same engine that Squoosh uses).

### 3. AI prompt

```
Find all images in my app. Convert them to WebP, resize them to the maximum size they're actually displayed at, and update the references. Use cwebp.
```

---

## What bad looks like

A **3.8MB** `hero.png` that every visitor downloads on mobile data before seeing your headline.

---

## Why it matters

Page speed is one of the biggest reasons people leave your website.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
