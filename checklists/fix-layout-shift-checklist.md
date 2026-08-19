# Fix anything that jumps around while loading

> **What to check**
>
> While your page loads, buttons and text stay where they are. That annoying "I tried to tap the button and the page shifted" feeling has a name (layout shift). Google measures this.

---

## How to check it

### 1. Manual check
Open your site on your phone with a slow connection (turn off wifi).

Watch the page load. Does anything visibly jump, shift, or push content down?

The usual suspects: images without fixed sizes, fonts swapping late, banners appearing at the top.

### 2. AI prompt

```
Add explicit width and height to every image in my app, and reserve space for anything that loads late (banners, embeds), so the layout doesn't shift while loading.
```

### 3. Better: use the skill
This is the one check where a skill beats a prompt. Layout shift has a name (**CLS**) and a target (**under 0.1**), and this skill knows every pattern that causes it:

```bash
npx skills add addyosmani/web-quality-skills --skill core-web-vitals
```

Then say **"fix my layout shift"**.

---

## What bad looks like

The user goes to tap "Sign up", an image loads above, and they tap "Pricing" instead.

---

## Why it matters

It makes your app feel broken even when it isn't. It also hurts your Google ranking, because it's one of the **Core Web Vitals**.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
