# openshift-servicemesh-2.6-to-3.0-migration
Manifests and playbooks to migrate OpenShift Service Mesh from 2.6 to 3.x.  
This solution **needs downtime**; if you want to do a **canary** migration, you must **reorder** the files you apply (**NetworkPolicy must be the last thing to create**).

## 00-demo-2-6-servicemesh
This folder contains the SMCP CR for version 2.6 and the Bookinfo application to initialize the project before starting the migration.

## 01-prepare-addon
Disable the Kiali, Prometheus, and Jaeger add-ons provided by SMCP, because OpenShift Service Mesh 3.x does not include these add-ons. You must install them separately.

## 02-prepare-other-thing
Disable auto-creation of NetworkPolicies, Routes, and the IngressGateway, then create **istio-ingressgateway** as a **Deployment**. Istio will not manage the ingress gateway for you.

## 03-start-migrate
This folder contains the CR manifests to create Service Mesh v3.x and steps to move applications from 2.6 to 3.x.

## 04-clean-up-servicemesh-2-6
After migrating to Service Mesh 3.x, delete the Service Mesh 2.6 CR and related resources.

