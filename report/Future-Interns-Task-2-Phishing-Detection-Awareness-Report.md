# Future Interns -- Cyber Security Task 2 (2026)

## Phishing Email Detection & Awareness Report

**Analyst:** Laxmi Sri Priya\
**Task:** Cyber Security Task 2 (2026)\
**Analysis Type:** Static phishing-email analysis\
**Sample:** Sample-01 / `sample-10.eml`\
**Classification:** PHISHING\
**Confidence:** HIGH\
**Overall Risk:** HIGH

------------------------------------------------------------------------

## 1. Executive Summary

This report documents a static analysis of a publicly sourced phishing
email sample collected by the `rf-peixoto/phishing_pot` honeypot
project. The message impersonates the Microsoft account team and claims
that an unusual sign-in occurred from Russia/Moscow.

The investigation examined the email headers, sender identity,
authentication results, reply destination, embedded links, and
social-engineering content. No embedded URL was visited and no action
was performed against the sender infrastructure.

Multiple independent indicators support a high-confidence phishing
classification:

-   Microsoft brand impersonation.
-   A non-Microsoft `From` domain: `access-accsecurity.com`.
-   A different `Reply-To` address: `sotrecognizd@gmail.com`.
-   A different `Return-Path` domain: `thcultarfdes.co.uk`.
-   SPF result of `none`.
-   DKIM result of `none`.
-   DMARC result of `permerror`.
-   Urgency and fear based on an alleged unusual sign-in from
    Russia/Moscow.
-   The "Report The User" action points to a Gmail address rather than a
    Microsoft-controlled destination.
-   An unrelated external HTTP tracking resource is embedded in the
    message.

The email is therefore classified as **HIGH-RISK PHISHING with HIGH
confidence**.

------------------------------------------------------------------------

## 2. Objective

The objectives of this task were to:

1.  Analyze a real phishing-email sample.
2.  Examine sender and message headers.
3.  Identify phishing indicators and indicators of compromise (IOCs).
4.  Inspect embedded links without visiting them.
5.  Classify the email's risk.
6.  Explain the attack in simple language.
7.  Produce practical awareness and prevention guidance.

These objectives align with the Future Interns Task 2 requirements,
which call for phishing-sample analysis, indicator identification, risk
classification, simple explanations, prevention guidance, and a public
GitHub repository with the report and methodology.

------------------------------------------------------------------------

## 3. Scope and Safety

### In scope

-   Local static analysis of the `.eml` file.
-   Header and authentication analysis.
-   Sender/domain comparison.
-   Link and `mailto:` extraction.
-   Social-engineering analysis.
-   Risk classification.
-   Awareness recommendations.

### Out of scope

-   Visiting embedded URLs.
-   Replying to the phishing address.
-   Logging into any linked service.
-   Sending test emails.
-   Exploiting the infrastructure.
-   Attempting to access accounts or systems.

### Safety handling

The external tracking URL is defanged in this report:

`hxxp://thebandalisty[.]com/track/[REDACTED]`

The working phishing sample should not be re-hosted in the public
repository. The public repository should contain sanitized evidence and
analysis instead.

------------------------------------------------------------------------

## 4. Sample Information

**Source:** `rf-peixoto/phishing_pot`, a public honeypot phishing-email
collection.

**Sample file:** `email/sample-10.eml`

**Local filename:** `samples/sample-01/sample-10.eml`

**File type:** RFC 822 mail / ASCII text with CRLF line terminators

**SHA-256:**

`4fbf4c3d80aba156c59004c12c83ff53dd64c9cf7b7a6029e98fe1da0760783a`

**Message date:** Fri, 8 Sep 2023 05:47:04 +0000

**Recipient in sample:** `phishing@pot`

The sample was analyzed as a local file. Its contents were not sent
anywhere and its embedded links were not visited.

------------------------------------------------------------------------

## 5. Analysis Methodology

The investigation followed a simple SOC-style workflow:

**Collect → Preserve → Inspect → Extract → Correlate → Classify →
Recommend**

### Tools used

-   Kali GNU/Linux
-   GNU `grep`
-   GNU `sed`
-   GNU `sort`
-   GNU `head`
-   SHA-256 hashing with `sha256sum`
-   Standard text-file inspection with `cat`
-   Local evidence files for repeatable analysis

### Evidence generated

-   Key header extraction
-   Clean key headers
-   Authentication evidence
-   Full authentication header
-   HTTP URL extraction
-   `mailto:` extraction
-   All-link extraction
-   Body indicator notes
-   Phishing indicator matrix
-   Risk assessment

------------------------------------------------------------------------

## 6. Header Analysis

### Key sender fields

  --------------------------------------------------------------------------------------------------------------
  Header                  Observed value                                                 Assessment
  ----------------------- -------------------------------------------------------------- -----------------------
  From                    `Microsoft account team ,_<no-reply@access-accsecurity.com>`   Suspicious
                                                                                         impersonation

  Reply-To                `sotrecognizd@gmail.com`                                       Critical mismatch

  Return-Path             `bounce@thcultarfdes.co.uk`                                    Domain mismatch

  Subject                 `Microsoft account unusual signin activity`                    Urgency/fear

  Date                    `Fri, 8 Sep 2023 05:47:04 +0000`                               Observed message date

  X-Sender-IP             `89.144.44.2`                                                  Header-identified
                                                                                         sender IP

  Content-Type            `text/html; charset="UTF-8"`                                   HTML email

  Message-ID              Empty value observed                                           Header anomaly
  --------------------------------------------------------------------------------------------------------------

### Sender identity comparison

The message presents itself as Microsoft, but the technical identities
do not align:

-   Display/brand identity: **Microsoft account team**
-   `From` domain: **access-accsecurity.com**
-   SMTP envelope domain: **thcultarfdes.co.uk**
-   `Reply-To`: **sotrecognizd@gmail.com**

This combination is strongly inconsistent with a legitimate Microsoft
security notification.

------------------------------------------------------------------------

## 7. Authentication Analysis

The complete `Authentication-Results` header reported:

``` text
spf=none
smtp.mailfrom=thcultarfdes.co.uk
dkim=none
header.d=none
dmarc=permerror
header.from=access-accsecurity.com
```

The accompanying SPF result stated that `thcultarfdes.co.uk` did not
designate permitted sender hosts.

### Interpretation

**SPF: none**\
No positive SPF authorization result was available for the SMTP sender
domain.

**DKIM: none**\
The message was not DKIM-signed.

**DMARC: permerror**\
DMARC processing encountered an error.

These results do not independently prove maliciousness, but combined
with the sender-domain and Reply-To mismatches they provide strong
supporting evidence.

Additional headers showed:

``` text
X-MS-Exchange-Organization-AuthAs: Anonymous
X-MS-Exchange-Organization-SCL: 5
X-Sender-IP: 89.144.44.2
```

The SCL value is treated only as supporting evidence and is not used as
the primary reason for classification.

------------------------------------------------------------------------

## 8. Link and Destination Analysis

Four unique link destinations were extracted without opening them.

### External HTTP resource

``` text
hxxp://thebandalisty[.]com/track/[REDACTED]
```

This is an unrelated external HTTP tracking resource.

### Mail destinations

The message contains three `mailto:` destinations, all using:

``` text
sotrecognizd@gmail.com
```

The most important one is associated with the **"Report The User"**
action.

This is a critical indicator because the message visually presents the
action as part of a Microsoft account security notification, while the
actual destination is an unrelated Gmail mailbox.

### Safety note

The extracted URLs were treated as indicators only. They were not
opened, requested, submitted to, or otherwise interacted with during
this analysis.

------------------------------------------------------------------------

## 9. Social Engineering Analysis

The message uses several common social-engineering techniques.

### 9.1 Brand impersonation

The email repeatedly uses Microsoft branding and the phrase "Microsoft
account team" to create trust.

### 9.2 Fear and urgency

The subject and body describe an unusual sign-in and a new device in
Russia/Moscow.

This is designed to trigger concern and encourage immediate action.

### 9.3 Specific-looking technical details

The message gives:

-   Country/region: Russia/Moscow
-   IP address: `103.225.77.255`

Technical-looking details can make a phishing email appear more
authentic.

Importantly, `103.225.77.255` is the IP **claimed by the email as the
suspicious login IP**. It is not the sender IP identified in the
headers.

### 9.4 Action pressure

The user is encouraged to select:

**"Report The User"**

The destination, however, is an unrelated Gmail address.

### 9.5 Security-notification disguise

The message also provides an unsubscribe/security-notification option
pointing to the same Gmail address, further demonstrating that the
visible Microsoft security theme does not match the underlying
destinations.

------------------------------------------------------------------------

## 10. Phishing Indicator Matrix

  -------------------------------------------------------------------------------------
  Indicator        Evidence                                Severity Why suspicious
  ---------------- -------------------------- --------------------- -------------------
  Brand            "Microsoft account team"                    High Attempts to
  impersonation                                                     establish trust

  From-domain      `access-accsecurity.com`                Critical Does not match
  mismatch                                                          claimed Microsoft
                                                                    identity

  Reply-To         `sotrecognizd@gmail.com`                Critical Unrelated Gmail
  mismatch                                                          destination

  Return-Path      `thcultarfdes.co.uk`                        High Different domain
  mismatch                                                          from visible sender

  Authentication   SPF none, DKIM none, DMARC                  High Weak/inconsistent
  anomaly          permerror                                        sender
                                                                    authentication

  Urgency/fear     "unusual sign-in",                          High Encourages
                   Russia/Moscow                                    immediate action

  Suspicious       Report action → Gmail                   Critical Destination
  action                                                            contradicts claimed
  destination                                                       brand

  External         `thebandalisty[.]com`                     Medium Unrelated external
  tracking                                                          HTTP resource
  resource                                                          

  Claimed login IP `103.225.77.255`                   Informational Only presented as
                                                                    the alleged login
                                                                    IP

  Sender IP        `89.144.44.2`                      Informational Identified by
                                                                    message headers
  -------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 11. Risk Classification

**Classification:** PHISHING

**Confidence:** HIGH

**Overall Risk:** HIGH

### Primary reasons

1.  The message impersonates Microsoft.
2.  The visible sender domain is not a Microsoft domain.
3.  The Reply-To address is an unrelated Gmail account.
4.  The Return-Path uses another unrelated domain.
5.  SPF, DKIM and DMARC results show authentication anomalies.
6.  The message uses fear and urgency around an alleged account
    compromise.
7.  The "Report The User" action points to the Gmail address.
8.  The email contains an unrelated external tracking resource.

The classification is based on multiple independent indicators rather
than any single artifact.

------------------------------------------------------------------------

## 12. How the Attack Works -- Simple Explanation

A typical recipient may see:

> "Microsoft detected an unusual sign-in from Russia."

The recipient becomes worried that their account has been compromised.

The email then presents a security action such as:

> "Report The User"

The victim may assume the button will take them to Microsoft.

However, static inspection shows that the action actually targets:

`mailto:sotrecognizd@gmail.com`

This mismatch is the central deception.

The attacker is using **trusted-brand impersonation + fear + urgency + a
misleading action destination** to influence the recipient's behavior.

------------------------------------------------------------------------

## 13. User Awareness: How to Recognize This Phishing Email

### Check the sender

Do not trust the display name alone.

A message can say:

**Microsoft account team**

while actually coming from:

`access-accsecurity.com`

Always inspect the complete sender address.

### Check Reply-To

If a Microsoft notification asks you to communicate with:

`sotrecognizd@gmail.com`

that is a major warning sign.

### Check the destination before clicking

Hover over links when possible and verify the destination.

A security action should lead to a legitimate service controlled by the
organization it claims to represent.

### Be suspicious of urgency

Messages saying:

-   unusual activity
-   account will be locked
-   verify immediately
-   suspicious login
-   urgent security action

are common social-engineering techniques.

### Verify independently

Instead of clicking an email link, open the official service directly
through a known bookmark or manually entered official address.

------------------------------------------------------------------------

## 14. Employee Do's and Don'ts

### Do

-   Verify the complete sender address.
-   Inspect Reply-To and link destinations.
-   Report suspicious emails through the organization's approved
    reporting channel.
-   Verify account alerts through the official service directly.
-   Preserve suspicious messages for security analysis.

### Don't

-   Do not reply to suspicious emails.
-   Do not click suspicious links.
-   Do not enter passwords or OTPs after following an email link.
-   Do not trust branding or logos as proof of authenticity.
-   Do not forward live phishing URLs unnecessarily.

------------------------------------------------------------------------

## 15. Recommended SOC / Organization Controls

Organizations can reduce this type of phishing through:

1.  Strong DMARC enforcement for their own domains.
2.  SPF and DKIM configuration and monitoring.
3.  Secure email gateway filtering.
4.  Detection rules for sender/Reply-To mismatches.
5.  Detection of brand impersonation and lookalike domains.
6.  URL reputation and safe-link scanning.
7.  Employee phishing-awareness training.
8.  Easy phishing-reporting mechanisms.
9.  SIEM correlation of repeated phishing indicators.
10. Quarantine and block rules for confirmed malicious infrastructure.

------------------------------------------------------------------------

## 16. Evidence Index

The following local artifacts were produced during analysis:

``` text
evidence/
├── sample-01-key-headers.txt
├── sample-01-key-headers-clean.txt
├── sample-01-authentication.txt
├── sample-01-authentication-full.txt
├── sample-01-urls.txt
├── sample-01-mailto.txt
├── sample-01-all-links.txt
└── sample-01-body-indicators.txt

analysis/
├── sample-01-indicator-matrix.txt
└── sample-01-risk-assessment.txt
```

The original `.eml` sample was preserved locally and hashed with
SHA-256.

------------------------------------------------------------------------

## 17. Limitations

This was a static analysis. No phishing URL was visited and no external
service was contacted.

The report therefore does not claim:

-   that the extracted domains are currently active;
-   that the sender IP is definitively controlled by an attacker;
-   that the claimed login IP belongs to the attacker;
-   that a victim actually clicked the message;
-   that credentials were harvested.

Those conclusions would require additional controlled
threat-intelligence or incident-response evidence.

------------------------------------------------------------------------

## 18. Conclusion

Sample-01 demonstrates a realistic phishing pattern in which a trusted
brand is combined with urgency, mismatched sender identities, weak
authentication evidence, and an unrelated action destination.

The strongest finding is the mismatch between the claimed Microsoft
identity and the actual technical destinations:

``` text
Claimed identity:
Microsoft account team

From:
no-reply@access-accsecurity.com

Reply-To:
sotrecognizd@gmail.com

Return-Path:
bounce@thcultarfdes.co.uk

Authentication:
SPF none
DKIM none
DMARC permerror
```

The message should therefore be treated as **HIGH-RISK PHISHING** with
**HIGH confidence**.

------------------------------------------------------------------------

## 19. References

-   Future Interns Cyber Security Task 2 (2026): task objectives and
    deliverables.
-   `rf-peixoto/phishing_pot`: public honeypot phishing-email sample
    source.
-   Public phishing-analysis methodology was consulted for safe static
    analysis practices.
