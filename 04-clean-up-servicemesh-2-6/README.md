# Clean up
## Backup smcp and smmr
```
oc get smcp -n istio-system basic -oyaml > 01-smcp-basic-org.yaml
oc get smmr -n istio-system default -oyaml > 02-smmr-default-org.yaml
```

## Delete Service Mesh 2.6 CR
```
oc delete -f 01-smcp-basic-org.yaml
oc delete -f 02-smmr-default-org.yaml
```
