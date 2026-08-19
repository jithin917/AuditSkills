# 💳 Skill: Live Payment Flow & Webhook Verification

## 🎯 Objective
Guarantee that the application's payment flow works flawlessly in **live mode** with real money. Verify that webhooks are correctly configured, securely validated, returning `200 OK`, and that the local database accurately synchronizes with the payment provider's state (preventing the "split-brain" problem).

## 🧠 Context & "Why It Matters"
- **The Threat:** Test mode and live mode are two entirely separate configurations (different API keys, different webhook endpoints, different product prices). Developers often test extensively in test mode but never validate the live setup.
- **Real-world consequence:** Your first real customer pays, Stripe takes the money, but your app never hears about it because the live webhook was never configured or is failing. The customer pays but gets no access, resulting in an angry email, a chargeback, and lost trust.
- **The Rule:** You've run your checkout in test mode a hundred times; run it in live mode at least *once* before a real customer does. 

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** assume that a working test mode checkout guarantees a working live mode checkout. They are separate environments.
2. **NEVER** process a webhook without verifying the Stripe (or provider) signature. Unverified webhooks are a massive security vulnerability.
3. **ALWAYS** ensure the webhook endpoint returns a `200 OK` status *before* or *immediately after* processing the event. Returning a 500 error causes Stripe to retry, potentially creating duplicate records or "split-brain" state mismatches.
4. **ALWAYS** handle the full lifecycle: successful payments, failed payments, subscription cancellations, and refunds. 

## 🔍 Audit Protocol
When triggered, scan the codebase and provider dashboard configuration to verify live payment readiness:

- [ ] **Environment Variable Check:** Verify that `STRIPE_SECRET_KEY` (live) and `STRIPE_WEBHOOK_SECRET` (live) are correctly set in the production environment, distinct from test keys.
- [ ] **Webhook Endpoint Configuration:** Confirm the live webhook endpoint URL is registered in the Stripe Dashboard (Developers → Webhooks) and is listening to the correct events (e.g., `checkout.session.completed`, `customer.subscription.updated`, `invoice.payment_failed`).
- [ ] **Signature Verification:** Inspect the webhook handler code to ensure it uses the official Stripe library to construct the event and verify the signature using the live `STRIPE_WEBHOOK_SECRET`.
- [ ] **Idempotency & State Sync:** Check that the webhook handler is idempotent (can safely process the same event multiple times without duplicating database records) to prevent "split-brain" desynchronization.
- [ ] **Reverse Flow Check:** Verify that cancellation and refund webhooks are handled to revoke user access or update subscription status in the database.

## 🛠️ Remediation & Auto-Fix Steps
If the live payment setup is incomplete or fragile, execute the following fixes:

1. **Implement Robust Webhook Handler:** 
   - Generate a secure webhook route that verifies signatures, handles idempotency, and gracefully catches errors.
   - *Reference:* Strongly recommend following the best practices in the [t3dotgg/stripe-recommendations](https://github.com/t3dotgg/stripe-recommendations) guide to avoid split-brain architecture.
2. **Live Mode Test Checklist:** 
   - Provide the user with a step-by-step manual testing guide:
     1. Switch Stripe Dashboard to "Live Mode".
     2. Use a real credit card to purchase your own product.
     3. Verify the payment succeeds and the app grants access/sends a receipt.
     4. Check Stripe Dashboard → Developers → Webhooks to confirm the event was `Delivered` with a `200 OK` response.
     5. Issue a refund or cancel the subscription in the Stripe Dashboard.
     6. Verify the app correctly revokes access or updates the user's status.
3. **Fix Webhook Failures:** 
   - If webhooks are failing, add detailed logging to the webhook handler to capture the exact error, and ensure the endpoint responds with `200 OK` as quickly as possible (consider offloading heavy database work to a background queue if necessary).

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Live Payment & Webhook Audit**
> "Run a live payment audit. Check my environment variables, webhook endpoint code, and Stripe dashboard setup. Verify that live mode keys are used, webhook signatures are validated, and the handler is idempotent to prevent split-brain database states."

**Prompt 2: Fix Split-Brain Webhook Sync**
> "My Stripe webhooks are causing database sync issues (split-brain). Refactor my webhook handler to follow best practices: verify the signature, ensure idempotency (prevent duplicate processing), and return a 200 OK immediately. Reference the t3dotgg stripe recommendations."

**Prompt 3: Live Mode Testing Checklist**
> "I am ready to test my payment flow in live mode. Give me a step-by-step checklist of exactly what to do in the Stripe Dashboard and my app to verify that a real card payment succeeds, the webhook delivers with a 200 OK, and a subsequent refund correctly updates my database."