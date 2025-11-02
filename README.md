# 🐋 Iron Orca — Project Snapshot (v1.0, November 2025)

## Concept
Iron Orca is a modern reimagining of the Solaris-era **Orca** and **SE Toolkit**, designed to collect high-resolution host metrics locally, shape them into structured data, and feed them into a scalable backend for fleet-wide observability and analysis.

## Motivation
SNMP and polling-based systems miss short-lived anomalies and produce fragmented data. Iron Orca replaces that with a **push-based, context-rich model**, sampling its metrics using native OS tools on the host being monitored rather than polling that data at intervals from a remote monitoring system.

---

## Core Architecture

### Sardine (Agent)
A lightweight intermediary using `sar` (sysstat) as its data source.
- Emits **JSON-formatted vitals** based on the **USE Method** (Utilization, Saturation, Errors).
- Handles batching, tagging, and backpressure.
- Optionally reports local health state (OK/WARN/CRIT).

### Iron Orca Backend
- Ingests Sardine’s structured vitals into **M3DB**, Uber’s open-source, horizontally scalable time-series store.
- Provides a unified “fleet memory” instead of thousands of isolated RRDs.
- Offers **CLI**, **API**, and **Web UI** interfaces for querying and visualization.
- Integrates with **Jupyter** or **R** for exploratory analysis.

### Nagios Integration (Optional)
- Sardine can emit passive checks with CRIT/WARN/OK and diagnostic text.
- Leverages Nagios’s mature **PagerDuty** and **notification** pipeline.
- PNP4Nagios remains usable for quick trending graphs.

### RRD Compatibility and Migration
- Optional RRD-style perfdata output.
- Planned importer to consolidate legacy `.rrd` files into M3DB for unified analysis.

---

## Phased Plan (Summary)

1. **Phase 1:** Proof of concept — Sardine + `sar` + M3 + simple CLI/API.  
2. **Phase 2:** Fleet view, comparison, and web UI.  
3. **Phase 3:** Node-level health logic and Nagios passive alerts.  
4. **Phase 4:** RRD compatibility + migration of historical data.  
5. **Phase 5:** Optional local buffers, plugins for “pet” systems, and self-aware logic.

---

## Philosophy
Give every node just enough self-awareness to describe its health, collect only the most meaningful vitals, and centralize that knowledge in one powerful, open-source system.  
Iron Orca aims to be **industrial yet humane** — technical depth balanced with operational pragmatism.

**Mascot:** 🐋 *Keiko* — the “Iron Orca,” symbolizing freedom, intelligence, and industrial grace.
![Keiko the Iron Orca](iron-orca.png)
