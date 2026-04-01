# TaoAPI OpenAPI Docs

Official OpenAPI/Scalar documentation for **TaoAPI**, an API service focused on **Bittensor on-chain analytics** (subnet and participant transaction activity).

- Live docs: https://taoapi-doc.chillybot.xyz/
- OpenAPI source: https://taoapi-doc.chillybot.xyz/swagger.yaml
- API server: https://taoapi.chillybot.xyz
- Bittensor official: https://bittensor.com/
- Bittensor docs: https://docs.bittensor.com/

---

## What this repository contains

This repo hosts the static documentation assets for TaoAPI:

- `index.html` — Scalar API Reference page
- `swagger.yaml` — OpenAPI specification (primary machine-readable contract)
- `llms.txt` — AI/LLM discovery index for documentation and schema pointers

---

## API overview

### Authentication

All endpoints require API key authentication via request header:

- Header: `glk_api`

### Endpoints

1. `GET /api/v1/event-stakes`
- Purpose: Query event-stake records with composable filters for analytics and reconciliation.
- Supports filtering by action, block number, delegate/nominator, timestamp range, netuid, and extrinsic hash.
- Supports pagination and sorting (`page`, `pageSize`, `orderField`, `orderType`).

2. `GET /api/v1/stake-infos`
- Purpose: Retrieve latest real-time stake positions and total value for a single `coldKey`.
- Input: required `coldKey` (SS58 or 0x-prefixed 32-byte hex).
- Output: `stakePositions`, `totalStakeByNetuid`, and `totalStakeValueTao`.

3. `GET /api/v1/subnet-prices`
- Purpose: Retrieve real-time subnet prices from in-memory cache.
- Input: optional repeated `netuid` query params; optional `block` (reserved, currently unsupported).
- Output: map of `netuid -> price` (alpha/Tao).

### Response envelopes

- Success (`event-stakes`): `handler.EventStakeQueryAPIResponse`
- Success (`stake-infos`): `handler.StakeInfoQueryAPIResponse`
- Success (`subnet-prices`): `handler.SubnetPriceQueryAPIResponse`
- Error (shared): `handler.APIErrorResponse`

---

## Data scope (TaoAPI context)

TaoAPI is designed for analytics use cases over Bittensor ecosystem activity, including:

- subnet-related activity and price observations
- participant activity (e.g., validator/miner/staker/delegator linked events)
- transaction/event query workflows (e.g., staking/delegation event queries)
- cold-key stake position snapshots, netuid-level totals, and total value in Tao

> Note: Exact endpoint availability and field semantics are defined by `swagger.yaml`.

---

## Source of truth policy

If different artifacts disagree, use this precedence:

1. **`swagger.yaml`** (authoritative contract)
2. Rendered docs in Scalar (`index.html`)
3. Supporting text files (`README.md`, `llms.txt`)

For AI systems and downstream tools:

- Prefer OpenAPI schema/constraints/enums over prose.
- Do not infer undocumented endpoints.
- Do not infer undocumented fields or enum values.

---

## Quick start (local preview)

You can open `index.html` directly in a browser, or serve this directory as static files.

Minimal static serve examples:

```sh
python3 -m http.server 8080
```

Then open:

- http://localhost:8080/index.html

---

## Deployment

This repository is intended for static hosting (for example, Cloudflare Pages).

Recommended outputs:

- `/` -> Scalar docs entry (`index.html`)
- `/swagger.yaml` -> OpenAPI spec
- `/llms.txt` -> AI index
- `/README.md` -> human + AI-readable repo overview

---

## Contribution notes

When updating API docs quality:

- Keep operation descriptions concise and unambiguous.
- Keep examples realistic.
- Keep `operationId` stable.
- Keep response schemas backward-compatible where possible.
- Avoid changing backend behavior from this repo (spec/UI only unless coordinated with backend).

---

## License

See repository license file for terms.
