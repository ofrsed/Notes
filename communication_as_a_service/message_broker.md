![image](https://github.com/user-attachments/assets/5b924afc-25a3-43e1-a7db-40a35c6be79a)

Брокер сообщений - это сервис, который может хранить сообщения в упорядоченном виде, в который кто-то (producer, publisher) может отправить сообщение (enqueue), а кто-то (consumer, subscriber) его оттуда прочитать (dequeue).

__Publisher__ - (паблишер, издатель - от английского publish - публиковать), producer - это тот, кто публикует сообщение в RabbitMQ. Это может быть вообще любой сервис, который хочет связаться с любым другим сервисом с помощью брокера сообщений.

Publisher создаёт соединение (connection) по протоколу AMQP, и в рамках соединения создаёт канал (channel). Если обратиться к в веб-интерфейсу RabbitMQ, то можно увидеть вкладки Connections и Channels, в которых будут отображаться соединения и каналы, создаваемые паблишерами. В рамках одного соединения паблишер может создавать несколько каналов, но так делать не рекомендуется из-за возможного снижения производительности, потенциальных конфликтов, сложности отладки и т.п. Хорошая практика - на одно соединение один канал.

__Exchange__ - точка обмена, обменник, эксчейндж - базовая сущность RabbitMQ, отвечающая за машрутизацию всех сообщений от всех паблишеров. Паблишеры помещают свои сообщения в exchange, а уже оттуда они распределяются по дальнейшим компонентам системы.

Нужно отметить три важные особенности точек обмена:
1. Все сообщения от паблишеров всегда попадают сначала в exchange.
2. Если маршрута для сообщения нет, то сообщение будет удалено из системы. Exchange не подразумевает хранения сообщений, только их маршрутизацию.
3. Точек обмена может быть много в системе. Есть обменники по умолчанию и можно создавать кастомные.


__Binding__ (привязка) - связь между точками обмена и очередями, статический маршрут. Задача этой сущности направлять сообщения из exchange в определенную очередь. С помощью привязок можно создавать сложные схемы маршрутизации сообщений и управлять тем, как сообщения доставляются и обрабатываются в системе.

Queue - очередь. Отвечает за хранение сообщений. Информация об очередях, имеющихся в RabbitMQ на текущий момент, доступна во вкладке Queues and Streams веб-интерфейса и здесь же вручную можно добавлять новые очереди

__Message__ - сообщение - основная базовая сущность в рамках брокеров сообщений, отвечающая, за полезную информацию, которую нужно передать с помощью брокера. Собственно, это тот компонент, вокруг которого существует вся система. Сообщение проходит через все этапы обработки от паблишера к консьюмеру.

Возможно, термин "сообщение" может создать немного неверное представление о том, какая информация может быть передана с помощью RabbitMQ. Часто мы представляем себе какие-то осмысленные строки, когда говорим о сообщениях. И хотя через брокер очень часто передаются строковые сообщения, это не значит, что сервис может работать только с ними. Это также могут быть просто наборы байтов, с помощью которых можно передавать любые объекты: хоть картинки, хоть звук, хоть видео. Правда, нужно иметь в виду, что чем больше такие сообщения по объему, тем больше задержки в очередях, ведь для того, чтобы взять в обработку следующее сообщение, сначала нужно обработать текущее. Ну, и есть лимиты и рекомендации на размер сообщений.

__Consumer__ (консьюмер, получатель, подписчик, subscriber) - сущность, получающая сообщения из очереди для того, чтобы что-то, в связи с этим, сделать. Consumer, как и publisher создает соединение, а внутри него канал. Консьюмер может подписаться только на одну очередь и при появлении в этой очереди сообщения, RabbitMQ отправляет сообщение консьюмеру.

Для подтверждения обработки сообщения консьюмером существует механизм Acknowledge (ack), а также механизм возвращения сообщения обратно в очередь при неудачной обработке - Negative acknowledge (nack). Механизм nack также срабатывает автоматически при разрушении канала с консьюмером. Это дает дополнительную гарантию того, что сообщение будет обработано консьюмером, даже если он временно недоступен и сообщение потерялось по пути.


Маршрутизация. 

- __Direct Exchange__ - Такая точка направляет сообщения в очередь на основе точного совпадения ключа маршрутизации (routing key)
- __Fanout Exchange__ - Данный тип отвечает за то, что сообщения попадают во все, связанные с точкой обмена, очереди, игнорируя ключи маршрутизации и в сообщениях, и в привязках. (самый быстрый)
- __Topic Exchange__ - Они похожи на тип direct, только не по полному совпадению ключа маршрутизации, а по "маске" ключа.
  Решётка # заменяет любое количество слов в ключе, а звездочка * какое-то одно. 
  `<region>.<section>.<user_type>`
    - eu.*.free_user - в очередь будут попадать любые новости eu-региона для бесплатных пользователей
    - ru.# - в очередь будут попадать любые новости ru-региона для любых пользователей
    - *.culture.* - в очередь будут попадать новости культуры любого региона, адресованные пользователям всех типов
    - /# в очередь будут попадать сообщения с любыми ключами

# RabbitMQ

Для Python:
  - Синхронная: pika
  - Асинхронная: aiormq

import asyncio

import aiormq
from aiormq.abc import DeliveredMessage


# Callback-функция, вызываемая на каждое сообщение для консьюмера
async def on_message(message: DeliveredMessage):
    print(message.body.decode())

    # Явное подтверждение получения и обработки сообщения
    await message.channel.basic_ack(delivery_tag=message.delivery.delivery_tag)

publisher.py

```
import asyncio
import aiormq


async def publish():
    # Подключение к RabbitMQ
    connection = await aiormq.connect("amqp://rabbitmqlogin:rabbitmqpassword@localhost/")

    # Создание канала
    channel = await connection.channel()

    # Объявление точки обмена (создается, если не существует)
    await channel.exchange_declare("test_exchange", exchange_type="direct")

    # Отправка сообщения в exchange
    await channel.basic_publish(
        body="Привет из RabbitMQ!".encode('utf-8'),
        exchange="test_exchange",
        routing_key="test_routing_key"
    )

    # Закрытие соединения
    await connection.close()


asyncio.run(publish())
```

consumer.py

```
async def main():
    # Подключение к RabbitMQ
    connection = await aiormq.connect("amqp://rabbitmqlogin:rabbitmqpassword@localhost/")

    # Создание канала
    channel = await connection.channel()

    # Объявление точки обмена (создается, если не существует)
    await channel.exchange_declare("test_exchange", exchange_type="direct")

    # Объявление очереди (создается, если не существует)
    declare_ok = await channel.queue_declare('test_queue')

    # Привязка очереди к точке обмена
    await channel.queue_bind(
        queue=declare_ok.queue,
        exchange="test_exchange",
        routing_key="test_routing_key"
    )

    # Определение количества сообщений, которые консьюмер может получить за один раз
    await channel.basic_qos(prefetch_count=1)

    # Настройка прослушивания очереди
    await channel.basic_consume(declare_ok.queue, on_message, no_ack=False)

    # Создание бесконечного цикла для ожидания сообщений для консьюмера из очереди
    await asyncio.Future()


asyncio.run(main())
```

`image: "heidiks/rabbitmq-delayed-message-exchange:latest"` - отложенные сообщения


# Apache Kafka

![image](https://github.com/user-attachments/assets/aa6cc778-d991-425f-91af-a92f4542b437)



![image](https://github.com/user-attachments/assets/60122123-4a27-4616-bfb7-565ee47e9093)

Продьюсеры:
- По умолчанию продьюсеры используют стратегию Round-Robin для записи сообщений в партиции топика: сначала в партицию 0, затем в 1 и так далее.
- Ключ сообщения (key) — это опциональный элемент, который позволяет продьюсеру определять, в какую партицию будет записано сообщение. Это особенно полезно для логики, которая требует отправки связанных сообщений в одну и ту же партицию (например, все сообщения для одного пользователя).

Оффсет:
- Оффсет (offset) — это порядковый номер сообщения в партиции, который служит для указания его позиции в логах.

Форматы сообщений:
- Для передачи данных через Kafka часто используются форматы JSON, AVRO и Protobuf. Рекомендуется использовать один формат и структуру сообщений в рамках одного топика.

Репликация:
- Коэффициент репликации (replication factor) — это количество копий каждой партиции, включая основную партицию.

В Kafka есть два типа реплик: "in-sync" (синхронизированные) и "out-of-sync" (не синхронизированные).
- Реплика считается out-of-sync, если она не запрашивает сообщения у ведущей более 10 секунд (это настраивается с помощью replica.lag.time.max.ms) или отстала на N сообщений (если настроен параметр replica.lag.max.messages).
- Важно: Коэффициент репликации не может превышать количество брокеров в кластере.

Батчи и Сжатие:
- Батч (batch) — это группа сообщений, которые отправляются как единое целое для повышения производительности.

Сжатие:
- None — не рекомендуется.
- lz4 — лучший вариант по производительности.
- gzip — высокое сжатие, но нагрузка на процессор.
- zstd — компромисс между сжатием и нагрузкой на процессор.

Файлы:
- .log — файл, содержащий сообщения.
- .index — индексный файл, содержащий пары "offset" и "position".
- .timeindex — индекс, связывающий "CreateTime" и "offset".

Команды:

Создание топика:
`bin/kafka-topics.sh --create --topic test.kafka.topic --bootstrap-server localhost:9092`

Создание продьюсера:
`bin/kafka-console-producer.sh --topic orders.status --bootstrap-server localhost:9092`

Заголовки:
- Заголовки сообщений — это метаданные, которые можно добавить без изменения основного содержания сообщения (ключа и значения).
