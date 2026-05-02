vcluster list
vcluster platform start (start cluster GUI)
sudo vcluster create gfh -f vcluster.yaml 
kubectl apply -f namespace.yaml
kubectl apply -f prometheus-config.yaml
kubectl apply -f prometheus-service.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f grafana-service.yaml
kubectl apply -f grafana-deployment.yaml
kubectl get svc -A
CLUSTER-IP     EXTERNAL-IP   PORT(S)
xx.xx.xx.xx    xx.xx.xx.xx   3000:32042/TCP
xx.xx.xx.xx    xx.xx.xx.xx   9090:30378/TCP
Browse external IP: port (in our case 3000 and 9090)
grafana: admin/admin: need to change password at 1st login
gfh is cluster name
sudo vcluster delete gfh