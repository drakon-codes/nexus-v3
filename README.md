# Multi-Source Investigative Analytics Platform (NEXUS-INTEL)
## Complete User & Developer Technical Manual Guide

Welcome to the **Multi-Source Investigative Analytics Platform Suite**. This workspace contains three isolated, enterprise-grade investigative platforms built to unify fragmented digital evidence (**CDR**, **IPDR**, **Bank Statements**, and **Social Media OSINT**).

---

## 🏛️ Platform Portfolio & Active Ports

| Platform Version | Directory Path | Active Local URL | Core Focus & Architecture |
| :--- | :--- | :--- | :--- |
| **NEXUS-INTEL v1** | [`c:\chandigarah\`](file:///c:/chandigarah/) | `http://localhost:8080` | **Tactical Command Center**: Multi-modal glassmorphic visual interface, Cytoscape link graph, Leaflet GIS tower map, and automated anomaly cards. |
| **Correlation Engine v2** | [`c:\chandigarah\correlation_app\`](file:///c:/chandigarah/correlation_app/) | `http://localhost:8081` | **Multi-Hop Link Engine**: Data normalization pipeline, exact & fuzzy entity resolution, 2-hop Cypher graph expansion, and court draft exporter. |
| **NEXUS-INTEL v3** | [`c:\chandigarah\nexus_v3_platform\`](file:///c:/chandigarah/nexus_v3_platform/) | `http://localhost:8082` | **Three-Engine Architecture**: Strict 10-step investigation scenario, Connection Engine, Reconstruction Engine, Intelligence Engine, confidence scoring, and SHA-256 provenance logging. |

---

## 📂 Detailed File-by-File Manual Guide

### 1. NEXUS-INTEL v3 Platform (`c:\chandigarah\nexus_v3_platform\`)

#### `index.html`
* **Purpose**: The master UI interface for NEXUS-INTEL v3.
* **How It Works**: Houses the top navbar with Universal Search, live operational stats strip (Record counts, Discovered entities, Graph relationships, Active alert flags), sidebar tab navigation, and 6 workspace panes:
  1. **Data Ingestion Pane**: Interactive drag-and-drop upload cards for CDR.csv, IPDR.csv, Bank.csv, and Social.json.
  2. **Connection Engine Pane**: Cytoscape link graph canvas with side entity inspector.
  3. **Reconstruction Engine Pane**: Multi-track chronological event stream.
  4. **Cell Tower Map Pane**: Leaflet GIS spatial map.
  5. **Intelligence Engine Pane**: Anomaly radar threat cards.
  6. **Case Report Pane**: Evidentiary case report compiler.

#### `css/nexus_v3.css`
* **Purpose**: The tactical cyber dark-mode design system.
* **How It Works**: Defines HSL color tokens (`--accent-cyan`, `--accent-emerald`, `--accent-purple`, `--accent-red`), glassmorphism backdrop blur filters, responsive CSS grid layouts, pulse animation dots, and status badges.

#### `js/synthetic_generator.js`
* **Purpose**: Generates realistic multi-source datasets with baked-in investigation scenarios and background noise.
* **How It Works**:
  * Configures **Case #INV-2026-001 (Operation NEXUS)**.
  * Primary Target: `Rahul Kumar` (Phone: `9876543210`, Account: `ACC-001`, Social: `@rahul123`).
  * Stores 39,863 raw log counters, 1,842 discovered entities, 5,921 relationships, raw timestamped events, Neo4j graph nodes/edges, and 3 rule-based anomaly alerts.

#### `js/normalizer.js` (`CommonEventNormalizer`)
* **Purpose**: Adapts messy raw formats from different sources into a unified Common Event Schema.
* **How It Works**:
  * `normalizeCDR()`: Maps telecom `msisdn`, `caller`, `callee`, and `imei` to canonical event objects.
  * `normalizeIPDR()`: Maps subscriber pings, public/private IPs, ports, and app bytes.
  * `normalizeBanking()`: Maps account numbers, UPI VPAs, transaction amounts, and KYC names.
  * `normalizeSocial()`: Maps social handles, post snippets, platform tags, and IP logs.

#### `js/entity_resolution.js` (`EntityResolutionV3`)
* **Purpose**: Resolves disparate identifiers into single person entities and assigns confidence scores.
* **How It Works**:
  * Implements confidence scoring rules:
    * **1.00 (100%)**: Direct match on KYC name, phone number, or account number.
    * **0.85 (85%)**: Strong correlation (same IP session within 5-minute window).
    * **0.70 (70%)**: Spatial-temporal correlation (co-located at cell tower during transaction).
    * **0.40 (40%)**: Weak inference (secondary social contact).
  * `resolveEntityNetwork(query)`: Takes any search input (e.g., `9876543210`) and resolves all linked hardware, bank accounts, and IPs.

#### `js/connection_engine.js` (Engine 1)
* **Purpose**: Manages graph visualization and multi-hop network expansion.
* **How It Works**:
  * `initConnectionEngine()`: Renders Cytoscape.js force-directed layout (`cose`) with distinct node icons (Person: Hexagon/Red, Phone: Ellipse/Blue, Account: Rectangle/Green, Social: Rounded/Purple, IP: Diamond/Cyan, Device: Vee/Rose, Tower: Pentagon/Amber).
  * `inspectV3Node()`: Populates the right-side inspector panel with entity metadata and confidence badges.
  * `expand2HopGraph(nodeId)`: Dims all unrelated nodes beyond 2 hops from the selected node to isolate suspect networks.

#### `js/reconstruction_engine.js` (Engine 2)
* **Purpose**: Reconstructs chronological event streams across all 4 data domains.
* **How It Works**:
  * `renderReconstructionTimeline()`: Sorts normalized events by timestamp and renders a multi-track stream showing the exact sequence of events (Call ➔ IP session ➔ Bank transfer ➔ Social post ➔ Layering transfer).

#### `js/spatial_map.js`
* **Purpose**: Renders spatial cell tower coordinates and location pings.
* **How It Works**:
  * `initV3SpatialMap()`: Initializes Leaflet GIS map with dark tiles (CartoDB Dark Matter), rendering cell tower location markers and 400m coverage radii.

#### `js/intelligence_engine.js` (Engine 3)
* **Purpose**: Evaluates rule-based anomaly detection cards.
* **How It Works**:
  * `renderIntelligenceAnomalies()`: Renders risk cards for:
    1. **Rule 1 (Rapid Fund Layering - 98% Risk)**: Micro-transfers executed within 8 minutes.
    2. **Rule 2 (Cross-Source Temporal Correlation Spike - 91% Risk)**: Call + IPDR + Bank Transfer + Social post in a 15-minute window.
    3. **Rule 3 (SIM Swap & Shared Hardware Device - 88% Risk)**: Multiple SIMs inserted into one IMEI.

#### `js/app_v3.js`
* **Purpose**: Master application controller, Universal Search engine, and report exporter.
* **How It Works**:
  * `executeUniversalSearch(query)`: Searches phone numbers, accounts, or handles, resolves the target, and automatically navigates to the Connection Engine tab to highlight the suspect.
  * `renderEvidentiaryReport()`: Compiles case background, 2-hop network summary, timeline, anomaly alerts, and SHA-256 data provenance hashes into a printable case report.
  * `exportV3ReportPDF()`: Triggers native print/PDF export.

---

### 2. Standalone Correlation Engine v2 (`c:\chandigarah\correlation_app\`)

* **`index.html`**: Host page for Correlation Engine v2 on port 8081.
* **`css/correlation.css`**: Cyan-themed tactical stylesheet.
* **`js/synthetic_data.js`**: Case #2026-ALPHA dataset (Target: `Vijay Merchant`).
* **`js/schema_normalizer.js`**: `EntityResolutionEngine` class executing exact matching and record parsing.
* **`js/graph_engine.js`**: Cytoscape graph visualizer with `run2HopExpansion()` function.
* **`js/spatial_map.js`**: Leaflet GIS map plotting Bangalore cell towers (Indiranagar / MG Road).
* **`js/timeline_engine.js`**: Chronological event sorter.
* **`js/anomaly_rules.js`**: Threat rules renderer.
* **`js/correlation_app.js`**: Tab manager and evidentiary report compiler.

---

### 3. Tactical Command Center v1 (`c:\chandigarah\`)

* **`index.html`**: Command Center Dashboard on port 8080.
* **`css/styles.css`**: Tactical dark-mode theme stylesheet.
* **`js/data.js`**: Mock dataset for Case #2026-NEXUS (`Vikram Sharma`) and Case #2026-TITAN (`Karan Johar`).
* **`js/graph.js`**: Cytoscape link analysis visualizer with domain filters (Telecom, Banking, Social OSINT).
* **`js/map.js`**: Spatial GIS map with animated **Trajectory Playback** and co-location alert circles.
* **`js/timeline.js`**: Fused multi-domain timeline stream.
* **`js/analytics.js`**: Anomaly radar cards (Smurfing, SIM Swap, TOR exit pings).
* **`js/app.js`**: Case loader, tab navigator, and PDF exporter.

---

## ⚡ How to Run & Test the Platforms

You can run any or all of the three platforms concurrently using Python's built-in HTTP server:

### Run NEXUS v1 (Port 8080):
```bash
cd c:\chandigarah
python -m http.server 8080
```
*Access in browser:* `http://localhost:8080`

### Run Correlation Engine v2 (Port 8081):
```bash
cd c:\chandigarah\correlation_app
python -m http.server 8081
```
*Access in browser:* `http://localhost:8081`

### Run NEXUS-INTEL v3 (Port 8082):
```bash
cd c:\chandigarah\nexus_v3_platform
python -m http.server 8082
```
*Access in browser:* `http://localhost:8082`

---

## 🎯 10-Step Interactive Demo Walkthrough (Port 8082)

To demonstrate the platform in under 3 minutes:

1. Open `http://localhost:8082`.
2. View **Data Ingestion** counters (39,863 records ingested).
3. Type `9876543210` in the top **Universal Search** box and press Enter.
4. The system resolves **Rahul Kumar (Person A)** and switches to the **Connection Engine Graph**.
5. Click **`Expand 2-Hop Network (Rahul)`** to reveal connected targets (Sanjay Mehta & Vikram Merchant Shell Corp).
6. Click any node to view entity metadata and confidence scores (100% Direct Match, 91% TOR IP Match, 78% Social Match).
7. Navigate to **`3. Reconstruction Engine`** tab to view the chronological sequence (Call ➔ TOR IP ➔ Bank Transfer ➔ Social Post ➔ Layering Transfer).
8. Navigate to **`5. Intelligence Engine`** to inspect the 3 automated risk flags.
9. Navigate to **`6. Case Report`** and click **`Export Case Report (PDF)`** to generate the final court-ready intelligence document.
