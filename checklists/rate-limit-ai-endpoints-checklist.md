# Rate-limit your expensive (AI) endpoints

> **What to check**
>
> If your app has AI features, someone can script 10,000 requests against them overnight, and you pay the OpenAI or Anthropic bill.

---

## How to check it

Paste this into your AI tool:

```
Does my app have rate limiting on expensive endpoints, especially anything calling OpenAI/Anthropic/LLM APIs, sending emails, or hitting paid third-party APIs? If not, add sensible rate limits (per user and per IP) so a single visitor can't run up my costs.
```

---

## What bad looks like

An open `/api/chat` endpoint with no limit. This is very dangerous since an attacker can really drive up your bill and you will have to pay for it.

---

## Why it matters

One prompt and ten minutes of work protect your whole API budget.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
