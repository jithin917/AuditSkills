# 🤖 Skill: Invisible Bot Protection (Cloudflare Turnstile)

## 🎯 Objective
Protect application forms (signup, contact, waitlists) from bot spam using invisible, user-friendly verification like Cloudflare Turnstile. Prevent fake signups and burned email quotas without frustrating real users with complex image puzzles, and ensure legitimate AI crawlers are not blocked.

## 🧠 Context & "Why It Matters"
- **The Threat:** Bots scan and target newly deployed domains within hours. Without protection, your forms will be flooded with spam. However, traditional CAPTCHAs (identifying traffic lights, buses, or crosswalks) create terrible UX and cause real users to abandon your site.
- **Real-world consequence:** 400 fake signups overnight ruins your analytics, burns your transactional email quota with confirmation emails to garbage addresses, and clutters your database. Conversely, turning on aggressive "Bot Fight Mode" in Cloudflare can accidentally block good bots, including the crawlers behind ChatGPT and Perplexity, meaning AI tools can't find or cite your app.
- **The Rule:** Block the spammers, not the search engines or AI crawlers. Use invisible verification for forms, and keep general bot blocking permissive for good bots.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** use frustrating, visible CAPTCHAs (like reCAPTCHA v2 image challenges) for standard forms if an invisible alternative (like Turnstile) is available.
2. **NEVER** validate a bot protection token solely on the client-side. The token *must* be verified on the server-side (API route or Server Action) before processing the form submission.
3. **NEVER** enable aggressive "Bot Fight Mode" or strict WAF challenges if you want your site to be indexed and cited by AI search engines (Perplexity, ChatGPT) and standard search engines.

## 🔍 Audit Protocol
When triggered, scan the codebase and form implementations to verify bot protection:

- [ ] **Form Protection Check:** Identify all public-facing forms (signup, login, contact, newsletter). Check if they are protected by an invisible CAPTCHA (e.g., Cloudflare Turnstile, hCaptcha invisible).
- [ ] **Server-Side Validation:** Inspect the backend handler for these forms. Verify that the Turnstile secret key is used to validate the `cf-turnstile-response` token via Cloudflare's API before creating the user or sending the email.
- [ ] **Environment Variables:** Ensure both the Turnstile Site Key (public) and Secret Key (private) are correctly stored in environment variables.
- [ ] **Crawler Blocking Check:** If the user is using Cloudflare proxy, warn them to check their Cloudflare Dashboard > Security > Bots settings to ensure "Bot Fight Mode" isn't blocking legitimate AI and search crawlers.

## 🛠️ Remediation & Auto-Fix Steps
If forms lack bot protection or use frustrating CAPTCHAs, execute the following fixes:

1. **Install Turnstile Client Component:** 
   - Install the React wrapper: `npm install @marsidev/react-turnstile` (or the appropriate framework package).
   - Add the `<Turnstile>` component to the form, using the public `NEXT_PUBLIC_TURNSTILE_SITE_KEY`.
2. **Implement Server-Side Verification:** 
   - Create or update the form's API route / Server Action.
   - Extract the token from the form data.
   - Make a `POST` request to `https://challenges.cloudflare.com/turnstile/v0/siteverify` with the secret key and the token.
   - Only proceed with the form logic (e.g., creating the user) if the response `success` is `true`.
3. **Provide Setup Instructions:** 
   - Give the user the exact steps to get their keys: "Go to Cloudflare Dashboard > Turnstile > Add Site. Select 'Managed' mode. Copy the Site Key and Secret Key into your `.env.local`."
4. **Specialized Skill Integration:** 
   - Recommend the official Cloudflare skill for automated setup: `npx skills add cloudflare/skills --skill turnstile-spin`.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Turnstile Implementation**
> "Add Cloudflare Turnstile to my signup and contact forms. Implement the client-side widget and ensure the token is validated on the server side before processing. Use environment variables for the site and secret keys. I don't want annoying puzzles for real users."

**Prompt 2: Automated Setup via Cloudflare Skill**
> "I want to set up bot protection using the official Cloudflare skill. I am running: `npx skills add cloudflare/skills --skill turnstile-spin`. Now, apply this to my signup form to stop spam without blocking AI crawlers."

**Prompt 3: Server-Side Validation Fix**
> "I have Cloudflare Turnstile on my frontend, but I think my server is just trusting the client. Refactor my form submission API route to actually verify the Turnstile token with Cloudflare's siteverify endpoint using my secret key before creating the user."