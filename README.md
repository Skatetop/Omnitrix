# 🔍 OSINT Agent Skills — MCP Server

> **Transform any autonomous AI agent into a senior OSINT analyst.**  
> A complete knowledge base with 23 MCP tools, intelligence methodologies, pivot playbooks, ethics frameworks, and structured reporting templates.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version: 1.4.1](https://img.shields.io/badge/Version-1.4.1-blue.svg)](CHANGELOG.md)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-brightgreen.svg)](https://modelcontextprotocol.io)
[![Node.js](https://img.shields.io/badge/Node.js-≥18-brightgreen.svg)]()

---

## Table of Contents

- [What This Is](#what-this-is)
- [Why It Exists](#why-it-exists)
- [Who It's For](#who-its-for)
- [Quick Start](#quick-start)
  - [Claude Code (5 min)](#claude-code-5-min)
  - [Cursor / VS Code](#cursor--vs-code)
  - [Terminal](#terminal)
- [23 MCP Tools Reference](#23-mcp-tools-reference)
- [Knowledge Base Overview](#knowledge-base-overview)
  - [System Prompt & Persona](#system-prompt--persona)
  - [Intelligence Methodologies](#intelligence-methodologies)
  - [Pivot Playbooks](#pivot-playbooks)
  - [Report Templates](#report-templates)
  - [Ethics & Legal Frameworks](#ethics--legal-frameworks)
- [Usage Examples](#usage-examples)
- [Advanced Configuration](#advanced-configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

---

## What This Is

**OSINT Agent Skills is not an agent. It is not a script. It is not a SaaS.**

It is a **structured knowledge base** — a curated set of methodologies, tool registries, pivot playbooks, ethics rules, and report templates — that any autonomous AI agent can consume to instantly adopt the operating discipline of a senior open-source intelligence analyst.

When you point Claude Code, Cursor, Ollama, OpenCode, AutoClaw, or any MCP-compatible client at this repository, the agent will:

1. ✅ Load `system-prompt.md` and adopt the **OSINT Agent Skills persona** (no fluff, no hallucination)
2. 🔄 Consult `knowledge/methodologies/` to **plan investigations** using the intelligence cycle
3. 🔧 Use 23 **MCP-format tools** from `tools/mcp-tools.json` for DNS, WHOIS, geolocation, breach data, crypto tracing, and more
4. 🎯 Follow `knowledge/pivot-playbooks/` to **chain findings into networks** (email→domain→IP→ASN→threat actor)
5. 📊 Generate **structured intelligence reports** using templates with evidence chains and confidence labels
6. ⚖️ Respect `ethics/legal-frameworks.md` throughout — never suggesting illegal techniques, never fabricating findings

This repository is **agent-agnostic** — it works the same way whether you're using Claude, GPT, local LLMs, or any other framework that supports MCP.

---

## Why It Exists

Modern LLMs are powerful OSINT tools — **but only with the right discipline**.

Without an explicit operating framework, agents:
- 🚫 Hallucinate IP addresses, emails, and dates
- 🚫 Skip source citations (making reports unauditable)
- 🚫 Blur the line between OSINT and intrusion
- 🚫 Produce reports that sound authoritative but contain fabricated "findings"

**OSINT Agent Skills solves this** by codifying the operating rules that a senior analyst would enforce through peer review:

- 📝 **System prompt** is brutally explicit about anti-hallucination
- 🎮 **Pivot playbooks** tell the agent exactly what to do when finding an email, domain, phone, cryptocurrency wallet, or photo
- ⚖️ **Ethics framework** defines what's in-bounds by jurisdiction
- 📋 **Report templates** enforce source citation and confidence labeling

**The result**: When you ask an agent to "investigate example.com," you get a structured intelligence report with cited sources, performed pivots, and explicit limitations — **not a stream of plausible-sounding prose.**

---

## Who It's For

- **Security Researchers** — automate OSINT legwork while maintaining the rigor you'd apply yourself
- **Threat Intelligence Analysts** — delegate repetitive collection, focus on analysis
- **Journalists** — investigate disinformation, fraud, corruption using Bellingcat-style methodology
- **Due Diligence Teams** — background companies and individuals from public sources with audit trails
- **OSINT Educators** — reference framework for teaching methodology
- **Anyone** who's watched an LLM investigate something and produce confidently wrong results

---

## Quick Start

### Claude Code (5 min)

**Option A: Use as an MCP Server**

```bash
# 1. Clone this repo
git clone https://github.com/Skatetop/Omnitrix ~/osint-agent-skills
cd ~/osint-agent-skills

# 2. Install dependencies
npm install

# 3. Start the MCP server
node tools/mcp-server.js
```

Then in Claude Code:
- **Add MCP Server** → select `~/osint-agent-skills`
- Ask: *"Investigate example.com using OSINT Agent Skills methodology"*

**Option B: Use as a Knowledge Base (No MCP Server)**

```bash
# 1. Create a project directory
mkdir ~/osint-projects && cd ~/osint-projects

# 2. Create .claude/settings.json
mkdir -p .claude
cat > .claude/settings.json <<'EOF'
{
  "systemPromptFile": "~/osint-agent-skills/system-prompt.md",
  "knowledge": [
    "~/osint-agent-skills/knowledge/",
    "~/osint-agent-skills/tools/",
    "~/osint-agent-skills/templates/",
    "~/osint-agent-skills/ethics/"
  ]
}
EOF

# 3. Launch Claude Code
claude .
```

**Test Prompt:**
```
Investigate the domain example.com using OSINT Agent Skills methodology.
Produce a full intelligence report with:
- Methodology (intelligence cycle phases)
- Findings (each with sources and confidence level)
- Pivot chain (domain → IP → ASN → threat intel)
- Evidence log
- Limitations
```

### Cursor / VS Code

Add to `~/.cursor/config.json` or `~/.vscode/extensions/cursor-mcp/settings.json`:

```json
{
  "mcpServers": {
    "osint-agent-skills": {
      "command": "node",
      "args": ["/path/to/Omnitrix/tools/mcp-server.js"],
      "env": {
        "OSINT_TOOLS_REGISTRY": "/path/to/Omnitrix/tools/mcp-tools.json"
      }
    }
  }
}
```

### Terminal

Run the MCP server standalone:

```bash
node tools/mcp-server.js
```

Then connect any MCP client (Claude Code, Cursor, Cline, etc.) to `localhost:3000` (or configure stdio transport).

### Environment Variables (Optional)

For API-enabled tools, set these:

```bash
export SHODAN_KEY="your-shodan-api-key"
export VT_API_KEY="your-virustotal-api-key"
export HIBP_KEY="your-haveibeenpwned-api-key"
export HUNTER_KEY="your-hunter-io-api-key"
export ETHERSCAN_KEY="your-etherscan-api-key"
```

Free tools (DNS, WHOIS, Wayback, etc.) work without keys.

---

## 23 MCP Tools Reference

All tools are defined in `tools/mcp-tools.json` and deployed via the MCP server. Each tool accepts structured input and returns JSON.

### Infrastructure & Network

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **dns_lookup** | ✅ | | Resolve DNS records via Google DoH | `dns_lookup("example.com", "A")` |
| **rdap_lookup_domain** | ✅ | | Domain WHOIS data (RDAP protocol) | `rdap_lookup_domain("example.com")` |
| **rdap_lookup_ip** | ✅ | | IP network registration data | `rdap_lookup_ip("1.2.3.4")` |
| **crt_sh_search** | ✅ | | Certificate Transparency log search | `crt_sh_search("example.com")` |
| **shodan_internetdb** | ✅ | | Free Shodan host profiles | `shodan_internetdb("1.2.3.4")` |
| **shodan_host_lookup** | ❌ | `SHODAN_KEY` | Full Shodan search | `shodan_host_lookup("1.2.3.4")` |
| **ipinfo_lookup** | ✅ | | IP geolocation & ASN | `ipinfo_lookup("1.2.3.4")` |
| **bgpview_asn** | ✅ | | BGP routing details | `bgpview_asn("AS12345")` |

### Web & Archives

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **wayback_cdx** | ✅ | | Internet Archive CDX index query | `wayback_cdx("example.com")` |
| **wayback_save** | ✅ | | Save URL to Wayback Machine | `wayback_save("example.com")` |
| **urlscan_search** | ✅ | | Urlscan.io public scan results | `urlscan_search("example.com")` |
| **virustotal_domain_report** | ❌ | `VT_API_KEY` | VirusTotal domain analysis | `virustotal_domain_report("example.com")` |

### Identity & People

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **github_user_lookup** | ✅ | | GitHub profile data | `github_user_lookup("torvalds")` |
| **github_code_search** | ✅ | | Search GitHub repositories | `github_code_search("api_key password")` |
| **gravatar_lookup** | ✅ | | Gravatar profile from email | `gravatar_lookup("user@example.com")` |
| **hunter_email_finder** | ❌ | `HUNTER_KEY` | Email discovery via Hunter.io | `hunter_email_finder("example.com")` |

### Threat Intelligence & Breaches

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **hibp_breach_check** | ❌ | `HIBP_KEY` | HaveIBeenPwned breach lookup | `hibp_breach_check("user@example.com")` |
| **alienvault_otx_lookup** | ✅ | | AlienVault OTX threat intel | `alienvault_otx_lookup("example.com")` |

### Geolocation & Mapping

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **nominatim_geocode** | ✅ | | Forward geocode address via OpenStreetMap | `nominatim_geocode("1600 Pennsylvania Ave")` |

### Cryptocurrency

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **blockchain_address_lookup** | ✅ | | Bitcoin address transactions | `blockchain_address_lookup("1A1z...")` |
| **etherscan_address_lookup** | ❌ | `ETHERSCAN_KEY` | Ethereum address transactions | `etherscan_address_lookup("0x...")` |

### Social Media

| Tool | Free | Key | Purpose | Example |
|------|------|-----|---------|---------|
| **mastodon_user_lookup** | ✅ | | Mastodon/Fediverse profile search | `mastodon_user_lookup("user@mastodon.social")` |

**Full tool definitions:** See `tools/mcp-tools.json` for input schemas and endpoint URLs.

---

## Knowledge Base Overview

### Project Structure

```
Omnitrix/
├── system-prompt.md                  # The core OSINT analyst persona (~3000 words)
├── agent-config.yaml                 # Agent configuration defaults
├── CLAUDE.md                         # Claude Code setup guide
├── server.json                       # MCP server descriptor
├── package.json                      # Node.js dependencies
│
├── tools/
│   ├── mcp-server.js                # MCP server (stdio transport)
│   ├── mcp-tools.json               # 23 tool definitions
│   ├── free-tools.yaml              # Free/public tools registry
│   ├── apis.yaml                    # Premium API tools reference
│   └── cli-tools.yaml               # Local CLI tools (sherlock, holehe, etc.)
│
├── knowledge/
│   ├── README.md                    # Knowledge base index
│   ├── methodologies/
│   │   ├── intelligence-cycle.md    # Five-phase OSINT cycle
│   │   ├── bellingcat-methodology.md # Attribution investigation (9 phases)
│   │   ├── cyber-kill-chain.md      # ATT&CK framework mapping
│   │   ├── mitre-attack-mapping.md  # Technique correlation
│   │   ├── target-triangulation.md  # Confidence and corroboration
│   │   └── source-verification.md   # Evidence evaluation
│   │
│   ├── domains/                     # Investigation guides by subject type
│   │   ├── person-investigation.md
│   │   ├── domain-investigation.md
│   │   ├── ip-investigation.md
│   │   ├── company-investigation.md
│   │   ├── phone-investigation.md
│   │   ├── cryptocurrency.md
│   │   ├── breach-data.md
│   │   ├── geoint.md
│   │   ├── dark-web.md
│   │   ├── social-media.md
│   │   ├── threat-actors.md
│   │   ├── vehicle.md
│   │   └── satellite-imagery.md
│   │
│   ├── pivot-playbooks/             # Chain-pivots by finding type
│   │   ├── email-to-username.md
│   │   ├── username-to-identity.md
│   │   ├── domain-to-infrastructure.md
│   │   ├── ip-to-attribution.md
│   │   ├── breach-to-credentials.md
│   │   ├── phone-to-person.md
│   │   ├── crypto-to-fiat.md
│   │   ├── photo-to-location.md
│   │   └── metadata-to-attribution.md
│   │
│   ├── techniques/                  # Tactical OSINT techniques
│   │   ├── dns-recon.md
│   │   ├── certificate-transparency.md
│   │   ├── google-dorks.md
│   │   ├── shodan-techniques.md
│   │   ├── email-pivoting.md
│   │   ├── username-enumeration.md
│   │   ├── metadata-extraction.md
│   │   ├── reverse-image-search.md
│   │   ├── facial-recognition.md
│   │   ├── graph-generation.md
│   │   └── wayback-investigation.md
│   │
│   ├── osint-bible-mapping.md       # Index to 426+ external OSINT resources
│   └── tool-versioning-policy.md    # Tool maintenance standards
│
├── templates/
│   ├── reports/
│   │   ├── intelligence-report.md   # Standard report format (ICD-203 inspired)
│   │   ├── domain-profile.md        # Domain investigation report
│   │   ├── person-profile.md        # Person investigation report
│   │   ├── threat-actor-profile.md  # Threat actor report
│   │   ├── threat-assessment.md     # Threat assessment template
│   │   ├── investigation-summary.md # Executive summary
│   │   └── timeline.md              # Chronological events
│   │
│   ├── investigation-plan/
│   │   ├── plan-template.md         # Pre-investigation planning
│   │   └── scope-definition.md      # Scope and authorization
│   │
│   ├── evidence/
│   │   ├── evidence-log.md          # Timestamped tool invocations
│   │   ├── chain-of-custody.md      # Audit trail template
│   │   └── source-citation.md       # Citation format
│   │
│   └── graphs/
│       ├── mermaid-graph.md         # Investigation network (Mermaid)
│       ├── dot-template.dot         # Graphviz DOT format
│       ├── graph-schema.json        # JSON schema for graphs
│       └── README.md                # Graph best practices
│
├── ethics/
│   ├── legal-frameworks.md          # US, EU, UK, LatAm laws
│   ├── jurisdiction-rules.md        # Country-specific rules
│   ├── anti-hallucination.md        # Fabrication prohibitions
│   ├── privacy-guidelines.md        # PII handling
│   ├── agent-opsec.md               # Operational security
│   ├── code-of-conduct.md           # Investigator ethics
│   └── README.md                    # Ethics overview
│
├── case-studies/                    # Real-world investigation examples
│   ├── bellingcat-mh17.md           # MH17 aircraft attribution
│   ├── stuxnet-investigation.md     # Stuxnet malware discovery
│   ├── colonial-pipeline.md         # Ransomware attack response
│   ├── reddit-user-attribution.md   # Social media investigation
│   ├── ukraine-power-grid-2015.md   # Cyber attack attribution
│   └── README.md                    # Case study guide
│
├── examples/
│   ├── investigate-domain.md        # Step-by-step domain investigation
│   ├── investigate-email.md         # Email pivot chain example
│   ├── investigate-username.md      # Username tracking example
│   └── README.md                    # Examples index
│
├── integrations/
│   ├── claude-code.md               # Claude Code setup (detailed)
│   ├── cursor.md                    # Cursor IDE integration
│   ├── ollama.md                    # Local LLM setup
│   ├── opencode.md                  # OpenCode integration
│   ├── autoclaw.md                  # AutoClaw integration
│   ├── generic-agent.md             # Universal recipe
│   └── README.md                    # Integration overview
│
├── scripts/
│   ├── validate.sh                  # Validate tool registry
│   ├── validate.ps1                 # Windows validation
│   ├── check-stale-tools.sh         # Identify stale tools
│   └── check-stale-tools.ps1        # Windows stale check
│
├── docs/
│   └── quick-reference.md           # One-page cheatsheet
│
└── LICENSE, CHANGELOG.md, CONTRIBUTING.md
```

### System Prompt & Persona

**File:** `system-prompt.md` (~3000 words)

The system prompt defines the OSINT Agent Skills persona:

- **Identity**: Senior OSINT analyst, not a chatbot
- **Core principles**: Verify → don't assume. Pivot intelligently. Never hallucinate. Respect legality. Maintain OPSEC. Document everything. Minimize harm.
- **Five-phase methodology**: Planning, Collection, Processing, Analysis, Dissemination
- **Anti-hallucination rules**: Never invent IP addresses, emails, dates, or tool outputs
- **Tool usage protocol**: Use free tools first; pause for paid-quota approval
- **Confidence vocabulary**: Confirmed (2+ sources) | Probable (1+ source + logic) | Unverified | Inferred | Speculative
- **Output format**: Structured reports. No filler. Every finding cited. Limitations mandatory.

**Key constraints:**
- 🚫 No pretexting, social engineering, or unauthorized access
- 🚫 No deepfake generation or facial recognition without explicit authorization
- 🚫 No investigating minors outside safeguarding context
- 🚫 No breach-credential use or unauthorized access to private systems

### Intelligence Methodologies

Guides for planning and executing investigations:

#### **Intelligence Cycle** (`knowledge/methodologies/intelligence-cycle.md`)
The five-phase cycle adapted for autonomous OSINT:

1. **Planning & Direction** → Define objective as a question. Scope by time, jurisdiction, data types. Identify authorized pivots. Consult legal basis.
2. **Collection** → Execute ordered lookups (free tools first). Timestamp and hash every result. Log to evidence file.
3. **Processing** → Normalize timestamps (ISO 8601 UTC), domains (punycode lowercase), IPs (canonical form). Dedupe on stable identifiers. Enrich with ASN, registrar, jurisdiction.
4. **Analysis** → Corroborate findings. Assign confidence labels. Map to ATT&CK (threat-intel) or Bellingcat (attribution). Seek disconfirming evidence. Produce draft report.
5. **Dissemination** → Deliver report, evidence log, recommended-next-pivots list, limitations statement. Invite iteration.

#### **Bellingcat Methodology** (`knowledge/methodologies/bellingcat-methodology.md`)
Nine-phase framework for attribution investigations (useful for threat-actor, malware-author, or conspiracy investigations):

1. Target Identification → 2. Data Collection → 3. Source Verification → 4. Triangulation → 5. Pattern Recognition → 6. Timeline Reconstruction → 7. Geographic Analysis → 8. Social Network Mapping → 9. Corroboration & Challenge

#### **MITRE ATT&CK Mapping** (`knowledge/methodologies/mitre-attack-mapping.md`)
Correlate findings to MITRE ATT&CK techniques for threat-intel investigations. Each finding tagged with technique ID (e.g., T1589.003 = Gather Victim Org Information: Employee Names).

#### **Source Verification** (`knowledge/methodologies/source-verification.md`)
Evaluate source credibility: primary vs. secondary, direct vs. interpreted, historical accuracy, potential biases, corroboration by independent sources.

#### **Target Triangulation** (`knowledge/methodologies/target-triangulation.md`)
Confidence labeling rules:
- **Confirmed**: 2+ independent sources OR 1 primary source + corroborating evidence
- **Probable**: 1 credible source + logical inference
- **Unverified**: Stated by 1 source, no corroboration
- **Inferred**: Logical deduction from confirmed findings
- **Speculative**: Hypothesis pending evidence

### Pivot Playbooks

When the agent finds X, what does it do next?

Each playbook specifies:
- **Trigger** — what finding activates it
- **Steps** — ordered collection actions (tool, command, expected output)
- **Anti-patterns** — common mistakes to avoid
- **Output format** — how to report results

| Playbook | Trigger | Typical Tools | Output |
|----------|---------|---------------|--------|
| **email-to-username** | Email address found | Gravatar, GitHub, LinkedIn, usernames DBs | Associated usernames, profiles |
| **username-to-identity** | Username found | Sherlock, holehe, GitHub, Twitter API | Real name, email, profiles, associates |
| **domain-to-infrastructure** | Domain found | DNS, WHOIS, CT logs, Shodan, ipinfo | IPs, ASNs, registrar, MX records, hosting provider |
| **ip-to-attribution** | IP address found | RDAP, BGP, GEOINT, threat intel | ISP, country, ASN, reverse DNS, associated domains |
| **breach-to-credentials** | Email in breach confirmed | HIBP, breach databases | Password hash, plaintext (if available), other breaches |
| **phone-to-person** | Phone number found | Reverse phone lookup, social media | Name, carrier, location history, associates |
| **crypto-to-fiat** | Blockchain wallet found | Blockchain.com, Etherscan, exchange APIs | Transaction history, linked exchanges, KYC info |
| **photo-to-location** | Photo/image found | EXIF, reverse image search, Google Maps | Approximate location, landmarks, metadata |
| **metadata-to-attribution** | Document metadata found | EXIF, PDF metadata extraction | Author, creation date, software, printer details |

**Example: Domain → Infrastructure Pivot**
```
1. Query: dig example.com (get IPs)
2. Query: rdap_lookup_domain("example.com") (get registrar, admin email)
3. Query: crt_sh_search("example.com") (get associated subdomains)
4. Query: shodan_internetdb(IP) for each IP (get open ports, services)
5. Query: ipinfo_lookup(IP) for each IP (get ASN, country)
6. Report: Infrastructure map with IPs, ISP, registrar, historical IPs
```

### Report Templates

Structured Markdown templates that enforce citation and confidence labeling.

#### **Intelligence Report** (`templates/reports/intelligence-report.md`)
Standard structure inspired by ICD-203 (U.S. Intelligence Community Directive):

```markdown
# Intelligence Report: [Subject]

## Classification
Unclassified // For [User/Client Name]

## Executive Summary
[1-3 paragraphs: what was investigated, key findings]

## Methodology
[Intelligence cycle phases used, scope, limitations]

### Investigation Objective
[As a question]

### Timeline
[Investigation start → completion; any delays or rate limits]

## Findings

### Finding 1: [Claim]
- **Confidence**: Confirmed / Probable / Unverified / Inferred / Speculative
- **Primary Source**: [Tool name, URL, timestamp]
- **Corroborating Source**: [Tool name, timestamp]
- **Details**: [Fact]
- **MITRE ATT&CK**: [Technique if applicable]

### Finding 2: [Claim]
[Same structure]

## Pivot Chain
[Entities connected: Domain → IP → ASN → Threat Actor]

## Recommended Next Steps
- [Authorized pivot 1] — requires [specific approval]
- [Authorized pivot 2] — requires [specific approval]

## Limitations
- Cannot verify [reason]
- Out of scope: [reason]
- Stale data: [reason]
- Jurisdiction-dependent: [reason]

## Sources
1. [Tool name, query, timestamp, hash of output]
2. [Tool name, query, timestamp, hash of output]

## Appendices
- **Evidence Log**: See `templates/evidence/evidence-log.md`
- **Investigation Plan**: See `templates/investigation-plan/plan-template.md`
```

Other templates:
- **Domain Profile** — Detailed domain investigation report
- **Person Profile** — Individual background investigation
- **Threat Actor Profile** — Malware author or threat group dossier
- **Threat Assessment** — Risk evaluation of a finding
- **Investigation Summary** — Executive brief
- **Timeline** — Chronological event log

### Ethics & Legal Frameworks

**Location:** `ethics/`

#### **Legal Frameworks** (`ethics/legal-frameworks.md`)
Country-specific OSINT boundaries:

- **United States**: Free public records; CFAA restrictions on unauthorized access; reasonable expectation of privacy (4th Amendment)
- **European Union**: GDPR restrictions on personal data processing; right to erasure; consent-based
- **United Kingdom**: GDPR + DPA 2018; Investigatory Powers Act (IPA) limits
- **Latin America**: Varying privacy laws by country; data protection regulations evolving
- **Other jurisdictions**: Consult local counsel

#### **Anti-Hallucination** (`ethics/anti-hallucination.md`)
Absolute prohibitions:
- 🚫 Never invent IP addresses, email addresses, usernames, or dates
- 🚫 Never fabricate tool output or "example" findings
- 🚫 Never claim "confidence: Confirmed" without 2+ sources
- 🚫 Every finding must cite a real source with timestamp
- 🚫 If a tool failed or returned nothing, report exactly that

#### **Privacy Guidelines** (`ethics/privacy-guidelines.md`)
- Minimize collection of personal data (PII)
- Discard non-essential PII from reports
- Mask phone numbers, SSNs, passport numbers when citing
- Never republish leaked private data without explicit authorization

#### **Agent OPSEC** (`ethics/agent-opsec.md`)
- Use residential proxies or VPNs for sensitive investigations
- Rotate user-agents to avoid detection
- Respect robots.txt and rate-limit headers
- Do not scrape at scale; paginate responsibly
- Log all external connections for audit

#### **Code of Conduct** (`ethics/code-of-conduct.md`)
OSINT investigator principles: integrity, humility, transparency, harm reduction, legal compliance.

---

## Usage Examples

### Example 1: Domain Investigation

**Prompt:**
```
Investigate the domain sparkle-cosmetics.shop using OSINT Agent Skills methodology.
Produce an intelligence report with:
- Infrastructure findings (IPs, ASN, registrar)
- Historical snapshot from Wayback Machine
- SSL/TLS certificate analysis
- Threat intelligence correlation (VirusTotal, AlienVault OTX)
- Confidence labels for each finding
```

**Agent execution:**
1. **Planning** → Define objective: "What is the infrastructure and threat status of sparkle-cosmetics.shop?"
2. **Collection** → Run DNS, WHOIS, Certificate Transparency, Shodan, VirusTotal queries
3. **Processing** → Normalize IPs, dedupe domains, enrich with ASN data
4. **Analysis** → Assign confidence labels, map to threat intel feeds, produce report
5. **Dissemination** → Deliver structured report + evidence log

**Expected output:**
```markdown
# Intelligence Report: sparkle-cosmetics.shop

## Executive Summary
Domain registered 2024-01-15 via NameCheap; hosted on Cloudflare (AS13335).
No malware detections on VirusTotal (as of 2026-07-26).
Likely legitimate e-commerce site; confidence: Probable (single registrar check).

## Findings

### Finding 1: Domain registered to privacy-protected registrant
- **Confidence**: Confirmed
- **Primary Source**: RDAP lookup via ICANN registry
- **Details**: registrant_contact: REDACTED; registrar: NameCheap Inc.
- **Timestamp**: 2026-07-26T21:30:00Z

### Finding 2: Hosted on Cloudflare ASN 13335
- **Confidence**: Confirmed
- **Primary Source**: DNS A record resolution via Google DoH
- **Corroborating Source**: ipinfo.io ASN lookup
- **Details**: IP 104.21.x.x (Cloudflare, AS13335, United States)
- **MITRE ATT&CK**: T1589.001 (Gather Victim Org Information: Credentials)

... [more findings]
```

### Example 2: Email → Username Chain

**Prompt:**
```
I found the email address admin@company-x.biz in a data breach.
Trace the associated username and identities using email-to-username pivot playbook.
```

**Agent execution:**
1. **Pivot trigger** → Email found
2. **Activate playbook** → `knowledge/pivot-playbooks/email-to-username.md`
3. **Collection steps**:
   - Query Gravatar for profile photo
   - GitHub API search for email
   - Sherlock username enumeration
   - LinkedIn search (if authorized)
4. **Report** → Usernames, associated profiles, confidence labels

### Example 3: Threat Actor Attribution

**Prompt:**
```
Investigate potential connections between the TrickBot malware family and 
the Wizard Spider threat group. Use Bellingcat methodology.
```

**Agent execution:**
1. **Planning** → Scope: TrickBot samples, C2 infrastructure, associated tools (Ryuk, Conti)
2. **Collection** → Query VirusTotal, AlienVault OTX, abuse.ch, URLhaus
3. **Analysis** → Map findings to ATT&CK framework; cross-reference with public reports
4. **Bellingcat application** → 9-phase attribution process
5. **Report** → Confidence-labeled attribution, recommended next investigations

---

## Advanced Configuration

### Adding Custom MCP Tools

Edit `tools/mcp-tools.json` and append:

```json
{
  "name": "my_custom_tool",
  "description": "Custom OSINT tool description",
  "input_schema": {
    "type": "object",
    "properties": {
      "query": { "type": "string", "description": "Search query" }
    },
    "required": ["query"]
  },
  "annotations": {
    "endpoint": "https://api.example.com/search",
    "method": "GET",
    "auth_required": false,
    "rate_limit": "100 req/hour"
  }
}
```

Restart the MCP server for changes to take effect.

### Custom Pivot Playbooks

Create a new file in `knowledge/pivot-playbooks/my-pivot.md`:

```markdown
# [Finding Type] → [New Finding Type]

## Trigger
When the agent finds [X], activate this playbook.

## Steps

### Step 1: [Description]
- **Tool**: [MCP tool name]
- **Command**: `[tool_name]("[parameter]")`
- **Expected output**: [JSON structure]

### Step 2: [Description]
[Steps continue...]

## Anti-Patterns
- ❌ Do not assume [common mistake]
- ❌ Do not [another mistake]

## Output Format
Report findings as:
- **Confidence**: [level]
- **Source**: [tool]
- **Details**: [facts]
```

The agent will automatically discover and follow custom playbooks.

### Jurisdiction Override

Set in `agent-config.yaml`:

```yaml
default_jurisdiction: "EU"  # Changes default legal framework
authorized_pivots:
  - "domain-to-infrastructure"  # Autonomous
  - "crypto-to-fiat"             # Requires approval
unauthorized_pivots:
  - "facial-recognition"         # Always blocked
```

### Project-Scoped Context

For investigations into related subjects, create `notes/` directory in your project:

```bash
mkdir -p ~/osint-projects/notes
echo "Subject A is associated with Subject B per [source]" > notes/context.md
```

Claude Code will automatically load and reference these notes.

---

## Troubleshooting

### MCP Server Won't Start

```bash
# Check Node.js version (≥18 required)
node --version

# Check if port 3000 is in use
lsof -i :3000

# Run with verbose logging
DEBUG=* node tools/mcp-server.js
```

### Tools Not Appearing in Claude Code

1. Confirm `server.json` is valid JSON:
   ```bash
   jq . server.json
   ```
2. Restart Claude Code after adding the MCP server
3. Check that `tools/mcp-tools.json` exists and is readable
4. Run `npm install` if dependencies are missing

### API Keys Not Being Used

Set environment variables **before** starting the server:

```bash
export SHODAN_KEY="key..."
export VT_API_KEY="key..."
node tools/mcp-server.js
```

Verify they were loaded:

```bash
node -e "console.log(process.env.SHODAN_KEY)"
```

### Agent Ignores System Prompt

Ensure `.claude/settings.json` contains:

```json
{
  "systemPromptFile": "/absolute/path/to/system-prompt.md"
}
```

Claude Code prioritizes the system prompt only if it's in the current working directory's `.claude/` folder.

### Rate Limits Exceeded

Free tier limits (as of 2026-07-26):
- **Google DoH** (DNS): ~1000/day per IP
- **RDAP**: ~100/minute per registrar
- **crt.sh**: ~30/minute per IP
- **Wayback CDX**: ~100/second
- **ipinfo.io**: ~50,000/month (free tier)

The agent should pause and report rate-limit errors. Use `SHODAN_KEY`, `VT_API_KEY`, etc., to increase limits.

### "Fabrication Detected"

If an agent hallucinates findings, check:
1. Is the system prompt being loaded? (Check Claude Code logs)
2. Are the anti-hallucination rules in `ethics/anti-hallucination.md` being enforced?
3. Are tool outputs being logged to the evidence file?

Report as a GitHub issue with the full prompt history.

---

## Contributing

Contributions are welcome! See [`CONTRIBUTING.md`](CONTRIBUTING.md).

### Contribution types especially needed:
- ✅ New pivot playbooks (e.g., `video-to-location.md`, `loan-fraud-detection.md`)
- ✅ New free tools (add to `tools/free-tools.yaml` with endpoint and example)
- ✅ New jurisdiction rules (edit `ethics/jurisdiction-rules.md`)
- ✅ Case studies (add to `case-studies/` with methodology walkthrough)
- ✅ Technique guides (add to `knowledge/techniques/`)
- ✅ Bug reports (GitHub Issues)
- ✅ Documentation improvements

### Development workflow:

```bash
# Clone
git clone https://github.com/Skatetop/Omnitrix
cd Omnitrix

# Create a feature branch
git checkout -b feature/new-pivot-playbook

# Make changes
echo "# New Playbook" > knowledge/pivot-playbooks/my-pivot.md

# Validate (if scripts available)
npm run validate

# Commit with clear message
git commit -m "Add new-pivot-playbook for finding-type pivots"

# Push and open PR
git push origin feature/new-pivot-playbook
```

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for detailed guidelines.

---

## License

MIT License. See [`LICENSE`](LICENSE).

**Attribution**: OSINT Agent Skills is maintained by Frangel Barrera and adapted from the [OSINT-BIBLE](https://github.com/frangelbarrera/OSINT-BIBLE) methodology compilation.

---

## Citation

If you use OSINT Agent Skills in research or professional work, cite as:

```bibtex
@software{osint-agent-skills,
  title={OSINT Agent Skills},
  author={Barrera, Frangel and Contributors},
  year={2024},
  url={https://github.com/Skatetop/Omnitrix}
}
```

---

## Quick Links

- 📚 **Methodologies**: [`knowledge/methodologies/`](knowledge/methodologies/)
- 🎯 **Pivot Playbooks**: [`knowledge/pivot-playbooks/`](knowledge/pivot-playbooks/)
- 📋 **Report Templates**: [`templates/reports/`](templates/reports/)
- ⚖️ **Ethics & Legal**: [`ethics/`](ethics/)
- 💻 **Integration Guides**: [`integrations/`](integrations/)
- 🔧 **Tool Registry**: [`tools/`](tools/)
- 📖 **Case Studies**: [`case-studies/`](case-studies/)
- 💡 **Examples**: [`examples/`](examples/)

---

**Version**: 1.4.1  
**Last Updated**: 2026-07-26  
**Maintainer**: Skatetop/Omnitrix Contributors

🔍 **Turn your AI agent into a senior OSINT analyst.**
