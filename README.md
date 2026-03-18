# snappwd-share

An OpenClaw AgentSkill for secure secret sharing via [SnapPwd](https://snappwd.io).

## Purpose

Helps OpenClaw users securely share secrets, API keys, and credentials via self-destructing, end-to-end encrypted links.

## Features

- **Secure by Default**: Uses AES-256-GCM encryption, client-side
- **Self-Destructing**: Links work exactly once, then the secret is deleted
- **Zero-Knowledge**: Server never sees plaintext or encryption keys
- **No Account Required**: No signup, no tracking

## Installation

```bash
npx clawhub@latest install snappwd-share
```

## Usage

Once installed, OpenClaw will automatically use this skill when you mention:
- "Share this secret securely"
- "Create a secure link for this API key"
- "I need to send a password safely"
- "Share credentials with my teammate"

### Quick Start

The skill will guide you to create a secure link at **https://snappwd.io**:

1. Go to https://snappwd.io
2. Paste your secret
3. Click "Create Secure Link"
4. Share the link

### CLI Option

If you have `snappwd-cli` installed:

```bash
npm install -g @snappwd/cli
snappwd put "your-secret-here"
```

## Files

```
snappwd-skill/
├── README.md                   # This file (repo documentation)
├── LICENSE                     # MIT License
└── skill/                      # ClawHub skill package
    ├── SKILL.md                # Main skill instructions
    ├── scripts/
    │   └── snappwd-share.sh    # CLI wrapper script
    └── references/
        ├── cli-usage.md        # Detailed CLI documentation
        └── security-model.md   # Security architecture explanation
```

## License

MIT

## Links

- [SnapPwd](https://snappwd.io) - Main application
- [SnapPwd GitHub](https://github.com/SnapPwd/SnapPwd) - Source code
- [ClawHub](https://clawhub.ai) - Skill marketplace