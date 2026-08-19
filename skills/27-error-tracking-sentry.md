# 🐛 Skill: Error Tracking & Source Map Integration (Sentry)

## 🎯 Objective
Implement comprehensive, full-stack error tracking (frontend and backend/API) with source map integration. Guarantee that when the application crashes or throws an exception in production, the development team is instantly notified with a readable, actionable stack trace.

## 🧠 Context & "Why It Matters"
- **The Threat:** On launch day, real traffic will break things that never broke in local testing (e.g., a payment flow failing specifically for Safari users). Furthermore, 99% of users who encounter a bug will not report it—they will just leave and never come back.
- **Real-world consequence:** Your payment flow breaks for a specific browser on day 2. You don't find out until day 9, when you receive an angry email. That's a full week of silently lost signups and revenue.
- **The Rule:** You must find out when your app breaks for a user *before* the user tells you. Error tracking means you can fix critical issues in minutes, not weeks.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch a production application without a dedicated error tracking service (e.g., Sentry, Bugsnag, Datadog) installed and configured.
2. **NEVER** deploy without uploading source maps. Unmapped stack traces are useless; you need to see the exact line of your original code that failed, not the minified production bundle.
3. **NEVER** hardcode the error tracking DSN (Data Source Name). Always use environment variables to allow for different environments (dev, staging, prod).
4. **ALWAYS** ensure error tracking covers both the client-side (browser) and server-side (API routes, background jobs, database calls).

## 🔍 Audit Protocol
When triggered, scan the codebase and build configuration to verify error tracking is fully operational:

- [ ] **Provider Detection:** Check `package.json` for error tracking SDKs (e.g., `@sentry/nextjs`, `@sentry/react`, `@sentry/node`).
- [ ] **Full-Stack Coverage:** Verify that the SDK is initialized for the client (browser), server (Node.js/API), and edge (middleware/edge functions) if applicable.
- [ ] **Source Map Upload:** Inspect the build configuration (e.g., `next.config.js`, `vite.config.ts`, or CI/CD pipelines) to ensure the Sentry Webpack/Vite plugin is active and uploading source maps during the production build.
- [ ] **Environment Variables:** Verify that `SENTRY_DSN` (and `NEXT_PUBLIC_SENTRY_DSN` if needed) are defined in `.env.example` and properly injected.
- [ ] **Filtering Noise:** Check if basic noise filtering is applied (e.g., ignoring `ChunkLoadError` or specific third-party extension errors) to prevent alert fatigue.

## 🛠️ Remediation & Auto-Fix Steps
If error tracking is missing or misconfigured, execute the following fixes:

1. **Install and Initialize Sentry:**
   - *Next.js:* Run `npx @sentry/wizard@latest -i nextjs` or manually install `@sentry/nextjs`.
   - Generate the required configuration files: `sentry.client.config.ts`, `sentry.server.config.ts`, and `sentry.edge.config.ts`.
2. **Configure Source Maps:**
   - Update the framework config (e.g., `next.config.js`) to include the Sentry plugin and enable source map generation:
     ```javascript
     const { withSentryConfig } = require("@sentry/nextjs");
     module.exports = withSentryConfig(yourNextConfig, {
       hideSourceMaps: true,
     });
     ```
3. **Set Environment Variables:**
   - Add the DSN to `.env.local` and `.env.example`.
4. **Test the Integration:**
   - Instruct the user to create a temporary test route or button that intentionally throws an error (e.g., `throw new Error("Sentry Test Error")`).
   - Verify the error appears in the Sentry dashboard with a fully readable, unmapped stack trace.
5. **Clean Up:**
   - Remove the test error code after verification.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Full-Stack Sentry Setup**
> "Add Sentry error tracking to my app: frontend and backend/API errors, with source maps uploaded so I see readable stack traces. Use environment variables for the DSN. Ensure it covers client, server, and edge runtimes."

**Prompt 2: Fix Missing Source Maps**
> "My Sentry stack traces are showing minified code and are unreadable. Check my build configuration (Next.js/Vite/Webpack) and ensure the Sentry plugin is correctly installed and configured to upload source maps during the production build."

**Prompt 3: Test Error Tracking**
> "I just installed Sentry. Create a temporary, hidden test button on my homepage that throws a specific error when clicked. I will click it to verify the error shows up in my Sentry dashboard with a correct stack trace. Tell me when it's ready to test."