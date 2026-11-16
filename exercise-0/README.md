# GuestBook Observabilite

## Préparer votre environnement

Créer un cluster qui servira de version d'apprentissage pour les outils de Monitoring (Prometheus, Grafana).

### Ce que j'ai appris
On a crée un cluster minikube de 2 noeuds avec les indications du professeur. On a recrée un guestbook propre et on l'a chargé dans minikube. On a déployé Redis ainsi que le Guestbook.

Via la commande, on vérifie que me guestbook fonctionne et est connecté à Redis :
```
kubectl get pods -n data
```
