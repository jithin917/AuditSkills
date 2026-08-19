# Set up session recordings (with consent)

> **What to check**
>
> You can record exactly what users do in your app: where they got stuck, what they did after signup, what they did just before cancelling. In the first weeks after launch this is the fastest way to find the problems your numbers won't show you.

> **One rule:** only record with consent. Especially recording EU users without a cookie banner can get you in serious trouble down the line.

---

## How to check it

1. In **PostHog**, enable session recordings. The install wizard sets most of it up.
2. Put recording behind your **cookie banner** so it only starts after consent.
3. Check that sensitive inputs are **masked** (passwords, payment fields). PostHog masks inputs by default. Verify it's on.
4. Watch one of your own sessions to confirm it captures.

---

## What bad looks like

Recordings run from the first pageview, no consent, capturing everything users type. Or the opposite: launch week passes, users churn, and you have no idea what they did.

---

## Why it matters

Your funnel shows which step users drop off at. A recording shows what they did in that step. I would call it qualitative insight. Honestly it's a nice to have not a must have.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
