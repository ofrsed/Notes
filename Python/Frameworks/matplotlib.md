- Установка `pip install matplotlib`

- Импорт `import matplotlib.pyplot as plt`

- Обновление библиотеки `pip install --upgrade matplotlib`

абцисса - х
ордината - y

y = np.array([1,2,3,4,5])


matplotlib.use('') - задать бекэнд

print(matplotlib.get_backend()) - получить бекэнд

![image](https://github.com/user-attachments/assets/5bdd2979-3b4b-4cfd-8b8b-0532b0921017)

```
lines = plt.plot(x, y)
plt.setp(lines, linestyle='-.')
```

- `plt.figure(figsize=(7,4))` - создать фигуру

- `plt.title('График зависимости признаков х и у', fontsize=18, color='red', alpha=0.6)` - отображение заголовка

- `plt.xlabel()` и `plt.ylabel(rotation=0, fontsize=14, color='red', labelpad=20)` - задать названия осям

`plt.xlim()` и `plt.ylim(0,26)` - применяются для изменения размерности осей графика. Этим функциям передаются два числа - начало и конец того диапазона, который мы хотим видеть на нашем графике.

`plt.xticks()` и `plt.yticks(rotation=90)` - принудительно установить свои значения на осях графика.

`plt.fill_between(x, y, 0.5, where=(y < 0), color='r', alpha=0.5)` - заливка областей графика 

`plt.style.use('Solarize_Light2')` - стилизация вывода графиков (print(plt.style.available) - все стили)

`plt.grid(color='green', linestyle='--', linewidth=1)` - добавить сетку

`plt.legend()` - вывести легенду
  - `loc=2` - положение
    - 'best' или 0
    - 'upper right'  или 1
    - 'upper left'  или 2
    - 'lower left' или 3
    - 'lower right' или 4
    - 'right' или 5
    - 'center left' или 6
    - 'center right' или 7
    - 'lower center' или 8
    - 'upper center' или 9
    - 'center' или 10
  - если передать кортеж - положение относительнно X и Y
  - `title='Cities'` - название заголовка


### Работа с графиком

- `plt.plot(X=Индексы, Y, "--",)` - отображает двумерные графики
  - `Y` - Множество точек по координате Y (X - индексы ячеек)
  - "--" - тип линиий
    - "-" - Непрерывная линия (используется по умолчанию)
    - "--" - Штриховая линия
    - "-." - Штрихпунктирная линия
    - ":" - Пунктирная линия
    - "None" или " " - Без рисования линии
  - `"--r"` или `"r--"` или `color='g'` или `color='#0000CC'` или `color=(R,G,B, alpha=None)` - указать цвет
  - `"--o"` или `"--s"` или `markers="+"` - задать маркеры 
    - [Маркеры](https://matplotlib.org/stable/api/markers_api.html)
  - `markerfacecolor='w'` - указать цвет заливки маркера
  - `markersize=4` - изменить размер маркера
  - `markeredgecolor=yellow` - внешний контур
  - `markeredgewidth=3` - размер внешнего контура
  - `markerfacecolor='green'` - заполнить внутреннюю поверхность маркера каким-либо другим цветом.
  - `linewidth=4` - толщина линии
  - `alpha=4` - прозрачность
  - `label='x1_y1'` - название для меток легенды
  - [Остальные параметры](https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.plot.html)
     
`plt.plot(X1,Y1, X2, Y2)` / `plt.plot(X1,Y1) ; plt.plot(X2,Y2)` - несколько графиков в одних и тех же осях



### Отображение нескольких координатных осей в одном окне

- `subplot(nrows, ncolsm, index)` - создать координатрую ось (Axes)
  - `nrows`, `ncols` – число строк и столбцов;
  - `index` – индекс текущих координатных осей.

- `f, ax = plt.subplots(nrows, ncolsm)` - заранее создает figure. 
  - nrows, ncols – число строк и столбцов;
  - f - ссылка на фигуру
    - f.set_size_inches(7, 4) - размер 7 x 4 дюймов
    - f.set_facecolor('#eee') - цвет фона (светло-серый)
    - [Остальные методы](https://matplotlib.org/stable/api/figure_api.html)
  - ax - ссылка список координатных осей (ax[0,1], ax[0,2])

- `plt.tight_layout()` - убрать наложение графиков

- `plt.suptitle('Графики')` - задать заголовок фигуры

#### Компоновка графиков с помощью GridSpec

```
from matplotlib.gridspec import GridSpec

ws = [1, 2, 5] # размеры каждого графика (относительно суммарной длины всех ячеек) в виде списков
hs = [2, 0.5]

fig = plt.figure(figsize=(7, 4))
gs = GridSpec(ncols=3, nrows=2, figure=fig, width_ratios=ws, height_ratios=hs) # 3 столбца и 2 строки

ax1 = plt.subplot(gs[0, 0])
ax1.plot(np.arange(0, 5, 0.2))
ax2 = fig.add_subplot(gs[1, 0:2])
ax2.plot(np.random.random(10))
ax3 = fig.add_subplot(gs[:, 2])
ax3.plot(np.random.random(10))
```
![image](https://github.com/user-attachments/assets/ebad4edc-aa94-4a37-bd0a-ed70787b3daf)


-`plt.show()` - передает управление пользователю

