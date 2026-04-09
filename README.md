# File-Sharing

# File Sharing — The Definitive Complete Reference

---

## What File Sharing Is

File sharing is any mechanism by which files stored in one location are made accessible to another system, user, process, or organisation — over a local network, the internet, between services, or physically. It underpins every area of computing: business operations, software infrastructure, media, security, healthcare, finance, research, and personal use.

Every scenario where a file needs to move, be accessed remotely, be synchronised, or be made available to more than one consumer involves file sharing in some form.

---

## The Two Fundamental Models

Every file sharing mechanism falls into one of two models:

**Centralised** — there is a single authoritative source. All clients connect to that source to upload or download. The source controls access, availability, and integrity. If the source goes down, access is lost.

**Distributed** — there is no single source. Files or pieces of files are spread across many participants. Clients fetch from multiple sources simultaneously. No single node going down breaks availability.

---

## Complete Taxonomy

```
FILE SHARING
│
├── CENTRALISED
│   ├── Network Mounts          SMB, NFS, AFP, WebDAV
│   ├── Secure Transfer         SFTP, SCP, RSync
│   ├── Legacy Transfer         FTP, FTPS
│   ├── B2B Transfer            AS2, MFT Platforms
│   ├── Web and API             HTTPS, Presigned URLs, REST API
│   ├── Object Storage          S3, Azure Blob, MinIO, GCS
│   ├── CDN                     Cloudflare, CloudFront, Fastly
│   ├── Cloud Sync Platforms    Dropbox, Google Drive, OneDrive,
│   │                           SharePoint, Nextcloud, Box
│   ├── Messaging Platforms     Slack, Teams, Telegram, WhatsApp
│   ├── Version Control         Git, Git LFS, DVC
│   ├── Database Storage        PostgreSQL BLOB, MongoDB GridFS
│   ├── Email                   SMTP / IMAP attachments
│   └── Physical Media          USB, LTO Tape, DVD, Transfer Appliance
│
└── DISTRIBUTED
    ├── Peer to Peer            BitTorrent
    ├── Decentralised Storage   IPFS, Filecoin, Storj
    └── Local Wireless          AirDrop, Nearby Share, Snapdrop
```

---

## Protocol and Tool Reference

| Type | Protocol / Tool | Port / Transport | Encryption | Access Model | Model |
|---|---|---|---|---|---|
| Network Mount | SMB / CIFS | TCP 445 | SMB3 encrypts | Mount as drive | Centralised |
| Network Mount | NFS | TCP/UDP 2049 | NFSv4 + Kerberos | Mount as directory | Centralised |
| Network Mount | AFP | TCP 548 | TLS | Mount as drive | Centralised |
| Network Mount | WebDAV | TCP 80/443 | TLS | Mount or browser | Centralised |
| Secure Transfer | SFTP | TCP 22 | SSH always | CLI / client | Centralised |
| Secure Transfer | SCP | TCP 22 | SSH always | CLI copy | Centralised |
| Secure Transfer | RSync | TCP 22 SSH mode | SSH | Delta sync | Centralised |
| Legacy Transfer | FTP | TCP 21 | None | CLI / client | Centralised |
| Legacy Transfer | FTPS | TCP 21/990 | TLS | CLI / client | Centralised |
| B2B Transfer | AS2 | TCP 443 | TLS + signing | Automated B2B | Centralised |
| B2B Transfer | MFT Platform | SFTP/FTPS/AS2 | Always enforced | Governed platform | Centralised |
| Web / API | HTTPS | TCP 443 | TLS always | Browser / API | Centralised |
| Web / API | Presigned URL | TCP 443 | TLS always | Browser / API | Centralised |
| Object Storage | S3 API | TCP 443 | TLS always | API / SDK | Centralised |
| CDN | HTTPS edge | TCP 443 | TLS always | Browser / API | Centralised |
| Cloud Sync | Nextcloud / Drive | TCP 443 | TLS always | Sync client / browser | Centralised |
| Messaging | Slack / Teams | TCP 443 | TLS always | App / browser | Centralised |
| Version Control | Git / Git LFS | TCP 22 / 443 | SSH / TLS | CLI / GUI | Centralised |
| Database | BLOB / GridFS | Internal | App-layer | SQL / query | Centralised |
| Email | SMTP / IMAP | TCP 587/993 | TLS | Mail client | Centralised |
| Physical | USB / LTO Tape | Physical | Encrypted device | Direct | Centralised |
| Peer to Peer | BitTorrent | TCP 6881+ | Optional | P2P client | Distributed |
| Decentralised | IPFS | TCP 4001 | Optional | CLI / gateway | Distributed |
| Local Wireless | AirDrop / Snapdrop | WiFi / Bluetooth | Always | Device UI | Distributed |

---

# Centralised File Sharing

---

## 1. Network Mounts

Remote directories mounted and used as if they were local disk. Applications read and write without knowing the storage is remote.

---

### SMB / CIFS — Server Message Block

The dominant LAN file sharing protocol. Originates from Windows. Implemented on Linux by Samba. Clients mount a named share and interact with it exactly like a local folder.

**Authentication:** Windows credentials or Active Directory. On Linux via Kerberos or local Samba accounts.

**Scenarios:**
- A company with 200 staff maps `\\fileserver\Finance` as a drive letter. All staff read and write to the same central location. Active Directory controls who can access which share.
- A Linux Samba server serving files to a mixed Windows and Linux office — cross-platform transparency.
- A NAS device sharing a media library across all devices on a home or office network.
- A developer mounting a remote project folder from a VM onto their local machine for live editing.

**Strengths:** Native Windows integration, broad OS support, fine-grained permission control via AD, works seamlessly for end users.

**Limitations:** Designed for LAN — performs poorly over high-latency WAN links. Not suitable for internet-facing access.

---

### NFS — Network File System

The Unix and Linux equivalent of SMB. Standard in data centres, HPC clusters, and Linux-heavy infrastructure. Access is controlled by IP address and optionally Kerberos. NFSv3 has no built-in encryption — safe only on trusted networks. NFSv4 adds security improvements.

**Scenarios:**
- Ten application servers behind a load balancer all mount `/mnt/uploads` from the same NFS server. A file written by any server is immediately readable by all others — no synchronisation logic needed in the application.
- A Kubernetes cluster using NFS as a persistent volume backend shared across pods.
- A render farm where all compute nodes mount the same asset library — no copying datasets per node.
- Two data centre nodes in different regions sharing configuration directories over a VPN tunnel.

**Strengths:** Transparent to applications, high performance on LAN, scales well across many clients.

**Limitations:** NFSv3 has no encryption — only use on trusted networks or over VPN. NFS over high-latency WAN is slow and unreliable.

---

### AFP — Apple Filing Protocol

Apple's legacy LAN file sharing protocol. Deprecated — macOS now defaults to SMB even for Apple-to-Apple transfers.

**Scenarios:**
- Legacy Mac environments and older NAS devices that predate the SMB default switch.
- Still found in some Time Machine configurations on older hardware.

---

### WebDAV — Web Distributed Authoring and Versioning

File transfer and management over HTTP/HTTPS. Extends HTTP with methods for creating, moving, copying, and deleting files remotely. Can be mounted as a network drive on most operating systems.

**Scenarios:**
- Nextcloud and ownCloud expose storage via WebDAV — clients mount it as a network drive or sync via the desktop client.
- Older SharePoint versions used WebDAV for file access from Windows Explorer.
- A remote team mounting a WebDAV share over HTTPS to access files without VPN.
- CalDAV and CardDAV — extensions of the same protocol used for calendar and contact sync.

**Strengths:** Works over standard HTTPS, firewall-friendly, cross-platform mountable.

**Limitations:** Higher overhead than NFS or SMB for large file operations. Not suited for high-performance data centre workloads.

---

## 2. Secure Transfer

File transfer over encrypted channels. Files are explicitly sent or received — no persistent mount. Used by administrators, automated scripts, CI/CD pipelines, and external partner integrations.

---

### SFTP — SSH File Transfer Protocol

File transfer over SSH. Completely separate from FTP despite the name. Everything is encrypted — credentials, commands, and file data. Supports browsing, uploading, downloading, renaming, deleting, and directory creation on the remote filesystem.

**Authentication:** SSH key pairs (preferred) or passwords.

**Scenarios:**
- A developer deploying files to a production server.
- A cron job pushing nightly reports to a partner's server on a schedule.
- A bank or fintech platform receiving ISO 20022 or MT940 payment files from a counterparty — each partner has a dedicated drop folder, authenticates via SSH key, and the platform monitors for new arrivals.
- A customer portal where clients drop sensitive documents into a secure intake folder.
- Automated backup scripts sending compressed encrypted archives offsite nightly.
- A sysadmin pulling log files from a remote server for analysis.
- CI/CD pipelines pushing build artifacts to a staging server.

**Strengths:** Universal support, strong encryption, key-based auth eliminates password risk, full remote filesystem management.

---

### SCP — Secure Copy Protocol

Also runs over SSH. Designed purely for copying files — no browsing or remote filesystem management. Simpler than SFTP. Being phased out in favour of SFTP in most modern tools.

**Scenarios:**
- Quick one-off file copies between servers: `scp archive.tar.gz user@server:/backup/`
- Scripts that need simple no-frills remote copy without SFTP overhead.

---

### RSync

A synchronisation tool that runs over SSH or its own daemon. Transfers only the changed parts of files using a delta algorithm — making it highly efficient for large files or large directory trees where most content does not change between syncs.

**Scenarios:**
- Incremental server backups: `rsync -avz /data/ backup-server:/backups/data/` — only changed blocks transferred.
- Keeping two servers in sync — primary to replica, syncing continuously or on schedule.
- Migrating a server — RSync the full filesystem, then do a final delta sync at cutover to minimise downtime.
- Distributing configuration files from a master config server to all application nodes.
- Syncing a local development directory to a remote staging server during development.
- Backing up NFS and SMB share contents to an offsite backup server nightly.

**Strengths:** Delta transfer minimises bandwidth, resumable, preserves permissions and timestamps, highly scriptable.

---

## 3. Legacy Transfer

---

### FTP — File Transfer Protocol

The original file transfer protocol. Completely plaintext — credentials and data transmitted unencrypted. Should not be used for anything internet-facing or sensitive.

**Scenarios:**
- Legacy web hosting — uploading HTML files to an old shared hosting provider.
- Isolated internal lab environments on air-gapped networks where encryption is not a concern.
- Old enterprise systems that have never been updated and cannot support SFTP.

**Limitations:** No encryption. Credentials visible on the network. Actively dangerous on any untrusted network.

---

### FTPS — FTP Secure

FTP with TLS encryption layered on top. Encrypts credentials and data. Separate from SFTP — completely different protocol stack.

**Scenarios:**
- Organisations that must use FTP for legacy compatibility with partners but require encryption.
- EDI file exchanges with supply chain partners whose systems predate SFTP support.
- Some banking and insurance file exchange systems still using FTPS for historical reasons.

---

## 4. B2B and Enterprise Transfer

---

### AS2 — Applicability Statement 2

An HTTP-based protocol designed specifically for secure reliable business-to-business file exchange. Provides TLS encryption, digital signatures for non-repudiation, and delivery receipts (MDN — Message Disposition Notification). The receiver sends a signed acknowledgement confirming receipt and integrity.

**Scenarios:**
- A retailer exchanging purchase orders and invoices with hundreds of suppliers — each exchange is signed and acknowledged, providing legal non-repudiation.
- EDI (Electronic Data Interchange) file exchange in supply chain, logistics, and retail.
- Healthcare networks exchanging patient records between systems with proof of delivery.
- Any B2B scenario where the sender needs cryptographic proof the file arrived intact and unmodified.

**Strengths:** Non-repudiation via signed receipts, widely supported in supply chain and retail, encrypted and signed end to end.

---

### MFT Platforms — Managed File Transfer

A software category providing a governed, auditable, automated platform for file transfer between organisations and systems. Sits above raw protocols and adds workflow automation, scheduling, encryption enforcement, retry logic, alerting, and compliance reporting. Examples include IBM Sterling, GoAnywhere MFT, MOVEit, and Axway.

**Scenarios:**
- A bank managing file exchanges with 80 counterparties across SFTP, FTPS, AS2, and legacy FTP — all managed from one platform with a single audit trail.
- A healthcare network automating HIPAA-compliant file exchanges between hospitals, labs, and insurers — the platform enforces encryption, logs every transfer, and alerts on failure.
- A government agency automating file ingestion from multiple data providers with full audit trail for regulatory accountability.
- Onboarding a new trading partner — configure the connection in the MFT platform in hours rather than building a custom integration.

**Strengths:** Single platform for all protocols, enforced encryption, complete audit trail, scheduling and retry, compliance reporting built in.

---

## 5. Web and API Delivery

---

### HTTPS Upload and Download

Files delivered over HTTP/HTTPS. The web server is the interface. The actual storage may be local disk, NFS, or object storage behind the scenes.

**Scenarios:**
- A user uploads a file via a browser form — the browser POSTs the file to the app server over HTTPS.
- A web server directly serves static files from a directory — software downloads, public datasets, documentation.
- An internal tool exposing build artifacts or processed reports via a simple URL.
- A REST API endpoint accepting a file upload and returning a processed result.

---

### Presigned URLs

A time-limited cryptographically signed URL generated by an object storage service. Grants temporary access to a specific file without requiring the requester to have storage credentials. Can be generated for upload (PUT) or download (GET).

**Scenarios:**
- A web app generates a presigned PUT URL. The browser uploads a large video directly to object storage — bypassing the app server entirely. App server never handles the file bytes.
- A user requests a download. The app generates a presigned GET URL expiring in 15 minutes. The user's browser downloads directly from object storage.
- A microservice passes a presigned URL to a downstream service so it can retrieve a file without needing storage credentials.
- Sharing a specific file from a private bucket with an external party for a limited time window.

---

## 6. Object Storage

Files stored as objects in flat namespaces (buckets) addressed by key. Accessed via HTTP API. No filesystem hierarchy — just bucket, key, and value. The modern standard for durable scalable file storage in production systems.

**Providers:** AWS S3, Google Cloud Storage, Azure Blob Storage, MinIO (self-hosted), Wasabi, Backblaze B2.

**Key features:** Versioning, lifecycle policies (auto-archive or delete after N days), cross-region replication, event notifications on new objects, presigned URLs, encryption at rest and in transit.

**Scenarios:**
- A production web application storing all user-uploaded files. App servers store only the object key in the database.
- A data pipeline where each processing stage writes output to object storage and passes the key to the next stage via a message queue.
- A fintech platform archiving seven years of transaction documents for regulatory compliance — lifecycle policy automatically moves files to archive tier after 90 days.
- A microservice architecture where object storage is the universal handoff point between services — no service passes file bytes directly over API calls.
- Database backups compressed, encrypted, and pushed to object storage nightly. Versioning retains 30 days of history. Cross-region replication provides geographic redundancy.
- ML training datasets stored centrally in object storage and pulled by training jobs on demand.
- Static website hosting — HTML, CSS, JS served directly from an S3 bucket behind a CDN.

**Strengths:** Scales to any size, decouples storage from compute, built-in redundancy, lifecycle management, globally accessible via HTTPS.

---

## 7. CDN — Content Delivery Network

A globally distributed network of edge servers that cache files close to end users. The origin (object storage or web server) is only hit once per region per file. All subsequent requests for that region are served from the edge cache.

**Providers:** Cloudflare, AWS CloudFront, Fastly, Akamai.

**Scenarios:**
- A news site serving images and videos — CDN absorbs millions of requests that would otherwise hit the origin server.
- A software company distributing a 2GB installer globally — each region's CDN node caches it after the first download. Users everywhere get fast local download speeds.
- A game studio distributing a day-one patch to millions of players simultaneously — without CDN the origin would be overwhelmed.
- An e-learning platform serving course video content — students in all regions get smooth playback from a nearby edge node.
- A government agency publishing public data files — CDN makes downloads fast globally without the agency paying for international bandwidth.

**Strengths:** Dramatic latency reduction for geographically distributed users, protects origin from traffic spikes, reduces origin bandwidth cost.

---

## 8. Cloud Sync Platforms

Managed platforms that combine storage, synchronisation, versioning, sharing, and collaboration in one product. Abstract the underlying protocol — typically HTTPS with a proprietary sync protocol. The most common file sharing experience for non-technical users.

**Consumer:** Google Drive, Dropbox, iCloud Drive, OneDrive.
**Enterprise:** SharePoint, Box, Google Workspace Drive, OneDrive for Business, Nextcloud (self-hosted).

**How sync works:** A desktop client monitors a local folder. When a file changes, the client uploads the delta to the platform's servers. Other devices running the same client download the delta and apply it. All devices converge to the same state. Files can also be accessed via web browser or mobile app without syncing locally.

**Scenarios:**
- A company using SharePoint as its intranet file store, integrated with Microsoft 365 — staff edit documents collaboratively, version history is automatic.
- A freelancer sharing a final deliverable with a client via a Dropbox link — client downloads without needing an account.
- A startup using Google Workspace Drive as its entire file server — no on-premise infrastructure needed.
- A legal firm using Box for secure client document exchange — granular permissions, expiry dates on share links, full audit logs.
- A self-hosted Nextcloud instance with MinIO as its backend — company retains full data ownership, staff get a Dropbox-like experience.
- An individual automatically backing up phone photos to iCloud or Google Photos.

**Strengths:** Versioning, sharing links, access controls, audit trails, collaboration features, works on all devices, no infrastructure management for hosted platforms.

**Limitations:** Data sovereignty concerns with hosted platforms — your files live on someone else's infrastructure. Files shared via personal accounts bypass corporate controls (shadow IT risk).

---

## 9. Messaging Platforms as File Sharing

Slack, Microsoft Teams, Telegram, and WhatsApp all support file sharing as part of their messaging functionality. Files are uploaded to the platform's infrastructure over HTTPS and stored in their object storage backend.

**How it works:** A user drags a file into a conversation. The platform uploads it to its own storage, generates a download link, and embeds it in the message. Recipients click to download over HTTPS. Teams stores files in SharePoint behind the scenes, giving them a persistent location in the team's document library.

**Scenarios:**
- A developer shares a log file in a Slack channel for the team to inspect — faster than setting up SFTP access.
- A manager sends a spreadsheet to a colleague via Teams — it lands in the SharePoint document library automatically.
- Field workers send photos from a mobile device via WhatsApp to a central coordinator — but files are compressed by WhatsApp, which may be unacceptable for professional use.
- A Telegram channel distributes large archives and software builds to a subscriber community — Telegram supports files up to 2GB per transfer.

**Important considerations:**
- Files shared in chat are often not covered by corporate data retention and compliance policies — a significant audit risk.
- Sensitive files shared via personal WhatsApp bypass all corporate access controls — a shadow IT and data leakage risk.
- Retention periods vary by platform and plan — files may be automatically deleted on free tiers.

---

## 10. Version Control as File Sharing

Git and similar systems are file sharing mechanisms with history, attribution, and collaboration built in. Every clone is a full copy of all files and their complete history. Push and pull are fundamentally file synchronisation operations between machines.

**Components:**
- **Git** — versions text files and source code. Every commit is a snapshot of all tracked files.
- **Git LFS (Large File Storage)** — extends Git for binary files. The LFS pointer (a few bytes) lives in Git. The actual binary lives on an LFS server. Keeps the Git repository small.
- **DVC (Data Version Control)** — extends Git for large datasets. Metadata and pointers in Git. Actual data bytes in object storage (S3, GCS, Azure Blob). Used in data science and ML workflows.

**Scenarios:**
- A development team sharing and collaborating on source code — every change attributed to a person, every version recoverable.
- Infrastructure teams managing Terraform, Ansible, and Kubernetes manifests in Git — every infrastructure change versioned and auditable.
- A data science team using DVC to version datasets alongside the code that processes them — model training is reproducible because both code and data versions are pinned.
- Design teams using Git LFS to version Figma exports, PSD files, and video assets — binary assets versioned alongside the code that uses them.
- A technical writing team managing documentation in Markdown in Git — docs live with the product, changes reviewed via pull request.

**Strengths:** Complete history of every file change, attribution, branching, conflict resolution, distributed copies, pull request review workflow.

---

## 11. Database as File Store

Files stored directly inside a database as Binary Large Objects. The application retrieves them via queries rather than filesystem paths. Simple to implement but does not scale for large volumes or high-frequency access.

**Technologies:** PostgreSQL bytea and Large Objects, MySQL BLOB types, MongoDB GridFS (splits files into 255KB chunks for files over 16MB), Oracle BLOB.

**Scenarios:**
- A small application storing user avatars in PostgreSQL — simple, no additional infrastructure, easy to back up with the database.
- A legacy enterprise document management system storing all PDFs as Oracle BLOBs alongside their metadata — everything in one place, but backups are enormous.
- MongoDB GridFS storing large media files by chunking them across multiple documents — allows files larger than MongoDB's 16MB document limit.
- A migration project extracting database BLOBs, writing them to object storage, and updating the application to use presigned URLs — the standard modernisation path.

**Limitations:** Databases are not optimised for serving binary files. Backups become very large. Does not scale at high volume. Generally replaced by object storage in modern architectures — database stores only metadata and the object key.

---

## 12. Email Attachments

Files encoded and embedded inside email messages. One of the most universally used file delivery mechanisms despite its limitations.

**How it works:** The file is Base64-encoded and embedded in the MIME message body. The sending mail client submits the message via SMTP. The recipient's server stores it. The recipient retrieves it via IMAP or POP3 and the mail client decodes the attachment.

**Scenarios:**
- A finance manager sends a PDF invoice to a client — simple, direct, no shared infrastructure required.
- A bank sends a monthly statement as a PDF attachment to a customer automatically — the system generates and attaches the document programmatically via SMTP.
- A payroll system emails payslips to all employees on payday — each email contains a personalised PDF.
- A file too large for email is instead shared via a link to object storage or a cloud sync platform included in the email body — the email becomes the notification, not the delivery mechanism.

**Limitations:**
- Most mail servers cap attachment size at 10 to 25MB.
- No version control — multiple email threads with different versions of the same document cause confusion.
- Malicious attachments are a primary malware delivery vector — all attachments should be scanned at the mail gateway.

---

## 13. Physical Media Transfer

File transfer via physical storage devices. The only option for air-gapped environments. The most cost-effective option for truly massive data volumes. The cheapest option for long-term cold archiving.

**Media types:** USB flash drive, External HDD/SSD, SD card, DVD/Blu-ray, LTO tape, Cloud provider transfer appliance (AWS Snowball, Azure Data Box).

**Scenarios:**

**Air-gapped environments:** A government classified network or industrial control system has no internet connection by design. Files move in and out only via encrypted USB drives verified and scanned at a security checkpoint. Physical media is the only channel — this is intentional.

**Massive data migration:** A company needs to move 500TB to a cloud provider. Transferring over the internet would take months. An AWS Snowball appliance is shipped to the company, data is loaded locally, the device is shipped back, and the provider uploads directly to object storage. Transfer time drops from months to days.

**Long-term archiving:** A broadcaster archives every programme to LTO tape. A single LTO-9 tape holds 18TB natively (45TB compressed). Tapes are stored offsite in a climate-controlled facility. Cost per GB on tape is a fraction of any cloud storage tier — the cheapest storage available for data that must be retained for decades.

**Forensic transfer:** A forensic investigator connects a seized device via a hardware write-blocker and images it to an external SSD. The write-blocker ensures the original is not modified, preserving forensic integrity and chain of custody.

---

# Distributed File Sharing

---

## 14. BitTorrent — Peer to Peer File Sharing

The defining distributed file sharing protocol. No central server holds the file. The file is split into pieces distributed across every participant. Every downloader simultaneously uploads to others. The more participants, the faster everyone downloads — the opposite of centralised servers.

---

### Components

**Torrent file (.torrent)**
A small metadata file containing the file name, total size, piece size, tracker URL, and a SHA-1 cryptographic hash for every piece of the file. The hash of each piece is how integrity is verified — not the server, not the publisher, the mathematics.

**Magnet link**
A modern alternative to the .torrent file. Contains the info hash — a hash of the torrent metadata itself. The client uses this hash to find and download the metadata directly from the swarm. No .torrent file download required.

**Tracker**
A server whose sole job is peer discovery. It maintains a list of peers currently participating in a specific torrent. When your client starts a torrent it announces itself to the tracker and receives a list of peer IP addresses and ports. The tracker never touches the actual file data.

**DHT — Distributed Hash Table**
A decentralised replacement for trackers. Instead of one tracker server knowing all peers, every BitTorrent client stores a small portion of the peer directory. Your client queries nearby DHT nodes to find peers for a given info hash. No central server required — the network itself is the tracker. This is why torrents survive even when tracker sites are shut down.

**PEX — Peer Exchange**
Once connected to a few peers, your client asks them who else they are connected to. Peers share their peer lists directly with each other — further reducing reliance on any central server.

**Swarm**
The collective name for all peers currently participating in a torrent — both those still downloading and those who have finished and are uploading.

**Pieces and blocks**
The file is divided into fixed-size pieces (typically 256KB to 2MB). Each piece is further divided into blocks (typically 16KB) for actual transfer. Your client requests specific blocks from specific peers and assembles them into pieces. Each completed piece is verified against its hash. If verification fails the piece is discarded and re-requested from a different peer.

**Leecher**
A peer currently downloading. They have some pieces which they share with others but do not yet have the complete file.

**Seeder**
A peer who has the complete file and is uploading to others. Without seeders a torrent dies — incomplete pieces cannot be assembled by new downloaders.

**Ratio**
Upload volume divided by download volume. A ratio above 1.0 means you have given more than you received. Private tracker communities enforce minimum ratio requirements to keep the network healthy.

---

### How a Download Actually Works

```
1. You obtain a .torrent file or magnet link

2. Your client reads the metadata
   — file name, size, piece hashes, tracker URL or info hash

3. Your client contacts the tracker or queries DHT
   — announces: "I need peers for info hash X"
   — receives: list of peer IP addresses and ports

4. Your client connects to multiple peers simultaneously
   — typically 30 to 50 concurrent peer connections

5. Your client requests specific pieces from specific peers
   — uses rarest-first algorithm
   — pieces fewer peers have are prioritised
   — this improves overall swarm health by spreading rare pieces

6. Peers send blocks of those pieces to your client
   — multiple pieces downloading from multiple peers in parallel
   — your download bandwidth is the sum of all peer upload speeds

7. Your client verifies each completed piece
   — SHA-1 hash of received piece must match the torrent metadata
   — if mismatch: piece discarded, re-requested from a different peer

8. Your client immediately begins uploading pieces it has
   — even while still downloading you upload to other leechers
   — you are simultaneously a leecher and a partial seeder

9. Download completes — all pieces assembled into the final file
   — your client becomes a full seeder
   — you continue uploading until you manually stop
```

---

### How Multiple Sources Work Together

```
TRADITIONAL CENTRALISED (HTTPS, SFTP, NFS):

  [Server] ──────────────────────────────────► [You]
  One source. One stream. Full file from one place.


BITTORRENT DISTRIBUTED:

  [Peer A] ── pieces 1, 7, 12 ──────────────► ┐
  [Peer B] ── pieces 3, 8, 15 ──────────────► ┤
  [Peer C] ── pieces 2, 5, 11 ──────────────► ┼──► [You]
  [Peer D] ── pieces 4, 9, 14 ──────────────► ┤    assembles all pieces
  [Peer E] ── pieces 6, 10, 13 ─────────────► ┘    verifies each hash
                                                    reconstructs file

  Simultaneously you are uploading:

  [You] ── pieces 1, 3, 7 ───────────────────► [Peer F]
  [You] ── pieces 2, 8, 12 ──────────────────► [Peer G]
```

You are not a passive receiver. You are an active participant — downloading from many peers and uploading to others at the same time.

---

### Why This Model Is Powerful

**Self-scaling:** The more popular a file the more people have pieces. More sources means faster downloads for everyone. A file with 10,000 seeders downloads faster than a file with 10. The opposite of traditional servers where more users means slower downloads and higher costs.

**No single point of failure:** If any peer disconnects your client requests their pieces from another. If the tracker goes offline DHT and PEX keep the swarm alive. If the original publisher disappears entirely the file remains available as long as at least one seeder exists anywhere.

**Cryptographic integrity:** Every piece is SHA-1 verified. A corrupted or tampered piece is detected immediately and discarded. This is a stronger integrity guarantee than most centralised transfer protocols which rely on optional checksums.

**Zero publisher bandwidth cost:** Once seeded into the network the publisher needs no servers or bandwidth. The user community is the distribution infrastructure.

---

### Private Trackers

Public torrents use open trackers and DHT — anyone can join. Private tracker communities restrict access:

- DHT and PEX are disabled — peer discovery only via the private tracker server
- Access requires an account with invite-only registration
- Ratio requirements are enforced — members who only download and never seed are banned
- This creates a sustainable community of reliable seeders
- File availability is much higher than public torrents — content remains well-seeded for years

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
| File survives publisher disappearing | Yes — while seeders exist | No | No | No |
| Best for | Large public distribution | General web delivery | Secure transfer | Scalable app storage |

---

## 15. IPFS and Decentralised Storage

Content-addressed decentralised file storage. Files are addressed by what they are (their cryptographic hash) rather than where they are (a server URL). Any node that has the content can serve it.

---

### IPFS — InterPlanetary File System

**How it works:** When you add a file to IPFS it is split into blocks and each block is hashed. The top-level hash (CID — Content Identifier) uniquely identifies the file by its content. Any node in the IPFS network that has pinned the file can serve it. You request content by CID — the network finds whoever has it. If the content never changes, the CID never changes. If the file is modified the CID changes — this is how integrity is guaranteed by the address itself.

**Scenarios:**
- A blockchain application stores NFT assets on IPFS — the asset is not dependent on any single company's servers continuing to exist. The NFT contract stores the IPFS CID.
- A censorship-resistant publishing platform distributes content via IPFS — content cannot be taken down by targeting one server because there is no one server.
- A decentralised application (dApp) serves its frontend from IPFS — the interface is available as long as any node has it pinned.
- A research institution publishes a dataset to IPFS — the CID is the permanent citable reference. Anyone can verify the data has not changed because the hash must match.

**Filecoin:** A blockchain-based incentive layer on top of IPFS. Storage providers are paid in FIL cryptocurrency to store and serve content reliably. Provides economic guarantees for persistence — content stays available because providers are paid to keep it.

**Storj and Sia:** Alternative decentralised storage networks. Files are encrypted, split into pieces, and distributed across many independent storage nodes. No single node has the complete file. Access requires the encryption key and erasure coding to reassemble.

---

## 16. Local Wireless Transfer

Device-to-device file sharing over local WiFi or Bluetooth. No internet required. No central server. No accounts. The source and destination communicate directly.

**Tools:** Apple AirDrop, Android Nearby Share, Windows Nearby Sharing, Snapdrop (browser-based, WebRTC), LANDrop.

**How AirDrop works:** Sender and recipient discover each other via Bluetooth Low Energy. The actual file transfer happens over a direct peer-to-peer WiFi connection between the two devices — encrypted with TLS. Apple's servers are not involved in the transfer.

**How Snapdrop works:** Both devices open snapdrop.net in a browser on the same WiFi network. The browser uses WebRTC to establish a direct peer-to-peer connection. Files transfer directly between browsers — the Snapdrop server only facilitates the initial peer discovery handshake, not the file transfer itself.

**Scenarios:**
- A photographer at a shoot transfers RAW files from a MacBook to a colleague's iPad via AirDrop — fast, encrypted, no internet required.
- A team in a conference room shares a presentation file via Nearby Share — no email, no cable, no account needed.
- A cross-platform team where AirDrop and Nearby Share are incompatible uses Snapdrop — works on any device with a browser on the same WiFi.
- A field engineer transfers diagnostic reports from a tablet to a laptop with no internet connectivity — AirDrop or Snapdrop on the local network.

**Strengths:** Fastest transfer for devices in the same location. No infrastructure, no accounts, no internet dependency. Cross-platform via Snapdrop.

---

# All Scenarios — Complete Reference

---

## Scenario 1 — Enterprise Office File Sharing

**Context:** A company with 200 staff across two buildings needs shared access to documents organised by department.

**Primary:** SMB / Active Directory
**Supporting:** RSync (backup), SFTP (admin access)

IT sets up a Windows File Server. Department shares are created — Finance, HR, Engineering. AD groups control access. Staff map `\\fileserver\HR` as a drive letter. Files are central — no emailing documents back and forth. RSync runs nightly to a backup server. IT manages the server via SFTP or RDP.

---

## Scenario 2 — Remote and Distributed Teams

**Context:** Staff in multiple countries need shared file access without a central office network.

**Primary:** Nextcloud over WebDAV and HTTPS, Cloud sync client
**Supporting:** VPN plus NFS or SMB for regional offices, SFTP for admin

A self-hosted Nextcloud instance runs on a VPS with MinIO as its backend. Staff sync via the desktop client. Large files are accessed via WebDAV mount without full local sync. Regional office staff connect via VPN and mount NFS or SMB directly for low-latency access. External collaborators get time-limited HTTPS share links.

---

## Scenario 3 — Software Development and CI/CD

**Context:** A dev team builds, tests, deploys, and manages code across multiple servers.

**Primary:** Git, Object Storage, RSync
**Supporting:** SFTP, NFS, SCP, Git LFS, DVC

Code lives in Git. CI/CD builds artifacts and pushes them to object storage. Deployment pulls artifacts via S3 API. Configuration is distributed via RSync. Application nodes share a common NFS config mount. Logs ship to object storage via a log agent. Developers pull specific files via SFTP for debugging. Large binary assets use Git LFS. Datasets use DVC with object storage backend.

---

## Scenario 4 — Multi-Server Application Infrastructure

**Context:** Ten application servers behind a load balancer need access to the same files.

**Primary:** NFS, Object Storage
**Supporting:** RSync (backup), SFTP (admin)

NFS exports uploads, config, and shared libraries. All app servers mount at boot. Object storage holds durable permanent files. RSync backs up NFS exports hourly. New servers mount NFS on first boot and are immediately current.

---

## Scenario 5 — Web Application File Upload

**Context:** Users upload files via a browser. Files are stored, processed, and retrieved.

**Primary:** HTTPS upload, S3 presigned URLs, Object Storage, CDN
**Supporting:** NFS scratch volume, Processing queue, SFTP (ops)

Small files POST to the app server over HTTPS. Large files use presigned PUT — browser uploads directly to object storage. App records the object key. Processing workers virus scan, resize, and convert — using NFS scratch for intermediate files. Delivery is via presigned GET URL or CDN. Ops team accesses files via SFTP for bulk operations.

---

## Scenario 6 — Fintech and Banking File Exchange

**Context:** Automated payment file exchange with dozens of partner banks and financial institutions.

**Primary:** SFTP with SSH key auth, AS2, MFT Platform
**Supporting:** FTPS (legacy partners), Object Storage (archive), Compliance portal

Each partner has a dedicated SFTP drop folder with SSH key auth. New files trigger a processing pipeline. Acknowledgement files are written back. Legacy partners use FTPS. EDI partners use AS2 with signed delivery receipts. An MFT platform manages all partner connections, scheduling, retry, alerting, and audit. All files are archived to object storage with seven-year retention. Compliance team accesses archives via SFTP or internal portal.

---

## Scenario 7 — Media Platform

**Context:** Creators upload videos. Content is processed and delivered globally to millions.

**Primary:** S3 presigned PUT, Object Storage, CDN
**Supporting:** NFS scratch (transcoding), Processing queue, SFTP (ops)

Creator uploads via presigned PUT directly to object storage. Event triggers transcoding worker. Worker uses NFS scratch for intermediate files. Multiple resolution outputs written back to object storage. CDN delivers to viewers globally. First viewer in each region hits origin. All subsequent viewers in that region hit the CDN edge cache.

---

## Scenario 8 — Healthcare Records

**Context:** Patient records, scan images, and lab results. Strictly access-controlled and audited.

**Primary:** HTTPS portal, Object Storage with encryption, MFT Platform
**Supporting:** SMB (admin staff), SFTP (lab intake), Archive tier

Clinical staff upload via HTTPS portal. Object storage with strict bucket policies — no public access. All access logged. DICOM scans served via HTTPS to specialist viewers. Admin staff access non-clinical documents via SMB with role-based permissions. External labs deliver results via SFTP. MFT platform governs all external exchanges. Lifecycle policy moves files to archive tier automatically.

---

## Scenario 9 — Backup and Disaster Recovery

**Context:** Reliable automated backups with fast restore capability and geographic redundancy.

**Primary:** RSync over SSH, Object Storage
**Supporting:** SFTP (manual retrieval), GPG encryption, Cross-region replication

RSync backs up changed server files nightly — delta only, bandwidth efficient. Database dumps are compressed, GPG-encrypted, and pushed to object storage. Versioning retains 30 days. Lifecycle policy moves to archive at 90 days. Cross-region replication provides geographic redundancy. Monthly restore tests verify integrity. NFS and SMB volumes are snapshotted and pushed to object storage.

---

## Scenario 10 — Scientific and Research Computing

**Context:** Large computational jobs across a cluster reading and writing large shared datasets.

**Primary:** NFS (cluster storage), Object Storage (archive)
**Supporting:** SFTP, RSync, Globus, DVC

High-performance NFS serves all compute nodes. Jobs read and write directly without copying datasets. Researchers pull results via SFTP or RSync. Processed datasets archive to object storage. Inter-institution transfers via Globus or SFTP. DVC versions datasets alongside the code that processes them — reproducible science.

---

## Scenario 11 — Content and Software Distribution

**Context:** Distributing large files — software installers, game patches, media — to a global audience.

**Primary:** Object Storage, CDN, BitTorrent
**Supporting:** SFTP (editorial intake)

CMS uploads go to object storage. CDN serves all end users from edge cache. For the heaviest files — multi-gigabyte game patches, large installers — BitTorrent distributes peer to peer. The torrent file itself is a small CDN download. The actual data is distributed by the user community. Publisher bandwidth cost drops to near zero for the largest files. Editorial staff in remote locations submit large media via SFTP to an intake server.

---

## Scenario 12 — IoT and Edge Devices

**Context:** Thousands of sensors and cameras push data files to a central platform.

**Primary:** SFTP or HTTPS (device push), Object Storage
**Supporting:** Presigned URLs (operator retrieval), HTTPS (firmware distribution)

Each device runs an agent that pushes files on completion. Files land in object storage tagged with device ID, timestamp, and location. Analytics pipeline processes new files in near real time. Operators retrieve specific files via presigned URLs from a dashboard. Firmware updates are distributed back to devices via HTTPS from object storage.

---

## Scenario 13 — Peer to Peer Large-Scale Distribution

**Context:** Distributing a large file to a massive public audience with no central bandwidth cost.

**Primary:** BitTorrent
**Supporting:** HTTPS (torrent file distribution), DHT (decentralised peer discovery)

Publisher creates a torrent. Torrent file distributed via HTTPS. Users download torrent and open in client. Client contacts tracker or queries DHT for peers. Pieces downloaded from many peers simultaneously. Each piece SHA-1 verified. User immediately seeds pieces to other leechers while still downloading. When complete user becomes a full seeder. The larger the audience the faster it gets for everyone.

---

## Scenario 14 — Censorship-Resistant and Decentralised Distribution

**Context:** Content that must remain available regardless of server takedowns or political interference.

**Primary:** IPFS
**Supporting:** Filecoin (paid persistence), HTTPS gateway (browser access)

Content is added to IPFS and addressed by CID. Multiple nodes pin the content. Any node can serve any request. The original publisher can disappear and the content remains available from other nodes. A blockchain application stores the CID in a smart contract — the asset is permanently referenced without depending on any company's servers. Filecoin storage providers are paid to guarantee persistence.

---

## Scenario 15 — Email File Delivery

**Context:** Sending a specific file to a specific known recipient as part of a message.

**Primary:** SMTP / IMAP
**Supporting:** Object Storage link for files exceeding size limits

File Base64-encoded and embedded in MIME message. Sent via SMTP. Recipient retrieves via IMAP. For files exceeding 10 to 25MB the email contains a link to object storage or a cloud sync share instead. Automated systems — invoicing, payroll, bank statements — generate and attach PDFs programmatically.

---

## Scenario 16 — Team Chat File Sharing

**Context:** Quick operational file sharing in the flow of team communication.

**Primary:** Platform HTTPS (Slack, Teams, Telegram)
**Supporting:** SharePoint backend (Teams), Object Storage (platform backend)

Files dragged into chat are uploaded to platform storage via HTTPS. Teams files land in SharePoint. Telegram supports up to 2GB per file — used for community software distribution. WhatsApp compresses files — not suitable for professional quality requirements. Compliance note: chat files often fall outside corporate retention policies — shadow IT and audit risk.

---

## Scenario 17 — Version Controlled File Sharing

**Context:** Teams collaborating on files that change over time and need full history.

**Primary:** Git over SSH or HTTPS
**Supporting:** Git LFS (binary assets), DVC plus Object Storage (datasets)

All team members clone the repository — full copy of all files and history. Changes pushed and pulled. Every change attributed to a person with timestamp. Branching enables parallel work. Merge handles conflicts. Git LFS keeps large binaries out of the repository — pointers in Git, bytes on LFS server. DVC tracks dataset versions — code and data pinned together for reproducibility.

---

## Scenario 18 — Database File Store

**Context:** Small application storing files directly in the database for simplicity.

**Primary:** PostgreSQL BLOB or MongoDB GridFS
**Supporting:** Migration path to Object Storage

Small files stored as bytea in PostgreSQL alongside metadata — no separate storage infrastructure. GridFS chunks large files into 255KB documents for MongoDB storage beyond the 16MB limit. Works well at small scale. Modernisation path: extract BLOBs to object storage, store only the key in the database, serve via presigned URL — the standard upgrade once the application scales.

---

## Scenario 19 — Physical Media Transfer

**Context:** Air-gapped environment, massive data volume, forensic work, or long-term cold archive.

**Primary:** Encrypted USB, LTO Tape, Cloud Transfer Appliance
**Supporting:** Hardware write-blocker (forensic), Climate-controlled storage (tape)

Air-gapped network — encrypted USB is the only channel. 500TB migration — cloud provider transfer appliance shipped, loaded locally, shipped back, uploaded directly. Long-term archive — LTO-9 tape at 18TB native per cartridge, cheapest per-GB storage available. Forensic imaging — hardware write-blocker preserves original integrity, full image copied to external SSD.

---

## Scenario 20 — Local Wireless Transfer

**Context:** Two devices in the same location need to transfer files instantly.

**Primary:** AirDrop, Nearby Share, Snapdrop
**Supporting:** WebRTC (Snapdrop peer connection)

AirDrop for Apple-to-Apple — Bluetooth discovery, direct WiFi transfer, TLS encrypted, no internet. Nearby Share for Android-to-Android or Windows-to-Windows. Snapdrop for cross-platform on same WiFi — browser-based WebRTC peer-to-peer, no installation, no account, no internet required.

---

## Scenario 21 — Enterprise Multi-Partner File Exchange

**Context:** A large enterprise managing automated file exchanges with dozens of external partners each using different protocols.

**Primary:** MFT Platform (GoAnywhere, IBM Sterling, MOVEit)
**Supporting:** SFTP, FTPS, AS2, FTP (legacy)

Each partner connection configured in the MFT platform — protocol, credentials, schedule, paths, retry policy, alerting. Platform executes all transfers automatically. Every file logged with timestamp and checksum. Failures trigger alerts and automatic retry. Compliance dashboard shows complete audit trail across all partners. New partner onboarded in hours — not weeks of custom integration work.

---

## Scenario 22 — Microservice File Pipeline

**Context:** Multiple microservices need to pass files through a processing pipeline without tight coupling.

**Primary:** Object Storage as universal handoff, Message Queue for coordination
**Supporting:** S3 API, Presigned URLs, HTTPS

No service passes file bytes directly over API calls. Each service writes output to object storage and publishes the object key to a queue. The next service reads the key, pulls the file independently, processes it, writes output to object storage under a new key, and publishes forward. Services are completely decoupled — each scales independently. A failure in one worker does not lose the file. Jobs are retryable at any stage.

---

## The Universal Three-Layer Pattern

Every file sharing scenario is a specific combination of three layers:

```
┌──────────────────────────────────────────────────────────────┐
│                      INTAKE LAYER                            │
│  How files enter the system                                  │
│                                                              │
│  HTTPS upload · SFTP drop · Email attachment                 │
│  SMB write · NFS write · Device push (IoT)                   │
│  Git push · Physical media · AirDrop · Nearby Share          │
│  MFT scheduled pull · API POST · BitTorrent seed             │
│  Browser presigned PUT · Messaging platform upload           │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                     STORAGE LAYER                            │
│  Where files live                                            │
│                                                              │
│  Object Storage · NFS export · SMB share                     │
│  Local disk · Database BLOB · Git repository                 │
│  LTO tape · Cloud sync platform · MFT staging area           │
│  IPFS network · BitTorrent swarm · Physical media            │
└──────────────────────┬───────────────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────────────┐
│                    DELIVERY LAYER                            │
│  How files reach consumers                                   │
│                                                              │
│  CDN edge (HTTPS) · Presigned GET URL · SMB mount            │
│  NFS mount · SFTP pull · RSync pull · WebDAV mount           │
│  Email attachment · Chat platform link · AirDrop             │
│  Physical media · API response · BitTorrent download         │
│  IPFS gateway · Globus transfer · Git clone / pull           │
└──────────────────────────────────────────────────────────────┘
```

---

## Complete Master Reference

| Scenario | Primary | Supporting | Model |
|---|---|---|---|
| Office shared drives | SMB | RSync, SFTP, AD | Centralised |
| Remote and distributed teams | Nextcloud, WebDAV | VPN+NFS/SMB, HTTPS links | Centralised |
| Dev infrastructure and CI/CD | Git, Object Storage | RSync, NFS, SFTP, Git LFS, DVC | Centralised |
| Multi-server application | NFS, Object Storage | RSync, SFTP | Centralised |
| Web app file upload | HTTPS, Object Storage, CDN | NFS scratch, Queue, Presigned URLs | Centralised |
| Fintech partner exchange | SFTP, AS2, MFT | FTPS, Object Storage, Archive | Centralised |
| Media and video platform | Object Storage, CDN | Presigned URLs, NFS scratch | Centralised |
| Healthcare records | HTTPS, Object Storage, MFT | SMB, SFTP, Archive tier | Centralised |
| Backup and disaster recovery | RSync, Object Storage | SFTP, GPG, Replication | Centralised |
| Research and HPC | NFS, Object Storage | SFTP, RSync, Globus, DVC | Centralised |
| Content and software delivery | Object Storage, CDN | SFTP, BitTorrent | Centralised + Distributed |
| IoT data collection | SFTP, HTTPS | Object Storage, Presigned URLs | Centralised |
| Peer to peer large distribution | BitTorrent | HTTPS, DHT, PEX | Distributed |
| Censorship-resistant distribution | IPFS, Filecoin | HTTPS gateway | Distributed |
| Email file delivery | SMTP/IMAP | Object Storage link | Centralised |
| Team chat file sharing | Platform HTTPS | SharePoint, Shadow IT awareness | Centralised |
| Version controlled files | Git, Git LFS, DVC | SSH, HTTPS, Object Storage | Centralised |
| Database file store | BLOB, GridFS | Object Storage migration path | Centralised |
| Physical and air-gapped | USB, LTO tape, Appliance | Write-blocker, Encryption | Centralised (physical) |
| Local wireless transfer | AirDrop, Nearby Share, Snapdrop | WebRTC | Distributed (local) |
| Enterprise multi-partner MFT | MFT Platform | SFTP, FTPS, AS2, FTP | Centralised |
| Microservice file pipeline | Object Storage + Queue | S3 API, Presigned URLs | Centralised |

---

## Choosing the Right Mechanism

**Browser or end user over the internet**
→ HTTPS upload, presigned URL, CDN, cloud sync platform

**Automated machine-to-machine between known systems**
→ SFTP (internet-facing), RSync (server sync), AS2 (B2B with receipts), MFT (multi-partner governed)

**Applications treating remote storage as local disk**
→ NFS (Linux / data centre), SMB (Windows / mixed office), WebDAV (HTTP-based mount)

**Durable scalable storage for applications**
→ Object storage — hot tier for active files, archive tier for compliance retention

**Collaborative file working with full history**
→ Git (code and config), Cloud sync platform (documents), DVC (datasets)

**Massive public distribution with no central bandwidth cost**
→ BitTorrent — scales with demand, publisher cost near zero

**Censorship-resistant or content-addressed permanent storage**
→ IPFS — content addressed by hash, survives any single node disappearing

**No network or impractical data volume for network transfer**
→ Physical media — USB for air-gapped, LTO tape for cold archive, transfer appliance for massive migration

**Governed multi-partner enterprise exchange with compliance requirements**
→ MFT platform over SFTP, FTPS, and AS2

**Two devices in the same room**
→ AirDrop, Nearby Share, or Snapdrop — no internet, no accounts, instant

**Quick operational sharing inside team communication**
→ Slack or Teams file sharing — fast and convenient, but understand retention and compliance limitations
