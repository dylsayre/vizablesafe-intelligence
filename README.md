# VizableSafe Threat Intelligence Repository

This repository contains threat intelligence data for the VizableSafe browser extension, including:
- **Threat detection patterns** (regex patterns for malware, phishing, scams)
- **Whitelist** (trusted domains that skip analysis)
- **Blacklist** (known malicious domains to block immediately)

## Purpose

VizableSafe extensions fetch intelligence from this repository periodically to:
1. **Detect new threats** without requiring extension updates
2. **Respond rapidly** to emerging phishing campaigns
3. **Reduce false positives** by whitelisting trusted domains
4. **Block known threats** immediately via blacklist

## Files

### `patterns.json`
Regex patterns for detecting malicious content on web pages.

**Categories:**
- `malware` - Malware delivery (ClickFix, PowerShell execution)
- `phishing` - Credential theft attempts
- `scam` - Prize scams, tech support scams, cryptocurrency scams

**Update frequency:** Every 4 hours

### `whitelist.json`
Trusted domains that should skip security analysis entirely.

**Includes:**
- Major search engines (Google, Bing)
- Social media platforms (Twitter, Facebook, LinkedIn)
- Development platforms (GitHub, StackOverflow)
- Cloud providers (AWS, Azure, Cloudflare)
- Productivity tools (Microsoft 365, Google Workspace)

**Update frequency:** Every 24 hours

### `blacklist.json`
Known malicious domains and patterns to block immediately.

**Includes:**
- Exact domain matches (known phishing sites)
- Pattern matches (brand impersonation patterns)
- IP addresses (malicious servers)
- Free TLDs commonly used for phishing (.tk, .ml, .ga, .cf)

**Update frequency:** Every 1 hour (most critical for rapid response)

### `metadata.json`
Repository metadata including version tracking, statistics, and changelog.

## Usage

### For Extension Developers

The extension fetches intelligence from GitHub raw URLs:

```javascript
const BASE_URL = 'https://raw.githubusercontent.com/dylsayre/vizablesafe-intelligence/main';

// Fetch patterns
const patterns = await fetch(`${BASE_URL}/patterns.json`).then(r => r.json());

// Fetch whitelist
const whitelist = await fetch(`${BASE_URL}/whitelist.json`).then(r => r.json());

// Fetch blacklist
const blacklist = await fetch(`${BASE_URL}/blacklist.json`).then(r => r.json());
```

### For Threat Researchers

To contribute new patterns:

1. Fork this repository
2. Add your pattern to `patterns.json`:
```json
{
  "id": "your-pattern-id",
  "category": "malware|phishing|scam",
  "severity": "critical|high|medium|low",
  "regex": "your regex pattern here",
  "description": "What this pattern detects",
  "enabled": true,
  "added": "YYYY-MM-DD"
}
```
3. Update `metadata.json` version and changelog
4. Submit a pull request

### For Enterprise Deployments

Organizations can fork this repository to create custom intelligence:

1. Fork this repo to your organization's GitHub
2. Add organization-specific patterns/whitelist/blacklist
3. Configure extension to point to your fork:
```javascript
const INTELLIGENCE_BASE = 'https://raw.githubusercontent.com/YOUR-ORG/vizablesafe-intelligence/main';
```

## Update Workflow

### Adding a New Threat Pattern

```bash
# 1. Edit patterns.json
$ nano patterns.json

# 2. Add your pattern to the "patterns" array

# 3. Update version in metadata.json
$ nano metadata.json
# Increment version: 2024-01-06-001 → 2024-01-06-002

# 4. Commit and push
$ git add patterns.json metadata.json
$ git commit -m "Add pattern for [threat name]"
$ git push

# 5. Extensions will fetch new patterns within 4 hours
```

### Blacklisting a Phishing Domain

```bash
# 1. Edit blacklist.json
$ nano blacklist.json

# 2. Add domain to "domains" array
"domains": [
  "existing-bad-site.com",
  "new-phishing-site.com"  // Add this
]

# 3. Update version and commit
$ git add blacklist.json metadata.json
$ git commit -m "Blacklist new-phishing-site.com"
$ git push

# Extensions will block this domain within 1 hour
```

## Version Format

Versions follow the format: `YYYY-MM-DD-NNN`

Examples:
- `2024-01-06-001` - First update on January 6, 2024
- `2024-01-06-002` - Second update on January 6, 2024
- `2024-01-07-001` - First update on January 7, 2024

## Pattern Guidelines

**Good patterns:**
- ✅ Specific enough to avoid false positives
- ✅ Include description and references
- ✅ Tested against real-world examples
- ✅ Include severity rating

**Bad patterns:**
- ❌ Too broad (matches legitimate content)
- ❌ No description or context
- ❌ Untested regex
- ❌ Missing severity

**Example good pattern:**
```json
{
  "id": "clickfix-powershell-v1",
  "category": "malware",
  "severity": "critical",
  "regex": "Press Win\\+X.*PowerShell.*Administrator",
  "description": "ClickFix malware delivery - instructs user to open PowerShell as admin",
  "enabled": true,
  "added": "2024-01-06",
  "references": [
    "https://www.malwarebytes.com/blog/news/2024/clickfix-attacks"
  ]
}
```

## Changelog

See `metadata.json` for detailed changelog of all updates.

## License

This intelligence repository is provided as-is for use with VizableSafe extension.

## Contributing

Contributions welcome! Please:
1. Test your patterns thoroughly
2. Avoid false positives
3. Include references where applicable
4. Update metadata.json with changelog entry

## Security

To report a false positive or suggest improvements:
- Open an issue in this repository
- Tag with `false-positive` or `enhancement`
- Provide example URL and pattern ID

## Questions?

See the main VizableSafe repository for more information.
