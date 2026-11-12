# GuestBook Observabilite

## Répartir les pods (Topology Spread Constraints)
Apprendre à repartir les pods via le systme de Topology spread constraints.

### Problème rencontré et pourquoi il est survenu
Je ne sais pas comment ajouter des Topology spread constraints.

### Solution appliquée et pourquoi cette solution fonctionne
J'ai modifié le fichier deployment dans deploy/guestbook/templates/deployment.yaml pour y introduire un bloc de topologySpreadConstraints.
Puis, je drain un de mes deux noeuds, j'observe le status de mon noeud drainé.
Je uncordon le noeud drainé puis je supprime un pod. 
Enfin, je constate que à quels noeuds mes 3 pods appartiennent.

### Ce que j'ai appris
Après la modification du fichier de deployment.yaml, on le relance avec helm :
```
helm upgrade guestbook deploy/guestbook/
```
On peut constater dans quels noeuds sont nos pods :
```
kubectl get pods -o wide
```

Ensuite, on drain un noeud pour voir la repartition :
```
kubectl drain observability-m02 --ignore-daemonsets --delete-emptydir-data
```

Avec cette commande, on peut voir que le noeud drainé est passé au status "Ready,SchedulingDisabled" :
```
kubectl get nodes
```

On constate aussi que nos pods sont tous passés sur le noeud qui a encore le status "Ready".
```
kubectl get pods -o wide
```

Désormais, on "uncordon" le noeud qui a été drainé :
```
kubectl uncordon observability-m02
```

Enfin, on reverifie, les pods liés au noeuds, (si tous les pods sont sur le meme noeuds, alors on peut supprimer un pod pour mieux observer la nouvelle repartition)
Pour supprimer un noeud
```
kubectl delete pods/guestbook-df4bbb97b-29q8s
```

Pour voir la repartition des pods entre les noeuds :
```
kubectl get pods -o wide
```