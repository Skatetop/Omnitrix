# Financial OSINT & Money Laundering Investigation

> Investigate financial transactions, assets, beneficial ownership, and detect money laundering patterns using open-source intelligence.

---

## Investigation Framework

### Tier 1: Asset Tracing

#### Real Property (Real Estate)
- **Objective**: Identify properties owned by subject, assess portfolio value, detect shell ownership
- **Tools**:
  - County assessor records (US, by county)
  - Zillow, Redfin (listing history, valuation)
  - LoopNet (commercial real estate)
  - OpenData portals (European countries)
  - Company registries (property held by entities)
  - Deed records (state/local)
- **Technique**: Search by owner name, address history, corporate ownership
- **Red flags**: Property purchased through shell company, rapid turnover, price inflation

#### Vehicles & Vessels
- **Objective**: Identify registered vehicles/boats, detect patterns of movement/transit
- **Tools**:
  - DMV records (state-specific, limited public access)
  - MarineTraffic (vessel tracking)
  - FlightAware, FlightRadar24 (aircraft)
  - Port authority records (commercial shipping)
  - Customs records (import/export, if accessible)
- **Technique**: Identify transportation used in commerce, detect smuggling patterns
- **Analysis**: Vessel registration flags, beneficial owner opacity

#### Luxury Items & Collections
- **Objective**: Identify art, jewelry, watches, collectibles indicating wealth
- **Tools**:
  - Auction house databases (Christie's, Sotheby's archives)
  - Art market databases (Artnet, Askart)
  - News sources (society events, art acquisitions)
  - Instagram/social media (owners often post acquisitions)
  - Museum collection databases (if donor identified)
- **Technique**: Track acquisitions over time, identify price patterns (asset inflation)

### Tier 2: Account & Transaction Analysis

#### Bank Accounts & Financial Services
- **Objective**: Identify bank accounts, credit cards, payment processors
- **Tools**:
  - Corporate filings (banks/financial institutions disclosed)
  - FinCEN alerts (public money laundering alerts)
  - News sources (account freezes, sanctions compliance)
  - Company disclosures (banking relationships)
  - OFAC screening (sanctions designation)
- **Limitation**: Direct account information is confidential; rely on indirect evidence
- **Technique**: Infer bank relationships from transaction patterns, check sanctions lists

#### Cryptocurrency Transactions
- **Objective**: Trace cryptocurrency wallets, identify exchange linkages, detect mixing/laundering
- **Tools**:
  - `blockchain_address_lookup` (MCP) — Bitcoin transaction tracing
  - `etherscan_address_lookup` (MCP) — Ethereum transaction tracing
  - Blockchain.com (Bitcoin exchange watch)
  - Etherscan (Ethereum analytics)
  - Chainalysis (subscription, professional tracking)
  - CipherBlade (mixing detection)
  - Santiment (crypto flow analysis)
- **Technique**: Follow transaction chains, identify exchange deposit/withdrawal patterns
- **Anti-laundering**: Detect mixing services, identify tumbler usage
- **Output**: Transaction graph, exchange linkage, profit/loss analysis

#### Wire Transfers & Remittances
- **Objective**: Identify patterns of international fund movement
- **Tools**:
  - SWIFT database (international bank codes)
  - Financial filings (material transactions disclosed)
  - FinCEN reports (currency structuring, large transaction reports)
  - News sources (cross-border transactions announced)
  - Central bank data (international transaction flows)
- **Limitation**: Details confidential; inferred from public data only
- **Technique**: Correlate timing, amounts, and parties across disclosed transactions

### Tier 3: Business & Entity Investigations

#### Income & Revenue Sources
- **Objective**: Trace subject's claimed income, verify legitimacy
- **Tools**:
  - SEC filings (dividend income, investment returns)
  - Tax court records (dispute history)
  - Business registration (ownership of companies)
  - LinkedIn (employment history)
  - Patent/copyright income (royalties, licensing)
  - Real estate records (rental income implied)
- **Analysis**: Compare claimed income to documented sources; identify gaps

#### Corporate Financial Health
- **Objective**: Assess viability of business as front for money laundering
- **Tools**:
  - SEC EDGAR (public company filings)
  - Business bureau reports (ratings, complaints)
  - Credit rating agencies
  - Industry financial benchmarks
  - News sources (market conditions, profitability)
  - Supplier/customer relationship data
- **Red flags**: Unprofitable business, inflated revenue, high cash transactions (retail, restaurants)

#### Beneficial Ownership
- **Objective**: Trace true owners through shell companies and proxies
- **Tools**:
  - OpenCorporates (corporate registry)
  - Corporate filings (ultimate beneficial owner disclosures)
  - Officer network analysis (shared directors across entities)
  - Address clustering (companies at same address)
  - News sources (ownership announcements)
  - Sanctions databases (linked entity discovery)
- **Technique**: Build network graph of interconnected entities, identify patterns
- **Analysis**: Ownership chains, nominee detection, beneficial owner inference

### Tier 4: Sanctions & Compliance Screening

#### OFAC Sanctions Designation
- **Objective**: Verify subject/entities against US Treasury sanctions lists
- **Tools**:
  - OFAC SDN list (Specially Designated Nationals)
  - BIS Entity List (Commerce Department export controls)
  - State Department terrorist designations
  - INTERPOL Red Notices
  - Debarred contractors lists (GSA)
- **Process**: Screen against all relevant lists; check historical designations
- **Output**: Sanctions match (yes/no), designation criteria, linked entities

#### EU & International Sanctions
- **Objective**: Screen against European and international sanctions regimes
- **Tools**:
  - EU sanctions list (European Commission)
  - UN Security Council sanctions lists
  - UK sanctions list (post-Brexit)
  - Australia/Canada sanctions lists
  - Financial Action Task Force (FATF) blacklist
- **Technique**: Multi-jurisdictional screening, name variant search

#### AML/KYC Compliance
- **Objective**: Assess subject's AML/KYC profile, identify red flags
- **Tools**:
  - Corporate filings (AML policies disclosed)
  - Regulatory actions (AML violation records)
  - FinCEN reports (Currency Transaction Reports, Suspicious Activity Reports)
  - News sources (compliance violations, fines)
  - Due diligence firm reports (if publicly available)

### Tier 5: Money Laundering Detection

#### Transaction Pattern Analysis
- **Objective**: Identify money laundering techniques (placement, layering, integration)
- **Patterns to detect**:
  - **Structuring**: Multiple small transactions below reporting threshold
  - **Smurfing**: Multiple people making similar transactions (coordinated)
  - **Trade-based**: Over/under-invoicing of imports (disguised transfer)
  - **Cash-intensive**: Retail/hospitality with inflated revenue
  - **Rapid turnover**: Real estate or vehicles purchased/sold quickly at profit
  - **Mixing**: Legitimate + illicit funds combined
  - **Ripple effect**: Suspicious transactions rippling across multiple entities

#### Cash Flow Analysis
- **Objective**: Compare claimed income to observable assets/spending
- **Technique**: Build timeline of major transactions, correlate to known income
- **Red flags**: 
  - Assets exceed documented income
  - Large purchases financed through undocumented sources
  - Cash deposits without corresponding business income
  - Luxury spending inconsistent with salary

#### Trade Finance Manipulation
- **Objective**: Detect over/under-invoicing, phantom shipments
- **Tools**:
  - Customs data (if public)
  - Shipping databases (cargo tracking)
  - Port authority records (manifests, if accessible)
  - Trade finance news (major deals)
  - Corporate financial filings (goods sold vs. cash received)
- **Technique**: Cross-check invoice amounts against market prices, shipping records
- **Example**: Company imports cotton at $10/kg (market price $2/kg) = suspicious transfer pricing

---

## Investigation Workflows

### Workflow 1: Sanctions Screening (15 min)

```
1. Gather identifying information
   → Full legal name, alternate names, DOB, passport, address
   
2. Screen against lists
   → OFAC SDN list (US)
   → EU sanctions list (if Europe-relevant)
   → BIS Entity List (export controls)
   → UN Security Council lists
   → INTERPOL Red Notices
   
3. Deliverable
   → Match found? → YES/NO with citations
   → If match: Designation authority, effective date, linked entities
   → Recommended action (escalate if match)
```

### Workflow 2: Beneficial Owner Tracing (1-2 hours)

```
1. Identify company/entities
   → Subject's ownership stake
   → Corporate structure (holding companies, subsidiaries)
   
2. Build network graph
   → Each entity → owner/officers
   → Cross-link shared officers (other entities they control)
   → Trace to natural persons (ultimate beneficial owners)
   
3. Analyze ownership layers
   → Direct ownership
   → Indirect ownership (through holding companies)
   → Nominee detection (same officer across multiple entities)
   → Circular ownership (A owns B, B owns A)
   
4. Deliverable
   → Ownership structure diagram
   → Beneficial owner identification (with confidence level)
   → Red flags (opacity, nominee usage, unusual jurisdiction)
```

### Workflow 3: Money Laundering Risk Assessment (2-4 hours)

```
1. Asset mapping
   → Real property owned
   → Vehicles registered
   → Corporate assets (via filings)
   → Cryptocurrency holdings (if public)
   
2. Income analysis
   → Documented employment/business income
   → Investment returns (from filings)
   → Other claimed sources
   → Total: Does it explain assets?
   
3. Transaction timeline
   → Major asset acquisitions (date, price, source)
   → Significant transfers (timing, amounts)
   → Pattern analysis (structuring, smurfing?)
   
4. Red flag assessment
   → Assets exceed income? → RED
   → Cash-intensive business? → ORANGE
   → Rapid property turnover? → ORANGE
   → High-risk jurisdictions? → RED
   → Cryptocurrency mixing detected? → RED
   → Sanctions matches? → RED
   
5. Deliverable
   → AML Risk Assessment (Low/Medium/High)
   → Key risk factors identified
   → Recommended escalation (if High risk)
   → Further investigation items
```

### Workflow 4: Cryptocurrency Transaction Tracing

```
1. Identify wallet addresses
   → Subject's known wallets
   → Exchange deposit/withdrawal addresses
   
2. Trace transaction chains
   → `blockchain_address_lookup` or `etherscan_address_lookup` (MCP)
   → Track movement across addresses
   → Identify exchange linkage (exchange deposit = know-your-customer data)
   
3. Analyze flow
   → Inbound transactions (source of funds)
   → Outbound transactions (destination of funds)
   → Mixing detection (sudden address changes)
   → Value analysis (amount, timing)
   
4. Deliverable
   → Transaction graph (visual or tabular)
   → Exchange linkage identified (if applicable)
   → Mixing detection results
   → Confidence assessment per `target-triangulation.md`
```

---

## Anti-Patterns & Gotchas

### ❌ Mistakes to Avoid

1. **Assuming all high-value transactions are suspicious**
   - **Reality**: Wealthy individuals and corporations routinely move large sums
   - **Mitigation**: Look for *patterns* that deviate from known business model

2. **Confusing asset value with suspicious activity**
   - **Reality**: Luxury assets are legal (expensive watches, art, etc.)
   - **Mitigation**: Focus on *unexplained* wealth, not wealth itself

3. **Over-weighting cryptocurrency involvement**
   - **Reality**: Cryptocurrency is increasingly mainstream
   - **Mitigation**: Focus on *unusual patterns* (mixing, rapid conversions) not use itself

4. **Ignoring legitimate business explanations**
   - **Example**: Real estate developer with high property turnover is normal
   - **Mitigation**: Benchmark transaction frequency against industry norms

5. **Single-source assumptions**
   - **Reality**: One transaction alone is not suspicious
   - **Mitigation**: Look for *clusters* of behavior over time

---

## Confidence Labeling

Apply per `methodologies/target-triangulation.md`:

- **Confirmed**: Beneficial owner in corporate registry + corroborating sanctions match
- **Probable**: Corporate chain traced to principal + news confirmation
- **Unverified**: Ownership suspected but no official record
- **Inferred**: Multiple financial transactions suggest beneficial ownership
- **Speculative**: Circumstantial evidence only

---

## Report Template

See `templates/reports/threat-assessment.md` (adapt for financial risk assessment).

**Key sections**:
1. Subject identification (name, DOB, nationality, aliases)
2. Beneficial ownership (entities controlled, ownership chain)
3. Asset inventory (real property, vehicles, cryptocurrency, corporate assets)
4. Income analysis (documented sources vs. observed assets)
5. Transaction summary (major movements, timing, counterparties)
6. AML/KYC assessment (sanctions screening, red flags)
7. Money laundering risk (overall risk rating, justification)
8. Sources & confidence levels
9. Recommended next steps (escalation, further investigation)

---

## Tools & Resources

### Free Tier (No Subscription)
- OFAC SDN list
- EU sanctions list
- Blockchain.com (Bitcoin explorer)
- Etherscan (Ethereum explorer)
- OpenCorporates (corporate registry)
- Google (news, financial announcements)
- Company registries (country-specific)

### Requires Subscription
- Chainalysis (crypto transaction analysis)
- Refinitiv (formerly Reuters Eikon) — financial data
- Bloomberg Terminal — financial data
- Bureau van Dijk — corporate data
- Crunchbase — funding, venture data

### Government/Official Databases
- OFAC (US Treasury)
- European Commission (EU sanctions)
- UK Office of Financial Sanctions Implementation
- INTERPOL (Red Notices)
- FinCEN (US Treasury — limited public access)
- Central bank data (country-specific)

---

## Legal & Ethical Considerations

See `ethics/legal-frameworks.md`:
- **Public records access**: Generally unrestricted for corporate/property records
- **Privacy**: Personal financial data (bank accounts, investment accounts) is confidential; infer from public sources only
- **Sanctions screening**: May be **required** in regulated industries (financial services, defense, etc.)
- **Beneficial ownership**: Privacy regulations (GDPR) may limit disclosure of home addresses; use with caution

---

## Related Domains

- `domains/corporate-investigation.md` (ownership structure, business relationships)
- `domains/person-investigation.md` (individual wealth, asset ownership)
- `domains/cryptocurrency.md` (blockchain transaction analysis)

---

**See Also**:
- `methodologies/bellingcat-methodology.md` (for ownership mapping)
- `pivot-playbooks/crypto-to-fiat.md` (cryptocurrency tracing)
- `ethics/jurisdiction-rules.md` (financial investigation legal limits)
