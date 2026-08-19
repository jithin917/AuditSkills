# Add basic bot protection

> **What to check**
>
> Bots can't spam your signup form or scrape your app. But do so without making real users play Where's Waldo finding a bus. Or traffic lights, bikes, etc. I never get it right :')

---

## How to check it

### 1. Add Cloudflare Turnstile
For forms (signup, contact): add **Cloudflare Turnstile**. It's free, invisible for most real users, and you don't have to host with Cloudflare to use it. (No traffic lights.)

### 2. Use the skill
This skill sets it up for you:

```bash
npx skills add cloudflare/skills --skill turnstile-spin
```

### 3. Or use the prompt

```
Add Cloudflare Turnstile to my signup and contact forms, validated on the server side, so bots can't submit but real users don't see annoying puzzles.
```

> ⚠️ **One caution:** if you use Cloudflare and switch on aggressive bot blocking (like "Bot Fight Mode"), it can block the good bots too, including the crawlers behind ChatGPT and Perplexity. Then AI tools can't find or cite your app. Block the spammers, not the search engines.

---

## What bad looks like

400 fake signups overnight, your analytics ruined, your email quota burned by confirmation emails to garbage addresses.

---

## Why it matters

Bots find new domains within hours. Web traffic is not all human.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
