# Road to Staff AI Agentic Security Engineer

A hands-on, lab-first roadmap I'm following in public to learn how to secure **AI agents**, the **APIs** they call, and the **identity (IAM)** and **privileged access (PAM)** controls that keep them in check.

> Started: November 2026 · Status: 🟢 In progress · Current phase: **Phase 0: Foundations**

---

## The mental model

```
AI Agent ──calls──▶ API ──checked by──▶ IAM ──extra control for powerful actions──▶ PAM
```

| Link | Question it answers |
|---|---|
| **AI agent** | What is making the request, and could an attacker be steering it? |
| **API** | Which door does the request go through? |
| **IAM** | *Who* is calling, and *what* are they allowed to do? |
| **PAM** | How do we tightly control the *dangerous* accounts and actions (admin, delete, production)? |

Most real attacks on AI agents succeed because **one of these links is weak**. Every lab I do, I ask: *which link broke?*

**ServiceNow side:** how AI Control Tower, IRM, SecOps and PAM enforce these controls lives in my [ServiceNow repo](https://github.com/atoz-guy/ServiceNow-/tree/main/AI-Agentic-Security-Roadmap).

**The one rule behind it all:** *never trust anything that comes from the user (or the LLM), and check permissions on the server every time.*

---

## How I learn (the loop for every lab)

1. **Read** only the topic intro (15 min)
2. **Do the lab** (Apprentice level first)
3. **Write notes** using the [notes template](notes/TEMPLATE.md)
4. **Tag it** with the OWASP item and the link that broke

Stuck for more than 20 minutes? Read the solution, close it, and redo the lab from scratch.

---

## Progress

| Phase | Focus | Weeks | Status |
|---|---|---|---|
| 0 | [Foundations: OWASP Top 10](#phase-0--foundations-owasp-top-10) | 1–2 | 🟢 In progress |
| 1 | [API security](#phase-1--api-security) | 3–4 | ⚪ Not started |
| 2 | [IAM](#phase-2--iam-identity--access-management) | 5–6 | ⚪ Not started |
| 3 | [PAM](#phase-3--pam-privileged-access-management) | 7–8 | ⚪ Not started |
| 4 | [AI agent security](#phase-4--ai-agent-security) | 9–10 | ⚪ Not started |
| 5 | [Capstone](#phase-5--capstone-build-it-then-break-it) | 11–12 | ⚪ Not started |

---

## Phase 0: Foundations (OWASP Top 10)

Source: [PortSwigger Web Security Academy](https://portswigger.net/web-security), **Apprentice labs only**. Notes: [notes/00-foundations.md](notes/00-foundations.md)

- [ ] Access control (A01, the most important one)
- [ ] Authentication (A07)
- [ ] Path traversal (A01)
- [ ] OS command injection (A03)
- [ ] Server-side request forgery, SSRF (A10)
- [ ] Cross-site scripting, XSS (A03)
- [ ] Read the remaining OWASP Top 10 items (about 10 min each):
  - [ ] A02 Cryptographic Failures
  - [ ] A04 Insecure Design
  - [ ] A05 Security Misconfiguration
  - [ ] A06 Vulnerable & Outdated Components
  - [ ] A08 Software & Data Integrity Failures
  - [ ] A09 Security Logging & Monitoring Failures
- [ ] Review day: redo one lab per topic without hints

---

## Phase 1: API security

Notes: [notes/01-api.md](notes/01-api.md)

- [ ] PortSwigger: **API testing** (Apprentice labs)
- [ ] Read the [OWASP API Security Top 10 (2023)](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)
- [ ] [APIsec University](https://www.apisecuniversity.com/): *API Security Fundamentals* (free)
- [ ] [crAPI](https://github.com/OWASP/crAPI): OWASP's deliberately vulnerable API (Docker)
- [ ] Master **BOLA** (Broken Object Level Authorization), #1 on the API list

---

## Phase 2: IAM (Identity & Access Management)

Notes: [notes/02-iam.md](notes/02-iam.md)

- [ ] PortSwigger: **JWT attacks**
- [ ] PortSwigger: **OAuth authentication**
- [ ] [Keycloak](https://www.keycloak.org/): build it myself (Docker). Users, roles, groups, protect an app with OAuth/OIDC
- [ ] [flaws.cloud](http://flaws.cloud/): AWS misconfigurations
- [ ] [flaws2.cloud](http://flaws2.cloud/): attacker and defender paths

---

## Phase 3: PAM (Privileged Access Management)

Notes: [notes/03-pam.md](notes/03-pam.md)

- [ ] TryHackMe: **Linux privilege escalation** (the attacker side PAM stops)
- [ ] TryHackMe: **Windows privilege escalation**
- [ ] [HashiCorp Vault](https://developer.hashicorp.com/vault/tutorials): dev mode. Secrets, dynamic credentials, rotation
- [ ] [Teleport Community Edition](https://goteleport.com/): just-in-time access and session recording
- [ ] Optional: CyberArk free training
- [ ] Be able to explain: **least privilege, just-in-time access, credential vaulting, session recording**

---

## Phase 4: AI agent security

Notes: [notes/04-ai-agents.md](notes/04-ai-agents.md)

- [ ] [Gandalf by Lakera](https://gandalf.lakera.ai/): prompt injection game
- [ ] PortSwigger: **Web LLM attacks** (all labs)
- [ ] [Damn Vulnerable LLM Agent](https://github.com/ReversecLabs/damn-vulnerable-llm-agent): hijack an agent that has tools
- [ ] Read the [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/)
  - [ ] LLM01 Prompt Injection
  - [ ] LLM02 Sensitive Information Disclosure
  - [ ] LLM05 Improper Output Handling
  - [ ] LLM06 Excessive Agency

---

## Phase 5: Capstone (build it, then break it)

Bring every link together in one small project, and publish it here.

- [ ] Build a small AI agent that calls 2–3 tools/APIs
- [ ] Protect the APIs with **Keycloak** (IAM): the agent gets its own identity and least-privilege roles
- [ ] Store the agent's secrets in **Vault** (PAM): short-lived credentials, no hardcoded keys
- [ ] Attack it: prompt injection, BOLA, excessive agency
- [ ] Fix what I found, and write up the before/after

---

## Quick reference: OWASP Top 10 (2021)

| # | Name | One line |
|---|---|---|
| A01 | Broken Access Control | Users can do or see things they shouldn't |
| A02 | Cryptographic Failures | Sensitive data isn't properly protected |
| A03 | Injection | User input is treated as code (SQLi, XSS, command injection) |
| A04 | Insecure Design | The plan itself is flawed |
| A05 | Security Misconfiguration | Bad settings or defaults |
| A06 | Vulnerable & Outdated Components | Old libraries with known holes |
| A07 | Identification & Authentication Failures | Weak login and sessions |
| A08 | Software & Data Integrity Failures | Trusting code or data without verifying it |
| A09 | Security Logging & Monitoring Failures | Attacks happen and nobody notices |
| A10 | Server-Side Request Forgery | Tricking the server into making requests for you |

*2025 update:* Security Misconfiguration moved up to #2; Outdated Components became **Software Supply Chain Failures**; SSRF was folded into Broken Access Control; new item **Mishandling of Exceptional Conditions**.

**Policy vs OWASP:** OWASP is the public reference of *what the dangers are*. A policy is an organisation's rule of *what we must do*, and it often says "test against the OWASP Top 10".
