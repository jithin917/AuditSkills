# Test your payment flow with real money

> **What to check**
>
> Your payment flow works with real money. Test mode and live mode are two separate configurations: different API keys, different webhook endpoints, different prices.

---

## How to check it

### 1. Buy your own product
Switch to **live mode** and buy your own product with a real card. You can refund yourself after.

### 2. Verify the full flow
Did the payment go through, and did your app react?
- Subscription active?
- Access unlocked?
- Receipt sent?

### 3. Check webhook logs
Stripe: **Developers → Webhooks**. You want **delivered** and `200 OK`.

If the webhook fails, your customer pays and gets nothing.

### 4. Test cancellation/refund
Cancel or refund, and check your app picks that up too.

---

## How to set up Stripe right

If your webhooks keep breaking, the root problem is most likely what is sometimes referred to as **"the split-brain"**: the payment state lives in Stripe, and your database tries to stay in sync by listening to webhook events.

There is a great guide on how to best implement Stripe. Definitely have a read!

> [github.com/t3dotgg/stripe-recommendations](https://github.com/t3dotgg/stripe-recommendations)

---

## What bad looks like

Your first customer pays, Stripe takes the money, and your app never hears about it because you never configured the live webhook. You find out from an angry email.

---

## Why it matters

You've run your checkout in test mode a hundred times and in live mode zero times. Run it once before a customer does.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
