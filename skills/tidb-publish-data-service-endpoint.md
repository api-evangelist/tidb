---
name: tidb-publish-data-service-endpoint
description: Turn a SQL query into a callable HTTPS endpoint with TiDB Cloud Data Service — create the
  Data App, link a cluster, define and test the endpoint, deploy it, and issue its API key.
api: TiDB Cloud Data Service API
spec: openapi/_original/tidb-cloud-dataservice-v1beta1-openapi-original.json
host: https://dataservice.tidbapi.com
operations:
  - DataApp_CreateDataApp
  - DataSource_CreateDataSource
  - Endpoint_CreateEndpoint
  - Endpoint_TestEndpoint
  - Deployment_CreateDeployment
  - APIKey_CreateApiKey
  - APISpecification_GetApiSpec
  - Endpoint_UpdateEndpoint
  - Endpoint_DeleteEndpoint
  - DataApp_DeleteDataApp
generated: '2026-09-17'
method: generated
source: openapi/_original/tidb-cloud-dataservice-v1beta1-openapi-original.json +
  data-model/tidb-data-model.yml + conventions/tidb-conventions.yml
---

# Publish a SQL query as an HTTPS endpoint

Data Service is the one place in TiDB Cloud where the control plane reaches into the data plane: you write
SQL, and TiDB Cloud publishes it as a REST endpoint under `data.tidbcloud.com` with its own OpenAPI
document and its own API keys.

## Steps

1. **Create the Data App.** `POST /v1beta1/dataApps` (`DataApp_CreateDataApp`). Capture `dataAppId`.
2. **Link a cluster as a data source.**
   `POST /v1beta1/dataApps/{dataAppId}/dataSources` (`DataSource_CreateDataSource`). The data source *is*
   a cluster, which is why the read and delete operations for it are keyed on `{clusterId}`, not on a
   separate data-source id.
3. **Define the endpoint.**
   `POST /v1beta1/dataApps/{dataAppId}/endpoints` (`Endpoint_CreateEndpoint`) with the HTTP method, the
   path, the SQL template and its parameters.
4. **Test it before shipping.** `POST /v1beta1/{endpoint.name}/test` (`Endpoint_TestEndpoint`). This is the
   nearest thing to a dry run anywhere in the TiDB Cloud surface — use it.
5. **Deploy it.**
   `POST /v1beta1/dataApps/{dataAppId}/deployments` (`Deployment_CreateDeployment`). An endpoint is not
   callable until it is deployed. Check with `Deployment_GetDeployment`.
6. **Issue a key for callers.**
   `POST /v1beta1/dataApps/{dataAppId}/apiKeys` (`APIKey_CreateApiKey`). This is a **Data App** API key —
   a different credential from the organization API key you used to make all of the calls above. Do not
   confuse the two.
7. **Hand out the contract.**
   `GET /v1beta1/dataApps/{dataAppId}/apiSpec` (`APISpecification_GetApiSpec`) returns the generated
   OpenAPI document for the Data App, which is what a consumer should generate a client from.

## Path parameter warning

Read the paths carefully: `Endpoint_UpdateEndpoint`, `Endpoint_GetEndpoint` and `Endpoint_DeleteEndpoint`
are all published at `/v1beta1/dataApps/{endpoint.name}` — the endpoint's **name**, in the position where
every sibling operation puts a `dataAppId`. Building that URL from the Data App id will address the wrong
resource.

## Undoing it

- `Endpoint_DeleteEndpoint` removes an endpoint; `DataApp_DeleteDataApp` removes the whole app and, with
  it, its endpoints and keys. Neither has a published undo window.
- `APIKey_DeleteApiKey` revokes a caller's key immediately.
- A deployment is not reversible — redeploy a corrected endpoint rather than looking for a rollback
  operation, because none is published.

## Rate limits

The management calls above share the 100 requests/minute per organization API key budget. The published
endpoints you create are separate. Note that **Chat2Query**, the AI Data App, is limited to **100 requests
per day per Data App** — two orders of magnitude tighter — and that is the limit that will bite an agent.
