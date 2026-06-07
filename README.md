# 🎣 Phishing — Social Engineering Write-Up

> **Course Exercise** | Social Engineering Module | UniKL MIIT  
> **Platform:** [TryHackMe](https://tryhackme.com) — Phishing Emails 1  
> **Author:** [Dannyz15](https://github.com/Dannyz15)

---

## 📖 What is Phishing?

**Phishing** is a form of **social engineering** where an attacker sends fraudulent messages — typically emails — designed to trick individuals into revealing sensitive information, clicking malicious links, or downloading harmful attachments.

Phishing remains one of the most effective attack vectors in cybersecurity because it targets the **human element** rather than technical vulnerabilities.

---

## 🎯 Types of Phishing

| Type | Description |
|---|---|
| **Phishing** | Mass emails sent to many targets pretending to be a trusted entity |
| **Spear Phishing** | Targeted attack against a specific individual using personalised info |
| **Whaling** | Spear phishing aimed at high-value targets (CEOs, executives) |
| **Smishing** | Phishing conducted via SMS text messages |
| **Vishing** | Phishing conducted via voice calls |
| **Clone Phishing** | A legitimate email is cloned and modified with malicious content |
| **BEC** | Business Email Compromise — attacker uses a real internal account to commit fraud |

---

## 📧 Anatomy of a Phishing Email

Phishing emails are crafted to appear legitimate. Key components to investigate:

### 1. Email Address Structure
```
username @ domain
─────────────────
hatsalesman @ tryhatme.com
```
- **Username** — who the email claims to be from
- **Domain** — where it was sent from (look for lookalike domains, e.g. `amaz0n.com`)

### 2. Email Header Fields

| Field | What to Check |
|---|---|
| `From` | Display name vs actual address — often mismatched |
| `Reply-To` | May redirect replies to attacker-controlled address |
| `X-Originating-IP` | The real IP the email was sent from |
| `Received` | Trace the email path across mail servers |
| `Authentication-Results` | Shows if SPF / DKIM / DMARC passed or failed |

### 3. Email Body Red Flags

- Urgency or fear-inducing language ("Your account will be suspended!")
- Hyperlinks that don't match the displayed text
- Unexpected attachments (PDFs, ZIPs, Office docs with macros)
- Poor grammar or generic greetings ("Dear Customer")
- Spoofed branding mimicking trusted companies

---

## Email Delivery Protocols

Understanding how email works helps identify where phishing can be detected:

```
[Sender] ──SMTP──► [Sender Mail Server] ──DNS (MX Lookup)──► [Recipient Mail Server] ──IMAP/POP3──► [Recipient]
```

| Protocol | Role |
|---|---|
| **SMTP** | Sends email from client to mail server |
| **DNS** | Resolves the recipient's mail server via MX records |
| **IMAP** | Retrieves email; syncs across multiple devices |
| **POP3** | Retrieves email; downloads to a single device |

---

## 🛠️ Investigation Techniques

### Reading Raw Email Source
Open `.eml` files in a mail client (e.g. Thunderbird) → **View → Message Source**

```
Received: from [IP] (EHLO smtp3-160.piican.com)
X-Originating-IP: 43.255.56.161
Subject: Help protect your budget by protecting your home
From: "ADT Security Services" <newsletters@ant.anki-tech.com>
Reply-To: reply@ant.anki-tech.com
```

### Decoding Attachments
Email attachments are Base64-encoded in the raw source. Use:
- 🔧 [CyberChef](https://gchq.github.io/CyberChef/) → **From Base64**
- 🔧 Any online PDF/file converter

### Defanging IOCs
When sharing Indicators of Compromise (IOCs), **defang** them to prevent accidental clicks:

| Original | Defanged |
|---|---|
| `103.234.236.83` | `103[.]234[.]236[.]83` |
| `http://malicious.com` | `hxxp://malicious[.]com` |

---

## Key Takeaways

- Always verify the **actual sender domain**, not just the display name
- Check `Reply-To` — it is frequently abused in phishing campaigns
- Use the `X-Originating-IP` to trace where the email actually came from
- **IMAP** is preferred over POP3 when accessing email from multiple devices
- **BEC (Business Email Compromise)** uses legitimate internal accounts, making it harder to detect than standard phishing

---

## 🔗 Resources

- [TryHackMe — Phishing Emails 1](https://tryhackme.com/room/phishingemails1tryoe)
- [CyberChef](https://gchq.github.io/CyberChef/)
- [MXToolbox — Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)
- [PhishTool](https://www.phishtool.com/)
- [VirusTotal](https://www.virustotal.com/)

---

<div align="center">

*Part of the Social Engineering exercise — UniKL MIIT*  
*SOC Level 1 Path | Phishing Analysis Module*

</div>
