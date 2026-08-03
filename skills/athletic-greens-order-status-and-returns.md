---
name: Check an AG1 order and request a return
description: Use AG1's OAuth-protected Customer Account MCP server to look up order
  status, read store credit balances, and file a return request on behalf of a
  signed-in AG1 customer.
api: https://account.drinkag1.com/customer/api/mcp
transport: MCP over HTTP (JSON-RPC 2.0)
auth: OAuth 2.0 authorization code + PKCE (Shopify customer accounts), scope
  customer-account-mcp-api:full
operations: [get_most_recent_order_status, get_order_status, get_store_credit_balances,
  request_return]
---

# Check an AG1 order and request a return

AG1 subscriptions and orders live behind Shopify customer accounts. `tools/list` on this
server answers anonymously, but every tool call is customer-scoped and needs a bearer
token.

## 1. Get a token

Discovery: `https://account.drinkag1.com/.well-known/openid-configuration`

- issuer: `https://shopify.com/authentication/15234600`
- authorize: `https://account.drinkag1.com/authentication/oauth/authorize`
- token: `https://account.drinkag1.com/authentication/oauth/token`
- PKCE: `S256` (required — only `S256` is advertised)
- grants: `authorization_code`, `refresh_token`, `urn:ietf:params:oauth:grant-type:jwt-bearer`
- scopes to request: `openid email customer-account-mcp-api:full`

Send the token as `Authorization: Bearer <token>` — the protected-resource metadata
advertises `bearer_methods_supported: ["header"]` only.

## 2. Check the order

Most recent order, no arguments:

```
POST https://account.drinkag1.com/customer/api/mcp
Authorization: Bearer <token>

{"jsonrpc":"2.0","id":1,"method":"tools/call",
 "params":{"name":"get_most_recent_order_status","arguments":{}}}
```

A specific order:

```
{"jsonrpc":"2.0","id":2,"method":"tools/call",
 "params":{"name":"get_order_status","arguments":{"order_number":"<order number>"}}}
```

`order_number` is required — it is the human-facing number from the buyer's confirmation
email, not the internal order id.

## 3. Store credit

```
{"jsonrpc":"2.0","id":3,"method":"tools/call",
 "params":{"name":"get_store_credit_balances","arguments":{}}}
```

Returns balances only if the customer has any; an empty result is a valid answer, not an
error.

## 4. Request a return

```
{"jsonrpc":"2.0","id":4,"method":"tools/call",
 "params":{"name":"request_return","arguments":{
   "order_id":"<order id>",
   "order_number":"<order number>",
   "line_items":[{"line_item_id":"<id>","quantity":1}]}}}
```

`line_items` is the only required argument, but supply the order identifiers you have.
Confirm the buyer's intent before calling — this is a write against their account.

Check the refund window with `search_shop_policies_and_faqs` on the storefront MCP server
(`https://shop.drinkag1.com/api/mcp`) or read
`https://shop.drinkag1.com/policies/refund-policy` before promising an outcome.

## Conventions and failure modes

- Errors are JSON-RPC error objects; a missing/expired token surfaces as an
  authorization failure rather than a Problem Details document.
- There is no idempotency key on this surface — do not blind-retry `request_return`.
  Re-read with `get_order_status` first.
- Responses carry `x-request-id`; include it in any support escalation to
  `support@drinkag1.com`.
