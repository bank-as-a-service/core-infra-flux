# Flux Configuration
FluxCD is so obsessed with GitOps that it uses GitOps for its own configuration. 
This means that the configuration for FluxCD is stored in this repository. 
FluxCD is configured to watch this repository for changes and apply them to the cluster.

# Setup Flux

## Pre-requisites
- AWS CLI and an existing Kubernetes cluster
```shell
aws eks --region us-west-2 update-kubeconfig --name BankCoreCluster-EKS
```
- kubectl
```shell
kubectl get nodes
```
- github credentials
```shell
export GITHUB_TOKEN=<your-token>
export GITHUB_USER=<your-username>
```
- fluxctl
```shell
brew install fluxcd/tap/flux
flux check --pre
```

## Bootstrap Flux
```shell
flux bootstrap github \
  --owner=bank-as-a-service \
  --repository=core-infra-flux \
  --branch=main \
  --path=./clusters/BankCoreCluster \
  --personal
```