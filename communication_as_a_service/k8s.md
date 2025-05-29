base:
- Кластер - это группа серверов (нод), которые работают вместе как единая система
- Pod -  минимальная единица запуска. Обычно содержит один контейнер, но может быть несколько.


| Команда  | Действие |
| --- | --- |
| `minikube version` | --- |
| `minikube start` | --- |
| `minikube start --cpus=4 --memory=8gb --disk-size=25gb` | --- |
| `minikube start --driver=docker` | --- |
| `minikube stop` | --- |
| `minikube delete`  | --- |
| `minikube ssh` | подключиться |


| Команда  | Действие |
| --- | --- |
| `kubectl version` | Версия клиента и сервера |
| `kubectl version --client` | Версия клиента |
| `kubectl get componentstatuses` | Показать состояние k8s cluster`a |
| `kubectl cluster-info` | Показать информацию о k8s cluster`a |
| `kubectl get nodes` | Показать все сервера k8s cluster`a  |



