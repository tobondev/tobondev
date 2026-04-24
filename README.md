# Hi. I'm Marcos.

I've been running Linux since before I had a reason to.
What started as teenage curiosity — hardware forums, IRC, breaking things to see what happened —
became a 12-year foundation that I've spent the last year turning into something documentable.

That's the honest version of my background.
The rest is below.

---

## What I'm Building
The `homelab` repository is a living record of Architectural Decision Records that track what I thought I knew, what I actually found out by breaking things in production, and how I engineered the solution.
It's modeled on enterprise principles not because I'm simulating a job, but because the discipline of treating it
like production is the point. Things break. I document why. I fix them. I document that too.

The architecture spans:

- **Network:** OPNsense edge routing, VLAN segmentation across 20+ endpoints, B.A.T.M.A.N. Advanced L2 mesh decoupled from L3, Suricata IDS/IPS, Cloudflare Zero-Trust tunnels with no inbound port exposure
- **Storage & Security:** LUKS full-disk encryption across all bare-metal systems, BTRFS with snapshot management via btrbk, automated 3-2-1 backup pipeline to AWS Glacier
- **Automation:** Ansible-driven provisioning and security hardening across all network nodes, SOPS + age encryption for secrets management in version control
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
| Current-state architecture overview | [`docs/architecture/CURRENT-STATE.md`](https://github.com/tobondev/homelab/blob/main/docs/architecture/CURRENT-STATE.md) |
| Runbooks & operational procedures | [`docs/runbooks/`](https://github.com/tobondev/homelab/tree/main/docs/runbooks) |

---

## Currently Active

- **LGAP Observability Stack** — deployed Loki, Grafana, Alloy, and Prometheus across all infrastructure services, VMs, and bare-metal hosts; integrated with Suricata IDS. Pending Wazuh deployment and Integration.
- **Active Directory / Entra ID** — mixed-OS domain integration (Arch Linux + RHEL + Windows), including hybrid Azure AD enrollment scenarios
- **Wazuh XDR** — network-wide endpoint detection and response, integrating with OPNsense and LGAP Stack for unified security visibility

---

## How I Think About This Work

Infrastructure is full of things people know the answer to without understanding why it works. 
And sometimes, when you dig into why it works, you realize the answer you had was incomplete.

That tension — between knowing and understanding — is what most of my documentation is actually about.
The ADRs aren't just records of decisions. They're records of what I thought I knew, what I found out,
and what I'd do differently next time.

If that's a useful way to think about systems, the repo is public.
If you want to talk about it: [tobon.dev](https://tobon.dev) · [LinkedIn](https://tobon.dev/linkedin) · [marcostobon@proton.me](mailto:marcostobon@proton.me)

---

Linux Systems Administrator · *CompTIA Security+ · Brooklyn, NY · He/They*
