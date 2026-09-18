# Phishing Email Detection & Awareness System

**Future Interns -- Cyber Security Task 2 (2026)**

## Overview

This project documents a safe, static analysis of a publicly sourced
phishing email sample. The objective is to identify phishing indicators,
analyze sender and authentication information, extract suspicious
destinations without visiting them, classify risk, and produce practical
phishing-awareness guidance.

> **Safety:** The original `.eml` sample is kept out of the public
> repository. Suspicious URLs and email addresses are defanged or
> sanitized where appropriate. No phishing infrastructure was contacted
> during analysis.

## Objectives

-   Analyze a phishing email sample.
-   Inspect email headers and sender identity.
-   Review SPF, DKIM, and DMARC results.
-   Identify social-engineering techniques.
-   Extract and safely document suspicious URLs and `mailto:`
    destinations.
-   Classify the message by risk and confidence.
-   Produce user-awareness and SOC prevention recommendations.

## Sample

-   **Sample:** `sample-01 / sample-10.eml`
-   **Source:** `rf-peixoto/phishing_pot` public honeypot collection
-   **Message theme:** Microsoft account unusual sign-in alert
-   **SHA-256:**
    `4fbf4c3d80aba156c59004c12c83ff53dd64c9cf7b7a6029e98fe1da0760783a`
-   **Analysis:** Static/local only

## Key Findings

  Indicator                       Evidence                               Severity
  ------------------------------- -------------------------------------- ----------
  Brand impersonation             Microsoft account team                 High
  From-domain mismatch            `access-accsecurity.com`               Critical
  Reply-To mismatch               `sotrecognizd@gmail[.]com`             Critical
  Return-Path mismatch            `thcultarfdes.co.uk`                   High
  Authentication anomaly          SPF none, DKIM none, DMARC permerror   High
  Urgency/fear                    Unusual sign-in, Russia/Moscow         High
  Suspicious action destination   Report The User → Gmail                Critical
  External tracking resource      `thebandalisty[.]com`                  Medium

## Analysis Workflow

``` text
Collect
   ↓
Preserve + SHA-256 hash
   ↓
Inspect headers
   ↓
Analyze SPF/DKIM/DMARC
   ↓
Extract URLs and mailto destinations
   ↓
Analyze social-engineering indicators
   ↓
Correlate evidence
   ↓
Risk classification
   ↓
Awareness + SOC recommendations
```

## Tools

-   Kali GNU/Linux
-   `grep`
-   `sed`
-   `sort`
-   `head`
-   `cat`
-   `sha256sum`
-   Local text-based evidence files

## Repository Structure

``` text
Task-2-Phishing/
├── README.md
├── report/
│   ├── Future-Interns-Task-2-Phishing-Detection-Awareness-Report.pdf
│   └── Future-Interns-Task-2-Phishing-Detection-Awareness-Report.md
├── analysis/
│   ├── sample-01-indicator-matrix.txt
│   └── sample-01-risk-assessment.txt
├── evidence/
│   ├── sample-01-key-headers.txt
│   ├── sample-01-key-headers-clean.txt
│   ├── sample-01-authentication.txt
│   ├── sample-01-authentication-full.txt
│   ├── sample-01-urls.txt
│   ├── sample-01-mailto.txt
│   ├── sample-01-all-links.txt
│   └── sample-01-body-indicators.txt
├── awareness/
│   └── phishing-awareness.md
└── samples/
    └── sample-01/
        └── README.md
```

## Main Evidence

### Sender identity

``` text
Display name: Microsoft account team
From: no-reply@access-accsecurity.com
Reply-To: sotrecognizd@gmail[.]com
Return-Path: bounce@thcultarfdes.co.uk
```

### Authentication

``` text
SPF: none
DKIM: none
DMARC: permerror
```

### Important IP distinction

The message contains two different IP addresses:

-   `89.144.44.2` --- identified by the email headers as the sender IP.
-   `103.225.77.255` --- presented inside the email as the alleged
    suspicious-login IP.

The second IP is not treated as the sender or attacker IP without
independent evidence.

## Risk Assessment

**Classification:** PHISHING\
**Confidence:** HIGH\
**Overall Risk:** HIGH

The classification is based on multiple independent indicators rather
than a single header or URL.

## Awareness Guidance

### Do

-   Inspect the complete sender address.
-   Check Reply-To and actual link destinations.
-   Verify account alerts through the official service directly.
-   Report suspicious messages through the approved reporting channel.
-   Preserve suspicious emails for security analysis.

### Don't

-   Do not reply to suspicious messages.
-   Do not click suspicious links.
-   Do not enter passwords or OTPs after following an email link.
-   Do not trust logos or display names as proof of authenticity.
-   Do not re-host live phishing URLs.

## Safety and Ethics

This repository intentionally avoids publishing the original phishing
email and avoids active interaction with suspicious infrastructure.

All suspicious URLs in public-facing evidence should be:

-   Defanged with `hxxp://` instead of `http://`.
-   Defanged with `[.]` instead of `.`, where appropriate.
-   Redacted if the URL contains a unique tracking token.
-   Documented as indicators rather than opened.

## Evidence Screenshots

Recommended screenshots are listed in
`evidence/SCREENSHOT-CHECKLIST.md`.

Screenshots should show **your own Kali terminal and local analysis**,
not screenshots copied from unrelated websites.This preserves evidence
provenance and makes the project more credible.

## Limitations

This project performs static analysis only. It does not claim that an
extracted domain or IP is currently malicious, that the infrastructure
is still active, or that a victim interacted with the message.

## Conclusion

The analyzed message uses Microsoft impersonation, sender-identity
mismatches, authentication anomalies, urgency, and a misleading Gmail
action destination. These independent indicators support a
**high-confidence, high-risk phishing classification**.

## References

-   Future Interns -- Cyber Security Task 2 (2026)
-   `rf-peixoto/phishing_pot` -- public phishing honeypot sample
    collection
