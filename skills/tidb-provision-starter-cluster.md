---
name: tidb-provision-starter-cluster
description: Create, inspect and tear down a TiDB Cloud Starter or Essential instance through the TiDB
  Cloud Starter and Essential API (v1beta1), including how to pick a region first and how to undo.
api: TiDB Cloud Starter and Essential API
spec: openapi/_original/tidb-cloud-starter-essential-v1beta1-openapi-original.json
host: https://serverless.tidbapi.com/v1beta1
operations:
  - ClusterService_ListRegions
  - ClusterService_CreateCluster
  - ClusterService_GetCluster
  - ClusterService_ListClusters
  - ClusterService_PartialUpdateCluster
  - ClusterService_DeleteCluster
generated: '2026-09-17'
method: generated
source: openapi/_original/tidb-cloud-starter-essential-v1beta1-openapi-original.json +
  conventions/tidb-conventions.yml + errors/tidb-problem-types.yml
---

# Provision a TiDB Cloud Starter or Essential instance

## Before you start

- Authenticate with **HTTP Digest**, not a bearer token. The username is the API key's public key and the
  password is the private key: `curl --digest --user 'PUBLIC:PRIVATE'`. The published spec declares no
  `securityDefinitions`, so a generated client will not wire this for you.
- Keys are created at <https://tidbcloud.com/org-settings/api-keys>.
- You get **100 requests per minute per key**. Read `X-Ratelimit-Remaining-Minute`; on `429` wait
  `X-Ratelimit-Reset` seconds. There is no `Retry-After`.
- **There is no idempotency key.** A retried `ClusterService_CreateCluster` creates a second instance and
  bills for it. Guard creates yourself.

## Steps

1. **Pick a region.** `GET /regions` (`ClusterService_ListRegions`) and choose a region name from the
   response. Do not hard-code one; availability differs by cloud provider and plan.
2. **Create the instance.** `POST /clusters` (`ClusterService_CreateCluster`) with the display name, the
   region, and the spending limit if you want one. Capture `clusterId` from the response — every later
   call needs it.
3. **Wait for it to be usable.** Poll `GET /clusters/{clusterId}` (`ClusterService_GetCluster`) until the
   state reports the instance is ready. Poll on a backoff; the 100/min budget is shared with everything
   else you are doing.
4. **Confirm it is in the list.** `GET /clusters` (`ClusterService_ListClusters`). Page with `pageSize`
   and `pageToken`, and follow `nextPageToken` — this API uses token pagination, unlike the older v1beta
   API which uses `page`/`page_size`.
5. **Change it later.** `PATCH /clusters/{cluster.clusterId}` (`ClusterService_PartialUpdateCluster`).
   Note the path parameter is spelled `cluster.clusterId` on this operation and plain `clusterId` on the
   others — a real quirk of the gateway, not a typo.

## Undoing it

- `DELETE /clusters/{clusterId}` (`ClusterService_DeleteCluster`) is the reversal of step 2.
- **Deletion has no published undo window.** PingCAP documents no soft-delete or retention period for a
  deleted Starter or Essential instance. Treat delete as final and take an export first
  (`ExportService_CreateExport`) if the data matters.
- Do not reach for `ClusterService_PauseCluster` here — pause/resume exist on the **Dedicated** API
  (`dedicated.tidbapi.com`), not on this one.

## Errors

| Status | What it means here |
|---|---|
| 400 | Bad region name, or a field failed validation. Read `message`; field detail is in `details[]`. |
| 401 | Digest was not negotiated, or the key pair is wrong. |
| 403 | The key is valid but lacks the role for this organization or project. |
| 429 | Rate limit. Back off on `X-Ratelimit-Reset`. |

The error body is a `google.rpc.Status` — `{code, message, details[]}` — and `code` is a
**google.rpc.Code, not the HTTP status**. It is not RFC 9457 and there is no `request-id` header to quote
to support, so log the `clusterId` and the timestamp yourself.
