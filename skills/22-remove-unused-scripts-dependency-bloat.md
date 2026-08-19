# 🧹 Skill: Remove Unused Third-Party Scripts & Dependency Bloat

## 🎯 Objective
Identify, evaluate, and eliminate unused, unnecessary, or overly heavy third-party scripts and libraries (e.g., chat widgets, redundant analytics, tracking pixels) to maximize application performance, reduce bundle size, and improve load times.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI coding assistants and developers often install third-party libraries "just in case" they might be needed later. 
- **Real-world consequence:** An Intercom or Zendesk widget (300KB+) loading synchronously on every single page for an app that has zero users yet can cost half a second of critical load time. 
- **The Rule:** At the early stage: use one analytics tool, no chat widget, and nothing you can't name a specific, immediate reason for. Add tools only when you need them. Every script you remove makes the app faster today.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** load heavy, non-critical third-party scripts (chat widgets, session recorders, secondary analytics) synchronously in the `<head>` or on every page.
2. **NEVER** keep unused `npm` packages or CDN links in the codebase "just in case." If it's not actively used, remove it.
3. **ALWAYS** lazy-load necessary but non-critical scripts (e.g., load chat widgets only after the main content has rendered, or only on specific support pages).

## 🔍 Audit Protocol
When triggered, scan the codebase, `package.json`, and layout files to identify bloat:

- [ ] **Package.json Audit:** List all third-party dependencies. Flag any that are not actively imported or used in the codebase (e.g., `framer-motion` if no animations exist, heavy date libraries like `moment.js` when `date-fns` is available).
- [ ] **Script Tag Scan:** Search for external `<script>` tags in `layout.tsx`, `index.html`, or `<head>` components (e.g., Intercom, Hotjar, Google Tag Manager, Facebook Pixel).
- [ ] **Load Strategy Check:** For each identified script, determine:
  1. What does it do?
  2. How big is it (approximate KB)?
  3. Is it loaded on *every* page or just where needed?
- [ ] **Redundancy Check:** Flag if multiple tools do the same thing (e.g., Google Analytics + Plausible + Mixpanel all tracking basic pageviews).

## 🛠️ Remediation & Auto-Fix Steps
If bloat or misconfigured scripts are found, execute the following fixes:

1. **Remove Unused Packages:** 
   - Run `npm uninstall <unused-package>` and remove all related import statements and code.
2. **Lazy-Load Necessary Scripts:** 
   - If a script is needed but not critical for initial render (e.g., a chat widget), refactor it to load lazily.
   - *Next.js Example:* Use `<Script src="..." strategy="lazyOnload" />` or `afterInteractive`.
   - *Vanilla/React Example:* Dynamically inject the script tag only after `window.onload` or when the user scrolls/interacts.
3. **Conditional Loading:** 
   - Move global scripts to specific routes where they are actually relevant (e.g., only load the pricing calculator script on the `/pricing` page).
4. **Consolidate Analytics:** 
   - Recommend keeping only one primary analytics tool (e.g., PostHog, Plausible, or GA4) and removing redundant tracking pixels.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Script Audit**
> "List every third-party script and external library my app loads (chat widgets, analytics, tracking pixels, embeds). For each: what does it do, how big is it, and is it loaded on every page? Recommend which ones to remove entirely and which ones to lazy-load."

**Prompt 2: Lazy-Load Heavy Widgets**
> "I have a heavy third-party script (like Intercom, Hotjar, or a chat widget) loading on every page. Refactor it to load lazily (e.g., using Next.js `strategy='lazyOnload'` or dynamic injection after user interaction) so it doesn't block my initial page render."

**Prompt 3: Package.json Cleanup**
> "Scan my `package.json` and my codebase. Identify any installed dependencies that are no longer imported or used anywhere in my app. Provide the exact `npm uninstall` commands to remove them and clean up my bundle size."