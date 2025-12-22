# M3 Framework: Tooling Matrix

This matrix maps the **Mount-Monitor-Manage** phases to specific, pragmatic tools suitable for SMBs and Fractional Leadership. The focus is on "Low Friction" deployment—tools that provide immediate value without weeks of configuration.

> **Disclaimer:** This list is maintained by the community. "Primary Recommendation" indicates tools that best fit the *M3 philosophy* (easy to deploy, cost-effective for SMBs).

---

## 🏗 Phase 1: MOUNT (Visibility & Control Plane)

**Goal:** Establish immediate visibility into user actions and Shadow AI without complex network re-architecture.

| Category | Primary Tool | Alternatives | Function in M3 | Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Browser Security (DLP)** | **Sinaptic.AI** | LayerX, Island.io | The core sensor. Injects into the browser to detect PII paste events, block malicious extensions, and map SaaS usage. | 🟢 Low (Plugin) |
| **DNS / Network Filter** | **Cloudflare Gateway** | NextDNS, Cisco Umbrella | Blocks malware domains and creates a "log" of all visited sites (Shadow IT discovery) at the network level. Free for <50 users. | 🟢 Low (DNS change) |
| **Endpoint Agent (EDR)** | **MS Defender for Business** | SentinelOne, CrowdStrike | Standard antivirus + behavioral monitoring. Usually pre-included in M365 Business Premium. | 🟡 Med (Policy config) |
| **Identity / SSO** | **Google Workspace / M365** | Okta, JumpCloud | The single source of truth for "Who is logging in?". Used to enforce MFA. | 🟡 Med |

---

## 🔍 Phase 2: MONITOR (Detection & Logging)

**Goal:** Collect evidence of risks (Shadow AI, Leaks, Slop) to satisfy "Due Diligence" (GDPR/AI Act).

| Category | Primary Tool | Alternatives | Function in M3 | Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Log Aggregation (SIEM)** | **Graylog** (Open Source) | Wazuh, Elastic Stack | Centralizes logs from Sinaptic, Cloudflare, and Defender. Provides a searchable history of "Who did what". | 🔴 High (Requires server) |
| **SaaS Discovery** | **Sinaptic / LayerX** | Torii, BetterCloud | Automatically builds a list of all AI tools used by employees (e.g., "User A uses ChatGPT, User B uses Jasper"). | 🟢 Low (Auto-generated) |
| **AI Quality Monitor** | **Custom Prompts** | LangSmith, Helicone | *Advanced:* If building internal AI apps, these tools log the "quality" of AI responses to detect "AI Slop". | 🟡 Med |

---

## 🛡 Phase 3: MANAGE (Protection & Policy)

**Goal:** Enforce rules automatically based on data collected in the Monitor phase.

| Category | Primary Tool | Alternatives | Function in M3 | Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Device Management (MDM)**| **Microsoft Intune** | Jamf (Mac), Kandji | "Locking the door". Enforces encryption (BitLocker), remote wipe, and OS updates. | 🔴 High (Initial setup) |
| **Data Masking (Sanitization)**| **Sinaptic.AI** | PrivateAI | Automatically replaces emails/credit cards with `[REDACTED]` before sending data to ChatGPT. | 🟢 Low (Policy toggle) |
| **Access Policy** | **Cloudflare Access** | Twingate, Tailscale | Replaces VPN. Allows access to internal admin panels only from managed devices (Zero Trust). | 🟡 Med |

---

## 💡 Typical SMB "Starter Pack"

For a company of 10-50 people, we recommend this stack to achieve M3 Compliance in <48 hours:

1.  **Browser:** Sinaptic.AI (Visibility into AI usage & DLP)
2.  **Network:** Cloudflare Zero Trust (Free tier - DNS filtering)
3.  **Endpoint:** Microsoft Defender (Built-in)
4.  **Logs:** Native dashboards of the tools above (No complex SIEM initially).

---

### How to propose a tool?
To add a tool to this matrix, please submit a Pull Request. The tool must be:
1.  **Accessible:** Has a free trial or transparent pricing.
2.  **Deployable:** Can be set up in <1 day.
3.  **Relevant:** Solves a specific M3 phase problem.