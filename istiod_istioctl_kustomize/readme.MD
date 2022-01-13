1. Check istioctl client verson with `istioctl version`
    - install istioctl if it is neaded or your version is wrong
    ``` 
    curl -sL https://istio.io/downloadIstioctl | ISTIO_VERSION=1.9.9 sh -
    export PATH=$PATH:$HOME/.istioctl/bin
    ```
2. Generate manifest with from `istiod_istioctl` dir:
    `istioctl manifest generate -f istiooperator.yaml  > base/istiod.yaml`
