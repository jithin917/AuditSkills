# Track web vitals from day one

> **What to check**
>
> You're collecting performance data from real visitors. PageSpeed Insights tells you how your site runs on Google's test machine. Web vitals tell you how it runs on your users' three-year-old Androids on the hotel wifi.

---

## How to check it

### 1. Enable web vitals in your analytics tool
**PostHog** has it built in — it's one toggle.

### 2. Verify data is flowing
Visit your site, then check that data shows up in the dashboard.

### 3. Watch three numbers

| Metric | Target | What it measures |
|--------|--------|------------------|
| **LCP** | Under 2.5 seconds | Loading |
| **INP** | Under 200 milliseconds | Responsiveness |
| **CLS** | Under 0.1 | Layout shift |

### 4. When one goes red
This skill tells you what to actually change:

```bash
npx skills add addyosmani/web-quality-skills --skill core-web-vitals
```

---

## What bad looks like

Users leave because the app feels slow, and nobody tells you. Or you want performance data in week three and have to start collecting from zero.

---

## Why it matters

The data only collects while the toggle is on. Turn it on before launch and you have a baseline from day one.

---

*Source: Nico Burkart's Security Checklist for AI-Built Apps*
