# Paste-ready metadata for OSF Preprints and other archives

## GLINR-WP-2026-101: Restore Is the Product

- Title: Restore Is the Product
- Subtitle: Backups you can prove: measuring RPO and RTO, mapping threats to surviving copies, and testing restores before you need them
- Authors: Gagan Deep Singh (ORCID 0009-0002-0579-6514), GLINR Studios
- License: CC BY 4.0
- Subject: Engineering, then Computer Engineering (or Physical Sciences and Mathematics, then Computer Sciences)
- Keywords (tags): backups, restore testing, RPO, RTO, failure domains, immutable backups, ransomware, disaster recovery, restore drills
- DOI of the Zenodo version: 10.5281/zenodo.24238984
- Paper page: https://glinr.com/research/2026-101-backups-you-can-restore
- Supplemental repository: https://github.com/glincker/wp-2026-101-backup-restore-testing
- PDF to upload: guides/papers/2026-101-backups-you-can-restore/build/2026-101-backups-you-can-restore.pdf
- Conflict of interest: The author builds Levelrail, a self-hosted deployment platform, through GLINR Studios. No product is recommended in this paper. Tools appear only as test subjects, with versions.
- Funding: No external funding. This is the author's own open-source work, paid for by the author.

Abstract:

A backup job reports that it ran. It does not report that your data can come back. In tests on one laptop, four backup jobs that saved nothing useful all exited 0, flipped bytes in a restic repository passed the default check, and a one-database restore that took 0.21 s still needed four rounds of fixes before the application's database role could log in. This paper treats a backup as a system you measure, starting from the restore: four gates a copy must pass, public incidents mapped to the gate each one failed, the 3-2-1-1-0 rule recast as a table of failure domains, and a method to declare and then measure RPO and RTO on a clean host. Only the machine side was timed, on one laptop; no full application was started and no isolated-environment drill was run. It closes with a runbook and an evidence checklist. The scripts and raw results are published.

## GLINR-WP-2026-301: DNS in Production

- Title: DNS in Production
- Subtitle: TTLs, failover and failure modes, measured in two resolvers and four client runtimes
- Authors: Gagan Deep Singh (ORCID 0009-0002-0579-6514), GLINR Studios
- License: CC BY 4.0
- Subject: Engineering, then Computer Engineering (or Physical Sciences and Mathematics, then Computer Sciences)
- Keywords (tags): DNS TTL, DNS failover, negative caching, serve-stale, resolver TTL clamping, DNS cutover time, client DNS caching, delegation, RFC 2308, RFC 8767
- DOI of the Zenodo version: 10.5281/zenodo.24238986
- Paper page: https://glinr.com/research/2026-301-dns-in-production
- Supplemental repository: https://github.com/glincker/wp-2026-301-dns-failover-ttl-testing
- PDF to upload: guides/papers/2026-301-dns-in-production/build/2026-301-dns-in-production.pdf
- Conflict of interest: The author builds Levelrail, a self-hosted deployment platform, through GLINR Studios. No product is recommended in this paper. Resolvers and providers appear only as test subjects, with versions, or as quoted documentation.
- Funding: No external funding. This is the author's own open-source work, paid for by the author.

Abstract:

A DNS change takes effect when several independent clocks expire, and the TTL you set is only one of them. This paper measures the others in a Docker lab with two resolvers, Unbound 1.22.0 and BIND 9.20.30, and four client runtimes: Python, Go, curl and Java. Both resolvers honored configured TTL floors and caps. The cache part of a cutover equaled the remaining TTL to within about 1 s, and lowering a TTL only at the moment of change barely helped. Serve-stale kept answering for the configured window in Unbound, and intermittently in BIND. Client runtimes differed widely in how long they kept the old address and in whether they tried a second address when the first was dead. The paper reads the 2025 AWS DynamoDB outage against these clocks, and ends with a TTL policy, a pre-change runbook and a monitoring checklist. The authoritative server is a custom lab server, so every figure is indicative and a lower bound for a real cutover. The harness and raw results are published.

## GLINR-WP-2026-501: Zero-Downtime Migrations, Tested

- Title: Zero-Downtime Migrations, Tested
- Subtitle: Lock queues, expand and contract and rolling restarts, measured on Postgres 16 and 17 and nginx
- Authors: Gagan Deep Singh (ORCID 0009-0002-0579-6514), GLINR Studios
- License: CC BY 4.0
- Subject: Engineering, then Computer Engineering (or Physical Sciences and Mathematics, then Computer Sciences)
- Keywords (tags): zero downtime migration, Postgres lock queue, lock_timeout retry, expand and contract, CREATE INDEX CONCURRENTLY, NOT VALID constraint, rolling restart, connection draining
- DOI of the Zenodo version: pending
- Paper page: https://glinr.com/research/2026-501-zero-downtime-migrations
- Supplemental repository: https://github.com/glincker/wp-2026-501-zero-downtime-migrations-testing
- PDF to upload: guides/papers/2026-501-zero-downtime-migrations/build/2026-501-zero-downtime-migrations.pdf
- Conflict of interest: The author builds Levelrail, a self-hosted deployment platform. No product is recommended here.
- Funding: None, self-funded.

Abstract:

A one line ALTER TABLE runs in milliseconds, yet it can stall every query on the table for as long as an unrelated transaction stays open. This paper measures that on PostgreSQL 16.15 and 17.11 with a pgbench workload at a fixed rate, then tests lock_timeout with retry, changes that rewrite or scan a table, concurrent indexes, NOT VALID constraints, a rename done in one step versus expand and contract, and a rolling restart behind nginx 1.27.2. A queued ADD COLUMN stalled all reads for about 5 s, and lock_timeout cut each stall to about the timeout. Each step was tested alone. The ordered procedure was then run end to end once, on one version without lock contention, and two of its rollback points were tested; the rest are derived. The database ran on tmpfs with scaled data, so every time is a shape, not a production time. Replicas, managed services, Kubernetes and migration tools were not tested. The harness and raw results are published at release.
