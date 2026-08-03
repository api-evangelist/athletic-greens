---
name: Find and price AG1 products
description: Search the AG1 store catalog for a buyer and return accurate, localized
  pricing and variant options, using AG1's anonymous Storefront MCP server.
api: https://shop.drinkag1.com/api/mcp
transport: MCP over HTTP (JSON-RPC 2.0)
auth: none
operations: [search_catalog, get_product_details]
---

# Find and price AG1 products

AG1 (drinkag1.com) sells a single flagship product line through a Shopify storefront at
`shop.drinkag1.com`. The store exposes an anonymous MCP server; you do not need a key.

## 1. Confirm the surface (optional, once per session)

```
GET https://shop.drinkag1.com/.well-known/ucp
```

Confirms UCP version `2026-04-08` and that the `dev.ucp.shopping.catalog.search` and
`dev.ucp.shopping.catalog.lookup` capabilities are live.

## 2. Search the catalog

```
POST https://shop.drinkag1.com/api/mcp
Content-Type: application/json

{"jsonrpc":"2.0","id":1,"method":"tools/call",
 "params":{"name":"search_catalog","arguments":{
   "catalog":{
     "query":"AG1 daily greens powder",
     "context":{"address_country":"US","currency":"USD","language":"en"},
     "filters":{"price":{"max":10000}}
   }}}}
```

Rules:

- Pass at least one of `catalog.query` or `catalog.filters` — the tool requires one.
- Always set `catalog.context.address_country` and `catalog.context.currency`. Pricing and
  availability are localized; omitting them yields the store default, not the buyer's.
- Prices in `filters.price.min/max` are **minor units** (5000 = $50.00).
- The first page is deliberately small. Only fetch more when the buyer asks, by passing
  the returned `pagination.cursor` back as `catalog.pagination.cursor`.

## 3. Resolve the exact variant

```
{"jsonrpc":"2.0","id":2,"method":"tools/call",
 "params":{"name":"get_product_details","arguments":{
   "product_id":"<id from search_catalog>",
   "options":{"Size":"30 servings"},
   "country":"US","language":"en"}}}
```

`options` selects a specific variant. AG1's subscription cadences are modelled as selling
plans on the variant — surface the one-time price and the subscription price separately
rather than quoting only the cheapest.

## 4. Answer store questions with the store's own words

For policy or FAQ questions (shipping, refunds, subscription terms), call
`search_shop_policies_and_faqs` with the buyer's question rather than guessing:

```
{"jsonrpc":"2.0","id":3,"method":"tools/call",
 "params":{"name":"search_shop_policies_and_faqs","arguments":{"query":"return window"}}}
```

## Conventions and failure modes

- Responses carry `x-request-id`; log it when reporting a problem.
- The MCP endpoint is rate-limited per IP. Back off on `429`.
- Errors come back as JSON-RPC error objects, not `application/problem+json`.
- Do **not** scrape `drinkag1.com`; that host returns `429` to non-browser clients. Use
  `shop.drinkag1.com` MCP, or the public `GET /products.json` if you only need raw listings.
