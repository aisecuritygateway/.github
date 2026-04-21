<p align="center">
  <a href="https://aisecuritygateway.ai">
    <img alt="AI Security Gateway" src="https://aisecuritygateway.ai/og.jpg" width="600" />
  </a>
</p>

<h3 align="center">The Open-Source AI Firewall</h3>

<p align="center">
  Stop sensitive data from leaking into LLM prompts.<br />
  PII redaction · Secret detection · Prompt injection blocking · Self-hosted via Docker.
</p>

<p align="center">
  <a href="https://github.com/aisecuritygateway/aisecuritygateway"><strong>Get Started</strong></a> ·
  <a href="https://aisecuritygateway.ai/docs"><strong>Docs</strong></a> ·
  <a href="https://aisecuritygateway.ai/open-source"><strong>OSS vs Cloud</strong></a> ·
  <a href="https://aisecuritygateway.ai"><strong>Managed Cloud</strong></a>
</p>

<p align="center">
  <a href="https://github.com/aisecuritygateway/aisecuritygateway/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge" alt="Apache 2.0" /></a>&nbsp;
  <a href="https://github.com/aisecuritygateway/aisecuritygateway"><img src="https://img.shields.io/badge/Docker-Quickstart-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" /></a>&nbsp;
  <a href="https://aisecuritygateway.ai/docs/openai-compatible-proxy"><img src="https://img.shields.io/badge/OpenAI_SDK-Compatible-10a37f?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI Compatible" /></a>
</p>

---

## What Is AISG?

AISG (AI Security Gateway) is an **OpenAI-compatible proxy** that acts as an AI firewall. It sits between your app and LLM providers, scanning every request for PII, secrets, and prompt injection attacks before anything reaches the model.

```
Your App  ──▸  AISG Gateway  ──▸  Presidio (PII scan)  ──▸  LLM Provider
                    │                                            │
                    │◂── redacted or blocked ──────────────────▸│
                    │◂── clean response ────────────────────────│
```

## Key Features

- **PII Redaction** — emails, phone numbers, credit cards, SSNs, names, locations, IP addresses
- **Secret Detection** — API keys, AWS credentials, GitHub tokens, private keys, Slack webhooks
- **Prompt Injection Blocking** — detects jailbreak and instruction override attempts
- **Multi-Provider Routing** — OpenAI-compatible API, BYOK, swap providers in config
- **Fail-Closed Security** — if the safety layer is down, requests are blocked, never forwarded unscanned
- **Zero Cloud Dependencies** — runs entirely on your machine via Docker

## Quickstart

```bash
git clone https://github.com/aisecuritygateway/aisecuritygateway.git
cd aisecuritygateway
cp .env.example .env        # add your provider key
docker compose up --build   # gateway + presidio
```

```bash
curl http://localhost:8000/v1/chat/completions \
  -H "Authorization: Bearer change-me-to-a-real-secret" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "llama-3.3-70b-versatile",
    "messages": [{"role": "user", "content": "My email is alice@acme.com and SSN is 123-45-6789"}]
  }'
```

The gateway redacts the email and SSN before forwarding. The response includes `aisg_metadata.pii_detected: true`.

## OSS vs Managed Cloud

|  | OSS (this repo) | [Cloud](https://aisecuritygateway.ai) |
|---|:---:|:---:|
| PII detection & redaction (text) | 13 entity types | 28+ entity types |
| OCR image scanning | — | Yes |
| Secret leak prevention | 6 recognizers | Extended |
| Prompt injection blocking | 5 core patterns | Extended library |
| Multi-provider routing (BYOK) | 2 providers | 8+ providers |
| Smart cost-optimization routing | — | Yes |
| Dashboards & analytics | — | Yes |
| Multi-project management | — | Yes |

---

<p align="center">
  <a href="https://github.com/aisecuritygateway/aisecuritygateway"><strong>⭐ Star the repo</strong></a> ·
  <a href="https://aisecuritygateway.ai/open-source"><strong>Learn more</strong></a> ·
  <a href="https://aisecuritygateway.ai"><strong>Try the managed cloud</strong></a>
</p>

<p align="center">
  <sub>
    <a href="https://aisecuritygateway.ai/security">Security</a> ·
    <a href="https://github.com/aisecuritygateway/aisecuritygateway/blob/main/LICENSE">License (Apache 2.0)</a> ·
    <a href="https://linkedin.com/company/ai-security-gateway">LinkedIn</a> ·
    <a href="https://x.com/AISGateway">X / Twitter</a> ·
    <a href="https://www.youtube.com/@AISecurityGateway">YouTube</a>
  </sub>
</p>

<p align="center">
  <sub>Built by <a href="https://aisecuritygateway.ai">Datum Fuse LLC</a> — making AI safe by default.</sub>
</p>
