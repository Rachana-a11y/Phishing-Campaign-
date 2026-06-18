# Phishing Awareness Simulation

A controlled, authorized phishing simulation built with **GoPhish** to study employee susceptibility to credential-harvesting attacks. Conducted as part of the Cybersecurity Internship at **Naviotech Solution Pvt. Ltd.**

> ⚠️ **Disclaimer:** This project was carried out strictly in an isolated lab environment (Kali Linux VM, local GoPhish instance) for educational purposes. No real users, third-party platforms, or production systems were targeted. Do not use this repository to conduct unauthorized phishing campaigns — that is illegal.

---

## 📋 Project Overview

| | |
|---|---|
| **Tool Used** | [GoPhish](https://getgophish.com/) (open-source phishing framework) |
| **Environment** | Kali Linux (Oracle VirtualBox) |
| **Scenario** | Simulated "Instagram Security Alert" phishing email |
| **Targets** | 2 simulated users (Premium Member, VIP) |
| **Goal** | Measure click-through and credential-submission rates; identify awareness gaps |

The simulation replicates a real-world social engineering attack chain — from a spoofed sender identity, to an urgent phishing email, to a cloned login page that harvests credentials — entirely within a sandboxed lab.

---

## 🛠️ Setup

### 1. Target Group
A group named `Instagram Security` was created in GoPhish with 2 test users:

| Name | Email | Role |
|------|-------|------|
| Rachana Varma | rachana.appani05@gmail.com | Premium Member |
| Rakesh varma | appanirachana@gmail.com | VIP |

### 2. Sending Profile (SMTP)
| Field | Value |
|-------|-------|
| From | `Instagram <hackr.xpert3@gmail.com>` |
| Host | `smtp.gmail.com:465` |
| Interface | SMTP (Gmail App Password) |

### 3. Landing Page
A cloned Instagram login page was built with:
- **Capture Submitted Data:** ✅ Enabled
- **Capture Passwords:** ✅ Enabled
- **Redirect URL:** `http://www.instagram.com/` (after submission, to avoid suspicion)

### 4. Email Template
Subject: `⚠️ Unusual login attempt on your account`
Sender disguised as **Instagram**, using an urgency-based message and a `{{.FirstName}}` merge tag for personalization, with an embedded CTA link to the cloned landing page.

---

## 📊 Results

4 test campaigns were run while refining the template; the final campaign (`instagram`) produced the following results:

| Metric | Count |
|---|---|
| Emails Sent | 6 |
| Emails Opened | 1 |
| Links Clicked | 1 |
| Credentials Submitted | 1 |
| Emails Reported | 0 |

### Engagement Funnel (2 unique targets)
| Stage | Users |
|-------|-------|
| Email Sent | 2 / 2 |
| Clicked Link | 1 / 2 (50%) |
| Submitted Credentials | 1 / 2 (50%) |
| Reported Phishing | 0 / 2 (0%) |

### Timeline — Target "Rakesh varma"
| Event | Timestamp |
|-------|-----------|
| Campaign Created | June 15, 2026, 8:41:13 PM |
| Email Sent | June 15, 2026, 8:41:19 PM |
| Clicked Link | June 15, 2026, 8:41:44 PM (**25 sec** after delivery) |
| Submitted Data | June 15, 2026, 8:42:19 PM |

Captured (lab-only, cleartext per GoPhish default) credentials:
```
username: Rachana
password: password
```

---

## 🧩 MITRE ATT&CK Mapping

| Technique ID | Tactic | Technique |
|---|---|---|
| T1566.001 | Initial Access | Spearphishing Link |
| T1598.003 | Reconnaissance | Phishing for Information |
| T1056.003 | Credential Access | Web Portal Capture |
| T1078 | Defense Evasion | Valid Accounts (legitimate SMTP relay) |
| T1204.001 | Execution | User Execution – Malicious Link |
| T1534 | Lateral Movement | Internal Spearphishing (if extended) |

---

## 🔐 Key Findings

- **50% click rate** and **50% credential-submission rate** — in line with real-world industry phishing simulation averages.
- **0% reporting rate** — neither target flagged the email as suspicious, indicating a security awareness gap.
- The victim clicked the link within **25 seconds** of receiving the email, showing how urgency-based pretexts drive fast, low-scrutiny action.
- Sender impersonation + urgency + a convincing clone page were sufficient to bypass user judgment without any technical exploit.

---

## ✅ Recommendations

1. **Security Awareness Training** — Regular phishing simulations and staff training on identifying suspicious emails.
2. **Enable MFA** — Mitigates the impact of credential theft even if phishing succeeds.
3. **Email Authentication (SPF/DKIM/DMARC)** — Reduces sender-spoofing success rate.
4. **Link Verification Habits** — Train users to inspect URLs/domains before clicking.
5. **Easy Reporting Mechanism** — One-click "Report Phishing" buttons to encourage reporting.
6. **Recurring Simulations** — Quarterly GoPhish campaigns to track improvement over time.

---

## 🧪 Lessons Learned & Challenges

| Challenge | Takeaway |
|---|---|
| **Traffic visibility** | Routing only Kali VM traffic through monitoring (and not the host browser) can cause assets to go undetected — a gap also seen in a parallel authorized pentest engagement. |
| **Email deliverability** | Gmail SMTP intermittently triggered spam/security warnings; required header tuning and test sends before the live campaign. |
| **Believable pretexting** | Early email drafts were too generic — iterated through 4 campaign versions before landing on urgency + impersonation copy that drove a click in 25 seconds. |
| **Cleartext credential storage** | GoPhish stores captured credentials in cleartext by default, reinforcing why production systems must never log credentials unencrypted. |
| **Redirect realism** | Redirecting to the real instagram.com post-submission was key — victims had no visual cue anything was wrong. |
| **Speed of compromise** | Click-to-credential-theft completed in under 60 seconds, underscoring that detection speed matters as much as prevention. |

## 🧠 Skills Demonstrated

- **Offensive Security:** GoPhish campaign configuration, social engineering/pretexting, credential-harvesting page design, SMTP sender impersonation
- **Tools & Platforms:** Kali Linux, Oracle VirtualBox, Gmail SMTP (App Passwords), HTML/CSS landing page editing
- **Analysis & Reporting:** MITRE ATT&CK technique mapping, engagement funnel/metrics analysis, timeline reconstruction, professional report and deck writing

---

## 🎯 Conclusion

This simulation demonstrated a complete, end-to-end credential-phishing attack chain — from sender impersonation to a cloned login page to credential capture — executed entirely within a controlled, authorized lab environment.

- **50% click rate** and **50% credential-submission rate**, closely mirroring real-world industry phishing-test benchmarks.
- **0% reporting rate** — no target flagged the email, exposing a critical detection/reporting gap.
- The attack succeeded purely through **social engineering** (impersonation + urgency + a convincing clone page), with **no technical exploit** required.
- **Human behavior is the weakest link** in the security chain; technical controls (SPF/DKIM/DMARC, MFA, email filtering) must be paired with continuous awareness training to meaningfully reduce risk.
- The project reinforced practical, transferable skills in offensive tooling, attack-chain analysis, and security reporting — directly applicable to SOC analyst and blue-team roles.

**Bottom line:** Phishing remains the #1 initial access vector for real-world breaches. Regular, realistic simulations like this one are one of the most effective ways to measure — and improve — an organization's human firewall.

---

## 📁 Repository Structure

```
.
├── README.md                  # This file
├── report/
│   └── Phishing_Awareness_Simulation_Report.pdf
├── presentation/
│   └── Phishing_Awareness_Simulation_Rachana.pptx
└── screenshots/
    ├── sending_profile_smtp.png
    ├── landing_page_editor.png
    ├── campaign_dashboard.png
    ├── victim_timeline.png
    └── credentials_captured.png
```

---

## 👤 Author

**Rachana Appani**
B.Tech CSE (Cybersecurity), Malla Reddy Engineering College for Women
Cybersecurity Intern — Naviotech Solution Pvt. Ltd. (June 2026)

[GitHub](https://github.com/Rachana-a11y) · [LinkedIn](https://linkedin.com/in/rachana-appani)

---

## ⚖️ Ethical Use Statement

This project is intended **solely for educational and authorized security-awareness purposes**. All testing was performed against accounts and infrastructure owned and controlled by the author within an isolated VM environment. No production systems, third-party services, or non-consenting individuals were targeted. Phishing real users without explicit written authorization is illegal under the IT Act, 2000 (India) and equivalent laws elsewhere.
