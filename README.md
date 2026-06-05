# Spark Cluster with Kafka, Zookeeper, and Jupyter

A distributed streaming environment built with Docker Compose, combining Apache Spark, Kafka, Zookeeper, and Jupyter for interactive data processing.

## Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Jupyter     │────▶│ Spark Master  │────▶│  Kafka      │
│  (port 8888) │     │  (port 8080)  │     │ (port 9092) │
└─────────────┘     ├──────────────┤     └──────┬──────┘
                    │ Spark Worker  │            │
                    │  (port 8081)  │            │
                    ├──────────────┤     ┌──────▼──────┐
                    │ Spark Worker  │     │ Zookeeper   │
                    │  (port 8082)  │     │(port 2181)  │
                    └──────────────┘     └─────────────┘
```

## Components

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **spark-master** | `bitnami/spark:3.3.0` | `8080` | Spark cluster coordinator (standalone mode) |
| **spark-worker-1** | `bitnami/spark:3.3.0` | `8081` | Spark worker (1 core, 1 GB memory) |
| **spark-worker-2** | `bitnami/spark:3.3.0` | `8082` | Spark worker (1 core, 1 GB memory) |
| **zookeeper** | `bitnami/zookeeper:latest` | `2181` | Distributed coordination service |
| **kafka** | `bitnami/kafka:latest` | `9092` | Distributed streaming platform |
| **jupyter** | Custom (`notebooks/Dockerfile`) | `8888` | Interactive notebook server with PySpark |

## Quick Start

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/) (v2+)

### 1. Configure environment variables

```bash
cp .env.example .env
# Edit .env to customize tokens and settings
```

### 2. Start all services

```bash
docker compose up -d
```

### 3. Access the services

| Service | URL |
|---------|-----|
| Spark Master UI | http://localhost:8080 |
| Jupyter Notebook | http://localhost:8888 |

The Jupyter token is configured via the `JUPYTER_TOKEN` variable in `.env` (default: `DarthVader`).

### 4. Stop all services

```bash
docker compose down
```

## Configuration

Environment variables can be set in a `.env` file at the project root. See [`.env.example`](.env.example) for all available options.

| Variable | Default | Description |
|----------|---------|-------------|
| `JUPYTER_TOKEN` | `DarthVader` | Jupyter authentication token |
| `KAFKA_ADVERTISED_LISTENERS` | `PLAINTEXT://kafka:9092` | Kafka advertised listener address |
| `ALLOW_ANONYMOUS_LOGIN` | `yes` | Allow anonymous Zookeeper login (**set to `no` in production**) |
| `ALLOW_PLAINTEXT_LISTENER` | `yes` | Allow non-TLS Kafka listeners (**set to `no` in production**) |

## Project Structure

```
.
├── docker-compose.yml        # Main orchestration file
├── notebooks/
│   ├── Dockerfile            # Jupyter + PySpark image
│   └── docker-compose.yml   # Standalone Jupyter setup
├── spark-streaming/
│   ├── Dockerfile            # Spark streaming image
│   └── docker-compose.yml   # Standalone streaming setup
├── requirements.txt          # Python dependencies
├── .env.example              # Environment variable template
└── .editorconfig             # Editor formatting rules
```

## Security Notes

- **Zookeeper** is configured with `ALLOW_ANONYMOUS_LOGIN=yes` — change to `no` before exposing publicly.
- **Kafka** uses plaintext listeners — enable TLS for production deployments.
- **Jupyter token** should be changed from the default in any shared environment.
- **Spark master** runs as `root` user inside the container; consider restricting this for production.

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
