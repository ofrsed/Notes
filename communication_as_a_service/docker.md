docker - это программная платформа для разработки, доставки и запуска контейнерных приложений.

docker image -  Образ (шаблон), куда упакованы все компоненты для раюоты приложения (ОС, программа, доп. библиотеки, настройки, конфиг запуска). Объект только для чтения, контейнер берет из него только ту инфу, которая нужна сейчас, и выполняет в оперативке

Какую проблему решает?
- Не нужно настраивать каждый сервер
- Все взлетает моментально
- Все работает правильно

Контейнер - конкретное запущенное приложение на основе шаблона

У контейнера своя файловая система, своя сеть, безопасность + права, легкая масштабируемость

docker hub - реестр, хранилище image`й

Контейнер может пользоваться интернет соединением хоста

## Разница между Docker и Виртуальной машиной

| Виртуальная машина | Docker контейнер |
| --- | --- |
| Изоляция процесса на аппаратном уровне | Изоляция процесса на уровне ОС |
| Каждая виртуальная машина имеет отдельную ОС | Каждый контейнер может совместно использовать ОС |
| Виртуальные машины занимают несколько ГБ | Контейнеры легкие (КБ / МБ) |
| Низкое быстродействие (виртуальзация ядра) | Отсутствие ядра, быстродейстрие лучше |
| Больше использования ресурса | Меньшее использование ресурсов |


Структура image:
- Образ операционной системы
- Зависимость 1
- Зависисость 2
- Python
- библиотека
- приложение

# Базовые комманды

`docker images` - Перечень images которые есть в системе

`docker run hello-world` - автоматически качается latest. run автоматически создает новый контейнер

`docker run hello-world:1.0.0` - скачать определенную версию

`docker run --rm hello-world:latest` - запуск, чтобы как остановится, автоматичемки удалялся

`docker run --name hello hello-world:latest` - задать имя при запуске

`docker run -d --name server nginx` - `-d` - отсоединенный, запустить в отдельноп процессе, запустить как демон

`docker run -d -p 8000:80 --name server nginx` - порт на хосте будет пробрасываться на порт 80 внутрь контейнера

`docker run -d -p 127.0.0.1:8000:80 --name server nginx` - связываем только localhost

`docker exec -it <идя контейнера> <команду которую нужно выполнить (bash, sh)>` - открыть дополнительный процесс

| REPOSITORY | TAG | IMAGE ID | CREATED | SIZE |
| --- | --- | --- | --- | --- |
| Имя репозитормя | версия | ID | дата создания | размер |

`docker ps` - вывести запущенные контейнеры

`docker ps -a` - вывести все контейнеры

`docker ps -a -q` или `docker ps -aq` - вывести id контейнеров

`docker container inspect <имя контейнера>` - информация конттейнера

| CONTAINER ID | IMAGE | COMMAND | CREATED | STATUS | PORTS | NAMES |
| --- | --- | --- | --- | --- | --- | --- |
| уникальный ID | его image | внутренняя команда, которая была выполнена (она записана в images) | дата создания | Статус (Exited (0) - завершился корректно | порт | имена контейнеров (если не указываем, дается автоматически)|

`docker rm <id или имя>` - удалить контейнер 

`docker rmi <id или имя вместе с тегом>` - удалить image

`docker rm $(docker ps -aq)` - удалить все не работающие контейнеры по списку id

`docker container prune` - удалить все не работающие контейнеры 

`docker system prune` - удалить все 

`docker system prune -a` - удалить все (удалит image)

`docker builder prune` - удалить кэш сборок

`docker start <имя контейнера>` - запуск контейнера (фоново)

`docker start -i <имя контейнера>` - запуск контейнера c с выводом в терминал

`docker logs <имя контейнера>` - логи контейнера

`docker stats` - выводит сколько ресурсов потребляет ваш контейнер

`docker diff <имя контейнера>` - выводит что было добавлено в контейнер

`docker commit <имя контейнера> <имя для image>`

# как уменьшить вес контейнера?
-уменьшить кол0во слоев

# Работа с образами

`docker run -i -t ubuntu` - интерактивный терминал
`docker start -i ubuntu` - зайти в контейнер linux

# Сборка
Dockerfile

```
FROM ubuntu    <- название образа на основе которого собираем
 
RUN apt-get update; \
    apt-get install -y curl   <- название комманд, которые нужно выполнить (-y - автоматическое подтверждение [Y/n]) выполняются во время сборки
```

```
FROM python:3.11.9-alpine    <- название образа на основе которого собираем

WORKDIR /app   <- рабочая директория в контейнере

ENV PYTHONUNBUFFERED=1 <- настройка для python, чтобы STDOUT выводил в терминал все

COPY . .   <- откуда и куда

CMD ["python", "app.py"]    <-  команды выполняются при старте контейнера
```

```
FROM python:3.11.9-alpine    <- название образа на основе которого собираем

WORKDIR /app   <- рабочая директория в контейнере

ENV PYTHONUNBUFFERED=1 <- настройка для python, чтобы STDOUT выводил в терминал все

COPY requirements.txt  . 

RUN pip install --upgrate pip
RUN pip install --no-cache-dir -r requirements.txt      <- чтобы не сохранялся кэш библиотеки (чтобы меньше весил обяз.)

COPY . .   <- откуда и куда

CMD ["python", "app.py"]    <-  команды выполняются при старте контейнера
```


docker build . -t <имя моего образа>:<номер версии> - создать сборку

Docker Compose

`compose.yml`

специальный компонент, который позволяет управлять и создавать одновременно множеством контейнеров. в одной сети

позволяет с помощью файла в формате yml описать создание одного\многих контейнеров и полностью сконфигурировать работу

```
services:
  web:
    image: nginx
    container_name: server
    ports:
      - 127.0.0.1:8000:80
    volumes:
      - ./site:/usr/share/nginx/html
```

`docker compose up -d` - запустить compose
`docker compose down` - остановить


`docker network ls`

-e - переменная окружения

```
NETWORK ID     NAME      DRIVER    SCOPE
5db1778a4da5   bridge    bridge    local  <- помогает объединить контейнеры в одну сеть и предоставить порты на host
66d65ec80785   host      host      local  <- напрямую предоставить доступ к подключению по ip и портам самого хоста (не делат сеть
aa56384cd1ff   none      null      local  <-
```

Делаем сеть
docker network create mynetwork

Запускаем контейнер с монго
docker run --name mymongo --network mynetwork -d mongo

Запускаем контейнер с mongo-express
docker run --name dbbrowser --network mynetwork -e ME_CONFIG_MONGODB_SERVER=mymongo -p 8081:8081 -d mongo-express

Запускаем контейнер checker
docker build -t app ./checker
docker run --name myapp --network mynetwork -d app

Запускаем наш бек/фронт сервис
docker build -t flask ./plot
docker run --name plot --network mynetwork -p 5000:5000 -d flask

```
services:
  mymongo:
    image: mongo
    volumes:
      - ./data:/data/db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=root
      - MONGO_INITDB_ROOT_PASSWORD=example

  dbbrowser:
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=root
      - ME_CONFIG_MONGODB_ADMINPASSWORD=example
      - ME_CONFIG_MONGODB_URL=mongodb://root:example@mymongo:27017/
    depends_on:  #Зависимость от ...
      - mymongo
    
  api:
    build: ./checker  #указываем путь к Dockerfile
    image: app:1.0.0  #имя
    depends_on: 
      - mymongo
  
  web:
    build: ./plot
    image: plot:1.0.0
    ports:
      - 127.0.0.1:5000:5000
    depends_on:
      - api
```
