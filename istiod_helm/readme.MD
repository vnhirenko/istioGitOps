1. Generate helm charts:
```
cd /tmp
export ISTIO_VERSION=1.9.9
curl -L https://istio.io/downloadIstio | TARGET_ARCH=x86_64 sh -
cd istio-$ISTIO_VERSION
cp -a  manifests/charts/base/ ${path_to_repo}/operator_helm/
cp -a  manifests/charts/istio-control/istio-discovery/ ${path_to_repo}/operator_helm/
```
2. Add values_custom.yaml
