# GuestBook Observabilite

## Déployer la stack Prometheus
Déployer la stack Prometheus avec Grafana via Helm, en la configurant avec Minikube

### Ce que j'ai appris
```
kubectl get pods -n monitoring -w
```

```
kubectl get secret -n monitoring prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

```
kubectl port-forward -n monitoring svc/prometheus-grafana 8080:80
```
