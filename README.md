# 🛡️ Pre-Launch Audit Skills (37 Production Checks)

> **A battle-tested collection of 37 AI Agent Skills and Pre-Launch Audit Checklists for SaaS, web apps, and digital products.**

Ensure your web application is secure, fast, discoverable, compliant, and rock-solid before launching to production.

---

## 📂 Repository Structure

```
AuditSkills/
├── skills/          # 37 Detailed AI Agent Skill Modules (Protocols, Fixes, & Trigger Prompts)
├── checklists/      # 37 Actionable Pre-Launch Checklists (Snippets & Pitfalls)
├── AuditSummary.md  # Complete 37 Pre-Launch Audit Framework & Priority Overview
├── .gitignore       # Standard gitignore for web & development projects
└── README.md        # Documentation and master index
```

---

## 📋 The 37 Pre-Launch Checks Overview

The audit is organized into **7 core domains** with priority ratings:
- 🔴 **Launch Blocker:** Must be fixed before any public launch.
- 🟡 **First Week:** Must be completed within the first 7 days of launch.
- 🟢 **Nice to Have:** High-value optimizations and polish.

---

### 1. 🛡️ Security (6 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 01 | 🔴 | **Database Row-Level Security (RLS)** | [Checklist](checklists/rls-security-checklist.md) | [01-database-row-level-security-rls.md](skills/01-database-row-level-security-rls.md) |
| 02 | 🔴 | **Server-Side Auth & Paywall Enforcement** | [Checklist](checklists/client-side-protection-checklist.md) | [02-server-side-authentication-paywall.md](skills/02-server-side-authentication-paywall.md) |
| 03 | 🔴 | **Prevent `.env` & Config File Exposure** | [Checklist](checklists/env-file-exposure-checklist.md) | [03-prevent-env-config-file-exposure.md](skills/03-prevent-env-config-file-exposure.md) |
| 04 | 🔴 | **Prevent Frontend Secret Key Exposure** | [Checklist](checklists/remove-secrets-from-frontend-checklist.md) | [04-prevent-frontend-secret-key-exposure.md](skills/04-prevent-frontend-secret-key-exposure.md) |
| 05 | 🟡 | **HTTPS Enforcement & Canonical Domain** | [Checklist](checklists/url-canonicalization-checklist.md) | [05-https-enforcement-canonical-domain.md](skills/05-https-enforcement-canonical-domain.md) |
| 06 | 🟡 | **Rate-Limit Expensive & AI Endpoints** | [Checklist](checklists/rate-limit-ai-endpoints-checklist.md) | [06-rate-limit-expensive-endpoints.md](skills/06-rate-limit-expensive-endpoints.md) |

---

### 2. 📧 Emails & Deliverability (5 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 07 | 🔴 | **Email Authentication (SPF, DKIM, DMARC)** | [Checklist](checklists/spf-dkim-dmarc-checklist.md) | [07-email-authentication-spf-dkim-dmarc.md](skills/07-email-authentication-spf-dkim-dmarc.md) |
| 08 | 🔴 | **Essential Transactional Email Flows** | [Checklist](checklists/transactional-emails-checklist.md) | [08-essential-transactional-email-flows.md](skills/08-essential-transactional-email-flows.md) |
| 09 | 🔴 | **Cross-Provider Email Deliverability** | [Checklist](checklists/email-deliverability-checklist.md) | [09-cross-provider-email-deliverability.md](skills/09-cross-provider-email-deliverability.md) |
| 10 | 🔴 | **Email Subdomain Isolation** | [Checklist](checklists/email-subdomain-isolation-checklist.md) | [10-email-sending-domain-isolation.md](skills/10-email-sending-domain-isolation.md) |
| 11 | 🟢 | **Mail-Tester Validation (Score 9+)** | [Checklist](checklists/mail-tester-score-checklist.md) | [11-mail-tester-email-validation.md](skills/11-mail-tester-email-validation.md) |

---

### 3. 🔍 Findability / SEO (7 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 12 | 🔴 | **Open Graph (OG) & Social Preview Metadata** | [Checklist](checklists/og-image-preview-checklist.md) | [12-open-graph-social-preview-metadata.md](skills/12-open-graph-social-preview-metadata.md) |
| 13 | 🟡 | **Sitemap & Google Search Console** | [Checklist](checklists/sitemap-google-search-console-checklist.md) | [13-sitemap-google-search-console.md](skills/13-sitemap-google-search-console.md) |
| 14 | 🟡 | **Prevent Accidental Noindex Blocking** | [Checklist](checklists/google-indexing-checklist.md) | [14-prevent-accidental-noindex-blocking.md](skills/14-prevent-accidental-noindex-blocking.md) |
| 15 | 🟡 | **Unique Page Titles & Meta Descriptions** | [Checklist](checklists/page-titles-descriptions-checklist.md) | [15-unique-page-titles-meta-descriptions.md](skills/15-unique-page-titles-meta-descriptions.md) |
| 16 | 🟡 | **Remove Localhost & Staging Leakage** | [Checklist](checklists/remove-localhost-staging-checklist.md) | [16-remove-localhost-staging-leakage.md](skills/16-remove-localhost-staging-leakage.md) |
| 17 | 🟢 | **Marketing & App Domain Separation** | [Checklist](checklists/split-app-landing-page-checklist.md) | [17-marketing-app-domain-separation.md](skills/17-marketing-app-domain-separation.md) |
| 18 | 🟢 | **Robots.txt & LLMs.txt Configuration** | [Checklist](checklists/robots-txt-checklist.md) | [18-robots-txt-llms-txt-configuration.md](skills/18-robots-txt-llms-txt-configuration.md) |

---

### 4. ⚡ Speed & Performance (4 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 19 | 🔴 | **PageSpeed Insights & Performance Budget** | [Checklist](checklists/pagespeed-insights-checklist.md) | [19-pagespeed-insights-performance-budget.md](skills/19-pagespeed-insights-performance-budget.md) |
| 20 | 🟡 | **Image Compression & WebP Optimization** | [Checklist](checklists/compress-images-squoosh-checklist.md) | [20-image-compression-webp-optimization.md](skills/20-image-compression-webp-optimization.md) |
| 21 | 🟡 | **Fix Layout Shift (CLS)** | [Checklist](checklists/fix-layout-shift-checklist.md) | [21-fix-layout-shift-cls.md](skills/21-fix-layout-shift-cls.md) |
| 22 | 🟢 | **Remove Dependency & Script Bloat** | [Checklist](checklists/remove-unused-libraries-checklist.md) | [22-remove-unused-scripts-dependency-bloat.md](skills/22-remove-unused-scripts-dependency-bloat.md) |

---

### 5. 📊 Analytics & Monitoring (6 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 23 | 🔴 | **Analytics Installation & Firing Check** | [Checklist](checklists/analytics-before-launch-checklist.md) | [23-analytics-installation-firing-verification.md](skills/23-analytics-installation-firing-verification.md) |
| 24 | 🟡 | **Core Web Vitals Real User Monitoring** | [Checklist](checklists/track-web-vitals-checklist.md) | [24-core-web-vitals-rum-tracking.md](skills/24-core-web-vitals-rum-tracking.md) |
| 25 | 🟡 | **Invisible Bot Protection (Turnstile)** | [Checklist](checklists/bot-protection-checklist.md) | [25-invisible-bot-protection-turnstile.md](skills/25-invisible-bot-protection-turnstile.md) |
| 26 | 🟡 | **Core Conversion Funnel Tracking** | [Checklist](checklists/conversion-funnel-checklist.md) | [26-core-conversion-funnel-instrumentation.md](skills/26-core-conversion-funnel-instrumentation.md) |
| 27 | 🟡 | **Error Tracking & Sentry Integration** | [Checklist](checklists/error-tracking-checklist.md) | [27-error-tracking-sentry.md](skills/27-error-tracking-sentry.md) |
| 28 | 🟢 | **Session Recordings & Consent Management** | [Checklist](checklists/session-recordings-checklist.md) | [28-session-recordings-consent-management.md](skills/28-session-recordings-consent-management.md) |

---

### 6. ⚖️ Legal & Compliance (3 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 29 | 🔴 | **Legal Pages (Terms of Service & Privacy)** | [Checklist](checklists/terms-privacy-policy-checklist.md) | [29-legal-pages-terms-privacy-policy.md](skills/29-legal-pages-terms-privacy-policy.md) |
| 30 | 🟡 | **Merchant of Record & Tax Compliance** | [Checklist](checklists/merchant-of-record-checklist.md) | [30-merchant-of-record-tax-compliance.md](skills/30-merchant-of-record-tax-compliance.md) |
| 31 | 🟡 | **Cookie Consent Banner & Compliance** | [Checklist](checklists/cookie-consent-banner-checklist.md) | [31-cookie-consent-banner-compliance.md](skills/31-cookie-consent-banner-compliance.md) |

---

### 7. 🧪 Final Manual Testing (6 Checks)

| # | Priority | Check / Skill | Checklist | Skill Module |
|---|:---:|---|---|---|
| 32 | 🔴 | **Live Payment Flow & Webhooks** | [Checklist](checklists/test-payment-flow-checklist.md) | [32-live-payment-flow-webhook-verification.md](skills/32-live-payment-flow-webhook-verification.md) |
| 33 | 🔴 | **Cross-Browser & Cross-Device Testing** | [Checklist](checklists/cross-browser-testing-checklist.md) | [33-cross-browser-device-compatibility.md](skills/33-cross-browser-device-compatibility.md) |
| 34 | 🔴 | **Mobile & Incognito User Journey** | [Checklist](checklists/end-to-end-user-journey-checklist.md) | [34-core-flow-mobile-incognito-testing.md](skills/34-core-flow-mobile-incognito-testing.md) |
| 35 | 🟡 | **Dead Links & Broken Buttons Audit** | [Checklist](checklists/dead-links-checklist.md) | [35-dead-link-button-functionality-audit.md](skills/35-dead-link-button-functionality-audit.md) |
| 36 | 🟡 | **Form Validation & Double-Submit Protection**| [Checklist](checklists/break-your-forms-checklist.md) | [36-form-validation-double-submit-prevention.md](skills/36-form-validation-double-submit-prevention.md) |
| 37 | 🟢 | **Custom 404 Page & Status Code** | [Checklist](checklists/custom-404-page-checklist.md) | [37-custom-404-page-http-status.md](skills/37-custom-404-page-http-status.md) |

---

## 🚀 How to Use with AI Coding Assistants

Each skill in `skills/` contains:
1. **Objective & Threat Context** (why this fails in production)
2. **Non-Negotiable Critical Rules**
3. **Audit Protocol** (step-by-step checklist)
4. **Remediation & Auto-Fix Steps**
5. **Ready-to-Use User Prompts**

### In Cursor / Claude / Antigravity / Windsurf:
- **Direct Prompt:** Copy and paste the ready-to-use prompt from any skill file into your AI chat.
- **Rules / Skills integration:** Reference the skill module path (e.g. `@skills/01-database-row-level-security-rls.md`) to run an automated audit on your codebase.

---

## 🔗 Credits & Source
Derived from the 37 Pre-Launch Checks framework by **Nico Burkart**.
