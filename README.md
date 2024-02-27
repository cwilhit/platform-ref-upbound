# platform-ref-upbound

This repository contains a reference implementation for deploying Crossplane at scale with Upbound self-hosted Spaces. 

## Repo tour

This repo is built based upon a fictitious organization composed of three business units: a consumers services business unit, a manufacturing services business unit, and a marketing business unit. Each business unit operates their own app teams, deploying software and infrastructure for their line of business. This platform operates a managed control plane mapping to a cloud account boundary. Each business unit deploys software into `test` and `prod` environments. Therefore, you'll find this reference architecture deploys a control plane group for each business unit, and then 2 control planes for each test and prod software environment. The result is 6 managed control planes, plus a seventh "sandbox" control plane which all business units can use for a sandbox environment.

This project requires the following:

* A deployment of Upbound self-hosted Spaces (deployed into your preferred Kubernetes cluster). Specifically, when deploying a Space, make sure to deploy the [on cluster Argo CD plugin](https://docs.upbound.io/spaces/use-argo-flux/#on-cluster-argo-cd).
* A deployment of Argo CD on the same cluster

We've broken the repo into three folders:

1. **bootstrap:** This folder contains the manifests to configure Argo CD to sync desired control plane infrastructure and configure each control plane, driven from Git.
2. **infrastructure:** This folder contains the declaration of the desired runtime configuration of each managed control plane.
3. **configuration:** This folder contains the desired Crossplane configurations of each control plane.

In each of these three root folders, we've grouped elements together based on the business unit (3 groups, plus a sandbox group).