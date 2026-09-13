# Phishing Awareness Guide

## How to Recognize a Phishing Email

Phishing emails are designed to make the recipient trust a fake message and take an unsafe action. Attackers commonly impersonate trusted organizations, create urgency, and direct victims toward suspicious destinations.

### 1. Check the Complete Sender Address

Do not trust the display name alone.

In the analyzed sample, the display name claims:

`Microsoft account team`

However, the actual sender uses:

`no-reply@access-accsecurity.com`

A legitimate-looking display name does not prove that the email was sent by the claimed organization.

### 2. Check the Reply-To Address

The analyzed message contains:

`sotrecognizd@gmail[.]com`

as its Reply-To destination.

A Microsoft security notification directing communication to an unrelated Gmail address is a major warning sign.

### 3. Be Suspicious of Urgency and Fear

Phishing emails often try to make users act before they have time to verify the message.

Common examples include:

* Unusual sign-in
* Suspicious activity
* Account will be locked
* Verify immediately
* Security alert
* Unauthorized login

The analyzed sample claims that a new sign-in occurred from Russia/Moscow and encourages the recipient to report the activity.

### 4. Check Link Destinations

Do not assume that a button or link goes where its text claims.

The analyzed email contains an action labelled:

`Report The User`

but its destination is an unrelated Gmail address.

It also contains an external HTTP tracking resource:

`hxxp://thebandalisty[.]com/track/[REDACTED]`

Suspicious destinations should never be opened just to investigate them.

### 5. Verify Security Alerts Independently

If an email claims that an account has been compromised:

1. Do not click the email's link.
2. Open the organization's official website or application directly.
3. Sign in through the normal trusted route.
4. Check the account's security/activity page.
5. Report the suspicious email through the approved reporting process.

### 6. Do Not Trust Branding Alone

Attackers can copy:

* Logos
* Colors
* Fonts
* Security-alert layouts
* Company names
* Email signatures

Technical sender information and destination addresses are more useful for verification than appearance alone.

---

## Employee Do's

* Inspect the complete sender address.
* Check the Reply-To address.
* Inspect link destinations before clicking.
* Be cautious about urgent security messages.
* Verify account alerts independently.
* Report suspicious emails to the security team.
* Preserve suspicious messages when requested for investigation.
* Use multi-factor authentication where available.

## Employee Don'ts

* Do not reply to suspicious emails.
* Do not click suspicious links.
* Do not enter passwords through an email link.
* Do not provide OTPs or authentication codes.
* Do not download unexpected attachments.
* Do not trust a display name without checking the address.
* Do not forward live phishing URLs unnecessarily.

---

## What to Do If You Clicked a Phishing Link

If you accidentally interacted with a suspicious message:

1. Stop entering information immediately.
2. Close the suspicious page.
3. Report the incident to the organization's security team.
4. If credentials were entered, change the password through the official website.
5. Revoke or terminate suspicious sessions if the service provides that option.
6. Inform the security team about what happened.
7. Follow the organization's incident-response procedure.

---

## SOC / Organization Recommendations

Organizations can reduce phishing risk by implementing:

* SPF, DKIM and DMARC.
* DMARC monitoring and enforcement.
* Secure email gateways.
* Sender and Reply-To mismatch detection.
* Lookalike-domain detection.
* URL reputation and sandboxing.
* External sender warnings.
* Employee security-awareness training.
* Easy phishing-reporting mechanisms.
* SIEM correlation and alerting.
* Quarantine and blocking of confirmed malicious indicators.

---

## Key Lesson From Sample-01

The analyzed message demonstrates a common phishing pattern:

**Trusted brand → Fear/urgency → Requested action → Suspicious destination**

The strongest warning signs were the mismatch between the claimed Microsoft identity and the actual technical sender/destination information.

When an email creates urgency, **slow down and verify through an independent trusted channel**.
