# Synaptic Data

Personal data-engineering operation. I build and run small, sharp systems
end to end: data pipelines, web apps, crawlers, defensive infrastructure —
from a dev machine, through a local virtualized testbed, to production on
a cloud VPS. Everything below is deployed and serving, not a demo.

The code lives in private repositories. This profile describes what the
systems do and how they're built.

## Flagship: MTGScout

Collection management for *Magic: The Gathering*, backed by a real data
pipeline — live at [mtgscout.synapticdata.ca](https://mtgscout.synapticdata.ca).

- **Data pipeline**: daily ingestion of the MTGJSON dataset (full card
  catalog plus a ~28M-row price history) with staged diffing, envelope
  gates, and fingerprint-verified parity from dev machine to every target.
- **Web app**: Django — searchable catalog, collection tracking, Commander
  precons, price analytics, and a news desk with sourced provenance.
- **Telemetry**: an event-driven Ops panel (no daemons) tracks every job,
  incident, and deployment with its own state machines.
- **Media**: a ~240k-object image library served from object storage.

## Supporting systems

| Project | What it is |
|---|---|
| **Recon** | Standalone, dependency-free web crawler. Topic skills (the MTG news desk is one) emit signed, provenance-stamped artifacts over an HMAC peer contract. |
| **Mars** | Bot mitigation defending the production edge. |
| **Contact Relay** | Hardened contact-form backend (spam traps, CAPTCHA verification, spooled delivery) serving the portfolio sites. |

## How things are built here

- **Local → testbed → prod.** Nothing reaches production without passing on a local virtualized staging environment first. The paths are kept as similar as possible so what works in staging works in prod.
- **Transfers, not reloads.** Database targets converge through pre-computed diffs with replay protection and parity checks — never full table reloads.
- **Gates over hope.** Every pipeline stage and deployment has pre-flight checks that fail closed; monitoring trips on unexpected states (unknown accounts, unconverged targets, stale backups).
- **Boring technology, rigorously applied.** Django, MariaDB, Docker, Traefik, systemd, Ansible. Dependencies are added with a reason, not a mood.
- **History is append-only.** No rebases, no rewrites — the log tells the truth about how each system got here.

## Elsewhere

- 🌐 [synapticdata.ca](https://synapticdata.ca)
- 🃏 [mtgscout.synapticdata.ca](https://mtgscout.synapticdata.ca)
