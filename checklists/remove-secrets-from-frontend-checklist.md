# Remove secret keys from your frontend

> **What to check**
>
> API keys that cost you money (OpenAI, Anthropic, Stripe, AWS) aren't in the code your browser downloads. If they are, anyone can extract them and spend on your account.

---

## How to check it (simple version)

### 1. Manual check
Open your live site, right-click, **"View page source"**

Press **Ctrl/Cmd+F** and search for: `sk-` and `sk_live`

If you find them, it's bad!

### 2. AI prompt

```
Search my codebase for API keys or secrets that end up in the frontend/client bundle. Especially: any env variable starting with NEXT_PUBLIC_, VITE_, PUBLIC_ or REACT_APP_ that contains a key, secret, token, or password. Server secrets must never use these prefixes. List everything you find.
```

### 3. Shortcut
If you use **Claude Code**, just type `/security-review`. Anthropic's built-in security audit finds leaked secrets like these automatically, plus injection risks and client-only auth.

---

## Good to know

Some keys are meant to be public:
- Stripe keys starting with `pk_live_` ✅
- Supabase "anon" key ✅

These are **never** fine in the browser:
- `sk_live_` ❌
- `sk-...` ❌

---

## How to fix it

### 1. Rotate first
Found a real secret? Rotate it first. Consider it already public — crawlers are quick.

### 2. Move it server-side

```
Move every secret key out of my frontend: put them in server-side environment variables without NEXT_PUBLIC_, VITE_ or PUBLIC_ prefixes, and route the calls that need them through a backend endpoint instead of calling the API from the browser.
```

---

## What bad looks like

`NEXT_PUBLIC_OPENAI_KEY=sk-proj-...` in your code.

**1 in 4 AI-built apps on Vercel** leaked server secrets exactly this way.

---

## Why it matters

An exposed OpenAI key means strangers spend your money. An exposed Stripe secret key means strangers touch your payments.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
