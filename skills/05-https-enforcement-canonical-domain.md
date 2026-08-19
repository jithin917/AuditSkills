# 🛡️ Skill: HTTPS Enforcement & Canonical Domain Redirects

## 🎯 Objective
Ensure that every variation of the application's URL (HTTP/HTTPS, www/non-www) automatically and securely redirects to a single, canonical HTTPS domain. Prevent browser security warnings, broken shared links, and SEO splitting.

## 🧠 Context & "Why It Matters"
- **The Threat:** Hosting platforms often provision SSL certificates automatically, but fail to configure the redirect logic between `www` and `non-www` variants, or leave HTTP ports open without forcing HTTPS.
- **Real-world consequence:** If `www.yourapp.com` shows an error while `yourapp.com` works, half the links people share will be broken. Furthermore, Google treats `www` and `non-www` as two completely different sites if not properly redirected, splitting your SEO authority. Browser security warnings instantly destroy user trust.
- **The Rule:** All four variations (`http://`, `https://`, `http://www.`, `https://www.`) must land on the exact same secure `https://` page.

## 🚨 Critical Rules (Non-Negotiable)
1. **ALWAYS** enforce HTTPS. Unencrypted HTTP traffic must be immediately redirected to HTTPS.
2. **ALWAYS** choose a single canonical domain (either `yourapp.com` OR `www.yourapp.com`) and redirect all other variations to it.
3. **NEVER** leave multiple domain variants active without proper 301 (Permanent) redirects configured at the host or DNS level.

## 🔍 Audit Protocol
When triggered, verify the domain and SSL configuration based on the hosting provider:

- [ ] **Canonical Choice:** Identify the chosen canonical domain (e.g., `https://yourapp.com`).
- [ ] **Vercel Check:** Verify that both `yourapp.com` and `www.yourapp.com` are added in the Vercel Domains settings, and the "Redirect" toggle is enabled for the non-canonical version.
- [ ] **Netlify Check:** Verify that both domains are in Netlify Domain Management, and a redirect rule is set.
- [ ] **Cloudflare Check:** Verify "Always Use HTTPS" is enabled in the SSL/TLS settings, and a Page Rule or Redirect Rule is set for the canonical domain.
- [ ] **SSL Grade:** (Optional but recommended) Confirm the domain is configured to achieve an "A" grade on ssllabs.com/ssltest (e.g., no outdated TLS versions, valid certificate chain).

## 🛠️ Remediation & Auto-Fix Steps
If misconfigurations are found, generate the exact configuration needed to fix them:

1. **For Vercel:** 
   - Instruct the user to go to Project Settings > Domains, add both variants, and click "Redirect" on the non-canonical one.
   - Alternatively, provide a `vercel.json` snippet:
     ```json
     {
       "redirects": [
         { "source": "http://(.*)", "destination": "https://$1", "permanent": true },
         { "source": "https://www.yourapp.com/(.*)", "destination": "https://yourapp.com/$1", "permanent": true }
       ]
     }
     ```
2. **For Netlify:** 
   - Provide a `_redirects` file or `netlify.toml` snippet:
     ```toml
     [[redirects]]
       from = "http://*"
       to = "https://:splat"
       status = 301
       force = true

     [[redirects]]
       from = "https://www.yourapp.com/*"
       to = "https://yourapp.com/:splat"
       status = 301
       force = true
     ```
3. **For Nginx:** 
   - Provide the server block configuration to listen on port 80 and `www`, returning a 301 redirect to the canonical HTTPS domain.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Domain & SSL Audit**
> "Run the HTTPS and Domain Redirect audit. Check my hosting configuration (Vercel, Netlify, Cloudflare, or Nginx) to ensure that http://, https://, http://www., and https://www. all redirect to a single canonical https:// domain. Provide the exact config changes needed if any variant is missing or not redirecting."

**Prompt 2: Auto-Fix Redirects (Vercel/Netlify)**
> "I want to enforce HTTPS and redirect all www traffic to my bare domain (or vice versa). Generate the exact vercel.json or netlify.toml redirect rules to ensure http:// and www. variants permanently (301) redirect to my canonical https:// domain."

**Prompt 3: SSL Configuration Check**
> "Review my current SSL/TLS setup. What do I need to configure in my DNS or hosting provider to ensure I get an 'A' grade on SSL Labs and that no HTTP traffic is served unencrypted?"