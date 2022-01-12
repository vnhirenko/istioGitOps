1. There are two ways to get operator manifests

  a) Download generated manifests from the repo and change image docker registry and version and remove autoscaling config if it is needed and set number of istiod replicas
    - https://raw.githubusercontent.com/istio/istio/1.9.9/manifests/charts/base/files/gen-istio-cluster.yaml
    - https://github.com/istio/istio/blob/1.9.9/manifests/charts/istio-control/istio-discovery/files/gen-istio.yaml

  b) Use helm template
  ```
  cd /tmp
  export ISTIO_VERSION=1.9.9
  curl -L https://istio.io/downloadIstio | TARGET_ARCH=x86_64 sh -
  cd istio-$ISTIO_VERSION
  helm template --release-name istio manifests/charts/base/ --set base.enableCRDTemplates=true > /tmp/gen-istio-cluster.yaml
  helm template --release-name istio --namespace istio-system -f ${path_to_repo}/istiod_kustomize/values_custom.yaml manifests/charts/istio-control/istio-discovery/ > /tmp/gen-istio.yaml

  cp /tmp/gen-istio.yaml ${path_to_repo}/istiod_kustomize/base/gen-istio.yaml
  cp /tmp/gen-istio-cluster.yaml ${path_to_repo}/istiod_kustomize/base/gen-istio-cluster.yaml
```
3. generate kustomization.yaml (depend on way from p.1)
