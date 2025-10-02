# Install Red Hat OpenShift Service Mesh 3. In this demo we use version 3.1.2

# Create istioCNI CR
oc create ns istio-cni
oc create -f 01-istio-cni.yaml  

Create istio CR
oc creat -f istio.yaml

# labels istio and applications namespace
REV_NAME=$(oc get istio ossm-3 -ojson | jq -r .status.activeRevisionName)
oc label ns istio-system istio.io/rev=$REV_NAME maistra.io/ignore-namespace="true" istio-injection- --overwrite=true
oc label ns bookinfo-demo istio.io/rev=$REV_NAME maistra.io/ignore-namespace="true" istio-injection- --overwrite=true
oc rollout restart deployments -n istio-system
oc rollout restart deployments -n bookinfo-demo

# check version ~/istio-1.27.0/bin/istioctl ps

# Create IstioRevisionTag
oc create -f 03-rev-tag.yaml

# Unlabels istio.io/rev due to we set rev as default with IstioRevisionTag
oc label ns istio-system istio-injection=enabled istio.io/rev-
oc label ns bookinfo-demo istio-injection=enabled istio.io/rev-
