vcluster list
vcluster platform start (start cluster GUI)
sudo vcluster create gfh -f vcluster.yaml 
kubectl apply -f namespace.yaml
kubectl apply -f prometheus-config.yaml
kubectl apply -f prometheus-service*.yaml
kubectl apply -f prometheus-deployment.yaml
kubectl apply -f grafana-service*.yaml
kubectl apply -f grafana-deployment.yaml

kubectl get all -A

if you use lb files kubectl get svc -A
TYPE           EXTERNAL-IP      PORT(S)
LoadBalancer   xx.xx.xx.xx      3000:32000/TCP
LoadBalancer   xx.xx.xx.xx      9090:30000/TCP

Browse external IP: port (in our case 3000 and 9090)

grafana: admin/admin: need to change password at 1st login
Connect Data Source: In Grafana, add a new "Prometheus" data source and set the URL to http://xx.xx.xx.xx:9090
click on save and test, Drilldown > Metrics

if you use npe files
kubectl port-forward svc/grafana 3000:3000 -n monitoring (keep window open)
kubectl port-forward svc/prometheus-service 9090:9090 -n monitoring (keep window open)

kubectl get all -A

TYPE        PORT(S)
NodePort    3000:32000/TCP
NodePort    9090:30000/TCP

Browse localhost: port (in our case 3000 and 9090)

grafana: admin/admin: need to change password at 1st login
Connect Data Source: In Grafana, add a new "Prometheus" data source and set the URL to http://prometheus-service:9090
click on save and test, Drilldown > Metrics

gfh is cluster name
sudo vcluster delete gfh