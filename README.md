# Вопросы к дипломной работе

## Вопрос 1
День добрый. Все таки пришлось развернуть k8s кластер как SaaS, т.к. `Ingress controller for Managed Service for Kubernetes` служит только для SaaS решения, а для кастомного кластера найти что-то подобное в `YC` не удалось.
Но вопрос не об этом. Развернул систему мониторинга с помощью пакета `kube-prometheus`. Через `kubectl --namespace monitoring port-forward svc/grafana 3000` доступ к grafana имеется. Но через `ingress`, ссылающийся на тот же сервис, зайти на grafana не получается (504 Gateway Time-out).
`ingress-nginx-controller` установлен и получил внешний ip адрес (для чистоты эксперимента на него было повешено доменное имя `grafana.netology.asicminer8.com`).

Если тот же `ingress` изменить на работу с моим кастомным приложением, то маршрутизации происходит без проблем. 
Пример настройки на работу с кастомным приложением (`webapp`) закомментирован.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: monitoring
  namespace: monitoring
#  namespace: webapp
spec:
  ingressClassName: nginx
  rules:
  - host: grafana.netology.asicminer8.com
    http:
      paths:
      - backend:
          service:
            name: monitoring
#            name: webapp
            port:
              name: http
        path: /
        pathType: Prefix
```

Сделано всё согласно документации и идей почти не осталось.

## Вопрос 2
Для `jenkins`, как для мастера так и для агентов, создавать отдельные инcтанцы или лучше поместить их в кластер k8s?
Больше склоняюсь к созданию отдельных инстанцов, но все таки хотелось бы уточнить что есть лучше для продакшена.
