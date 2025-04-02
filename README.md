# Multi-Cloud Platform (MCP) for NVIDIA NGC

A container-first approach for accessing remote GPU resources through the NVIDIA NGC API, enabling seamless transitions between local development and cloud GPU resources.

## Features

- **Container-First Development**: Develop locally using Docker containers that mirror cloud environments
- **Seamless Cloud Integration**: Deploy to cloud GPU resources when needed
- **Unified API Access**: Consistent interface for NVIDIA NGC services
- **Environment Flexibility**: Graceful fallbacks for non-GPU environments
- **Kubernetes Integration**: Easy deployment to managed Kubernetes services

## Getting Started

### Prerequisites

- Docker and Docker Compose
- NVIDIA NGC API Key (get one from [NGC](https://ngc.nvidia.com/))
- (Optional) kubectl for Kubernetes deployments

### Quick Start

1. Clone this repository:
   ```bash
   git clone https://github.com/jeflowers/nvidia-mcp-remote-gpu.git
   cd nvidia-mcp-remote-gpu
   ```

2. Set your NGC API key in `.env` file:
   ```
   NGC_API_KEY=your-api-key-here
   ```

3. Start local development environment:
   ```bash
   ./scripts/run-local.sh
   ```

4. Access Jupyter notebooks at http://localhost:8888

### Cloud Deployment

To deploy to a cloud environment with GPU resources:

1. Ensure you have kubectl configured for your cluster
2. Run:
   ```bash
   ./scripts/deploy-cloud.sh
   ```

## Project Structure

```
├── .github/            # GitHub Actions workflows
├── config/             # Configuration files
├── data/               # Data directory (mounted in containers)
├── deploy/             # Deployment manifests (Kubernetes, etc.)
├── notebooks/          # Jupyter notebooks
├── scripts/            # Utility scripts
├── src/                # Source code
│   ├── api/            # API client code
│   ├── data/           # Data utilities
│   └── utils/          # Common utilities
├── docker-compose.yml  # Local development environment
├── Dockerfile          # Custom Docker image (if needed)
└── README.md           # This file
```

## Development

### Local Development with Containers

The provided Docker Compose setup allows you to develop locally with containers. It includes:

- Morpheus container with Jupyter notebooks
- Optional NeMo container for specific tasks
- Shared volume mounts for notebooks and data

### Adding Custom Dependencies

If you need additional dependencies, create a custom Dockerfile:

```dockerfile
FROM nvcr.io/nvidia/morpheus:latest

# Install additional dependencies
RUN pip install --no-cache-dir \
    python-dotenv \
    requests \
    kubernetes

# Add any custom configurations
COPY config/jupyter_notebook_config.py /root/.jupyter/
```

Then update the docker-compose.yml to use your custom image.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [NVIDIA NGC](https://ngc.nvidia.com/)
- [NVIDIA Morpheus](https://developer.nvidia.com/morpheus)
- [NVIDIA NeMo](https://developer.nvidia.com/nemo)
