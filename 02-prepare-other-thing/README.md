# Disable auto-creation of NetworkPolicies, Routes, and the IngressGateway, then create networkPolicy, route and istio-ingressgateway as a Deployment. Istio will not manage the ingress gateway for you.
```
oc apply -f 00-disable-gateway-nepol-route.yaml  
oc apply -f 01-network-policy  
oc apply -f 02-route  
oc apply -f 03-istio-ingressgateway-canary.yaml
```
