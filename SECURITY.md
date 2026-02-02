# Security Policy

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 1.x     | :white_check_mark: |

## Reporting a Vulnerability

We take security seriously at SmoothDev. If you discover a security vulnerability in this GitHub Action, please report it responsibly.

### How to Report

1. **Do NOT** create a public GitHub issue for security vulnerabilities
2. Email security@smoothdev.io with:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Any suggested fixes (optional)

### What to Expect

- **Acknowledgment**: Within 48 hours of your report
- **Initial Assessment**: Within 5 business days
- **Resolution Timeline**: Depends on severity, typically:
  - Critical: 24-48 hours
  - High: 1 week
  - Medium: 2 weeks
  - Low: Next release cycle

### Scope

This security policy covers:
- The GitHub Action code in this repository
- The composite action workflow

Out of scope:
- The SmoothDev CLI (report to [sd-smooth-cli](https://github.com/smoothdev-io/sd-smooth-cli))
- The SmoothDev API/backend (report to security@smoothdev.io)

## Security Best Practices

When using this action:

1. **Store API keys securely**: Always use GitHub Secrets for your `SMOOTHDEV_API_KEY`
2. **Limit permissions**: Only grant the minimum required permissions to your workflow
3. **Pin versions**: Use specific version tags (e.g., `@v1.0.0`) rather than `@main`
4. **Review workflow logs**: Ensure no sensitive data is being logged

## Acknowledgments

We appreciate responsible disclosure and will acknowledge security researchers who report valid vulnerabilities (with permission).
