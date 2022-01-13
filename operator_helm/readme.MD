1. Generate helm chart:
```
cd /tmp
export ISTIO_VERSION=1.9.9
curl -L https://istio.io/downloadIstio | TARGET_ARCH=x86_64 sh -
cd istio-$ISTIO_VERSION
cp -a  manifests/charts/istio-operator/* ${path_to_repo}/operator_helm/
```
2. Add templates/istiooperator.yaml
