oc apply -f 00-disable-gateway-nepol-route.yaml  
oc apply -f 01-network-policy  
oc apply -f 02-route  
oc apply -f 03-istio-ingressgateway-canary.yaml
