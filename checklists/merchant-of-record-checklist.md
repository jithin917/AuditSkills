# Choose your merchant of record for international sales

> **What to check**
>
> If you sell to international users, someone has to report VAT and sales tax in every country your customers live in. That someone is called the merchant of record. With the basic 2.9% Stripe integration, that's you (and this is painful!).

---

## How to check it

### 1. Are you using plain Stripe?
Then **you are the merchant of record**, and tax filings in your customers' countries are your problem.

### 2. To hand it off:

| Option | Description | Cost |
|--------|-------------|------|
| **Polar** | Built on Stripe, handles merchant of record for you, and also does things like tiered subscriptions. Cheaper and easier for indie apps. (I use them in my projects) | Lower fee |
| **Stripe Managed Payments** | Stripe's own merchant of record option | Extra **3.5%** on top of the 2.9% transaction fee :') |

---

## What bad looks like

A year of international sales through plain Stripe, then finding out you owed VAT registrations in a dozen countries the whole time.

---

## Why it matters

Picking a merchant of record on day one costs a higher fee. Unreported VAT later costs a tax advisor and back payments. (Again: It's painful.)

> Read more: [stripe.com/in/resources/more/merchant-of-record](https://stripe.com/in/resources/more/merchant-of-record)

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
