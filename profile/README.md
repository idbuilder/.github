# IDBuilder

A distributed ID generation service supporting multiple ID types for modern applications.

## What is IDBuilder?

IDBuilder is a high-performance, distributed ID generation service written in Rust. It provides three types of unique identifiers:

- **Auto-increment** — Sequential numeric IDs (`1001, 1002, 1003`)
- **Snowflake** — Twitter-style distributed unique IDs (`6982386234567892992`)
- **Formatted String** — Human-readable business IDs with customizable patterns (`INV20230101-0001`)

## Repositories

| Repository | Description |
|------------|-------------|
| [proposal](https://github.com/idbuilder/proposal) | Design proposals for IDBuilder |
| [worker](https://github.com/idbuilder/worker) | Core ID generation service (Rust) |
| [controller](https://github.com/idbuilder/controller) | Coordination service for distributed deployments (Go) |
| [idbuilder-rust](https://github.com/idbuilder/idbuilder-rust) | Rust client library for IDBuilder |
| [idbuilder-java](https://github.com/idbuilder/idbuilder-java) | Java client library for IDBuilder |
| [idbuilder-golang](https://github.com/idbuilder/idbuilder-golang) | Go client library for IDBuilder |
| [idbuilder-python](https://github.com/idbuilder/idbuilder-python) | Python client library for IDBuilder |

## Getting Started

### Quick Start

```bash
# Clone the repository
git clone https://github.com/idbuilder/worker.git
cd worker

# Build the service
make build

# Run tests
make test

# Start the service
./target/release/idbuilder-worker
```

### Generate Your First ID

```bash
# Create a configuration (requires admin token)
curl -X POST http://localhost:8080/v1/config/increment \
  -H "Authorization: Bearer <admin-token>" \
  -H "Content-Type: application/json" \
  -d '{"key": "order-id", "start": 1000, "step": 1}'

# Get a key token
curl "http://localhost:8080/v1/auth/token?key=order-id" \
  -H "Authorization: Bearer <admin-token>"

# Generate IDs
curl "http://localhost:8080/v1/id/increment?key=order-id&size=5" \
  -H "Authorization: Bearer <key-token>"
```

## Contributing

We welcome contributions from the community! Here's how you can help:

- **Report bugs** — Open an issue describing the problem
- **Suggest features** — Share your ideas for improvements
- **Submit PRs** — Fix bugs or implement new features
- **Improve docs** — Help make our documentation clearer

## License

Apache License 2.0.
