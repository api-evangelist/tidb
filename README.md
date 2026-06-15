# tidb (tidb)

TiDB is an open-source distributed SQL database that supports Hybrid Transactional and Analytical Processing workloads, with horizontal scalability, strong consistency, and high availability.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/tidb/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/tidb/refs/heads/main/apis.yml)

## Timestamps

- **Modified:** 2026-05-19

## APIs

### TiDB Cloud API

The TiDB Cloud API is a REST interface that provides programmatic access to manage administrative objects within TiDB Cloud. It supports managing projects, clusters, backups, restores, data imports, billing, and private endpoint connections across both TiDB Cloud Serverless and TiDB Cloud Dedicated tiers. The API uses digest authentication with public and private API keys and returns JSON-formatted responses.

- **Human URL:** [https://docs.pingcap.com/tidbcloud/api-overview/](https://docs.pingcap.com/tidbcloud/api-overview/)
- **Base URL:** `https://api.tidbcloud.com`

#### Tags

- Cloud
- Cluster Management
- Database
- Distributed SQL

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/api-overview/)
- [Documentation](https://docs.pingcap.com/tidbcloud/api/v1beta/)
- [OpenAPI](openapi/tidb-cloud-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tidb-cloud-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tidb-cloud-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/tidb-cluster-schema.json) — [JSON Schema](https://json-schema.org/specification)

### TiDB Cloud Data Service API

TiDB Cloud Data Service enables developers to access TiDB Cloud data via HTTPS requests using custom API endpoints backed by SQL queries. Developers define endpoints within a Data App, specifying the HTTP method, path, and the SQL logic that the endpoint executes against a linked TiDB Cloud cluster. Endpoints support GET, POST, PUT, and DELETE methods, return JSON-formatted results, and can be configured with pagination, rate limiting, and caching.

- **Human URL:** [https://docs.pingcap.com/tidbcloud/data-service-overview/](https://docs.pingcap.com/tidbcloud/data-service-overview/)
- **Base URL:** `https://data.tidbcloud.com`

#### Tags

- Cloud
- Data Access
- Database
- REST
- Serverless

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/data-service-overview/)
- [Documentation](https://docs.pingcap.com/tidbcloud/data-service-get-started/)
- [OpenAPI](openapi/tidb-cloud-data-service-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tidb-cloud-data-service.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tidb-cloud-data-service.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/tidb-data-service-schema.json) — [JSON Schema](https://json-schema.org/specification)

### TiDB Cloud Chat2Query API

The TiDB Cloud Chat2Query API is an AI-powered interface that allows developers to generate and execute SQL statements against TiDB Cloud clusters using natural language instructions. It is exposed as a special Data App within TiDB Cloud and authenticated via API keys scoped to the Chat2Query Data App.

- **Human URL:** [https://docs.pingcap.com/tidbcloud/use-chat2query-api/](https://docs.pingcap.com/tidbcloud/use-chat2query-api/)
- **Base URL:** `https://data.tidbcloud.com`

#### Tags

- AI
- Cloud
- Database
- Natural Language
- SQL Generation

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/use-chat2query-api/)
- [OpenAPI](openapi/tidb-cloud-chat2query-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tidb-cloud-chat2query.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tidb-cloud-chat2query.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### TiDB HTTP API

The TiDB HTTP API is a built-in administrative interface available on self-managed TiDB server instances, accessible on port 10080 by default. It exposes endpoints for retrieving server status, database and table schema information, region metadata, MVCC key details, DDL job history, and hot region data. Operators and monitoring systems use this API to inspect the internal state of a running TiDB node, integrate with observability tooling, and troubleshoot distributed SQL execution.

- **Human URL:** [https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md](https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md)
- **Base URL:** `http://localhost:10080`

#### Tags

- Database
- Monitoring
- Operations
- Self-Managed
- Status

#### Properties

- [Documentation](https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md)
- [Documentation](https://docs.pingcap.com/tidb/stable/tidb-monitoring-api/)
- [OpenAPI](openapi/tidb-http-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/tidb-http-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/tidb-http-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/pingcap)
- [JSON-LD](json-ld/tidb-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [JSON Schema](json-schema/tidb-cluster-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/tidb-data-service-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [Spectral Rules](rules/tidb-rules.yml) — [Spectral](https://docs.stoplight.io/docs/spectral)
- [Vocabulary](vocabulary/tidb-vocabulary.yml)
