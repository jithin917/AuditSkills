# Turn on RLS so your database isn't publicly readable

> **What to check**
>
> A stranger with your app's URL can't read or write your database. This is the #1 way AI-built apps get hacked: the AI creates the tables but never locks them down.

---

## Real Example

One app leaked **1.5 million API keys** because Row Level Security was never turned on. A single flaw in Lovable-built apps exposed data across **170 production apps**.

---

## How to check it (simple version)

Paste this into your AI tool (Cursor, Lovable, Claude):

```
Check if my database is protected from public access. If I use Supabase: is Row Level Security (RLS) enabled on EVERY table with user data, and does each table have policies so users can only read/write their own rows? If I use Firebase: are my security rules locked down, or world-readable? Show me exactly which tables/collections are unprotected.
```

If you use **Convex**: your security lives in your functions. Ask your AI to check that every query and mutation verifies the logged-in user with `ctx.auth`.

> I build all my apps with Convex for this reason. Because the security lives in your code → easier for AI to read.

---

## How to fix it

### 1. Supabase users, paste this:

```jsx
Enable Row Level Security on every table with user data, and write policies so users can only read and write their own rows. Then test each policy by querying as an anonymous user and as a second test user.
```

### 2. Starting fresh or rebuilding?

I use **Convex**, because every read and write goes through a function in your code, and AI can read and fix your security like any other file.

This skill sets it up:

```bash
npx skills add get-convex/agent-skills --skill convex-quickstart
```

---

## What bad looks like

The AI answers: **"RLS is not enabled on table X."**

That means anyone can read every row in it. **Today.**

---

## Why it matters

If one table is unprotected, anyone can read your data on day one.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
