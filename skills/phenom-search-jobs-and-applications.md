---
name: Search jobs and review applications
description: Search the Phenom job catalog and pull the applications/applicants for a job.
api: openapi/phenom-platform-openapi.yml
operations: [getJobs, getApplications, getApplicantsByJob]
---

# Search jobs and review applications

## Auth
- Bearer token in the `Authorization` header on every request.
- `x-ph-userId` header is required on the applicants operation.
- `Content-type: application/json`, `Accept: application/json`.

## Steps
1. **Search jobs** — call `getJobs` (`GET /jobs-api/v1/jobs`) with optional `jobId`, `locale`, `category`, `siteType`, `offset`, `limit`. The response returns `totalRecordsCount` and a `data[]` of jobs (`applyUrl`, `ats`, `category`, `companyName`).
2. **List applications** — call `getApplications` (`GET /apply/v2/applications`) with `offset`/`limit` to page combined candidate + job records.
3. **Applicants for a job** — call `getApplicantsByJob` (`GET /candidates-api/applications/v1/jobs/{jobId}/applicants`) with path `jobId` and required `from`/`size` query params plus the `x-ph-userId` header. The response paginates via `pagination.{total,size,from}`.

## Conventions
Two pagination styles are used: `offset`/`limit` (jobs, applications) and `from`/`size` (applicants). Errors use the `{ status, message }` envelope (errors/phenom-error-codes.yml).
