Python

## Типы данных в python
Неизменяемые: int , float, string, bool, frozen set
Изменяемые: списки ( list ), словари ( dict ) и множества ( set )

## Что такое Python?
Python — высокоуровневый язык программирования с динамической типизацией.
(типы переменных определяются во время выполнения)
## Чем is отличается от двойного равенства (==)?
«==» сравнивает значения, а «is» проверяет, указывают ли объекты на одну и ту же область памяти


## Чем многопоточное приложение отличается от многопроцессорного?
Многопоточные приложения выполняются в рамках одного процесса, но разделены на потоки. Это значит, что каждый поток имеет доступ к общим ресурсам: файлам, памяти, сети и ресурсам машины. Многопроцессорные приложения делятся на отдельные процессы. У каждого собственный изолированный набор ресурсов.
В Python для реализации многопроцессорного подхода используют библиотеки concurrent.futures и multiprocessing, а для многопоточности — threading.


## Что такое aiohttp?
это асинхронный клиентский HTTP-сервер для платформы Python. 
Поддерживает Python версии выше 3.5 и использует библиотеку asyncio. Имеет ряд функций, которые помогают ускорить и повысить эффективность обработки запросов и результатов.

## Асинхронность
слово async идет до def, чтобы показать, что метод является асинхронным. 
слово await показывает, что вы ожидаете завершения сопрограммы.

## Что такое корутина 
Блок кода который работает асинхронно
## Чем корутина отличается от потока?
Корутины не требуют переключения контекста, поэтому код потребляет мало ресурсов. Потоки выполняются на аппаратном или системном уровне. Корутины — более высокоуровневое решение.
## Что такое REST
REST (Representational state transfer «передача состояния представления») – соглашение о том, как выстраивать сервисы. 
веб-приложение с набором урлов – конечных точек. Урлы принимают и возвращают данные в формате JSON. Тип операции задают методом HTTP-запроса, например:
GET – получить объект или список объектов
POST – создать объект
PUT – обновить существующий объект
PATCH – частично обновить существующий объект
DELETE – удалить объект

HEAD – получить метаданные объекта

1.	Единообразие интерфейса
2.	Клиент-сервер
3.	Отсутствие состояния
4.	Кэширование
5.	Слои
6.	Код по требованию (необязательное ограничение)

## Чем пакеты отличаются от модулей?
Пакет представляет собой коллекцию модулей, а модуль — файл или набор файлов.
## Что такое лямбда-функция?
Анонимная функция
## Что такое интерфейс?
Интерфейс — это набор инструментов, который позволяет пользователю взаимодействовать с программой.
Общее

## Какие принципы программирования вы знаете
`SOLID`
- S: Single Responsibility Principle (Принцип единственной ответственности). - Каждый класс должен решать лишь одну задачу.
- O: Open-Closed Principle (Принцип открытости-закрытости). - Программные сущности (классы, модули, функции) должны быть открыты для расширения, но не для модификации.
- L: Liskov Substitution Principle (Принцип подстановки Барбары Лисков). - Необходимо, чтобы подклассы могли бы служить заменой для своих суперклассов.
- I: Interface Segregation Principle (Принцип разделения интерфейса). - Создавайте узкоспециализированные интерфейсы, предназначенные для конкретного клиента. Клиенты не должны зависеть от интерфейсов, которые они не используют.
- D: Dependency Inversion Principle (Принцип инверсии зависимостей). - объектом зависимости должна быть абстракция, а не что-то конкретное.

`YAGNI`
You Aren’t Gonna Need It («Тебе это не понадобится») нежелательно оставлять в продакшене «точки расширения» 

`DRY `
Don’t Repeat Yourself («Не повторяйся»)  - каждое повторяемое поведение в коде следует обособлять для возможности многократного использования
`KISS`
Keep It Stupid Simple («Придерживайся простоты») - следить за тем, чтобы код оставался как можно более простым

Docker
## Что такое docker?
Docker — это открытая платформа с помощью которой разработчики могут создавать, упаковывать, доставлять и запускать приложения в виде легких, портативных, самодостаточных контейнеров
## Что такое контейнер Docker?
Контейнер — базовая единица программного обеспечения, покрывающая код и все его зависимости для обеспечения запуска приложения независимо от окружения
Контейнер Docker может быть создан с использованием образа Docker. Это исполняемый пакет программного обеспечения, содержащий все необходимое для запуска приложения, например, системные программы, библиотеки, код, среды исполнения и настройки.
## Опишите составные части архитектуры Docker
сервер, содержит сервис Docker, образы и контейнеры. Сервис связывается с Registry, образы — метаданные приложений, запускаемых в контейнерах Docker.
клиент, применяется для запуска различных действий на сервере Docker.
registry, используется для хранения образов. Есть публичные, доступные каждому, например, Docker Hub и Docker Cloud.
Назовите наиболее важные команды Docker
build, сборка образа для Docker
create, создание нового контейнера
kill. принудительная остановка контейнера
dockerd, запуск сервиса Docker
commit, создание нового образа из изменений в контейнере
## Как определить состояние контейнера Docker?
docker ps –a  - Эта команда выведет список всех доступных контейнеров с их состоянием на сервере. Из этого списка нужно выбрать требуемый контейнер и узнать его состояние.
## Что такое Dockerfile?
Dockerfile содержит инструкции для сборки образов, которые передаются в Docker. 
Текстовый документ, содержащий все возможные команды, с помощью которых пользователь, последовательно их запуская, может собрать образ.
## как ускорить сборку Docker-образов
Уменьшаем контекст 
Или .dockerignore, или положить все файлы, нужные для сборки в отдельную папку
Использовать родительский образ Alpine

Базы данных
Как в postgresql можно заблокировать на изменение получены сороки
Блокировки на уровне таблицы
LOCK TABLE my_table IN SHARE MODE;

13.3.2. Блокировки на уровне строк
SELECT * FROM employees WHERE id = 40 FOR UPDATE;

13.3.3. Блокировки на уровне страниц
Джоины
 


какая временная сложность взятия элемента по ключу из словаря в худшем случае?
В худшем случае, когда все ключи хэшируются в одно и то же значение (например, если используется плохая хэш-функция или большое количество коллизий), доступ к элементу по ключу потребует просмотра всех элементов, что делает время выполнения линейным относительно количества элементов в хэш-таблице, то есть O(n).
В общем случае, при хорошо спроектированной хэш-таблице, сложность доступа к элементу по ключу составляет O(1) в среднем случае и O(n) в худшем случае.
