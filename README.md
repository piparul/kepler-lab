# Introduction

This lab gives a hands on experience on how to use Kepler to measure container energy consumption.

## About Kepler

TO-DO

## Getting Started

1.  Installing the Kepler Operator and creating Kepler Custom Resource

```bash

## Clone the kepler-operator repository
git clone https://github.com/sustainable-computing-io/kepler-operator.git

## Deploy the operator
cd kepler-operator

make deploy IMG=quay.io/sustainable_computing_io/kepler-operator:latest

oc project kepler-operator-system

oc get pods

## Create Kepler Custom Resource
kubectl apply -f config/samples/

## Check if kepler-exporter is up and running
oc get pods

## Check kepler-exporter service
oc get svc

## Check if kepler-exporter metrics are available

oc port-forward svc/kepler-exporter 9107:9107

```

2. Installing the Grafana Operator

* Copy the Bearer Token and update in the Grafana Datasource manifest.


```bash
oc whoami --show-token

vi hack/dashboard/openshift/03-grafana-datasource-UPDATETHIS.yaml

## Update bearer token to match your environment
## httpHeaderValue1: 'Bearer ${BEARER_TOKEN}'
## Replace ${BEARER_TOKEN} with the output from oc whoami --show-token
## save and close the file using ESC + wq!
```

* Run the `hack/dashboard/openshift/deploy.sh` to set up Grafana.

```bash
hack/dashboard/openshift/deploy-grafana.sh

## Allow sometime for grafana installation

oc get pods

```

3. Accessing the Grafana Dashboard (For step 3 attach screenshots for each steps)

* Navigate to OpenShift Console/UI -> Networking -> Routes
* Select `kepler-operator-system` namespace
* Click on the grafana route
* Grafana dashboard is opened in a new tab
* Enter username as `kepler` and password as `kepler`
