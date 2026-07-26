# Critical Infrastructure OSINT (ICS/OT/SCADA)

> Investigate industrial control systems, critical infrastructure vulnerabilities, and operational technology using open-source intelligence.

---

## Investigation Framework

### Tier 1: Infrastructure Discovery

#### SCADA/ICS Identification
- **Objective**: Locate exposed industrial control systems, PLCs, HMIs
- **Tools**:
  - `shodan_internetdb` (MCP) — Free Shodan search for ICS fingerprints
  - Shodan ICS filters (requires API key):
    - `port:502` — Modbus (PLC protocol)
    - `port:503` — Modbus over TCP
    - `port:20000` — Enrich (Wonderware SCADA)
    - `port:44818` — EtherNet/IP
    - `port:5000` — GE Automation
    - `port:9200` — Elasticsearch (often exposed)
  - Censys ICS scanning (certificate-based discovery)
  - Google Dorks:
    - `intitle:"SCADA" OR "PLC" OR "HMI"`
    - `inurl:cgi-bin/admin.cgi "login"`
    - `filetype:csv "modbus" OR "profinet"`
  
- **Output**: List of exposed systems, software versions, default credentials observed

#### Network & Facility Discovery
- **Objective**: Map critical infrastructure facilities (power plants, water treatment, etc.)
- **Tools**:
  - Google Maps (facility location, satellite imagery)
  - Wikidata (infrastructure data)
  - OpenStreetMap (power lines, substations, pipelines)
  - Public utility websites (outage maps, planned maintenance)
  - Property records (facility ownership)
  - News sources (facility announcements, incidents)
- **Technique**: Identify facility by name, location, operator
- **Output**: Facility map, approximate coordinates, operator identity

#### Network Topology
- **Objective**: Infer network architecture (segmentation, Internet connectivity)
- **Tools**:
  - `dns_lookup` (MCP) — Resolve infrastructure domain names
  - `bgpview_asn` (MCP) — Identify ASN/routing
  - `rdap_lookup_ip` (MCP) — IP ownership
  - nmap (network scanning, if authorized)
  - Traceroute (path analysis)
  - RIPE/Shadowserver data (network operators, abuse contacts)
- **Analysis**: Determine if systems are air-gapped or Internet-connected
- **Output**: Network diagram, connectivity assessment

### Tier 2: Vulnerability & Security Posture

#### Known Vulnerabilities (CVEs)
- **Objective**: Identify CVEs affecting discovered systems
- **Tools**:
  - `virustotal_domain_report` (MCP) — Malware checks
  - NVD (National Vulnerability Database) — CVE search
  - ICS-CERT (US CISA) — ICS-specific advisories
  - MITRE ATT&CK (ICS-specific techniques)
  - Vendor advisory databases (Siemens, GE, ABB, Honeywell)
- **Technique**: Match system version to known CVE database
- **Output**: CVE list, CVSS scores, proof-of-concept availability

#### Weak Default Configuration
- **Objective**: Identify systems with default credentials, weak auth
- **Red flags**:
  - Telnet ports open (no encryption)
  - Default usernames (admin, operator, service)
  - Blank or simple passwords (123456, password)
  - No authentication enabled
  - Unencrypted protocols (HTTP, Modbus plain)
- **Tools**:
  - Shodan (search results show auth status)
  - Public documentation (default credentials often documented)
  - Community forums (users asking about defaults)
- **Output**: Weak auth registry, risk assessment

#### Firmware & Software Analysis
- **Objective**: Identify outdated/unsupported software versions
- **Tools**:
  - Vendor documentation (end-of-life dates)
  - CVE databases (filter by software/version)
  - Web archives (historical version announcements)
  - News sources (vendor security updates)
- **Output**: Software inventory, support status, patch availability

### Tier 3: Operational Data

#### Maintenance Schedules & Outages
- **Objective**: Infer critical infrastructure operations, maintenance windows
- **Tools**:
  - Public utility websites (outage maps, notices)
  - News sources (planned maintenance announcements)
  - Social media (utility account posts, customer complaints)
  - NORAD (satellite imagery for power generation capacity)
  - USGS (water level, hydroelectric data)
  - National Weather Service (facility impact from weather)
- **Analysis**: Identify critical systems, maintenance patterns, resilience capabilities
- **Output**: Operational timeline, facility criticality assessment

#### Staffing & Access Control
- **Objective**: Identify key personnel, access patterns, shift schedules
- **Tools**:
  - LinkedIn (employee directory for facility/company)
  - Company website (organizational chart, key contacts)
  - News sources (promotions, personnel changes)
  - Public records (property access, security clearances, if available)
- **Output**: Personnel roster, estimated facility staffing, access control inference

#### Third-Party Dependencies
- **Objective**: Identify contractors, vendors, system integrators
- **Tools**:
  - Company website (vendor partnerships, system integrators)
  - News sources (contract awards, partnerships)
  - LinkedIn (contractor employees working on-site)
  - Corporate filings (vendor relationships disclosed)
- **Analysis**: Assess supply chain risk, identify single-points-of-failure
- **Output**: Vendor roster, dependency assessment

### Tier 4: Attack Surface Analysis

#### ICS-Specific Attack Vectors
- **Objective**: Assess potential attack paths (cyber-physical)
- **MITRE ATT&CK ICS Framework**:
  - **Reconnaissance**: Network reconnaissance, environment mapping (covered above)
  - **Resource Development**: Command & control infrastructure, malware staging
  - **Initial Access**: Supply chain compromise, phishing, default credentials
  - **Execution**: Malware execution, lateral movement
  - **Persistence**: Firmware modification, persistence mechanisms
  - **Privilege Escalation**: Exploit vulnerable processes
  - **Defense Evasion**: Disable logging, modify firewall rules
  - **Credential Access**: Credential dumping, default account exploitation
  - **Discovery**: Network discovery, environment mapping
  - **Lateral Movement**: Network segmentation bypass, protocol exploitation
  - **Collection**: HMI/SCADA data exfiltration, sensor data collection
  - **Exfiltration**: Data exfiltration over network
  - **Impact**: Denial of service, physical damage to equipment, process disruption

- **Output**: Attack chain analysis, threat scenarios

#### Supply Chain OSINT
- **Objective**: Identify malware/backdoor risk in software/hardware supply chain
- **Tools**:
  - Vendor advisory databases (security patches, patches)
  - News sources (supply chain compromises: SolarWinds, Kaseya, etc.)
  - Software repository scanning (GitHub code audits)
  - Community threat intel (security researchers, threat feeds)
- **Output**: Supply chain risk assessment, vendor trustworthiness

### Tier 5: Geopolitical & Threat Intelligence

#### Nation-State Interest
- **Objective**: Assess likelihood of state-sponsored targeting
- **Indicators**:
  - Strategic infrastructure (power generation, water treatment, nuclear)
  - Geopolitical significance (border regions, resource extraction)
  - Historical targeting (APT activity, previous incidents)
- **Tools**:
  - CISA alerts (nation-state targeting notices)
  - Threat intel reports (APT-specific targeting patterns)
  - News sources (geopolitical tensions, military exercises)
- **Output**: State-sponsored threat likelihood, relevant APT groups

#### Active Threat Monitoring
- **Objective**: Detect active exploitation attempts against infrastructure
- **Tools**:
  - CISA Alerts (real-time ICS advisories)
  - Shadowserver (abuse notifications for exposed systems)
  - URLhaus (malware tracking)
  - MalwareBazaar (malware sample tracking)
  - threat intel feeds (dark web monitoring, threat actor tracking)
- **Output**: Active threat summary, exploit-in-the-wild status

---

## Investigation Workflows

### Workflow 1: Critical Infrastructure Reconnaissance (30-45 min)

```
1. Facility identification
   → Company name, location, operator
   → Facility type (power, water, gas, etc.)
   
2. Network discovery
   → dns_lookup (domain names)
   → bgpview_asn (ASN, routing)
   → Shodan search (exposed systems, versions)
   
3. Vulnerability scan
   → Match versions to CVE database
   → Identify known exploits
   
4. Deliverable
   → Facility summary (location, operator, type)
   → Exposed systems list (count, types, versions)
   → Critical vulnerabilities identified (count, CVSS)
   → Recommended assessment (requires human security review)
```

### Workflow 2: SCADA Security Assessment (2-4 hours)

```
1. Network mapping
   → Identify all connected systems
   → Map protocols (Modbus, Profibus, EtherNet/IP)
   → Assess segmentation (Internet-connected vs. air-gapped)
   
2. Vulnerability analysis
   → Enumerate installed software/firmware
   → Cross-check against CVE database
   → Identify missing patches
   
3. Configuration audit
   → Default credentials detected? (Shodan results)
   → Authentication enabled? (protocol analysis)
   → Encryption in use? (TLS versions)
   
4. Threat modeling
   → Identify critical assets (generators, control valves, etc.)
   → Assess attack paths (initial access → impact)
   → Evaluate impact (safety, availability, confidentiality)
   
5. Deliverable
   → Security assessment report
   → Vulnerability inventory (prioritized)
   → Configuration audit (compliance with standards)
   → Threat model (scenario analysis)
```

### Workflow 3: Supply Chain Risk Assessment

```
1. Identify vendors & integrators
   → System integrators
   → Software providers
   → Hardware vendors
   
2. Assess vendor risk
   → Known breaches/compromises?
   → Security practices (certification, audits)?
   → Geographic origin (foreign interference risk)?
   
3. Evaluate software supply chain
   → Open-source components (known vulnerabilities)?
   → Compiler/build chain trust?
   → Firmware update mechanisms?
   
4. Deliverable
   → Vendor risk matrix
   → Supply chain dependency map
   → Recommendations (vendor due diligence, monitoring)
```

---

## Anti-Patterns & Gotchas

### ❌ Mistakes to Avoid

1. **Assuming all Shodan hits are exploitable**
   - **Reality**: Exposed != Exploitable. May be test systems, isolated networks, honeypots
   - **Mitigation**: Cross-check with vendor documentation, verify accessibility

2. **Over-weighting single CVE**
   - **Reality**: Old systems may have many CVEs, but defense-in-depth may mitigate
   - **Mitigation**: Assess overall security posture, not individual CVEs

3. **Ignoring air-gap defenses**
   - **Reality**: Systems may be physically isolated from Internet
   - **Mitigation**: Verify connectivity; assume systems may be segmented

4. **Assuming critical infrastructure is always well-protected**
   - **Reality**: Legacy systems, budget constraints, insider threats persist
   - **Mitigation**: Conduct thorough assessment regardless of assumed maturity

5. **Missing proprietary protocol analysis**
   - **Reality**: Industrial protocols (Profibus, Modbus) are non-standard
   - **Mitigation**: Research protocol documentation, identify protocol vulnerabilities

---

## Confidence Labeling

Apply per `methodologies/target-triangulation.md`:

- **Confirmed**: Shodan hit + banner confirmation + CVE match
- **Probable**: DNS record + routing data + known vendor patterns
- **Unverified**: Single source (Shodan only, no verification)
- **Inferred**: Facility location + inferred systems based on industry norms
- **Speculative**: Theoretical vulnerability (CVE exists, but not confirmed present)

---

## Report Template

See `templates/reports/threat-assessment.md` (adapt for infrastructure assessment).

**Key sections**:
1. Executive summary (facility type, critical systems, key risks)
2. Asset inventory (systems, versions, connectivity)
3. Vulnerability assessment (CVE list, exploitability)
4. Configuration audit (weak auth, default creds, encryption)
5. Threat modeling (attack scenarios, impact assessment)
6. Supply chain risk (vendor assessment, software dependencies)
7. Recommendations (patches, architecture changes, monitoring)
8. Sources & confidence levels

---

## Tools & Resources

### Free Tier (No Subscription)
- Shodan (limited free queries, but ICS-specific)
- NVD (National Vulnerability Database)
- CISA (US Cybersecurity & Infrastructure Security Agency)
- MITRE ATT&CK (ICS framework)
- ICS-CERT (vendor advisories)
- Google (news, facility information)

### Requires API Key/Subscription
- Shodan (full API access, ICS filters)
- Censys (ICS scanning)
- Threat intel feeds (custom monitoring)
- Exploit database subscriptions (zero-day research)

### Government/Academic Databases
- CISA Alerts (free)
- FIRST.org (incident response information)
- NIST (critical infrastructure standards)
- IEEE (ICS standards, research)

### Vendor Security Resources
- Siemens (CERT-Siemens advisories)
- GE Digital (advisories)
- ABB (advisories)
- Honeywell (advisories)
- Rockwell Automation (advisories)

---

## Legal & Ethical Considerations

See `ethics/legal-frameworks.md`:
- **Public OSINT only**: Do not attempt to access systems without authorization
- **CFAA implications**: Unauthorized access to control systems is serious federal crime
- **Reporting responsibility**: If critical vulnerabilities found, report to facility/CISA
- **Critical infrastructure protection**: CISA has authority to issue protective orders

### Responsible Disclosure
- Identify vulnerability
- Report to facility/vendor (not public)
- Allow 45-90 day remediation window
- Disclose to CISA/appropriate authorities
- Publish after patch available

---

## Related Domains

- `domains/threat-actors.md` (nation-state targeting of infrastructure)
- `methodologies/mitre-attack-mapping.md` (ICS-specific techniques)
- `pivot-playbooks/domain-to-infrastructure.md` (infrastructure mapping)

---

**See Also**:
- CISA (https://www.cisa.gov/ics) — US critical infrastructure agency
- ICS-CERT Advisories (https://www.cisa.gov/ics-advisories)
- MITRE ATT&CK ICS (https://attack.mitre.org/matrices/ics/)
- NIST Cybersecurity Framework (https://www.nist.gov/cyberframework)
