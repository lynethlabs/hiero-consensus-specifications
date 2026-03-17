# HCS-25 (Signal): ERC-8004 Feedback Summary (Informative)

## Purpose

Collect ERC-8004 feedback summaries (average rating + volume) for agents registered under ERC-8004 networks.

## Applicability

Applied to ERC-8004 agents. The reference supports:

- EVM ERC-8004 feedback summaries, and
- optional Solana feedback ingestion (devnet).

## Stored fields (example schema)

Stored in `subject.metadata.erc8004FeedbackSummary`:

| Field | Type | Meaning |
| --- | --- | --- |
| `averageScore` | number | Average score `[0,100]` |
| `totalFeedbacks` | number | Feedback count (non-negative integer) |
| `registry` | string | Registry identifier |
| `network` | string | Network identifier |
| `updatedAt` | ISO timestamp | Refresh time |
| `status` | `ok` \| `missing` \| `error` | Signal status (HCS-25 canonical). Omit only if inferrable: absent object ⇒ `missing`; present with valid numeric fields ⇒ `ok`. |
| `sources` | string[] | Optional provenance (e.g., chain id, contract address). |

**Status and provenance:** Implementations MUST assign a canonical status when producing this signal. If the summary object is absent for the subject, the signal status is `missing`. If the object is present and `averageScore`/`totalFeedbacks` are valid, status is typically `ok`; use `error` when ingestion failed or data is invalid. Provenance (e.g., `updatedAt`, optional `sources`) SHOULD be stored so consumers can interpret freshness.

## Production example (Registry Broker; informative)

- Endpoint: `https://hol.org/registry/api/v1/agents/{uaid}`
- Example UAID: `uaid:aid:4H2Rnf4oSM7N6HbFy8Su9qhUSpaE8yyVXoTj8UhXQ2qKfjQQ2CFjutJbJWy8NXKWi9;uid=11155111:724;registry=erc-8004;proto=erc-8004;nativeId=11155111:724`
