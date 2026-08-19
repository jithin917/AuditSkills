# 🛡️ Skill: Server-Side Authentication & Paywall Enforcement

## 🎯 Objective
Ensure that all premium features, protected routes, and sensitive data are strictly gated by server-side authentication and authorization checks. Eliminate the vulnerability of "client-side-only" protection where users can bypass UI paywalls by calling APIs directly.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI coding tools often implement paywalls or protected routes by simply hiding UI elements (e.g., `if (!isPremium) return null`) or guarding frontend routes. 
- **Real-world consequence:** An app called Enrichlead had its paywall bypassed publicly because the "is this user paying?" check only existed in the browser. Users simply bypassed the UI and called the API directly to get premium data for free.
- **The Rule:** Hiding a button does nothing. The API behind it on your BACKEND has to say no too. Frontend checks are for UX; backend checks are for security.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** rely solely on client-side logic (React state, local storage, frontend route guards) to protect data, API endpoints, or premium features.
2. **ALWAYS** enforce authentication (who is this?) and authorization (are they allowed to do this/see this?) on the server (API route, database rule, middleware, or server action) *before* returning any data or executing a mutation.
3. **TREAT** frontend checks purely as User Experience (UX) enhancements to prevent UI flickering or showing disabled states, never as a security boundary.

## 🔍 Audit Protocol
When triggered, scan the codebase to identify client-side-only protection flaws:

- [ ] **Identify Protected Assets:** List all premium features, logged-in-only pages, and sensitive data endpoints.
- [ ] **Trace the Data Flow:** For each asset, identify the underlying API route, server action, or database query that fetches the data.
- [ ] **Inspect Backend Handlers:** Check the server-side code for these handlers. 
- [ ] **Verify Server-Side Checks:** Ensure the backend explicitly checks the logged-in user's session (e.g., via Clerk, NextAuth) AND their subscription tier/role before returning the payload.
- [ ] **Flag Vulnerabilities:** Flag any API route that returns premium data or executes a premium action without verifying the user's identity and plan status on the server.

## 🛠️ Remediation & Auto-Fix Steps
If client-side-only protection is found, execute the following fixes:

1. **Inject Server-Side Guards:** Add middleware or server-side verification to the vulnerable API routes.
2. **Verify Session & Plan:** Ensure the backend extracts the user ID from the secure session cookie/token and queries the database to verify their `subscription_status` or `role`.
3. **Enforce Hard Denials:** If the user is unauthenticated or lacks the required tier, the server must return a `401 Unauthorized` or `403 Forbidden` HTTP status code and halt execution.
4. **Convex Specifics:** If using Convex, ensure `ctx.auth` is used inside the query/mutation to fetch the user and verify their plan status before proceeding.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Security Review**
> "Check my app for client-side-only protection. For every premium feature and every logged-in-only page: is the check enforced on the server (API route, database rule, or middleware), or only in the frontend? Flag anything where a user could access data or features by calling the API directly, without the UI."

**Prompt 2: Auto-Fix Backend Guards**
> "For every API route and database function in my app that returns user data or premium features: add a server-side check of the logged-in user and their plan before returning anything. Keep the frontend checks, but treat them as UX, not security. Ensure unauthorized requests get a 401/403 response."

**Prompt 3: Convex + Clerk Setup**
> "I need a clean auth setup. Configure authentication with Clerk, and ensure every backend function checks who's calling. If using Convex, ensure `ctx.auth` is used to verify the user. Provide the setup commands and code structure for this."