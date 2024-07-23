# Kubernetes Monitoring with Prometheus and Grafana

This project sets up a monitoring solution for a Kubernetes cluster using Prometheus and Grafana. It visualizes metrics such as CPU usage, memory consumption, and pod status.

## Components

### Prometheus

Prometheus is an open-source systems monitoring and alerting toolkit. In this setup, Prometheus collects metrics from the Kubernetes cluster and its components.

- **prometheus/configmap.yaml**: Defines the Prometheus configuration. It includes scrape configurations for collecting metrics from Kubernetes nodes and pods.
- **prometheus/deployment.yaml**: Deploys Prometheus as a single-instance deployment.
- **prometheus/service.yaml**: Exposes Prometheus on a NodePort for external access.

### Node Exporter

Node Exporter is a Prometheus exporter for hardware and OS metrics exposed by *nix kernels. It's deployed as a DaemonSet to ensure an instance runs on each node.

- **node-exporter/daemonset.yaml**: Deploys Node Exporter as a DaemonSet to collect node-level metrics.
- **node-exporter/service.yaml**: Exposes Node Exporter metrics on a NodePort for Prometheus to scrape.

### Grafana

Grafana is an open-source platform for monitoring and observability. It allows users to query, visualize, alert on, and explore metrics and logs.

- **grafana/configmap.yaml**: Defines Grafana's data source configuration. It sets up Prometheus as the default data source.
- **grafana/deployment.yaml**: Deploys Grafana as a single-instance deployment.
- **grafana/service.yaml**: Exposes Grafana on a NodePort for external access.

## Setup

### Prometheus

1. Apply Prometheus configuration:
    ```sh
    kubectl apply -f manifests/prometheus/configmap.yaml
    ```

2. Deploy Prometheus:
    ```sh
    kubectl apply -f manifests/prometheus/deployment.yaml
    kubectl apply -f manifests/prometheus/service.yaml
    ```

### Node Exporter

1. Deploy Node Exporter:
    ```sh
    kubectl apply -f manifests/node-exporter/daemonset.yaml
    kubectl apply -f manifests/node-exporter/service.yaml
    ```

### Grafana

1. Apply Grafana configuration:
    ```sh
    kubectl apply -f manifests/grafana/configmap.yaml
    ```

2. Deploy Grafana:
    ```sh
    kubectl apply -f manifests/grafana/deployment.yaml
    kubectl apply -f manifests/grafana/service.yaml
    ```

## Accessing the Dashboards

- **Prometheus**: Accessible at `http://<node-ip>:32001`
- **Grafana**: Accessible at `http://<node-ip>:32000`

## Adding Grafana Dashboards

1. Login to Grafana (default credentials: `admin/admin`).
2. Configure the Prometheus data source (it should already be configured via the ConfigMap).
3. Import pre-built dashboards or create your own to visualize metrics.

## Conclusion

This setup provides a simple yet effective monitoring solution for Kubernetes clusters using Prometheus and Grafana. You can expand and customize this solution based on your monitoring needs.

## License
This project is licensed under the MIT License.
