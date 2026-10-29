# AG1

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AG1 (formerly Athletic Greens) is a direct-to-consumer health and nutrition company founded in December 2010 by Chris Ashenden and headquartered in Carson City, Nevada. It sells a single flagship product - AG1, a daily foundational nutrition powder - on a subscription model through drinkag1.com, and the brand was renamed from Athletic Greens to AG1 in December 2021. Revenue grew from roughly $160M in 2021 to approximately $600M in 2024, with a valuation near $1.2B reported in January 2025, built largely on podcast and creator affiliate marketing. AG1 is a consumer commerce business rather than a developer-facing API provider - it publishes no developer portal, no API reference and no OpenAPI - but its Shopify storefront at shop.drinkag1.com does expose a real, anonymously reachable agentic commerce surface: a Universal Commerce Protocol (UCP 2026-04-08) merchant profile at /.well-known/ucp, a Storefront MCP server at /api/mcp, a UCP/MCP commerce endpoint at /api/ucp/mcp, a Customer Account MCP server at account.drinkag1.com, an introspectable Shopify Storefront GraphQL API, and published agents.md / llms.txt / robots.txt agent instructions. Authentication for customer-scoped surfaces is Shopify customer accounts OAuth 2.0 + OpenID Connect with PKCE.

**Areas:** Company · Consumer · Health · Nutrition · Supplements · Direct to Consumer · E-Commerce · Subscription · Wellness · Agentic Commerce · MCP · Universal Commerce Protocol

## AG1 on APIs.io

Everything profiled for AG1 is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/athletic-greens/](https://apis.io/providers/athletic-greens/)** — or go straight to one of the APIs or properties below.

### APIs (4)

- [AG1 Storefront GraphQL API](https://apis.io/apis/athletic-greens/athletic-greens-storefront-graphql/) — The Shopify Storefront GraphQL API as served from AG1's own storefront host, shop.drinkag1.com. Anonymous schema introspection succeeds, exposing 35 query…
- [AG1 Storefront MCP Server](https://apis.io/apis/athletic-greens/athletic-greens-storefront-mcp/) — Anonymous Model Context Protocol server on AG1's storefront host exposing five tools - search_catalog, get_product_details, get_cart, update_cart and…
- [AG1 UCP Commerce Endpoint](https://apis.io/apis/athletic-greens/athletic-greens-ucp-mcp/) — The Universal Commerce Protocol MCP transport for AG1's store, advertised in the store's /.well-known/ucp merchant profile. Implements the dev.ucp.shopping…
- [AG1 Customer Account MCP Server](https://apis.io/apis/athletic-greens/athletic-greens-customer-account-mcp/) — Model Context Protocol server on AG1's customer account host exposing four order-management tools - get_most_recent_order_status, get_order_status,…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [athletic-greens-mcp.yml](https://apis.io/servers/athletic-greens/athletic-greens-mcp-yml/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Athletic Greens Authentication](https://apis.io/security/athletic-greens/athletic-greens-authentication/)
- [Athletic Greens Domain Security](https://apis.io/security/athletic-greens/athletic-greens-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Athletic Greens Scopes](https://apis.io/scopes/athletic-greens/athletic-greens-scopes/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://drinkag1.com/)
- [Documentation](https://shop.drinkag1.com/agents.md)
- [Sign up](https://drinkag1.com/members)
- [Terms of service](https://drinkag1.com/about-us/terms-and-conditions)
- [Privacy policy](https://drinkag1.com/privacy)

## API Evangelist rating

**Kin Score 24.4** — emerging · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 10.4 |
| Contract governance | 18.2 |
| Operational transparency | 0.0 |
| Developer ergonomics | 28.0 |
| Access clarity | 17.1 |

**Agent readiness 34.2** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | platform (partial credit) |

**Regulatory alignment 29.7** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/athletic-greens/](https://apis.io/providers/athletic-greens/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AG1: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/athletic-greens/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
