# Hi. I'm Marcos.
 
I've been running Linux since before I had a reason to.
It started as teenage curiosity: support forums, IRC. Breaking things, then working out how to fix them.
Today, it's become the foundation of what is a formalized, documented and auditable Project Repository of my Infrastructure Engineering.

That's the honest version of my background.
The rest is below.

---

## What I'm Building
The `homelab` repository is a living record of Architectural Decision Records that track what I thought I knew, what I actually found out by breaking things in production, and how I engineered the solution.
It's modeled on enterprise principles not because I'm simulating a job, but because the discipline of treating it
like production is the point. Things break. I document why. I fix them. I document that too.

The architecture spans:

- **Network:** OPNsense edge routing, VLAN segmentation across 20+ endpoints, B.A.T.M.A.N. Advanced L2 mesh decoupled from L3, Suricata IDS/IPS, Cloudflare Zero-Trust tunnels with no inbound port exposure
- **Storage & Security:** LUKS full-disk encryption across all bare-metal systems. Three-tier, stateful backup architecture: local/remote BTRFS snapshots orchestrated natively via `systemd` and `btrbk`, and atomic delta-syncs to AWS Glacier Deep Archive using a custom `rclone` Last Known Good Backup (LKGB) pipeline.
- **Identity and Access Management:** VLAN-Segmented Active Directory Domain, featuring a Server Core Domain Controller, and a testbed for GPO and security hardening, with a 1000-user AD Domain.
- **Automation:** Ansible-driven provisioning and security hardening across all network nodes, with SOPS + age encryption enforcing secrets management across all configuration and deployment pipelines. PowerShell-based JSON schema for Active Directory Domain population.
- **Observability:** LGAP stack (Loki, Grafana, Alloy, Prometheus) for centralized log aggregation, alerting, and telemetry correlation
- **Pre-boot:** tinyssh for remote LUKS unlock during disaster recovery, with strictly separated key material from standard SSH access

Everything is version-controlled. Every architectural decision has a record. Every incident has a post-mortem.

---

## Where to Start in the Repo

The repository has a lot of files. Here's what's worth reading first depending on what you're looking for:

| Looking for | Start here |
|---|---|
| Incident response | [`docs/incidents/`](https://github.com/tobondev/homelab/tree/main/docs/incidents) |
| Architectural decision-making | [`docs/adrs/`](https://github.com/tobondev/homelab/tree/main/docs/adrs) |
| Deployment & change management | [`docs/operations/`](https://github.com/tobondev/homelab/tree/main/docs/operations) |
| Infrastructure Engineering & Automation | [`scripts/admin/backup/`](https://github.com/tobondev/homelab/tree/main/scripts/admin/backup) |
| Current-state architecture overview | [`docs/architecture/CURRENT-STATE.md`](https://github.com/tobondev/homelab/blob/main/docs/architecture/CURRENT-STATE.md) |
| Runbooks & operational procedures | [`docs/runbooks/`](https://github.com/tobondev/homelab/tree/main/docs/runbooks) |

---

## How I Write: The Documentation Pipeline

I ran into massive documentation friction early in the lifecycle of this repository. The context switch between executing complex terminal operations, troubleshooting live systems, and retroactively writing down what happened meant I was either moving too slow, or my notes were incomplete. The gap between "knowing what I did" and "proving what I did" was too wide.

To permanently solve this, I built `Journal Helper`. It is a custom Bash-based documentation pipeline that acts as a dynamic `IDE` for my entire infrastructure. When I start an operational task, the tool generates a markdown template, wraps my terminal in a tracked script session, and allows me to tag operational phases dynamically in real-time. When I finish the work and exit the shell, a robust `perl` and `col` parsing pipeline strips all ANSI escape sequences, box-drawing characters, and shell noise. It then directly injects the perfectly formatted, phase-separated transcript into the markdown file.

This is how I maintain operational discipline. It guarantees that every configuration change or incident response I publish is accompanied by exact, real-world terminal output, eliminating manual transcription entirely.

You can find the output of this work in `docs/incidents/` and `docs/operations`.

---

## Currently Active Projects

- **Hybrid Identity Cloud Bridge** — Synchronizing the on-premise AD domain with a Microsoft 365 Entra ID tenant to validate SSO, delta syncs, and conditional access paths.
- **Offensive Security & Telemetry Analysis** — Executing deliberate attack paths (Kerberoasting, Bloodhound, password spraying) against intentionally vulnerable AD service accounts to capture and analyze defensive telemetry via Grafana.
- **Cross-OS Domain Integration** — Enforcing centralized identity across operating systems by joining RHEL endpoints to the Windows domain via `realmd` and `sssd`.
- **Suricata IDS & Wazuh XDR** — Layered network and endpoint detection, integrating an OPNsense-based IDS with a network-wide Wazuh VM deployment, forwarding logs directly to the LGAP stack.

---

## How I Think About This Work

Infrastructure is full of things people know the answer to without understanding why it works. 
And sometimes, when you dig into why it works, you realize the answer you had was incomplete.

That tension — between knowing and understanding — is what most of my documentation is actually about.
The ADRs aren't just records of decisions. They're records of what I thought I knew, what I found out,
and what I'd do differently next time.

If that's a useful way to think about systems, the repo is public.
If you want to talk about it: [tobon.dev](https://tobon.dev) · [LinkedIn](https://tobon.dev/linkedin) · [marcos@tobon.dev](mailto:marcos@tobon.dev)

---

Linux Systems Administrator & Cybersecurity Professional · *CompTIA Security+ & Google Cybersecurity Certified · Brooklyn, NY · He/They*
