# Knowledge Base Index

This directory is the operational core of `osint-agent-skills`. It holds the methodology, domain knowledge, techniques, and pivot playbooks that an autonomous agent consults while running an investigation. The `system-prompt.md` at the repository root tells the agent *how to behave*; this directory tells the agent *what to do*.

## Subdirectories

### `methodologies/`
Framework-level guidance. These files define the analytical models an agent applies to raw findings: the five-phase Intelligence Cycle, the Cyber Kill Chain, MITRE ATT&CK mapping, the Bellingcat open-source investigation methodology, target triangulation, and source verification. Consult these when planning an investigation, when deciding how to characterize findings, and when resolving conflicting signals.

**Files**:
- `intelligence-cycle.md` — Five-phase OSINT investigation framework
- `bellingcat-methodology.md` — Attribution investigation (9 phases)
- `cyber-kill-chain.md` — Threat-centric investigation model
- `mitre-attack-mapping.md` — ATT&CK framework correlation
- `source-verification.md` — Evidence credibility assessment
- `target-triangulation.md` — Confidence labeling & corroboration
- `structured-analytic-techniques.md` — Analytical reasoning techniques

### `domains/`
Subject-specific deep dives. One file per investigative domain — person, domain, IP, company, phone, cryptocurrency, social media, breach data, dark web, GEOINT, corporate investigation, financial investigation, and critical infrastructure. Each file lists the canonical sources for that domain, the expected data shapes, and the cross-domain pivots that frequently pay off. Consult the relevant domain file before collecting on a new subject type.

**Core Domains**:
- `person-investigation.md` — Individual backgrounds, social networks, assets
- `domain-investigation.md` — Websites, DNS, registrars, hosting
- `ip-investigation.md` — IP geolocation, ASN, routing, services
- `company-investigation.md` — Corporate structure, ownership, executives
- `phone-investigation.md` — Phone number tracking, reverse lookup
- `cryptocurrency.md` — Blockchain transaction tracing
- `social-media.md` — Cross-platform account enumeration
- `breach-data.md` — Breach database searching, credential validation
- `dark-web.md` — Tor, I2P, marketplace reconnaissance
- `geoint.md` — Geolocation, satellite imagery, mapping
- `threat-actors.md` — Attribution, APT research, threat actor profiles
- `vehicle.md` — Vehicle registration, tracking, ownership

**2026 Expansion Domains** (OSINT Bible integration):
- `corporate-investigation.md` — Due diligence, subsidiary mapping, financial analysis
- `financial-investigation.md` — Asset tracing, beneficial ownership, money laundering detection
- `critical-infrastructure.md` — ICS/SCADA discovery, vulnerability assessment

### `techniques/`
Single-purpose techniques — Google dorks, username enumeration, email pivoting, metadata extraction, Wayback lookups, Certificate Transparency log analysis, DNS reconnaissance, Shodan queries, facial recognition, and reverse image search. Each technique file documents the trigger, the procedure, the tool, and the failure modes. Consult these when a playbook step references a technique by name.

**Files**:
- `google-dorks.md` — Advanced search operators & dork patterns
- `username-enumeration.md` — Cross-platform username discovery
- `email-pivoting.md` — Email-based chain investigations
- `metadata-extraction.md` — EXIF, PDF, document metadata analysis
- `wayback-investigation.md` — Internet Archive CDX queries & analysis
- `certificate-transparency.md` — CT log searching & subdomain discovery
- `dns-recon.md` — DNS enumeration, zone transfer, query analysis
- `shodan-techniques.md` — Shodan filters, ICS queries, banner analysis
- `facial-recognition.md` — Ethical considerations & tool usage
- `reverse-image-search.md` — Geolocation & identity verification
- `graph-generation.md` — Network visualization, relationship mapping

### `pivot-playbooks/`
The canonical chains that turn one finding into a network. Each playbook specifies a trigger, ordered steps, anti-patterns, and output format. The agent follows these by default unless the user constrains scope. Consult these whenever a new artifact is discovered — the playbook tells the agent what to do next.

**Pivot Chains**:
- `email-to-username.md` — Email → Social media accounts, usernames
- `username-to-identity.md` — Username → Real name, profiles, associates
- `domain-to-infrastructure.md` — Domain → IPs, ASN, hosting provider
- `ip-to-attribution.md` — IP → ISP, country, threat intelligence
- `breach-to-credentials.md` — Breach email → Associated passwords, other breaches
- `phone-to-person.md` — Phone number → Carrier, location, associated person
- `crypto-to-fiat.md` — Cryptocurrency wallet → Exchange, KYC, fiat linkage
- `photo-to-location.md` — Photo/image → Geolocation, landmark identification
- `metadata-to-attribution.md` — Document metadata → Author, creation details, devices

## How an agent should consult this directory

Treat the four subdirectories as different layers of abstraction. `methodologies/` answers "how do I think about this problem?" `domains/` answers "what does this subject class look like?" `techniques/` answers "how do I execute this one step?" `pivot-playbooks/` answers "given finding X, what should I do next?" When in doubt, the system prompt's KNOWLEDGE BASE REFERENCES section routes each question type to the correct subdirectory.

## Suggested reading order for a new agent

1. `methodologies/intelligence-cycle.md` — the operating rhythm.
2. `methodologies/source-verification.md` and `methodologies/target-triangulation.md` — how to weigh evidence.
3. `methodologies/bellingcat-methodology.md` — verification-first mindset for attribution work.
4. `methodologies/cyber-kill-chain.md` and `methodologies/mitre-attack-mapping.md` — for threat-intelligence products.
5. Skim every file in `pivot-playbooks/` to know the canonical chains by name.
6. Skim every file in `domains/` to know what each subject class yields.
7. Consult `techniques/` on demand when a playbook step references one.

After this pass, an agent has the conceptual map. The directories are then consulted selectively during each investigation, not reread in full.

---

## OSINT Bible Integration

**See also**: `osint-bible-integration.md` (complete mapping of OSINT Bible 426+ tools to OSINT Agent Skills framework)

This knowledge base is built on the foundation of the **OSINT Bible** (https://github.com/frangelbarrera/OSINT-BIBLE) — a comprehensive catalog of 426+ OSINT tools and techniques across 47 specialized domains.

### Two-Tier OSINT Strategy

**Tier 1: Autonomous (OSINT Agent Skills)**
- 23 MCP tools deployed as callable functions
- Anti-hallucination constraints, evidence logging, confidence labeling
- Structured reports with audit trails
- No API keys required (free tier tools)
- Ideal for: Auditable, repeatable, cloud-native investigations

**Tier 2: Comprehensive (OSINT Bible + CLI)**
- 426+ tools across 47 domains (domains.py, methodologies, and beyond)
- Specialized tool chains (SpiderFoot, Recon-ng, Maltego, etc.)
- Human-guided investigations with deep specialization
- Ideal for: Complex, multi-tool investigations requiring expertise

### Integration Examples

**Domain Investigation** (OSINT Agent Skills + OSINT Bible):
1. Use MCP tools first (fast, free, auditable) — `dns_lookup`, `crt_sh_search`, `shodan_internetdb`
2. Export results to evidence log
3. Consult OSINT Bible Section 7 (Domain/IP/DNS) for 30+ additional tools
4. Run CLI tools locally (Amass, DNSDumpster, SecurityTrails) for deeper reconnaissance
5. Feed results back to Claude Code for analysis & reporting

**Threat Actor Attribution** (Bellingcat methodology + MITRE ATT&CK):
1. Use MCP tools for infrastructure mapping — `bgpview_asn`, `ipinfo_lookup`, `alienvault_otx_lookup`
2. Apply Bellingcat 9-phase framework (`methodologies/bellingcat-methodology.md`)
3. Correlate to MITRE ATT&CK techniques (`methodologies/mitre-attack-mapping.md`)
4. Consult OSINT Bible Section 33 (Threat Intelligence Feeds) for advanced threat intel

### OSINT Bible Section Coverage

| Section | Coverage | Location |
|---------|----------|----------|
| 1. Fundamentals | ✅ Complete | `methodologies/intelligence-cycle.md` |
| 2. 4-Step Methodology | ✅ Complete | `methodologies/intelligence-cycle.md` (5-phase variant) |
| 4. Internet Search | ✅ Mapped | `techniques/google-dorks.md` + MCP tools |
| 5–7. Social/GEOINT/Domain | ✅ Complete | `domains/` + `pivot-playbooks/` |
| 11. Legal Considerations | ✅ Complete | See root `ethics/legal-frameworks.md` |
| 28. Professional Methodologies | ✅ Complete | `methodologies/` (ICD-203, Bellingcat, ATT&CK) |
| 33. Threat Intel Feeds | ✅ Mapped | MCP: `alienvault_otx_lookup`, `virustotal_domain_report` |
| 34. ICS/Critical Infrastructure | ✅ New | `domains/critical-infrastructure.md` (2026) |
| 36. Financial OSINT | ✅ New | `domains/financial-investigation.md` (2026) |
| 47. Corporate OSINT | ✅ New | `domains/corporate-investigation.md` (2026) |
| **All Others** | 🟡 Referenced | See `osint-bible-integration.md` for detailed mapping |

### Quick Reference: Domain → OSINT Bible Section Mapping

- `domains/person-investigation.md` ← OSINT Bible Section 31
- `domains/company-investigation.md` ← OSINT Bible Section 32
- `domains/corporate-investigation.md` ← OSINT Bible Section 47
- `domains/financial-investigation.md` ← OSINT Bible Section 36
- `domains/critical-infrastructure.md` ← OSINT Bible Section 34
- `domains/cryptocurrency.md` ← OSINT Bible Section 17
- `domains/breach-data.md` ← OSINT Bible Section 16
- `domains/dark-web.md` ← OSINT Bible Section 25
- `techniques/google-dorks.md` ← OSINT Bible Sections 4, 29

---

## How to Extend This Knowledge Base

### Adding a New Domain

1. Create `domains/[domain-name].md` following the standard template:
   - **Investigation Framework** (Tier 1–5 workflow)
   - **Investigation Workflows** (5-30 min, 2-4 hour examples)
   - **Anti-Patterns & Gotchas** (common mistakes)
   - **Confidence Labeling** (per `target-triangulation.md`)
   - **Report Template** (cross-reference existing)
   - **Tools & Resources** (free tier vs. subscription)
   - **Legal & Ethical** (reference `ethics/legal-frameworks.md`)

2. Link from relevant `pivot-playbooks/` if new pivot chain
3. Update this README (add to Domains list above)
4. Submit PR with examples

### Adding a New Pivot Playbook

1. Identify trigger: "When the agent finds X..."
2. Create `pivot-playbooks/[x]-to-[y].md` with:
   - **Trigger** — exact finding type
   - **Steps** — ordered collection actions (tool, expected output)
   - **Anti-Patterns** — what NOT to do
   - **Output Format** — how to report results
   - **Confidence Criteria** — per `target-triangulation.md`

3. Link from relevant domain files
4. Reference in `system-prompt.md` (if major)
5. Submit PR with examples

### Contributing OSINT Bible Tool Mappings

1. Identify OSINT Bible section (e.g., Section 34: ICS/SCADA)
2. Check if coverage exists (see table above)
3. If missing, create new domain or technique file
4. Map tools to MCP equivalents (see `osint-bible-integration.md`)
5. Add to integration document's coverage table
6. Submit PR

---

## See Also

- **Root directory**: `system-prompt.md` (agent persona), `CLAUDE.md` (setup guide)
- **OSINT Bible**: https://github.com/frangelbarrera/OSINT-BIBLE (426+ tools, 47 sections)
- **OSINT Bible Integration**: `osint-bible-integration.md` (complete mapping, workflows, examples)
- **Ethics & Legal**: See root `ethics/` directory (legal frameworks, anti-hallucination rules, code of conduct)
- **Templates**: See root `templates/` directory (report formats, evidence logs)
- **Examples**: See root `examples/` directory (worked investigations)

---

**Version**: 1.4.1  
**Last Updated**: 2026-07-26  
**Maintainer**: OSINT Agent Skills Contributors
