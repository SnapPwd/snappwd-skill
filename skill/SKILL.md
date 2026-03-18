---
name: snappwd-share
description: Securely share secrets, API keys, and credentials with OpenClaw agents and team members via self-destructing links. Use when the user needs to share sensitive information (passwords, API keys, tokens, credentials) in chat, email, or any messaging context. Triggers on phrases like "share this secret", "send this password securely", "create a secure link for this API key", "share credentials safely", or when user mentions needing to share sensitive data.
---

# SnapPwd Secure Secret Sharing

Share secrets securely via self-destructing, end-to-end encrypted links.

## When to Use This Skill

- User wants to share a password, API key, or credential in chat
- User mentions they need to send sensitive data to someone
- User is troubleshooting and needs to share configuration details with secrets
- User asks about secure ways to share credentials

## Quick Start

### Option 1: Web Interface (Recommended)

Direct user to create a secure link at **https://snappwd.io**:

1. Go to https://snappwd.io
2. Paste the secret
3. Click "Create Secure Link"
4. Share the generated link

The link self-destructs after one view. The secret is encrypted client-side and the server never sees the key.

### Option 2: CLI (For Terminal Users)

If the user has `snappwd-cli` installed:

```bash
# Install if needed
npm install -g @snappwd/cli

# Create a secure link
snappwd put "your-secret-here"

# Output: https://snappwd.io/g/abc123...#encryption-key...
```

## Security Model

**Key points to explain to users:**

1. **Zero-Knowledge Encryption**: Secrets are encrypted in the browser/CLI before upload. The server never sees the plaintext or encryption key.

2. **Self-Destructing**: Links work exactly once. After viewing, the secret is permanently deleted from the server.

3. **Key in URL Fragment**: The encryption key is embedded in the URL after `#`, which means it's never sent to the server—it stays in the browser.

4. **No Account Required**: No signup, no tracking, no logs of who created or viewed the secret.

## Common Use Cases

| Use Case | Example |
|----------|---------|
| API Key Sharing | "I need to share my OpenAI API key with a teammate" |
| Database Credentials | "Send the DB password to the new developer" |
| OAuth Tokens | "Share this access token with the integration team" |
| Temporary Access | "Give the contractor the SSH key temporarily" |
| Troubleshooting | "I need to share my config file (with secrets) for debugging" |

## Best Practices

1. **Never paste secrets directly in chat** — Chat history is permanent and searchable.

2. **Use for one-time sharing** — SnapPwd is designed for ephemeral sharing, not long-term storage.

3. **Verify the recipient** — Anyone with the link can view the secret once.

4. **Set appropriate expiration** — For sensitive secrets, consider setting a short TTL.

## Integration with OpenClaw

When users need to share credentials for OpenClaw configuration:

1. User creates a SnapPwd link with the credential
2. User shares the link in the OpenClaw chat
3. OpenClaw (or the human on the other side) opens the link to retrieve the credential
4. Link self-destructs, leaving no trace in chat history

This is especially useful for:
- Sharing API keys for agent configuration
- Providing temporary access to services
- Sharing secrets during troubleshooting sessions

## Troubleshooting

**"The link says it was already viewed"**
- The secret was already accessed. You'll need to create a new link.

**"I need to share with multiple people"**
- Create separate links for each recipient, or use the "peek" feature to check metadata without destroying the secret.

## References

- For CLI installation details: See [references/cli-usage.md](references/cli-usage.md)
- For security architecture: See [references/security-model.md](references/security-model.md)