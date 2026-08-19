# Publish your Terms of Service and Privacy Policy

> **What to check**
>
> Your site has a Terms of Service and a Privacy Policy, both linked in the footer. You'll need them as soon as you want a payment processor like Stripe to approve you, and EU or California visitors make them a legal requirement.

The Terms of Service needs a fulfillment policy, a refund policy, and most importantly a **limitation of liability** and a **warranty disclaimer**. Those last two protect you when something breaks.

The Privacy Policy covers what data you collect, why, and how users can get it deleted. That's the core of GDPR and CCPA compliance.

---

## How to check it

1. Do the footer links to both pages work?
2. Does signup say "By signing up you agree to..."?
3. Does the ToS contain the four parts above? Does the Privacy Policy name your actual tools (analytics, cookies, payment provider)?

---

## How to fix it

### 1. Use the skill (recommended)
Copy the AI skills I use. They build the pages tailored to your app, GDPR and CCPA compliant:

```bash
npx skills add kostja94/marketing-skills/skills/pages/legal
```

### 2. Or use the prompt
If you don't want to use skills this prompt gets you most of the way but I really recommend the skills...

```
Create a Terms of Service and Privacy Policy for my app. The ToS needs a fulfillment policy, refund policy, limitation of liability, and warranty disclaimer. The Privacy Policy must be GDPR and CCPA compliant: list what data we collect (including analytics and cookies), why, how long we keep it, and how users request deletion. Add both as public pages linked in the footer.
```

### 3. Have a lawyer review
Ideally have a lawyer review both. AI gets you a solid draft but get legal advice if you can afford it. Especially if you are handling sensitive data. Protect yourself.

---

## What bad looks like

No policies, EU users signing up, and a Stripe application stalling because the required pages aren't on your site.

---

## Why it matters

Stripe requires them before approving you. And the first "please delete my data" email will come eventually.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
