# Corporate Investigation & Due Diligence OSINT

> Comprehensive methodology for investigating companies, subsidiaries, executives, and business relationships using open-source intelligence.

---

## Investigation Framework

### Tier 1: Company Fundamentals

#### Ownership & Incorporation
- **Objective**: Identify company legal status, ownership structure, jurisdiction
- **Tools**:
  - SEC EDGAR (US public companies)
  - Companies House (UK)
  - Bundeszentralamt für Steuern (Germany)
  - SIAC (Singapore)
  - National registration databases (country-specific)
- **Evidence**: EIN/Tax ID, incorporation certificate, ownership documents

#### Executive Team
- **Objective**: Identify board members, C-level executives, beneficial owners
- **Tools**:
  - LinkedIn (employee roster, executive profiles)
  - Company website (leadership page)
  - SEC proxy statements (US public companies)
  - OpenCorporates (global company registry)
  - Crunchbase (startup executives)
- **Pivot**: Each executive → personal investigation (see `person-investigation.md`)

#### Financial Health
- **Objective**: Assess revenue, profitability, liabilities, credit risk
- **Tools**:
  - SEC EDGAR (10-K, 10-Q filings)
  - Bloomberg (subscription)
  - Reuters Eikon (subscription)
  - Yahoo Finance (free, limited)
  - Company financial statements (from website or disclosure platforms)
  - Credit rating agencies (Moody's, S&P, Fitch via subscription)
- **Analysis**: Trend revenue, identify red flags (declining profit, debt increase)

### Tier 2: Corporate Structure

#### Subsidiaries & Affiliates
- **Objective**: Map corporate family tree and shell companies
- **Tools**:
  - OpenCorporates API (global subsidiary search)
  - Bureau van Dijk (subscription)
  - Crunchbase (acquisitions, investments)
  - SEC EDGAR (ownership sections)
  - LinkedIn corporate affiliations
- **Technique**: Search by common address, shared officers, stock ownership

#### Intellectual Property
- **Objective**: Identify patents, trademarks, copyrights
- **Tools**:
  - USPTO (US patents & trademarks)
  - WIPO (international patents)
  - Google Patents (free search)
  - Patent databases (country-specific)
- **Analysis**: Technology focus, R&D investment, licensing agreements

#### Government Contracts & Sanctions
- **Objective**: Identify public contracts, sanctions designations, regulatory actions
- **Tools**:
  - SAM.gov (US government contracts)
  - OFAC (sanctions screening)
  - EU sanctions list (European Commission)
  - INTERPOL Red Notices
  - Regulatory action databases (country-specific)
  - Court records (litigation history)
- **Evidence**: Contract awards, contract values, sanctions designation notices

### Tier 3: Business Relationships

#### Customers & Suppliers
- **Objective**: Map supply chain, identify dependencies, assess risk
- **Tools**:
  - SEC filings (major customer/supplier disclosure)
  - LinkedIn sales/procurement staff
  - Government contracts (SAM.gov)
  - Company partnerships page
  - Press releases (announcements)
- **Analysis**: Revenue concentration, supply chain resilience

#### Business Partners & Joint Ventures
- **Objective**: Identify strategic partnerships, joint ventures, licensing agreements
- **Tools**:
  - Company press releases
  - SEC filings (Related Party Transactions)
  - LinkedIn business relationships
  - Industry news sources
  - Company annual reports
- **Technique**: Cross-reference officer networks, identify shared addresses

#### Financing & Investment
- **Objective**: Identify funding sources, investors, debt holders
- **Tools**:
  - Crunchbase (funding rounds, investors)
  - SEC EDGAR (equity issuances, debt filings)
  - PitchBook (subscription)
  - Press releases (funding announcements)
  - Stock exchange filings (listed companies)
- **Analysis**: Investor profile (institutional vs. individual), debt covenants

### Tier 4: Reputation & Risk

#### Litigation & Regulatory Actions
- **Objective**: Identify lawsuits, regulatory violations, settlements
- **Tools**:
  - Google Scholar (case law search)
  - PACER (US federal courts)
  - State court records (varies by state)
  - SEC EDGAR (litigation disclosures)
  - Regulatory agency databases (EPA, OSHA, etc.)
- **Evidence**: Lawsuit docket, settlement amounts, regulatory fines

#### Integrity Issues (Fraud, Misconduct)
- **Objective**: Identify fraud allegations, corruption investigations, misconduct
- **Tools**:
  - FBI press releases
  - DOJ announcements
  - News sources (specialized fraud journalism)
  - OCCRP (organized crime database)
  - Transparency International (corruption indices)
  - SEC Enforcement Actions
- **Technique**: Search officer names in sanctions databases, law enforcement records

#### Environmental & Social Compliance
- **Objective**: Assess ESG compliance, environmental violations, labor issues
- **Tools**:
  - EPA databases (environmental violations)
  - OSHA records (workplace safety)
  - SEC disclosures (ESG reporting)
  - Amnesty International (labor violations)
  - Greenpeace investigations
  - News aggregators (ESG focus)

#### Media & News Analysis
- **Objective**: Assess company reputation, identify controversies
- **Tools**:
  - Google News Alerts (real-time monitoring)
  - NewsGuard (source credibility)
  - Factiva (subscription news search)
  - LexisNexis (subscription)
  - Company press releases (official channel)
  - Social media monitoring (Twitter, LinkedIn)

### Tier 5: Digital & Technical

#### Web Infrastructure
- **Objective**: Identify hosting provider, CDN, DNS details, technology stack
- **Tools**:
  - `dns_lookup` (MCP) — DNS records
  - `rdap_lookup_domain` (MCP) — Domain registration
  - `crt_sh_search` (MCP) — SSL certificates
  - `shodan_internetdb` (MCP) — Open ports
  - Wappalyzer (technology stack)
  - BuiltWith (tech stack, plugins)
- **Analysis**: Infrastructure maturity, security posture (SSL/TLS version)

#### Domain & Email Infrastructure
- **Objective**: Identify email servers, subdomains, email security
- **Tools**:
  - `dns_lookup` (MCP) — MX, SPF, DKIM, DMARC records
  - `crt_sh_search` (MCP) — Subdomains
  - MXToolbox (email validation)
  - Hunter.io (corporate email discovery via MCP)
  - Email validation services
- **Analysis**: Email infrastructure maturity, spam reputation

#### Online Presence
- **Objective**: Identify company's digital footprint (websites, social media, etc.)
- **Tools**:
  - Google Search (branded search)
  - Social Media (LinkedIn, Twitter, Facebook, Instagram)
  - Wayback Machine (historical web pages)
  - Brand monitoring tools
  - Domain search tools (alternatives.to, similar-sites)
- **Analysis**: Brand consistency, social media engagement, digital maturity

---

## Investigation Workflows

### Workflow 1: Rapid Due Diligence (30 min)

```
1. Company fundamentals
   → SEC EDGAR (if US public)
   → Company website (basic info)
   → LinkedIn (executive team)
   
2. Red flags scan
   → SEC litigation disclosures
   → Google News search
   → OFAC sanctions check
   
3. Deliverable
   → Executive summary (Positive/Neutral/Red Flags)
   → Key risks identified
   → Recommended next investigations
```

### Workflow 2: Deep Corporate Investigation (2-4 hours)

```
1. Ownership structure
   → Incorporation documents
   → Beneficial owner analysis
   → Subsidiary mapping
   
2. Executive network mapping
   → Each officer → personal background check
   → Cross-linked positions (shared boards)
   → Family relationships (if public)
   
3. Financial analysis
   → Revenue trend (5-year)
   → Debt analysis
   → Customer concentration
   → Sector benchmarking
   
4. Risk assessment
   → Litigation history (last 10 years)
   → Regulatory actions
   → Environmental violations
   → Labor disputes
   
5. Business relationship mapping
   → Major customers
   → Major suppliers
   → Strategic partnerships
   → Investment syndicate (if funded)
   
6. Deliverable
   → Detailed corporate profile
   → Risk matrix (operational, financial, reputational, legal)
   → Recommended due diligence items (further investigation)
   → Chain of title (ownership history)
```

### Workflow 3: Supply Chain Validation

```
1. Identify company's supply chain
   → SEC filings (major supplier disclosure)
   → Company disclosures
   → News mentions
   
2. For each supplier:
   → Ownership verification (Tier 2 above)
   → Sanction screening (OFAC, EU list)
   → Litigation/regulatory history
   → Financial stability
   
3. Deliverable
   → Supply chain risk assessment
   → Concentration analysis (single-source dependencies)
   → Recommended supplier verification protocols
```

---

## Anti-Patterns & Gotchas

### ❌ Mistakes to Avoid

1. **Relying solely on LinkedIn** for executive team
   - **Reality**: LinkedIn data can be outdated or inaccurate
   - **Mitigation**: Cross-check with SEC filings, company website, news

2. **Assuming all shell companies are suspicious**
   - **Reality**: Shell companies are legal (tax optimization, IP holding, etc.)
   - **Mitigation**: Look for *patterns* of shell abuse (rapid formation/dissolution, unusual jurisdictions)

3. **Missing beneficial owner information**
   - **Reality**: Corporate registries often show nominees, not true owners
   - **Mitigation**: Check executive networks, cross-link to other entities

4. **Ignoring historical company names**
   - **Reality**: Companies rebrand, acquire, merge constantly
   - **Mitigation**: Use Wayback Machine, SEC EDGAR (name changes), news archives

5. **Over-relying on financial ratios without context**
   - **Reality**: Industry, geography, and business model all matter
   - **Mitigation**: Benchmark against sector peers; understand business model first

---

## Confidence Labeling

Apply per `methodologies/target-triangulation.md`:

- **Confirmed**: Company registration document (primary source) + corroborating article/filing
- **Probable**: SEC filing + news mention + LinkedIn profile
- **Unverified**: Single news source, no corroboration
- **Inferred**: Multiple data points logically connected (e.g., same address → shared director)

---

## Report Template

See `templates/reports/domain-profile.md` (adapt for corporate profile).

**Key sections**:
1. Company fundamentals (legal name, jurisdiction, founding date, status)
2. Ownership structure (beneficial owners, shareholding)
3. Executive team (names, roles, linked entities)
4. Financial overview (revenue, profitability, debt)
5. Risk assessment (litigation, regulatory, reputational)
6. Business relationships (major customers, suppliers, partners)
7. Sources & limitations

---

## Tools & Resources

### Free Tier (No API Key)
- SEC EDGAR (US)
- Companies House (UK)
- Google (news, patents)
- LinkedIn (basic search)
- Wayback Machine
- OpenCorporates

### Requires API Key
- Crunchbase
- PitchBook
- Factiva
- LexisNexis

### Country-Specific Registries
- **US**: Secretary of State (state-by-state)
- **UK**: Companies House
- **EU**: National registries (Belgium, Germany, etc.)
- **Singapore**: ACRA
- **Hong Kong**: Companies Registry
- **BVI**: Registry of Corporate Affairs
- **Panama**: Public Registry
- **UAE**: Ministry of Economy

---

## Legal Considerations

See `ethics/legal-frameworks.md`:
- **Public records access**: Generally unrestricted
- **Personal data**: GDPR/DPA restrictions apply to executive home addresses
- **Sanctions screening**: Required for many jurisdictions (OFAC, EU)
- **Export control**: Technology and financial due diligence may involve export restrictions

---

## Next Steps

- Completed fundamental investigation → Consider specialized deep-dive (supply chain, litigation, financial)
- Identified red flags → Escalate for human review
- Cleared due diligence → Proceed with decision

---

**See Also**:
- `domains/person-investigation.md` (for executive background checks)
- `domains/financial-investigation.md` (for detailed financial analysis)
- `methodologies/bellingcat-methodology.md` (for ownership structure mapping)
- `templates/reports/domain-profile.md` (report template)
