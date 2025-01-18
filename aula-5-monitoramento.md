- Copiar o `deployment.yml` do prometheus e fazer deploy
- Prometheus foi feito para cloud
- secrets não são tão seguras assim, pq para pegar a senha do grafana podemos usar esse comando

```
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

```