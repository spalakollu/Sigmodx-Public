# Sigmodx

Sigmodx is audit infrastructure for AI agents.

AI agents take real actions — moving money, calling tools, changing systems. Sigmodx records those actions as tamper-evident audit events and turns them into verifiable proof of what happened, so agent behavior can be proven, not just claimed.

🌐 [sigmodx.com](https://www.sigmodx.com) · Patent Pending · U.S. Application No. 64/040,964

## Overview

Sigmodx provides a repeatable audit architecture for agent-driven systems:

- **Audit scenarios** — pre-built, repeatable audit programs covering common agent risk areas, implemented across database, API, UI, and SDK.
- **Append-only event log** — every agent action is recorded immutably; history cannot be rewritten.
- **Reliability signals** — per-scenario signals computed from the event record.
- **Attestations** — HMAC-signed audit attestations that third parties can verify independently.
- **Review queues** — human oversight workflows for flagged agent activity.
- **Tenant controls** — strict organization isolation with cross-org safeguards.

## How it works

1. **Emit** — Agents and apps send audit events via the API or SDKs. Payloads are hashed client-side (SHA-256) before transmission.
2. **Record** — Events land in an append-only store with integrity hashes; API keys are stored hashed.
3. **Evaluate** — Reliability signals are computed per audit scenario.
4. **Attest** — Signed attestations are generated for completed audits.
5. **Verify** — Anyone can independently verify attestations and the event record without trusting Sigmodx infrastructure.
6. **Review** — Flagged activity surfaces in human review queues.

## Integrations

- **SDKs**: Python and TypeScript
- **Agent frameworks**: LangChain, LangGraph, CrewAI, OpenAI Agents
- **MCP server** for tool-based agent access
- **Public verification** endpoints and pages

## Cryptographic guarantees

- **Client-side SHA-256 payload hashing** — event contents are hashed before they leave the client.
- **Append-only enforcement** — at the database and application layers; historical records cannot be modified or deleted.
- **HMAC-signed attestations** — audit results carry signatures verifiable by third parties.
- **Hashed API keys** — keys are never stored in recoverable form.
- **Deterministic serialization** — identical data always hashes identically, regardless of system or ordering differences.

## Technology stack

**Frontend**:
- Next.js (App Router)
- React
- Tailwind CSS

**Backend**:
- FastAPI
- Supabase (PostgreSQL with Row Level Security)
- Redis (caching and task queue)

**Deployment**:
- Vercel (frontend)
- Railway (backend)

## Design principles

**Append-only governance**: Historical data cannot be modified or deleted. All changes are additive, creating an immutable audit trail.

**Tenant isolation**: Organizations operate in strict isolation. Cross-organization access is denied by default at every layer.

**Cryptographic verifiability**: Audit results can be independently verified through hashes and signatures. Third parties can verify integrity without relying on Sigmodx infrastructure.

**Human oversight**: Automated signals inform, but flagged activity is always reviewable by humans before it becomes a finding.

## Repository status

> This public repository is a showcase snapshot. Active development happens in private repositories; public snapshots are refreshed periodically and may lag the live product at [sigmodx.com](https://www.sigmodx.com).

## License

MIT — see [LICENSE](LICENSE).
