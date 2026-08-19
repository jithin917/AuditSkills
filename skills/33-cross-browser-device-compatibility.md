# 📱 Skill: Cross-Browser & Cross-Device Compatibility Testing

## 🎯 Objective
Ensure the application functions correctly, renders consistently, and provides a seamless user experience across different browsers (specifically Safari vs. Chrome/Edge) and device types (desktop vs. mobile).

## 🧠 Context & "Why It Matters"
- **The Threat:** Developers naturally build and test in their primary browser (usually Chrome or Edge on a large desktop monitor). 
- **Real-world consequence:** Everything works perfectly in Chrome, but the date picker is completely broken in Safari, or a button is unclickable on mobile. Since every iPhone uses Safari, this instantly alienates a massive portion of your mobile traffic.
- **The Rule:** You built and tested in one browser. Your users will pick their own. Always validate the core user flow in at least one alternative browser and on a mobile device before launch.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** assume that a feature working in Chrome guarantees it will work in Safari, Firefox, or mobile browsers.
2. **NEVER** rely on default browser styling for critical form elements (like `<input type="date">` or `<select>`) without testing them in Safari/iOS, as they render drastically differently.
3. **ALWAYS** ensure the `<meta name="viewport" content="width=device-width, initial-scale=1">` tag is present and correctly configured to prevent mobile scaling issues.

## 🔍 Audit Protocol
When triggered, scan the codebase for common cross-browser pitfalls and provide a manual testing checklist:

- [ ] **Viewport Check:** Verify the root HTML/layout file contains the correct viewport meta tag for mobile responsiveness.
- [ ] **Form Element Check:** Flag any native HTML date pickers (`<input type="date">`), file inputs, or custom dropdowns that might suffer from Safari/iOS rendering quirks.
- [ ] **CSS Prefix/Compatibility Check:** Identify any modern CSS features (e.g., `backdrop-filter`, specific grid/flexbox behaviors, `:has()`) that might need fallbacks or `-webkit-` prefixes for older Safari versions.
- [ ] **Touch Target Check:** Ensure interactive elements (buttons, links) have a minimum height/width of 44x44px to be easily tappable on mobile devices.

## 🛠️ Remediation & Auto-Fix Steps
If potential cross-browser issues are identified, execute the following fixes:

1. **Fix Safari Form Quirks:** 
   - Add CSS resets for problematic inputs. For example, to fix iOS Safari's default styling on inputs:
     ```css
     input, select, textarea {
       -webkit-appearance: none;
       -moz-appearance: none;
       appearance: none;
       border-radius: 4px; /* Re-add desired radius */
     }
     ```
2. **Ensure Viewport Correctness:** 
   - Inject the standard viewport meta tag into the `<head>` if missing.
3. **Provide Manual Testing Checklist:** 
   - Generate a step-by-step guide for the user to physically test the app:
     1. Open the app in your secondary browser (e.g., Safari if you use Chrome).
     2. Open the app on a physical mobile device (or a highly accurate simulator like BrowserStack).
     3. Execute the core flow: Sign up, navigate to the main feature, fill out a form, and complete a payment.
     4. Note any layout shifts, unclickable buttons, or weird input behaviors.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Cross-Browser Quirk Audit**
> "Audit my codebase for common cross-browser compatibility issues, especially for Safari and iOS. Check my form inputs, date pickers, and CSS for anything that might break or render weirdly outside of Chrome. Provide the exact CSS fixes or polyfills needed."

**Prompt 2: Mobile Responsiveness & Touch Target Check**
> "Scan my UI components to ensure they are mobile-friendly. Verify I have the correct viewport meta tag, and check that all buttons and interactive elements meet the minimum 44x44px touch target size for mobile users."

**Prompt 3: Generate Manual Testing Checklist**
> "I am about to launch. Give me a concise, step-by-step manual testing checklist to verify my core user flow (signup, core feature, payment) works perfectly in Safari, Chrome, and on a physical mobile device. Highlight the specific things I should look out for."