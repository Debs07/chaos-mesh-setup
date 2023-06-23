- Install chaos mesh using helm

```
helm repo add chaos-mesh https://charts.chaos-mesh.org
helm repo update
helm install chaos-mesh chaos-mesh/chaos-mesh --namespace=chaos-testing --create-namespace --set dashboard.create=true
```

Replace the NodePort service with an LB service to avoid getting blocked by zscaler:

```
kubectl delete svc -n chaos-testing chaos-dashboard
kubectl apply -f ./lb-service.yaml 
```

Install RBAC to generate token for login:

```
kubectl apply -f rbac.yaml
```

Get token for login:

```
kubectl create token account-default-viewer-zfhpn
```

Get address for web UI:

```
echo $(kubectl get svc chaos-dashboard | awk {'print $4'} | grep amazon )
```
