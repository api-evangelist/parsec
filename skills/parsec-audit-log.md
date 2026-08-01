---
name: Pull the team audit log
description: Retrieve and page through Parsec team audit-log events within a time window.
api: openapi/parsec-teams-openapi.yml
operations: [listAuditLogEvents]
---

# Pull the team audit log

## Auth
Send `Authorization: Bearer YOUR_API_KEY`. Requires the **Access Audit Log**
permission.

## Steps
1. **Query events** with `listAuditLogEvents`
   (`GET /v2/teams/{teamID}/events`), passing `start_at` and `end_at` (RFC 3339),
   plus optional `user_id`, `event_names`, and `limit`.
2. **Page** through results with the `cursor` / `after` cursor parameters until the
   window is exhausted. Set `Accept-Encoding: gzip` for large exports.
3. This endpoint is rate limited to **50 requests / 5 minutes**; on `429` back off
   for 5 minutes before resuming.

## Notes
- The `/v1/teams/{teamID}/events` endpoint (`getAuditLogEvents`) is the older
  variant; prefer v2 for cursor pagination and gzip.
