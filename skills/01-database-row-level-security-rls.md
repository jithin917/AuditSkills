# 🛡️ Skill: Database Row-Level Security (RLS) & Access Control

## 🎯 Objective
Guarantee that the application's database is completely protected from public/unauthenticated access. Prevent the #1 vulnerability in AI-generated apps: creating database tables without locking them down, which leads to catastrophic data leaks.

## 🧠 Context & "Why It Matters"
- **The Threat:** AI coding tools frequently create tables but forget to enable Row Level Security (RLS) or write security rules. 
- **Real-world consequence:** A single flaw in AI-built apps has previously exposed data across hundreds of production apps, including one that leaked 1.5 million API keys because RLS was never turned on.
- **The Rule:** If one table is unprotected, anyone can read your data on day one.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** create a new table/collection containing user or sensitive data without immediately applying access controls.
2. **NEVER** default to "world-readable" or "world-writable" for any table unless it is explicitly public, static configuration data (and even then, restrict writes).
3. **ALWAYS** enforce that users can only read, update, or delete their *own* rows (or rows they are explicitly authorized to access).

## 🔍 Audit Protocol
When triggered, scan the codebase and database schema to verify the following based on the backend technology in use:

### If using Supabase (PostgreSQL):
- [ ] Is `ALTER TABLE ... ENABLE ROW LEVEL SECURITY;` applied to **EVERY** table with user data?
- [ ] Are there explicit policies for `SELECT`, `INSERT`, `UPDATE`, and `DELETE`?
- [ ] Do the policies correctly use `auth.uid()` to restrict access (e.g., `auth.uid() = user_id`)?

### If using Firebase (Firestore / Realtime Database):
- [ ] Are the security rules strictly locked down?
- [ ] Is there any instance of `allow read, write: if true;` on sensitive paths?
- [ ] Do rules verify `request.auth.uid` before granting access to user-specific documents?

### If using Convex:
- [ ] Does **every** query and mutation explicitly verify the logged-in user?
- [ ] Is `ctx.auth` being checked at the very beginning of the function to prevent unauthorized execution?

## 🛠️ Remediation & Auto-Fix Steps
If unprotected tables or weak rules are found, execute the following fixes:

1. **For Supabase:** 
   - Enable RLS on the exposed tables.
   - Generate and apply the exact SQL `CREATE POLICY` statements to restrict access to the resource owner.
2. **For Firebase:** 
   - Rewrite the `firestore.rules` or `database.rules.json` to require authentication and validate user IDs against document fields.
3. **For Convex:** 
   - Inject `ctx.auth` checks into the vulnerable queries/mutations. If no user is found, throw an authentication error.
4. **Verification:** 
   - Generate 2 test queries: 
     - *Test 1:* Query as an anonymous/unauthenticated user (Must fail or return empty).
     - *Test 2:* Query as an authenticated user (Must succeed and only return their own data).

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: General Audit**
> "Run the Database Security Audit. Check if my database is protected from public access. Identify my database provider (Supabase, Firebase, or Convex). If Supabase: Is RLS enabled on EVERY table with user data, and do policies restrict users to only read/write their own rows? If Firebase: Are security rules locked down or world-readable? If Convex: Does every query/mutation verify `ctx.auth`? List exactly which tables/collections are unprotected and generate the fix."

**Prompt 2: Supabase Specific Fix**
> "Enable Row Level Security on every table with user data in my Supabase project. Write policies so users can only read and write their own rows. Then, provide the SQL to test each policy by querying as an anonymous user and as a second test user to prove it works."

**Prompt 3: Convex Specific Setup**
> "I am starting fresh with Convex. Set up my database functions so that every read and write goes through a function in my code, and ensure every single query and mutation verifies the logged-in user with `ctx.auth`."