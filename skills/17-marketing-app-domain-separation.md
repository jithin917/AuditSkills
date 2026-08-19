# 🏗️ Skill: Marketing & App Domain Separation

## 🎯 Objective
Ensure the marketing/landing pages (e.g., `yourapp.com`) and the core web application (e.g., `app.yourapp.com`) are deployed and hosted separately. Optimize landing page performance, enable independent deployment cycles, and allow the use of specialized no-code tools (like Framer or Webflow) for marketing.

## 🧠 Context & "Why It Matters"
- **The Threat:** Bundling the marketing site and the web app into a single deployment/domain seems convenient initially, but creates tight coupling. 
- **Real-world consequence:** Fixing a simple typo on the homepage forces a full redeployment of the entire application codebase. The landing page loads slower because it carries the app's heavy JavaScript bundle. If you try to split them *after* launch, every user bookmark, shared link, and OAuth redirect URL will break.
- **The Rule:** Before launch, this is just one DNS record. After launch, it's a painful migration. Do it on day one.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** bundle the heavy JavaScript/application logic of the authenticated dashboard with the public-facing marketing pages.
2. **ALWAYS** host the authenticated application on a dedicated subdomain (e.g., `app.yourapp.com`, `dashboard.yourapp.com`).
3. **ALWAYS** keep public, SEO-critical pages (Home, Pricing, Blog, Legal, About) on the root domain (`yourapp.com`).

## 🔍 Audit Protocol
When triggered, analyze the project structure and deployment setup:

- [ ] **Deployment Check:** Determine if the marketing pages and the app are currently served from the same codebase and deployment URL.
- [ ] **Bundle Size Check:** Verify that the root domain (`/`) is not loading heavy app-specific dependencies (e.g., database clients, complex state management, heavy UI libraries) unnecessarily.
- [ ] **DNS Configuration:** Check if a CNAME record exists for the `app` subdomain pointing to the application hosting provider (e.g., Vercel, Railway, Render).
- [ ] **Redirect/Callback Check:** If splitting is happening, verify that all OAuth providers (Clerk, NextAuth, Google) and payment gateways (Stripe) have their redirect/callback URLs updated to the new `app.yourapp.com` domain.

## 🛠️ Remediation & Auto-Fix Steps
If the app and marketing site are currently bundled, execute the following separation steps:

1. **DNS Configuration:** 
   - Instruct the user to go to their DNS provider (Cloudflare, Namecheap, etc.).
   - Create a new `CNAME` record: Name = `app`, Value = `[your-app-hosting-url, e.g., cname.vercel-dns.com]`.
2. **Codebase Separation (If applicable):** 
   - If using a monorepo, ensure the marketing site and app are distinct packages/apps with separate build outputs.
   - If using Next.js, suggest using Middleware to redirect `/app/*` traffic to `app.yourapp.com` if legacy links exist.
3. **Update Auth & Payment Configs:** 
   - Generate a checklist for the user to update:
     - Clerk/NextAuth: Allowed redirect URLs and Callback URLs.
     - Stripe: Webhook endpoints and Customer Portal return URLs.
     - Google Search Console: Verify the new `app.` subdomain separately if needed.
4. **No-Code Integration (Optional):** 
   - If the user wants to use Framer/Webflow for the landing page, provide the specific DNS A/CNAME records required by those platforms for the root domain.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Domain Separation Audit**
> "Run the Domain Separation audit. Check if my marketing pages and my core app are currently bundled in the same deployment. If they are, outline the exact steps to split them so the app lives on 'app.yourapp.com' and the marketing site stays on 'yourapp.com'."

**Prompt 2: DNS & Subdomain Setup Guide**
> "I want to host my app on 'app.yourapp.com' and my landing page on 'yourapp.com'. Give me the exact DNS records (CNAME/A records) I need to add in Cloudflare/Namecheap to point the 'app' subdomain to my Vercel/Render deployment, while keeping the root domain for marketing."

**Prompt 3: Post-Split OAuth & Webhook Update Checklist**
> "I am moving my app to a subdomain (app.yourapp.com). Generate a comprehensive checklist of every place I need to update my URLs, including Clerk/NextAuth callback URLs, Stripe webhook endpoints, and Google OAuth console settings, so nothing breaks."