1. There are two ways to get operator manifests

  a) Download generated manifests from the repo and change image docker registry and version
    - https://raw.githubusercontent.com/istio/istio/${VERSION}/manifests/charts/istio-operator/crds/crd-operator.yaml
    - https://raw.githubusercontent.com/istio/istio/${VERSION}/manifests/charts/istio-operator/files/gen-operator.yaml

  b) Use helm template
  ```
  cd /tmp
  export ISTIO_VERSION=1.9.9
  curl -L https://istio.io/downloadIstio | TARGET_ARCH=x86_64 sh -
  cd istio-$ISTIO_VERSION
  helm template manifests/charts/istio-operator/ --set hub=docker.io/istio --set tag=$ISTIO_VERSION --set operatorNamespace=istio-operator --set istioNamespace=istio-system --set enableCRDTemplates=true > /tmp/gen-operator.yaml
  cp manifests/charts/istio-operator/crds/crd-operator.yaml  ${path_to_repo}/operator_kustomize/base/crd-operator.yaml
  cp /tmp/gen-operator.yaml  ${path_to_repo}/operator_kustomize/base/gen-operator.yaml
```
2. create overlays (/dev/overrides)
3. generate kustomization.yaml (depend on way from p.1)

Note! Do not set namespace because istio-operator should be installed to instio-system namespace.
