### falco sidekick blog
    https://falco.org/blog/extend-falco-outputs-with-falcosidekick/

### new blog
    https://falco.org/blog/falcosidekick-2-29-0/

### helm installation
    kubectl create namespace falco
    helm repo add falcosecurity https://falcosecurity.github.io/charts
    helm install falco falcosecurity/falco \
    --set falcosidekick.enabled=true \
    --set falcosidekick.webui.enabled=true \
    -n falco 

### for testing change svc type for NodePort
    kubectl -n falco get all
    kubectl edit -n falco svc falco-falcosidekick-ui