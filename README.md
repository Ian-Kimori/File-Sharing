# File-Sharing

# File Sharing — The Definitive Complete Reference

---

## What File Sharing Is

File sharing is any mechanism by which files stored in one location are made accessible to another system, user, process, or organisation — over a local network, the internet, between services, or physically. It underpins every area of computing: business operations, software infrastructure, media delivery, security, healthcare, finance, research, and personal use.

Every scenario where a file needs to move, be accessed remotely, be synchronised, or be made available to more than one consumer involves file sharing in some form.

---

## The Two Fundamental Models

**Centralised** — there is a single authoritative source. All clients connect to that source to upload or download. The source controls access, availability, and integrity. If the source goes down, access is lost.

**Distributed** — there is no single source. Files or pieces of files are spread across many participants. Clients fetch from multiple sources simultaneously. No single node going down breaks availability.

---

## Complete Taxonomy

```
FILE SHARING
│
├── CENTRALISED
│   ├── Block-Level Storage
│   │   ├── iSCSI
│   │   ├── Fibre Channel (FC)
│   │   └── FCoE
│   │
│   ├── File-Level Network Mounts
│   │   ├── SMB / CIFS
│   │   ├── SMB over QUIC
│   │   ├── Windows DFS (Namespace + Replication)
│   │   ├── NFS (v3, v4, v4.1, v4.2)
│   │   ├── AFP (legacy)
│   │   ├── WebDAV
│   │   └── Cloud Managed (AWS EFS, Azure Files, GCP Filestore)
│   │
│   ├── High-Performance Parallel Filesystems
│   │   ├── Lustre
│   │   ├── GPFS / IBM Spectrum Scale
│   │   └── BeeGFS
│   │
│   ├── Distributed Big Data Filesystems
│   │   └── HDFS
│   │
│   ├── Secure Transfer
│   │   ├── SFTP
│   │   ├── SCP
│   │   └── RSync (SSH mode + rsyncd daemon)
│   │
│   ├── Legacy and Lightweight Transfer
│   │   ├── FTP
│   │   ├── FTPS
│   │   └── TFTP
│   │
│   ├── B2B and Enterprise Transfer
│   │   ├── AS2
│   │   └── MFT Platforms
│   │
│   ├── Web and API
│   │   ├── HTTPS upload / download
│   │   ├── Presigned URLs
│   │   └── REST API file transfer
│   │
│   ├── Object Storage
│   │   ├── S3, GCS, Azure Blob
│   │   ├── MinIO (self-hosted)
│   │   └── Cloud Storage Gateways
│   │
│   ├── CDN
│   │
│   ├── Cloud Sync Platforms
│   │   ├── Consumer (Drive, Dropbox, iCloud, OneDrive)
│   │   └── Enterprise (SharePoint, Box, Nextcloud)
│   │
│   ├── Messaging Platforms
│   │
│   ├── Version Control
│   │   ├── Git
│   │   ├── Git LFS
│   │   ├── DVC
│   │   └── Git Annex
│   │
│   ├── Database Storage
│   │   ├── BLOB (PostgreSQL, MySQL, Oracle)
│   │   └── GridFS (MongoDB)
│   │
│   ├── Email (SMTP / IMAP)
│   │
│   ├── Media Sharing (DLNA / UPnP / Plex)
│   │
│   ├── Network Provisioning
│   │   ├── TFTP + PXE Boot
│   │   └── Multicast Distribution
│   │
│   ├── Remote Desktop File Transfer
│   │   └── RDP Drive Mapping
│   │
│   ├── Physical Media
│   │   ├── USB / External Disk
│   │   ├── LTO Tape
│   │   ├── Cloud Transfer Appliance
│   │   └── Sneakernet
│   │
│   └── Database Replication
│       ├── MySQL / MariaDB binlog
│       └── PostgreSQL WAL streaming
│
└── DISTRIBUTED
    ├── Peer to Peer
    │   ├── BitTorrent
    │   └── WebRTC (browser to browser)
    ├── Decentralised Storage
    │   ├── IPFS
    │   ├── Filecoin
    │   └── Storj / Sia
    └── Local Wireless
        ├── AirDrop
        ├── Nearby Share
        └── Snapdrop
```

---

## Protocol Quick Reference

| Protocol / Tool | Layer | Port / Transport | Encryption | Model |
|---|---|---|---|---|
| iSCSI | Block | TCP 3260 | Optional (IPsec) | Centralised |
| Fibre Channel | Block | FC fabric | FC-SP | Centralised |
| FCoE | Block | Ethernet | FC-SP | Centralised |
| SMB / CIFS | File mount | TCP 445 | SMB3 encrypts | Centralised |
| SMB over QUIC | File mount | UDP 443 | QUIC always | Centralised |
| Windows DFS | File mount | TCP 445 | SMB3 | Centralised |
| NFS | File mount | TCP/UDP 2049 | NFSv4 + Kerberos | Centralised |
| AFP | File mount | TCP 548 | TLS | Centralised |
| WebDAV | File mount | TCP 80/443 | TLS | Centralised |
| AWS EFS / Azure Files | File mount | TCP 2049/445 | TLS | Centralised |
| Lustre | Parallel FS | TCP 1988 | Optional | Centralised |
| HDFS | Big data FS | TCP 9000 | Kerberos/TLS | Centralised |
| SFTP | Transfer | TCP 22 | SSH always | Centralised |
| SCP | Transfer | TCP 22 | SSH always | Centralised |
| RSync | Sync | TCP 22 / 873 | SSH / optional | Centralised |
| FTP | Transfer | TCP 21 | None | Centralised |
| FTPS | Transfer | TCP 21/990 | TLS | Centralised |
| TFTP | Transfer | UDP 69 | None | Centralised |
| AS2 | B2B transfer | TCP 443 | TLS + signing | Centralised |
| MFT Platform | B2B governed | Various | Always enforced | Centralised |
| HTTPS | Web / API | TCP 443 | TLS always | Centralised |
| Presigned URL | Web / API | TCP 443 | TLS always | Centralised |
| S3 API | Object store | TCP 443 | TLS always | Centralised |
| CDN | Delivery | TCP 443 | TLS always | Centralised |
| Cloud Sync | Sync platform | TCP 443 | TLS always | Centralised |
| Git / Git LFS | Version control | TCP 22/443 | SSH / TLS | Centralised |
| SMTP / IMAP | Email | TCP 587/993 | TLS | Centralised |
| DLNA / UPnP | Media | TCP 1900/HTTP | Optional | Centralised |
| TFTP + PXE | Provisioning | UDP 69 | None | Centralised |
| RDP | Remote desktop | TCP 3389 | TLS always | Centralised |
| USB / LTO Tape | Physical | Physical | Encrypted device | Centralised |
| BitTorrent | P2P | TCP 6881+ | Optional | Distributed |
| IPFS | Decentralised | TCP 4001 | Optional | Distributed |
| WebRTC | Browser P2P | UDP/TCP | DTLS always | Distributed |
| AirDrop | Local wireless | WiFi/BT | TLS always | Distributed |
| Snapdrop | Local wireless | WebRTC | DTLS always | Distributed |

---

---

# Part One — Centralised File Sharing

---

## Section 1 — Block-Level Storage

Block-level storage shares raw disk — not folders or files. The client operating system sees a locally attached disk which it formats and manages itself. Block storage is the foundation layer that many file sharing systems run on top of. Understanding it is essential for understanding the full storage stack.

**The distinction:**
- File-level (NFS, SMB) — server manages the filesystem, clients access named files and folders
- Block-level (iSCSI, FC) — client manages the filesystem on raw blocks, server provides raw disk

---

### iSCSI

SCSI storage commands tunnelled over TCP/IP networks. A server connects to a remote storage target over standard Ethernet. The operating system sees it as a locally attached disk. Any filesystem can be placed on it.

**Components:**
- **Initiator** — the client (server connecting to storage)
- **Target** — the storage device being connected to
- **IQN (iSCSI Qualified Name)** — unique identifier for initiators and targets
- **LUN (Logical Unit Number)** — a logical partition of storage exposed by the target

**Scenarios:**
- A database server attaches to an iSCSI target on a SAN. The database sees dedicated raw block storage. It has full control over its own filesystem and I/O scheduling — no filesystem overhead from NFS or SMB.
- A virtualisation cluster uses iSCSI SAN storage for VM disk images. VMs live-migrate between hosts because all hosts access the same block storage.
- A small business NAS exposes iSCSI targets to Windows servers — the servers see additional local drives, formatted as NTFS, backed by the NAS.
- A backup appliance presents an iSCSI target to backup software — the software writes directly to block storage as if writing to a local tape drive.

**Strengths:** Low overhead, any filesystem, familiar local disk experience for applications.
**Limitations:** Requires careful access control — one misconfigured initiator can corrupt a target. Not designed for concurrent access by multiple hosts to the same LUN without a cluster filesystem.

---

### Fibre Channel (FC)

A high-speed network protocol specifically designed for storage area networks. Not Ethernet-based. Runs on dedicated FC switches and HBAs (Host Bus Adapters). Extremely low latency and extremely high throughput. The standard in enterprise data centres, financial institutions, and broadcast facilities where performance is non-negotiable.

**Components:**
- **HBA (Host Bus Adapter)** — the FC network card in a server
- **FC Switch / Director** — the network fabric connecting servers to storage
- **WWN (World Wide Name)** — unique identifier for FC devices, analogous to MAC address
- **Zoning** — access control on FC switches determining which initiators can see which targets

**Scenarios:**
- A financial trading platform uses FC-attached storage for microsecond-latency disk access. NFS and iSCSI add too much protocol overhead for this use case.
- A VMware vSphere enterprise cluster uses an FC SAN for shared VM storage. All ESXi hosts connect to the FC fabric and access shared datastores. VMs live-migrate between hosts with no interruption.
- A broadcast facility attaches 4K and 8K video editing workstations to an FC SAN. Editors collaborate on shared media at throughput rates impossible to achieve over NFS.
- A large database installation uses FC for its primary storage — the storage array provides guaranteed IOPS and sub-millisecond latency over the FC fabric.

**Strengths:** Highest performance available, deterministic latency, purpose-built for storage, mature enterprise ecosystem.
**Limitations:** Expensive — dedicated switches, HBAs, and cabling. Separate network to manage alongside Ethernet. Specialist skills required.

---

### FCoE — Fibre Channel over Ethernet

Fibre Channel frames carried over 10GbE or faster Ethernet. Converges storage and data networking onto a single cable infrastructure — one set of cables, switches, and NICs for both data and storage traffic. Requires Data Centre Bridging (DCB) Ethernet to provide lossless transport.

**Scenarios:**
- A data centre consolidating its cabling infrastructure uses FCoE — one 25GbE connection per server carries both data and FC storage traffic.
- A new data centre build avoiding the cost of a separate FC switch fabric while retaining FC semantics and performance.

**Strengths:** Reduces cabling and switch infrastructure costs. Retains FC protocol semantics and tooling.
**Limitations:** Requires DCB-capable Ethernet switches. Adds complexity. iSCSI over 25GbE is often simpler and sufficient for most workloads.

---

## Section 2 — File-Level Network Mounts

Remote directories exposed over the network and mounted on client machines. Applications read and write as if storage is local. The server manages the filesystem. The client accesses named files and folders.

---

### SMB / CIFS — Server Message Block

The dominant LAN file sharing protocol. Originated in Windows. Implemented on Linux and macOS by Samba. Clients mount a named share and interact with it exactly like a local folder. SMB3 (Windows 8 / Server 2012 and later) adds encryption, multichannel, and significant performance improvements.

**Authentication:** Windows credentials, Active Directory with Kerberos, or local Samba accounts. In enterprise environments AD with Kerberos is the standard — no passwords travel the network, only Kerberos tickets.

**Versions:**
- SMB1 — legacy, insecure, should be disabled everywhere
- SMB2 — improved performance, reduced chattiness
- SMB3 — encryption, multichannel (multiple NICs for bandwidth aggregation), transparent failover

**Scenarios:**
- A company with 300 staff maps `\\fileserver\Finance` as drive letter F. All finance staff read and write centrally. AD groups control who can access which share. Staff on any Windows machine see the same files.
- A Linux Samba server serving files to a mixed Windows and Linux office — cross-platform transparency via the same SMB protocol.
- A NAS device sharing a media library across all devices on a home or office network.
- A developer mounting a remote project folder from a Linux VM onto their Windows workstation for live editing via SMB.
- MacOS connecting to a corporate file server — macOS supports SMB natively and defaults to it over AFP.

**Strengths:** Native Windows integration, broad OS support, fine-grained permissions via AD, works transparently for end users.
**Limitations:** Designed for LAN. Performs poorly over high-latency WAN without optimisation. Not suitable for internet-facing access without SMB over QUIC.

---

### SMB over QUIC

A modern variant of SMB introduced in Windows Server 2022 and Windows 11. Runs SMB over the QUIC transport protocol — UDP-based, always encrypted, multiplexed, resilient to IP address changes. Enables SMB to work safely over the internet without VPN.

**Scenarios:**
- Remote workers access corporate file shares directly over the internet — no VPN client required. The connection is encrypted by QUIC.
- Azure Files accessed from Windows machines over QUIC — native drive mapping to cloud storage.
- A branch office accessing headquarters shares over QUIC without site-to-site VPN complexity.
- A travelling employee connects to the office file server from a hotel network over QUIC — same drive letter, same experience as being in the office.

**Strengths:** Encrypted by default, internet-safe, no VPN required, same SMB semantics and tooling.
**Limitations:** Requires Windows Server 2022 or newer on the server side. Windows 11 or newer on the client side. Not yet universally supported.

---

### Windows DFS — Distributed File System

A layer on top of SMB providing namespace abstraction and automatic replication. Two components: DFS Namespace and DFS Replication.

**DFS Namespace:** A single unified path (e.g. `\\company\files`) that transparently maps to underlying SMB shares on different servers. Users see one path regardless of where files physically live or which server serves them.

**DFS Replication:** Automatically replicates file share contents between servers using a compressed delta algorithm (RDC — Remote Differential Compression). Keeps branch offices in sync with headquarters and provides redundancy.

**Scenarios:**
- A multinational with file servers in Nairobi, Dublin, and Singapore presents `\\company\projects` globally. DFS routes users to their nearest server. DFS Replication keeps all three servers in sync. Users see one path, one experience.
- A disaster recovery setup where DFS Replication keeps a standby server current — failover is transparent because the namespace path never changes.
- A server migration where the underlying file server is replaced — DFS namespace path remains the same, users notice nothing, cutover is zero-downtime.
- A branch office with limited WAN bandwidth uses DFS Replication to maintain a local copy of headquarters files — staff access files locally at LAN speed.

**Strengths:** Location transparency, automatic replication, high availability, zero-downtime migrations.

---

### NFS — Network File System

The Unix and Linux equivalent of SMB. Standard in data centres, HPC clusters, and Linux-heavy infrastructure. The server exports directories. Clients mount them via the OS. Access control by IP address in NFSv3, adding Kerberos identity in NFSv4.

**Versions:**
- NFSv3 — stateless, no built-in encryption, access controlled by IP address only. Safe only on trusted networks.
- NFSv4 — stateful, ACL support, Kerberos authentication, better WAN performance.
- NFSv4.1 — pNFS (parallel NFS) allowing clients to read and write directly to multiple storage servers simultaneously.
- NFSv4.2 — server-side copy, sparse file support, application I/O advise.

**Scenarios:**
- Ten application servers behind a load balancer mount `/mnt/uploads` from one NFS server. A file written by any server is immediately readable by all others — no synchronisation logic in the application.
- A Kubernetes cluster using NFS as a ReadWriteMany persistent volume backend — multiple pods on different nodes mount the same NFS export.
- A render farm where all compute nodes mount the same asset library — no copying datasets per node, jobs run against shared data.
- Your Kenya and Ireland data centres sharing configuration directories over a VPN tunnel via NFSv4 with Kerberos — encrypted, authenticated, without IP-trust-only NFSv3.
- A Raspberry Pi cluster booting from an NFS root filesystem — no SD cards, the OS is the NFS mount.

**Strengths:** Transparent to applications, high performance on LAN, standard on all Unix and Linux systems.
**Limitations:** NFSv3 has no encryption — only use on trusted networks or over VPN/dedicated circuits. High-latency WAN degrades NFS performance significantly.

---

### NFS Over Dedicated Circuits

In enterprise and telco environments NFS runs over dedicated MPLS circuits, dark fibre, or leased lines between sites — not the public internet and not VPN tunnels. Provides predictable low-latency performance between facilities.

**Scenarios:**
- A bank running NFS between its primary data centre and DR site over a dedicated 10Gbps dark fibre circuit — consistent sub-millisecond latency.
- A broadcaster sharing media assets between production facilities in different cities over an MPLS WAN — guaranteed bandwidth with no internet congestion.
- A financial institution sharing a compliance document repository between its primary and secondary data centres over a leased line — deterministic performance, no VPN overhead.

---

### AFP — Apple Filing Protocol

Apple's legacy LAN file sharing protocol. Deprecated — macOS now defaults to SMB even for Apple-to-Apple transfers since macOS Ventura.

**Scenarios:**
- Legacy Mac environments and older NAS devices that predate the SMB default switch.
- Older Time Machine configurations on legacy hardware still using AFP.

---

### WebDAV — Web Distributed Authoring and Versioning

File transfer and management over HTTP/HTTPS. Extends standard HTTP with methods for creating, moving, copying, locking, and deleting files remotely. Can be mounted as a network drive on most operating systems. Firewall-friendly — uses standard ports 80 and 443.

**Scenarios:**
- Nextcloud and ownCloud expose storage via WebDAV — clients mount it as a network drive or use the desktop sync client.
- Older SharePoint versions used WebDAV for direct file access from Windows Explorer.
- A remote team mounts a WebDAV share over HTTPS to access files without VPN — any firewall allowing HTTPS allows WebDAV.
- CalDAV and CardDAV — extensions of WebDAV for calendar and contact synchronisation — used by all major calendar and contacts applications.

**Strengths:** Works over standard HTTPS, firewall-friendly, cross-platform, no special ports required.
**Limitations:** Higher overhead than NFS or SMB for large file operations. Not suited for high-performance data centre workloads.

---

### Cloud-Managed File Systems

Managed NFS and SMB services provided by cloud providers. No infrastructure to deploy or manage — the provider operates the file system. Mounted by cloud VMs and containers as standard NFS or SMB.

**AWS EFS (Elastic File System):** Managed NFS. Automatically scales. Mounted by EC2 instances or containers as a standard NFSv4 mount.

**AWS FSx for Windows:** Managed Windows File Server. Full SMB with Active Directory integration. Identical to an on-premises Windows file server.

**AWS FSx for Lustre:** Managed Lustre for HPC and ML workloads. Can be linked to S3 buckets.

**Azure Files:** Managed SMB and NFS shares. Accessible over SMB over QUIC from the internet. Mountable by Windows and Linux.

**Google Cloud Filestore:** Managed NFS for GCP workloads.

**Scenarios:**
- A containerised application on AWS ECS mounts EFS as a shared persistent volume — no NFS server to manage, scales automatically with usage.
- A Windows application migrated to Azure mounts Azure Files as a drive letter — identical experience to on-premises SMB with no infrastructure to run.
- A machine learning training cluster on AWS mounts EFS so all training nodes share the same dataset directory — no data copying between nodes.
- A legacy Windows application in Azure uses FSx for Windows File Server — fully managed SMB with AD integration.
- An HPC job on AWS uses FSx for Lustre linked to an S3 bucket — input data streams from S3 to Lustre automatically, job runs at full Lustre throughput.

**Strengths:** Zero infrastructure management, automatic scaling, cloud-native integration, pay-per-use.

---

## Section 3 — High-Performance Parallel Filesystems

Parallel filesystems stripe files across multiple storage servers simultaneously. All clients read and write in parallel to multiple servers at once — achieving aggregate throughput that no single NFS server can provide. Used in HPC, AI/ML training, genomics, climate science, and any workload where data I/O is the bottleneck.

---

### Lustre

The dominant open-source parallel distributed filesystem. Designed for massive throughput — hundreds of GB/s aggregate. Files are striped across multiple OSTs (Object Storage Targets). A metadata server (MDS) tracks file locations. All clients communicate with all storage servers simultaneously.

**Components:**
- **MGS (Management Server)** — stores cluster configuration
- **MDS (Metadata Server)** — manages filenames, directories, permissions
- **OSS (Object Storage Server)** — stores actual file data
- **OST (Object Storage Target)** — individual storage volumes on OSS nodes
- **Client** — mounts the Lustre filesystem and reads/writes in parallel across all OSTs

**Scenarios:**
- A supercomputing centre running climate simulation jobs — thousands of compute nodes read and write to Lustre simultaneously at aggregate throughputs exceeding 1TB/s. Impossible with NFS.
- An AI training cluster running large language model training — hundreds of GPUs need to stream training data faster than any single storage server can provide. Lustre stripes data across dozens of OSTs.
- AWS FSx for Lustre — managed Lustre in the cloud. A training job reads input data from an S3 bucket via the FSx-S3 linkage at full Lustre throughput.
- A genomics research facility processing whole-genome sequencing — petabyte-scale datasets, massively parallel analysis jobs.

---

### GPFS / IBM Spectrum Scale

IBM's enterprise parallel filesystem. Used in supercomputing centres, large enterprises, and financial institutions. Provides very high throughput, built-in data management, tiering, and encryption. More feature-rich than Lustre with stronger enterprise support.

**Scenarios:**
- The world's largest supercomputers run GPFS for their shared parallel storage.
- A financial institution uses Spectrum Scale for its data lake — petabytes of trading data accessible at high throughput.
- A large media company manages its entire media archive on Spectrum Scale with automatic tiering from fast NVMe to tape.

---

### BeeGFS

A parallel filesystem popular in research computing, AI/ML, and mid-range HPC. Easier to deploy than Lustre. No kernel modules on clients — user-space client. Good performance scaling from a few nodes to hundreds.

**Scenarios:**
- A university AI/ML research cluster uses BeeGFS as its shared training data filesystem.
- A bioinformatics facility uses BeeGFS for shared genomics pipeline storage.
- A medium-sized enterprise HPC cluster uses BeeGFS instead of Lustre for its simpler deployment and management.

---

## Section 4 — Distributed Big Data Filesystems

---

### HDFS — Hadoop Distributed File System

A distributed filesystem designed for very large datasets on commodity hardware. Files are split into large blocks (128MB default) and replicated across multiple data nodes (default 3 copies). A NameNode tracks where each block lives. Designed for high-throughput sequential reads — the compute runs where the data is (data locality), not the other way around.

**Components:**
- **NameNode** — tracks block locations, manages namespace. Single point of failure in classic HDFS (HDFS HA uses two NameNodes).
- **DataNode** — stores actual blocks, serves read and write requests.
- **Block** — the unit of storage, 128MB by default.
- **Replication** — each block stored on 3 DataNodes by default.

**Scenarios:**
- A big data platform stores petabytes of log data in HDFS. Spark jobs process data where it lives — no moving data to a processing server.
- A large e-commerce company stores all clickstream data in HDFS for batch analytics and machine learning feature generation.
- A data warehouse ingestion pipeline lands raw data in HDFS, processes with Spark, and writes results to a relational database.

**Note:** HDFS is increasingly replaced by object storage (S3) plus compute frameworks (Spark, Presto) that read directly from S3. New data platforms rarely start with HDFS today but it remains widely deployed in existing installations.

---

## Section 5 — Secure Transfer

File transfer over encrypted channels. Files are explicitly sent or received — no persistent mount. Used by administrators, automated scripts, CI/CD pipelines, and external partner integrations.

---

### SFTP — SSH File Transfer Protocol

File transfer over SSH. Completely separate from FTP despite the name. Everything encrypted — credentials, commands, file data. Supports full remote filesystem management: browse, upload, download, rename, delete, create directories. The standard secure file transfer protocol for internet-facing use.

**Authentication:** SSH key pairs (preferred — no passwords transmitted) or passwords (acceptable, less preferred).

**Scenarios:**
- A developer deploying files to a production server.
- A cron job pushing nightly reports to a partner server on a schedule.
- A fintech platform receiving ISO 20022 or MT940 payment files from counterparty banks — each partner has a dedicated drop folder, authenticates via SSH key, a monitoring service triggers processing on new file arrival.
- A customer portal where clients drop sensitive documents into a secure intake folder — no client needs a full server account.
- Automated backup scripts sending compressed encrypted archives to an offsite server nightly.
- A sysadmin pulling specific log files from a remote server for analysis.
- CI/CD pipelines pushing build artifacts to a staging server.
- An ops team performing bulk file access to object storage via an SFTP-to-S3 gateway.

---

### SCP — Secure Copy Protocol

Also runs over SSH. Designed purely for copying files — no browsing or remote filesystem management. Simpler than SFTP. Being replaced by SFTP in most modern tools as SCP has known protocol limitations.

**Scenarios:**
- Quick one-off file copies between servers: `scp archive.tar.gz user@server:/backup/`
- Scripts that need simple no-frills remote copy without full SFTP client overhead.

---

### RSync

A synchronisation tool running over SSH or its own daemon (rsyncd on TCP 873). The defining feature is delta transfer — only changed blocks within files are transferred, not whole files. Highly efficient for large files or large directory trees where most content does not change between syncs.

**SSH mode:** Encrypted, authenticated via SSH keys, standard for internet-facing use.
**rsyncd daemon mode:** Runs on TCP 873, no SSH overhead, used for internal trusted network mirrors and public distribution mirrors. No encryption unless combined with SSL/TLS wrapper.

**Scenarios:**
- Incremental server backups — only changed blocks transferred nightly. `rsync -avz /data/ backup-server:/backups/data/`
- Keeping two servers in sync — primary to replica, on schedule or continuously.
- Migrating a server — RSync the full filesystem, then a final delta sync at cutover minimises downtime.
- Distributing configuration files from a master server to all application nodes.
- Linux distribution mirrors (Ubuntu, Debian, CentOS) — public mirror servers expose rsyncd endpoints so anyone can efficiently mirror the entire repository.
- Internal package mirrors inside a data centre — application servers sync from an internal mirror via rsyncd without SSH overhead.
- Backing up NFS and SMB share contents to an offsite server nightly.

---

## Section 6 — Legacy and Lightweight Transfer

---

### FTP — File Transfer Protocol

The original file transfer protocol. Completely plaintext — credentials and data are transmitted unencrypted. Should not be used for anything internet-facing or sensitive. Port 21 for control, passive mode ports for data.

**Scenarios:**
- Legacy web hosting — uploading HTML files to an old shared hosting provider.
- Isolated internal lab environments on air-gapped or trusted-only networks.
- Very old enterprise systems that cannot support SFTP and have never been updated.

**Limitation:** No encryption. Credentials visible on any network tap. Actively dangerous on untrusted networks. Replace with SFTP wherever possible.

---

### FTPS — FTP Secure

FTP with TLS encryption layered on top. Encrypts credentials and data. Completely different protocol from SFTP — shares the FTP command structure but wraps it in TLS.

**Scenarios:**
- Organisations that must exchange files with legacy partners whose systems only support FTP but require encryption.
- EDI file exchanges with supply chain partners whose systems predate SFTP support.
- Some banking and insurance file exchange systems using FTPS for historical reasons.
- An MFT platform managing FTPS connections alongside SFTP and AS2 for partners that cannot upgrade.

---

### TFTP — Trivial File Transfer Protocol

A simple lightweight UDP-based file transfer protocol. No authentication, no encryption, no directory listing. Designed for simplicity — used where a full FTP or SFTP implementation is too heavy.

**Scenarios:**
- Network devices (routers, switches, firewalls) use TFTP to download firmware or configuration from a TFTP server on first boot or during recovery.
- PXE boot — a machine boots from the network, downloads a bootstrap loader via TFTP, then downloads an OS installer.
- Cisco and other network equipment use TFTP to upload and download configuration files and OS images during provisioning and upgrades.
- An IT team provisions 200 new machines via PXE — each boots, fetches an OS image via TFTP and HTTP, installs automatically with no manual intervention.

---

## Section 7 — B2B and Enterprise Transfer

---

### AS2 — Applicability Statement 2

An HTTP-based protocol designed specifically for secure reliable business-to-business file exchange. Provides TLS encryption, digital signatures (non-repudiation), and MDN delivery receipts — the receiver sends a signed acknowledgement confirming the file arrived intact and unmodified. The standard for EDI in supply chain, retail, and logistics.

**Scenarios:**
- A retailer exchanging purchase orders and invoices with hundreds of suppliers — each exchange is digitally signed and acknowledged. Non-repudiation means neither party can deny a transaction occurred.
- EDI file exchange in supply chain and logistics — AS2 is mandated by major retailers (Walmart, Amazon, Target) for supplier file exchange.
- Healthcare networks exchanging patient records between systems with cryptographic proof of delivery.
- Any B2B scenario where the sender requires legal proof the file arrived intact and unmodified.

**Strengths:** Non-repudiation, signed delivery receipts, encrypted end-to-end, widely mandated in retail and supply chain.

---

### MFT Platforms — Managed File Transfer

A software category providing a governed auditable automated platform for file transfer. Sits above raw protocols (SFTP, FTPS, AS2, FTP) and adds workflow automation, scheduling, encryption enforcement, retry logic, alerting, audit logging, and compliance reporting. Examples: IBM Sterling, GoAnywhere MFT, MOVEit, Axway.

**Scenarios:**
- A bank managing file exchanges with 80 counterparties across SFTP, FTPS, AS2, and legacy FTP — all managed from one platform with one audit trail.
- A healthcare network automating HIPAA-compliant file exchanges between hospitals, labs, and insurers — the platform enforces encryption, logs every transfer, and alerts on failure.
- A government agency automating file ingestion from multiple data providers with full audit trail for regulatory accountability.
- A new trading partner onboarded in hours — configure the connection in the MFT platform rather than building a custom integration from scratch.
- A compliance team reviewing all file exchanges from the past 90 days via the MFT audit dashboard during a regulatory audit.

**Strengths:** Single platform for all protocols, enforced encryption, complete audit trail, scheduling and retry, compliance reporting, rapid partner onboarding.

---

## Section 8 — Web and API Delivery

---

### HTTPS Upload and Download

Files delivered or received over HTTP/HTTPS. The most universal file transfer mechanism — any device with a browser or HTTP client can participate. The web server or application handles the transfer. Storage backend may be local disk, NFS, or object storage.

**Scenarios:**
- A user uploads a file via a browser form — the browser POSTs the file to the app server over HTTPS as a multipart/form-data request.
- A web server directly serves static files from a directory — software downloads, public datasets, documentation, reports.
- An internal tool exposing build artifacts or processed reports via a simple URL — authenticated via session token or API key.
- A REST API endpoint accepting a file upload, processing it, and returning a result — a document conversion, image resize, or data parsing service.
- A webhook receiver accepting file payloads from a partner system via HTTPS POST.

---

### Presigned URLs

A time-limited cryptographically signed URL generated by an object storage service. Grants temporary access to a specific object without requiring the requester to have storage credentials. Issued for upload (PUT) or download (GET). The signature encodes the expiry time, bucket, key, and permitted operation — any modification invalidates the signature.

**Scenarios:**
- A web app generates a presigned PUT URL. The browser uploads a large video directly to object storage — bypassing the app server entirely. App server handles no file bytes.
- A user requests a download. The app generates a presigned GET URL expiring in 15 minutes. The browser downloads directly from object storage or CDN.
- A microservice passes a presigned URL to a downstream service so it can retrieve a file without needing storage credentials.
- Sharing a specific file from a private bucket with an external party for a limited time — the URL expires, access is automatically revoked.
- A compliance system generating presigned URLs for a regulator to access specific archived documents for a defined window.

---

## Section 9 — Object Storage

Files stored as objects in flat namespaces (buckets) addressed by a key. Accessed via HTTP API — typically the S3 API which has become the universal standard. No filesystem hierarchy — just bucket, key, and value. The modern standard for durable scalable file storage in production systems.

**Key features:** Versioning, lifecycle policies (auto-archive or delete after N days), cross-region replication, event notifications on new objects, presigned URLs, server-side encryption, object locking (WORM — Write Once Read Many for compliance).

**Providers:** AWS S3, Google Cloud Storage, Azure Blob Storage, MinIO (self-hosted, S3-compatible), Wasabi, Backblaze B2.

**Scenarios:**
- A production web application storing all user-uploaded files. App servers store only the object key in the database. Files retrieved via presigned URLs.
- A data pipeline where each processing stage writes output to object storage and passes the key to the next stage via a message queue — object storage is the universal decoupling point.
- A fintech platform archiving seven years of transaction documents for regulatory compliance — lifecycle policy automatically moves files to archive tier after 90 days, deletes at seven years.
- Database backups compressed, encrypted with GPG, and pushed to object storage nightly. Versioning retains 30 days. Cross-region replication provides geographic redundancy.
- ML training datasets stored centrally, pulled by training jobs on demand — no copying datasets per job.
- Static website hosting — HTML, CSS, JS served directly from an S3 bucket behind a CDN.
- A microservice architecture where no service passes file bytes over API calls — all inter-service file handoff via object storage keys.
- Object storage with WORM locking for regulatory compliance — files cannot be modified or deleted for the mandated retention period.

---

### Cloud Storage Gateways

Hybrid appliances (hardware or VM) that sit on-premises and present a standard file interface (NFS, SMB, or iSCSI) to local machines while transparently storing data in cloud object storage. Local machines interact with a familiar file protocol. The gateway handles caching, tiering, and synchronisation to the cloud.

**Examples:** AWS Storage Gateway, Azure StorSimple.

**Scenarios:**
- A branch office uses an NFS mount backed by AWS Storage Gateway — files appear local, are actually stored in S3. No local NAS hardware required.
- A backup solution where an on-premises backup application writes to an iSCSI target presented by Storage Gateway — backups automatically land in S3 Glacier.
- A manufacturing facility with legacy systems that cannot use cloud APIs uses a gateway to provide cloud-backed NFS storage without any application changes.
- An organisation tiering cold data from on-premises NAS to S3 automatically — hot data cached locally, cold data transparently retrieved from S3 on demand.

---

## Section 10 — CDN — Content Delivery Network

A globally distributed network of edge servers that cache files close to end users. The origin (object storage or web server) is only contacted once per region per file. All subsequent requests from that region are served from the edge cache at the nearest point of presence.

**Providers:** Cloudflare, AWS CloudFront, Fastly, Akamai, Bunny.net.

**How it works:** A user requests a file. DNS resolves to the nearest CDN edge node. If the edge has the file cached it serves it immediately. If not (a cache miss) it fetches from the origin, caches it locally, and serves it. Every subsequent request from that region is a cache hit.

**Scenarios:**
- A news site serving images and videos globally — CDN absorbs millions of requests that would otherwise hit the origin. Origin sees only cache misses.
- A software company distributing a 2GB installer globally — each regional edge node caches it after the first download in that region. Users everywhere get local download speeds.
- A game studio distributing a day-one patch to millions of players simultaneously — CDN distributes the load across hundreds of edge nodes globally.
- An e-learning platform serving course video content — students in all regions stream from a nearby edge node with consistent low latency.
- A government agency publishing public data files — CDN makes downloads fast globally without paying for international bandwidth at the origin.

**Strengths:** Dramatic latency reduction, protects origin from traffic spikes, reduces origin bandwidth cost, DDoS mitigation.

---

## Section 11 — Cloud Sync Platforms

Managed platforms combining storage, synchronisation, versioning, sharing, and collaboration. Abstract the underlying protocol — typically HTTPS with a proprietary sync protocol and delta algorithm. The most common file sharing experience for non-technical users.

**Consumer:** Google Drive, Dropbox, iCloud Drive, OneDrive.
**Enterprise:** SharePoint, Box, Google Workspace Drive, OneDrive for Business, Nextcloud (self-hosted), Citrix ShareFile.

**How sync works:** A desktop client monitors a local folder. When a file changes, it uploads the delta to the platform's servers. Other devices running the same client download the delta and apply it. All devices converge to the same state. Files can also be accessed via web browser or mobile app without syncing locally.

**Scenarios:**
- A company using SharePoint as its intranet file store integrated with Microsoft 365 — staff edit documents collaboratively, version history is automatic, access from any device.
- A freelancer sharing a final deliverable with a client via a Dropbox link — client downloads without needing an account.
- A startup using Google Workspace Drive as its entire file server — no on-premise infrastructure.
- A legal firm using Box for secure client document exchange — granular permissions, expiry dates on share links, full audit logs meet compliance requirements.
- A self-hosted Nextcloud instance with MinIO as its backend — company retains full data ownership, staff get a Dropbox-like experience.
- An individual automatically backing up phone photos to iCloud or Google Photos.

**Important considerations:**
- Data sovereignty — hosted platforms store files on the provider's infrastructure. Regulated industries must ensure this meets their jurisdiction requirements.
- Shadow IT — files shared via personal Dropbox or Google Drive accounts bypass corporate access controls and retention policies.

---

## Section 12 — Messaging Platforms

Slack, Microsoft Teams, Telegram, and WhatsApp support file sharing as part of their messaging functionality. Files are uploaded to the platform's infrastructure over HTTPS and stored in their object storage backend. Convenient for operational sharing in the flow of communication.

**How it works:** A user drops a file into a conversation. The platform uploads it to its own storage, generates a download link, and embeds it in the message. Recipients download over HTTPS. Teams stores files in SharePoint behind the scenes.

**Scenarios:**
- A developer shares a log file in a Slack channel for the team to diagnose — faster than setting up SFTP access.
- A manager sends a spreadsheet to a colleague via Teams — it lands in the team's SharePoint document library automatically.
- Field workers send photos from a mobile device via WhatsApp to a coordinator — note that WhatsApp compresses images, which may be unacceptable for professional use.
- A Telegram channel distributes large archives and software builds to a community — Telegram supports files up to 2GB per transfer.

**Important considerations:**
- Files shared in chat are often not covered by corporate data retention and compliance policies — a significant audit and legal risk.
- Sensitive files shared via personal WhatsApp bypass all corporate access controls — shadow IT and data leakage risk.
- Retention periods vary by platform and plan — files may be automatically deleted on free tiers.

---

## Section 13 — Version Control

Git and related systems are file sharing mechanisms with history, attribution, and collaboration built in. Every clone is a full copy of all files and their complete history. Push and pull are file synchronisation operations between machines.

---

### Git

Versions text files and source code. Every commit is a snapshot of all tracked files. Distributed — every clone has the full history. Central hosting (GitHub, GitLab, Gitea) adds access control, code review, and collaboration workflows.

**Scenarios:**
- A development team collaborating on source code — every change attributed to a person, every version recoverable, conflicts resolved via merge.
- Infrastructure teams managing Terraform, Ansible, and Kubernetes manifests — every infrastructure change versioned and auditable.
- A technical writing team managing documentation in Markdown — docs live with the product, changes reviewed via pull request.

---

### Git LFS — Large File Storage

Extends Git for binary files. The LFS pointer (a few bytes) lives in the Git repository. The actual binary lives on an LFS server. Keeps the Git repository small while versioning large files.

**Scenarios:**
- Design teams versioning Figma exports, PSD files, and video assets alongside code.
- Game development teams versioning large binary assets — textures, audio, models — in the same repository as code.

---

### DVC — Data Version Control

Extends Git for large datasets and ML models. Metadata and pointers in Git. Actual data bytes in object storage (S3, GCS, Azure Blob). Code and data versions are pinned together — training runs are reproducible.

**Scenarios:**
- A data science team versioning datasets alongside the code that processes them — any past experiment is fully reproducible.
- An ML team tracking model versions alongside training data and code — full lineage from data to model.

---

### Git Annex

Manages large files with Git without a dedicated LFS server. Files stored in a key-value store locally or on remotes (SSH, S3, WebDAV, rsync). Git tracks which files exist and where their content lives without storing the content in the repository.

**Scenarios:**
- A researcher managing a large collection of datasets and papers across multiple storage locations — Git Annex provides a unified view with deduplication.
- A digital archivist managing a large media collection — content stored across local disk, remote SSH server, and S3 simultaneously with a unified access interface.

---

## Section 14 — Database as File Store

Files stored directly inside a database as Binary Large Objects. The application retrieves them via queries. No separate storage infrastructure required. Works at small scale but does not scale for large volumes or high-frequency access.

**Technologies:** PostgreSQL bytea and Large Objects, MySQL BLOB, Oracle BLOB, MongoDB GridFS (255KB chunks for files over the 16MB document limit).

**Scenarios:**
- A small application storing user profile pictures in PostgreSQL — simple, no additional infrastructure, easy to back up with the database.
- A legacy enterprise document management system storing all PDFs as Oracle BLOBs alongside metadata — everything in one system, but database backups are enormous.
- MongoDB GridFS storing large media files by chunking — allows files exceeding MongoDB's 16MB document limit.
- A modernisation project extracting BLOBs to object storage, storing only the key in the database, serving via presigned URLs — the standard migration path when the application outgrows BLOB storage.

**Limitations:** Databases are not optimised for serving binary files. Backups become very large. Does not scale at high volume. The standard migration path leads to object storage.

---

## Section 15 — Email Attachments

Files encoded and embedded inside email messages. One of the most universally used file delivery mechanisms. Simple and direct but limited by size and lacking version control.

**How it works:** The file is Base64-encoded and embedded in the MIME message. Sent via SMTP. Retrieved via IMAP or POP3. The mail client decodes the attachment.

**Scenarios:**
- A finance manager sends a PDF invoice to a client — simple, direct, no shared infrastructure required.
- A bank sends monthly statements as PDF attachments automatically — generated and attached programmatically via SMTP.
- A payroll system emails payslips to all employees on payday — each personalised PDF attached.
- A file exceeding the size limit (typically 10–25MB) is instead shared via a link to object storage or cloud sync platform in the email body — email becomes the notification channel, not the delivery mechanism.

**Limitations:** Size caps. No version control. Malicious attachments are a primary malware delivery vector — all attachments should be scanned at the mail gateway.

---

## Section 16 — Media Sharing (DLNA / UPnP / Plex)

A distinct file sharing model specifically for media on local and home networks. No mounting, no explicit file transfer — the player streams directly from the server. Devices discover content automatically via network service discovery.

**DLNA (Digital Living Network Alliance):** A standard based on UPnP allowing media servers to advertise their content to players on the local network. Smart TVs, games consoles, and media players discover and stream content automatically.

**Plex / Jellyfin / Emby:** Media server applications that index a local media library and serve it to any device — phone, TV, browser — with transcoding to adapt quality to available bandwidth. Accessible over LAN and internet.

**Scenarios:**
- A NAS running a DLNA server shares a media library to smart TVs and games consoles on the home network — no file copying, devices browse and stream directly.
- A Plex Media Server on a home server transcodes and streams to any device anywhere — phone on mobile data, browser at a friend's house, TV at home — all from one library.
- A Kodi or VLC media player browses a DLNA server and streams films — no file copying or mounting required.
- A small business conference room where videos stored on a media server are streamed to a smart TV without USB drives or file transfers.

---

## Section 17 — Network Provisioning

File sharing at the infrastructure layer — distributing OS images, firmware, and configuration files to machines and network devices. Essential for data centre operations and IT provisioning.

---

### TFTP + PXE Boot

Machines boot from the network by downloading a bootstrap loader via TFTP from a TFTP server. The bootstrap then downloads an OS installer via HTTP or TFTP. Fully automated, no physical media required.

**Scenarios:**
- A data centre provisions 100 new servers simultaneously — each PXE boots, receives a TFTP bootstrap, downloads a kickstart file and OS image, and installs automatically with no human intervention.
- A company reimages 300 laptops after a security incident — PXE boot from the corporate network, OS image served from an internal HTTP or TFTP server.
- A Raspberry Pi cluster boots from a network NFS root filesystem — no SD cards, the OS is served from the network on every boot.
- Network equipment (switches, routers) use TFTP to download firmware during initial setup or recovery.

---

### Multicast File Distribution

A network-level mechanism for delivering the same file to many recipients simultaneously on a LAN. The sender transmits one stream that all recipients join. The network replicates packets at the switch and router level — not at the sender.

**Tools:** UDPcast, UFTP, Tsunami UDP Protocol.

**Scenarios:**
- Imaging 500 computers in a school or enterprise simultaneously — one multicast stream, all machines receive the OS image at the same time. Far faster than 500 separate unicast transfers.
- Distributing a large software update to hundreds of servers simultaneously — one transmission, all servers receive.
- Broadcasting a live market data feed to many consumer applications simultaneously — one stream serves all consumers.

---

## Section 18 — Remote Desktop File Transfer

File sharing via remote desktop sessions. Often overlooked as file sharing but commonly used by administrators and support teams.

**RDP Drive Mapping:** Windows Remote Desktop Protocol allows mapping local drives into the remote session. The remote machine sees the local drive and can read and write to it. Files transfer via the RDP channel — encrypted, over TCP 3389.

**Scenarios:**
- A sysadmin connected via RDP to a Windows server maps their local drive into the session to copy a script or configuration file to the server.
- A support engineer pastes a configuration file into a remote session via clipboard — the clipboard transfer carries file content over the RDP channel.
- VDI (Virtual Desktop Infrastructure) environments where users work on remote desktops — file sharing between the local device and remote desktop is via RDP drive mapping. Users see their local files from inside the virtual desktop.
- A developer RDPs into a Windows build server, maps their local drive, and copies build output back to their local machine.

---

## Section 19 — Physical Media Transfer

File transfer via physical storage devices. The only option for air-gapped environments. The fastest option for truly massive data volumes. The cheapest option for long-term cold archiving.

**Sneakernet:** The informal term for transferring files by physically carrying storage media — named because you walk (in sneakers) instead of using a network. A recognised term in networking. Andrew Tanenbaum's observation remains valid: never underestimate the bandwidth of a station wagon full of tapes hurtling down the highway.

**Media types:** USB flash drive, External HDD/SSD, SD card, DVD/Blu-ray, LTO tape, Cloud provider transfer appliance (AWS Snowball, Azure Data Box).

**Scenarios:**

**Air-gapped environment:** A government classified network or industrial control system has no internet connection by design. Files move in and out only via encrypted USB drives verified and scanned at a security checkpoint. This is intentional — the physical gap is the security control.

**Massive data migration:** A company needs to move 500TB to AWS. Transferring over the internet would take months. An AWS Snowball appliance is shipped to the company, data is loaded locally at full disk speed, the device is shipped back, and AWS uploads directly to S3. Transfer time drops from months to days.

**Long-term archiving:** A broadcaster archives every programme to LTO tape. A single LTO-9 tape holds 18TB natively (45TB compressed). Tapes stored offsite in a climate-controlled facility. Cost per GB on tape is a fraction of any cloud storage tier — the cheapest storage for data retained for decades. Major studios, broadcasters, and national archives all use tape for their ultimate cold archive.

**Forensic transfer:** A forensic investigator connects a seized device via a hardware write-blocker and images it to an external SSD. The write-blocker ensures the original device is not modified — preserving forensic integrity and chain of custody. The image file is then the working copy for analysis.

---

## Section 20 — Database Replication

Replication is file and data sharing at the database layer. Changes on a primary database are continuously streamed to one or more replicas — keeping them current and available for read queries or failover.

**MySQL / MariaDB Binary Log Replication:** The primary writes every change to a binary log. Replicas connect and stream the binary log, replaying changes to stay in sync. Used for read scaling and high availability.

**PostgreSQL WAL Streaming:** The primary streams Write-Ahead Log (WAL) records to standbys in near real time. Standbys replay WAL to stay current. Physical replication (exact block-level copy) or logical replication (table-level, cross-version).

**Scenarios:**
- A primary database streams changes to a replica in a different region — the replica always has a near-current copy for disaster recovery.
- Read replicas serving read queries while the primary handles writes — replicated data shared across multiple nodes for horizontal read scaling.
- A fintech platform maintaining a standby in a secondary data centre — streaming replication means minimal data loss on failover.
- A MariaDB replica in your Kenya data centre receiving binary log stream from the Ireland primary — near real-time data sharing across regions without application changes.

---

---

# Part Two — Distributed File Sharing

---

## Section 21 — BitTorrent — Peer to Peer File Sharing

The defining distributed file sharing protocol. No central server holds the file. The file is split into pieces distributed across every participant. Every downloader simultaneously uploads to others. The more participants the faster everyone downloads — the inverse of centralised servers.

---

### Components

**Torrent file (.torrent)**
A small metadata file (kilobytes, not the content). Contains file name, total size, piece size, tracker URL, and a SHA-1 cryptographic hash for every piece. The hashes are how integrity is verified — not the server, the mathematics.

**Magnet link**
A modern alternative to the .torrent file. Contains the info hash — a hash of the torrent metadata itself. The client uses this hash to find and download the metadata directly from the swarm. No .torrent file download required.

**Tracker**
A server whose sole job is peer discovery. Maintains a list of peers currently participating in a specific torrent. When a client starts a torrent it announces itself to the tracker and receives a list of peer IP addresses and ports. The tracker never touches the actual file data.

**DHT — Distributed Hash Table**
A decentralised replacement for trackers. Every BitTorrent client stores a small portion of the global peer directory. A client queries nearby DHT nodes to find peers for a given info hash. No central tracker server required — the network itself is the directory. Torrents survive tracker shutdowns because DHT has no single point of failure.

**PEX — Peer Exchange**
Once connected to a few peers your client asks them who else they know. Peers share their peer lists directly — further reducing reliance on any central service.

**Swarm**
The collective name for all peers currently participating in a torrent — both leechers (still downloading) and seeders (complete file, uploading only).

**Pieces and blocks**
The file is divided into fixed-size pieces (typically 256KB to 2MB). Each piece further divided into 16KB blocks for actual wire transfer. Your client requests specific blocks from specific peers and assembles them into pieces. Each completed piece is SHA-1 verified. If verification fails the piece is discarded and re-requested from a different peer.

**Leecher**
A peer currently downloading. Has some pieces which it shares with others but does not yet have the complete file.

**Seeder**
A peer with the complete file uploading to others. Without seeders a torrent eventually dies — new leechers cannot complete their download.

**Ratio**
Upload volume divided by download volume. Above 1.0 means you have given more than you received. Private tracker communities enforce minimum ratio requirements to sustain the network.

---

### How a Download Works

```
1. Obtain a .torrent file or magnet link

2. Client reads metadata
   — file name, size, piece hashes, tracker URL or info hash

3. Client contacts tracker or queries DHT
   — announces: "I need peers for info hash X"
   — receives: list of peer IP addresses and ports

4. Client connects to multiple peers simultaneously
   — typically 30 to 50 concurrent peer connections

5. Client requests specific pieces from specific peers
   — rarest-first algorithm prioritises pieces
     that fewer peers have
   — improves overall swarm health by spreading rare pieces

6. Peers send blocks of pieces to the client
   — multiple pieces downloading from multiple peers
     in parallel simultaneously
   — effective download speed is sum of all
     peer upload speeds combined

7. Client verifies each completed piece
   — SHA-1 hash must match the torrent metadata
   — mismatch: piece discarded, re-requested
     from a different peer

8. Client immediately begins uploading pieces it has
   — even while still downloading
   — simultaneously a leecher and a partial seeder

9. Download completes — all pieces assembled
   — client becomes a full seeder
   — continues uploading until manually stopped
```

---

### How Multiple Sources Work Together

```
CENTRALISED (HTTPS, SFTP, NFS):

  [Server] ─────────────────────────────► [You]
  One source. One stream. Full file.


BITTORRENT:

  [Peer A] ── pieces 1, 7, 12 ─────────► ┐
  [Peer B] ── pieces 3, 8, 15 ─────────► ┤
  [Peer C] ── pieces 2, 5, 11 ─────────► ┼──► [You] assembles + verifies
  [Peer D] ── pieces 4, 9, 14 ─────────► ┤
  [Peer E] ── pieces 6, 10, 13 ────────► ┘

  Simultaneously you upload to others:

  [You] ── pieces 1, 3, 7 ─────────────► [Peer F]
  [You] ── pieces 2, 8, 12 ────────────► [Peer G]
```

---

### Why This Model Is Powerful

**Self-scaling:** More participants means more sources means faster downloads for everyone. A file with 10,000 seeders downloads faster than one with 10. The opposite of centralised servers where more users means slower downloads.

**No single point of failure:** Peer disconnects — client requests their pieces from another. Tracker goes down — DHT and PEX keep the swarm alive. Original publisher disappears — file remains available as long as any seeder exists.

**Cryptographic integrity:** Every piece is SHA-1 verified. Corrupted or tampered pieces are detected and discarded immediately. Stronger guarantee than most centralised protocols.

**Zero publisher bandwidth cost:** Once seeded into the network the publisher needs no servers or bandwidth. The user community is the distribution infrastructure.

---

### Private Trackers

Public torrents use open trackers and DHT — anyone can join. Private tracker communities restrict access:

- DHT and PEX disabled — peer discovery only via the private tracker
- Invite-only registration
- Ratio requirements enforced — only-downloaders are banned
- Creates sustainable communities of reliable long-term seeders
- Content remains well-seeded for years — far better availability than public torrents

---

### BitTorrent vs Centralised Delivery

| Property | BitTorrent | HTTPS / CDN | SFTP | Object Storage |
|---|---|---|---|---|
| Source | Distributed — many peers | Centralised | Centralised | Centralised |
| Scales with demand | Yes — more users means faster | Partially via CDN | No | Yes but costs more |
| Publisher bandwidth cost | Near zero | High | Medium | Medium |
| File integrity | Always — SHA-1 per piece | Optional checksums | Optional | Optional ETags |
| Requires central server | No — DHT removes need | Yes | Yes | Yes |
| Suitable for access control | No — public by nature | Yes | Yes | Yes |
| Survives publisher disappearing | Yes — while seeders exist | No | No | No |
| Best use | Large public distribution | General web delivery | Secure transfer | Scalable app storage |

---

## Section 22 — IPFS and Decentralised Storage

Content-addressed decentralised file storage. Files are addressed by what they are — their cryptographic hash — rather than where they are — a server URL. Any node that has the content can serve it.

---

### IPFS — InterPlanetary File System

**How it works:** A file added to IPFS is split into blocks. Each block is hashed. The top-level hash (CID — Content Identifier) uniquely identifies the file by its content. Any IPFS node that has pinned the file can serve it. You request content by CID — the network finds whoever has it. If content never changes the CID never changes. If the file is modified the CID changes — integrity is guaranteed by the address itself.

**Scenarios:**
- A blockchain application stores NFT assets on IPFS — the asset is not dependent on any single company's servers. The NFT smart contract stores the IPFS CID. As long as any node has pinned the content it remains accessible.
- A censorship-resistant publishing platform distributes content via IPFS — content cannot be taken down by targeting one server because there is no one server.
- A decentralised application serves its frontend from IPFS — available as long as any node has it pinned. No central hosting required.
- A research institution publishes a dataset to IPFS — the CID is the permanent citable reference. Anyone can verify the data has not changed because the hash must match.

---

### Filecoin

A blockchain-based incentive layer built on top of IPFS. Storage providers are paid in FIL cryptocurrency to store and serve content reliably. Provides economic guarantees for persistence — content stays available because providers are paid to keep it.

---

### Storj and Sia

Decentralised storage networks. Files are encrypted client-side, split into pieces using erasure coding, and distributed across many independent storage nodes globally. No single node has the complete file. No node operator can read the file — only the key holder can decrypt and reassemble. Provide an S3-compatible API in some implementations.

**Scenarios:**
- A privacy-focused application storing sensitive user files — not even the storage provider can read the content.
- A decentralised alternative to S3 — pay per GB to a network of independent operators rather than a single cloud provider.

---

## Section 23 — WebRTC — Browser to Browser File Transfer

A browser API enabling direct peer-to-peer connections between browsers. Originally designed for video calling. Its data channel supports arbitrary binary data — including file transfer. Files transfer directly between browsers without passing through a server.

**How it works:** Two browsers use a signalling server (typically HTTPS) to exchange connection metadata (ICE candidates, SDP offer/answer). Once negotiated, a direct DTLS-encrypted peer-to-peer connection is established. Files transfer over this direct channel — the signalling server is no longer involved after connection establishment.

**Scenarios:**
- Snapdrop — browsers on the same WiFi network discover each other, connect via WebRTC data channel, transfer files directly without any server involvement in the transfer.
- ShareDrop and JustBeamIt — browser-to-browser file transfer over the internet via WebRTC. The file never touches a server. The sender and receiver connect directly.
- A privacy-focused file sharing tool where transfer is end-to-end direct between browsers — no server stores the file at any point.
- A web application implementing real-time collaborative file sharing — participants stream file pieces directly to each other via WebRTC data channels.

**Strengths:** File never stored on a server, encrypted DTLS, no installation required, works in any browser.

---

## Section 24 — Local Wireless Transfer

Device-to-device file sharing over local WiFi or Bluetooth. No internet required. No central server. No accounts. Source and destination communicate directly — a distributed local model.

---

### AirDrop

Apple's local wireless transfer protocol. Sender and recipient discover each other via Bluetooth Low Energy. The actual file transfer happens over a direct peer-to-peer WiFi connection — encrypted with TLS. Apple's servers are not involved in the transfer. Works between iPhone, iPad, and Mac.

**Scenarios:**
- A photographer transfers RAW files from a MacBook to a colleague's iPad on a shoot — fast, encrypted, no internet required.
- A team member shares a presentation file instantly in a meeting — no email, no USB, no account.

---

### Android Nearby Share / Windows Nearby Sharing

Google's Android equivalent of AirDrop. Works between Android devices and Chrome OS. Windows Nearby Sharing provides the same capability between Windows machines.

**Scenarios:**
- Android users sharing files between phones and tablets on the same network.
- Windows users sharing files between machines without needing a shared folder or email.

---

### Snapdrop and LANDrop

Cross-platform browser-based local wireless transfer using WebRTC. Both devices open the tool in a browser on the same WiFi network. Files transfer directly between browsers — no installation, no accounts, no OS restriction.

**Scenarios:**
- A mixed environment where AirDrop (Apple) and Nearby Share (Android) are incompatible — Snapdrop works on any device with a browser.
- A field engineer transferring files between a tablet and a laptop with no internet — Snapdrop on the local network.
- A temporary office environment where no shared infrastructure is available — Snapdrop via any browser on any device.

---

---

# All Scenarios — Complete Reference

---

## Scenario 1 — Enterprise Office File Sharing

**Context:** 300 staff across two buildings need shared organised file access by department.

**Primary:** SMB, Windows File Server or Samba, Active Directory
**Supporting:** DFS Namespace and Replication, RSync (backup), SFTP (admin)

IT deploys a Windows File Server. Department shares created — Finance, HR, Engineering. AD groups control access. Staff map shares as drive letters. DFS Namespace presents `\\company\files` as a single path regardless of which underlying server serves the content. DFS Replication keeps the secondary server current for redundancy. RSync backs up share contents nightly to an offsite server. IT manages via SFTP or RDP.

---

## Scenario 2 — Remote and Distributed Teams

**Context:** Staff across multiple countries need shared file access without a central office network.

**Primary:** Nextcloud over WebDAV and HTTPS
**Supporting:** VPN plus NFS or SMB for regional offices, SFTP (admin), Object Storage (backend)

Self-hosted Nextcloud on a VPS with MinIO as backend. Staff sync via desktop client. Large files accessed via WebDAV without full local sync. Regional office staff connect via VPN and mount NFS or SMB for low-latency access to large datasets. External collaborators receive time-limited HTTPS share links. All transfers encrypted via HTTPS or VPN.

---

## Scenario 3 — Software Development and CI/CD

**Context:** A dev team builds, tests, deploys, and manages code across multiple servers.

**Primary:** Git, Object Storage (artifacts), RSync (config distribution)
**Supporting:** SFTP, NFS (shared config mount), SCP, Git LFS, DVC

Code in Git. CI/CD builds artifacts, pushes to object storage. Deployment pulls via S3 API. Config distributed via RSync. App nodes share a common NFS config mount. Logs ship to object storage. Developers pull specific files via SFTP. Large binary assets via Git LFS. Datasets via DVC with object storage backend.

---

## Scenario 4 — Multi-Server Application Infrastructure

**Context:** Ten application servers behind a load balancer all need access to the same files.

**Primary:** NFS (shared hot storage), Object Storage (permanent store)
**Supporting:** RSync (backup), SFTP (admin)

NFS exports uploads, config, and shared libraries. All app servers mount at boot. Object storage holds permanent durable files. RSync backs up NFS exports hourly. New servers mount NFS on first boot and are immediately current.

---

## Scenario 5 — Web Application File Upload

**Context:** Users upload files via browser. Files stored, processed, and retrieved.

**Primary:** HTTPS upload, S3 Presigned PUT (large files), Object Storage, CDN
**Supporting:** NFS scratch (processing workers), Message Queue, Presigned GET (delivery)

Small files POST to app server over HTTPS. Large files use presigned PUT — browser uploads directly to object storage bypassing the app server. App records the object key. Workers virus-scan, resize, convert — using NFS scratch for large intermediate files. Delivery via presigned GET or CDN URL.

---

## Scenario 6 — Fintech and Banking File Exchange

**Context:** Automated payment file exchange with dozens of partner banks.

**Primary:** SFTP with SSH key auth, AS2, MFT Platform
**Supporting:** FTPS (legacy partners), Object Storage (compliance archive), Compliance portal

Each partner has a dedicated SFTP drop folder with SSH key auth. New files trigger processing pipeline. Acknowledgement files written back. Legacy partners use FTPS. EDI partners use AS2 with signed delivery receipts. MFT platform manages all connections, scheduling, retry, alerting, and audit. All files archived to object storage with seven-year retention and WORM locking.

---

## Scenario 7 — Media Platform (Video and Image Hosting)

**Context:** Creators upload videos. Content processed and delivered globally to millions.

**Primary:** S3 Presigned PUT (upload), Object Storage (store), CDN (delivery)
**Supporting:** NFS scratch (transcoding workers), Processing Queue

Creator uploads via presigned PUT directly to object storage. Event triggers transcoding workers. Workers use NFS scratch for intermediate files. Multiple resolution outputs written back to object storage. CDN delivers to viewers globally from edge cache.

---

## Scenario 8 — Healthcare Records Management

**Context:** Patient records, scan images, lab results. Strictly controlled, audited, compliant.

**Primary:** HTTPS portal, Object Storage with encryption and WORM, MFT Platform
**Supporting:** SMB (admin staff), SFTP (lab intake), Archive tier

Clinical staff upload via HTTPS portal. Object storage with strict bucket policies, WORM locking for compliance records, and full access logging. Admin staff access non-clinical documents via SMB. External labs deliver via SFTP. MFT platform governs all external exchanges with full audit trail. Lifecycle policy automatically archives files.

---

## Scenario 9 — Backup and Disaster Recovery

**Context:** Reliable automated backups. Fast restore. Geographic redundancy.

**Primary:** RSync over SSH (server files), Object Storage (database dumps, archives)
**Supporting:** GPG encryption, Cross-region replication, SFTP (manual retrieval)

RSync backs up changed server files nightly — delta only. Database dumps compressed, GPG-encrypted, pushed to object storage. Versioning retains 30 days. Lifecycle moves to archive at 90 days. Cross-region replication provides geographic redundancy. Monthly restore tests verify integrity. NFS and SMB volumes snapshotted and pushed to object storage.

---

## Scenario 10 — Scientific and Research Computing

**Context:** Large cluster computational jobs reading and writing large shared datasets.

**Primary:** NFS or Lustre (cluster storage), Object Storage (archive)
**Supporting:** SFTP, RSync, Globus, DVC

High-performance NFS or Lustre serves all compute nodes. Jobs read and write directly without copying datasets. Researchers pull results via SFTP or RSync. Raw datasets archive to object storage. Inter-institution transfers via Globus or SFTP. DVC versions datasets alongside the code that processes them.

---

## Scenario 11 — HPC and AI/ML Training

**Context:** Hundreds of GPUs need to stream training data faster than a single NFS server can provide.

**Primary:** Lustre or BeeGFS (parallel filesystem), AWS FSx for Lustre (cloud)
**Supporting:** Object Storage (dataset archive), DVC (dataset versioning)

Lustre stripes training data across dozens of storage servers. All GPU nodes read in parallel — aggregate throughput in hundreds of GB/s. Cloud training jobs use FSx for Lustre linked to an S3 bucket — data streams from S3 to Lustre automatically, training runs at full parallel filesystem throughput. DVC ensures training data and code versions are pinned together for reproducibility.

---

## Scenario 12 — Enterprise Data Centre Storage Stack

**Context:** A financial institution needs the highest-performance lowest-latency storage for databases and virtualisation.

**Primary:** Fibre Channel SAN (block storage), iSCSI (secondary block storage)
**Supporting:** NFS (file sharing between servers), Cloud Storage Gateway (hybrid tiering)

FC SAN provides sub-millisecond latency block storage for the trading database and VMware cluster. iSCSI provides block storage for less latency-sensitive workloads. NFS shares sit on top of the SAN — the NFS server itself runs on FC-attached block storage. A cloud storage gateway presents an NFS interface to on-premises systems while tiering cold data to S3 automatically.

---

## Scenario 13 — Content and Software Distribution

**Context:** Distributing large files globally — software installers, game patches, media.

**Primary:** Object Storage (origin), CDN (delivery), BitTorrent (heaviest files)
**Supporting:** SFTP (editorial intake)

CMS uploads to object storage. CDN serves all end users from edge cache. For multi-gigabyte game patches BitTorrent is used — the torrent file is a small CDN download. Actual patch data is distributed peer to peer by the user community. Publisher bandwidth cost drops to near zero for the largest files.

---

## Scenario 14 — IoT and Edge Devices

**Context:** Thousands of sensors and cameras push data files centrally.

**Primary:** SFTP or HTTPS (device push), Object Storage
**Supporting:** Presigned URLs (operator retrieval), HTTPS (firmware distribution back to devices)

Each device agent pushes files on completion. Files land in object storage tagged with device ID and timestamp. Analytics processes new files in near real time. Operators retrieve via presigned URLs from a dashboard. Firmware updates distributed back to devices via HTTPS from object storage.

---

## Scenario 15 — IT Infrastructure Provisioning

**Context:** A data centre needs to provision and reimage many machines automatically.

**Primary:** TFTP + PXE Boot (OS provisioning), Multicast (simultaneous mass imaging)
**Supporting:** HTTP (OS image delivery), NFS (network root filesystem), TFTP (network device firmware)

New servers PXE boot, receive TFTP bootstrap, download kickstart file and OS image, install automatically. Mass reimaging uses multicast — one stream images all machines simultaneously. Network switches and routers download firmware via TFTP from a network management server. Raspberry Pi cluster nodes boot from NFS root filesystem — no local media.

---

## Scenario 16 — Peer to Peer Large-Scale Distribution

**Context:** Distributing a large file to a massive public audience with no central bandwidth cost.

**Primary:** BitTorrent
**Supporting:** HTTPS (torrent file / magnet link distribution), DHT (decentralised peer discovery)

Publisher creates torrent. Torrent distributed via HTTPS. Users open in client. Client contacts tracker or queries DHT for peers. Pieces downloaded from many peers simultaneously. Each piece SHA-1 verified. User seeds to others while downloading. Becomes full seeder on completion. The larger the audience the faster for everyone.

---

## Scenario 17 — Censorship-Resistant and Decentralised Distribution

**Context:** Content that must remain available regardless of server takedowns.

**Primary:** IPFS
**Supporting:** Filecoin (paid persistence), HTTPS gateway (browser access without IPFS client)

Content added to IPFS addressed by CID. Multiple nodes pin the content. Original publisher can disappear and content remains available from other nodes. Blockchain application stores CID in smart contract — asset permanently referenced without depending on any company's infrastructure. Filecoin providers paid to guarantee persistence.

---

## Scenario 18 — Backup to Physical Archive

**Context:** Long-term cold archive at minimum cost, or massive data migration, or air-gapped environment.

**Primary:** LTO Tape (long-term archive), USB/Appliance (air-gapped or migration)
**Supporting:** Hardware write-blocker (forensic), Climate-controlled offsite storage (tape)

Long-term archive to LTO-9 tape at 18TB native per cartridge — cheapest per-GB storage available. Air-gapped classified network uses encrypted USB as the only data channel. 500TB cloud migration uses AWS Snowball — data loaded locally, device shipped, uploaded to S3 directly. Forensic imaging via hardware write-blocker preserves original integrity and chain of custody.

---

## Scenario 19 — Email File Delivery

**Context:** Sending a specific file to a specific known recipient.

**Primary:** SMTP / IMAP
**Supporting:** Object Storage or Cloud Sync link for files exceeding size limits

File Base64-encoded in MIME message, sent via SMTP, retrieved via IMAP. For files over 10–25MB the email body contains a link to object storage or cloud sync instead. Automated systems — invoicing, payroll, bank statements — generate and attach PDFs programmatically.

---

## Scenario 20 — Team Chat File Sharing

**Context:** Quick operational file sharing inside team communication.

**Primary:** Platform HTTPS (Slack, Teams, Telegram)
**Supporting:** SharePoint (Teams backend), Shadow IT policy

Files uploaded to platform storage, shared as links in conversation. Teams files land in SharePoint. Telegram supports 2GB per file. Compliance note: chat file sharing often falls outside corporate retention policies — shadow IT and audit risk must be managed by policy.

---

## Scenario 21 — Enterprise Multi-Partner File Exchange

**Context:** Managing automated file exchanges with dozens of external partners using different protocols.

**Primary:** MFT Platform (IBM Sterling, GoAnywhere, MOVEit)
**Supporting:** SFTP, FTPS, AS2, FTP (legacy partners)

Each partner connection configured in MFT platform — protocol, credentials, schedule, paths, retry, alerting. Platform executes all transfers automatically. Every file logged with timestamp and checksum. Compliance dashboard shows full audit trail. New partner onboarded in hours.

---

## Scenario 22 — Microservice File Pipeline

**Context:** Multiple microservices pass files through a processing pipeline without tight coupling.

**Primary:** Object Storage as universal handoff, Message Queue for coordination
**Supporting:** S3 API, Presigned URLs, HTTPS

No service passes file bytes over API calls. Each service writes output to object storage, publishes the object key to a queue. Next service reads the key, pulls the file, processes it, writes output to object storage under a new key, publishes forward. Services fully decoupled. Failures retryable. No service is a bottleneck.

---

## Scenario 23 — Local and Same-Room Transfer

**Context:** Two devices in the same location need to transfer files instantly.

**Primary:** AirDrop (Apple), Nearby Share (Android/Windows), Snapdrop (cross-platform)
**Supporting:** WebRTC (Snapdrop peer connection)

AirDrop — Bluetooth discovery, direct WiFi transfer, TLS encrypted, no internet, Apple-only. Nearby Share — Android to Android or Windows to Windows. Snapdrop — any device, any OS, browser-based, WebRTC peer to peer, no installation, no internet required.

---

## Scenario 24 — Media Streaming on Local Network

**Context:** A media library shared across all devices on a home or office network without file copying.

**Primary:** DLNA / UPnP (automatic device discovery and streaming), Plex / Jellyfin (transcoding and remote access)
**Supporting:** SMB (direct file access fallback), NFS (if media stored on NAS)

DLNA server on NAS advertises media library. Smart TVs and games consoles discover and stream automatically. Plex transcodes to match device capability and available bandwidth. Accessible locally and remotely over HTTPS. Media files stored on NAS via NFS or SMB — DLNA and Plex serve as the delivery layer on top.

---

## Scenario 25 — Database Replication as Shared Data

**Context:** A primary database sharing live data with replicas in other regions for DR and read scaling.

**Primary:** PostgreSQL WAL streaming or MariaDB binary log replication
**Supporting:** VPN or dedicated circuit (transport), Object Storage (base backup for replica initialisation)

Primary streams WAL or binary log changes to standbys in near real time. Standbys replay changes and stay current. Read replicas serve read queries. A standby in a secondary data centre receives streaming replication over a VPN or dedicated circuit — minimal data loss on failover. Initial replica creation via base backup from object storage — full database dump restored then streaming replication takes over.

---

---

## The Universal Three-Layer Pattern

Every file sharing scenario regardless of industry, scale, or technology is a combination of three layers:

```
┌─────────────────────────────────────────────────────────────────┐
│                        INTAKE LAYER                             │
│  How files enter the system                                     │
│                                                                 │
│  HTTPS upload · SFTP drop · Email attachment · SMB write        │
│  NFS write · Device push (IoT) · Git push · PXE / TFTP          │
│  Physical media · AirDrop · Nearby Share · MFT scheduled pull   │
│  REST API POST · BitTorrent seed · Browser presigned PUT        │
│  Messaging platform upload · RDP drive mapping                  │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                       STORAGE LAYER                             │
│  Where files live                                               │
│                                                                 │
│  Object Storage · NFS export · SMB share · Lustre / BeeGFS      │
│  Local disk · iSCSI / FC block storage · Database BLOB          │
│  Git repository · LTO tape · Cloud sync platform               │
│  MFT staging area · IPFS network · BitTorrent swarm             │
│  Physical media · HDFS · Cloud-managed FS (EFS, Azure Files)    │
└──────────────────────────┬──────────────────────────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                      DELIVERY LAYER                             │
│  How files reach consumers                                      │
│                                                                 │
│  CDN edge (HTTPS) · Presigned GET URL · SMB mount · NFS mount   │
│  SFTP pull · RSync pull · WebDAV mount · Email attachment       │
│  Chat platform link · AirDrop · Physical media · API response   │
│  BitTorrent download · IPFS gateway · Git clone / pull          │
│  Globus transfer · DLNA stream · Plex stream · RDP drive map    │
│  Multicast stream · iSCSI / FC block attachment                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Complete Master Reference Table

| Scenario | Primary | Supporting | Model |
|---|---|---|---|
| Enterprise office shared drives | SMB, DFS | RSync, SFTP, AD, Kerberos | Centralised |
| Remote and distributed teams | Nextcloud, WebDAV | VPN+NFS/SMB, Object Storage | Centralised |
| Dev infrastructure and CI/CD | Git, Object Storage, RSync | SFTP, NFS, Git LFS, DVC | Centralised |
| Multi-server application | NFS, Object Storage | RSync, SFTP | Centralised |
| Web app file upload | HTTPS, Object Storage, CDN | NFS scratch, Queue, Presigned URLs | Centralised |
| Fintech partner exchange | SFTP, AS2, MFT | FTPS, Object Storage, WORM | Centralised |
| Media and video platform | Object Storage, CDN | Presigned URLs, NFS scratch | Centralised |
| Healthcare records | HTTPS, Object Storage, MFT | SMB, SFTP, Archive, WORM | Centralised |
| Backup and disaster recovery | RSync, Object Storage | GPG, Replication, SFTP | Centralised |
| Research and HPC | NFS, Object Storage | SFTP, RSync, Globus, DVC | Centralised |
| HPC and AI/ML training | Lustre, BeeGFS, FSx | Object Storage, DVC | Centralised |
| Enterprise data centre storage | FC SAN, iSCSI | NFS, Cloud Gateway | Centralised |
| Content and software delivery | Object Storage, CDN | BitTorrent, SFTP | Centralised + Distributed |
| IoT data collection | SFTP, HTTPS | Object Storage, Presigned URLs | Centralised |
| IT infrastructure provisioning | TFTP, PXE, Multicast | HTTP, NFS | Centralised |
| Peer to peer large distribution | BitTorrent | HTTPS, DHT, PEX | Distributed |
| Censorship-resistant distribution | IPFS, Filecoin | HTTPS gateway | Distributed |
| Physical and air-gapped transfer | USB, LTO Tape, Appliance | Write-blocker, Sneakernet | Centralised (physical) |
| Email file delivery | SMTP / IMAP | Object Storage link | Centralised |
| Team chat file sharing | Platform HTTPS | SharePoint, Policy | Centralised |
| Enterprise MFT multi-partner | MFT Platform | SFTP, FTPS, AS2, FTP | Centralised |
| Microservice file pipeline | Object Storage + Queue | S3 API, Presigned URLs | Centralised |
| Same-room local transfer | AirDrop, Nearby Share, Snapdrop | WebRTC | Distributed (local) |
| Local media streaming | DLNA, Plex, Jellyfin | SMB, NFS | Centralised |
| Database replication | WAL streaming, Binlog | VPN, Object Storage | Centralised |

---

## Choosing the Right Mechanism

**Browser or end user over the internet**
→ HTTPS upload, Presigned URL, CDN, Cloud sync platform

**Automated machine-to-machine between known systems**
→ SFTP (internet-facing), RSync (server sync), AS2 (B2B with receipts), MFT (multi-partner governed)

**Applications treating remote storage as local disk — Linux/data centre**
→ NFS, WebDAV, AWS EFS, Google Cloud Filestore

**Applications treating remote storage as local disk — Windows/mixed**
→ SMB, DFS, Azure Files, AWS FSx for Windows

**Highest performance storage for databases and virtualisation**
→ Fibre Channel SAN, iSCSI

**Massive parallel throughput for HPC or AI/ML training**
→ Lustre, BeeGFS, GPFS, AWS FSx for Lustre

**Big data distributed processing**
→ HDFS (existing platforms), Object Storage + Spark (new platforms)

**Durable scalable application file storage**
→ Object Storage — hot tier for active files, archive tier for compliance

**Collaborative file working with full history**
→ Git (code and config), Cloud sync platform (documents), DVC (datasets), Git Annex (mixed collections)

**Governed multi-partner enterprise exchange with compliance**
→ MFT Platform over SFTP, FTPS, AS2

**Massive public distribution with no central bandwidth cost**
→ BitTorrent — scales with demand, publisher cost near zero

**Censorship-resistant or permanently referenced content**
→ IPFS — content addressed by hash, survives any single node disappearing

**No network or impractical data volume for network transfer**
→ Physical media — USB for air-gapped, LTO tape for cold archive, transfer appliance for massive migration

**Two devices in the same room**
→ AirDrop, Nearby Share, or Snapdrop — no internet, no accounts, instant

**Network device firmware and OS provisioning**
→ TFTP + PXE Boot, Multicast for mass simultaneous imaging

**Media streaming to local devices without file copying**
→ DLNA, Plex, or Jellyfin on the local network

**Quick operational sharing in team communication**
→ Slack or Teams — fast and convenient, but manage retention and compliance by policy
