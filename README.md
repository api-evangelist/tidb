# TiDB (tidb)
TiDB is an open-source, distributed SQL database developed by PingCAP that supports both OLTP and OLAP workloads on a single platform. TiDB Cloud is the fully managed cloud service offering, providing serverless and dedicated tiers with built-in scaling, high availability, and MySQL compatibility. PingCAP provides a developer platform with REST APIs for managing cloud infrastructure, accessing data, and querying databases using AI-powered natural language interfaces.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/tidb/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags:

 - Database, Cloud, Distributed SQL, AI, Serverless, Cluster Management

## Timestamps

- **Created:** 2026-03-21
- **Modified:** 2026-03-21

## APIs

### TiDB Cloud API
The TiDB Cloud API is a REST interface that provides programmatic access to manage administrative objects within TiDB Cloud. It supports managing projects, clusters, backups, restores, data imports, billing, and private endpoint connections across both TiDB Cloud Serverless and TiDB Cloud Dedicated tiers. The API uses digest authentication with public and private API keys and returns JSON-formatted responses.

**Human URL:** [https://docs.pingcap.com/tidbcloud/api-overview/](https://docs.pingcap.com/tidbcloud/api-overview/)


#### Tags:

 - Database, Cloud, Distributed SQL, Cluster Management

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/api-overview/)
- [Documentation](https://docs.pingcap.com/tidbcloud/api/v1beta/)
- [OpenAPI](openapi/tidb-cloud-api-openapi.yml)

### TiDB Cloud Data Service API
TiDB Cloud Data Service enables developers to access TiDB Cloud data via HTTPS requests using custom API endpoints backed by SQL queries. Developers define endpoints within a Data App, specifying the HTTP method, path, and the SQL logic that the endpoint executes against a linked TiDB Cloud cluster. The service uses a serverless execution model, automatically handling compute resources and scaling without requiring infrastructure management.

**Human URL:** [https://docs.pingcap.com/tidbcloud/data-service-overview/](https://docs.pingcap.com/tidbcloud/data-service-overview/)


#### Tags:

 - Database, Cloud, Data Access, Serverless, REST

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/data-service-overview/)
- [Documentation](https://docs.pingcap.com/tidbcloud/data-service-get-started/)
- [OpenAPI](openapi/tidb-cloud-data-service-openapi.yml)

### TiDB Cloud Chat2Query API
The TiDB Cloud Chat2Query API is an AI-powered interface that allows developers to generate and execute SQL statements against TiDB Cloud clusters using natural language instructions. It is exposed as a special Data App within TiDB Cloud and provides endpoints for generating data summaries, translating natural language prompts into SQL, and executing the resulting queries. It is intended for building AI-assisted data exploration tools, reporting interfaces, and applications that need to query structured data without requiring users to write SQL directly.

**Human URL:** [https://docs.pingcap.com/tidbcloud/use-chat2query-api/](https://docs.pingcap.com/tidbcloud/use-chat2query-api/)


#### Tags:

 - Database, AI, SQL Generation, Natural Language, Cloud

#### Properties

- [Documentation](https://docs.pingcap.com/tidbcloud/use-chat2query-api/)
- [OpenAPI](openapi/tidb-cloud-chat2query-openapi.yml)

### TiDB HTTP API
The TiDB HTTP API is a built-in administrative interface available on self-managed TiDB server instances, accessible on port 10080 by default. It exposes endpoints for retrieving server status, database and table schema information, region metadata, MVCC key details, DDL job history, and hot region data. Operators and monitoring systems use this API to inspect the internal state of a running TiDB node, integrate with observability tooling, and troubleshoot distributed SQL execution.

**Human URL:** [https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md](https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md)


#### Tags:

 - Database, Monitoring, Self-Managed, Operations, Status

#### Properties

- [Documentation](https://github.com/pingcap/tidb/blob/master/docs/tidb_http_api.md)
- [Documentation](https://docs.pingcap.com/tidb/stable/tidb-monitoring-api/)
- [OpenAPI](openapi/tidb-http-api-openapi.yml)

## Common Properties

- [Portal](https://tidbcloud.com/)
- [Documentation](https://docs.pingcap.com/tidbcloud/overview)
- [Website](https://www.pingcap.com/)
- [PrivacyPolicy](https://www.pingcap.com/privacy-policy/)
- [TermsOfService](https://www.pingcap.com/terms-of-service/)
- [Support](https://tidbcloud.com/support)
- [Blog](https://www.pingcap.com/blog/)
- [Login](https://tidbcloud.com/console/login)

## Maintainers

**FN:** API Evangelist

**Email:** info@apievangelist.com
