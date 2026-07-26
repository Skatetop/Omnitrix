# OSINT Agent Skills — MCP Server

This is an open-source MCP (Model Context Protocol) server that provides 23 specialized OSINT tools for autonomous intelligence investigation. It works with Claude Code, Cursor, and any MCP-compatible client.

## Quick Start

### For Claude Code Users
```bash
cd /home/user/Omnitrix
npm install
node tools/mcp-server.js
```

Then in Claude Code: **Add MCP Server** → select this directory

### For Cursor / Other MCP Clients
Add to your `~/.claude/config.json`:
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

## Project Structure

- **`tools/mcp-server.js`** — MCP server entrypoint (stdio transport)
- **`tools/mcp-tools.json`** — Tool registry with 23 OSINT tools
- **`tools/free-tools.yaml`** — Free/public OSINT tools (no API key required)
- **`tools/apis.yaml`** — Premium API tools (requires env var API keys)
- **`system-prompt.md`** — Agent persona and operational guidelines
- **`knowledge/`** — Methodology reference, investigation frameworks
- **`templates/`** — Report templates, evidence logs, investigation plans
- **`ethics/`** — Legal frameworks and ethical guidelines by jurisdiction
- **`server.json`** — MCP server descriptor (for the MCP registry)
- **`package.json`** — npm dependencies and scripts

## Available Tools

The MCP server exposes 23 tools:

| Tool | Free | API Key | Purpose |
|---|---|---|---|
| `dns_lookup` | ✓ | | DNS resolution via Google DoH |
| `rdap_lookup_domain` | ✓ | | Domain registration data |
| `rdap_lookup_ip` | ✓ | | IP network information |
| `crt_sh_search` | ✓ | | Certificate Transparency logs |
| `wayback_cdx` | ✓ | | Internet Archive query |
| `wayback_save` | ✓ | | Save URL to Wayback Machine |
| `shodan_internetdb` | ✓ | | Free Shodan host profiles |
| `shodan_host_lookup` | | `SHODAN_KEY` | Full Shodan search |
| `ipinfo_lookup` | ✓ | | IP geolocation & ASN |
| `bgpview_asn` | ✓ | | BGP routing data |
| `github_user_lookup` | ✓ | | GitHub profile data |
| `github_code_search` | ✓ | | GitHub code search |
| `urlscan_search` | ✓ | | Urlscan.io scans |
| `alienvault_otx_lookup` | ✓ | | AlienVault threat intel |
| `hibp_breach_check` | | `HIBP_KEY` | HaveIBeenPwned breach lookup |
| `gravatar_lookup` | ✓ | | Gravatar profile lookup |
| `virustotal_domain_report` | | `VT_API_KEY` | VirusTotal domain reports |
| `securitytrails_history` | | | Historical DNS records |
| `hunter_email_finder` | | `HUNTER_KEY` | Email discovery via Hunter.io |
| `nominatim_geocode` | ✓ | | OpenStreetMap geocoding |
| `blockchain_address_lookup` | ✓ | | Bitcoin address lookup |
| `etherscan_address_lookup` | | `ETHERSCAN_KEY` | Ethereum address lookup |
| `mastodon_user_lookup` | ✓ | | Mastodon/Fediverse profiles |

## Environment Variables (Optional)

For API-enabled tools, set these in your shell:

```bash
export SHODAN_KEY="your-shodan-api-key"
export VT_API_KEY="your-virustotal-api-key"
export HIBP_KEY="your-haveibeenpwned-api-key"
export HUNTER_KEY="your-hunter-io-api-key"
export ETHERSCAN_KEY="your-etherscan-api-key"
```

## Usage Example

Once the MCP server is running, ask your agent:

> Investigate the domain `example.com` using OSINT Agent Skills methodology. Produce a full intelligence report.

The agent will:
1. Load the system prompt and adopt the OSINT analyst persona
2. Plan the investigation using intelligence cycle methodology
3. Execute DNS/WHOIS/CT lookups against free tools
4. Follow domain-to-infrastructure pivot playbooks
5. Generate a structured, cited intelligence report

## Key Features

- **Anti-hallucination**: System prompt enforces factual discipline and source citation
- **Pivot playbooks**: Explicit methodology for chaining pivots (email→domain, domain→IP, etc.)
- **Ethics-aware**: Legal frameworks by jurisdiction; never suggests illegal techniques
- **Structured reporting**: Templates enforce evidence chains and confidence labeling
- **Agent-agnostic**: Works with Claude Code, Cursor, Ollama, or any MCP client

## Documentation

- **For integration help**: See `integrations/`
- **For methodology**: See `knowledge/methodologies/`
- **For playbooks**: See `knowledge/pivot-playbooks/`
- **For reporting**: See `templates/reports/`
- **For ethics/legal**: See `ethics/legal-frameworks.md`
- **For examples**: See `examples/`

## Contributing

This project is open-source (MIT). Contributions welcome. See `CONTRIBUTING.md`.

## License

MIT — See `LICENSE`

---

**Version**: 1.4.1  
**Repository**: https://github.com/frangelbarrera/osint-agent-skills  
**Maintainer**: Frangel Barrera
