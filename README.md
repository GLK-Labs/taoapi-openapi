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

## Data scope (TaoAPI context)

TaoAPI is designed for analytics use cases over Bittensor ecosystem activity, including:

- subnet-related activity
- participant activity (e.g., validator/miner/staker/delegator linked events)
- transaction/event query workflows (e.g., staking/delegation event queries)

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

Minimal static serve example:

```sh
python3 -m http.server 8080
```

Then open:

- http://localhost:8080/index.html

---

## Deployment

This repository is intended for static hosting (for example, Cloudflare Pages).

Recommended outputs:

- `/` → Scalar docs entry (`index.html`)
- `/swagger.yaml` → OpenAPI spec
- `/llms.txt` → AI index
- `/README.md` → human + AI-readable repo overview

---

## Contribution notes

When updating API docs quality:

- Keep operation descriptions concise and unambiguous.
- Keep examples realistic.
- Keep `operationId` stable.
- Avoid changing endpoint behavior from this repo (spec/UI only unless coordinated with backend).

---
  
## License

See repository license file for terms.