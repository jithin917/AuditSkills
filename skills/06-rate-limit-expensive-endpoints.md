# 🛡️ Skill: Rate-Limit Expensive & High-Cost Endpoints

## 🎯 Objective
Protect the application's financial budget and infrastructure by enforcing strict, sensible rate limits on computationally or financially expensive API endpoints. Prevent cost-spike attacks on AI, email, and paid third-party services.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI tools frequently generate fully functional API routes (like `/api/chat`) but omit abuse prevention. Attackers, competitors, or even well-meaning users can script thousands of requests overnight.
- **Real-world consequence:** An unprotected LLM endpoint or transactional email route can result in massive, unexpected bills from OpenAI, Anthropic, SendGrid, or AWS. You are legally and financially responsible for the usage.
- **The Rule:** One prompt and ten minutes of work to implement rate limiting protects your entire API budget.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** deploy an endpoint that calls an LLM (OpenAI, Anthropic, Cohere), generates images, or sends emails/SMS without rate limiting.
2. **ALWAYS** implement dual-layer rate limiting: limit by **IP address** for unauthenticated users, and limit by **User ID** for authenticated users.
3. **ALWAYS** return a standard `429 Too Many Requests` HTTP status code with a `Retry-After` header when a limit is breached. Never silently drop the request or return a `500 Server Error`.

## 🔍 Audit Protocol
When triggered, scan the codebase to identify and secure expensive operations:

- [ ] **Identify Expensive Routes:** Find all API routes, server actions, or edge functions that:
  - Call OpenAI, Anthropic, Replicate, or other LLM/AI APIs.
  - Trigger transactional emails (Resend, SendGrid, Postmark) or SMS (Twilio).
  - Interact with paid third-party data enrichment or scraping APIs.
- [ ] **Check for Rate Limiting Middleware:** Inspect these routes for the presence of rate-limiting logic (e.g., `@upstash/ratelimit`, Redis-based limits, Vercel KV, or Cloudflare WAF rules).
- [ ] **Verify Scope:** Ensure the limits are applied *before* the expensive third-party API call is executed (fail fast).
- [ ] **Verify Granularity:** Check if the limits distinguish between anonymous IP limits (stricter) and authenticated user limits (slightly more generous, but still capped).

## 🛠️ Remediation & Auto-Fix Steps
If expensive endpoints lack rate limiting, execute the following fixes:

1. **Select a Rate Limiting Provider:** 
   - *For Vercel/Next.js:* Use `@upstash/ratelimit` and `@upstash/redis`.
   - *For Express/Node:* Use `express-rate-limit` backed by Redis.
   - *For Cloudflare:* Configure Cloudflare WAF Rate Limiting rules at the edge.
2. **Apply Middleware:** Wrap the vulnerable endpoints with the rate limiter.
3. **Set Sensible Defaults:** 
   - *AI/LLM generation:* Max 3-5 requests per minute per user.
   - *Email/SMS sending:* Max 2-3 requests per hour per user.
4. **Handle Rejections:** Ensure the endpoint catches the `RatelimitUpstashError` (or equivalent) and gracefully returns a `429` status with a user-friendly message like "You are generating too fast, please wait a moment."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Endpoint Audit**
> "Run the Expensive Endpoint Audit. Scan my API routes and server actions for any calls to OpenAI, Anthropic, LLMs, email providers, or paid third-party APIs. Check if these specific endpoints have rate limiting applied per user and per IP. Flag any open endpoints that could run up my bill."

**Prompt 2: Auto-Fix (Next.js / Vercel / Upstash)**
> "I need to protect my AI and email endpoints from cost-spike attacks. Implement rate limiting using `@upstash/ratelimit` and `@upstash/redis`. Apply a strict limit (e.g., 5 requests per minute) to my `/api/chat` and `/api/send` routes. Ensure it checks both IP for anonymous users and User ID for logged-in users, and returns a 429 status code when hit."

**Prompt 3: Express / Node.js Auto-Fix**
> "Add rate limiting to my Express.js server for my expensive routes. Use `express-rate-limit` backed by Redis. Apply strict limits to any route that hits an LLM or sends an email. Ensure the limits prevent a single visitor or script from running up my costs."