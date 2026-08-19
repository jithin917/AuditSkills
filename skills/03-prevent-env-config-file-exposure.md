# 🛡️ Skill: Prevent `.env` and Config File Exposure

## 🎯 Objective
Ensure that `.env` files, `.git` directories, and other sensitive configuration files are strictly excluded from public web access, build outputs, and version control. Prevent accidental exposure of API keys, database URLs, and secrets.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI coding tools and modern build systems can sometimes misconfigure public directories or server routing, accidentally serving sensitive files as static assets.
- **Real-world consequence:** Bots actively and automatically scan every newly deployed domain for paths like `/.env` and `/.git/config` within hours of deployment. If found, every secret in your app is considered instantly stolen.
- **The Rule:** This check takes 60 seconds. Skipping it can cost you every account, database, and third-party service your app touches.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** commit `.env`, `.env.local`, or `.env.production` files to version control (Git).
2. **NEVER** place `.env` files inside public-facing directories (e.g., `public/`, `static/`, `www/`).
3. **ALWAYS** treat any exposed secret as immediately compromised. If a file is reachable, rotate the key immediately—do not just hide it and assume it's safe.

## 🔍 Audit Protocol
When triggered, perform the following checks on the codebase and deployment configuration:

- [ ] **Git Ignore Check:** Verify that `.env*` (including `.env.local`, `.env.production`, `.env.test`) and `.git/` are explicitly listed in the `.gitignore` file.
- [ ] **Public Directory Check:** Scan the `public/` or `static/` folders to ensure no `.env` or `.git` files have been accidentally placed there.
- [ ] **Build Config Check:** Review build configurations (e.g., `next.config.js`, `vite.config.ts`, `webpack.config.js`) to ensure environment files are not being copied to the output directory.
- [ ] **Server/Host Config Check:** Verify that the hosting provider (Vercel, Netlify, Nginx, Apache) is configured to block HTTP requests to `/.env*` and `/.git/*` paths.

## 🛠️ Remediation & Auto-Fix Steps
If vulnerabilities or misconfigurations are found, execute the following fixes:

1. **Immediate Mitigation (If Exposed):** 
   - Alert the user: "CRITICAL: `.env` files are publicly accessible. You must rotate ALL keys in this file immediately via your provider dashboards (e.g., Supabase, OpenAI, Stripe)."
2. **Update `.gitignore`:** 
   - Append `.env*` and `.env` to the root `.gitignore` file.
3. **Clean Public Folders:** 
   - Delete any `.env` or `.git` files found inside `public/` or `static/` directories.
4. **Enforce Server Blocking:** 
   - Generate the necessary configuration snippet to block these paths. 
     - *Vercel/Netlify:* Add a redirect rule with `status: 404` or `403` for `/.env*` and `/.git/*`.
     - *Nginx:* Add `location ~ /\.env { deny all; }` and `location ~ /\.git { deny all; }`.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Exposure Audit**
> "Run the Environment Security Audit. Check my codebase and deployment config to ensure `.env`, `.env.local`, `.env.production`, and `.git/config` cannot be downloaded from the internet. Verify they are in `.gitignore`, not in public folders, and blocked by the host config."

**Prompt 2: Auto-Fix Misconfiguration**
> "My `.env` file might be reachable on my live domain. Make sure `.env*` files are excluded from the build and public output, blocked in my host config (provide the Vercel/Nginx rules), and strictly listed in `.gitignore`. Also, remind me to rotate keys if they were ever exposed."

**Prompt 3: Post-Deployment Verification**
> "I just deployed my app. Give me a checklist of URLs I should manually test in my browser to prove that my `.env` and `.git` files are returning 404/403 errors and not showing file contents."