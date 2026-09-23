---
name: tidb-import-data
description: Run and supervise a data import into a TiDB Cloud instance, on both the Starter/Essential and
  the Dedicated API, including cancelling one that is going wrong.
api: [TiDB Cloud Starter and Essential API, TiDB Cloud Dedicated API]
spec:
  - openapi/_original/tidb-cloud-starter-essential-v1beta1-openapi-original.json
  - openapi/_original/tidb-cloud-dedicated-v1beta1-openapi-original.json
operations:
  - ImportService_CreateImport
  - ImportService_GetImport
  - ImportService_ListImports
  - ImportService_CancelImport
  - CreateImport
  - GetImport
  - ListImports
  - CancelImport
generated: '2026-09-17'
method: generated
source: openapi/_original/tidb-cloud-*-openapi-original.json + conventions/tidb-conventions.yml
---

# Import data into a TiDB Cloud instance

## Which API you are on matters

The same flow exists twice with **different operationIds and different path parameter names**:

| | Starter / Essential | Dedicated |
|---|---|---|
| Host | `serverless.tidbapi.com/v1beta1` | `dedicated.tidbapi.com/v1beta1` |
| Create | `ImportService_CreateImport` | `CreateImport` |
| Get | `ImportService_GetImport` — `/clusters/{clusterId}/imports/{id}` | `GetImport` — `/clusters/{clusterId}/imports/{importId}` |
| List | `ImportService_ListImports` | `ListImports` |
| Cancel | `ImportService_CancelImport` — `…/imports/{id}:cancel` | `CancelImport` — `…/imports/{importId}:cancel` |

Resolve which one you are on from the cluster's plan before building the URL. The import id is `{id}` on
Starter/Essential and `{importId}` on Dedicated.

> The **v1beta** API (`api.tidbcloud.com`) also has Import operations. They are marked **deprecated** by
> PingCAP's own overview page. Do not build on them.

## Steps

1. **Create the import.** `POST /clusters/{clusterId}/imports` with the source (S3, GCS, Azure Blob or a
   local file, depending on plan), the target database and table, and the file format. Capture the import
   id from the response.
2. **Watch it.** Poll the Get operation. The response carries a phase/status enum
   (`ImportStatusImportTaskPhase` in the Dedicated spec) — drive your state machine off that, not off the
   HTTP status, which is `200` for a running, completed and failed import alike.
3. **List history** with the List operation when you need prior runs.

## Undoing it

- `POST …/imports/{id}:cancel` cancels a **running** import. The contract does not state a deadline beyond
  "while it is still running", so cancel as soon as you decide to.
- **Cancelling does not roll back rows already written.** No operation in the surface reverses a partial
  import. If that matters, import into a **branch** first (see `tidb-branch-and-reset`) and only then
  promote, or take a backup first.

## Guardrails

- No idempotency key. A retried create starts a **second** import against the same tables. Before retrying
  a create that timed out, call the List operation and check whether the first one actually landed.
- 100 requests/minute per API key covers your polling too. Back off — one poll every 10–30 seconds is
  plenty for an import.
