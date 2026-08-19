# 🛡️ Skill: Prevent Frontend Secret Key Exposure

## 🎯 Objective
Ensure that sensitive API keys, secrets, and tokens (e.g., OpenAI, Anthropic, Stripe secret keys, AWS credentials) are strictly kept on the server-side and never bundled into the client-side code. Prevent unauthorized usage, financial loss, and data breaches.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI coding tools often default to placing API keys in public-facing environment variables (like `NEXT_PUBLIC_`) to make things "work" quickly in the browser. 
- **Real-world consequence:** 1 in 4 AI-built apps on platforms like Vercel have leaked server secrets this way. An exposed OpenAI key means strangers drain your balance. An exposed Stripe secret key means strangers can manipulate your payments.
- **The Rule:** Bots and crawlers scan public repositories and live bundles for `sk-` and `sk_live_` patterns within minutes. Treat any exposed secret as instantly compromised.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** prefix sensitive keys (passwords, tokens, `sk-`, `sk_live_`) with `NEXT_PUBLIC_`, `VITE_`, `PUBLIC_`, or `REACT_APP_`.
2. **NEVER** call third-party APIs that require secret keys directly from the browser/client. Always route these calls through a secure backend API route or server action.
3. **ALWAYS** distinguish between safe public keys (e.g., Stripe `pk_live_`, Supabase `anon` key) and dangerous secret keys (e.g., Stripe `sk_live_`, OpenAI `sk-proj-...`).

## 🔍 Audit Protocol
When triggered, scan the codebase and environment files to identify leaked secrets:

- [ ] **Search for Dangerous Prefixes:** Find all environment variables starting with `NEXT_PUBLIC_`, `VITE_`, `PUBLIC_`, or `REACT_APP_`.
- [ ] **Inspect Values:** Check if any of these prefixed variables contain strings matching secret patterns (e.g., `sk-`, `sk_live_`, `password`, `token`, `secret`).
- [ ] **Search for Raw Secrets:** Grep the entire codebase for `sk-` or `sk_live_` to ensure no hardcoded secrets exist in the frontend bundle.
- [ ] **Verify API Call Origins:** Identify any frontend components or client-side utilities making direct HTTP requests to services that require secret keys (e.g., OpenAI API, AWS SDK).

## 🛠️ Remediation & Auto-Fix Steps
If exposed secrets or client-side API calls are found, execute the following fixes:

1. **Immediate Mitigation (If Exposed):** 
   - Alert the user: "CRITICAL: A secret key is exposed in the frontend. You must rotate this key immediately in your provider's dashboard (e.g., OpenAI, Stripe). Consider it stolen."
2. **Sanitize Environment Variables:** 
   - Rename the variable to remove the public prefix (e.g., change `NEXT_PUBLIC_OPENAI_KEY` to `OPENAI_API_KEY`).
3. **Create Backend Proxy:** 
   - Generate a secure server-side API route (e.g., `/api/chat`, `/api/stripe`) that reads the secret key from the server environment.
   - Update the frontend code to call this new internal API route instead of the third-party service directly.
4. **Clean Up:** 
   - Remove any hardcoded secrets from the codebase and add them to `.env.local` (ensuring `.env*` is in `.gitignore`).

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Secret Audit**
> "Search my codebase for API keys or secrets that end up in the frontend/client bundle. Especially: check any env variable starting with NEXT_PUBLIC_, VITE_, PUBLIC_, or REACT_APP_ that contains a key, secret, token, or password. Also search for 'sk-' or 'sk_live_'. List everything you find and flag if server secrets are incorrectly prefixed."

**Prompt 2: Auto-Fix Frontend Secrets**
> "Move every secret key out of my frontend. Put them in server-side environment variables WITHOUT NEXT_PUBLIC_, VITE_, or PUBLIC_ prefixes. Then, create backend API routes to handle the calls that need these secrets, and update my frontend to call these new backend endpoints instead of the third-party API directly."

**Prompt 3: Claude Code Shortcut**
> "/security-review" *(Note: If using Claude Code, this built-in command automatically audits for leaked secrets, injection risks, and client-only auth).*