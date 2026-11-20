# Ali Fakhrabadi

Senior Python backend, AI automation and DevOps engineer. 15+ years across software
engineering, Linux operations and network security (M.Sc. in IT; LPIC-2, CCNP, CEH,
Security+).

I build Python APIs, self-hosted AI and n8n automation, and the monitoring and
infrastructure code that keeps them running in production.

## Portfolio

Every number below was measured, and each README links to the result files.

### Platform and operations

Three projects that work together: an audit service, the stack that monitors it, and an
engine that triages the alerts.

| Project | What it is | Measured |
|---|---|---|
| [sentinel-iam-audit-service](https://github.com/ali-fakhrabadi/sentinel-iam-audit-service) | IAM, RBAC and an append-only audit log as a headless API: Django 5.2, DRF, PostgreSQL, Celery, signed webhooks, Helm chart | Ingest p95 33.5 ms at 50 req/s; 1,760 events/s in bulk; 1,200 of 1,200 webhooks delivered |
| [cloud-native-observability-iac](https://github.com/ali-fakhrabadi/cloud-native-observability-iac) | Prometheus, Grafana, Loki and Alertmanager as code, with Ansible roles and Terraform for AWS | 26 unit-tested alerts; a crash loop notified in 58 s; 727 MiB footprint; bare Debian 12 to a running stack in 2 min 42 s |
| [aiops-n8n-incident-engine](https://github.com/ali-fakhrabadi/aiops-n8n-incident-engine) | FastAPI engine that turns alerts into incidents, analyses the logs with a local LLM and notifies through self-hosted n8n | Critical alerts paged in 12.6 s; 5 of 5 causes found and 0 prompt injections followed in the evaluation |

```mermaid
flowchart LR
    s["Sentinel<br/>audit service"] -->|"metrics, logs"| o["Observability stack<br/>Prometheus, Loki, Grafana"]
    o -->|"alerts"| a["AIOps engine<br/>FastAPI, local LLM"]
    a -->|"signed webhook"| n["n8n"] --> t["Telegram"]
```

### AI applications

Self-hosted LLM applications for business data, each with an evaluation dataset and a
benchmark report.

| Project | What it is | Measured |
|---|---|---|
| [rag-support-chatbot](https://github.com/ali-fakhrabadi/rag-support-chatbot) | Secure RAG assistant: cited answers from private documents, workspace isolation with PostgreSQL row-level security; FastAPI, pgvector, Ollama, React | 135 test questions: 100 % retrieval recall@5, 26 of 26 correct "no answer" cases, 0 cross-workspace citations, 7 of 7 injection tests passed |
| [ai-lead-qualification-crm-automation](https://github.com/ali-fakhrabadi/ai-lead-qualification-crm-automation) | Lead intake, AI qualification under deterministic rules, CRM sync and human-approved follow-ups; FastAPI, self-hosted n8n, Ollama, React | 128 scenarios: 0 duplicate CRM contacts, 22 of 22 repeat submissions caught, 0 messages sent without approval; one injection gap found by the benchmark, fixed and re-tested |

## How I work

* Tests, strict typing and CI on everything, including alert rules, Ansible roles and
  Terraform modules.
* Security by default: non-root containers, secrets from files, signed webhooks, SSRF
  protection, pinned dependencies.
* Claims backed by measurements: load tests and fault-injection drills, with the raw
  results in the repository.

## Stack

**Backend:** Python, Django, DRF, FastAPI, PostgreSQL, pgvector, Redis, Celery
**AI and automation:** n8n (self-hosted), Ollama, OpenAI API, RAG, LLM agents
**Frontend:** React, TypeScript
**DevOps:** Docker, Kubernetes, Helm, Terraform, Ansible, GitHub Actions
**Observability:** Prometheus, Grafana, Loki, Alertmanager
