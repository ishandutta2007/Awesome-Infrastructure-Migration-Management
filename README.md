# Awesome-Infrastructure-Migration-Management

# Top Infrastructure Migration Management Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Server Replication, Database Conversion & Self-Hosted Migration Engines*  
**Last updated: November 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Infrastructure Migration Management**. These tools enable organizations to move workloads, databases, and storage between environments—physical-to-cloud, cloud-to-cloud, or on-premises refreshes—while minimizing downtime and preserving data integrity.

**Examples** include AWS Application Migration Service, Azure Migrate, Google Migrate, Carbonite Migrate, Turbonomic, RiverMeadow, Zerto, NetApp Cloud Sync, PlateSpin Migrate, and Data Center Migration Hub (the category leaders).

**Open-source emphasis**: Infrastructure Migration Management is a domain where open-source tooling is **genuinely capable but fragmented across distinct migration layers**. **PostgreSQL Migrator** is the standout for database migrations—a stable 1.0 release (September 2026) from Dalibo, pure Go binary, migrating Oracle and MySQL/MariaDB to PostgreSQL with schema conversion, code transpilation, and high-performance bulk COPY . **Bani** provides an Apache Arrow-powered database migration engine with connectors for PostgreSQL, MySQL, MSSQL, Oracle, and SQLite, plus an MCP server for AI agents . For object storage, **Chorus** offers a distributed, vendor-agnostic S3/Swift migration and routing tool with checkpointed resumable transfers and real-time change capture , while **sclone** benchmarks faster than rclone for S3-to-S3 transfers . The critical caveat: **no open-source project matches the hypervisor-level replication** of Zerto or RiverMeadow—those platforms replicate entire VMs at the block level with near-zero downtime, a capability that requires kernel drivers and hypervisor integration commercial vendors have perfected .

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-products)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[AWS Application Migration Service (MGN)](https://aws.amazon.com/application-migration-service/)**  
  Hyperscaler-native block-level replication for lifting physical, virtual, or cloud servers into AWS. Includes **2,160 hours (90 days) of free replication per source server**, though target EC2/EBS costs still accrue during testing . **Best for teams committed to AWS** as the migration target.

- **[Azure Migrate](https://azure.microsoft.com/en-us/products/azure-migrate)**  
  Microsoft's unified migration hub combining discovery, right-sizing assessment, and execution. Scores well on ease of use and real-time analytics per G2 reviewer data . **Best for organizations standardizing on Azure**, especially Windows/VMware estates where Entra ID and Hybrid Benefit reduce friction .

- **[Google Migrate (Migration Center)](https://cloud.google.com/migration-center)**  
  Discovery and planning hub with AI-powered Quick Assessments and multi-year TCO projections. Assessment activation is free beyond provisioned test resources . **Best for building the business case** before a Google Cloud move, or Linux/container estates that map cleanly to GCP .

- **[Carbonite Migrate](https://www.carbonite.com/)**  
  Real-time replication migration for physical, virtual, and cloud workloads with minimal downtime; continuous data replication keeps target synchronized until cutover.

- **[IBM Turbonomic](https://www.ibm.com/products/turbonomic)**  
  Performance and cost optimization platform for public, private, and hybrid clouds; continuously adjusts resources to assure application performance while eliminating inefficiencies . **Best for post-migration optimization**—not the migration execution itself.

- **[RiverMeadow](https://www.rivermeadow.com/)**  
  Third-party migration platform purpose-built for **large-scale workload mobility** with automated discovery, dependency mapping, and wave-based orchestration across heterogeneous sources (VMware, Hyper-V, physical, cloud). Proven at enterprise scale with thousands of VMs and built-in validation/rollback . **Best for complex, large VM estates** with tight timelines—but adds licensing cost and a tool your team must learn .

- **[Zerto (HPE)](https://www.zerto.com/)**  
  Continuous replication-based migration optimized for **lift-and-shift with near-zero downtime**; part of HPE portfolio with native Morpheus integration. **Best for mission-critical workloads** where minutes of downtime are unacceptable—but requires licensing, places significant bandwidth demands at scale, and VirtIO drivers must be manually injected for HVM targets .

- **[NetApp Cloud Sync](https://cloud.netapp.com/cloud-sync-service)**  
  File and object sync service for cloud migration; supports NFS, SMB, S3, and Azure Blob targets.

- **[PlateSpin Migrate](https://www.microfocus.com/)**  
  Workload migration for physical and virtual servers across data centers and clouds; supports Windows and Linux with block-level replication.

- **[Data Center Migration Hub](https://aws.amazon.com/migration-hub/)**  
  AWS's central tracking and orchestration service for migrations; **stopped accepting new customers November 2025**, with capabilities moved to AWS Transform .

## Open-Source GitHub Projects

### Database Migration Engines (PostgreSQL Migrator, Bani)

- **[PostgreSQL Migrator](https://gitlab.com/dalibo/pg_migrate)**  
  The **most mature open-source database migration tool** for moving **Oracle and MySQL/MariaDB to PostgreSQL** (PostgreSQL License, v1.0 stable September 2026) . Features: **pure Go binary with zero proprietary dependencies**; **offline catalog inspection** (extract once, iterate conversion offline); **complexity scoring** to assess migration difficulty; **interactive web UI** for browsing original and converted catalogs; **schema and data conversion** (datatype mapping, column-to-boolean conversion); **code analysis and transpilation** via companion `transqlate` tool for SQL, PL/SQL, and routines; **high-performance streamed bulk COPY** with low memory usage; and **TOML configuration** for fine-tuning . **Coverage**: Oracle 11g–26ai, MySQL 8.4+, MariaDB 10+ to PostgreSQL 16–19; conversion currently limited to roles, schemas, sequences, tables, constraints, and indexes (views and procedural objects planned) . **Best for Oracle/MySQL-to-Postgres migrations**—the clear open-source leader for this specific path.

- **[Bani](https://pypi.org/project/bani-tools/)**  
  Open-source **database migration engine powered by Apache Arrow** (PyPI, `pip install bani-tools`) . Features: **5 database connectors** (PostgreSQL, MySQL, MSSQL, Oracle, SQLite); **Apache Arrow columnar interchange** for high-throughput batch transfers; **declarative BDL** (XML/JSON) for version-controlled migrations; **Python SDK** with `ProjectBuilder` API; **CLI** with 11 commands (run, validate, preview, init, schema inspect); **MCP server** with 10 tools for AI agents (Claude, Cursor); **web dashboard** with real-time monitoring; and **cross-platform** deployment (macOS app, Linux packages, Windows installer, Docker) . **Best for multi-database migrations** with AI-agent integration—but it is newer than PostgreSQL Migrator and less battle-tested for Oracle→Postgres specifically.

### Object Storage Migration (Chorus, sclone)

- **[Chorus](https://github.com/clyso/chorus)**  
  The **most complete open-source object storage migration tool** (Go, v0.7.10) . Features: **distributed, vendor-agnostic** support for S3 and OpenStack Swift across AWS, Google, Ceph, and any S3-compatible provider; **resumable transfers with checkpointing**; **sync of existing buckets, objects, and metadata** (ACLs); **real-time capture and propagation** of bucket/object changes during migration; **user-level and bucket-level replication policies**; **S3 proxy for routing requests** to different storages; **diff check** for integrity verification; and **zero-downtime provider switching** . Deployment via Docker, standalone binary, or Helm/Kubernetes. **Best for S3-to-S3 or S3-to-Swift migrations**—the strongest open-source option for object storage.

- **[sclone](https://www.npmjs.com/package/@steevepay/sclone)**  
  Open-source **Storage Clone** tool for S3 and OpenStack Swift (npm, v1.2.0) . Features: **unidirectional and bidirectional sync**; **cron-based scheduling**; **parallelized workloads** with file list caching; **MD5 integrity checks** (optional); **metadata preservation** between S3 and Swift; and **dry-run mode** . **Benchmarks**: 10GB S3-to-S3 transfer in **3.30 minutes** vs. rclone's 5.45 minutes; bidirectional 8GB sync in **3.59 minutes** vs. rclone's 8.4 minutes . **Best for teams wanting a faster rclone alternative** for S3/Swift sync—but it is Node.js-based and less feature-rich than Chorus for zero-downtime switching.

### VPS & Server Migration (vps-backup-sync)

- **[vps-backup-sync](https://gitea.com/cash602-cmd/vps-backup-sync)**  
  Zero-dependency shell-based **VPS backup and server migration utility** (MIT) . Features: **full stack backup** (website directories + auto-detected MySQL/MariaDB/PostgreSQL databases); **resume-supported rsync over SSH** (`--partial --inplace`) for interrupted transfers; **SHA256 integrity verification**; **direct server-to-server migration** without downloading to local PC; **automated crontab** with 7-day retention purge . **Best for small VPS-to-VPS migrations** where a simple shell script is sufficient—not for enterprise-scale or hypervisor-level replication.

### Additional Strong Open-Source Options

- **omnidbm** — Universal database-to-database transfer engine (PyPI, v0.1.0) supporting MongoDB, PostgreSQL, MySQL, SQLite, Redis, CSV, JSONL with interactive CLI and auto table creation . **Best for quick any-to-any data moves**—but it is v0.1.0 and lacks schema conversion.
- **bg-coolify-migrate** — Coolify-specific migration toolkit with byte-exact volume mirroring, DNS cutover gating, and rollback capability . **Niche**—for Coolify users only.
- **rsync.ai** — Self-hosted AI data platform with batch pipelines and CDC via Debezium/Kafka . **Not a migration tool**—it is a data platform with sync capabilities, heavier than needed for pure migration.

**Frameworks for building custom systems**: For **Oracle/MySQL to PostgreSQL migrations**, PostgreSQL Migrator is the mature open-source leader . For **multi-database migrations with AI-agent integration**, Bani . For **S3/Swift object storage migration with zero-downtime switching**, Chorus . For **fast S3 sync**, sclone . For **simple VPS-to-VPS moves**, vps-backup-sync . **No open-source project matches the hypervisor-level block replication** of Zerto or RiverMeadow—those require kernel-level drivers and hypervisor integration that commercial vendors have perfected .

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Infrastructure migration platforms handling production workloads must comply with organizational security policies and data governance requirements; **self-hosted solutions place full responsibility for credential management, transfer integrity, and cutover planning on the operator**.
- **Open-source infrastructure migration is capable at database and object-storage layers but fundamentally limited for hypervisor-level replication**—PostgreSQL Migrator and Bani handle database conversions , and Chorus handles S3/Swift migration . However, **no open-source project matches the block-level VM replication** of Zerto or RiverMeadow, which requires kernel drivers and hypervisor integration . Choose based on whether you need database migration (PostgreSQL Migrator, Bani), object storage (Chorus, sclone), or full VM replication (commercial only).
- Verify license terms for commercial use; PostgreSQL Migrator uses the PostgreSQL License , and Chorus is open-source (check repository).

---

**Made for infrastructure engineers, migration architects, and organizations planning workload moves.**  
Let's make infrastructure migration more open, but with clear eyes about the hypervisor-level replication and enterprise orchestration gaps that commercial platforms still fill.
