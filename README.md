# Tabby (tabby-ml)

Tabby is an open-source, self-hosted AI coding assistant from TabbyML (Apache-2.0) - a privacy-first alternative to GitHub Copilot. You run the Tabby server yourself (Docker, a consumer-grade GPU, or your own cloud); it is self-contained, needs no external DBMS or cloud service, and makes no external calls to third parties. The server exposes an OpenAPI-documented REST surface (Swagger UI at `/swagger-ui`, spec at `/api-docs/openapi.json`, default port `8080`) for code completion, OpenAI-compatible chat completions, an Answer Engine backed by a doc-ingestion knowledge base, health, the model registry, and telemetry events.

**Access model (important):** Tabby is **self-hosted, per-instance**. There is no shared multi-tenant TabbyML API for the core server - the base URL is **your own deployment** (default `http://localhost:8080`). Endpoints authenticate with a Bearer registration token minted by your instance. Completion and chat endpoints return `501 Not Implemented` when the corresponding model is not configured. TabbyML also sells hosted Community, Team, and Enterprise plans layered over the same server API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tabby-ml/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tabby-ml/refs/heads/main/apis.yml)

## Tags

- AI Coding Assistant
- Code Completion
- Open Source
- Developer Tools
- LLM
- AI
- Self-Hosted
- Code Generation
- Copilot Alternative

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

All base URLs below are the default self-hosted address (`http://localhost:8080`). Replace the host and port with your own Tabby deployment.

### Tabby Code Completions API

`POST /v1/completions` - the core code-completion endpoint that powers Tabby's IDE plugins. Takes a language and code segments (prefix/suffix around the cursor), applies retrieval-augmented generation against your indexed repositories, and returns ranked completion choices. Returns 501 when no completion model is configured.

- **Human URL:** [https://tabby.tabbyml.com/docs/api/](https://tabby.tabbyml.com/docs/api/)
- **Base URL:** `http://localhost:8080`

#### Tags

- Code Completion
- Completions
- AI Coding Assistant

#### Properties

- [Documentation](https://tabby.tabbyml.com/docs/welcome/)
- [API Reference](https://tabby.tabbyml.com/api/)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tabby-ml.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tabby-ml.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Tabby Chat Completions API

`POST /v1/chat/completions` - an OpenAI-compatible chat completions endpoint (with a legacy `/v1beta/chat/completions` alias) that streams responses as Server-Sent Events. Powers Tabby's inline chat and Answer Engine, and lets OpenAI-style SDKs point at your Tabby server. Returns 501 when no chat model is configured.

- **Human URL:** [https://tabby.tabbyml.com/docs/references/models-http-api/openai/](https://tabby.tabbyml.com/docs/references/models-http-api/openai/)
- **Base URL:** `http://localhost:8080`

#### Tags

- Chat
- Completions
- LLM
- OpenAI Compatible

#### Properties

- [Documentation](https://tabby.tabbyml.com/docs/administration/answer-engine/)
- [API Reference](https://tabby.tabbyml.com/api/)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Tabby Doc Ingestion API

`POST /v1beta/ingestion` - feed your own materials (project docs, technical articles, internal knowledge base entries) into Tabby's knowledge system. Documents are grouped by source, indexed asynchronously, and surfaced as cited context in Answer Engine responses. Supports an optional `ttl` expiry and deletion by source or id.

- **Human URL:** [https://www.tabbyml.com/blog/doc-ingestion-api](https://www.tabbyml.com/blog/doc-ingestion-api)
- **Base URL:** `http://localhost:8080`

#### Tags

- Answer Engine
- Knowledge Base
- RAG
- Search

#### Properties

- [Documentation](https://www.tabbyml.com/blog/doc-ingestion-api)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Tabby Models API

`GET /v1beta/models` - returns the model registry configured on the Tabby server, listing the completion and chat models currently loaded and available to clients.

- **Human URL:** [https://tabby.tabbyml.com/api/](https://tabby.tabbyml.com/api/)
- **Base URL:** `http://localhost:8080`

#### Tags

- Models
- Registry
- Catalog

#### Properties

- [Documentation](https://tabby.tabbyml.com/docs/references/models-http-api/openai/)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Tabby Health API

`GET /v1/health` - reports the server's runtime configuration and readiness, including the completion model, device, chat model, chat device, and webserver settings. `GET /v1beta/server_setting` exposes additional server settings. Used by IDE clients and orchestration to confirm the instance is up.

- **Human URL:** [https://tabby.tabbyml.com/api/](https://tabby.tabbyml.com/api/)
- **Base URL:** `http://localhost:8080`

#### Tags

- Health
- Status
- Monitoring

#### Properties

- [Documentation](https://tabby.tabbyml.com/docs/welcome/)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Tabby Events API

`POST /v1/events` - logs completion-acceptance and other client telemetry events (LogEventRequest) so a self-hosted deployment can measure suggestion quality and usage locally, without sending data to any third party.

- **Human URL:** [https://tabby.tabbyml.com/api/](https://tabby.tabbyml.com/api/)
- **Base URL:** `http://localhost:8080`

#### Tags

- Events
- Telemetry
- Logging

#### Properties

- [Documentation](https://tabby.tabbyml.com/docs/welcome/)
- [OpenAPI](openapi/tabby-ml-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [GitHub Organization](https://github.com/TabbyML)
- [LinkedIn](https://www.linkedin.com/company/tabbyml)
- [Website](https://www.tabbyml.com)
- [Documentation](https://tabby.tabbyml.com/docs/welcome/)
- [Plans](plans/tabby-ml-plans-pricing.yml)
- [Rate Limits](rate-limits/tabby-ml-rate-limits.yml)
- [Fin Ops](finops/tabby-ml-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
