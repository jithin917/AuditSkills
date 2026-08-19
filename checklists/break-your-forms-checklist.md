# Try to break your forms

> **What to check**
>
> Your forms survive real users: empty submits, weird input, impatient double-clicks.

---

## How to check it

On every form (signup, contact, checkout):

1. **Submit it completely empty.** Do you get a helpful error, or a crash?
2. **Put text where a number belongs,** and a fake email like `a@b`
3. **Double-click the submit button fast.** Does it submit twice? Check if you got two emails or two entries.

---

## How to fix it

```
Add proper validation to every form in my app: required fields, email format check, helpful inline error messages. Disable the submit button while a submission is running so double-clicks can't create duplicates.
```

---

## What bad looks like

A white screen after an empty submit. Two charges after a double-click on "Pay".

---

## Why it matters

Users mash buttons and paste weird things. Build your forms for that.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
