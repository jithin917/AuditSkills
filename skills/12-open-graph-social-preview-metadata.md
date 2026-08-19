# 🎨 Skill: Open Graph (OG) & Social Preview Metadata

## 🎯 Objective
Ensure that every public page in the application has properly configured Open Graph (OG) and Twitter Card metadata. This guarantees that when links are shared on WhatsApp, iMessage, X (Twitter), LinkedIn, or other platforms, they render as rich, professional previews with an image, title, and description.

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers often focus on the app's internal UI and forget how it looks *outside* the app. 
- **Real-world consequence:** On launch day, your link gets shared more than ever. A bare grey link with no image, or worse, a preview pointing to `localhost:3000`, destroys credibility and drastically reduces click-through rates. Social platforms cache these previews, meaning a broken one can stick around for days even after you fix the code.
- **The Rule:** The preview image gets more attention and more clicks, and it takes less than two minutes to set up. Get it right before the first share.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** deploy a public-facing page without `og:title`, `og:description`, `og:image`, and `twitter:card` metadata.
2. **NEVER** leave `localhost`, `127.0.0.1`, or staging URLs in any metadata tags or image paths.
3. **ALWAYS** ensure the `og:image` is exactly 1200x630 pixels for optimal rendering across all major platforms.
4. **ALWAYS** include a favicon (`favicon.ico` or `favicon.svg`) in the root or public directory.

## 🔍 Audit Protocol
When triggered, scan the codebase (especially layout files, head components, or server-side metadata exports) to verify:

- [ ] **Tag Presence:** Confirm the presence of `<meta property="og:title">`, `<meta property="og:description">`, `<meta property="og:image">`, and `<meta name="twitter:card" content="summary_large_image">`.
- [ ] **Absolute URLs:** Verify that the `og:image` and `og:url` use absolute, production-ready URLs (e.g., `https://yourapp.com/og.png`), not relative paths.
- [ ] **Localhost Check:** Grep the codebase for `localhost` within any `<meta>` tags or metadata objects.
- [ ] **Favicon Check:** Verify a favicon is linked in the `<head>` or defined in the framework's metadata config.
- [ ] **Dynamic Pages:** For dynamic routes (e.g., `/product/[id]`), ensure the metadata is dynamically generated to reflect the specific product/title, with a fallback to the default `og.png`.

## 🛠️ Remediation & Auto-Fix Steps
If metadata is missing, incomplete, or contains localhost references, execute the following fixes:

1. **Generate Metadata Code:** 
   - *Next.js (App Router):* Generate the `export const metadata = { ... }` or `generateMetadata` function with all required OG and Twitter tags.
   - *React/Vite/HTML:* Generate the standard `<meta>` tags to be placed in the `<head>` of `index.html` or a layout component.
2. **Image Placement Instructions:** Instruct the user to create or generate an `og.png` (1200x630px) and place it in the `public/` directory.
3. **Favicon Setup:** Provide a standard favicon link tag or Next.js `icon` metadata configuration.
4. **Cache Busting Tip:** Remind the user that if they update an existing `og.png`, they should rename it (e.g., `og-v2.png`) or use a query string (`og.png?v=2`) to force social platforms to clear their cache.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Metadata Audit & Fix**
> "Add Open Graph preview metadata to my app. Create the metadata tags (og:title, og:description, og:image, twitter:card summary_large_image) for my main layout. Tell me exactly where to put the og.png file (1200x630px) and ensure no localhost URLs are present. Also add a favicon if missing."

**Prompt 2: Dynamic Page Metadata**
> "My app has dynamic pages (e.g., /item/[id]). Update the metadata generation so that each page dynamically pulls the item's name and description for the og:title and og:description, with a fallback to the default og.png if the item lacks a specific image."

**Prompt 3: Next.js App Router Specific**
> "Generate the complete Next.js App Router `metadata` and `generateMetadata` export for my root layout and dynamic routes, ensuring all Open Graph and Twitter Card tags are correctly formatted with absolute URLs pointing to my production domain."