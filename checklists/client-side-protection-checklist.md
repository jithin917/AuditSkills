# Client-side-only protection can be bypassed

> **What to check**
>
> Your protection actually protects. If your app only hides the premium features in the browser, anyone who opens developer tools gets them for free.

---

## Real Example

An app called **Enrichlead** had its paywall bypassed publicly. The "is this user paying?" check only existed in the browser/client, so people just skipped it.

---

## How to check it

### Option 1: Claude Code (built-in)
If you use **Claude Code**, type `/security-review`. It's built in, nothing to install, and client-side-only auth is one of the things it looks for.

### Option 2: Paste this into your AI tool

```
Check my app for client-side-only protection. For every premium feature and every logged-in-only page: is the check enforced on the server (API route, database rule, or middleware), or only in the frontend? Flag anything where a user could access data or features by calling the API directly, without the UI.
```

---

## How to fix it

```
For every API route and database function that returns user data or premium features: add a server-side check of the logged-in user and their plan before returning anything. Keep the frontend checks, but treat them as UX, not security.
```

### The clean setup

Authentication with **Clerk**, and every backend function checks who's calling (in Convex that's `ctx.auth`).

This skill sets up Convex auth with Clerk included:

```bash
npx skills add get-convex/agent-skills --skill convex-setup-auth
```

---

## What bad looks like

The AI finds an API route that returns premium data without checking who's asking. 

**Hiding a button does nothing.** The API behind it on your **BACKEND** has to say no too.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
