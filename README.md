# IDBuilder

A distributed ID generation service that supports multiple ID types for various business requirements.

## Overview

IDBuilder provides a unified API for generating distributed unique identifiers. Unlike solutions that focus on a single ID type, IDBuilder supports multiple formats to meet diverse application needs:

| ID Type              | Example                    | Use Case                         |
|----------------------|----------------------------|----------------------------------|
| Auto-increment       | `1001, 1002, 1003, ...`    | Sequential order numbers         |
| Snowflake            | `6982386234567892992`      | Distributed unique IDs           |
| Formatted String     | `INV20230101-0001`         | Human-readable business IDs      |

## Features

- **Multiple ID Types** — Support for auto-increment, snowflake, and custom formatted string IDs
- **Distributed Architecture** — Horizontal scalability with worker coordination
- **Flexible Configuration** — Customizable ID formats with composable parts
- **Two-Tier Authentication** — Admin tokens for management, key tokens for ID generation
- **High Performance** — Client-side generation for snowflake IDs

## Architecture

```
┌─────────────┐                          ┌─────────────┐                    ┌─────────────┐
│             │  ──── ID Request ────▶   │             │                    │             │
│ Client/SDK  │                          │   Worker    │ ◀──── Config ────  │ Controller  │
│             │  ◀─── ID Response ────   │             │                    │             │
└─────────────┘                          └─────────────┘                    └─────────────┘
```

## Quick Start

### Generate Auto-Increment IDs

```bash
# Get key token (requires admin token)
curl -X GET "http://idbuilder/v1/auth/token?key=order-id" \
  -H "Authorization: Bearer <admin_token>"

# Generate IDs
curl -X GET "http://idbuilder/v1/id/increment?key=order-id&size=5" \
  -H "Authorization: Bearer <key_token>"
```

### Generate Formatted String IDs

```bash
curl -X GET "http://idbuilder/v1/id/formatted?key=invoice-id&size=2" \
  -H "Authorization: Bearer <key_token>"

# Response: {"id": ["INV20230101-0001", "INV20230101-0002"]}
```

## Documentation

- [Basic Design](proposal/design/001-basic-design.md) — Architecture and API specification

## Contributing

We welcome contributions from the community! Here's how you can help:

1. **Report Issues** — Found a bug or have a feature request? [Open an issue](../../issues)
2. **Submit PRs** — Fork the repo, make your changes, and submit a pull request
3. **Improve Docs** — Help us improve documentation and examples

### Development Setup

```bash
# Clone the repository
git clone https://github.com/idbuilder/idbuilder.git
cd idbuilder

# Install dependencies
go mod download

# Run tests
go test ./...
```

### Proposal Process

For significant changes, please follow the proposal process:

1. Create a proposal document in `proposal/design/`
2. Open an issue for discussion
3. Implement after consensus is reached

## License

This project is open source. See [LICENSE](../LICENSE) for details.

## Community

- [GitHub Discussions](../../discussions) — Ask questions and share ideas
- [Issues](../../issues) — Report bugs and request features
