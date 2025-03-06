# Logs with Loki

Set up and configure [Loki](https://grafana.com/oss/loki/) with Alloy and Grafana to analyse logs in your Kubernetes cluster.

## Charts installation

Before installing all the components, don't forget to check default configurations and update some values according to your needs!

Create a kind cluster or use your own Kubernetes cluster:

```sh
kind create cluster --config ./kind.yaml --name k8s-loki
```

Define the helm repository for charts installation:

```sh
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

Install Loki:

```sh
helm install loki grafana/loki --version 6.27.0 --namespace observability --create-namespace --values ./values-loki.yaml
```

Install Alloy:

```sh
helm install alloy grafana/alloy --version 0.12.1 --namespace observability --create-namespace --values ./values-alloy.yaml
```

And finally, install Grafana:

```sh
helm install grafana grafana/grafana --version 8.10.1 --namespace observability --create-namespace --values ./values-grafana.yaml
```

Get access to Grafana with the ``kubectl port-forward`` command if there is no ingress configured:

```sh
kubectl -n observability port-forward svc/grafana 8080:80
```

## Blog posts

Don't hesitate to read the following blog posts to find out more about configuring Loki:

* [Take back control of your logs with Loki](https://blog.filador.fr/en/posts/take-back-control-of-your-logs-with-loki) - English version
* [Reprenez le contrôle de vos logs avec Loki](https://blog.filador.fr/posts/reprenez-le-controle-de-vos-logs-avec-loki/) - French version
