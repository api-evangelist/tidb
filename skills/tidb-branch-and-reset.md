---
name: tidb-branch-and-reset
description: Use TiDB Cloud Starter/Essential branches as the safe place to run destructive or unreviewed
  work, then reset or delete the branch — the closest thing this API has to a sandbox.
api: TiDB Cloud Starter and Essential API
spec: openapi/_original/tidb-cloud-starter-essential-v1beta1-openapi-original.json
host: https://serverless.tidbapi.com/v1beta1
operations:
  - BranchService_CreateBranch
  - BranchService_ListBranches
  - BranchService_GetBranch
  - BranchService_ResetBranch
  - BranchService_DeleteBranch
generated: '2026-09-17'
method: generated
source: openapi/_original/tidb-cloud-starter-essential-v1beta1-openapi-original.json +
  sandbox/tidb-sandbox.yml + conventions/tidb-conventions.yml
---

# Branch before you break something

TiDB Cloud has **no test mode**. One API key works against real, billable resources, and there are no test
credentials to switch to. Branches are the available substitute: a branch forks the data of a Starter or
Essential instance so destructive work lands somewhere you can throw away.

## Steps

1. **Create the branch.** `POST /clusters/{clusterId}/branches` (`BranchService_CreateBranch`). Capture
   `branchId`.
2. **Confirm it is ready.** `GET /clusters/{clusterId}/branches/{branchId}` (`BranchService_GetBranch`).
3. **Do the work** against the branch's own connection endpoint over MySQL — or, for an agent, point the
   TiDB MCP Server at it by setting `TIDB_HOST` / `TIDB_USERNAME` / `TIDB_PASSWORD` to the branch's
   credentials before running `uvx --from "pytidb[mcp]" tidb-mcp-server`. Every MCP tool, including
   `db_execute`, then operates on the branch and not on the parent.
4. **Roll back.** `POST /clusters/{clusterId}/branches/{branchId}:reset` (`BranchService_ResetBranch`)
   returns the branch to its parent's state. This is the genuine undo in this surface.
5. **Clean up.** `DELETE /clusters/{clusterId}/branches/{branchId}` (`BranchService_DeleteBranch`).

## What this does not do

- A branch is a **product feature that is billed**, not a free sandbox. It consumes the organization's RU
  and storage allowance.
- Reset has **no published time window** — PingCAP states no retention period for branch history — so do
  not assume you can reset to an arbitrary earlier point. Reset means "back to the parent", nothing finer.
- Branches exist on Starter and Essential only. There is no branch operation on the Dedicated or Premium
  APIs.

## Guardrails

- No idempotency key on create. A retried create makes a second branch.
- List branches (`BranchService_ListBranches`) before creating one in a retry path.
