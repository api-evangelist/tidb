# TiDB

TiDB is an open-source, distributed SQL database developed by PingCAP that supports both OLTP and OLAP workloads (HTAP) on a single platform. TiDB Cloud is the fully managed cloud service offering, providing Serverless and Dedicated tiers with built-in scaling, high availability, and MySQL compatibility. PingCAP provides a developer platform with REST APIs for managing cloud infrastructure, accessing data, and querying databases using AI-powered natural language interfaces.

**Website:** [https://www.pingcap.com](https://www.pingcap.com)  
**Cloud Portal:** [https://tidbcloud.com](https://tidbcloud.com)  
**Documentation:** [https://docs.pingcap.com](https://docs.pingcap.com)

## APIs

| API | Description | Docs |
|-----|-------------|------|
| TiDB Cloud API | Cluster, backup, import, and billing management | [Docs](https://docs.pingcap.com/tidbcloud/api-overview/) |
| TiDB Cloud Data Service API | Custom SQL-backed API endpoints via Data Apps | [Docs](https://docs.pingcap.com/tidbcloud/data-service-overview/) |
| TiDB Cloud Chat2Query API | AI-powered natural language to SQL execution | [Docs](https://docs.pingcap.com/tidbcloud/use-chat2query-api/) |
| TiDB HTTP API | Self-managed node administration and monitoring | [Docs](https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md) |

## OpenAPI Specifications

| Spec | Path |
|------|------|
| TiDB Cloud API | [openapi/tidb-cloud-api-openapi.yml](openapi/tidb-cloud-api-openapi.yml) |
| TiDB Cloud Data Service API | [openapi/tidb-cloud-data-service-openapi.yml](openapi/tidb-cloud-data-service-openapi.yml) |
| TiDB Cloud Chat2Query API | [openapi/tidb-cloud-chat2query-openapi.yml](openapi/tidb-cloud-chat2query-openapi.yml) |
| TiDB HTTP API | [openapi/tidb-http-api-openapi.yml](openapi/tidb-http-api-openapi.yml) |

## JSON Schemas

| Schema | Path |
|--------|------|
| TiDB Cluster | [json-schema/tidb-cluster-schema.json](json-schema/tidb-cluster-schema.json) |
| TiDB Data Service | [json-schema/tidb-data-service-schema.json](json-schema/tidb-data-service-schema.json) |

## JSON Structure

| Structure | Path |
|-----------|------|
| TiDB Cluster Structure | [json-structure/tidb-cluster-structure.json](json-structure/tidb-cluster-structure.json) |

## JSON-LD

| Context | Path |
|---------|------|
| TiDB Context | [json-ld/tidb-context.jsonld](json-ld/tidb-context.jsonld) |

## Examples

| Example | Path |
|---------|------|
| Cloud API List Clusters | [examples/tidb-cloud-api-list-clusters-example.json](examples/tidb-cloud-api-list-clusters-example.json) |
| Chat2Query Execute | [examples/tidb-cloud-chat2query-example.json](examples/tidb-cloud-chat2query-example.json) |
| HTTP API Get Status | [examples/tidb-http-api-get-status-example.json](examples/tidb-http-api-get-status-example.json) |

## Spectral Rules

| Ruleset | Path |
|---------|------|
| TiDB API Rules | [rules/tidb-rules.yml](rules/tidb-rules.yml) |

## Naftiko Capabilities

### Shared API Definitions

| API | Path |
|-----|------|
| TiDB Cloud API | [capabilities/shared/tidb-cloud-api.yaml](capabilities/shared/tidb-cloud-api.yaml) |
| TiDB Data Service | [capabilities/shared/tidb-data-service.yaml](capabilities/shared/tidb-data-service.yaml) |

### Workflow Capabilities

| Workflow | APIs | Description |
|----------|------|-------------|
| [Database Operations](capabilities/database-operations.yaml) | Cloud API + Data Service | Cluster management, backups, imports, and AI-assisted SQL queries |

## Vocabulary

| Vocabulary | Path |
|------------|------|
| TiDB Vocabulary | [vocabulary/tidb-vocabulary.yml](vocabulary/tidb-vocabulary.yml) |
