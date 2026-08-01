---
name: Source a candidate and tag them
description: Look up a candidate on the Phenom platform and apply a tag for downstream workflows.
api: openapi/phenom-platform-openapi.yml
operations: [getCandidate, createTag]
---

# Source a candidate and tag them

Use the Phenom platform to fetch a candidate record and apply a tag.

## Auth
- Supply a bearer token in the `Authorization` header on every request.
- Supply the acting user's id in the `x-ph-userId` header (required on candidate and tag operations).
- Set `Content-type: application/json` and `Accept: application/json`.

## Steps
1. **Find the candidate** — call `getCandidate` (`GET /candidates-api/v2/candidates`) with one of `candidateId`, `email`, `atsId`, or `linkedInProfileUrl` as a query parameter. The response `data` object carries `candidateId`, name fields, `company`, and `employeeId`.
2. **Create/apply a tag** — call `createTag` (`POST /tags-api/v1/tags`) with body `{ "tagName": "<tag>" }` and the same `x-ph-userId` header. A `400` is returned if the tag name or headers are missing.

## Errors
All 4xx/5xx responses use the standard envelope `{ status, message }` (see errors/phenom-error-codes.yml). There is no documented idempotency key — do not assume retries are deduplicated.
