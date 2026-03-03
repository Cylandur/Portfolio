# eM Client AI Connector

**Natural language email automation — describe the email you want, Claude writes and sends it.**

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python)
![Claude AI](https://img.shields.io/badge/Claude_AI-Powered-D97757?style=flat)
![macOS](https://img.shields.io/badge/macOS-Optimized-000000?style=flat&logo=apple)
![IMAP](https://img.shields.io/badge/IMAP%20%2F%20SMTP-Compatible-4A90E2?style=flat)

---

## Overview

The eM Client AI Connector is a macOS-native Python bridge between the Anthropic Claude API and eM Client (or any IMAP/SMTP-compatible email client). It enables natural language control of your inbox — describe what you want to write, and Claude drafts, addresses, and sends it.

Built as a practical productivity tool, it supports reading recent emails, composing replies, and sending new messages entirely through natural language prompts from the command line.

---

## Features

**Email Reading**
- IMAP-based inbox access — reads recent messages, threads, and metadata
- Multi-folder support: inbox, sent, drafts, and custom folders
- Summary mode — Claude summarizes unread emails or threads on request

**AI-Powered Composition**
- Natural language drafting — describe tone, intent, and recipient; Claude writes the email
- Context-aware replies — feed Claude a received email and ask for a reply; it matches tone and addresses the content
- Subject line generation included

**Sending**
- Full SMTP send integration — sends directly from your configured account
- Multi-provider support: Gmail (App Password), Outlook/Exchange, and any custom SMTP server
- Dry-run mode — previews the drafted email without sending

**Platform**
- Optimized for macOS with Homebrew Python
- CLI interface — runs from Terminal, scriptable, and automation-friendly
- Multi-account configuration via a simple YAML config file
- No dependency on eM Client's API — works at the IMAP/SMTP layer directly

---

## Quick Start

**Requirements**
- macOS (tested on Ventura and Sonoma)
- Homebrew Python 3.11+
- An Anthropic API key
- An email account with IMAP/SMTP access enabled

**Installation**
```bash
# Install dependencies via Homebrew Python
/opt/homebrew/bin/pip3 install anthropic imaplib2 pyyaml

# Clone the repo
git clone https://github.com/shaunreiland/em-client-connector
cd em-client-connector

# Configure your accounts
cp config.example.yaml config.yaml
nano config.yaml   # Add your email credentials and API key
```

**Usage**
```bash
# Read recent emails
python3 connector.py read --count 10

# Compose and send with natural language
python3 connector.py send --to "boss@company.com" \
  --prompt "Write a professional follow-up on the Q2 report we discussed yesterday"

# Reply to a specific email
python3 connector.py reply --message-id 12345 \
  --prompt "Acknowledge receipt and say I'll review by Friday"

# Dry run (preview without sending)
python3 connector.py send --to "test@example.com" \
  --prompt "Quick thank-you note for the meeting" --dry-run
```

---

## Configuration

```yaml
# config.yaml

anthropic:
  api_key: "your_anthropic_api_key"
  model: "claude-opus-4-5"

accounts:
  - name: "Work"
    imap_host: "imap.gmail.com"
    imap_port: 993
    smtp_host: "smtp.gmail.com"
    smtp_port: 587
    email: "you@gmail.com"
    password: "your_app_password"   # Gmail App Password, not your main password
    default: true

  - name: "Personal"
    imap_host: "outlook.office365.com"
    imap_port: 993
    smtp_host: "smtp.office365.com"
    smtp_port: 587
    email: "you@outlook.com"
    password: "your_password"
```

---

## Gmail Setup Note

Gmail requires an **App Password** rather than your main account password. To generate one:
1. Go to Google Account → Security → 2-Step Verification
2. Scroll to **App passwords**
3. Generate a password for "Mail" on "Mac"
4. Use that 16-character password in `config.yaml`

---

## Architecture

```
em-client-connector/
├── connector.py        # Main CLI entry point
├── imap_client.py      # IMAP read layer
├── smtp_client.py      # SMTP send layer
├── ai_composer.py      # Claude API prompt + response handling
├── config.yaml         # Account and API key configuration (gitignored)
├── config.example.yaml # Safe example config to commit
└── requirements.txt
```

---

## Tech Stack

| Component | Technology |
|---|---|
| Language | Python 3.11+ (Homebrew, macOS) |
| AI | Anthropic Claude API |
| Email Read | IMAP via `imaplib` |
| Email Send | SMTP via `smtplib` |
| Config | YAML via `pyyaml` |
| Platform | macOS (Ventura / Sonoma tested) |

---

## Security Notes

- `config.yaml` is included in `.gitignore` — never commit credentials
- Supports Gmail App Passwords and standard IMAP/SMTP authentication
- No credentials are sent to any third party beyond your email provider and Anthropic's API
