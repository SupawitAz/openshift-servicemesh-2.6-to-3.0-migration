# Create Service Mesh 2.6
```
oc new-project istio-project
oc create -f 00-basic-smcp.yaml  
oc create -f 01-smmr-default.yaml
```
# Create bookinfo application in bookinfo-demo ns
```
oc new-project bookinfo-demo
oc create -f 02-bookinfo.yaml -n bookinfo-demo
oc create -f 03-gateway-virtualservice.yaml -n bookinfo-demo
```
