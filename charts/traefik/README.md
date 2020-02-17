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

1. Create a `values.yaml` file. Example configuration:

```yaml
## Default values for Traefik
image:
  name: traefik
  tag: 2.0.5
#
deployment:
  replicas: 1
#
ports:
  web:
    port: 80
  websecure:
    port: 443
  traefik:
    port: 8080
#
service:
  annotations:
#  externalTrafficPolicy: Cluster
#
yaml:
  resources:
    requests:
      cpu: "100m"
      memory: "50Mi"
    limits:
      cpu: "300m"
      memory: "150Mi"
#  nodeSelector: {}
#  tolerations: []
#
api:
  insecure: true
  dashboard:
    enabled: true
    entryPoints:
      - web
#    middlewares:
#      - auth
#    certResolver: default
#    host: host.dashboard.com
#
staticConfig:
dynamicConfig:
#
acme:
  enabled: false
  challengeType: dns
  persistence:
    enabled: true
    annotations: {}
    ## acme data Persistent Volume Storage Class
    ## If defined, storageClassName: <storageClass>
    ## If set to "-", storageClassName: "", which disables dynamic provisioning
    ## If undefined (the default) or set to null, no storageClassName spec is
    ##   set, choosing the default provisioner.  (gp2 on AWS, standard on
    ##   GKE, AWS & OpenStack)
    ##
    # storageClass: "-"
    accessMode: ReadWriteOnce
    size: 1Gi
    ## A manually managed Persistent Volume Claim
    ## Requires persistence.enabled: true
    ## If defined, PVC must be created manually before volume will be bound
    ##
    # existingClaim:
  dnsProvider:
    name: nil
    existingSecretName: ""
    auroradns:
      AURORA_USER_ID: ""
      AURORA_KEY: ""
      AURORA_ENDPOINT: ""
    azure:
      AZURE_CLIENT_ID: ""
      AZURE_CLIENT_SECRET: ""
      AZURE_SUBSCRIPTION_ID: ""
      AZURE_TENANT_ID: ""
      AZURE_RESOURCE_GROUP: ""
    cloudflare:
      CLOUDFLARE_EMAIL: ""
      CLOUDFLARE_API_KEY: ""
    digitalocean:
      DO_AUTH_TOKEN: ""
    dnsimple:
      DNSIMPLE_OAUTH_TOKEN: ""
      DNSIMPLE_BASE_URL: ""
    dnsmadeeasy:
      DNSMADEEASY_API_KEY: ""
      DNSMADEEASY_API_SECRET: ""
      DNSMADEEASY_SANDBOX: ""
    dnspod:
      DNSPOD_API_KEY: ""
    dreamhost:
      DREAMHOST_API_KEY: ""
    dyn:
      DYN_CUSTOMER_NAME: ""
      DYN_USER_NAME: ""
      DYN_PASSWORD: ""
    exoscale:
      EXOSCALE_API_KEY: ""
      EXOSCALE_API_SECRET: ""
      EXOSCALE_ENDPOINT: ""
    gandi:
      GANDI_API_KEY: ""
    godaddy:
      GODADDY_API_KEY: ""
      GODADDY_API_SECRET: ""
    gcloud:
      GCE_PROJECT: ""
      GCE_SERVICE_ACCOUNT_FILE: ""
    linode:
      LINODE_API_KEY: ""
    namecheap:
      NAMECHEAP_API_USER: ""
      NAMECHEAP_API_KEY: ""
    ns1:
      NS1_API_KEY: ""
    otc:
      OTC_DOMAIN_NAME: ""
      OTC_USER_NAME: ""
      OTC_PASSWORD: ""
      OTC_PROJECT_NAME: ""
      OTC_IDENTITY_ENDPOINT: ""
    ovh:
      OVH_ENDPOINT: ""
      OVH_APPLICATION_KEY: ""
      OVH_APPLICATION_SECRET: ""
      OVH_CONSUMER_KEY: ""
    pdns:
      PDNS_API_URL: ""
    rackspace:
      RACKSPACE_USER: ""
      RACKSPACE_API_KEY: ""
    rfc2136:
      RFC2136_NAMESERVER: ""
      RFC2136_TSIG_ALGORITHM: ""
      RFC2136_TSIG_KEY: ""
      RFC2136_TSIG_SECRET: ""
      RFC2136_TIMEOUT: ""
    route53:
      AWS_REGION: ""
      AWS_ACCESS_KEY_ID: ""
      AWS_SECRET_ACCESS_KEY: ""
    vultr:
      VULTR_API_KEY: ""
#
accessLog:
  enabled: true
  volume:
    mountPath: /mountlogs
    hostPath: /logs

```

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
