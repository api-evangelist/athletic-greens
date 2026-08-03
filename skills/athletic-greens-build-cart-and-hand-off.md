---
name: Build an AG1 cart and hand off for buyer approval
description: Assemble a cart on AG1's Shopify storefront via MCP - line items, buyer
  identity, delivery address, delivery option, discount and gift card codes - then stop
  and hand the checkout URL to the human for approval. Never completes payment.
api: https://shop.drinkag1.com/api/mcp
transport: MCP over HTTP (JSON-RPC 2.0)
auth: none for cart; checkout completion requires buyer approval
operations: [search_catalog, get_product_details, get_cart, update_cart]
---

# Build an AG1 cart and hand off for buyer approval

**Hard rule first.** AG1's `robots.txt` and `agents.md` both state that checkout, payment
and order placement must not be completed automatically — no scripted form fills, no
browser automation, no end-to-end flow that finalizes payment without an explicit,
contemporaneous human approval step. This skill therefore ends at the checkout URL.

## 1. Pick the variant

Use the `athletic-greens-find-and-price-products` skill (`search_catalog` →
`get_product_details`) to resolve the exact variant id the buyer wants.

## 2. Create or update the cart

`update_cart` is a single fan-out tool. Call it with only the fields you are changing:

```
POST https://shop.drinkag1.com/api/mcp
{"jsonrpc":"2.0","id":1,"method":"tools/call",
 "params":{"name":"update_cart","arguments":{
   "add_items":[{"product_variant_id":"<variant id>","quantity":1}]
 }}}
```

Omit `cart_id` on the first call to start a cart; pass the returned `cart_id` on every
subsequent call.

Fields, and what each one drives:

| argument | effect |
|---|---|
| `add_items` / `update_items` / `remove_line_ids` | line items |
| `buyer_identity` | email, phone, country for the buyer |
| `delivery_addresses_to_add` / `delivery_addresses_to_replace` | shipping address |
| `selected_delivery_options` | shipping method |
| `discount_codes` / `gift_card_codes` | promotions and gift cards |
| `note` | order note |

Note that AG1's store advertises `allows_multi_destination.shipping: false` in its UCP
profile — one shipping destination per cart. Do not attempt a split shipment.

## 3. Read the cart back before you quote

```
{"jsonrpc":"2.0","id":2,"method":"tools/call",
 "params":{"name":"get_cart","arguments":{"cart_id":"<cart id>"}}}
```

`get_cart` returns items, shipping options, discount information and the **checkout url**.
Quote totals from this response — never from your own arithmetic over line prices.

## 4. Hand off

Present the buyer with: the line items, the delivered total from `get_cart`, and the
checkout URL. Stop there. If you need a path that can transact, `agents.md` directs
personal shopping agents to install `https://shop.app/SKILL.md` and route the purchase
through Shop Pay, which enforces buyer approval at the moment of payment.

## Conventions and failure modes

- There is **no idempotency key** on this surface. Cart writes are last-write-wins keyed
  by `cart_id` — re-sending `add_items` after a timeout can double a line. Re-read with
  `get_cart` before retrying a write.
- The UCP endpoint (`/api/ucp/mcp`) is the richer commerce transport (checkout,
  fulfillment, discount, order capabilities) but requires a resolvable UCP agent profile
  URI in `meta.ucp-agent.profile`; without one it returns JSON-RPC `-32001`
  `invalid_profile_url`.
- Back off on `429`. Log `x-request-id` from failed responses.
