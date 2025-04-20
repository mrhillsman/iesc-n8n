# n8n Workflow Automation using OpenShift GitOps

This repository contains OpenShift manifests for deploying [n8n](https://n8n.io/) workflow automation platform using OpenShift GitOps, with Redis for message queuing and PostgreSQL for persistent data storage.

## Overview

n8n is a fair-code licensed workflow automation tool that allows you to connect different services and build automated workflows with a visual editor. This repository provides a GitOps approach to deploying n8n in an OpenShift environment.

## Architecture

The deployment consists of three main components:

1. **n8n** - The workflow automation platform
2. **Redis** - Used as a message queue for handling workflow executions
3. **PostgreSQL** - Persistent storage for workflow definitions and execution data

## Prerequisites

- OpenShift cluster
- OpenShift GitOps operator installed on your cluster
- openshift client configured to communicate with your cluster

## Repository Structure

```bash
.
├── apps/                       # GitOps application definitions
│   ├── n8n.yaml                # n8n application
│   ├── redis.yaml              # Redis application
│   └── postgres.yaml           # PostgreSQL application
├── manifests/                  # OpenShift manifests
│   ├── n8n/                    # n8n deployment manifests
│   ├── redis/                  # Redis deployment manifests
│   └── postgres/               # PostgreSQL deployment manifests
└── scripts/                    # Utility scripts
    └── setup.sh                # Setup script
```

## Deployment

### 1. Clone this repository

```bash
git clone https://github.com/mrhillsman/iesc-n8n.git
cd iesc-n8n
```

### 2. Update configuration (if needed)

Review and update the configuration in the manifest files according to your environment needs.

### 3. Deploy using ArgoCD

Apply the GitOps application definitions:

```bash
oc apply -f apps/
```

OpenShift GitOps will automatically deploy all components in the correct order.

## Configuration

### PostgreSQL

The PostgreSQL deployment includes:
- Persistent volume for data storage
- Secrets for database credentials
- Service for internal access

Configuration options can be adjusted in `manifests/postgres/deployment.yaml`.

### Redis

The Redis deployment includes:
- Persistent volume for data storage
- Service for internal access

Configuration options can be adjusted in `manifests/redis/deployment.yaml`.

### n8n

The n8n deployment includes:
- Configuration for PostgreSQL connection
- Configuration for Redis as queue manager
- Route for external access

Configuration options can be adjusted in `manifests/n8n/deployment.yaml`.

## Customization

You can customize the deployment by modifying the manifests in the respective folders. After pushing changes to the repository, OpenShift GitOps will automatically sync the changes to your cluster.

## Scaling

For production environments, consider:
- Setting up Redis in cluster mode
- Implementing PostgreSQL with replication
- Scaling n8n horizontally for high availability

## Troubleshooting

Common issues:
- Check OpenShift GitOps UI for sync status and errors
- Verify database connection from n8n pods
- Ensure PVCs are properly created and bound

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
