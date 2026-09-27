# OSINT Agent Skills + Mac Setup Guide

Complete setup instructions for connecting the OSINT Agent Skills MCP server on macOS (Intel & Apple Silicon).

## Prerequisites

- **macOS 10.15+** (Catalina or later)
- **Node.js 18+** — [Install via Homebrew](https://formulae.brew.sh/formula/node) or [nodejs.org](https://nodejs.org)
- **Claude Code** (latest version) — [Download](https://claude.ai/code) or use `brew install claude-code`
- **Git** — Pre-installed, or `brew install git`

## Step 1: Verify Node.js Installation

```bash
node --version
npm --version
```

Expected: `v18.0.0` or higher.

If not installed:
```bash
# Using Homebrew (recommended)
brew install node

# Or download from https://nodejs.org
```

## Step 2: Clone the Repository

Choose a stable location (e.g., `~/Library/Mobile Documents/com~apple~CloudDocs/osint-agent-skills` for iCloud sync, or `~/osint-agent-skills` for local):

```bash
# Local installation
mkdir -p ~/osint-agent-skills
cd ~/osint-agent-skills
git clone https://github.com/frangelbarrera/osint-agent-skills .

# Or if cloning into a new directory
git clone https://github.com/frangelbarrera/osint-agent-skills ~/osint-agent-skills
cd ~/osint-agent-skills
```

## Step 3: Install Dependencies

```bash
npm install
```

This installs any required Node.js dependencies and verifies the MCP server is ready.

## Step 4: Configure Claude Code on Mac

Create a Claude Code project directory and configure the MCP server:

```bash
# Create project directory
mkdir -p ~/osint-projects/.claude
cd ~/osint-projects
```

Create `~/.claude/settings.json` (or `~/osint-projects/.claude/settings.json` for project-scoped settings):

### Option A: Full Configuration (Recommended)

```json
{
  "systemPromptFile": "~/osint-agent-skills/system-prompt.md",
  "knowledgeBase": [
    "~/osint-agent-skills/agent-config.yaml",
    "~/osint-agent-skills/knowledge/",
    "~/osint-agent-skills/tools/",
    "~/osint-agent-skills/templates/",
    "~/osint-agent-skills/ethics/",
    "~/osint-agent-skills/case-studies/",
    "~/osint-agent-skills/examples/"
  ],
  "mcpServers": {
    "osint-agent-skills": {
      "command": "node",
      "args": ["~/osint-agent-skills/tools/mcp-server.js"],
      "env": {
        "OSINT_TOOLS_REGISTRY": "~/osint-agent-skills/tools/mcp-tools.json"
      }
    }
  },
  "permissions": {
    "allow": [
      "Bash(dig:*)",
      "Bash(curl:*)",
      "Bash(whois:*)",
      "Bash(nslookup:*)"
    ],
    "deny": [
      "Bash(rm -rf:*)",
      "Bash(sudo:*)"
    ]
  }
}
```

### Option B: Absolute Paths (If ~ Expansion Doesn't Work)

If tilde expansion doesn't work, use absolute paths:

```json
{
  "systemPromptFile": "/Users/YOUR_USERNAME/osint-agent-skills/system-prompt.md",
  "mcpServers": {
    "osint-agent-skills": {
      "command": "node",
      "args": ["/Users/YOUR_USERNAME/osint-agent-skills/tools/mcp-server.js"]
    }
  }
}
```

Replace `YOUR_USERNAME` with your actual macOS username.

## Step 5: Test the Connection

### Start Claude Code

```bash
# Navigate to the project directory
cd ~/osint-projects

# Launch Claude Code
claude
```

### Run a Test Investigation

Paste this into Claude Code:

```
Investigate the domain example.com using OSINT Agent Skills methodology.
Produce a full intelligence report.
```

**Expected result:** Claude Code should:
1. Load the OSINT Agent Skills system prompt
2. Consult the intelligence cycle methodology
3. Execute DNS/WHOIS/RDAP/certificate transparency lookups
4. Generate a structured intelligence report

## Troubleshooting on Mac

### Issue: "node: command not found"

**Solution:**
```bash
# Install Node.js via Homebrew
brew install node

# Verify installation
node --version
```

### Issue: "MCP server not found" or "Command 'node' not found in PATH"

**Solution 1 – Check Node.js location:**
```bash
which node
# Should output something like: /usr/local/bin/node or /opt/homebrew/bin/node
```

**Solution 2 – Use absolute path to node:**
```bash
# Find Node.js installation
which node
# Copy the output path and use it in settings.json:
```

Update `settings.json`:
```json
{
  "mcpServers": {
    "osint-agent-skills": {
      "command": "/usr/local/bin/node",
      "args": ["~/osint-agent-skills/tools/mcp-server.js"]
    }
  }
}
```

For Apple Silicon (M1/M2/M3):
```bash
# Homebrew installs to /opt/homebrew on Apple Silicon
which node  # Usually: /opt/homebrew/bin/node
```

### Issue: "File not found" for system-prompt.md

**Solution:**
```bash
# Verify the file exists
ls -la ~/osint-agent-skills/system-prompt.md

# Use absolute path instead of ~
# In settings.json, change:
# "systemPromptFile": "~/osint-agent-skills/system-prompt.md"
# To:
# "systemPromptFile": "/Users/YOUR_USERNAME/osint-agent-skills/system-prompt.md"
```

### Issue: "Permission denied" when running MCP server

**Solution:**
```bash
# Make the MCP server executable
chmod +x ~/osint-agent-skills/tools/mcp-server.js

# Verify shebang is present
head -n 1 ~/osint-agent-skills/tools/mcp-server.js
# Should output: #!/usr/bin/env node
```

### Issue: DNS lookups fail or timeout

**Solution:**
```bash
# Test basic DNS resolution
dig example.com

# Test if CloudFlare DoH is accessible
curl -s "https://1.1.1.1/dns-query?name=example.com&type=A" \
  -H "accept: application/dns-json"

# If blocked, the network may restrict DoH queries
# Contact your network administrator or use a VPN
```

## Advanced Setup: API Keys (Optional)

For paid API tools, configure environment variables in your shell profile:

```bash
# Edit ~/.zshrc (Zsh, default on recent macOS) or ~/.bash_profile (Bash)
nano ~/.zshrc

# Add these lines:
export SHODAN_KEY="your-api-key-here"
export VT_API_KEY="your-api-key-here"
export HUNTER_KEY="your-api-key-here"
export HIBP_KEY="your-api-key-here"
export ETHERSCAN_KEY="your-api-key-here"

# Save (Ctrl+X, then Y, then Enter in nano)
# Reload shell
source ~/.zshrc
```

Then launch Claude Code from the same terminal:
```bash
claude
```

## Verification Checklist

- [ ] Node.js 18+ installed (`node --version`)
- [ ] Repository cloned to stable location (`~/osint-agent-skills`)
- [ ] `.claude/settings.json` configured with correct paths
- [ ] Claude Code can read `system-prompt.md`
- [ ] MCP server starts without errors
- [ ] Test investigation of `example.com` completes successfully
- [ ] Intelligence report generated with proper structure

## Next Steps

Once connected:

1. **Read the methodology:** Review `knowledge/methodologies/intelligence-cycle.md` to understand the five-phase intelligence process
2. **Explore pivot playbooks:** See `knowledge/pivot-playbooks/` for domain-to-infrastructure, email-to-domain chains, etc.
3. **Use report templates:** Check `templates/reports/intelligence-report.md` for the standard report structure
4. **Enable API tools:** Configure API keys in your shell environment for premium lookups (Shodan, VirusTotal, Hunter.io, etc.)
5. **Review ethics:** Understand legal frameworks in `ethics/legal-frameworks.md` for your jurisdiction

## Support

For issues:
- Check the troubleshooting section above
- Review `integrations/README.md` for other client integrations
- Open an issue on GitHub: https://github.com/frangelbarrera/osint-agent-skills/issues

---

**Last updated:** 2026-09-01  
**macOS support:** 10.15+ (Intel & Apple Silicon M1/M2/M3)  
**Node.js requirement:** 18.0.0+
