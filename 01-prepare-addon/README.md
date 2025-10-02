### Add on migration
# istio_requests_total
# 00-disable-addon.yaml
oc apply -f 00-disable-addon.yaml

# 01-tempo-stack-demo.yaml in your tempo namespace
#Create tempo stack for store trace data in this demo we use minio as storage
oc create -f 01-tempo-stack-demo.yaml 

# 02-otelCollector.yaml in istio-system namespace
#Deploy opentelemetry collector for collect trace from applicastion pods in istio-system nasmepace
oc create -f 02-otelCollector.yaml

# 03-telemetry.yaml in istio-system namespace
#Create Telemetry CR
oc create -f 03-telemetry.yaml

# 04-kiali.yaml in istio-system namespace
#Create Kiali CR
oc create -f 04-kiali.yaml

# 05-prometheus (folder) in istio-system and smmr (istio member) namesapces
#Create servicemonitor in istio-system and podMonitor CR in each smmr member include istio-system. The prometheus in openshift-monitoring will scrape the involve metrics in the config namespace. 
#Note: the network policy allow-from-openshift-monitoring must be created in each smmr namespace.
oc create -f 05-monitoring-prometheus-config

