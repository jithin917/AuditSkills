# 🚪 Skill: Custom 404 Page & HTTP Status Code Validation

## 🎯 Objective
Ensure the application serves a user-friendly, custom 404 (Not Found) page that correctly returns an HTTP 404 status code (not 200 OK). This preserves SEO integrity and retains visitors who encounter broken links or typos in URLs.

## 🧠 Context & "Why It Matters"
- **The Threat:** Every launch has broken links from typos in social media posts, DMs, or outdated bookmarks. 
- **Real-world consequence:** A user clicks a broken link and sees a blank white screen, a raw framework error message, or a "Page Not Found" text that secretly reports a `200 OK` status to Google (a "soft 404"). This destroys user trust, causes immediate bounce, and actively harms SEO.
- **The Rule:** A good 404 page acknowledges the mistake, maintains brand tone, and provides a clear path back to the homepage, keeping those visitors on your site.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** allow a missing route to return an HTTP `200 OK` status code. It must be a true `404 Not Found`.
2. **NEVER** show a raw, unstyled framework error screen (e.g., default Next.js or Vite error pages) in production.
3. **ALWAYS** include a clear, actionable way for the user to recover, such as a prominent button linking back to the homepage (`/`) or the dashboard.
4. **ALWAYS** ensure the custom 404 page itself does not trigger secondary errors (e.g., missing fonts or broken images).

## 🔍 Audit Protocol
When triggered, verify the existence and correctness of the 404 handling:

- [ ] **File Existence:** Check for the framework-specific 404 file (e.g., `app/not-found.tsx` or `pages/404.tsx` in Next.js, `404.html` in Vite/static hosts).
- [ ] **UI Check:** Verify the page contains a friendly message (e.g., "Oops, this page doesn't exist") and a working link/button back to the homepage.
- [ ] **HTTP Status Verification:** Instruct the user to test a nonsense URL (e.g., `yourapp.com/asdfasdf`) using a tool like `httpstatus.io` or browser DevTools (Network tab) to confirm the response status is exactly `404`, not `200`.
- [ ] **Layout Consistency:** Ensure the 404 page still renders the global layout (or intentionally strips it for a clean look) without crashing.

## 🛠️ Remediation & Auto-Fix Steps
If the 404 page is missing, ugly, or returning the wrong status code, execute the following fixes:

1. **Generate Custom 404 Component:** 
   - *Next.js (App Router):* Create `app/not-found.tsx`. Ensure it exports a React component with a helpful message and a `<Link href="/">Return Home</Link>`.
2. **Enforce 404 Status Code:** 
   - *Next.js:* The `not-found.tsx` file automatically returns a 404 status. If using a custom error boundary, ensure `headers().set('x-status', '404')` or equivalent is used.
   - *Vite/Static:* Ensure the hosting provider (Vercel, Netlify, Cloudflare Pages) is configured to serve `404.html` for unmatched routes with a 404 status.
3. **Provide Testing Instructions:** 
   - Give the user the exact steps to verify: "Go to httpstatus.io, enter `https://yourapp.com/this-page-does-not-exist`, and verify the tool reports a 404 status code."

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Create Custom 404 Page**
> "Create a custom 404 page for my app. It should have a friendly message, a clear link back to the homepage, and it must return a real HTTP 404 status code, not 200. Use my app's existing design system/styling."

**Prompt 2: Audit 404 Status Code**
> "Check my app's 404 handling. Verify that navigating to a nonsense URL (like /asdfasdf) returns a true 404 HTTP status code and not a 200 OK 'soft 404'. Tell me how to test this using httpstatus.io or browser DevTools."

**Prompt 3: Fix Framework Default Error Pages**
> "I am seeing the default framework error page when a route is missing. Replace it with a branded, custom 404 component that matches my app's design and safely guides the user back to the homepage."