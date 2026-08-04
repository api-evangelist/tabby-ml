# Tabby (tabby-ml)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
