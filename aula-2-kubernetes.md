## Comandos que eu usei que vi na aula e meu entendimento de cada coisa

```bash

# cria cluster
k3d cluster create meucluster --servers 1 --agents 3

# -p (expoe port do cluter docker para a maquina)
k3d cluster create meucluster --servers 1 --agents 3 -p "8080:30000@loadbalancer"

# exluir cluster
k3d cluster delete meucluster

# lista info das api k8s muito interessante na hora de escrever manifestos k8s como apiVersion/kind
kubectl api-resources

# acessar de forma direta um pod (tbm pode usar para services etc)
kubectl port-forward <POD_NAME> 8080:5000

# historico de deploys feitos
kubectl rollout history deployment conversao-distancia

# forma chique de fazer rollback
kubectl rollout undo deployment conversao-distancia
```

