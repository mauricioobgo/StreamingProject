FROM docker.io/bitnami/spark:3.3.0

USER root

# Install Jupyter Notebook and dependencies
RUN apt-get update && \
    apt-get install -y python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install jupyter pyspark

USER 1001

# Expose Jupyter Notebook port
EXPOSE 8888

# Start Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]