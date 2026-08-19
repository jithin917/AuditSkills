# Set up your transactional emails

> **What to check**
>
> Before you test whether emails arrive, check that they exist. Your app needs at least: a signup confirmation or welcome email, a password reset email, and a receipt if you charge money. Builders forget the password reset one the most, and it's the one that locks users out.

---

## How to check it

1. **Sign up.** Did a welcome or confirmation email send?
2. **Log out and click "Forgot password".** Did a reset email send? Does the link work?
3. **Buy your product.** Did a receipt arrive? Stripe and Polar can send these for you, but only if you switch it on.
4. **Also check your app even has a "Forgot password" link.** Auth providers like Clerk handle this for you. Hand-rolled auth often doesn't.

> **PS:** Don't build your auth from scratch if you're not technical! I'm technical and I don't, because it's a headache! Use **Clerk** or if you are selling to enterprise and need SSO → **WorkOS**.

---

## How to fix it

### 1. Receipts
In **Stripe** or **Polar**, switch on customer emails.

### 2. Email setup
Resend has an MCP server. I haven't tried it myself but you might be able to set your emails up with Claude. Worth a try → [resend.com/mcp](https://resend.com/mcp)

(I'll update this once I've tried it myself.)

---

## What bad looks like

A user forgets their password and there's no reset flow, so their only option is emailing you. Or there's a reset button that says "email sent" and nothing sends.

> Also check the [SPF, DKIM and DMARC](spf-dkim-dmarc-checklist.md) checklist item.

---

## Why it matters

Testing the happy path won't catch this. The first locked-out user two weeks after launch will.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
