---
name: tidb-manage-changefeed
description: Create, pause, resume, scale and delete a TiDB Cloud changefeed — the CDC stream that
  replicates row changes to Kafka, MySQL or object storage — on the Dedicated and Premium APIs.
api: [TiDB Cloud Dedicated API, TiDB Cloud Premium API]
spec:
  - openapi/_original/tidb-cloud-dedicated-v1beta1-openapi-original.json
  - openapi/_original/tidb-cloud-premium-v1beta2-openapi-original.json
operations:
  - ListChangefeedRCUs
  - CreateChangefeed
  - ListChangefeeds
  - GetChangefeed
  - PauseChangefeed
  - ResumeChangefeed
  - ScaleChangefeed
  - EditChangefeedDownstreamConfig
  - DeleteChangefeed
generated: '2026-09-17'
method: generated
source: openapi/_original/tidb-cloud-dedicated-v1beta1-openapi-original.json +
  asyncapi/tidb-webhooks.yml + conventions/tidb-conventions.yml
---

# Manage a TiDB Cloud changefeed

Changefeeds are TiDB Cloud's change-data-capture streams. They were added to the REST surface recently —
Dedicated (v1beta1) on 2026-07-07 and Premium (v1beta2) on 2026-09-08 — and the same operationIds are used
on both hosts.

Downstreams: Apache Kafka, MySQL, Amazon S3, Google Cloud Storage, Azure Blob Storage (Dedicated) and
Alibaba Cloud OSS (Premium).

## A quirk worth knowing first

Changefeeds are addressed at the **root** of the API — `/changefeeds/{changefeedId}` — not nested under
their cluster. The cluster is named inside the changefeed's upstream configuration in the request body. So
you cannot enumerate one cluster's changefeeds by path; list them all and filter.

## Steps

1. **Size it.** `GET /changefeedRCUs` (`ListChangefeedRCUs`) to see the available capacity units before
   choosing one.
2. **Create it.** `POST /changefeeds` (`CreateChangefeed`) with the upstream cluster, the tables to
   replicate, the downstream sink and its credentials, and the RCU size. Capture `changefeedId`.
3. **Check it.** `GET /changefeeds/{changefeedId}` (`GetChangefeed`). The status enum is what your alerting
   should read — `FAILED` and `WARNING` are both published alert conditions.
4. **Adjust.** `POST /changefeeds/{changefeedId}:scale` (`ScaleChangefeed`) to change RCUs;
   `POST /changefeeds/{changefeedId}:editDownstreamConfig` (`EditChangefeedDownstreamConfig`) to change
   the sink.

## Undoing it

- `POST /changefeeds/{changefeedId}:pause` (`PauseChangefeed`) and
  `POST /changefeeds/{changefeedId}:resume` (`ResumeChangefeed`) are a true reversible pair — pause when
  the downstream is unhealthy, resume when it is back.
- `DELETE /changefeeds/{changefeedId}` (`DeleteChangefeed`) is final; there is no published undo and no
  stated retention on a deleted changefeed's checkpoint.
- **Prefer pause over delete** when you are not sure. Pausing a paused changefeed is a no-op, so pause is
  safe to retry; create is not.

## Monitoring

TiDB Cloud publishes changefeed alert conditions — latency over 600 seconds, status `FAILED`, status
`WARNING` — and can POST them to a generic webhook. But **the webhook subscriber can only be configured in
the console**, not through this API, and the payload format is not published or customizable. If you need
programmatic monitoring, poll `GetChangefeed` rather than waiting on a webhook you cannot verify.
