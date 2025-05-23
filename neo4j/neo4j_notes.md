# Neo4j

**Neo4j** — это графовая база данных. В отличие от реляционных баз данных, которые используют таблицы для организации данных, графовые базы данных используют вершины (ноды), рёбра (edges), и свойства для представления информации. Neo4j широко применяется в задачах, где важно понимать и анализировать отношения между объектами, например, в социальных сетях, рекомендательных системах и анализе маршрутов.

### Преимущества использования Neo4j
- Гибкость:
   Графовые базы данных идеально подходят для данных с сложными взаимосвязями. С Neo4j можно легко моделировать такие структуры, как социальные сети, связи между пользователями и продуктами.

- Производительность:
   Запросы в графовых базах данных часто быстрее, чем в реляционных, особенно когда нужно работать с большими объёмами данных, где связи между объектами имеют первостепенное значение.

- Логика запросов:
   Cypher позволяет легко выражать сложные запросы для анализа данных, таких как нахождение коротких путей, определение центральных узлов, поиск сообществ и многое другое.

### Основные концепции

1. **Вершины (Nodes)**:
   - Вершины представляют сущности (например, людей, товары, места).
   - В каждой вершине могут храниться данные (свойства), такие как имя, возраст, адрес и т. д.
  
```
cypher

CREATE (person:Person {name: 'Alice', age: 29})
```
   
2. **Рёбра (Relationships)**:
   - Рёбра связывают вершины и представляют собой отношения между ними.
   - Рёбра тоже могут иметь свойства (например, дата начала, тип отношения и т. д.).
  
```
CREATE (alice)-[:FRIEND]->(bob)
```
   
3. **Свойства (Properties)**:
   - Свойства — это пары "ключ-значение", которые можно прикреплять к вершинам или рёбрам. Они используются для хранения информации о сущности или отношении.
  
```
CREATE (alice)-[:FRIEND {since: 2020}]->(bob)
```

4. **Метки (Labels)**:
   - Метки используются для классификации узлов. Например, можно назначить метку "Person" для узлов, представляющих людей, и метку "Product" для узлов, представляющих продукты.
  
```
CREATE (alice:Person {name: 'Alice'})
```
   
5. **Запросы в Cypher**:
   - **Cypher** — это язык запросов, используемый в Neo4j, аналогичный SQL, но с фокусом на графы.
   - Cypher позволяет создавать, читать, обновлять и удалять данные в графе.



### Основные команды Cypher
1. Создание данных:

```
CREATE (person:Person {name: 'Alice', age: 29})
```

2. Чтение данных:

Для чтения данных используется команда MATCH. Можно использовать различные фильтры для поиска данных.

```
MATCH (person:Person {name: 'Alice'}) RETURN person
```

3. Обновление данных:

Для обновления свойств вершины или рёбра используется команда SET.

```
MATCH (person:Person {name: 'Alice'})
SET person.age = 30
```

4. Удаление данных:

Для удаления вершины или рёбора используется команда DELETE.

```
MATCH (person:Person {name: 'Alice'})
DELETE person
```

5. Поиск рёбер между вершинами:

Для поиска рёбер между вершинами используется команда MATCH с указанием направленности рёбер.

```
MATCH (person:Person)-[:FRIEND]->(friend)
RETURN person, friend
```

### Индексы и уникальные ограничения

1. Индексы:

Индексы ускоряют поиск данных по определённым свойствам. Например, можно создать индекс на имя человека, чтобы ускорить запросы.

```
CREATE INDEX ON :Person(name)
```
2. Уникальные ограничения:

Уникальные ограничения гарантируют, что значение свойства будет уникальным в графе.

```
CREATE CONSTRAINT ON (p:Person) ASSERT p.email IS UNIQUE
```

