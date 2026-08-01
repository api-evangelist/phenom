---
name: Parse a resume and predict skills
description: Extract structured candidate data from a resume, then predict related skills.
api: openapi/phenom-platform-openapi.yml
operations: [parseResume, predictSkills]
---

# Parse a resume and predict skills

Turn a raw resume file into structured candidate data and enrich it with predicted skills.

## Auth
- Bearer token in the `Authorization` header on every request.
- `Content-type: application/json`, `Accept: application/json`.

## Steps
1. **Parse the resume** — call `parseResume` (`POST /parser/resume/v1/parse`) with body `{ "filename": "<name>", "datastream": "<base64>" }`. The response `data` object contains parsed fields (name, contact, education, work experience, skills).
2. **Predict skills** — take the parsed job titles and skills and call `predictSkills` (`POST /prediction/v1/skills`) with body `{ "titles": [...], "skills": [...], "size": <n> }`. The response returns ranked predicted skills.

## Errors
4xx/5xx responses use the standard `{ status, message }` envelope (errors/phenom-error-codes.yml).
