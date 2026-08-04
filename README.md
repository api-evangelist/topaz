# Topaz (topaz)

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

Topaz is an open-source (Apache-2.0) authorizer for fine-grained, policy-based, real-time access control for applications and APIs, maintained by Aserto ([github.com/aserto-dev/topaz](https://github.com/aserto-dev/topaz)). It combines the Open Policy Agent (OPA) decision engine with a built-in Zanzibar-style relationship directory, so you can express authorization as policy-as-code and model RBAC, ReBAC, and ABAC over an object graph of users, groups, resources, and relations.

**Topaz is self-hosted.** You run the authorizer yourself - as a Docker container (`ghcr.io/aserto-dev/topaz`) or a binary, typically as a sidecar or nearby service - and it serves its APIs from your own instance. There is no single public endpoint: the base URL is per-instance. By default the REST gateway listens on `https://localhost:8383`, the authorizer gRPC on `:8282`, the directory gRPC on `:9292`, and a local web Console on `:8080`. (In split deployments the directory REST endpoints may be exposed on `:9393`.) **Aserto** ([aserto.com](https://www.aserto.com/)) is the separate commercial hosted control plane built on Topaz for centrally managing policies, directory data, and decision logs across many deployed authorizers.

Topaz exposes both **gRPC** and **REST** (via the gRPC-gateway). This entry documents the REST surface. There is no public WebSocket API - all APIs are request/response.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/topaz/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/topaz/refs/heads/main/apis.yml)

## Tags

- Access Control
- Authorization
- Fine-Grained Authorization
- Open Source
- RBAC
- ReBAC
- Zanzibar
- OPA
- Policy as Code

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### Topaz Authorizer API

The decision API. `POST /api/v2/authz/is` (allowed/denied for a user, action, and resource), `POST /api/v2/authz/decisiontree` (evaluate many decisions at a policy path in one call), and `POST /api/v2/authz/query` (run an arbitrary Rego/OPA query) - each taking an `identityContext`, `policyContext`, and optional `resourceContext`. `GET /api/v2/policies` lists the OPA policy modules loaded into the authorizer. Served over gRPC (`:8282`) and REST (`:8383`).

- **Human URL:** [https://www.topaz.sh/docs/authorizer-guide/overview](https://www.topaz.sh/docs/authorizer-guide/overview)
- **Base URL:** `https://localhost:8383` (self-hosted; replace with your own instance)

#### Tags

- Access Control
- Authorization
- Fine-Grained Authorization
- Decisions
- OPA

### Topaz Directory Objects API

The Directory v3 object graph. Read a single object by type and id, list objects of a type, and (writer) create/update or delete objects - the users, groups, resources, and other entities decisions are made about. Under `/api/v3/directory/object(s)`.

- **Human URL:** [https://www.topaz.sh/docs/directory/apis](https://www.topaz.sh/docs/directory/apis)
- **Base URL:** `https://localhost:8383` (self-hosted)

#### Tags

- Access Control
- Directory
- Objects
- Zanzibar
- RBAC

### Topaz Directory Relations API

The Directory v3 relationship graph. Get a single relation, list relations, walk the graph, and (writer) create/update or delete relations - the tuples that connect subjects to objects (user X is a member of group Y, group Y owns resource Z). The ReBAC/Zanzibar backbone Topaz evaluates during checks. Under `/api/v3/directory/relation(s)`.

- **Human URL:** [https://www.topaz.sh/docs/directory/apis](https://www.topaz.sh/docs/directory/apis)
- **Base URL:** `https://localhost:8383` (self-hosted)

#### Tags

- Access Control
- Directory
- Relations
- ReBAC
- Zanzibar

### Topaz Directory Checks API

The Directory v3 check surface for graph-based access decisions. `POST /api/v3/directory/check` asks whether a subject has a given relation or permission on an object by traversing the relationship graph; `GET /api/v3/directory/graph` expands the set of subjects or objects reachable through a relation. The data-driven, Zanzibar-style complement to the policy-driven Authorizer `is` API.

- **Human URL:** [https://www.topaz.sh/docs/directory/apis](https://www.topaz.sh/docs/directory/apis)
- **Base URL:** `https://localhost:8383` (self-hosted)

#### Tags

- Access Control
- Authorization
- Fine-Grained Authorization
- Checks
- ReBAC

## Common Properties

- [GitHub Organization](https://github.com/aserto-dev/topaz)
- [LinkedIn](https://www.linkedin.com/company/aserto)
- [Website](https://www.topaz.sh/)
- [Documentation](https://www.topaz.sh/docs)
- [Plans](plans/topaz-plans-pricing.yml)
- [Rate Limits](rate-limits/topaz-rate-limits.yml)
- [Fin Ops](finops/topaz-finops.yml)
- [Source Code](https://github.com/aserto-dev/topaz)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
