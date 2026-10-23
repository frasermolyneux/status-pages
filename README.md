# Status communications

Central incident source for [MX status](https://mxstatus.io) and
[XtremeIdiots status](https://status.xtremeidiots.com).

## Declare an incident

1. Open an issue using the relevant brand's incident template, from the repository
   owner's account or an explicitly trusted maintainer account.
2. Write the public impact and current response in **Public update**. Add the
   matching workload label(s) below. Choose exactly one `severity:degraded` or
   `severity:outage` label; the templates default to degraded.
3. Review the content and affected workloads. An authorized repository maintainer
   adds **`status:published`** to publish it. Without that label it is a private
   draft in the status operations workspace, not a public status incident.

| Brand | Workload labels |
|---|---|
| `site:mx` | `workload:molyneux-me`, `workload:geo-location`, `workload:bishops-bees` |
| `site:xi` | `workload:xi-forums`, `workload:geo-location`, `workload:portal-web`, `workload:portal-repository`, `workload:portal-servers-integration`, `workload:portal-server-events`, `workload:portal-server-agent`, `workload:xi-redirect` |

Workload labels map to approved public components in the status service's
[catalogue](https://github.com/frasermolyneux/platform-status-web/blob/main/src/MX.Platform.Status.Service/catalog.json).
For a cross-brand incident, add both site labels and matching affected workloads
for each brand. Do not use unrelated workloads merely to satisfy validation.
Advanced maintainers can use `component:<public-component-id>` instead.
Unknown, restricted or cross-brand-only attribution is rejected.

## Update, resolve or withdraw

After publication, edits and comments from trusted maintainers are synchronized
automatically, normally within five minutes plus one publication interval.
Comments from other users never become public status updates.
Use a plain-text update; optionally begin the comment with a state header:

```text
state: monitoring
The fix is deployed and we are monitoring recovery.
```

Supported states are `investigating`, `identified`, `monitoring`, `resolved`.
You may also apply one `state:<state>` label for the issue's current state.
Without a state label, the last trusted update selects the active state.
To resolve, close the issue or add `state:resolved`; a resolved comment alone
does not mark an open issue resolved.
When reopening a resolved issue, remove a stale `state:resolved` label.
Closing the issue resolves the incident; reopening makes it active again unless
its state label still explicitly marks it resolved.

Remove `status:published` to withdraw the incident. Remove `status:incident` to
stop importing it. Neither action deletes the service's audit history.
GitHub-managed incidents must be edited here, rather than through the local
incident editor.

The repository owner is trusted by default. Additional trusted authors require
a reviewed service runtime configuration change; a public issue author's
association with the repository is not sufficient. Adding a publish label to an
untrusted author's issue does not approve that author's future edits.

**Everything in this repository is public. Never include private monitoring
evidence, subscription identifiers, credentials or confidential notes.**

## Announcements and monitoring

Use `/ops/evidence` to review monitoring results and prepare an editable incident
draft from an evidence item. Source context remains private; review the public
wording and explicitly choose whether to publish. Manage locally authored
incidents and maintenance at `/ops/incidents`, and banners at `/ops/banners`.
Banners support preview,
publish/withdraw, scheduling and expiry, and are scoped to the current brand.
Azure alerts and public service advisories appear as readable restricted
evidence there; they do not automatically create public incidents.

GitHub or database outages do not interrupt public status reads. The service
retains its last durable publication and reports ingestion errors privately.
During validation, leave test issues unpublished; do not create fake public
outages or announcements.
