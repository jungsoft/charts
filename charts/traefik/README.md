# Traefik

[Traefik](https://traefik.io/) is a modern HTTP reverse proxy and load balancer made to deploy
microservices with ease.

## Introduction

This chart bootstraps Traefik version 2 as a Kubernetes ingress controller

## Prerequisites

- Kubernetes 1.10+
- You are deploying the chart to a cluster with a cloud provider capable of provisioning an
external load balancer (e.g. AWS or GKE)
- You control DNS for the domain(s) you intend to route through Traefik

## Installation

1. Create a `values.yaml` file

2. Clone the repository and install the helm chart. You can set a [static](https://docs.traefik.io/reference/static-configuration/file/) and/or a [dynamic](https://docs.traefik.io/reference/dynamic-configuration/file/) configuration file when installing the chart:

```bash
git clone git@github.com:rschef/traefik-helm-chart.git

helm install traefik-helm-chart \
  --name traefik-ingress-controller \
  --namespace kube-system \
  --values values.yaml \
  --set-file staticConfig="traefik-static-config.yaml" \
  --set-file dynamicConfig="traefik-dynamic-config.yaml"
```
