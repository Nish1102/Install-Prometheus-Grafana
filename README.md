# Installation Guide for Prometheus and Grafana using Helm

This guide provides step-by-step instructions for installing Prometheus and Grafana using Helm charts. Helm is a package manager for Kubernetes that simplifies the deployment and management of applications.

## Prerequisites

Before starting the installation process, ensure you have the following prerequisites installed:

- Kubernetes cluster up and running
- Helm installed on your local machine
- Access to the Helm charts repository for Prometheus and Grafana

## Installation Steps

1. **Create Namespace:**

    ```bash
    kubectl create namespace monitoring
    ```

2. **Add Helm Repositories:**

    ```bash
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo add grafana https://grafana.github.io/helm-charts
    ```

3. **Update Repositories:**

    ```bash
    helm repo update
    ```

4. **Install Prometheus:**

    ```bash
    helm install prometheus prometheus-community/prometheus --namespace monitoring
    ```

5. **Install Grafana:**

    ```bash
    helm install grafana grafana/grafana --namespace monitoring
    ```

6. **Access Grafana Dashboard:**

    After installation, get the Grafana admin password:

    ```bash
    kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
    ```

    Access the Grafana dashboard using the following command and login with the admin credentials:

    ```bash
    kubectl port-forward --namespace monitoring service/grafana 3000:80
    ```

    Open a web browser and navigate to `http://localhost:3000`.

7. **Access Prometheus Dashboard:**

    You can access the Prometheus dashboard via the following command:

    ```bash
    kubectl port-forward --namespace monitoring service/prometheus-server 9090
    ```

    Open a web browser and navigate to `http://localhost:9090`.

## Configuration

Both Prometheus and Grafana can be further configured according to your specific requirements. Refer to the official documentation for more details:

- [Prometheus Helm Chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/prometheus)
- [Grafana Helm Chart](https://github.com/grafana/helm-charts/tree/main/charts/grafana)

## Troubleshooting

If you encounter any issues during the installation process, refer to the Helm chart documentation or check the Kubernetes logs for error messages.

## References

- [Prometheus Official Documentation](https://prometheus.io/docs/)
- [Grafana Official Documentation](https://grafana.com/docs/)
- [Helm Official Documentation](https://helm.sh/docs/)

