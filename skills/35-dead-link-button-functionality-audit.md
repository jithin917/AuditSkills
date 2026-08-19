# 🔗 Skill: Dead Link & Button Functionality Audit

## 🎯 Objective
Ensure every internal link, external link, and interactive button in the application routes to a valid destination or triggers a defined action. Eliminate dead ends, placeholder links, and non-functional UI elements that degrade user trust and make the app feel unfinished.

## 🧠 Context & "Why It Matters"
- **The Threat:** During rapid development, it's common to leave placeholder links (like `#` or `javascript:void(0)`) or buttons without `onClick` handlers, intending to "fix them later."
- **Real-world consequence:** A visitor clicks "Terms of Service" and gets a 404. They click the Twitter icon in the footer and nothing happens. They click "View Pricing" and it leads nowhere. Visitors hit *one* dead link and instantly assume the whole app is unfinished or broken, and they leave.
- **The Rule:** No dead ends. Every link goes somewhere real, and every button does something. 

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** deploy a link pointing to `#`, `javascript:void(0)`, or an empty string unless it is explicitly styled as disabled (e.g., `opacity-50`, `cursor-not-allowed`, `pointer-events-none`).
2. **NEVER** leave navigation, footer, or content links pointing to routes that do not exist in the application's router.
3. **NEVER** leave external links (social media, documentation, support) pointing to placeholder URLs or the developer's personal accounts.
4. **ALWAYS** ensure every `<button>` has a clear purpose: either an `onClick` handler, a `type="submit"` (if inside a form), or a valid `href` (if acting as a link).

## 🔍 Audit Protocol
When triggered, scan the codebase to map valid routes and cross-reference them with all interactive elements:

- [ ] **Route Mapping:** Identify all valid internal routes (e.g., by scanning the `app/` or `pages/` directory structure).
- [ ] **Link Extraction:** Parse all components (especially `Header`, `Footer`, `Sidebar`, `Hero`, and `Pricing` sections) to extract all `<a>`, `<Link>`, and `<button>` elements.
- [ ] **Internal Link Validation:** Cross-reference internal `href` or `to` attributes against the valid route map. Flag any that result in a 404.
- [ ] **Placeholder Check:** Grep the codebase for `href="#"`, `href=""`, `href="javascript:void(0)"`, and `onClick={() => {}}` (empty functions).
- [ ] **External Link Check:** Verify all external URLs (social icons, footer links) point to the correct, live, and public-facing profiles or pages.
- [ ] **Button Action Check:** Flag any `<button>` elements that lack an `onClick` handler, `type="submit"`, or `type="button"` with a clear action.

## 🛠️ Remediation & Auto-Fix Steps
If dead links or non-functional buttons are found, execute the following fixes:

1. **Fix Internal 404s:** 
   - If the route exists but the link is typo'd, fix the typo.
   - If the feature isn't built yet, either remove the link entirely or style it as "Coming Soon" (disabled state).
2. **Remove Placeholders:** 
   - Delete or comment out any `href="#"` or empty `onClick` handlers. 
   - If the element is meant to be interactive later, wrap it in a feature flag or conditionally render it only when the feature is ready.
3. **Update External URLs:** 
   - Replace placeholder social media or support links with the actual, live URLs for the business.
4. **Add Missing Handlers:** 
   - For buttons missing actions, either attach the correct `onClick` logic or convert them to `<Link>` components if they are meant to navigate.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Dead Link Audit**
> "Go through my app and list every internal link and button. Check each one leads to a real page or action. List everything that's broken, missing, points to a 404, or goes to a placeholder like '#'. Tell me exactly how to fix them."

**Prompt 2: Footer & Navigation Cleanup**
> "Scan my Header, Footer, and Sidebar components. Identify any social media icons, 'Terms' links, or navigation items that are pointing to placeholder URLs, '#', or non-existent routes. Update them to the correct live URLs or remove them."

**Prompt 3: Button Functionality Check**
> "Audit all <button> elements in my codebase. Flag any buttons that are missing an onClick handler, lack a type attribute, or have empty/placeholder functions. Provide the code to either wire up the correct action or disable the button visually if the feature isn't ready."