# Chapter 9 Cheat Sheet: Rapid Prototyping UI & Cloud Deployment

## Streamlit vs Gradio
| Feature | Streamlit | Gradio |
|---|---|---|
| Best for | Multi-page dashboards, data apps | Quick single-model demos |
| UI control | High, full layout API | Low, declarative I/O components |
| Built-in ML widgets | Manual | Native (Image, Audio, Chatbot, Label) |
| Caching | `@st.cache_data`, `@st.cache_resource` | Manual |
| Sharing | Deploy required | `share=True` → 72hr public link |

## Caching Decision Rule (Streamlit)
- Serializable return value (DataFrame, dict, API JSON) → `@st.cache_data`
- Unserializable shared object (loaded model, DB/API client) → `@st.cache_resource`

## Secrets Management — Never Do
- Hardcode API keys in source or Dockerfile
- Commit `.env` files to git
- Store secrets in public S3/storage buckets

## Secrets Management — Correct Pattern
- Local dev: `.env` + `.gitignore` + `os.environ.get()`
- Cloud: AWS Secrets Manager / Azure Key Vault / GCP Secret Manager, injected via IAM-scoped runtime access
- Exposed key response: **revoke/rotate first**, then purge from git history

## Docker Essentials
| Concept | Command/Rule |
|---|---|
| Build image | `docker build -t app:tag .` |
| Run container | `docker run -p 8501:8501 app:tag` |
| Multi-stage build | `FROM ... AS builder` → copy only artifacts to final stage |
| Cache-efficient order | base image → system deps → `COPY requirements.txt` → `pip install` → `COPY . .` |
| Image vs Container | Image = template; Container = running instance |

## Cloud Serverless Container Equivalents
| AWS | Azure | GCP |
|---|---|---|
| Fargate (ECS/EKS) | Container Apps | Cloud Run |

## Secrets Services by Cloud
| AWS | Azure | GCP |
|---|---|---|
| Secrets Manager (auto-rotation, ~$0.40/secret/mo) | Key Vault | Secret Manager |
| SSM Parameter Store (free, no rotation) | App Configuration | — |

## Rate Limiting Pattern
1. Request fails with HTTP 429
2. Wait using **exponential backoff + jitter**
3. Retry up to a bounded max attempts
4. Never tight-loop retry; never silently drop

## UX Patterns for AI Apps
- **Streaming**: token-by-token output for perceived responsiveness
- **Retries**: automatic backoff for transient LLM/API errors, surfaced to user only after exhausted
- **Transparency**: show sources, confidence, or reasoning steps; disclose AI-generated content

## Performance Optimization
- **Caching**: cache expensive/deterministic calls (embeddings, model loads)
- **Batching**: group multiple inference requests to reduce per-call overhead
- **Async**: use `async`/`await` for concurrent I/O-bound calls (API requests), not for CPU-bound rate-limit issues

## Git Workflow
`main` (protected) ← PR ← `feat/<name>` or `fix/<name>` branch. Secret scanning/pre-commit hooks required before merge.

## CI/CD Foundation
Build → Test → Build Docker image → Push to registry → Deploy to Cloud Run/Fargate/Container Apps → Automated rollback on health-check failure.
