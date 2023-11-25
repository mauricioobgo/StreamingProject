# Spark Cluster with Kafka, Zookeeper, and Jupyter

## Overview

This project sets up a distributed computing environment using Docker Compose, incorporating Apache Spark as the primary data processing engine. The Spark cluster includes a master node (`spark-master`) and two worker nodes (`spark-worker-1` and `spark-worker-2`). Additionally, the environment includes Kafka as a distributed message broker (`kafka`), Zookeeper for distributed coordination and configuration management (`zookeeper`), and a Jupyter notebook server (`jupyter`) for interactive data analysis with Spark.

## Components

### 1. Spark Master (`spark-master`)

The Spark master node serves as the central coordinator for the Spark cluster. It is configured to operate in standalone mode and provides a web UI accessible at `http://localhost:8080`. This UI allows monitoring of the Spark cluster and its applications.

### 2. Spark Workers (`spark-worker-1` and `spark-worker-2`)

The Spark worker nodes are responsible for executing tasks assigned by the Spark master. Each worker node is configured to allocate 1 core and 1GB of memory for Spark processing. These worker nodes communicate with the Spark master to receive task assignments.

### 3. Zookeeper (`zookeeper`)

Zookeeper is a distributed coordination service that plays a crucial role in distributed systems. In this setup, it is utilized for managing configuration information across the Spark and Kafka components.

### 4. Kafka (`kafka`)

Kafka is a distributed streaming platform that facilitates the building of real-time data pipelines and streaming applications. In this project, Kafka is configured with a broker ID of 1 and listens on port 9092. It connects to Zookeeper for distributed coordination.

### 5. Jupyter (`jupyter`)

The Jupyter notebook server is used for interactive data analysis and visualization. It is configured to connect to the Spark cluster with the master URL set to `spark://spark-master:7077`. The Jupyter notebook is accessible at `http://localhost:8888`, and the token for authentication is set to 'DarthVader'.

## Usage

To run the entire environment, execute the following command in the directory containing the `docker-compose.yml` file:

```bash
docker-compose up

```

Once the services are up and running, you can access the Spark master web UI at 
http://localhost:8080 and the Jupyter notebook at http://localhost:8888.

## Dependencies
- Docker
- Docker Compose

Notes
Ensure that the necessary Docker images are available locally. The provided configuration pulls images from Docker Hub.