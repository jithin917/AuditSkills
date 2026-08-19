# 📐 Skill: Fix Layout Shift (Cumulative Layout Shift / CLS)

## 🎯 Objective
Eliminate visual layout shifts during page load by enforcing explicit dimensions and reserving space for dynamic content. Achieve a Cumulative Layout Shift (CLS) score of under 0.1 to ensure a smooth, professional user experience and maintain strong Core Web Vitals for SEO.

## 🧠 Context & "Why It Matters"
- **The Threat:** As resources (images, fonts, banners, embeds) load asynchronously, they can push existing content around the screen. 
- **Real-world consequence:** A user goes to tap "Sign Up", but an image loads above it, pushing the button down, and the user accidentally taps "Pricing" or a random ad instead. This makes the app feel broken and unprofessional.
- **The Rule:** Google explicitly measures and penalizes this via Core Web Vitals. A CLS score must be under 0.1. Prevent the shift before it happens by reserving space.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** use `<img>`, `<video>`, or `<iframe>` tags without explicit `width` and `height` attributes (or CSS `aspect-ratio`) so the browser can reserve the space before the asset downloads.
2. **NEVER** insert new content (banners, ads, notifications, embeds) above existing content without a reserved placeholder container that has a defined `min-height`.
3. **ALWAYS** optimize web font loading to prevent "Flash of Invisible Text" (FOIT) or "Flash of Unstyled Text" (FOUT) from causing layout shifts. Use `font-display: swap` or preload critical fonts.

## 🔍 Audit Protocol
When triggered, scan the codebase and simulate a slow-network load to identify CLS triggers:

- [ ] **Image/Video Dimensions:** Check all `<img>`, `<video>`, and `<iframe>` elements. Flag any missing `width` and `height` attributes or missing CSS `aspect-ratio`.
- [ ] **Dynamic Content Injection:** Identify components that conditionally render *after* initial paint (e.g., cookie banners, top-of-page notifications, third-party embeds, ads). Verify they have reserved space.
- [ ] **Font Loading:** Check CSS or framework font configurations for `font-display` properties. Flag fonts that block rendering or cause visible text reflow.
- [ ] **Skeleton Loaders:** Verify that data-fetching components (e.g., dashboards, lists) use skeleton loaders with fixed heights rather than rendering nothing and then popping in.

## 🛠️ Remediation & Auto-Fix Steps
If layout shift triggers are found, execute the following fixes:

1. **Enforce Image Dimensions:** 
   - Add explicit `width` and `height` to raw HTML tags, or ensure framework-specific image components (e.g., Next.js `<Image>`) are used correctly, as they automatically handle aspect ratio reservation.
2. **Reserve Space for Dynamic UI:** 
   - Wrap late-loading content (e.g., banners, embeds) in a container with a fixed or `min-height` style matching the expected content size.
3. **Optimize Font Loading:** 
   - Add `<link rel="preload" as="font" ...>` for critical fonts, or ensure `@font-face` rules include `font-display: swap`.
4. **Leverage Specialized Skills:** 
   - Recommend installing and running the Addy Osmani web quality skill for automated CLS detection: `npx skills add addyosmani/web-quality-skills --skill core-web-vitals`.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General CLS Audit & Fix**
> "Fix my layout shift (CLS). Add explicit width and height (or aspect-ratio) to every image, video, and iframe in my app. Also, reserve space for anything that loads late (like banners or embeds) so the layout doesn't jump while loading. Target a CLS score under 0.1."

**Prompt 2: Font & Text Shift Prevention**
> "Check my font loading configuration. Ensure I am not experiencing Flash of Invisible Text (FOIT) or layout shifts from late-loading fonts. Add 'font-display: swap' or preload critical fonts to prevent text from jumping on load."

**Prompt 3: Activate Core Web Vitals Skill**
> "I want to fix my layout shift using best practices. I am running: 'npx skills add addyosmani/web-quality-skills --skill core-web-vitals'. Now, scan my codebase for CLS issues and fix them according to the skill's guidelines."