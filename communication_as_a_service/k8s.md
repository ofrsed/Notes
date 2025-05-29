Основные понятия:
- Кластер - это группа серверов (нод), которые работают вместе как единая система
- Pod -  минимальная единица запуска. Обычно содержит один контейнер, но может быть несколько.
- Node - физический или виртуальный сервер, на котором работают Pod'ы
- Cluster - совокупность всех нод, управляемая одним Control Plane.
- Kubelet - программа (агент), установленная на ноде.
- kubectl - команда в терминале (утилита), через которую отправляются команды в кластер.

Объекты:
- Deployment - управляет созданием и обновлением Pod'ов
- Service - объект, обеспечивающий стабильный доступ к Pod'ам по IP/имени.
- Ingress - объект для маршрутизации HTTP/HTTPS-запросов (например, по домену или пути).
- ConfigMap / Secret -  объекты, в которых хранятся настройки и секреты (в виде ключ-значение).
- Volume - объект, описывающий подключаемое хранилище.
- Namespace  - логическая область в кластере для изоляции ресурсов.

Главные объекты:

0. Container
1. Pod
2. Deployment
3. Service
4. Nodes
5. Cluster



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
| `kubectl apply -f файл.yaml` | применить |




