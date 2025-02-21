# tap-teradata

A high-performance [Singer](https://www.singer.io/) tap for Teradata that combines Rust's performance with Python's ease of use. This tap uses Teradata Parallel Transporter (TPT) for efficient data extraction and is available as a Python package.

[![PyPI version](https://badge.fury.io/py/tap-teradata.svg)](https://badge.fury.io/py/tap-teradata)
[![Rust](https://github.com/pesnik/tap-teradata/workflows/Rust/badge.svg)](https://github.com/pesnik/tap-teradata/actions)
[![Python](https://github.com/pesnik/tap-teradata/workflows/Python/badge.svg)](https://github.com/pesnik/tap-teradata/actions)

## Development Checklist

- [ ] Initial Setup
  - [x] Create GitHub repository
  - [x] Set up project structure
  - [ ] Initialize Rust project
  - [ ] Initialize Python package
  - [ ] Set up PyO3 bindings

- [ ] Core Implementation
  - [ ] Implement TPT connection handling
  - [ ] Create schema discovery functionality
  - [ ] Implement data sync operations
  - [ ] Add incremental replication support
  - [ ] Implement error handling

- [ ] Testing
  - [ ] Set up Rust unit tests
  - [ ] Set up Python unit tests
  - [ ] Create integration tests
  - [ ] Add test coverage reporting
  - [ ] Create test documentation

- [ ] Documentation
  - [x] Create comprehensive README
  - [ ] Add API documentation
  - [ ] Create CONTRIBUTING.md
  - [ ] Add inline code documentation
  - [ ] Create Wiki pages

- [ ] CI/CD
  - [ ] Set up GitHub Actions
  - [ ] Configure PyPI deployment
  - [ ] Add code quality checks
  - [ ] Set up automated testing
  - [ ] Configure version management

- [ ] Package Distribution
  - [ ] Create Python wheel
  - [ ] Configure cross-platform builds
  - [ ] Set up automated releases
  - [ ] Create installation verification tests

## Features

- 🚀 High-performance Rust core with TPT integration
- 🐍 Easy installation via pip
- 📦 Automatic schema discovery
- 🔄 Incremental replication support
- 🛠 Configurable TPT operators and attributes
- 🔒 Safe memory handling through Rust

## Prerequisites

- Python 3.8 or higher
- Teradata Tools and Utilities (TTU) installed
- TPT operator access on Teradata instance
- Rust toolchain (for development)

## Installation

### From PyPI

```bash
pip install tap-teradata
```

### From Source

```bash
git clone https://github.com/pesnik/tap-teradata
cd tap-teradata
pip install -e .
```

## Configuration

Create a `config.json` file:

```json
{
  "host": "your-teradata-host",
  "username": "your-username",
  "password": "your-password",
  "database": "your-database",
  "schema": "your-schema",
  "tpt_operator": {
    "export_operator": "/path/to/tdexport",
    "attributes": [
      "ErrorLimit=100",
      "MaxSessions=8"
    ],
    "buffers": 8
  }
}
```

### Configuration Parameters

| Parameter | Description | Required | Default |
|-----------|-------------|----------|---------|
| host | Teradata host address | Yes | - |
| username | Database username | Yes | - |
| password | Database password | Yes | - |
| database | Database name | Yes | - |
| schema | Schema name | Yes | - |
| tpt_operator.export_operator | Path to TPT export operator | Yes | - |
| tpt_operator.attributes | TPT attributes list | No | [] |
| tpt_operator.buffers | Number of TPT buffers | No | 4 |

## Usage

### Command Line Interface

1. Discovery Mode:
```bash
tap-teradata --config config.json --discover > catalog.json
```

2. Sync Mode:
```bash
tap-teradata --config config.json --catalog catalog.json
```

### Python API

```python
from tap_teradata import TeradataTap

# Initialize the tap
config = {
    "host": "your-host",
    "username": "your-username",
    "password": "your-password",
    "database": "your-database",
    "schema": "your-schema"
}

tap = TeradataTap(config)

# Discovery mode
catalog = tap.discover()

# Sync mode
tap.sync(catalog)
```

## Performance Tuning

### TPT Configuration

Optimize performance through TPT settings:

1. Buffer Management:
```json
{
  "tpt_operator": {
    "buffers": 16,
    "attributes": ["BufferSize=1024KB"]
  }
}
```

2. Parallel Sessions:
```json
{
  "tpt_operator": {
    "attributes": ["MaxSessions=12"]
  }
}
```

### Memory Usage

The Rust implementation automatically handles memory efficiently, but you can tune the buffer size based on your system's capabilities.

## Development

### Building from Source

1. Clone the repository:
```bash
git clone https://github.com/pesnik/tap-teradata
cd tap-teradata
```

2. Install development dependencies:
```bash
pip install -e ".[dev]"
```

3. Build Rust components:
```bash
cargo build --release
```

### Running Tests

```bash
# Run Python tests
pytest

# Run Rust tests
cargo test

# Run integration tests
pytest tests/integration
```

## Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

1. Fork the repository
2. Create a virtual environment
3. Install development dependencies
4. Make your changes
5. Run tests
6. Submit a pull request

## Troubleshooting

### Common Issues

1. TPT Operator Not Found:
```
Error: TPT operator path not found
Solution: Verify the export_operator path in config.json
```

2. Memory Issues:
```
Error: Buffer allocation failed
Solution: Reduce the buffer size or number of parallel sessions
```

3. Connection Issues:
```
Error: Failed to connect to Teradata
Solution: Check host, credentials, and network connectivity
```

## Architecture

The tap is built with a hybrid architecture:
- Core data extraction in Rust using TPT
- Python wrapper for Singer compatibility
- PyO3 for seamless integration
- Efficient memory management through Rust ownership system

## Roadmap

- [ ] Support for custom SQL queries
- [ ] Advanced TPT optimization options
- [ ] Multiple authentication methods
- [ ] Data type conversion customization
- [ ] Streaming large result sets
- [ ] Performance monitoring tools

## License

Apache License 2.0

## Repository Information

- 📫 Maintainer: [@pesnik](https://github.com/pesnik)
- 🌐 Repository: [https://github.com/pesnik/tap-teradata](https://github.com/pesnik/tap-teradata)
- 📦 PyPI: [https://pypi.org/project/tap-teradata](https://pypi.org/project/tap-teradata)
- 📖 Documentation: [Wiki](https://github.com/pesnik/tap-teradata/wiki)

## Acknowledgments

- [Singer.io](https://www.singer.io/) for the ETL specification
- [PyO3](https://pyo3.rs/) for Rust-Python bindings
- Teradata for TPT functionality

## Support

- 🐛 Issues: [GitHub Issues](https://github.com/pesnik/tap-teradata/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/pesnik/tap-teradata/discussions)
- 📝 Changes: [CHANGELOG.md](CHANGELOG.md)
