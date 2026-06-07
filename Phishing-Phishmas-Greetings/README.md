# TryHackMe — Spotting Phishing (AOC 2025)

> **Room:** [Spotting Phishing — Advent of Cyber 2025](https://tryhackme.com/room/spottingphishing-aoc2025-r2g4f6s8l0)
> **Category:** Phishing Analysis / Email Security
> **Difficulty:** Easy
> **Status:** Completed

---

## Overview

This room is part of TryHackMe's **Advent of Cyber 2025** challenge. The task involves analysing six suspicious emails and correctly classifying each one as either **Spam** or **Phishing**, while also identifying the specific phishing signals present in each email.

### Learning Objectives
- Differentiate between **Spam** and **Phishing** emails
- Identify common phishing signals such as impersonation, spoofing, and social engineering
- Understand techniques attackers use to deceive victims (fake invoices, malicious attachments, typosquatting, etc.)

---

## Phishing Signal Glossary

| Signal | Description |
|---|---|
| **Impersonation** | Attacker pretends to be a trusted person or organisation |
| **Spoofing** | Email header/sender address is forged to appear legitimate |
| **Typosquatting/Punycodes** | Domain looks like a real one but uses subtle misspellings or special characters |
| **External Sender Domain** | Email originates from a domain outside the expected organisation |
| **Social Engineering Text** | Language designed to manipulate the recipient into taking action |
| **Sense of Urgency** | Creates pressure to act quickly without thinking |
| **Fake Invoice** | Fraudulent billing document used to trick the recipient into paying |
| **Malicious Attachment** | File attached to the email that contains or leads to malware |
| **Fake Login Page** | Link directs to a page harvesting credentials |
| **Side Channel Communication Attempt** | Tries to move conversation to another platform (e.g., WhatsApp, phone) |

---

## Email Analysis

---

### Email 1 — Invoice from Santa Claus

**Classification:** Phishing

**Analysis:**
This email poses as a legitimate invoice from "Santa Claus," which is an immediate red flag. The sender's address is forged (**Spoofing**) to appear trustworthy. The invoice itself is fabricated (**Fake Invoice**) to trick the recipient into making a payment. The email also creates pressure to pay immediately (**Sense of Urgency**), a classic phishing manipulation tactic.

**Phishing Signals Identified:**

| Signal | Detected |
|---|---|
| Spoofing | ✅ |
| Sense of Urgency | ✅ |
| Fake Invoice | ✅ |

> **Flag:** `THM{yougotnumber1-keep-it-going}`

---

### Email 2 — TBFC HR: Annual Salary Raise Approval PDF

**Classification:**  Phishing

**Analysis:**
This email impersonates the TBFC HR department (**Impersonation**), a trusted internal source, to get the recipient to open an attached PDF. The sender's identity has been spoofed (**Spoofing**) to look like it's coming from HR. The attached PDF is the payload — a **Malicious Attachment** designed to compromise the recipient's machine or steal credentials.

**Phishing Signals Identified:**

| Signal | Detected |
|---|---|
| Impersonation | ✅ |
| Spoofing | ✅ |
| Malicious Attachment | ✅ |

> **Flag:** `THM{nmumber2-was-not-tha-thard!}`

---

### Email 3 — Urgent: McSkidy VPN Access for Incident Response

**Classification:** Phishing

**Analysis:**
This email impersonates McSkidy (**Impersonation**), a known figure within the organisation, and uses an urgent incident response scenario to pressure the recipient into acting without verification. The fabricated urgency (**Sense of Urgency**) is a hallmark phishing technique. The message body contains manipulative language designed to bypass critical thinking (**Social Engineering Text**).

**Phishing Signals Identified:**

| Signal | Detected |
|---|---|
| Impersonation | ✅ |
| Social Engineering Text | ✅ |
| Sense of Urgency | ✅ |

> **Flag:** `THM{Impersonation-is-areal-thing-keepIt}`

---

### Email 4 — New Audio Message from McSkidy

**Classification:** Phishing

**Analysis:**
This email again impersonates McSkidy (**Impersonation**) but this time claims there is a new audio message waiting. The email originates from an external domain not associated with the organisation (**External Sender Domain**), which is a clear indicator it is not legitimate. The social engineering language (**Social Engineering Text**) is crafted to make the recipient curious enough to click a link.

**Phishing Signals Identified:**

| Signal | Detected |
|---|---|
| Impersonation | ✅ |
| External Sender Domain | ✅ |
| Social Engineering Text | ✅ |

> **Flag:** `THM{Get-back-SOC-mas!!}`

---

### Email 5 — Improve Your Event Logistics This SOC-mas Season

**Classification:** Spam

**Analysis:**
This email is unsolicited marketing content advertising event logistics services using the SOC-mas theme. While annoying and unwanted, it does **not** attempt to steal credentials, deliver malware, or deceive the recipient into performing a harmful action. There are no phishing signals — it is simply **Spam**.

**Phishing Signals Identified:** None

> **Flag:** `THM{It-was-just-a-sp4m!!}`

---

### Email 6 — TBFC IT: Christmas Laptop Upgrade Agreement

**Classification:** Phishing

**Analysis:**
This email impersonates the TBFC IT department (**Impersonation**), offering a Christmas laptop upgrade to entice the recipient. The sender domain uses **Typosquatting/Punycodes** — the domain appears legitimate at first glance but contains subtle differences (misspellings or special Unicode characters). The email also contains socially engineered language (**Social Engineering Text**) to convince the recipient to click a link or sign an agreement.

**Phishing Signals Identified:**

| Signal | Detected |
|---|---|
| Impersonation | ✅ |
| Typosquatting/Punycodes | ✅ |
| Social Engineering Text | ✅ |

> **Flag:** `THM{number6-is-the-last-one!-DX!}`

---

## Summary Table

| # | Email Subject | Classification | Key Signals | Flag |
|---|---|---|---|---|
| 1 | Invoice from Santa Claus | 🎣 Phishing | Spoofing, Sense of Urgency, Fake Invoice | `THM{yougotnumber1-keep-it-going}` |
| 2 | TBFC HR: Annual Salary Raise Approval PDF | 🎣 Phishing | Impersonation, Spoofing, Malicious Attachment | `THM{nmumber2-was-not-tha-thard!}` |
| 3 | Urgent: McSkidy VPN Access for Incident Response | 🎣 Phishing | Impersonation, Social Engineering Text, Sense of Urgency | `THM{Impersonation-is-areal-thing-keepIt}` |
| 4 | New Audio Message from McSkidy | 🎣 Phishing | Impersonation, External Sender Domain, Social Engineering Text | `THM{Get-back-SOC-mas!!}` |
| 5 | Improve Your Event Logistics This SOC-mas Season | 📢 Spam | — | `THM{It-was-just-a-sp4m!!}` |
| 6 | TBFC IT: Christmas Laptop Upgrade Agreement | 🎣 Phishing | Impersonation, Typosquatting/Punycodes, Social Engineering Text | `THM{number6-is-the-last-one!-DX!}` |

---

## Key Takeaways

1. **Spam ≠ Phishing.** Spam is unsolicited bulk mail. Phishing actively attempts to deceive you into harmful action (stealing credentials, delivering malware, fraudulent payments).

2. **Impersonation is everywhere.** Four out of five phishing emails in this room used impersonation — pretending to be HR, IT, or a trusted colleague. Always verify the sender independently.

3. **Multiple signals = stronger confidence.** Each phishing email had at least three identifiable signals. The more signals present, the more confident you can be in a phishing classification.

4. **Urgency is a manipulation tool.** Attackers deliberately create time pressure to stop you from thinking critically. Slow down when an email demands immediate action.

5. **Check the domain carefully.** Typosquatting and external sender domains are easy to miss at a glance. Always hover over or inspect the full sender address before clicking anything.
