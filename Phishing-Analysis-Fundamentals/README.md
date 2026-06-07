# TryHackMe — Phishing Emails 1

**Room:** [Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe)  
**Difficulty:** Easy  
**Category:** SOC Level 1 / Phishing Analysis  
**Status:**  Completed

---

## Overview

This room covers the fundamentals of email structure and phishing analysis. Topics include:

- Anatomy of an email address
- Email delivery protocols (SMTP, DNS, IMAP/POP3)
- Reading email headers
- Analyzing email body and attachments
- Identifying phishing techniques
- Business Email Compromise (BEC)

---

## Task 1 — Introduction

No questions. Read the introduction and proceed.

---

## Task 2 — The Email Address

### Concepts

An email address is made up of three components:

| Part | Component | Example |
|---|---|---|
| 1 | Username | `david` |
| 2 | @ Symbol | `@` |
| 3 | Domain Name | `tryhackme.com` |

**Analogy:**
- The **domain** = the street or apartment building
- The **username** = the specific mailbox within that building

### Question

> Identify the domain used in the following email address: `hatsalesman@tryhatme.com`

<details>
<summary>Answer</summary>

```
tryhatme.com
```

</details>

---

## Task 3 — Email Delivery

### Concepts

Email delivery involves several protocols working together:

| Protocol | Role |
|---|---|
| **SMTP** | Sends email from client to mail server |
| **DNS** | Looks up the recipient domain's mail server (MX record) |
| **IMAP** | Retrieves email; syncs across multiple devices |
| **POP3** | Retrieves email; downloads to one device only |

### Questions

> Which protocol is responsible for sending an email from a client to a mail server?

<details>
<summary>Answer</summary>

```
SMTP
```

</details>

---

> Which service is used to look up the recipient domain's mail server?

<details>
<summary>Answer</summary>

```
DNS
```

</details>

---

> Bob wants to access his email from multiple devices, including his phone and laptop. Which protocol should he use?

<details>
<summary>Answer</summary>

```
IMAP
```

</details>

---

## Task 4 — Email Header

### Concepts

Email headers contain metadata about a message, including:

- **Received:** — Shows the path the email took, including originating IP
- **From / To / Subject** — Basic sender/recipient info
- **DKIM-Signature** — Cryptographic signature for email authentication
- **X-Originating-IP** — The IP address of the sender's machine
- **Reply-To** — Where replies are directed (may differ from `From`)

> ⚠️ The `Reply-To` field is commonly abused in phishing — attackers set it to redirect replies to a different address than the displayed sender.

### Questions

> What is the full subject line of `email1.eml`?

<details>
<summary>Answer</summary>

```
Help protect your budget by protecting your home
```

</details>

---

> View the message source of `email1.eml` using Thunderbird in your VM. What is the IP address listed as the `X-Originating-Ip`?

<details>
<summary>Answer</summary>

```
43.255.56.161
```

</details>

---

## Task 5 — Email Body

### Concepts

Email bodies can contain:

- **Plain text or HTML** — HTML emails can hide malicious links
- **Attachments** — Encoded in Base64 within the raw email source
- **Content-Type header** — Describes the type of content/attachment

Common `Content-Type` values seen in phishing:

| Content-Type | Description |
|---|---|
| `application/pdf` | PDF file |
| `application/zip` | ZIP archive |
| `application/octet-stream` | Generic binary |
| `text/html` | HTML content |

### Questions

> Open up the `email2.txt` file to view the source of an attachment. What is the `Content-Type` of the attachment?

<details>
<summary>Answer</summary>

```
application/pdf
```

</details>

---

> What is the name of the attachment from the previous question?

<details>
<summary>Answer</summary>

```
zmqpalgh.pdf
```

</details>

---

> Decode the base64 string using either a PDF converter or CyberChef. What is the hidden flag value?

<details>
<summary>Answer</summary>

```
THM{BENIGN_PDF_ATTACHMENT}
```

**Method:** Copy the Base64 string from the raw email source → paste into [CyberChef](https://gchq.github.io/CyberChef/) → use **From Base64** operation → inspect the decoded PDF content for the flag.

</details>

---

## Task 6 — Types of Phishing

### Concepts

Common phishing categories:

| Type | Description |
|---|---|
| **Spear Phishing** | Targeted attack against a specific individual or organization |
| **Whaling** | Spear phishing aimed at executives (C-suite) |
| **Smishing** | Phishing via SMS |
| **Vishing** | Phishing via voice/phone call |
| **Clone Phishing** | Legitimate email cloned and modified with malicious content |

### Investigation — `email3.eml`

Analyze the phishing email in your VM. Key indicators to look for:

- Spoofed brand in the `From` display name
- Mismatched sender domain
- Suspicious `X-Originating-IP`
- `Authentication-Results` header for server attribution

### Questions

> Which reputable organization is being spoofed in this phishing attempt?

<details>
<summary>Answer</summary>

```
Home Depot
```

</details>

---

> What is the sender's email address?

<details>
<summary>Answer</summary>

```
support@teckbe.com
```

> Note: The domain `teckbe.com` is NOT affiliated with Home Depot — classic sender spoofing.

</details>

---

> Inspect the email message source. What is the defanged `X-Originating-IP`?

<details>
<summary>Answer</summary>

```
103[.]234[.]236[.]83
```

> **Defanging** replaces `.` with `[.]` to make IPs/URLs safe to share without accidentally creating clickable links.

</details>

---

> Continue analyzing the email message source. Which mail server generated the `Authentication-Results` header?

<details>
<summary>Answer</summary>

```
atlas102.free.mail.gq1.yahoo.com
```

</details>

---

## Task 7 — Conclusion

### Summary

In this room we covered:

1. Email address anatomy (username @ domain)
2. Delivery protocols — SMTP sends, DNS routes, IMAP/POP3 retrieves
3. Reading raw email headers for investigation
4. Analysing email body HTML and Base64 attachments
5. Identifying phishing techniques and spoofed brands

### Business Email Compromise (BEC)

> BEC is an attack where an adversary gains access to a **legitimate internal email account** and uses it to trick employees into performing unauthorized or fraudulent actions (e.g. wire transfers, credential disclosure).

Unlike standard phishing, BEC emails come from **real** company addresses, making them harder to detect.

### Question

> What attack, signified by the acronym BEC, uses a compromised email to trick employees into fraud?

<details>
<summary>Answer</summary>

```
Business Email Compromise
```

</details>

---

## Answer Summary

| Task | Question | Answer |
|---|---|---|
| 2 | Domain of `hatsalesman@tryhatme.com` | `tryhatme.com` |
| 3 | Protocol: client → mail server | `SMTP` |
| 3 | Service for MX lookup | `DNS` |
| 3 | Protocol for multi-device access | `IMAP` |
| 4 | Subject line of `email1.eml` | `Help protect your budget by protecting your home` |
| 4 | `X-Originating-Ip` in `email1.eml` | `43.255.56.161` |
| 5 | `Content-Type` of attachment in `email2.txt` | `application/pdf` |
| 5 | Attachment filename | `zmqpalgh.pdf` |
| 5 | Hidden flag | `THM{BENIGN_PDF_ATTACHMENT}` |
| 6 | Spoofed organization | `Home Depot` |
| 6 | Sender email address | `support@teckbe.com` |
| 6 | Defanged `X-Originating-IP` | `103[.]234[.]236[.]83` |
| 6 | Mail server in `Authentication-Results` | `atlas102.free.mail.gq1.yahoo.com` |
| 7 | Full name of BEC | `Business Email Compromise` |

