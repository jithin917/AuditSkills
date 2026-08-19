# 📊 Skill: Core Conversion Funnel Instrumentation

## 🎯 Objective
Define, instrument, and track at least one end-to-end conversion funnel (e.g., Landing Page → Sign Up Click → Account Created → Core Feature Reached) to pinpoint exactly where users drop off in the critical early user journey.

## 🧠 Context & "Why It Matters"
- **The Threat:** Launching with only basic pageview analytics gives you a vanity metric (e.g., "500 visitors, 3 signups") but zero diagnostic power. 
- **Real-world consequence:** You know the launch "went meh," but you have no idea if the problem was a weak headline, a confusing pricing page, a broken signup form, or a lack of onboarding. Without a funnel, you are just guessing what to fix.
- **The Rule:** A funnel turns vague disappointment into actionable data (e.g., "84% of users dropped off at the signup form"). You must know where the leak is before you can patch it.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch without at least one complete, instrumented funnel tracking the journey from initial landing to the "Aha!" moment (core feature usage).
2. **NEVER** rely solely on pageviews to track critical conversion steps. Always use explicit, named event tracking (e.g., `cta_clicked`, `signup_completed`) for actions.
3. **ALWAYS** ensure the final step of the funnel represents actual value delivery (e.g., reaching the dashboard, creating the first item), not just a "Thank You" page.

## 🔍 Audit Protocol
When triggered, map out the intended user journey and verify the codebase is firing the correct events:

- [ ] **Define the Journey:** Identify the 3-4 critical steps for this specific app (Standard: `Visited landing` → `Clicked sign up` → `Created account` → `Reached core feature`).
- [ ] **Event Instrumentation Check:** Scan the frontend and backend code to verify that a distinct analytics event is fired at each of these exact moments.
- [ ] **Data Payload Check:** Ensure the events include necessary properties (e.g., `signup_completed` should include `user_id`, `plan_type`, or `referral_source`).
- [ ] **Provider Verification:** Confirm the analytics tool (e.g., PostHog, Mixpanel) is successfully receiving these specific event names.

## 🛠️ Remediation & Auto-Fix Steps
If funnel events are missing or poorly instrumented, execute the following fixes:

1. **Instrument Frontend Clicks:** 
   - Add tracking to the primary Call-to-Action (CTA) buttons.
   - *Example:* `posthog.capture('signup_cta_clicked', { location: 'hero_section' })`
2. **Instrument Backend/Auth Success:** 
   - Add tracking immediately after a successful database write or authentication callback.
   - *Example:* `posthog.capture('account_created', { method: 'google_oauth' })`
3. **Instrument the "Aha!" Moment:** 
   - Add tracking when the user completes the core value action for the first time.
   - *Example:* `posthog.capture('core_feature_viewed', { feature: 'dashboard' })`
4. **Dashboard Setup Guide:** 
   - Provide step-by-step instructions for the user to build the funnel in their analytics UI (e.g., PostHog > Insights > New Insight > Funnel > Add the 4 events in order).

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Instrument Core Funnel Events**
> "I need to track my core conversion funnel: Landing Page -> Clicked Sign Up -> Account Created -> Reached Core Feature. Scan my codebase and add the exact analytics tracking events (using PostHog/my current provider) at each of these specific steps. Ensure they fire reliably and include relevant properties."

**Prompt 2: PostHog Funnel Setup Guide**
> "I have instrumented my signup and core feature events. Give me a step-by-step guide on how to build a 4-step Funnel Insight in the PostHog dashboard using these events, and tell me how to interpret the drop-off percentages."

**Prompt 3: Identify Missing Funnel Steps**
> "Review my current analytics event tracking. Based on my app's functionality, what are the critical steps in my user journey that I am currently failing to track? Suggest the exact event names and where in the code I should add them to complete my primary conversion funnel."