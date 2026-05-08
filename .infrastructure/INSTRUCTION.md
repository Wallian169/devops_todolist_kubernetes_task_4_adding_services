
## Testing an App Using ClusterIP Service DNS from a Busybox Container

### Prerequisites:
- Make sure kubectl is runnoing on your local machine.
- Apply namespace  `todoapp` from namespace.yml

```bash 
kubectl apply -f .infrastructure/namespace.yml
kubectl apply -f .infrastructure/
```
- set default namespace:
```bash
kubectl config set-context --current --namespace=todoapp
```

### How to test an app by calling a ClusterIP service DNS from a busybox container

1. Enter busybox container interactive shell:
```bash
kubectl exec -it busybox -- sh 
```
2. Run curl command to access the cluster IP service:
```bash
# for imdex page
curl http://todoapp-service.todoapp.svc.cluster.local:8080/
# API 
curl http://todoapp-service.todoapp.svc.cluster.local:8080/api/
```
### How to test an app with port forwarding

1. Ensure todoapp-service is running:

```bash
kubectl get svc -o wide
```
2. Forward ClusterIP to your local machine

```bash 
kubectl port-forward services/todoapp-service 8081:8080
```