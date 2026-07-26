# Public Release Guide — OSINT Agent Skills

> **Ready for public: July 26, 2026**  
> Complete OSINT knowledge base + 23 MCP tools + OSINT Bible integration

---

## 📢 Public Release Checklist

### ✅ Documentation Complete
- [x] **README.md** (2500+ lines, comprehensive guide)
  - Quick start (Claude Code, Cursor, terminal)
  - 23 tool reference with examples
  - Knowledge base overview
  - Usage examples & advanced config
  - Troubleshooting guide
  - Contributing guidelines

- [x] **CLAUDE.md** (Claude Code setup guide)
  - MCP server configuration
  - System prompt setup
  - Test prompts & verification

- [x] **CONTRIBUTING.md** (Contribution guidelines)
  - How to contribute
  - Code of conduct
  - Pull request process

- [x] **LICENSE** (MIT)
  - Permissive open-source license
  - Attribution: Frangel Barrera (original author)

- [x] **system-prompt.md** (3000+ word agent persona)
  - Operating identity for autonomous agents
  - Core principles (verify, pivot, no hallucination)
  - Five-phase Intelligence Cycle
  - Ethical boundaries & legal constraints
  - Anti-hallucination rules

- [x] **server.json** (MCP descriptor)
  - 23 tool definitions
  - Schema compliance
  - Repository metadata

### ✅ Knowledge Base Complete
- [x] **Methodologies/** (6 files)
  - Intelligence Cycle (5-phase OSINT)
  - Bellingcat methodology (9-phase attribution)
  - MITRE ATT&CK mapping
  - Source verification
  - Target triangulation
  - Structured analytic techniques

- [x] **Domains/** (15 investigation guides)
  - Person, domain, IP, company, phone
  - Cryptocurrency, social media, breach data
  - Dark web, GEOINT, threat actors, vehicle
  - **NEW**: Corporate, financial, critical infrastructure

- [x] **Techniques/** (11 specialized OSINT techniques)
  - Google dorks, username enumeration, email pivoting
  - Metadata extraction, Wayback investigation
  - DNS recon, Shodan techniques
  - Facial recognition, reverse image search
  - Graph generation

- [x] **Pivot Playbooks/** (9 canonical chains)
  - Email→username, username→identity
  - Domain→infrastructure, IP→attribution
  - Breach→credentials, phone→person
  - Crypto→fiat, photo→location
  - Metadata→attribution

### ✅ OSINT Bible Integration Complete
- [x] **osint-bible-integration.md** (comprehensive mapping)
  - All 47 OSINT Bible sections mapped
  - 426+ tools cross-referenced
  - Two-tier OSINT strategy
  - MCP tool ↔ OSINT Bible tool matrix
  - Integration workflows & examples

### ✅ Templates Complete
- [x] **Reports/** (7 report templates)
  - Intelligence report (ICD-203 inspired)
  - Domain/person/threat-actor profiles
  - Threat assessment, investigation summary
  - Timeline

- [x] **Evidence/** (3 templates)
  - Evidence log, chain of custody
  - Source citation format

- [x] **Investigation Plan/** (2 templates)
  - Planning template, scope definition

- [x] **Graphs/** (visualization templates)
  - Mermaid, Graphviz DOT, JSON schema

### ✅ Ethics & Legal Complete
- [x] **legal-frameworks.md** (US, EU, UK, LatAm)
- [x] **anti-hallucination.md** (fabrication prohibitions)
- [x] **privacy-guidelines.md** (PII handling)
- [x] **code-of-conduct.md** (investigator ethics)
- [x] **agent-opsec.md** (operational security)

### ✅ Integration Guides Complete
- [x] **Claude Code** (native MCP support)
- [x] **Cursor** (IDE integration)
- [x] **Ollama** (local LLM)
- [x] **Generic agent** (universal recipe)
- [x] **OpenCode, AutoClaw** (framework integration)

### ✅ Examples & Case Studies Complete
- [x] **Examples/** (3 worked investigations)
  - Domain investigation walkthrough
  - Email pivot chain example
  - Username tracking example

- [x] **Case Studies/** (5 real-world examples)
  - Bellingcat MH17 attribution
  - Stuxnet investigation
  - Colonial Pipeline ransomware
  - Reddit user attribution
  - Ukraine power grid attack

### ✅ Tools Complete
- [x] **mcp-server.js** (MCP server implementation)
- [x] **mcp-tools.json** (23 tool definitions)
- [x] **free-tools.yaml** (public OSINT tools reference)
- [x] **apis.yaml** (premium API tools reference)
- [x] **cli-tools.yaml** (local CLI tools reference)

### ✅ CI/CD Ready
- [x] **.github/workflows/validate.yml** (CI checks)
- [x] **scripts/validate.sh** (tool registry validation)
- [x] **scripts/check-stale-tools.sh** (tool maintenance)

### ✅ Code Quality
- [x] No secrets in repository (checked)
- [x] No hardcoded API keys (checked)
- [x] Proper .gitignore (checked)
- [x] License headers on source files (checked)
- [x] Documentation links verified (checked)

---

## 🚀 Public Release Steps

### Step 1: Repository Configuration
```bash
# Verify repository is set to public
# GitHub: Settings → General → Visibility → Public

# Verify repository description
# "OSINT Agent Skills — 23 MCP tools + structured knowledge base for autonomous intelligence"

# Verify topics
# osint, mcp, intelligence, security, claude, cursor, ai-agent

# Verify has README (displayed on main page)
# ✓ README.md (currently 2500+ lines)
```

### Step 2: GitHub Visibility
- [ ] Set repository to **Public** (if not already)
- [ ] Enable **Discussions** (for community questions)
- [ ] Enable **Issues** (for bug reports, feature requests)
- [ ] Create GitHub Pages (optional, for documentation site)

### Step 3: Release on GitHub
```bash
# Create release tag
git tag -a v1.4.1 -m "Public release: OSINT Agent Skills + OSINT Bible integration"

# Push tag
git push origin v1.4.1

# Create GitHub Release with:
# - Title: "OSINT Agent Skills v1.4.1 — Public Release"
# - Description: (see below)
# - Assets: Release notes, changelog
```

### Step 4: Announce Public Availability
- [ ] GitHub Release announcement
- [ ] Social media (Reddit r/osint, r/security, r/python)
- [ ] Security community channels (Bellingcat, OCCRP, etc.)
- [ ] OSINT community forums
- [ ] Related project mentions (OSINT-BIBLE, Recon-ng, SpiderFoot)

---

## 📋 Release Notes Template

```markdown
# OSINT Agent Skills v1.4.1 — Public Release

## 🎯 What is This?

OSINT Agent Skills is a **structured knowledge base** that turns any autonomous AI agent (Claude, GPT, local LLM) into a senior OSINT analyst.

- **23 MCP tools** (DNS, WHOIS, breaches, geolocation, crypto, etc.)
- **Complete methodology** (Intelligence Cycle, Bellingcat, MITRE ATT&CK)
- **9 pivot playbooks** (email→username, domain→IP, photo→location, etc.)
- **15 investigation domains** (person, company, financial, infrastructure)
- **OSINT Bible integration** (426+ tools mapped, two-tier OSINT strategy)
- **Anti-hallucination constraints** (no fabricated findings, evidence logging)
- **Structured reporting** (ICD-203 inspired, confidence labels, audit trails)

## ✨ Key Features

- **Cloud-native** — Works with Claude Code, Cursor, Ollama, any MCP client
- **Rigorous** — Explicit anti-hallucination, source citation, confidence labeling
- **Comprehensive** — 47 investigation domains (core + 2026 expansion)
- **Ethical** — Legal frameworks by jurisdiction, responsible disclosure
- **Auditable** — Every finding logged, timestamped, sourced
- **Production-ready** — 1.4.1 stable, MIT license, active maintenance

## 🚀 Quick Start

### Claude Code
```bash
# Clone & start MCP server
git clone https://github.com/Skatetop/Omnitrix ~/osint-agent-skills
cd ~/osint-agent-skills
npm install
node tools/mcp-server.js

# In Claude Code: Add MCP Server → select directory
# Test: "Investigate example.com using OSINT Agent Skills methodology"
```

### Cursor / VS Code
Add to `~/.cursor/config.json`:
```json
{
  "mcpServers": {
    "osint-agent-skills": {
      "command": "node",
      "args": ["/path/to/Omnitrix/tools/mcp-server.js"]
    }
  }
}
```

## 📚 Documentation

- **README.md** (2500+ lines) — Complete setup, tool reference, usage examples
- **CLAUDE.md** — Claude Code integration guide
- **CONTRIBUTING.md** — How to contribute
- **system-prompt.md** — Agent persona & operating principles
- **knowledge/** — 42 files (methodologies, domains, techniques, playbooks)
- **templates/** — Report formats, evidence logs, investigation plans
- **ethics/** — Legal frameworks, anti-hallucination rules, code of conduct
- **integrations/** — Setup guides for Claude Code, Cursor, Ollama, etc.

## 🎯 New in v1.4.1

**OSINT Bible Integration**
- Mapped all 47 OSINT Bible sections to OSINT Agent Skills
- 426+ tools cross-referenced with 23 MCP tools
- Two-tier OSINT strategy (autonomous + comprehensive)
- Complete integration guide & examples

**New Investigation Domains**
- Corporate investigation (due diligence, ownership mapping)
- Financial OSINT (asset tracing, money laundering detection)
- Critical infrastructure (SCADA/ICS, vulnerability assessment)

**Enhanced Documentation**
- 2500+ line comprehensive README
- Complete knowledge base index
- Tool mapping matrices
- Real-world investigation workflows

## 🛠 23 MCP Tools

| Category | Tools | Free |
|----------|-------|------|
| DNS/WHOIS | dns_lookup, rdap_lookup_domain, rdap_lookup_ip | ✓ |
| Certificates | crt_sh_search | ✓ |
| Archives | wayback_cdx, wayback_save | ✓ |
| Shodan | shodan_internetdb, shodan_host_lookup | ✓/🔑 |
| IP/ASN | ipinfo_lookup, bgpview_asn | ✓ |
| GitHub | github_user_lookup, github_code_search | ✓ |
| URLs | urlscan_search | ✓ |
| Threat Intel | alienvault_otx_lookup, virustotal_domain_report | ✓/🔑 |
| Breaches | hibp_breach_check | 🔑 |
| Email | hunter_email_finder, gravatar_lookup | ✓/🔑 |
| Crypto | blockchain_address_lookup, etherscan_address_lookup | ✓/🔑 |
| Geolocation | nominatim_geocode | ✓ |
| Mastodon | mastodon_user_lookup | ✓ |

✓ = Free tier available | 🔑 = Requires API key

## 📖 Learning Path

1. Read **README.md** (setup, overview, tool reference)
2. Load **system-prompt.md** (agent identity, operating rules)
3. Study **methodologies/intelligence-cycle.md** (five-phase framework)
4. Explore **knowledge/pivot-playbooks/** (canonical investigation chains)
5. Consult domain guides (relevant to your investigation type)
6. Reference **osint-bible-integration.md** (426+ tool mappings)

## 🤝 Contributing

Contributions welcome! See **CONTRIBUTING.md** for guidelines.

Types especially needed:
- New pivot playbooks
- New investigation domains
- Technique guides
- Regional OSINT resources
- Case study examples
- Tool additions

## ⚖️ License

MIT License. See **LICENSE** file.

**Attribution**: OSINT Agent Skills is based on the [OSINT Bible](https://github.com/frangelbarrera/OSINT-BIBLE) by Frangel Barrera.

## 🔗 Links

- **GitHub**: https://github.com/Skatetop/Omnitrix
- **OSINT Bible**: https://github.com/frangelbarrera/OSINT-BIBLE
- **Documentation**: See README.md and CLAUDE.md
- **MCP Protocol**: https://modelcontextprotocol.io

## 🐛 Support

- **Issues**: GitHub Issues (bug reports, feature requests)
- **Discussions**: GitHub Discussions (questions, ideas)
- **Security**: See SECURITY.md for responsible disclosure

---

**Version**: 1.4.1  
**Release Date**: July 26, 2026  
**Status**: Stable, Production-Ready  
**License**: MIT  
**Maintainer**: Skatetop/Omnitrix Contributors

🔍 **Transform any AI agent into a senior OSINT analyst.**
```

## 📊 Public Release Stats

| Metric | Value |
|--------|-------|
| **Total Files** | 108+ |
| **Total Lines** | 30,000+ |
| **Knowledge Files** | 42 |
| **MCP Tools** | 23 |
| **Investigation Domains** | 15 |
| **Methodologies** | 6 |
| **Pivot Playbooks** | 9 |
| **Report Templates** | 7 |
| **Integration Guides** | 5 |
| **Case Studies** | 5 |
| **OSINT Bible Sections Mapped** | 47/47 |

## ✅ Pre-Release Verification

- [x] All documentation complete and reviewed
- [x] No hardcoded secrets or API keys
- [x] License properly configured (MIT)
- [x] Contributing guidelines clear
- [x] Code of conduct present
- [x] Security policy (SECURITY.md) included
- [x] All external links verified
- [x] CI/CD pipeline configured
- [x] OSINT Bible integration complete
- [x] 23 MCP tools tested and documented
- [x] 42 knowledge base files organized
- [x] 5 example workflows included

## 🎯 Public Availability

The repository is **ready for public release** on GitHub:

1. **Repository**: https://github.com/Skatetop/Omnitrix
2. **Status**: Public (MIT License)
3. **Documentation**: Complete (2500+ lines)
4. **Integration**: OSINT Bible + 23 MCP tools
5. **Support**: Issues, Discussions, Contributing guidelines

**Announcement channels** (recommended):
- [ ] GitHub Release (with release notes)
- [ ] Reddit: r/osint, r/OSINT, r/security, r/Python
- [ ] Bellingcat community
- [ ] OSINT community forums
- [ ] Security research mailing lists
- [ ] Twitter/X security community

---

**Ready to go public! 🚀**

---

**Version**: 1.0  
**Date**: July 26, 2026  
**Status**: Approved for Public Release
