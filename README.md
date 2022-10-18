# Вопросы к дипломной работе

## 1. Правильно ли я понял порядок действий создания окружений?
1) Создаём инфраструктуру в двух (`stage` и `prod`) окружениях. (`terraform`).
2) Разворачиваем `k8s` кластера, с одним `namespace`, например `netology`, в каждом из окружений.

## 2. Не получается развернуть `ingress-nginx-controller`
`ingress-nginx-controller` не получает внешний адрес, состояние `<pending>`.
В документации сказано - generally, this is because it doesn't support services of type LoadBalancer.

```shell
kubectl get service ingress-nginx-controller --namespace=ingress-nginx

# NAME                       TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE
# ingress-nginx-controller   LoadBalancer   10.233.9.174   <pending>     80:32685/TCP,443:32410/TCP   3m37s
```

При создании `service` с типом `LoadBalancer` та же проблема.
```shell
kubectl get services -n webapp

# NAME     TYPE           CLUSTER-IP    EXTERNAL-IP   PORT(S)                      AGE
# webapp   LoadBalancer   10.233.23.8   <pending>     80:31443/TCP,443:30069/TCP   7m44s
```
