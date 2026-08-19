# Remove libraries AI installed but didn't end up using

> **What to check**
>
> Every third-party script you added "just in case" slows you down: chat widgets, extra analytics, session recorders. The chat widget nobody will use for your first 100 users can cost you half a second of load time.

---

## How to check it

Paste into your AI tool:

```
List every third-party script my app loads (chat widgets, analytics, tracking pixels, embeds). For each: what does it do, how big is it, and is it loaded on every page? Recommend which ones to remove or lazy-load.
```

---

## What bad looks like

An Intercom widget (300KB+) loaded on every page, for an app with zero users yet.

---

## Why it matters

At your stage: one analytics tool, no chat widget, nothing you can't name a reason for. Add tools when you need them. Every script you remove makes the app faster today.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
