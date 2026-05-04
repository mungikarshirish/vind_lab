vcluster list
vcluster platform start (start cluster GUI)
sudo vcluster create gp-helm -f vcluster.yaml 
kubectl apply -f namespace.yaml
helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace monitoring -f values.yaml 
Get Grafana 'admin' user password by running: 
    kubectl --namespace monitoring get secrets prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 -d ; echo
kubectl get svc -n monitoring | grep Load
    prometheus-stack-grafana                    LoadBalancer   xx.xx.xx.xx   80:31376/TC
    prometheus-stack-kube-prom-prometheus       LoadBalancer   xx.xx.xx.xx   90:31546/TCP,8080:30219/TCP

helm uninstall prometheus-stack -n monitoring
Manual Cleanup (Post-Uninstall)
    Helm does not automatically remove all resources to protect data. For a complete removal, manual cleanup is required:
        CRDs: Delete the remaining Custom Resource Definitions, such as alertmanagers.monitoring.coreos.com and prometheuses.monitoring.coreos.com.
        PVCs: Remove Persistent Volume Claims (pvc) linked to the release.
        Secrets/Services: Check for and delete residual admission secrets or services (kubelet) in the monitoring or kube-system namespaces.

Verify removal by checking all namespaces for the release
helm list -A

gp-helm is cluster name
sudo vcluster delete gp-helm