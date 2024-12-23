- Установка `pip install matplotlib`
- Импорт `import matplotlib.pyplot as plt`
- Обновление библиотеки `pip install --upgrade matplotlib`

абцисса - х
ордината - y

`y = np.array([1,2,3,4,5])`


- `matplotlib.use('')` - задать бекэнд (`print(matplotlib.get_backend()`) - получить бекэнд)

![image](https://github.com/user-attachments/assets/5bdd2979-3b4b-4cfd-8b8b-0532b0921017)

`lines = plt.plot(x, y); plt.setp(lines, linestyle='-.')`

### Основные команды

- `plt.figure(figsize=(7,4))` - создать фигуру
- `plt.title('График зависимости признаков х и у', fontsize=18, color='red', alpha=0.6)` - отображение заголовка
- `plt.xlabel()` и `plt.ylabel(rotation=0, fontsize=14, color='red', labelpad=20)` - задать названия осям
- `plt.xticks()` и `plt.yticks(rotation=90)` - принудительно установить свои значения на осях графика.
- `plt.fill_between(x, y, 0.5, where=(y < 0), color='r', alpha=0.5)` - заливка областей графика 
- `plt.style.use('Solarize_Light2')` - стилизация вывода графиков (print(plt.style.available) - все стили)
- `plt.grid(color='green', linestyle='--', linewidth=1)` - добавить сетку
- plt.minorticks_on() - минорная сетка
- `plt.legend()` - вывести легенду
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
- `plt.show()` - передает управление пользователю

### Граничные значения осей и локаторы для расположения меток на них

- `plt.xlim()` и `plt.ylim(0,26)` - применяются для изменения размерности осей графика. Этим функциям передаются два числа 
 начало и конец того диапазона, который мы хотим видеть на нашем графике.
- `ax.set_xlim(xmin=-5, xmax=5)` и `ax.set_xlim(xmin=-5, xmax=5)` - то же, но одну границу можно не указывать
- `set_major_locator()` – управление рисками крупной сетки;
- `set_minor_locator()` – управление рисками мелкой сетки.

```
from matplotlib.ticker import NullLocator

lc = NullLocator() # LinearLocator(5) \ MultipleLocator(base=1) - шаг

ax.grid()
ax.xaxis.set_major_locator(lc) # ax.yaxis.set_major_locator(lc) для оси Y
```

- NullLocator() - убирает ось
- LinearLocator(5) - используется для задания нужного числа меток по выбранной оси графика
- MultipleLocator(base=1) - шаг сетки
- IndexLocator(base, offset) - работает аналогичным образом, что и класс MultipleLocator, но производит отсчет значений рисок не от 0, а от наименьшего значения данных графика.
  - base – шаг изменения между соседними рисками;
  - offset – смещение относительно наименьшего значения.
- FixedLocator([-2, -1, 0, 1, 2, 3]) - устанавливает метки в указанных значениях
- LogLocator(base=2) - Для формирования логарифмических делений по осям.  Его параметр base определяет число, которое будет возводиться в степень
- MaxNLocator() - выполняет самостоятельную разбивку интервала на число рисок не более значения nbins
- +

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


### Настраиваем формат отображения меток у координатных осей

`matplotlib.ticker import NullFormatter`

- `ax.set_xticklabels([])`, `ax.set_yticklabels([])` - можно отключить отображение чисел на осях
- `ax.xaxis.set_major_formatter()` 
  - NullFormatter() - для оси X убрать отображение значенмй осей
  - FormatStrFormatter('y =.2f') - устанавливает формат числовых данных
  - FuncFormatter(formatOy) - формирующий значения на основе заданной функции. Для каждого значения будет вызвана функция, которую мы создадим. Функция принимает 2 обяз. значения (x, pos)
  - ScalarFormatter() - используется по умолчанию. Можно переопределить
  - FixedLocator([-3, -2, -1, 0, 1, 2, 3])) - для каждой риски определяем значение
 
### Делаем логарифмический масштаб у координатных осей

1. Можно переопределить масштаб для оси Y
-  `ax.set_yscale('liner')` - линейный (по умолчанию)
- `ax.set_yscale('log', base=2, subs=[2,9])` - логарифмический (по основанию 10, можно изменить через base=2)
  - `base=2` - изменить основание
  - subs=[2,9] - какие риски отображать
- `ax.set_yscale('symlog', linthresh=2, linscale=5)` - вблизи нуля (в указанных пределах) масштаб линейный, а в остальной области - логарифмический
  - linthresh=2 - определяем где будет линейный (от 2 до 2), а все остальное - логарифмический
  - linscale=5 - линейный масштаб можно растянуть, указав масштаб в дополнительном параметре linscale
2. Вместо plot используем semilogy

`ax.loglog` - применить для оси X и Y одновременно


### Типовое размещение графиков

минорная сетка
```
plt.minorticks_on()

plt.grid(which='major', color = '#444', linewidth = 1)
plt.grid(which='minor', color='#aaa', ls=':')
```

```
fig = plt.figure(figsize=(7, 4), , facecolor='#eee')
ax = fig.add_subplot()
plt.figtext(0.05, 0.6, 'Текст в области окна')
fig.suptitle('Заголовок окна')
ax.set_xlabel('Ox')
ax.set_ylabel('Oy')
 
ax.text(0.05, 0.1, 'Произвольный текст в координатных осях')
ax.annotate('Аннотация', xy=(0.2, 0.4), xytext=(0.6, 0.7),
            arrowprops={'facecolor': 'gray', 'shrink': 0.1})
 
plt.show()
```

#### Оформление текстовых элементов
| Свойство | Описание |
| - | - |
| alpha | степень прозрачности (число в диапазоне [0; 1]) |
| backgroundcolor | цвет фона |
| color или c | цвет текста |
| fontfamily или family | тип шрифта |
| fontsize или size | размер шрифта |
| fontstyle или style | стиль шрифта: {'normal', 'italic', 'oblique'} |
| fontweight или weight | степень утолщения – число от 0 до 1000 или константы: 'ultralight', 'light', 'normal', 'regular', 'book', 'medium', 'roman', 'semibold', 'demibold', 'demi', 'bold', 'heavy', 'extra bold', 'black' |
| horizontalalignment или ha | выравнивание по горизонтали: {'center', 'right', 'left'} |
| label | текст заголовка |
| position | координаты текста (x, y) |
| rotation | поворот текста: вещественное число [0; 1] или константы {'vertical', 'horizontal'} |
| verticalalignment или va | выравнивание по вертикали: {'center', 'top', 'bottom', 'baseline', 'center_baseline'} |
| visible | отображение текста: True/False |
| x | координата x – вещественное число [0; 1] |
| y | координата y – вещественное число [0; 1] |

Так же у текстовых элементов есть параметр bbox {'...':'...', ...} - оформление эллементов


| Свойство | Описание |
| - | - |
| boxstyle | вид рамки вокруг текста |
| alpha | степень прозрачности фона |
| color | цвет фона с рамкой |
| edgecolor или ec | цвет рамки |
| facecolor или fc | цвет заливки |
| fill | использовать ли заливку: True/False |
| hatch | тип штриховки: {'/', '\', '|', '-', '+', 'x', 'o', 'O', '.', '*'} |
| linestyle или ls | стиль линии границы: {'-', '--', '-.', ':', '', (offset, on-offseq), ...} |
| linewidth или lw | толщина рамки |

