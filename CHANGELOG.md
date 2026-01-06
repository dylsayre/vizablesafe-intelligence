# Changelog

All notable changes to VizableSafe threat intelligence will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and versions use the format `YYYY-MM-DD-NNN`.

## [2024-01-06-003] - 2024-01-06

### Added - Blacklist
- Initial blacklist created
- Added 6 known phishing domains (PayPal, Microsoft, Apple impersonation)
- Added 12 blacklist patterns for common brand impersonation
- Blocked free TLDs commonly used for phishing (.tk, .ml, .ga, .cf)

## [2024-01-06-002] - 2024-01-06

### Added - Whitelist
- Initial whitelist created with 50+ trusted domains
- Added major search engines (Google, YouTube, Bing)
- Added social media platforms (Twitter/X, Facebook, LinkedIn, Reddit)
- Added development platforms (GitHub, StackOverflow, npm)
- Added cloud providers (AWS, Azure, Cloudflare)
- Added productivity tools (Microsoft 365, Office, Outlook)
- Added localhost and 127.0.0.1 path whitelisting for development

## [2024-01-06-001] - 2024-01-06

### Added - Patterns
- Initial pattern set created with 10 detection patterns
- **ClickFix Malware Detection (3 patterns)**
  - `clickfix-powershell-v1` - PowerShell admin execution instructions
  - `clickfix-powershell-v2` - Generic PowerShell execution variants
  - `clickfix-run-command` - Run dialog exploitation
- **Credential Theft / Phishing (3 patterns)**
  - `credential-theft-urgent` - Urgency-based social engineering
  - `credential-theft-action-required` - Action-required tactics
  - `fake-security-alert` - Fake security alerts
- **Scams (4 patterns)**
  - `prize-scam` - Prize/lottery scams
  - `tech-support-scam` - Tech support scams with phone numbers
  - `cryptocurrency-doubler` - Crypto doubling scams
  - `fake-invoice-payment` - Fake invoice/payment phishing

### Categories
- Malware: 3 patterns
- Phishing: 6 patterns
- Scam: 2 patterns

### Severity Breakdown
- Critical: 3 patterns
- High: 6 patterns
- Medium: 2 patterns

---

## Update Guidelines

When updating intelligence files:

1. **Increment version** in the appropriate file
2. **Update metadata.json** with new version and timestamp
3. **Add changelog entry** in this file
4. **Commit with descriptive message**:
   - `"Add pattern for X"` - New pattern
   - `"Blacklist domain X"` - New blacklist entry
   - `"Whitelist domain X"` - New whitelist entry
   - `"Disable pattern X"` - Disabled false-positive pattern
   - `"Update pattern X"` - Modified existing pattern

### Version Numbering

Format: `YYYY-MM-DD-NNN`

- `YYYY-MM-DD` - Date of update
- `NNN` - Sequence number (001, 002, 003, etc.)
- Multiple updates on same day increment sequence number
- Each file (patterns, whitelist, blacklist) has independent versioning

### Examples

```
2024-01-06-001  # First update on Jan 6
2024-01-06-002  # Second update on Jan 6
2024-01-07-001  # First update on Jan 7
```
