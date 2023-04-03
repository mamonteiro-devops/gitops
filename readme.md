
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
    
    cd /home/mamonteiro/manuel.monteiro.github/helm-apps/argo-cd
    k create ns argocd
    helm install argocd-cluster . --namespace argocd
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
    kubectl port-forward service/argocd-cluster-server -n argocd 8080:443
    
## Install Strimzi operator
    k create ns strimzi-operator
    k create ns strimzi
    cd /home/mamonteiro/manuel.monteiro.github/helm-apps/strimzi/strimzi-kafka-operator
    helm install strimzi . --namespace strimzi-operator
    
    or 
    cd /home/mamonteiro/manuel.monteiro.github/gitops/
    k apply -f kafka-strimzi-operator-with-argocd.yaml


## Install Kafka cluster
    k create ns kafka

    ## srill not working
    kubectl apply -f strimzi-Helm-cluster.yaml -n argocd

    cd /home/mamonteiro/manuel.monteiro.github/kafka/strimzi
    k apply -f kafka-persistent-single.yaml -n kafka

## Install kafka-ui
```
    k create ns kafka-ui
    helm install kafka-ui charts/kafka-ui --namespace kafka-ui
    ### obviously needs to be configured with the kafka cluster
    
```
## Install Prometheus and  Grafana
Link Extra: https://github.com/naturalett/continuous-delivery
            \
            https://dzone.com/articles/deploying-prometheus-and-grafana-as-applications-u

```
cd /home/mamonteiro/manuel.monteiro.github/helm-apps/prom-graf/kube-prometheus-stack
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install my-kube-prometheus-stack prometheus-community/kube-prometheus-stack --version 45.8.1 --namespace monitoring
helm install my-grafana grafana/grafana --version 6.17.11 --namespace monitoring
```



## Install Alert Manager 
```
    --- NOT TESTED ---
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo update
    helm install my-alertmanager prometheus-community/alertmanager --version 0.27.0 --namespace monitoring
    kubectl port-forward service/my-alertmanager-alertmanager -n monitoring 9093:9093
```


## Install Kiali
## Install Jaeger
## Install Istio
## Install OPenTelemetry
## Install OPA

## Install efk
```
    
    Path: https://github.com/scriptcamp/kubernetes-efk
    cd /home/mamonteiro/manuel.monteiro.github/helm-apps/kubernetes-efk
    kubectl apply -f . -n logging
    kubectl rollout restart ds -n logging
    
    Note: Is using fluentd AND NOT fluentbit, NEEDS TO BE CHANGED
    
```

## Install cert-manager
## Install nginx-ingress

## Install GitOps apps
```
    k create ns gitops-examples
    Source is here : /home/mamonteiro/manuel.monteiro.github/helm-apps/strimzi-jaeger-eval
    k apply -f application-topics.yaml
```

## Install keda


