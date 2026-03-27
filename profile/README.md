<p align="center">
  <a href="https://opensourceaihub.ai">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://opensourceaihub.ai/logo-white.svg" />
      <source media="(prefers-color-scheme: light)" srcset="https://opensourceaihub.ai/logo-dark.svg" />
      <img alt="OpenSourceAIHub" src="https://opensourceaihub.ai/Opensourceaihub_banner_vision.png" width="320" />
    </picture>
  </a>
</p>

<h3 align="center">The Enterprise AI Firewall & Governance Gateway</h3>

<p align="center">
  Stop AI data leaks and control spend with a drop-in proxy that sits between your app and LLM providers.<br />
  PII redaction (28+ entities + OCR) · Prompt injection blocking · Budget enforcement · Full governance dashboard.
</p>

<p align="center">
  <a href="https://opensourceaihub.ai"><strong>Website</strong></a> ·
  <a href="https://opensourceaihub.ai/docs"><strong>Docs</strong></a> ·
  <a href="https://opensourceaihub.ai/docs/openai-compatible-proxy"><strong>API Reference</strong></a> ·
  <a href="https://opensourceaihub.ai/demo-dashboard"><strong>Product Tour</strong></a> ·
  <a href="https://opensourceaihub.ai/models"><strong>Model Catalog</strong></a>
</p>

<p align="center">
  <a href="https://opensourceaihub.ai/login"><img src="https://img.shields.io/badge/Free_Credits-1%2C000%2C000-10b981?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJub25lIiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiPjxwYXRoIGQ9Ik0xMiAydjIwbTgtOEg0Ii8+PC9zdmc+" alt="1M Free Credits" /></a>&nbsp;
  <a href="https://opensourceaihub.ai/docs/openai-compatible-proxy"><img src="https://img.shields.io/badge/OpenAI_SDK-Compatible-blue?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI Compatible" /></a>&nbsp;
  <a href="https://opensourceaihub.ai/security"><img src="https://img.shields.io/badge/Architecture-Stateless-8b5cf6?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIyNCIgaGVpZ2h0PSIyNCIgdmlld0JveD0iMCAwIDI0IDI0IiBmaWxsPSJub25lIiBzdHJva2U9IndoaXRlIiBzdHJva2Utd2lkdGg9IjIiPjxyZWN0IHg9IjMiIHk9IjExIiB3aWR0aD0iMTgiIGhlaWdodD0iMTEiIHJ4PSIyIi8+PHBhdGggZD0iTTcgMTFWN2E1IDUgMCAwMTEwIDB2NCIvPjwvc3ZnPg==" alt="Stateless" /></a>
</p>

---

## How It Works

```
Your App  ──▶  OpenSourceAIHub  ──▶  LLM Provider
               (AI Firewall)
               ├─ PII Scan (28+ entities + OCR)
               ├─ Prompt Injection Detection
               ├─ Budget & Token Enforcement
               └─ Smart Cost Routing
```

The Hub is an **OpenAI-compatible proxy**. If your app uses the OpenAI SDK, integration is a **two-line change** — swap the `baseURL` and `apiKey`:

## Quickstart

### TypeScript / Node.js

```typescript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey:  "os_hub_your_key_here",                    // ← Hub API key
  baseURL: "https://api.opensourceaihub.ai/v1",       // ← Hub endpoint
});

const res = await client.chat.completions.create({
  model: "oah/llama-3.3-70b",   // smart-routed virtual model
  messages: [{ role: "user", content: "Explain zero-trust architecture." }],
});

console.log(res.choices[0].message.content);
```

### Python

```python
from openai import OpenAI

client = OpenAI(
    api_key="os_hub_your_key_here",                    # ← Hub API key
    base_url="https://api.opensourceaihub.ai/v1",      # ← Hub endpoint
)

res = client.chat.completions.create(
    model="oah/llama-3.3-70b",
    messages=[{"role": "user", "content": "Explain zero-trust architecture."}],
)

print(res.choices[0].message.content)
```

### Go

```go
package main

import (
	"context"
	"fmt"

	"github.com/openai/openai-go"
	"github.com/openai/openai-go/option"
)

func main() {
	client := openai.NewClient(
		option.WithAPIKey("os_hub_your_key_here"),                // ← Hub API key
		option.WithBaseURL("https://api.opensourceaihub.ai/v1"), // ← Hub endpoint
	)

	completion, _ := client.Chat.Completions.New(context.TODO(), openai.ChatCompletionNewParams{
		Model: "oah/llama-3.3-70b",
		Messages: []openai.ChatCompletionMessageParamUnion{
			openai.UserMessage("Explain zero-trust architecture."),
		},
	})

	fmt.Println(completion.Choices[0].Message.Content)
}
```

### cURL

```bash
curl -X POST https://api.opensourceaihub.ai/v1/chat/completions \
  -H "Authorization: Bearer os_hub_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "oah/llama-3.3-70b",
    "messages": [{"role": "user", "content": "Explain zero-trust architecture."}],
    "max_tokens": 512
  }'
```

> **Model names:** Use `oah/` prefixed virtual models for smart cost-routing, or explicit provider models like `groq/llama-3.3-70b-versatile`. See the [full model catalog](https://opensourceaihub.ai/models).

---

## What the Hub Protects

| Layer | What It Does |
|-------|-------------|
| **PII Redaction** | Detects and redacts 28+ entity types (SSN, credit cards, emails, phone numbers, API keys, etc.) + OCR for images — before the LLM ever sees your data |
| **Prompt Injection** | Blocks adversarial prompt injection patterns in real-time |
| **Budget Enforcement** | Per-project credit quotas with hard limits — no more surprise AI bills |
| **Token Limits** | Configurable max tokens per request (up to 32K) to prevent runaway costs |
| **Stateless Architecture** | We never store prompt content or AI responses. Only metadata is logged. AES-256 encryption for credentials |

## Supported Providers

Route to **100+ models** across **9 providers** with one API key:

| Provider | Example Models |
|----------|---------------|
| OpenAI | GPT-4.1, GPT-4.1 Mini, o4-mini |
| Anthropic | Claude Sonnet 4.6, Opus 4.6, Haiku 4.5 |
| Google Gemini | Gemini 2.5 Pro, Gemini 2.5 Flash |
| Groq | Llama 4 Scout, Llama 3.3, DeepSeek |
| xAI | Grok 3, Grok 3 Mini |
| Together.ai | Llama 4, DeepSeek R1, Qwen 3 |
| Mistral AI | Mistral Large, Small, Codestral |
| AWS Bedrock | Claude, Llama, Mistral via Bedrock |
| DeepInfra | DeepSeek V3, Llama 4, Qwen 3 |

## Repositories

| Repository | Description |
|-----------|-------------|
| [**.github**](https://github.com/opensourceaihub/.github) | Organization profile (you are here) |
| [**quickstart-ts**](https://github.com/opensourceaihub/opensourceaihub/tree/main/opensourceaihub-quickstart-ts) | TypeScript / Node.js quickstart — clone, `npm install`, run |
| [**quickstart-python**](https://github.com/opensourceaihub/opensourceaihub/tree/main/opensourceaihub-quickstart-python) | Python quickstart — clone, `pip install`, run |
| [**quickstart-go**](https://github.com/opensourceaihub/opensourceaihub/tree/main/opensourceaihub-quickstart-go) | Go quickstart — clone, `go run`, done |
| [**postman**](https://github.com/opensourceaihub/opensourceaihub/tree/main/opensourceaihub-postman) | Postman collection + environment for the full API |

## Pricing

| Plan | What You Get |
|------|-------------|
| **Free** | 1,000,000 Hub Credits on signup. Full DLP protection. All features. |
| **Managed Credits** | Pay-as-you-go. Add credits to your wallet. We handle provider accounts. |
| **Pro (BYOK)** | $29/month. Bring your own provider API keys. Zero markup on LLM costs. |

> **No credit card required** to start. Sign up and get 1M credits instantly.

---

<p align="center">
  <a href="https://opensourceaihub.ai/login"><strong>Get Started — 1M Free Credits →</strong></a>
</p>

<p align="center">
  <sub>
    <a href="https://opensourceaihub.ai/security">Security</a> ·
    <a href="https://opensourceaihub.ai/privacy">Privacy Policy</a> ·
    <a href="https://opensourceaihub.ai/tos">Terms of Service</a> ·
    <a href="mailto:support@opensourceaihub.ai">Contact</a>
  </sub>
</p>

<p align="center">
  <sub>Built by <a href="https://opensourceaihub.ai">Datum Fuse LLC</a> · Stateless Architecture · No Data Retention · AES-256 Encryption</sub>
</p>
