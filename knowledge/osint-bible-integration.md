# OSINT Bible Integration & Resource Mapping

> **OSINT Agent Skills + OSINT Bible = Complete Intelligence Framework**
>
> This document bridges the OSINT Agent Skills structured knowledge base with the OSINT Bible's comprehensive 426+ tool catalog across 47 sections.

---

## Overview

**OSINT Bible** (https://github.com/frangelbarrera/OSINT-BIBLE) is a curated index of 426+ open-source intelligence tools, techniques, and resources organized across 47 specialized domains.

**OSINT Agent Skills** implements a rigorous, anti-hallucination framework with 23 MCP tools and structured methodologies.

**This integration** creates a two-tier approach:
1. **Structured tier** (OSINT Agent Skills) — for autonomous agents with discipline and audit trails
2. **Comprehensive tier** (OSINT Bible) — for human analysts seeking complete tool catalogs

---

## OSINT Bible 47-Section Map

### Section 1: Fundamentals
**Key Concepts**: OSINT, OPSEC, Intelligence Cycle, PII, Primary/Secondary Sources

**Mapping to OSINT Agent Skills**:
- See `methodologies/intelligence-cycle.md` (Five phases)
- See `ethics/privacy-guidelines.md` (PII handling)
- See `ethics/agent-opsec.md` (Minimizing footprint)

### Section 2: 4-Step Methodology
**Key Framework**: Define → Identify → Collect → Validate & Document

**Mapping to OSINT Agent Skills**:
- Phase 1 (Planning) → Define question, identify sources
- Phase 2 (Collection) → Execute lookups, timestamp everything
- Phase 3 (Processing) → Normalize, dedupe, enrich
- Phase 4 (Analysis) → Validate, corroborate, assign confidence
- Phase 5 (Dissemination) → Report with evidence chain

### Section 3: Tools Mind Map
**Visual Overview**: 100+ tools across 6 categories (Search, Social, Geo, Domain/IP, Deep/Dark, Automate)

**Cross-reference**: Each tool category maps to sections below.

### Section 4: Internet Search (Google Dorks, Alt Search Engines)
**Coverage**: 80+ search platforms, 20 Google dork patterns, archives

**MCP Tool Mapping**:
| BIBLE Tool | MCP Alternative | Notes |
|---|---|---|
| Google Dorks | `dns_lookup`, `github_code_search` | Free text search via DNS or GitHub |
| Shodan | `shodan_internetdb` (free) or `shodan_host_lookup` (requires key) | Host discovery |
| Censys | `crt_sh_search` (free alt) | Certificate transparency search |
| AlienVault OTX | `alienvault_otx_lookup` (free) | Threat intelligence feed |
| VirusTotal | `virustotal_domain_report` (requires key) | Domain analysis |
| URLhaus | Manual lookup (free tier) | Malware URL database |
| Have I Been Pwned | `hibp_breach_check` (requires key) | Breach verification |
| Wayback Machine | `wayback_cdx` (free) | Internet Archive query |

**Advanced Google Dorks** (Section 29):
```
Reconnaissance:
site:linkedin.com "@target.com"          # Find employees
intitle:"index of" "target.com" passwords # Look for exposed files
site:github.com "target.com" API_KEY      # Leaked credentials
```

See `techniques/google-dorks.md` for structured dork library.

### Section 5: Social Networks (Facebook, Instagram, Twitter/X, LinkedIn, Reddit, etc.)
**Coverage**: 100+ social media investigation tools

**Use Cases**:
- Username enumeration
- Profile scraping
- Historical data retrieval
- Cross-platform account linking

**Pivot Playbook**: `knowledge/pivot-playbooks/email-to-username.md`

**Key Tools**:
- Maigret (username enumeration) — not in MCP, use CLI
- Twint/Twint-fork (Twitter archive) — not in MCP
- Instaloader (Instagram download) — not in MCP
- Osintgram (Instagram reconnaissance) — not in MCP

**MCP Alternative**: `github_user_lookup` + `mastodon_user_lookup` (partial coverage)

### Section 6: GEOINT & Images
**Coverage**: Satellite imagery, photo geolocation, EXIF extraction, reverse image search

**Pivot Playbook**: `knowledge/pivot-playbooks/photo-to-location.md`

**Key Tools**:
- Google Lens (reverse image search)
- Yandex (reverse image search)
- TinEye (reverse image search)
- ExifTool (metadata extraction)
- Overpass Turbo (OpenStreetMap query)
- Satellites.pro (live satellite imagery)
- Google Earth Pro (historical imagery)

**MCP Tool Mapping**:
| BIBLE Tool | MCP Alternative | Notes |
|---|---|---|
| Nominatim | `nominatim_geocode` (free) | Forward geocoding |
| Overpass Turbo | Manual lookup | OpenStreetMap features |
| ExifTool | CLI-based | Run locally in shell |

See `techniques/metadata-extraction.md` for detailed workflow.

### Section 7: Domain / IP / DNS
**Coverage**: WHOIS, DNS recon, certificate transparency, IP geolocation, ASN lookup

**Pivot Playbook**: `knowledge/pivot-playbooks/domain-to-infrastructure.md`

**MCP Tool Mapping** (Full Coverage):
| BIBLE Tool | MCP Tool | Status |
|---|---|---|
| WHOIS/RDAP | `rdap_lookup_domain`, `rdap_lookup_ip` | ✅ Fully supported |
| DNS Recon | `dns_lookup` (Google DoH) | ✅ Free tier |
| Certificate Transparency | `crt_sh_search` | ✅ Free tier |
| ipinfo.io | `ipinfo_lookup` | ✅ Free tier |
| BGPview | `bgpview_asn` | ✅ Free tier |
| Shodan | `shodan_internetdb`, `shodan_host_lookup` | ✅ Mixed (free + key) |
| DNSDumpster | Manual (crt.sh alternative) | 🟡 Partial |
| SecurityTrails | Not in MCP | Manual lookup needed |
| Amass | Not in MCP | Run locally |

See `techniques/dns-recon.md`, `techniques/certificate-transparency.md`, `domains/domain-investigation.md`.

### Section 8: Deep & Dark Web
**Coverage**: Tor, I2P, Onion sites, .onion indexing, marketplace research

**Key Tools**:
- Ahmia (Onion search)
- OnionScan (Onion site scanner)
- Recon-ng (Automation framework)
- SpiderFoot (All-in-one framework)

**Note**: Limited MCP support for dark web (ethical boundary). Use CLI tools or manual investigation.

See `domains/dark-web.md` for methodology.

### Section 9: Automation (Python)
**Coverage**: Python frameworks for OSINT automation (Recon-ng, SpiderFoot, Shodan CLI, etc.)

**Frameworks**:
- Recon-ng (modular reconnaissance)
- SpiderFoot (automated OSINT)
- Shodan CLI (internet scanning)
- Metagoofil (metadata extraction)

**Integration**: Run via CLI shell in Claude Code or as pre-collection steps.

### Section 10: Report Templates
**Coverage**: Intelligence report formats, evidence templates, chain of custody

**Mapping to OSINT Agent Skills** (Full):
| BIBLE Section | OSINT Agent Skills | Notes |
|---|---|---|
| ICD-203 Reports | `templates/reports/intelligence-report.md` | Standard format |
| Domain Reports | `templates/reports/domain-profile.md` | Domain-specific |
| Person Reports | `templates/reports/person-profile.md` | Individual profiles |
| Threat Actor | `templates/reports/threat-actor-profile.md` | Attribution focus |
| Evidence Logs | `templates/evidence/evidence-log.md` | Timestamped & hashed |
| Chain of Custody | `templates/evidence/chain-of-custody.md` | Audit trail |

See `templates/reports/` for all templates.

### Section 11: Legal Considerations
**Coverage**: Laws by jurisdiction (US, EU, UK, LatAm), CFAA, GDPR, DPA

**Mapping to OSINT Agent Skills** (Full):
| Jurisdiction | OSINT Agent Skills Reference |
|---|---|
| United States | `ethics/legal-frameworks.md` → US section |
| European Union | `ethics/legal-frameworks.md` → EU section |
| United Kingdom | `ethics/legal-frameworks.md` → UK section |
| Latin America | `ethics/legal-frameworks.md` → LatAm section |

See `ethics/legal-frameworks.md` for complete country-by-country breakdown.

### Section 12: Extra Resources
**Coverage**: Collections, educational materials, tool aggregators

**Cross-reference**: All resource links consolidated in `integrations/generic-agent.md`.

### Section 13: AI Intelligence
**Coverage**: AI-powered OSINT (ChatGPT for research, Claude for analysis, etc.)

**Integration**: OSINT Agent Skills IS the AI integration framework. See `system-prompt.md` for persona design.

**Recommended**: Use Claude Code + OSINT Agent Skills for AI-assisted investigations.

### Section 14: Facial Recognition
**Coverage**: Facial recognition tools (FaceSearch, Clearview AI, Yandex Face Search)

**⚠️ Ethical Boundary**: Disabled by default in `system-prompt.md`. Requires explicit user authorization.

See `ethics/code-of-conduct.md` for responsible use guidelines.

### Section 15: Email/Phone Investigation
**Coverage**: Email enumeration, phone lookup, reverse phone, email verification

**Pivot Playbook**: `knowledge/pivot-playbooks/email-to-username.md`, `knowledge/pivot-playbooks/phone-to-person.md`

**MCP Tool Mapping**:
| BIBLE Tool | MCP Alternative | Notes |
|---|---|---|
| Hunter.io | `hunter_email_finder` (requires key) | Email discovery |
| Gravatar | `gravatar_lookup` (free) | Email to profile |
| Infobel | Manual lookup | Phone reverse search |
| TrueCaller | Manual lookup | Phone verification |

### Section 16: Data Breaches
**Coverage**: Breach databases (HIBP, BreachBase, DeHashed, BleepingComputer)

**Pivot Playbook**: `knowledge/pivot-playbooks/breach-to-credentials.md`

**MCP Tool Mapping**:
| BIBLE Tool | MCP Alternative | Notes |
|---|---|---|
| Have I Been Pwned | `hibp_breach_check` (requires key) | Email breach lookup |
| BreachBase | Manual lookup | Breach database search |
| Breach Directory | Manual lookup | Curated breaches |

### Section 17: Blockchain/Crypto
**Coverage**: Blockchain explorers, wallet tracking, exchange monitoring, mixer tracing

**Pivot Playbook**: `knowledge/pivot-playbooks/crypto-to-fiat.md`

**MCP Tool Mapping** (Full Coverage):
| BIBLE Tool | MCP Alternative | Status |
|---|---|---|
| Blockchain.com | `blockchain_address_lookup` (free) | ✅ Bitcoin |
| Etherscan | `etherscan_address_lookup` (requires key) | ✅ Ethereum |
| BlockCypher | Not in MCP | Manual lookup |
| Chainalysis | Not in MCP | Requires subscription |

See `domains/cryptocurrency.md` for detailed methodology.

### Section 18: Transport OSINT
**Coverage**: Flight tracking (FlightAware, FlightRadar24), maritime (MarineTraffic, VesselFinder)

**Use Cases**: Asset tracking, travel pattern analysis, supply chain investigation

**Key Tools**:
- FlightAware (flight tracking)
- FlightRadar24 (real-time radar)
- MarineTraffic (ship tracking)
- VesselFinder (vessel search)

**Note**: Partially covered by external tools; not in MCP.

### Section 19: WiFi/Wardriving
**Coverage**: WiFi mapping (WiFi Map, Kismet), network scanning, access point enumeration

**Note**: Limited OSINT scope (primarily defensive OPSEC). See `ethics/agent-opsec.md`.

### Section 20: Content Verification
**Coverage**: Fact-checking, media authentication, reverse video search

**Key Methodology**: See `methodologies/source-verification.md` and `target-triangulation.md`.

### Section 21: Username Enumeration
**Coverage**: Maigret (cross-platform username search), Sherlock, Snoop

**Pivot Playbook**: `knowledge/pivot-playbooks/username-to-identity.md`

**Key Tools**:
- Maigret (100+ site search)
- Sherlock (username search)
- Snoop (user reconnaissance)

**Note**: CLI-based; not in MCP. Run via shell.

### Section 22: Web Scraping
**Coverage**: BeautifulSoup, Scrapy, Selenium, puppeteer, ethical scraping

**Note**: Respect robots.txt and rate limits. See `ethics/agent-opsec.md` → "Scraping responsibly".

### Section 23: Metadata Extraction
**Coverage**: ExifTool, mediainfo, pdf metadata, document analysis

**Technique**: See `techniques/metadata-extraction.md`.

**Use Case**: Photo location pivots, document authorship, file creation dates.

### Section 24: Network Scanning
**Coverage**: Nmap, Shodan, Censys, port scanning, vulnerability scanning

**Note**: Limited autonomous use (ethical boundaries). See `ethics/code-of-conduct.md`.

### Section 25: Dark Web
**Coverage**: Tor, I2P, Onion marketplaces, forum scraping

**Domain Guide**: See `domains/dark-web.md` for ethical investigation framework.

### Section 26: All-in-One Frameworks
**Coverage**: Recon-ng, SpiderFoot, Maltego, Shodan CLI, DNSRecon

**Integration Strategy**:
1. Use MCP tools for autonomous, audited workflows
2. Use CLI frameworks for complex, human-guided investigations
3. Log all external tool invocations to evidence log

**Recommended Integration**: Run SpiderFoot locally, export results, feed to Claude Code for analysis.

### Section 27: Advanced Maltego
**Coverage**: Maltego transforms, custom transforms, machine learning

**Note**: Specialized tool (not in MCP). Recommended for complex link analysis workflows.

### Section 28: Professional Methodologies
**Coverage**: ICD-203, Bellingcat, MITRE ATT&CK, structured analysis

**Mapping to OSINT Agent Skills** (Full):
| Professional Standard | OSINT Agent Skills Reference |
|---|---|
| ICD-203 Intelligence Reports | `templates/reports/intelligence-report.md` |
| Bellingcat Attribution | `methodologies/bellingcat-methodology.md` |
| MITRE ATT&CK | `methodologies/mitre-attack-mapping.md` |
| Structured Analytic Techniques | `methodologies/structured-analytic-techniques.md` |

### Section 29: Advanced Google Dorks
**Coverage**: 100+ specialized dorks for each target type

**Technique Guide**: See `techniques/google-dorks.md`.

**Examples**:
```
Exposed API keys:
site:github.com "[target] api_key" OR "APIKEY"

Exposed configuration:
intitle:"index.of" "config.php" OR "config.json"

Exposed credentials:
filetype:xlsx password OR admin OR secret
```

### Section 30: Learning Resources
**Coverage**: OSINT courses, certifications, educational platforms

**Cross-reference**: See `examples/` for worked walkthroughs.

### Section 31: People Investigations
**Coverage**: People search engines, public records, genealogy sites

**Domain Guide**: See `domains/person-investigation.md`.

**Key Tools**:
- LinkedIn (employer, network)
- Whitepages (address, phone)
- Ancestry.com (genealogy)
- Court records (legal history)

### Section 32: Company Research
**Coverage**: Corporate information, SEC filings, business registries, employee records

**Domain Guide**: See `domains/company-investigation.md`.

**Key Tools**:
- SEC EDGAR (public filings)
- Crunchbase (startup data)
- LinkedIn (employee roster)
- Glassdoor (company reviews, salaries)

### Section 33: Threat Intelligence Feeds
**Coverage**: MISP, YARA rules, IOC feeds, threat actor tracking

**MCP Mapping**:
| BIBLE Tool | MCP Alternative | Notes |
|---|---|---|
| AlienVault OTX | `alienvault_otx_lookup` (free) | Threat intelligence |
| VirusTotal | `virustotal_domain_report` (key) | Malware correlation |
| URLhaus | Manual lookup | Malware URL feeds |
| abuse.ch | Manual lookup | Phishing/malware tracking |

### Section 34: ICS/OT & Critical Infrastructure OSINT
**Coverage**: Shodan ICS filters, industrial control systems, SCADA research

**Specialized Domain**: See `knowledge/domains/` (add `critical-infrastructure.md` if needed).

**Key Tools**:
- Shodan with ICS filters (port 502, 503, 5000, etc.)
- DNSRecon for network enumeration
- nmap for port scanning (ethically)

### Section 35: AI Agent Skills & MCP
**Coverage**: This framework + MCP protocol + Claude Code

**Full Integration**: You are here! See `CLAUDE.md` and this document.

### Sections 36–47: 2026 Expansion Topics

#### Section 36: Financial OSINT
**Coverage**: Banking, cryptocurrency, sanctions screening, financial crimes

**Domains to Add**: 
- `knowledge/domains/financial-investigation.md` (recommended)

#### Section 37: Investigator OPSEC & Sock Puppets
**Coverage**: VPN/proxy selection, anonymization, cover stories

**Mapping**: See `ethics/agent-opsec.md` (adapt for human investigators).

#### Section 38: Cloud Storage OSINT
**Coverage**: Google Drive shares, Dropbox public links, AWS S3 buckets, Azure blobs

**Technique**: See `techniques/cloud-storage-osint.md` (to be added).

#### Section 39: Mobile App OSINT
**Coverage**: APK analysis, app store reconnaissance, mobile device fingerprinting

#### Section 40: Decentralized Social OSINT
**Coverage**: Mastodon, Bluesky, Nostr, ActivityPub federation

**MCP Tool**: `mastodon_user_lookup` (free, partial support).

#### Section 41: Counter-OSINT Self-Audit
**Coverage**: Information leakage assessment, digital footprint minimization

**Cross-reference**: `ethics/agent-opsec.md`.

#### Section 42: Discord & Telegram OSINT 2026
**Coverage**: Message archiving, user enumeration, bot reconnaissance

**Note**: Requires bot access; limited MCP support.

#### Section 43: Satellite OSINT 2026
**Coverage**: Open-source satellite imagery, change detection, temporal analysis

**Key Resources**:
- Satellites.pro (live imagery)
- Google Earth Pro (archive)
- Sentinel-2 (ESA open data)
- Maxar Open Data (disaster response)

#### Section 44: C2PA + SynthID + Deepfake Detection 2026
**Coverage**: Content authenticity, AI-generated content detection, media forensics

**Cross-reference**: `techniques/content-verification.md`.

#### Section 45: Professional Templates & Deliverables
**Coverage**: Report templates, brief formats, briefing slides

**Mapping**: See `templates/reports/` (full library included in OSINT Agent Skills).

#### Section 46: Regional OSINT
**Coverage**: Regional-specific resources, language-specific search engines, local databases

**Examples**:
- Middle East: Bayara, Zoomaal
- Latin America: government registries, regional press
- East Asia: Baidu, Yandex (CIS), regional social platforms
- Africa: national registries, regional news aggregators

#### Section 47: Corporate OSINT Tradecraft
**Coverage**: Due diligence, competitive intelligence, vendor assessment

**New Domain to Add**: `knowledge/domains/corporate-investigation.md` (recommended).

---

## Integration Strategy: Two-Tier OSINT

### Tier 1: Autonomous (OSINT Agent Skills MCP)
**When to use**: Structured, auditable, repeatable investigations

- ✅ Cloud-native (runs in Claude Code or any MCP client)
- ✅ Anti-hallucination constraints
- ✅ Built-in evidence logging
- ✅ Confidence labeling
- ✅ No paid API keys required (free tier tools)

**Workflow**:
```
Claude Code → Load system prompt → Consult knowledge base → Invoke MCP tools
  → Record evidence → Produce report → Output with citations
```

### Tier 2: Comprehensive (OSINT Bible + CLI Tools)
**When to use**: In-depth, complex investigations requiring tool specialization

- ✅ 426+ tools across all domains
- ✅ Specialized tool chains (e.g., SpiderFoot + Maltego)
- ✅ Framework-based automation (Recon-ng, SpiderFoot)
- ✅ Direct CLI access for power users

**Workflow**:
```
Select investigation domain → Consult OSINT Bible (Section N) → Identify tools
  → Run CLI tools → Export results → Feed to Claude Code for analysis
```

---

## Quick Reference: MCP Tool → BIBLE Tool Mapping

| MCP Tool | BIBLE Coverage | Best For | Alternatives |
|---|---|---|---|
| `dns_lookup` | Section 7 (DNS Recon) | Domain enumeration | DNSDumpster, Amass |
| `rdap_lookup_domain` | Section 7 (WHOIS) | Domain registration | WhoisLookup, ICANN |
| `rdap_lookup_ip` | Section 7 (IP Investigation) | IP ownership | MaxMind, RIPE |
| `crt_sh_search` | Section 7 (CT Logs) | Subdomain discovery | Amass, Censys |
| `shodan_internetdb` | Section 4 (Search), Section 24 (Scanning) | Host discovery (free) | Censys, Binaryedge |
| `shodan_host_lookup` | Section 4, 24 | Full Shodan search | Censys, FOFA, Netlas |
| `ipinfo_lookup` | Section 7 (IP/ASN) | Geolocation | MaxMind, IP2Location |
| `bgpview_asn` | Section 7 (ASN) | BGP/routing info | RIPE, Cymru, Shadowserver |
| `wayback_cdx` | Section 4 (Archives), Section 8 (Snapshots) | Historical pages | Archive.is, Stored.website |
| `wayback_save` | Section 4 (Archives) | Archive URLs | Archive.org, Perma.cc |
| `urlscan_search` | Section 4 (Archives) | URL scanning | VirusTotal, URLhaus |
| `github_user_lookup` | Section 5 (Social), Section 21 (Usernames) | Account discovery | GitHub API, Sherlock |
| `github_code_search` | Section 4 (Search), Section 29 (Dorks) | Credential leak detection | SearchCode, PublicWWW |
| `gravatar_lookup` | Section 5 (Social), Section 15 (Email) | Email to avatar | Hunter.io, Rocketreach |
| `hunter_email_finder` | Section 15 (Email) | Corporate email discovery | RocketReach, Clearbit |
| `hibp_breach_check` | Section 16 (Breaches) | Breach verification | BreachBase, DeHashed |
| `alienvault_otx_lookup` | Section 33 (Threat Intel) | Threat intelligence | VirusTotal, URLhaus |
| `virustotal_domain_report` | Section 4 (Search), Section 33 (Threat) | Malware detection | Hybrid-Analysis, URLhaus |
| `nominatim_geocode` | Section 6 (GEOINT) | Reverse geocoding | Google Maps, OpenStreetMap |
| `blockchain_address_lookup` | Section 17 (Crypto) | Bitcoin tracking | Blockchain.com, Chainalysis |
| `etherscan_address_lookup` | Section 17 (Crypto) | Ethereum tracking | Etherscan, EtherChain |
| `mastodon_user_lookup` | Section 40 (Decentralized Social) | Mastodon/Fediverse | Instances.social |

---

## Advanced Integration Examples

### Example 1: Complete Domain Investigation (OSINT Agent Skills + OSINT Bible)

**Tier 1: MCP-based (Autonomous)**
```python
# Claude Code execution
1. dns_lookup("target.com") → A, MX, TXT records
2. rdap_lookup_domain("target.com") → Registrar, admin email
3. crt_sh_search("target.com") → Subdomains, certificate history
4. shodan_internetdb(IP) → Open ports, services
5. wayback_cdx("target.com") → Historical snapshots
→ Generate report with MCP findings
```

**Tier 2: CLI-based (Human-Guided)**
```bash
# Run locally
amass enum -d target.com           # Aggressive subdomain discovery
subfinder -d target.com -o subdomains.txt  # Multi-source subdomain finder
massdns -r resolvers.txt subdomains.txt    # Parallel DNS resolution
masscan -p 1-65535 target.com              # Fast port scanning
nmap -sV -p- target.com                    # Detailed service enumeration
```

**Integration**:
1. Run MCP tools first (fast, auditable, free)
2. Export results to evidence log
3. Run CLI tools for deeper reconnaissance
4. Feed CLI results back to Claude Code for analysis & reporting

### Example 2: Threat Actor Attribution (OSINT Bible Section 28)

**Methodology**: Bellingcat 9-phase framework

**MCP Coverage**:
- Phase 1–3: Planning & collection (`dns_lookup`, `github_user_lookup`, `alienvault_otx_lookup`)
- Phase 4–7: Infrastructure & network mapping (`bgpview_asn`, `shodan_host_lookup`, `ipinfo_lookup`)
- Phase 8–9: Corroboration & challenge (manual review)

**BIBLE Supplements** (Section 33: Threat Intel Feeds):
- MISP threat feeds
- Abuse.ch malware tracking
- Shadowserver network behavior
- Mandiant/CrowdStrike research

---

## Contributing: Bridge OSINT Bible & OSINT Agent Skills

### How to Add BIBLE Coverage to Knowledge Base

**Step 1: Identify BIBLE Section**
```
Example: Section 40 (Decentralized Social OSINT) → Not fully covered
```

**Step 2: Create Mapping Document**
```
knowledge/domains/decentralized-social.md
├── Mastodon enumeration
├── Bluesky investigation
├── Nostr profile tracking
├── Cross-instance federation analysis
├── Tools: Mastodon API, instances.social, custom scripts
└── Pivot chain: Email → Mastodon handle → Associated domains
```

**Step 3: Link to MCP Tools**
```
mastodon_user_lookup (free, partial)
  → Alternative: Manual API queries
  → Supplement: BIBLE Section 40 tools
```

**Step 4: Add Pivot Playbook** (if new pivot type)
```
knowledge/pivot-playbooks/mastodon-to-identity.md
Trigger: Mastodon handle found
Steps:
  1. Query instances.social for server list
  2. Lookup user on each server via Mastodon API
  3. Extract bio, links, follow graph
  4. Identify cross-posts to Twitter, Bluesky, etc.
Output: Identity profile with confidence labels
```

**Step 5: Submit PR**

---

## OSINT Bible 2026 Roadmap Integration

### Immediate (This Quarter)

- [ ] Add `domains/critical-infrastructure.md` (Section 34)
- [ ] Add `domains/financial-investigation.md` (Section 36)
- [ ] Add `techniques/cloud-storage-osint.md` (Section 38)
- [ ] Add `domains/corporate-investigation.md` (Section 47)

### Medium-term (Next 6 Months)

- [ ] Expand `domains/decentralized-social.md` (Section 40)
- [ ] Add threat intelligence feed automation
- [ ] Integrate Satellite OSINT tools (Section 43)
- [ ] Create C2PA/SynthID verification workflows (Section 44)

### Long-term (2026+)

- [ ] Expand regional OSINT domains (Section 46)
- [ ] AI-generated content detection playbooks
- [ ] Advanced Maltego transform library
- [ ] ICS/SCADA investigation framework

---

## Key Resources

| Resource | Link | Coverage |
|---|---|---|
| OSINT Bible 2026 | https://github.com/frangelbarrera/OSINT-BIBLE | 426+ tools, 47 sections |
| OSINT Agent Skills | https://github.com/Skatetop/Omnitrix | 23 MCP tools, structured framework |
| Intelligence Cycle | https://www.nist.gov/publications | 5-phase methodology |
| ICD-203 | Classified (see unclassified analogues) | Intelligence report format |
| Bellingcat Academy | https://courses.bellingcatacademy.com | Investigation training |
| MITRE ATT&CK | https://attack.mitre.org | Threat framework |

---

## Summary

**OSINT Agent Skills** provides a rigorous, auditable, anti-hallucination framework for autonomous intelligence work.

**OSINT Bible** provides a comprehensive catalog of 426+ tools across 47 specialized domains.

**Together** they offer:
- ✅ Structured, disciplined investigations (OSINT Agent Skills)
- ✅ Complete tool coverage for deep-dive research (OSINT Bible)
- ✅ Mapped workflows for both autonomous and manual investigation
- ✅ Evidence chains and confidence labeling
- ✅ Ethical frameworks and legal guidance

**Next Step**: Point Claude Code at both resources and run a test investigation:

```
Investigate example.com using OSINT Agent Skills + OSINT Bible methodology.
Document every step. Produce a full intelligence report.
```

---

**Version**: 1.0  
**Last Updated**: 2026-07-26  
**Maintainer**: OSINT Agent Skills Contributors
