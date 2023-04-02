
## Install EKS ou K3d Cluster (or several clusters)
    ### K3d
        k3d cluster create multiserver --servers 1 --agents 9

    ### EKS
        eksctl create cluster \
        --version 1.23 \
        --region us-east-1 \
        --node-type t3.medium \
        --nodes 9 \
        --nodes-min 1 \
        --nodes-max 9 \
        --name strimzi-cluster

## Install ArgoCD
    k create ns argocd
    helm install argocd-cluster . --namespace argocd
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
    zcEXOH7QcS0c6Th4
    kubectl port-forward service/argocd-cluster-server -n argocd 8080:443
    
## Install Strimzi operator
    
    
## Install Kafka
## Install Prometheus
## Install Grafana
## Install Kiali
## Install Jaeger
## Install Istio
## Install OPenTelemetry
## Install OPA
## Install efk
## Install cert-manager
## Install nginx-ingress
## Install GitOps
    ### 
## Install keda



helm repo add argo https://argoproj.github.io/argo-helm
helm install my-argo-cd argo/argo-cd --version 5.27.5

kubectl -n default get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

helm install argocd-v1 . --namespace argo
CW62Ls5BxNHQLFjg%

kubectl port-forward service/argocd-v1-server -n argo 8080:443


https://artifacthub.io/packages/helm/argo/argo-cd

https://dzone.com/articles/deploying-prometheus-and-grafana-as-applications-u

