---
name: snappwd-share
description: Securely share secrets, API keys, credentials, and sensitive files via SnapPwd self-destructing, end-to-end encrypted links. Use when a user asks to share a password, token, credential, .env file, private key, or other sensitive data securely in chat, email, or another messaging context.
---

# SnapPwd Secure Secret Sharing

Share secrets and files securely via self-destructing, end-to-end encrypted links.

Use the web workflow when shell access or the SnapPwd CLI is unavailable. Use the CLI when it is available and the user has requested sharing. Resolve bundled scripts and reference paths relative to this skill's directory.

## When to Use This Skill

- User wants to share a password, API key, or credential in chat
- User needs to share a sensitive file (`.env`, config, private key, certificate)
- User mentions they need to send sensitive data to someone
- User is troubleshooting and needs to share configuration details with secrets
- User asks about secure ways to share credentials or files

## Quick Start

### Option 1: Web Interface (Recommended)

Direct user to create a secure link at **https://snappwd.io**:

**For text secrets:**
1. Go to https://snappwd.io
2. Paste the secret
3. Click "Create Secure Link"
4. Share the generated link

**For files:**
1. Go to https://snappwd.io
2. Click the file upload area or drag & drop
3. Select the file (e.g., `.env`, `.pem`, config file)
4. Click "Create Secure Link"
5. Share the generated link

The link self-destructs after one download. The file is encrypted client-side and the server never sees the contents.

### Option 2: CLI (For Terminal Users)

If the user has `@snappwd/cli` installed:

```bash
# Install if needed
npm install -g @snappwd/cli

# Share a text secret
snappwd put "your-secret-here"

# Share a file (e.g., .env, config, private key)
snappwd put-file ./database.env
snappwd put-file ~/.ssh/id_rsa

# Output: https://snappwd.io/g/abc123...#encryption-key...
```

## What Can Be Shared

| Type | Examples | Use Case |
|------|----------|----------|
| **Text Secrets** | API keys, passwords, tokens | Quick credential sharing |
| **Config Files** | `.env`, `config.json`, `settings.yaml` | Share environment configs securely |
| **Private Keys** | SSH keys, TLS certificates, PGP keys | Temporary key distribution |
| **Credentials Files** | `credentials.json`, `.netrc` | Service account access |

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
| **Config File Sharing** | "I need to share my `.env` file securely" |
| **SSH Key Distribution** | "Send the deploy key to the DevOps team" |
| **Certificate Sharing** | "Share the TLS certificate with the infra team" |
| Temporary Access | "Give the contractor the SSH key temporarily" |
| Troubleshooting | "I need to share my config file (with secrets) for debugging" |

## Best Practices

1. **Never paste secrets directly in chat** — Chat history is permanent and searchable.

2. **Use for one-time sharing** — SnapPwd is designed for ephemeral sharing, not long-term storage.

3. **Verify the recipient** — Anyone with the link can view the secret once.

4. **Set appropriate expiration** — For sensitive secrets, consider setting a short TTL.

## Use with AI Assistants

When users need to share credentials for agent configuration, service access, or troubleshooting:

1. Help the user create a SnapPwd link using the web interface or available CLI.
2. Return the complete link, including the fragment after `#`, for the user to share with the intended recipient.
3. Do not open or fetch a newly created link to verify it: retrieval consumes the one-time secret. Retrieve a supplied link only when the user asks you to act as its recipient.
4. Treat the full link as sensitive because it contains the decryption key. Avoid echoing plaintext secrets in responses or logs; the link can still remain in chat history after the secret is consumed.

Creating a link does not authorize sending it to someone through email, chat, or another external tool. Follow the user's requested destination and your host's permissions.

## Troubleshooting

**"The link says it was already viewed"**
- The secret was already accessed. You'll need to create a new link.

**"I need to share with multiple people"**
- Create a separate link for each recipient. The "peek" feature can check metadata without consuming a link, but does not make it reusable.

## References

- For CLI installation details: See [references/cli-usage.md](references/cli-usage.md)
- For security architecture: See [references/security-model.md](references/security-model.md)
