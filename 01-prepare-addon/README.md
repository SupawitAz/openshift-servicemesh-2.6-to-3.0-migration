# Add-on migration
##00-disable-addon.yaml
```
oc apply -f 00-disable-addon.yaml
```
##01-tempo-stack-demo.yaml (in your Tempo namespace)
Create a Tempo stack to store trace data. In this demo, we use MinIO as the storage backend.
```
oc create -f 01-tempo-stack-demo.yaml
```
##02-otelCollector.yaml (in the istio-system namespace)
Deploy the OpenTelemetry Collector to collect traces from application pods in the istio-system namespace.
```
oc create -f 02-otelCollector.yaml
```
##03-telemetry.yaml (in the istio-system namespace)
Create the Telemetry custom resource.
```
oc create -f 03-telemetry.yaml
```
##04-kiali.yaml (in the istio-system namespace)
Create the Kiali custom resource.
```
oc create -f 04-kiali.yaml
```
##05-prometheus (folder) in istio-system and SMMR (Service Mesh Member Roll) namespaces
Create a ServiceMonitor in istio-system and a PodMonitor in each SMMR member namespace, including istio-system. The Prometheus instance in openshift-monitoring will scrape the configured metrics in those namespaces.
Note: A NetworkPolicy (e.g., allow-from-openshift-monitoring) must be created in each SMMR namespace.
```
oc create -f 05-monitoring-prometheus-config
```

After deployment, try querying 'istio_requests_total' via Prometheus metrics.
