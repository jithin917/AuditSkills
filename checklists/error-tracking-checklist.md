# Turn on error tracking

> **What to check**
>
> When your app breaks for a user, you find out, not just the user. Most users never report a bug. They just leave.

---

## How to check it

### 1. Add Sentry
**Sentry** (free tier is plenty), or let your AI tool do it:

```
Add Sentry error tracking to my app: frontend and backend/API errors, with source maps uploaded so I see readable stack traces. Use environment variables for the DSN.
```

### 2. Test it
Throw a test error and confirm it shows up in your Sentry dashboard.

---

## What bad looks like

Your payment flow breaks for Safari users on day 2. You find out on day 9, from an angry email. One week of lost signups :')

---

## Why it matters

On launch day, things break under real traffic that never broke in testing (trust me, it will). Error tracking means you can fix them quick and don't have to rely on user feedback.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
