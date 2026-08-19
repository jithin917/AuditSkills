# ✉️ Skill: Mail-Tester Email Validation (Score 9+)

## 🎯 Objective
Achieve a score of 9/10 or higher on mail-tester.com by systematically identifying and fixing email deliverability issues, including missing authentication records, blacklisted IPs, broken links, and content problems that other checks might have missed.

## 🧠 Context & "Why It Matters"
- **The Threat:** Even if you've configured SPF, DKIM, and DMARC, there are dozens of other subtle factors (content structure, link validity, IP reputation, HTML formatting) that can tank your email deliverability.
- **Real-world consequence:** A 5/10 score with issues like "missing DMARC," "blacklisted IP," "broken links," or "image-only content" means your emails are being flagged as spam, and you won't know until users complain.
- **The Rule:** It's a free 2-minute second opinion on your whole email setup, and it lists exactly what to fix. Don't guess—get the objective score.

## 🚨 Critical Rules (Non-Negotiable)
1. **NEVER** launch your app's email system without achieving at least a 9/10 score on mail-tester.com.
2. **NEVER** ignore warnings about blacklisted IPs or broken links—these are critical failures that must be fixed immediately.
3. **ALWAYS** re-test after making any changes to your email templates, DNS records, or sending infrastructure.

##  Audit Protocol
When triggered, guide the user through a systematic mail-tester validation:

- [ ] **Generate Test Address:** Instruct the user to visit `mail-tester.com` and copy the unique temporary email address provided.
- [ ] **Trigger Email Flow:** Have the user sign up for their own app (or trigger a password reset/receipt) using that test address.
- [ ] **Review Score:** Instruct the user to click "Check your score" and document the exact score (target: 9/10 or higher).
- [ ] **Analyze Failures:** If the score is below 9, systematically review the detailed report for:
  - Missing or misconfigured SPF/DKIM/DMARC
  - Blacklisted IP addresses or domains
  - Broken links or invalid URLs in email content
  - Poor HTML structure or image-only content
  - Missing unsubscribe headers (for marketing emails)
  - Spammy content keywords
- [ ] **Cross-Reference:** Map each failure back to the relevant skills (e.g., missing DMARC → Skill #07, wrong domain → Skill #10).

## 🛠️ Remediation & Auto-Fix Steps
If the score is below 9/10, execute targeted fixes based on the mail-tester report:

1. **Missing Authentication Records:** 
   - If SPF/DKIM/DMARC are flagged, refer to Skill #07 and generate the exact DNS TXT records needed.
2. **Blacklisted IP/Domain:** 
   - Alert the user: "Your sending IP or domain is on a blacklist." Provide instructions to check `mxtoolbox.com/blacklists.aspx` and request delisting.
3. **Broken Links:** 
   - Scan email templates for any hardcoded URLs that might be invalid, localhost, or staging links. Replace with production environment variables.
4. **Content Issues:** 
   - If flagged for "image-only content" or "spammy keywords," refactor the email template to include more text-to-image ratio and remove trigger words.
5. **Missing Headers:** 
   - Add required email headers (List-Unsubscribe, Reply-To, proper MIME structure) to the email sending code.
6. **Re-Test:** 
   - After fixes are applied, instruct the user to repeat the mail-tester process until they achieve 9/10 or higher.

## 💬 Ready-to-Use User Prompts
*Copy and paste one of the following into the AI chat to trigger this skill:*

**Prompt 1: Full Mail-Tester Audit Guide**
> "I need to validate my email setup. Walk me through using mail-tester.com to score my app's emails. Give me step-by-step instructions on how to trigger an email to the test address, how to interpret the results, and what to do if I score below 9/10."

**Prompt 2: Fix Mail-Tester Failures**
> "I scored [X]/10 on mail-tester.com. Here are the specific issues it found: [paste issues]. Help me fix each one. Generate the exact code changes, DNS records, or configuration updates needed to resolve these problems."

**Prompt 3: Pre-Launch Email Validation Checklist**
> "Before I launch, I want to ensure my emails won't go to spam. Create a complete checklist for me to validate my email setup using mail-tester.com, including what flows to test (signup, password reset, receipt) and what score I need to achieve on each."