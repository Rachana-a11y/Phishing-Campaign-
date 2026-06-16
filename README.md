# Phishing Awareness Simulation Using GoPhish

**Cybersecurity Internship Project | Naviotech Solutions | June 2026**

> ⚠️ **Educational Use Only**
>
> This project was conducted entirely in a controlled laboratory environment using authorized test participants and test accounts. No real users, organizations, or external systems were targeted. This project was performed solely for cybersecurity awareness and educational purposes.

---

# Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [System Requirements](#system-requirements)
- [Tools & Technologies](#tools--technologies)
- [Project Architecture](#project-architecture)
- [Project Structure](#project-structure)
- [Setup & Configuration](#setup--configuration)
- [Campaign Workflow](#campaign-workflow)
- [Results](#results)
- [Key Findings](#key-findings)
- [Security Recommendations](#security-recommendations)
- [Post-Simulation Awareness Training](#post-simulation-awareness-training)
- [Challenges Encountered](#challenges-encountered)
- [Skills Demonstrated](#skills-demonstrated)
- [Screenshots](#screenshots)
- [Future Improvements](#future-improvements)
- [Learning Outcomes](#learning-outcomes)
- [Disclaimer](#disclaimer)

---

# Project Overview

Phishing remains one of the most effective social engineering techniques used by attackers to steal credentials and gain unauthorized access to systems. This project demonstrates a controlled phishing awareness simulation using **GoPhish**, an open-source phishing framework.

The simulation involved creating a phishing email campaign, deploying a simulated login page, tracking user interactions, and analyzing participant responses. The objective was to evaluate user awareness and demonstrate how phishing attacks operate in real-world scenarios.

---

# Objectives

- Deploy and configure GoPhish from scratch.
- Create a phishing email template.
- Design a phishing landing page.
- Track email opens, clicks, and submissions.
- Analyze user behavior during the campaign.
- Conduct awareness training after the simulation.
- Recommend security improvements based on findings.

---

# System Requirements

| Component | Requirement |
|------------|------------|
| Operating System | Kali Linux / Ubuntu Linux |
| RAM | Minimum 2 GB |
| Virtualization | Oracle VirtualBox |
| Framework | GoPhish |
| SMTP Service | Gmail SMTP or MailHog |
| Browser | Firefox |
| Web Server | Python HTTP Server |

---

# Tools & Technologies

| Tool | Purpose |
|--------|---------|
| Kali Linux | Security Testing Environment |
| GoPhish | Phishing Simulation Platform |
| HTML/CSS | Landing Page Development |
| Gmail SMTP | Email Delivery |
| Python HTTP Server | Hosting Awareness Pages |
| Firefox | Testing and Validation |
| Oracle VirtualBox | Virtual Lab Environment |

---

# Project Architecture

```text
Participant
     │
     ▼
Phishing Email
     │
     ▼
GoPhish Tracking Link
     │
     ▼
Landing Page
     │
     ▼
Credential Submission
     │
     ▼
Awareness Page
     │
     ▼
Campaign Analytics Dashboard
```

---

# Project Structure

```text
phishing-awareness-simulation/
│
├── templates/
│   └── email.html
│
├── landing-pages/
│   ├── index.html
│   └── awareness.html
│
├── screenshots/
│   ├── dashboard.png
│   ├── email-template.png
│   ├── landing-page.png
│   ├── awareness-page.png
│   └── results.png
│
└── README.md
```

---

# Setup & Configuration

## Step 1 – Install GoPhish

```bash
mkdir ~/phishing-lab
cd ~/phishing-lab

wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip

unzip gophish-v0.12.1-linux-64bit.zip
chmod +x gophish
```

---

## Step 2 – Configure GoPhish

Edit the configuration file:

```bash
nano config.json
```

Example configuration:

```json
{
  "admin_server": {
    "listen_url": "127.0.0.1:3333",
    "use_tls": true
  },
  "phish_server": {
    "listen_url": "0.0.0.0:80",
    "use_tls": false
  }
}
```

> **Note:** Port 80 requires root privileges. Use port 8080 if running without root access.

---

## Step 3 – Launch GoPhish

```bash
sudo ./gophish
```

Access the dashboard:

```text
https://127.0.0.1:3333
```

Login using the default credentials displayed in the terminal and change the password when prompted.

---

## Step 4 – Create the Landing Page

A custom HTML login page was developed to simulate a company login portal.

Features included:

- Responsive design
- Credential input fields
- Form submission tracking
- Awareness redirection page

---

## Step 5 – Configure Landing Page in GoPhish

Navigate to:

```text
Landing Pages → New Page
```

Configuration:

- Import custom HTML page
- Enable Capture Submitted Data
- Enable Capture Passwords
- Redirect to awareness page after submission

---

## Step 6 – Create Email Template

Navigate to:

```text
Email Templates → New Template
```

Template Features:

- Simulated IT support message
- Personalized recipient names
- Embedded GoPhish tracking links
- Urgency-based social engineering techniques

GoPhish Variables Used:

```text
{{.FirstName}}
{{.URL}}
```

---

## Step 7 – Configure Sending Profile

SMTP Configuration:

| Setting | Value |
|----------|--------|
| SMTP Server | smtp.gmail.com |
| Port | 465 |
| Encryption | TLS |
| Authentication | Gmail App Password |

Verify configuration using **Send Test Email** before launching the campaign.

---

## Step 8 – Create Target Group

Navigate to:

```text
Users & Groups → New Group
```

Add authorized participants who provided informed consent before the simulation.

---

## Step 9 – Launch Campaign

Navigate to:

```text
Campaigns → New Campaign
```

Configure:

| Field | Value |
|---------|---------|
| Email Template | IT Password Reset |
| Landing Page | Company Portal Login |
| Sending Profile | Gmail SMTP |
| Group | Test Participants |
| URL | Campaign URL |

Click **Launch Campaign** to begin tracking activity.

---

# Campaign Workflow

The phishing simulation followed the workflow below:

1. Phishing email delivered.
2. Participant opened the email.
3. Participant clicked the embedded link.
4. Simulated login page loaded.
5. User interaction recorded.
6. Awareness page displayed.
7. Campaign metrics collected.
8. Results analyzed.

---

# Results

| Metric | Count |
|----------|----------|
| Emails Sent | 2 |
| Emails Opened | 1 |
| Links Clicked | 1 |
| Credentials Submitted | 1 |
| Emails Reported | 0 |

## Campaign Statistics

| Metric | Result |
|----------|----------|
| Open Rate | 50% |
| Click Rate | 50% |
| Submission Rate | 50% |
| Reporting Rate | 0% |

---

# Key Findings

## Social Engineering Remains Effective

A simple phishing email using urgency and authority-based messaging was sufficient to encourage user interaction.

## Rapid Attack Progression

The entire phishing workflow, from email delivery to submission, occurred within a short period of time.

## Mobile Device Vulnerability

Users accessing email on mobile devices were less likely to verify URLs before interacting with the phishing page.

## Lack of Reporting Behavior

No participants reported the suspicious email, highlighting a gap in phishing awareness.

## Importance of Security Training

The results demonstrate the need for continuous phishing awareness programs and security education.

---

# Security Recommendations

## High Priority

- Enable Multi-Factor Authentication (MFA).
- Conduct regular phishing awareness training.
- Enforce strong password policies.

## Medium Priority

- Implement SPF, DKIM, and DMARC.
- Promote safe email practices.
- Encourage URL verification before clicking links.

## Low Priority

- Improve phishing reporting processes.
- Develop incident response procedures.
- Enhance user security awareness resources.

---

# Post-Simulation Awareness Training

After completion of the campaign:

- Participants were informed about the simulation.
- Common phishing indicators were explained.
- Safe email handling practices were reviewed.
- Security awareness materials were distributed.
- Recommendations were provided for recognizing phishing attempts.

---

# Challenges Encountered

- SMTP configuration and authentication setup.
- Self-signed certificate warnings in GoPhish.
- Landing page testing and validation.
- Email delivery verification.
- Campaign tracking configuration.

---

# Skills Demonstrated

- Phishing Awareness Simulation
- GoPhish Administration
- Social Engineering Analysis
- HTML/CSS Development
- Security Awareness Training
- Campaign Analytics
- Cybersecurity Reporting
- Security Documentation

---

# Screenshots

The following evidence was collected during the project:

### Screenshot 1 – GoPhish Dashboard

Campaign statistics and monitoring dashboard.




### Screenshot 2 – Phishing Email

Email received by participants.
<img width="1532" height="776" alt="image" src="https://github.com/user-attachments/assets/0ba2fec4-934a-45ef-b801-3950c1ce5339" />


### Screenshot 3 – Landing Page

Simulated login page.

### Screenshot 4 – Awareness Page

Training page displayed after submission.

### Screenshot 5 – Campaign Results

Submission and click statistics.








### Screenshot 6 – Post-Training Results

Comparison of user behavior after awareness training.

---

# Future Improvements

- Increase participant sample size.
- Conduct department-wise phishing assessments.
- Develop multiple phishing scenarios.
- Implement automated reporting dashboards.
- Measure improvements across multiple campaigns.

---

# Learning Outcomes

This project provided practical experience in:

- Designing phishing awareness campaigns.
- Configuring GoPhish infrastructure.
- Building phishing landing pages.
- Monitoring user interactions.
- Analyzing security metrics.
- Conducting cybersecurity awareness training.
- Producing professional security documentation.

---

# Disclaimer

This project was conducted solely for educational and cybersecurity awareness purposes as part of a cybersecurity internship with Naviotech Solutions.

All activities were performed in an isolated and controlled environment using authorized participants and test accounts. No unauthorized systems, organizations, or individuals were targeted.

Any attempt to reproduce these techniques against systems without explicit written permission may violate applicable cybersecurity and computer misuse laws.

---

**Organization:** Naviotech Solutions  
**Domain:** Cybersecurity  
**Project Type:** Phishing Awareness Simulation  
**Internship Period:** June 2026  
**Author:** [Your Name]
