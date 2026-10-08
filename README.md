# snappwd-share

A reusable agent skill for secure secret and file sharing via [SnapPwd](https://snappwd.io).

## Purpose

Helps AI assistants and their users securely share secrets, API keys, credentials, and sensitive files via self-destructing, end-to-end encrypted links. The package uses `SKILL.md` instructions with bundled scripts and references, and can be loaded by agents that support this skill format.

## Features

- **Secure by Default**: Uses AES-256-GCM encryption, client-side
- **Self-Destructing**: Links work exactly once, then the secret/file is deleted
- **Zero-Knowledge**: Server never sees plaintext or encryption keys
- **No Account Required**: No signup, no tracking
- **File Support**: Share `.env` files, SSH keys, certificates, config files

## Installation

### Skills CLI

Use the [Skills CLI](https://github.com/vercel-labs/skills) to select your agent and install the skill:

```bash
npx skills@latest add https://github.com/SnapPwd/snappwd-skill/tree/main/skill --skill snappwd-share
```

Add `--global` to make it available across projects. Installing the skill does not install the optional SnapPwd CLI.

### Manual Installation

```bash
git clone https://github.com/SnapPwd/snappwd-skill.git
```

Copy the entire `skill/` directory into your agent's documented skills directory, naming the destination folder `snappwd-share`. Keep `SKILL.md`, `scripts/`, and `references/` together so relative paths work. Reload your agent's skills if required.

### OpenClaw / ClawHub

OpenClaw users can also install through ClawHub:

```bash
npx clawhub@latest install snappwd-share
```

## Usage

Ask your agent to use `snappwd-share`, or make a request such as:

- "Share this secret securely"
- "Create a secure link for this API key"
- "I need to send a password safely"
- "Share credentials with my teammate"

Automatic discovery and explicit invocation syntax depend on your agent. The web workflow works without terminal access; agents with shell access can use the optional CLI.

### Quick Start

The skill will guide you to create a secure link at **https://snappwd.io**:

1. Go to https://snappwd.io
2. Paste your secret
3. Click "Create Secure Link"
4. Share the link

Treat the complete link as sensitive: it includes the decryption key. Opening it consumes the one-time secret, so leave that action to the intended recipient.

### CLI Option

Agents with shell access can use the [SnapPwd CLI](https://github.com/SnapPwd/snappwd-cli) ([`@snappwd/cli`](https://www.npmjs.com/package/@snappwd/cli) on npm):

```bash
npm install -g @snappwd/cli
snappwd put "your-secret-here"
```

See the [CLI documentation](https://www.snappwd.io/docs/cli) for every command and option.

## Files

```
snappwd-skill/
├── README.md                   # This file (repo documentation)
├── LICENSE                     # MIT License
└── skill/                      # Portable skill package
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
- [SnapPwd Docs](https://www.snappwd.io/docs) - Guides and reference
- [SnapPwd CLI](https://github.com/SnapPwd/snappwd-cli) - Command-line client used by this skill's CLI workflow
- [SnapPwd Service](https://github.com/SnapPwd/snappwd-service) - Open-source backend API
- [SnapPwd Web](https://github.com/SnapPwd/snappwd-web) - Self-hosted web app
- [ClawHub](https://clawhub.ai) - Optional OpenClaw installation
