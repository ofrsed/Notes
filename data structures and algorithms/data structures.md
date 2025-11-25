__Структуры данных__

- ["О" большое](#О-большое)
  - [Линейный поиск](#Линейный-поиск)

- [Массивы](#Массивы)
  - [Статический массив](#Статический-массив)
  - [Динамический массив](#Динамический-массив)
- [Связные списки](#Связные-списки)
  - [Односвязный список](#Односвязный-список)
  - [Двусвязный список](#Двусвязный-список)
- [Очередь](#Очередь)
- [Стеки](#)
- [Деревья](#)
  - [Бинарное дерево](#Бинарное-дерево)
  - [Префиксное нагруженное дерево](#Префиксное-нагруженное-дерево)
- [Графы](#)
- [Множества](#Множества)
- [Боры](#)
- [Хэш-таблицы](#Хэш-таблицы)



# О большое
<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/O.png" title="python" alt="python" width="600"  />;

`О большое` - запись для оценки худшего случая, или для ограничения заданной функции сверху. Это позволяет сделать асимптотическую оценку верхней границы скорости роста времени выполнения алгоритма.


# Линейный поиск

Последовательный перебор пока не найдем искомое значение O(n)



# Бинарный поиск (log n)

```
d = [-1, -3, 2, 4, 5, 7, 8, 9]
n = len(d)
 
search_v = 9
left, right = 0, n-1
 
while left <= right:
    middle = (left + right) // 2
    v = d[middle]
    if v == search_v:
        print(v, middle)
        break
    elif v < search_v:
        left = middle + 1
    elif v > search_v:
        right = middle - 1
else:
    print("значение не найдено")
```

NP - полные задачи. Число всех возможных вариантов = n! (факториал)

# Массивы

## Статический массив
Статический массив - массив, который не изменяет свой размер
1. Все элементы должны быть одного типа данных
2. Фиксированные число элементов
3. Все элементы располагаются в памяти подряд, без пропусков

Преимущества
- Скорость доступа к произвольному элементу О(1) для записи или чтения значения
- Просто реализуется и удобен для небольшого набора данных
Недостатки
- Хранение данных выполняется в непрерывной области памяти. Не всегда эффективно для больших объемов данных
- Не может менять число элементов в процессе работы программы Если зарезервированного места недостаточно, данные могут потеряться
- Вставка и удаление выполняются за О(n)

## Динамический массив
Динамический массив - это массив, который может менять число своих элементов в процессе работы программы. Если массива недостаточно, то создается массив в несколько раз больше предыдущего

Минусы

# Связные списки

## Односвязный список

Односвязный список - элементы ссылаются друг на друга попорядку
<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/%D0%BE%D0%B4%D0%BD%D0%BE%D1%81%D0%B2%D1%8F%D0%B7%D0%BD%D1%8B%D0%B9%20%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA.png" alt="python" width="600"  />;


Добавление в начало
Вставка в центр O(n)
Добавление в конец
Получить по индексу O(n)
Удаление
Добавление в середину

## Двусвязный список
<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/%D0%94%D0%B2%D1%83%D1%81%D0%B2%D1%8F%D0%B7%D0%BD%D1%8B%D0%B9%20%D1%81%D0%BF%D0%B8%D1%81%D0%BE%D0%BA.jpg" alt="python" width="800"  />;

||Команда| Big O |
|-|-|-|
| Добавление в начало | push_front() | O(1) |
| Добавление в конец | push_back() | O(1) |
| Удаление с конца | pop_back() | O(1) |
| Удаление с начала | pop_front() | O(1) |
| Вставка элемента | insert() | O(n) |
| Удаление промежуточных элементов | erase() | O(n) |
| Доступ к элементу | at() | O(n) |


# Очередь
Работает только с граничными элементами
Чаще для них используют двусвязные списки. Называются deque)
в python `from collections import deque`

## FIFO (First In, Forst Out)
Кто первым пришел, первыым и ушел

## LIFO (Last In, First Out)
Последним пришел, первым вышел

# Стек
O(1)
Организован по LIFO, единственное отличий что нельзя обращаться к произвольным элементам.
Та же очередь, но с ограниченным функционалом
В нем возможна работа только с верхними элементами
в python лучше сделать через `from collections import deque`

# Деревья

## Несбалансированное дерево
Подвершины деревьев отличаются более чем на 1 уровень
<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/unbalanced%20tree.png" alt="python" width="600"  />;

- Методы балансировки двоичных деревьев
  - АВЛ-дерево (AVL tree), разработан в 1968 году;
  - красно-черное дерево (red-black tree), разработан в 1972 году;
  - расширяющееся или косое дерево (splay tree), разработан в 1983 году.

## Бинарное дерево
O(log n)
<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/%D0%B1%D0%B8%D0%BD%D0%B0%D1%80%D0%BD%D0%BE%D0%B5%20%D0%B4%D0%B5%D1%80%D0%B5%D0%B2%D0%BE.png" alt="python" width="600"  />;

Дерево — это структура данных, где каждый элемент (называемый узлом) может иметь дочерние элементы.

У дерева есть:
- Корень (root) — верхний узел.
- Ребра (edges) — соединения между узлами.
- Листья (leaves) — узлы без потомков.
- Высота дерева — длина пути от корня до самого глубокого узла.

Правила формирования
- если добавляемое значение меньше значения в родительском узле, то новая вершина добавляет в левую ветвь, иначе – в правую
- если добавляемое значение уже присутствует в дереве, то оно игнорируется (то есть, дубли отсутствуют).

  > если нам известно, что в решаемой задаче данные (значения) поступают в случайном порядке, то в среднем, будет формироваться бинарное дерево близкое к сбалансированному

Способы обхода дерева:
- в ширину (breadth-first)
  - по левой ветви (всегда выдает значения по возрастанию)
  ```
  LNR `левое поддерево (L); промежуточная вершина (N); правое поддерево (R)` # по левой ветви
  
  p = root
  v = [p] #список из вершин текущего уровня в порядке слева-направо
  
  while v:
      vn = []
      for x in v:
          print(x.data)
          if x.left:
              vn += [x.left]
          if x.right:
              vn += [x.right]
      v = vn
  ```
   - по правой (RNL) (выдает значения по убыванию)
   - прочие комбинации

 - в глубину

```
def show_tree(self, node):
    if node is None:
        return
 
    self.show_tree(node.left)
    print(node.data)
    self.show_tree(node.right)

show_tree(root)
```

Удаление вершин бинарного дерева:
  - Удаление листовых вершин
  - удаление узла с одним потомком (правым или левым)
  - Удаление узла с двумя потомками



```
class Node:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None
 
 
class Tree:
    def __init__(self):
        self.root = None
 
    def __find(self, node, parent, value):
        if node is None:
            return None, parent, False
 
        if value == node.data:
            return node, parent, True
 
        if value < node.data:
            if node.left:
                return self.__find(node.left, node, value)
 
        if value > node.data:
            if node.right:
                return self.__find(node.right, node, value)
 
        return node, parent, False
 
    def append(self, obj):
        if self.root is None:
            self.root = obj
            return obj
 
        s, p, fl_find = self.__find(self.root, None, obj.data)
 
        if not fl_find and s:
            if obj.data < s.data:
                s.left = obj
            else:
                s.right = obj
 
        return obj
 
    def show_tree(self, node):
        if node is None:
            return
 
        self.show_tree(node.right)
        print(node.data)
        self.show_tree(node.left)
 
    def show_wide_tree(self, node):
        if node is None:
            return
 
        v = [node]
        while v:
            vn = []
            for x in v:
                print(x.data, end=" ")
                if x.left:
                    vn += [x.left]
                if x.right:
                    vn += [x.right]
            print()
            v = vn
 
    def __del_leaf(self, s, p):
        if p.left == s:
            p.left = None
        elif p.right == s:
            p.right = None
 
    def __del_one_child(self, s, p):
        if p.left == s:
            if s.left is None:
                p.left = s.right
            elif s.right is None:
                p.left = s.left
        elif p.right == s:
            if s.left is None:
                p.right = s.right
            elif s.right is None:
                p.right = s.left
 
    def __find_min(self, node, parent):
        if node.left:
            return self.__find_min(node.left, node)
 
        return node, parent
 
    def del_node(self, key):
        s, p, fl_find = self.__find(self.root, None, key)
 
        if not fl_find:
            return None
 
        if s.left is None and s.right is None:
            self.__del_leaf(s, p)
        elif s.left is None or s.right is None:
            self.__del_one_child(s, p)
        else:
            sr, pr = self.__find_min(s.right, s)
            s.data = sr.data
            self.__del_one_child(sr, pr)
 
 
v = [10, 5, 7, 16, 13, 2, 20]
#v = [20, 5, 24, 2, 16, 11, 18]
 
t = Tree()
for x in v:
    t.append(Node(x))
 
t.del_node(5)
t.show_wide_tree(t.root)
```

# Префиксное нагруженное дерево

<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/prefiksnoe-nagruzhennoe-trie-derevo.jpg" title="python" alt="python" width="500"  />;


  

# Множества
Это коллекция данных, состоящая из уникальных значений

# Хэш-таблицы

<img src="https://github.com/ofrsed/Notes/blob/main/data%20structures%20and%20algorithms/img/hash-funkcii.jpg" title="python" alt="python" width="500"  />;

Хеш-функция - алгоритм преобразования строки в индекс массива
в __Python__ на хеш-таблицах реализован dict и set



- Свойства хеш-функции:
  - для одного и того же ключа (названия товара) должна выдавать одно и то же значение (свойство последовательности);
  - для разных ключей (названий товаров) выдавать разные значения (индексы);
  - формируемые значения должны находиться в диапазоне от 0 до N-1, где N – размер массива, т.е. индексы должны быть действительными для используемой таблицы;
возможные ключи (названия) должны равномерно записываться в ячейки таблицы.

Коллизия - когда хеш-функция преобразует разные входные данные в один индекс
Методы разрешения коллизий:
- Метод цепочек - по разным ключам с одним индектом выходные данные записываются в виде двусвязного списка
- Метод открытой адресации
