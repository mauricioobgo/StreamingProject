# Use an official Spark runtime as a base image
FROM bitnami/spark:3.3.0

# Set environment variables
ENV SPARK_MODE=master \
    SPARK_RPC_AUTHENTICATION_ENABLED=no \
    SPARK_RPC_ENCRYPTION_ENABLED=no \
    SPARK_LOCAL_STORAGE_ENCRYPTION_ENABLED=no \
    SPARK_SSL_ENABLED=no

# Expose Spark web UI port
EXPOSE 3002