# 🛡️ Skill: Form Validation & Double-Submit Prevention

## 🎯 Objective
Ensure all application forms (signup, contact, checkout, settings) are robust against invalid inputs, empty submissions, and rapid double-clicks. Prevent application crashes, duplicate database entries, and accidental double charges by implementing strict client/server validation and submission state management.

## 🧠 Context & "Why It Matters"
- **The Threat:** Real users do not read instructions. They mash the "Submit" button impatiently, paste random text into number fields, and try to submit forms without filling out required fields.
- **Real-world consequence:** An empty submit causes a white screen of death. A user double-clicks the "Pay Now" button and gets charged twice. A user types `a@b` into the email field and the backend crashes trying to process it. 
- **The Rule:** Users mash buttons and paste weird things. Build your forms for that. Assume every input is hostile until proven otherwise.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** rely solely on client-side validation. The server (API route or Server Action) MUST re-validate all incoming data to prevent malicious or bypassed submissions.
2. **NEVER** allow a form to be submitted if it is already in a "loading" or "submitting" state. The submit button must be disabled immediately upon the first click.
3. **NEVER** show generic or technical error messages (e.g., "Error 500" or "Invalid type"). Always provide clear, inline, human-readable error messages next to the specific field that failed.
4. **ALWAYS** implement idempotency or backend checks for critical actions (like payments or account creation) to ensure a double-submit doesn't create duplicate records or charges.

## 🔍 Audit Protocol
When triggered, scan the codebase to evaluate form resilience:

- [ ] **Validation Schema Check:** Verify that forms are using a robust validation library (e.g., Zod, Yup, React Hook Form) for both client-side and server-side checks.
- [ ] **Empty Submission Check:** Identify what happens when a form is submitted with all fields empty. Ensure it triggers validation errors instead of crashing the app.
- [ ] **Data Type Check:** Verify that fields expecting numbers or specific formats (emails, URLs) reject text/garbage inputs gracefully.
- [ ] **Double-Submit Prevention:** Inspect all `<form>` submit buttons. Verify they are bound to an `isSubmitting` or `isLoading` state and become `disabled` while the network request is in flight.
- [ ] **Idempotency Check (Payments/Critical):** For checkout or account creation forms, verify the backend generates an idempotency key (e.g., Stripe `idempotencyKey`) or checks for existing records before creating a new one.

## 🛠️ Remediation & Auto-Fix Steps
If forms are vulnerable to bad inputs or double-clicks, execute the following fixes:

1. **Implement Schema Validation:** 
   - Generate a Zod schema for the form data.
   - Wrap the form in a validation library (e.g., `react-hook-form` with `@hookform/resolvers/zod`).
2. **Add Submission State Management:** 
   - Update the form's `onSubmit` handler to set an `isSubmitting` state to `true` immediately.
   - Pass this state to the submit button: `<button type="submit" disabled={isSubmitting}>`.
   - Add a loading spinner inside the button while `isSubmitting` is true.
3. **Render Inline Errors:** 
   - Ensure the form UI maps validation errors to the specific input fields and displays them directly below the input in a readable color (e.g., red text).
4. **Secure the Backend:** 
   - Update the corresponding API route or Server Action to parse and validate the incoming `request.body` or `formData` using the exact same Zod schema before touching the database.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Comprehensive Form Hardening**
> "Add proper validation to every form in my app: required fields, email format check, and helpful inline error messages. Disable the submit button while a submission is running so double-clicks can't create duplicates. Use Zod and React Hook Form (or my current stack)."

**Prompt 2: Fix Double-Submit & Duplicate Charges**
> "I'm worried about users double-clicking the checkout or signup button. Refactor my form submission logic to disable the button immediately on click, show a loading state, and ensure the backend uses an idempotency key (or checks for existing records) to prevent duplicate database entries or Stripe charges."

**Prompt 3: Server-Side Validation Check**
> "Audit my API routes and Server Actions that handle form submissions. Ensure they are not just trusting the client-side validation. Add strict server-side validation using Zod to reject empty submits, wrong data types, and malicious inputs before they hit the database."